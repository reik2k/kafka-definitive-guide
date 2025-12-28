# Chapter 14: Stream Processing

## TABLE OF CONTENTS

- [What Is Stream Processing?](#what-is-stream-processing)
- [Stream Processing Concepts](#stream-processing-concepts)
  - [Topology](#topology)
  - [Time](#time)
  - [State](#state)
  - [Stream-Table Duality](#stream-table-duality)
  - [Time Windows](#time-windows)
  - [Processing Guarantees](#processing-guarantees)
- [Stream Processing Design Patterns](#stream-processing-design-patterns)
  - [Single-Event Processing](#single-event-processing)
  - [Processing with Local State](#processing-with-local-state)
  - [Multiphase Processing/Repartitioning](#multiphase-processing-repartitioning)
  - [Processing with External Lookup: Stream-Table Join](#processing-with-external-lookup-stream-table-join)
  - [Table-Table Join](#table-table-join)
  - [Streaming Join](#streaming-join)
  - [Out-of-Sequence Events](#out-of-sequence-events)
  - [Reprocessing](#reprocessing)
  - [Interactive Queries](#interactive-queries)
- [Kafka Streams by Example](#kafka-streams-by-example)
  - [Word Count](#word-count)
  - [Stock Market Statistics](#stock-market-statistics)
  - [ClickStream Enrichment](#clickstream-enrichment)
- [Kafka Streams: Architecture Overview](#kafka-streams-architecture-overview)
  - [Building a Topology](#building-a-topology)
  - [Optimizing a Topology](#optimizing-a-topology)
  - [Testing a Topology](#testing-a-topology)
  - [Scaling a Topology](#scaling-a-topology)
  - [Surviving Failures](#surviving-failures)
- [Stream Processing Use Cases](#stream-processing-use-cases)
- [How to Choose a Stream Processing Framework](#how-to-choose-a-stream-processing-framework)
- [Summary](#summary)

## What Is Stream Processing?

Kafka was traditionally seen as a powerful message bus, capable of delivering streams of events but without processing or transformation capabilities. Starting from version 0.10.0, Kafka includes a powerful stream processing library as part of its collection of client libraries, called **Kafka Streams**.

A data stream (or event stream) is an abstraction representing an **unbounded dataset**. Unbounded means infinite and ever growing—new records keep arriving over time.

**Key attributes of event streams:**

- **Event streams are ordered**: There is an inherent notion of which events occur before or after other events
- **Immutable data records**: Events, once occurred, can never be modified
- **Event streams are replayable**: Critical ability to replay a raw stream of events that occurred months or years earlier

**Stream processing** refers to the ongoing processing of one or more event streams. It is a programming paradigm that fills the gap between:

- **Request-response**: Lowest latency (submilliseconds to milliseconds), blocking
- **Batch processing**: High latency/high throughput (minutes to hours), scheduled
- **Stream processing**: Continuous and nonblocking, processing happens continuously

## Stream Processing Concepts

### Topology

A stream processing application includes one or more processing topologies. A processing topology is a directed acyclic graph (DAG) of processors connected by event streams, starting with source processors and ending with sink processors.

### Time

Stream processing systems typically refer to three notions of time:

- **Event time**: The time the events occurred and the record was created
- **Log append time**: The time the event arrived at the Kafka broker (ingestion time)
- **Processing time**: The time at which a stream processing application received the event

### State

Stream processing becomes interesting when operations involve multiple events. State refers to information maintained across events:

- **Local or internal state**: Accessible only by a specific instance, maintained in embedded in-memory database
- **External state**: Maintained in external data store like Cassandra, accessible from multiple instances

### Stream-Table Duality

Streams and tables are two sides of the same coin:

- **Table to stream**: Capture changes that modify the table using change data capture (CDC)
- **Stream to table**: Apply all changes from the stream to materialize the current state

### Time Windows

Most operations on streams are windowed operations on slices of time:

- **Size of the window**: How long the window extends (5 minutes, 15 minutes, etc.)
- **Advance interval**: How often the window moves (hopping vs tumbling windows)
- **Grace period**: How long the window remains updatable for late arrivals

### Processing Guarantees

Kafka Streams uses Kafka's transactions to implement exactly-once guarantees. Enable by setting `processing.guarantee` to `exactly_once` or `exactly_once_beta` (for Kafka 2.5+).

## Stream Processing Design Patterns

### Single-Event Processing

The most basic pattern processes each event in isolation (map/filter pattern). No state maintenance needed, making recovery and load-balancing simple.

### Processing with Local State

Window aggregations require maintaining state. Kafka Streams:

- Stores state in-memory using embedded RocksDB
- Persists state to disk for quick recovery
- Sends all changes to a Kafka topic for recreation if needed

### Multiphase Processing/Repartitioning

When results require all available information, use a two-phase approach:

1. Calculate with local state
2. Repartition by writing to new topic with new keys
3. Second set of tasks processes repartitioned data

### Processing with External Lookup: Stream-Table Join

Enrich stream events with external data:

- Use CDC to capture database changes as stream
- Maintain local copy of table
- Update cache based on database change events
- Perform lookups on local state

### Table-Table Join

Joining two tables is always nonwindowed, joining current state of both tables. Kafka Streams supports equi-join and foreign-key join.

### Streaming Join

Join two real event streams with windowed join:

- Match events based on same key and time window
- Example: Match search queries with clicked results within seconds
- Kafka Streams maintains join window in RocksDB state store

### Out-of-Sequence Events

Handling events arriving out of order:

- Recognize events are out of sequence by examining event time
- Define reconciliation time period
- Maintain multiple aggregation windows for updates
- Update results when late events arrive

### Reprocessing

Two reprocessing variants:

1. Run improved version alongside old version, compare results
2. Fix bugs and reprocess from beginning

### Interactive Queries

Kafka Streams provides APIs for querying the state of applications directly, useful for reading results from state store instead of output topic.

## Kafka Streams by Example

### Word Count

Classic stream processing example demonstrating:

- Creating `StreamsBuilder` and defining topology
- Reading from source topic
- Splitting text into words with `flatMapValues()`
- Filtering unwanted words
- Grouping by key with `groupByKey()`
- Counting with `count()`
- Writing results to output topic

Configuration requirements:
- `APPLICATION_ID_CONFIG`: Unique ID for coordination
- `BOOTSTRAP_SERVERS_CONFIG`: Kafka cluster location
- `DEFAULT_KEY_SERDE_CLASS_CONFIG` and `DEFAULT_VALUE_SERDE_CLASS_CONFIG`: Serialization

### Stock Market Statistics

Demonstrates windowed aggregations:

- Calculate minimum ask price per 5-second window
- Count trades per window
- Calculate average ask price
- Uses custom Serde for Trade objects
- Implements `TimeWindows` with 5-second windows advancing every second
- Maintains state in RocksDB store
- Materializes results and writes to output topic

### ClickStream Enrichment

Illustrates streaming joins:

- **Stream-table join**: Enrich clicks with user profile data
- **Stream-stream join**: Join clicks with searches within time window
- Creates `KTable` for user profiles (materialized table)
- Creates `KStream` for page views and searches
- Uses `leftJoin()` with join methods to combine data
- Defines join window of 1 second after search
- Results include user profile, page viewed, and search terms

## Kafka Streams: Architecture Overview

### Building a Topology

Every streams application implements one topology (DAG):

- **Source processors**: Consume data from topics
- **Stream processors**: Transform events (filter, map, aggregate, etc.)
- **Sink processors**: Produce data to topics

### Optimizing a Topology

Three-step execution process:

1. Define logical topology with DSL operations
2. `StreamsBuilder.build()` generates physical topology
3. `KafkaStreams.start()` executes topology

Enable optimization by setting `StreamsConfig.TOPOLOGY_OPTIMIZATION` to `StreamsConfig.OPTIMIZE`.

### Testing a Topology

Testing tools:

- **TopologyTestDriver**: Unit tests with mock input/output topics
- **EmbeddedKafkaCluster**: Integration tests with JVM-embedded brokers
- **Testcontainers**: Integration tests with Docker containers (recommended)

### Scaling a Topology

Kafka Streams scales through:

- **Tasks**: Basic unit of parallelism, one per input partition
- **Threads**: Multiple threads per application instance
- **Instances**: Multiple instances across servers
- Automatic coordination and work distribution
- Tasks process partitions independently

### Surviving Failures

High availability through:

- Kafka's high availability for data persistence
- Consumer coordination for task reassignment
- Static group membership and cooperative rebalancing
- Exactly-once semantics
- **Standby replicas**: Shadow active tasks on different servers for faster recovery
- Aggressive compaction configuration for state recovery

## Stream Processing Use Cases

### Customer Service

Near real-time updates across all systems when events occur:

- Immediate reservation confirmations
- Real-time customer service access to all customer data
- Instant credit card processing and receipts
- Cross-system synchronization within seconds/minutes

### Internet of Things

Predictive maintenance through sensor data:

- Identify patterns signaling device maintenance needs
- Manufacturing quality control
- Telecommunications (faulty towers)
- Cable TV (faulty set-top boxes)
- Process events from devices at large scale

### Fraud Detection

Anomaly detection for various scenarios:

- Credit card fraud
- Stock trading fraud
- Video game cheaters
- Cybersecurity risks (beaconing detection)
- Near real-time response to catch fraud early
- Pattern recognition in large-scale event streams

## How to Choose a Stream Processing Framework

Consider the application type:

### Application Types

**Ingest**: Getting data from one system to another
- Consider Kafka Connect vs stream processing
- Need good connector selection

**Low milliseconds actions**: Near-immediate response required
- Event-by-event low-latency model
- Avoid microbatch-focused systems

**Asynchronous microservices**: Simple actions in larger business process
- Good message bus integration
- Change capture capabilities
- Local store support for caching

**Near real-time data analytics**: Complex aggregations and joins
- Advanced aggregation support
- Window operations
- Multiple join types
- Custom aggregation APIs

### Global Considerations

**Operability**:
- Easy deployment to production
- Monitoring and troubleshooting capabilities
- Scaling up/down flexibility
- Infrastructure integration
- Data reprocessing capabilities

**Usability**:
- API ease of use
- Development time efficiency
- Debugging capabilities

**Abstractions**:
- Clean APIs for complex operations
- Framework handling of scale and recovery details
- Minimal exposure of implementation complexity

**Community**:
- Active open source community
- Regular feature releases
- Bug fix responsiveness
- Documentation and support

## Summary

This chapter covered:

- **Definition of stream processing**: Continuous, nonblocking processing of unbounded datasets
- **Key concepts**: Topology, time semantics, state management, stream-table duality, windowing, exactly-once guarantees
- **Design patterns**: Single-event processing, local state, repartitioning, stream-table joins, table-table joins, streaming joins, out-of-sequence events, reprocessing, interactive queries
- **Kafka Streams examples**: Word count, stock market statistics, clickstream enrichment
- **Architecture overview**: Building, optimizing, testing, scaling topologies, and handling failures
- **Use cases**: Customer service, IoT, fraud detection
- **Framework selection**: Considerations for choosing appropriate stream processing framework

Stream processing fills the crucial gap between request-response and batch processing, enabling continuous analysis and action on event streams.

## External Resources

- [Making Sense of Stream Processing](https://oreil.ly/omhmK)
- [Streaming Systems](https://oreil.ly/vcBBF)
- [Flow Architectures](https://oreil.ly/ajOTG)
- [Mastering Kafka Streams and ksqlDB](https://oreil.ly/5Ijpx)
- [Kafka Streams in Action](https://oreil.ly/TfUxs)
- [Event Streaming with Kafka Streams and ksqlDB](https://oreil.ly/EK06e)
- [Stream Processing with Apache Flink](https://oreil.ly/ransF)
- [Stream Processing with Apache Spark](https://oreil.ly/B0ODf)
- [Kafka Streams Developer Guide](https://oreil.ly/bQ5nE)
- [Beyond the DSL Presentation](https://oreil.ly/4vson)
- [Word Count Example on GitHub](http://bit.ly/2ri00gj)
- [Stock Statistics Example on GitHub](http://bit.ly/2r6BLm1)
- [ClickStream Example on GitHub](http://bit.ly/2sq096i)
- [Testing Kafka Streams - A Deep Dive](https://oreil.ly/RvTIA)
- [Crossing the Streams - Kafka Summit 2020](https://oreil.ly/f34U6)
- [Foreign-Key Joins Blog Post](https://oreil.ly/hlKNz)
- [Kafka Streams Scalability and High Availability Blog](https://oreil.ly/mj9Ca)
- [Kafka Streams Scalability Talk](https://oreil.ly/cUvKa)
