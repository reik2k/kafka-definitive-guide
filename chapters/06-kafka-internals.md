# Chapter 6: Kafka Internals

## Overview

Understanding Kafka's internals is not strictly necessary to run Kafka in production, but it provides essential context for troubleshooting and understanding Kafka's behavior.

Key topics covered:
- **Kafka controller**: Manages cluster metadata and leader elections
- **Replication**: How Kafka ensures data durability and availability
- **Request processing**: How brokers handle client requests
- **Physical storage**: How Kafka manages data on disk

## Cluster Membership

### ZooKeeper-Based Registration

Kafka uses Apache ZooKeeper to maintain the list of brokers currently in a cluster.

- Each broker has a unique identifier (set in config or auto-generated)
- Brokers register themselves by creating **ephemeral nodes** in ZooKeeper (`/brokers/ids/[id]`)
- The ephemeral node is automatically removed when the broker loses connectivity
- Other components watch this path to be notified of broker additions/removals

### Important Behavior

- If a broker stops, its ephemeral node is removed from ZooKeeper
- If you start a new broker with the same ID as a stopped broker, it immediately joins the cluster with the same partitions
- ZooKeeper handles the replica information separately from the broker registration

## The Controller

### Controller Election

The controller is the broker responsible for electing partition leaders:

- The first broker to start creates an ephemeral node at `/controller`
- Other brokers receive a "node already exists" exception and watch this node
- When the controller disconnects, another broker creates the new controller node
- The cluster always has exactly one controller (guaranteed by ZooKeeper)

### Controller Responsibilities

1. **Leader election**: When brokers join/leave or fail
2. **Managing cluster metadata**: Topics, partitions, replicas
3. **Coordinating state changes**: Replica ISRs, leader/follower changes
4. **Handling shutdowns**: Both graceful and ungraceful

### Controller Epoch

Each controller election increments the **controller epoch**:
- Prevents "zombie" controllers from causing inconsistency
- Brokers ignore messages from controllers with older epochs
- Provides **zombie fencing**

### KRaft: Kafka Raft-Based Controller

Starting in Apache Kafka 2.8 (preview), KRaft replaces ZooKeeper-based controller:

**Why replace ZooKeeper?**
- Metadata updates are asynchronous, creating consistency gaps
- Controller restart requires reading all metadata from ZooKeeper (bottleneck)
- Requires operators to learn two distributed systems
- Doesn't scale well to millions of partitions

**KRaft Architecture:**
- Controller nodes form a Raft quorum
- Active controller handles all RPCs from brokers
- Follower controllers act as hot standbys
- Metadata stored in a log (not ZooKeeper)
- Brokers fetch metadata updates via new `MetadataFetch` API
- Brokers persist metadata to disk (faster startup)
- Fenced brokers cannot serve client requests

## Replication

### Replica Types

**Leader Replica:**
- Only one leader per partition
- All producer requests go through the leader
- Consumers can read from leader or followers
- Responsible for coordinating replication

**Follower Replica:**
- All other replicas for a partition
- Main job: replicate messages from leader
- Stay up-to-date with leader
- Can be elected as new leader if current leader fails

### In-Sync Replicas (ISR)

Followers that consistently request the latest messages from the leader:

- Replicas send `Fetch` requests to the leader (like consumers)
- Leader tracks how far behind each replica is
- Replica is out-of-sync if it hasn't requested messages in > `replica.lag.time.max.ms`
- Out-of-sync replicas cannot become leaders
- Only in-sync replicas are eligible for leader election

### Preferred Leader

- The first replica in the replica list for a partition
- Typically balanced across brokers when topic is created
- `auto.leader.rebalance.enable=true` automatically elects preferred leader
- Important for load balancing across brokers

### High-Water Mark

- Latest committed offset (messages replicated to all ISRs)
- Consumers cannot read messages beyond the high-water mark
- Guarantees consistency: if leader crashes, no consumer loses messages
- Follower reads include high-water mark to maintain safety guarantees

## Request Processing

### Binary Protocol

Kafka uses a binary protocol over TCP:

- Standardized request/response format
- Clients implement protocol in Java, C, Python, Go, etc.
- Clients initiate connections; brokers respond
- Requests from client processed in order received (ordering guarantee)

### Request Header

All requests include:
- **Request type** (API key)
- **Request version** (for compatibility)
- **Correlation ID** (for tracking and troubleshooting)
- **Client ID** (identifies the application)

### Request Processing Pipeline

1. **Acceptor thread** creates connection
2. **Processor thread** (network thread) picks up request
3. Request placed in **request queue**
4. **I/O thread** (request handler) processes request
5. Response placed in **response queue**
6. **Processor thread** sends response to client
7. Delayed responses held in **purgatory** (e.g., when awaiting data)

### Common Request Types

**Produce Requests:**
- Sent by producers with messages to write
- Routed to partition leader
- Response timing depends on `acks` setting

**Fetch Requests:**
- Sent by consumers and follower replicas
- Request offsets and limits
- Routed to partition leader
- Uses **zero-copy** optimization (send directly from filesystem cache)

**Metadata Requests:**
- Clients ask brokers for topic metadata
- Can be sent to any broker (all have metadata cache)
- Clients refresh metadata periodically (`metadata.max.age.ms`)
- Cache refreshed after "Not a Leader" errors

**Admin Requests:**
- Create/delete topics, manage configuration
- Coordinated by controller

### Zero-Copy Optimization

Kafka sends messages directly from filesystem cache (or disk) to network channel:

- Eliminates intermediate buffering
- Removes overhead of copying bytes and managing memory
- Significantly improves performance
- Different from most databases that buffer in local cache first

## Physical Storage

### Partition Storage

- Partitions cannot be split between brokers or even between disks
- Size limited by available space on a single mount point
- Configured via `log.dirs` parameter
- Typical config: one directory per mount point (JBOD or RAID)

### Tiered Storage

**Motivation:**
- Kafka stores large data (high throughput or long retention)
- Local disk is expensive; limits retention and partition counts
- Large partitions make cluster less elastic

**Architecture:**
- **Local tier**: Log segments on broker disks (current Kafka)
- **Remote tier**: External storage (HDFS, S3) for completed segments
- Separate retention policy for each tier
- Local: hours to days; Remote: days to months
- Latency-sensitive apps read from local; backfill reads from remote
- Benefits: infinite storage, lower costs, elasticity, isolation of historical vs real-time reads

### Partition Allocation

When creating a topic with multiple partitions and replicas:

1. **Spread replicas evenly** among brokers
2. **Different brokers** for each replica of a partition
3. **Different racks** for each replica (if rack awareness enabled)

Allocation algorithm:
- Start with random broker
- Assign partition leaders round-robin
- Place followers at increasing offsets from leader
- With rack awareness: use rack-alternating broker list

**Disk allocation:**
- New partitions go to directory with fewest partitions
- Balances partitions across disks (not considering size)

### File Management and Retention

**Retention policies:**
- Time-based: delete messages older than retention period
- Size-based: delete oldest messages when size limit reached
- Compaction: keep only latest value per key
- Delete and compact: combination with time-based deletion

**Segment concept:**
- Each partition split into segments (default: 1 GB or 7 days)
- Active segment never deleted
- Old segments deleted when retention policy triggered
- Allows efficient management of data

### File Format

**Message structure (v2):**
- Batch headers include offset, timestamp, size, checksum
- Record headers include size, offset difference, timestamp difference
- User payload: key, value, optional headers
- Very efficient: offset/timestamp stored as batch level with per-record deltas
- Reduces overhead per record when batching

**Batch details:**
- Magic number (version)
- First offset and last offset difference
- Timestamps (first and highest)
- Compression type
- Attributes (transaction, control batch, etc.)
- Producer ID and sequence for exactly-once semantics
- Messages in the batch

### Indexes

Kafka maintains two indexes per partition:

1. **Offset Index**: Maps offsets to segment file positions
   - Allows quick location of messages for any offset
   - Automatically regenerated if corrupted

2. **Timestamp Index**: Maps timestamps to offsets
   - Used when searching by timestamp
   - Useful for Kafka Streams and failover scenarios

### Log Compaction

**Use cases:**
- Storing customer shipping addresses (latest only)
- Application state snapshots (only latest state matters)
- Alternative to time-based retention

**How it works:**

1. **Clean vs Dirty sections:**
   - Clean: Already compacted (one value per key)
   - Dirty: New messages since last compaction

2. **Compaction process:**
   - Cleaner thread reads dirty section
   - Creates in-memory map of key hashes to offsets (24 bytes per entry)
   - Efficiently handles large segments (1 GB ≈ 24 MB map for 1 KB messages)
   - Reads clean segments, skips messages with keys that have newer values
   - Swaps old segment with compacted segment

3. **Memory efficiency:**
   - Only 24 bytes per map entry (16-byte key hash + 8-byte offset)
   - Configurable memory limit for offset maps
   - Must fit at least one full segment

4. **Compaction triggers:**
   - Default: when 50% of topic contains dirty records
   - Configurable with `log.cleaner.enable=true`
   - Multiple cleaner threads pick highest dirty ratio partition

5. **Compaction timing:**
   - `min.compaction.lag.ms`: minimum time before message eligible
   - `max.compaction.lag.ms`: maximum delay before compaction
   - Useful for GDPR compliance (e.g., delete within 30 days)

### Deleted Events (Tombstones)

To delete a key from a compacted topic:

1. Produce message with **key** and **null value** (tombstone)
2. Cleaner thread retains tombstone for configurable time
3. Consumers see tombstone and know value is deleted
4. After time expires, cleaner removes tombstone
5. Important: give consumers time to see tombstone

**Alternative delete method:**
- `AdminClient.deleteRecords()` moves low-water mark
- Makes records inaccessible but doesn't delete them
- Works on both retention and compacted topics

## Summary

Understanding Kafka internals is crucial for:
- Troubleshooting issues
- Tuning configuration parameters effectively
- Designing reliable Kafka applications
- Operating Kafka clusters in production

Key concepts:
- **Controller** manages cluster state and leader elections
- **Replication** ensures durability through in-sync replicas
- **Request processing** is optimized for throughput (zero-copy, batching)
- **Storage** is segment-based with efficient indexes
- **Log compaction** enables long-term state management
