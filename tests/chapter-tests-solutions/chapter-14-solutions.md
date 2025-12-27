# Chapter 14 - Stream Processing - Solutions

CCDAK Practice Test Solutions
**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 14

[Back to Test](../../chapter-tests/chapter-14-test.md) | [Main README](../../README.md)

### Answer 1

**B) An abstraction representing an unbounded and ever-growing dataset**

A data stream is defined as an unbounded dataset that is infinite and ever-growing. Over time, new records keep arriving, making the dataset unbounded. This abstraction can represent almost any business activity, from credit card transactions to sensor data to package deliveries.

----

### Answer 2

**D) Event streams require immediate processing**

Event streams do NOT require immediate processing. They are ordered, contain immutable data records, and are replayable, but they don't mandate immediate processing. Stream processing is continuous but non-blocking, filling the gap between millisecond response times and daily batch processing.

----

### Answer 3

**B) A client library integrated into applications**

Kafka Streams is a powerful stream processing library that is part of Kafka's collection of client libraries. It allows developers to consume, process, and produce events in their own applications without relying on an external processing framework or separate server cluster.

----

### Answer 4

**B) A directed acyclic graph of processing operations**

A topology (also called DAG) is a set of operations and transitions that every event moves through from input to output. It consists of processors (nodes in the graph) connected by streams, starting with source processors and finishing with sink processors.

----

### Answer 5

**C) Event time**

Event time is typically the most relevant for stream processing because it represents when events actually occurred. Log append time shows when events arrived at Kafka, and processing time shows when the stream application received the event. Event time is most important for accurate analysis like counting devices produced per day.

----

### Answer 6

**B) To define the processing topology**

StreamsBuilder is used to create a processing topology—a directed acyclic graph (DAG) of transformations applied to events in streams. You define the stream processing application by chaining operations on KStream and KTable objects created from the StreamsBuilder.

----

### Answer 7

**B) The concept that streams and tables are two views of the same data**

Stream-table duality recognizes that streams and tables are two sides of the same coin. A table contains the current state of the world (result of many changes), while a stream contains the history of changes. Systems that allow transitioning between both views are more powerful.

----

### Answer 8

**B) Converting stream events into a table by applying all changes**

Materializing a stream means applying all the changes that the stream contains to create a table. This involves going over all events in the stream from beginning to end, applying inserts, updates, and deletes to create a table representing state at a specific time.

----

### Answer 9

**B) State accessible only by a specific stream processing instance**

Local or internal state is accessible only by a specific instance of the stream processing application. It's usually maintained in an embedded, in-memory database like RocksDB running within the application. The advantage is speed, but it's limited by available memory.

----

### Answer 10

**C) In embedded RocksDB and change log topics**

Kafka Streams persists local state using embedded RocksDB (which persists to disk for recovery) and sends all state changes to Kafka topics with log compaction. If a node fails, the state can be recreated by rereading events from the Kafka change log topic.

----

### Answer 11

**B) A join operation limited to events within a specific time window**

A windowed join (also called streaming join) joins two event streams based on matching keys and events that occur within the same time window. For example, matching search queries with clicks that happen seconds after the query. The join is windowed because we only match events within a specific time period.

----

### Answer 12

**B) A fixed-size window that moves to completely non-overlapping positions**

A tumbling window has a fixed size and moves to completely non-overlapping positions. When the advance interval equals the window size, you get tumbling windows. For example, a 5-minute window that moves every 5 minutes creates non-overlapping time slices.

----

### Answer 13

**B) A fixed-size window that moves at regular intervals and may overlap**

A hopping window is a fixed-size window that advances at regular intervals, potentially creating overlapping windows. For example, a 5-minute window that moves every 1 minute creates overlapping windows where events can appear in multiple window calculations.

----

### Answer 14

**A) A window defined by periods of user activity and inactivity**

A session window is defined by a session gap—a period of inactivity. All events that arrive continuously with gaps smaller than the session gap belong to the same session. A gap in arrivals defines a new session. This is useful for analyzing user sessions on websites.

----

### Answer 15

**B) processing.guarantee=exactly_once**

Setting processing.guarantee to exactly_once enables exactly-once semantics in Kafka Streams. This uses Kafka's transactional producer and idempotent operations to ensure each record is processed exactly once, regardless of failures. Kafka Streams 2.6+ offers exactly_once_beta for better performance.

----

### Answer 16

**A) Processing each event in isolation with transformations**

The map/filter pattern processes each event individually, applying transformations (map) or selecting events (filter). This is the most basic stream processing pattern. Examples include filtering ERROR events to a high-priority stream or converting JSON to Avro. No state maintenance is needed.

----

### Answer 17

**B) Writing events to a new topic with new keys for redistribution**

Repartitioning in Kafka Streams means writing events to a new topic with new keys to redistribute the data. This is needed when you want to aggregate by a different key than the original partitioning. Kafka Streams handles this automatically by creating intermediate topics.

----

### Answer 18

**A) Capturing database changes as a stream of events**

Change Data Capture (CDC) captures all changes (inserts, updates, deletes) that happen to a database table as a stream of events. Many Kafka connectors can perform CDC, allowing you to pipe database changes into Kafka where they become available for stream processing.

----

### Answer 19

**B) Enriching stream events with table data**

A stream-table join enriches streaming events with data from a table. For example, enriching click events with user profile information. The stream provides the events being processed, while the table provides dimension data for enrichment. This is similar to fact-dimension joins in data warehouses.

----

### Answer 20

**B) By creating tasks based on partition count**

Kafka Streams scales by creating tasks based on the number of partitions in input topics. Each task processes a subset of partitions independently. Multiple threads can execute tasks, and multiple application instances can run different tasks. Scalability is directly tied to partition count.

----

### Answer 21

**B) The basic unit of parallelism processing a subset of partitions**

A task is the basic unit of parallelism in Kafka Streams. The Streams engine creates tasks based on the number of partitions, with each task subscribing to a subset of partitions. Tasks execute independently, and multiple threads or instances can run different tasks for horizontal scalability.

----

### Answer 22

**B) An unbounded stream of events**

KStream represents an unbounded stream of events where each record is an independent piece of data. Unlike KTable, KStream doesn't maintain state or represent a changelog—it's a continuous flow of events from producers.

----

### Answer 23

**B) A materialized view updated by a stream**

KTable represents a changelog stream where each record is an update to the previous value with the same key. It's a materialized view that maintains the current state, updated continuously by the underlying stream of changes.

----

### Answer 24

**B) To serialize and deserialize data**

Serde (Serializer/Deserializer) is used to serialize objects when writing to Kafka and deserialize when reading from Kafka. Every object stored in Kafka needs a Serde, including inputs, outputs, and intermediate results. Common implementations include JSON, Avro, and Protobuf Serdes.

----

### Answer 25

**B) Time allowed for late-arriving events to update window results**

Grace period defines how long after a window closes it can still receive and process late-arriving events. For example, with a 5-minute window and 4-hour grace period, events arriving up to 4 hours late can still update the window results.

----

### Answer 26

**B) Transforming each input record into zero or more output records**

flatMap transforms each input record into zero, one, or multiple output records. It's useful for operations like splitting a sentence into words, where one input produces multiple outputs. It "flattens" the resulting collection of records.

----

### Answer 27

**B) Ensures stream is partitioned by key for aggregations**

groupByKey() ensures the stream is correctly partitioned by key, which is required for aggregations. If data is already partitioned by key (hasn't been modified), this operation does nothing but prepares the stream for subsequent group-by operations.

----

### Answer 28

**B) A join where both sides share the same key and partitioning**

An equi-join is where both streams/tables are partitioned by the same key, which is also the join key. This allows efficient distributed joining because matching records are guaranteed to be on the same task, enabling local joins without data shuffling.

----

### Answer 29

**B) Uses event time and grace periods to reconcile late arrivals**

Kafka Streams handles out-of-sequence events by using event time (not processing time) and grace periods. Applications can define how long to keep aggregation windows open for updates, allowing late events to be reconciled and results updated accordingly.

----

### Answer 30

**B) Ability to directly query the state store of a running application**

Interactive queries allow you to directly query the state store of a running Kafka Streams application. Instead of reading results from an output topic, you can query the current state directly, which is faster for table-like results such as top 10 lists.

----

### Answer 31

**B) To coordinate instances and name internal topics**

APPLICATION_ID_CONFIG is unique for each Kafka Streams application and serves multiple purposes: coordinating multiple instances of the application (like a consumer group ID), naming internal topics (changelog and repartition topics), and identifying the application in monitoring systems.

----

### Answer 32

**B) High-level declarative stream operations**

The Kafka Streams DSL (Domain-Specific Language) provides high-level, declarative operations for defining stream processing logic. It allows chaining transformations like map, filter, join, and aggregate without dealing with low-level details. The lower-level Processor API provides more control.

----

### Answer 33

**B) Joining tables where key of one matches an arbitrary field of another**

A foreign-key join allows joining two tables where the key of one table matches an arbitrary field (not the key) of another table. This is more flexible than equi-joins but requires more complex coordination. Kafka Streams added this in recent versions.

----

### Answer 34

**B) Reassigns the task to an available thread**

When a task fails but other instances or threads are available, Kafka Streams automatically reassigns the task to an available thread. This leverages Kafka's consumer group coordination. The task will recover its state from the changelog topic before continuing processing.

----

### Answer 35

**B) A task that maintains warm state for faster failover**

A standby replica is a task that shadows an active task, maintaining a warm copy of the state on a different server. When failover occurs, the standby can take over immediately with current state, dramatically reducing recovery time compared to rebuilding state from changelog topics.

----

### Answer 36

**B) A portion of topology separated by repartitioning**

A subtopology is created when repartitioning splits the topology. Repartitioning writes to an intermediate topic, creating a natural boundary. The first subtopology writes to the repartition topic, and the second subtopology reads from it, allowing independent execution.

----

### Answer 37

**B) An initializer, adder function, and state store configuration**

The aggregate() operation requires: (1) an initializer that creates the initial aggregation object, (2) an adder function that updates the aggregation with each new record, and (3) state store configuration including name and Serde for the aggregation result.

----

### Answer 38

**B) Unit testing stream processing logic without Kafka brokers**

TopologyTestDriver enables unit testing of Kafka Streams applications without running actual Kafka brokers. You provide input data, run the topology with the test driver, and verify output. This makes tests fast, repeatable, and easy to debug.

----

### Answer 39

**B) Continuous nonblocking processing**

Stream processing fills the gap between request-response (millisecond responses) and batch processing (daily cycles). It provides continuous, nonblocking processing where business processes happen continuously and reports are updated continuously without requiring immediate millisecond responses or waiting for daily batches.

----

### Answer 40

**B) Malware periodically reaching out for commands**

Beaconing in fraud detection refers to malware inside an organization periodically reaching out to external servers for commands. Stream processing can detect this by recognizing patterns of communication that are abnormal for that host, enabling early detection before more harm occurs.

----

### Answer 41

**B) Embedded persistent key-value store for local state**

RocksDB is an embedded, persistent key-value store used by Kafka Streams to maintain local state. It stores aggregations, joins, and other stateful operations. RocksDB persists to disk for recovery while keeping frequently accessed data in memory for performance.

----

### Answer 42

**B) Counts records per key in a grouped stream**

The count() operation counts the number of records for each key in a grouped stream. It's typically used after groupByKey() and returns a KTable with the key and count as the value. This is commonly used for aggregations like word count or event counting.

----

### Answer 43

**B) When continuous updates are needed faster than batch cycles**

Use stream processing when you need continuous updates faster than daily batch cycles but don't require millisecond responses. Examples include updating customer service systems with reservations in real-time, IoT predictive maintenance, and fraud detection where timely detection is critical.

----

### Answer 44

**B) Includes all records from left side, matching or not**

A leftJoin() includes all records from the left side of the join, whether they match the right side or not. If there's no match, the right side value is null. This is useful for enrichment where some events might not have matching dimension data.

----

### Answer 45

**B) Number of partitions in input topics**

The number of tasks in a Kafka Streams application is determined by the number of partitions in the input topics. Each task handles a subset of partitions. To increase parallelism, increase the number of partitions in your topics.

----

### Answer 46

**B) Selects events matching a predicate condition**

The filter() operation selects events that match a predicate condition, passing through events where the predicate returns true and dropping others. For example, filtering only ERROR level log events or transactions over a certain amount.

----

### Answer 47

**C) By storing state in local stores with change logs in Kafka**

Kafka Streams achieves fault tolerance by maintaining local state in RocksDB and sending all state changes to compacted Kafka topics (change logs). If an instance fails, another instance can recover the state by replaying the change log, ensuring no data loss.

----

### Answer 48

**B) Low-level API for creating custom stream processors**

The Processor API is the low-level API in Kafka Streams that allows creating custom stream processors with fine-grained control over processing logic, state stores, and timestamps. The DSL is built on top of the Processor API and provides higher-level abstractions.

----

### Answer 49

**B) Predictive maintenance by analyzing sensor patterns**

A common IoT use case for stream processing is predictive maintenance—analyzing patterns from sensors to predict when equipment needs maintenance before failure. This applies to manufacturing, telecommunications, and other industries with connected devices.

----

### Answer 50

**B) Combines values for the same key using an associative function**

The reduce() operation combines all values for the same key using an associative combining function. Unlike aggregate(), reduce() doesn't create a new object—it combines existing values. For example, summing numbers or finding maximum values.

----

### Answer 51

**A) Only the latest value for each key is retained**

Log compaction for state store topics ensures only the latest value for each key is retained. Older values are removed during compaction, keeping topic size manageable while preserving the current state. This makes recovering state from changelog topics efficient.

----

### Answer 52

**B) Converts table changelog into a stream of updates**

The toStream() operation on a KTable converts the table's changelog into a stream of update events. Each change to the table becomes an event in the stream. This is useful when you need to process table updates as a stream of events.

----

### Answer 53

**B) Start multiple processes with the same APPLICATION_ID**

To run multiple instances of a Kafka Streams application, simply start multiple processes (on same or different machines) with the same APPLICATION_ID_CONFIG. Kafka Streams automatically coordinates between instances, distributing tasks across all available instances.

----

### Answer 54

**B) Runs as a simple library in your application**

The main advantage of Kafka Streams is that it runs as a library within your application—no separate cluster setup required. You don't need YARN, Mesos, or Kubernetes. Just include the library, run your app, and you have a distributed stream processing application.

----

### Answer 55

**B) Window results are recalculated and updated**

When late events arrive within the grace period, Kafka Streams recalculates and updates the window results. The updated result is written to the output topic, replacing the previous result. This ensures accurate results even with late-arriving data.

----

### Answer 56

**B) Transforms record values without changing keys**

mapValues() transforms record values without modifying keys. This is more efficient than map() when keys don't change because it avoids triggering repartitioning. Use this for value transformations like data enrichment or format conversion.

----

### Answer 57

**B) Splits a stream into multiple streams based on predicates**

The branch() operation splits one stream into multiple output streams based on a series of predicates. Each predicate is evaluated in order, and the record goes to the first matching branch. This is useful for routing events to different processing paths.

----

### Answer 58

**B) Determining event timestamp from record**

The TimestampExtractor interface determines how to extract the event timestamp from a record. Implementations can use the record's built-in timestamp, extract from record contents, or use other logic. This timestamp is used for window operations and event-time processing.

----

### Answer 59

**B) It provides reliable, replayable, ordered event streams**

Kafka is particularly good for stream processing because it provides reliable, replayable, and ordered event streams stored for long periods. This allows recovering from failures, reprocessing data, and running multiple versions of applications on the same data.

----

### Answer 60

**B) Scheduling periodic actions independent of input events**

The punctuate() method schedules periodic actions that run at specified intervals independent of input events. This is useful for operations like flushing caches, generating periodic reports, or cleaning up expired state, even when no new events arrive.