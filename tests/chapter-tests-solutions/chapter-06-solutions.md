# Chapter 6: Kafka Internals — Solutions

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 6

[Back to Test](../../chapter-tests/chapter-06-test.md) | [Main README](../../README.md)

---

## Answer Key

### Question 1: C) Apache ZooKeeper
**Explanation:** Kafka uses Apache ZooKeeper to maintain the list of brokers that are currently members of a cluster.

### Question 2: B) Ephemeral node
**Explanation:** Every time a broker starts, it registers itself with its ID in ZooKeeper by creating an ephemeral node.

### Question 3: B) The ephemeral node is automatically removed
**Explanation:** When a broker loses connectivity to ZooKeeper, the ephemeral node created when starting is automatically removed, and watching components are notified.

### Question 4: B) The first broker that starts in the cluster
**Explanation:** The first broker that starts in the cluster becomes the controller by creating an ephemeral node in ZooKeeper called /controller.

### Question 5: B) Electing partition leaders
**Explanation:** The controller is responsible for electing partition leaders in addition to usual broker functionality.

### Question 6: B) By creating an ephemeral node called /controller
**Explanation:** The controller creates an ephemeral node in ZooKeeper called /controller. Other brokers trying to create this node receive a "node already exists" exception.

### Question 7: B) They receive a "node already exists" exception
**Explanation:** When other brokers try to create the controller node, they receive a "node already exists" exception, indicating a controller already exists.

### Question 8: B) To prevent split-brain scenarios with zombie controllers
**Explanation:** The controller epoch allows brokers to ignore messages from old controllers (zombies), preventing split-brain scenarios.

### Question 9: B) When the current controller loses connectivity to ZooKeeper
**Explanation:** A new controller is elected when the current controller loses connectivity to ZooKeeper and its ephemeral node disappears.

### Question 10: B) Kafka's new Raft-based controller replacing ZooKeeper
**Explanation:** KRaft is Kafka's new Raft-based controller quorum designed to replace ZooKeeper dependencies.

### Question 11: C) Leader and Follower
**Explanation:** The two types of replicas are leader replica and follower replica.

### Question 12: C) The leader replica
**Explanation:** All produce requests go through the leader replica to guarantee consistency.

### Question 13: B) To replicate messages from the leader
**Explanation:** The main job of follower replicas is to replicate messages from the leader and stay up-to-date with the most recent messages.

### Question 14: C) When configured with client.rack and appropriate broker settings
**Explanation:** Consumers can read from follower replicas when configured with client.rack and broker settings like RackAwareReplicaSelector.

### Question 15: B) KIP-392
**Explanation:** KIP-392 added the ability to read from follower replicas to decrease network traffic costs.

### Question 16: B) By sending Fetch requests
**Explanation:** Followers stay in sync by sending Fetch requests to the leader, the same type of requests consumers use.

### Question 17: C) Whether it has requested messages recently and is caught up
**Explanation:** A replica is in-sync if it has requested messages recently and is caught up to the leader's messages.

### Question 18: B) replica.lag.time.max.ms
**Explanation:** replica.lag.time.max.ms controls how long a follower can be inactive or behind before being considered out of sync.

### Question 19: B) 10 seconds
**Explanation:** The default value for replica.lag.time.max.ms is 10 seconds.

### Question 20: B) The replica that was leader when the topic was created
**Explanation:** The preferred leader is the replica that was the leader when the topic was originally created, ensuring balanced load.

### Question 21: B) auto.leader.rebalance.enable
**Explanation:** auto.leader.rebalance.enable=true enables automatic preferred leader rebalancing.

### Question 22: C) Binary protocol over TCP
**Explanation:** Kafka has a binary protocol over TCP that specifies request formats and broker responses.

### Question 23: C) In the order they were received
**Explanation:** All requests sent to the broker are processed in the order they were received, providing ordering guarantees.

### Question 24: B) Metadata, Produce, Fetch
**Explanation:** The most common client request types are Metadata (for discovering topology), Produce (writing), and Fetch (reading).

### Question 25: B) Send a metadata request to discover partition leaders
**Explanation:** Clients send metadata requests to discover which partitions exist and which brokers are leaders before sending produce/fetch requests.

### Question 26: B) NotLeaderForPartitionException
**Explanation:** If a produce request is sent to a non-leader broker, the client receives a "Not a Leader for Partition" error.

### Question 27: C) Controlled by metadata.max.age.ms
**Explanation:** Metadata refresh intervals are controlled by the metadata.max.age.ms configuration parameter.

### Question 28: B) Wait for just the leader to acknowledge
**Explanation:** acks=1 means the broker responds after the leader writes the message to local disk.

### Question 29: C) Wait for all in-sync replicas
**Explanation:** acks=all means waiting for all in-sync replicas to acknowledge receipt before responding.

### Question 30: C) Purgatory
**Explanation:** Requests waiting for replication are stored in purgatory until the leader observes follower replication.

### Question 31: B) Sending messages from broker to consumers
**Explanation:** Zero-copy sends messages from the file/filesystem cache directly to the network channel without intermediate buffers.

### Question 32: B) To reduce CPU and network utilization on low-traffic topics
**Explanation:** Setting a lower boundary prevents clients from repeatedly requesting and getting few/no messages on low-traffic topics.

### Question 33: B) Only messages replicated to all in-sync replicas
**Explanation:** Only messages written to all in-sync replicas are available for clients to read (follower replicas are exempt).

### Question 34: B) The offset of the last message replicated to all in-sync replicas
**Explanation:** The high-water mark is the offset of the last message that was written to all in-sync replicas.

### Question 35: B) A cache storing partition lists to minimize metadata overhead
**Explanation:** Fetch session cache stores partition lists consumers are reading from, minimizing metadata overhead.

### Question 36: C) 61
**Explanation:** The Kafka protocol currently handles 61 different request types (and continues to evolve).

### Question 37: C) Partition replica
**Explanation:** The basic storage unit of Kafka is a partition replica, which cannot be split between brokers or disks.

### Question 38: B) log.dirs
**Explanation:** log.dirs parameter defines the list of directories where partitions will be stored.

### Question 39: B) Configuring local and remote storage tiers
**Explanation:** Tiered storage configures Kafka with local tier (broker disks) and remote tier (HDFS/S3) for different retention.

### Question 40: B) Local and Remote
**Explanation:** Tiered storage has local tier (broker disks) and remote tier (dedicated storage systems).

### Question 41: B) Completed log segments
**Explanation:** The remote tier stores completed log segments, while active segments remain in local tier.

### Question 42: C) Scaling storage independent of memory and CPU
**Explanation:** Tiered storage allows scaling storage independently from memory and CPU, enabling Kafka as long-term storage.

### Question 43: C) Round-robin with rack awareness
**Explanation:** Partitions are allocated using round-robin distribution with rack awareness to ensure availability during rack failures.

### Question 44: C) Directory with fewest partitions
**Explanation:** New partitions are added to the directory with the fewest partitions, balancing partition distribution.

### Question 45: A) Size or time limit
**Explanation:** Segments are split when they reach either 1 GB of data or a week of data, whichever comes first.

### Question 46: B) 1 GB
**Explanation:** The default segment size is 1 GB (or one week of data, whichever is smaller).

### Question 47: A) The segment being written to
**Explanation:** The active segment is the segment currently being written to; it is never deleted.

### Question 48: B) No, never
**Explanation:** Active segments are never deleted, even if retention period is exceeded. Only closed segments can be deleted.

### Question 49: C) v2
**Explanation:** Message format v2 was introduced in Kafka 0.11 and is the current format.

### Question 50: B) Better compression and reduced overhead
**Explanation:** Batching provides better compression (when enabled) and dramatically reduces per-message overhead.

### Question 51: C) DumpLogSegment
**Explanation:** DumpLogSegment tool allows examining partition segments in the filesystem.

### Question 52: B) Offset-to-file and Timestamp-to-offset
**Explanation:** Kafka maintains offset index (maps offsets to segment files/positions) and timestamp index (maps timestamps to offsets).

### Question 53: B) It gets regenerated from the log segment
**Explanation:** If an index becomes corrupted, it is regenerated from the matching log segment by rereading messages.

### Question 54: B) Delete and Compact
**Explanation:** The two retention policies are delete (removes old messages) and compact (keeps latest value per key).

### Question 55: C) The most recent value for each key
**Explanation:** Log compaction retains only the most recent value for each key in the topic.

### Question 56: B) Clean and Dirty
**Explanation:** Compacted logs have clean portion (already compacted) and dirty portion (written after last compaction).

### Question 57: A) A message with a null value used to delete a key
**Explanation:** A tombstone is a message with a key and null value, used to completely delete a key from a compacted topic.

### Question 58: B) 50%
**Explanation:** By default, compaction starts when 50% of the topic contains dirty records.

### Question 59: B) min.compaction.lag.ms
**Explanation:** min.compaction.lag.ms guarantees the minimum length of time before a message can be compacted.

### Question 60: B) They are completely removed
**Explanation:** In KRaft, ZooKeeper dependencies are completely removed; Kafka manages its own metadata using Raft consensus.

---

## Study Tips

### Key Concepts to Master:
1. **Cluster Membership:** ZooKeeper ephemeral nodes, broker registration
2. **Controller:** Election, epoch numbers, zombie fencing, KRaft migration
3. **Replication:** Leader/follower roles, in-sync replicas, preferred leaders
4. **Request Processing:** Metadata, Produce, Fetch requests; purgatory; zero-copy
5. **Storage:** Segments, indexes, tiered storage, partition allocation
6. **Compaction:** Clean/dirty portions, tombstones, compaction triggers

### Related CCDAK Topics:
- Kafka cluster architecture and controller role
- Replication mechanics and ISR management
- Request routing and metadata discovery
- Storage layout and segment management
- Log compaction for stateful applications
- Performance optimizations (zero-copy, batching)

---

[Back to Test](../../chapter-tests/chapter-06-test.md) | [Main README](../../README.md)