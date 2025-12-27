# Chapter 14 - Stream Processing - Test

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 14

**CCDAK Practice Test - 60 Questions**
**Time Limit: 90 minutes**  
**Passing Score: 70%**

[Link to Solutions](../../chapter-tests-solutions/chapter-14-solutions.md) | [Main README](../../README.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

### Question 1

**What is a data stream in stream processing?**

- A) A finite dataset with a fixed size
- B) An abstraction representing an unbounded and ever-growing dataset
- C) A batch of records processed at scheduled intervals
- D) A static database table

### Question 2

**Which attribute is NOT characteristic of event streams?**

- A) Event streams are ordered
- B) Immutable data records
- C) Event streams are replayable
- D) Event streams require immediate processing

### Question 3

**What does Kafka Streams use to expose stream processing functionality?**

- A) A separate server cluster
- B) A client library integrated into applications
- C) A standalone processing engine
- D) A YARN cluster

### Question 4

**What is a topology in stream processing?**

- A) The physical layout of Kafka brokers
- B) A directed acyclic graph of processing operations
- C) The network configuration of consumers
- D) The partition assignment strategy

### Question 5

**Which type of time is typically MOST relevant for stream processing?**

- A) Processing time
- B) Log append time
- C) Event time
- D) System time

### Question 6

**What is the purpose of the StreamsBuilder in Kafka Streams?**

- A) To manage broker connections
- B) To define the processing topology
- C) To configure consumer groups
- D) To handle serialization

### Question 7

**What is stream-table duality?**

- A) Using two separate databases
- B) The concept that streams and tables are two views of the same data
- C) Replicating data between streams
- D) Partitioning strategy for tables

### Question 8

**What does materializing a stream mean?**

- A) Compressing stream data
- B) Converting stream events into a table by applying all changes
- C) Archiving old stream data
- D) Encrypting stream contents

### Question 9

**What is local state in stream processing?**

- A) State stored in a central database
- B) State accessible only by a specific stream processing instance
- C) State replicated across all brokers
- D) Temporary cache that is always lost on restart

### Question 10

**How does Kafka Streams persist local state for recovery?**

- A) Only in memory
- B) In ZooKeeper
- C) In embedded RocksDB and change log topics
- D) In external NoSQL databases only

### Question 11

**What is a windowed join in stream processing?**

- A) Joining data from different windows in time
- B) A join operation limited to events within a specific time window
- C) Joining streams with tables
- D) A join without time constraints

### Question 12

**What is a tumbling window?**

- A) A window that overlaps with adjacent windows
- B) A fixed-size window that moves to completely non-overlapping positions
- C) A window based on event count
- D) A window that never closes

### Question 13

**What is a hopping window?**

- A) A window that randomly selects events
- B) A fixed-size window that moves at regular intervals and may overlap
- C) A window based on session gaps
- D) A window without a defined size

### Question 14

**What is a session window in Kafka Streams?**

- A) A window defined by periods of user activity and inactivity
- B) A fixed 30-minute window
- C) A window for authentication events
- D) A window that spans the entire stream

### Question 15

**What configuration enables exactly-once semantics in Kafka Streams?**

- A) replication.factor=3
- B) processing.guarantee=exactly_once
- C) isolation.level=read_committed
- D) enable.idempotence=true

### Question 16

**What is the map/filter pattern in stream processing?**

- A) Processing each event in isolation with transformations
- B) Aggregating events into summaries
- C) Joining multiple streams
- D) Persisting state to disk

### Question 17

**What is repartitioning in Kafka Streams?**

- A) Changing partition count of a topic
- B) Writing events to a new topic with new keys for redistribution
- C) Rebalancing consumers
- D) Deleting and recreating partitions

### Question 18

**What is change data capture (CD- C)?**

- A) Capturing database changes as a stream of events
- B) Backing up database tables
- C) Replicating data between Kafka clusters
- D) Compressing change logs

### Question 19

**What is a stream-table join used for?**

- A) Joining two unbounded streams
- B) Enriching stream events with table data
- C) Creating materialized views
- D) Aggregating multiple streams

### Question 20

**How does Kafka Streams scale processing?**

- A) By adding more brokers
- B) By creating tasks based on partition count
- C) By increasing replication factor
- D) By using larger messages

### Question 21

**What is a task in Kafka Streams?**

- A) A scheduled batch job
- B) The basic unit of parallelism processing a subset of partitions
- C) A broker operation
- D) A consumer group coordinator

### Question 22

**What does KStream represent in Kafka Streams?**

- A) A changelog stream
- B) An unbounded stream of events
- C) A static lookup table
- D) A compacted topic

### Question 23

**What does KTable represent in Kafka Streams?**

- A) An unbounded event stream
- B) A materialized view updated by a stream
- C) A batch processing table
- D) An external database table

### Question 24

**What is the purpose of a Serde in Kafka Streams?**

- A) To manage consumer offsets
- B) To serialize and deserialize data
- C) To partition data
- D) To compress messages

### Question 25

**What is a grace period in windowed operations?**

- A) The delay before starting processing
- B) Time allowed for late-arriving events to update window results
- C) The window size
- D) Time between window creations

### Question 26

**What is the flatMap operation used for?**

- A) Flattening nested data structures
- B) Transforming each input record into zero or more output records
- C) Compressing data
- D) Joining streams

### Question 27

**What does the groupByKey() operation do?**

- A) Creates new partition assignments
- B) Ensures stream is partitioned by key for aggregations
- C) Sorts events by key
- D) Removes duplicate keys

### Question 28

**What is an equi-join in Kafka Streams?**

- A) A join where both sides have equal data volume
- B) A join where both sides share the same key and partitioning
- C) A join with equal processing time
- D) A join with identical schemas

### Question 29

**How does Kafka Streams handle out-of-sequence events?**

- A) Rejects all late events
- B) Uses event time and grace periods to reconcile late arrivals
- C) Processes only by arrival time
- D) Sorts all events before processing

### Question 30

**What is interactive queries in Kafka Streams?**

- A) SQL-like query interface
- B) Ability to directly query the state store of a running application
- C) Batch query processing
- D) External database queries

### Question 31

**What is the purpose of the APPLICATION_ID_CONFIG in Kafka Streams?**

- A) To identify the application version
- B) To coordinate instances and name internal topics
- C) To set consumer group name
- D) To configure the broker ID

### Question 32

**What does Kafka Streams DSL provide?**

- A) Low-level processor API
- B) High-level declarative stream operations
- C) Database query language
- D) REST API for streams

### Question 33

**What is a foreign-key join?**

- A) Joining with external databases
- B) Joining tables where key of one matches an arbitrary field of another
- C) Joining streams from different clusters
- D) Joining with ZooKeeper data

### Question 34

**How does Kafka Streams handle rebalancing when a task fails?**

- A) Stops all processing
- B) Reassigns the task to an available thread
- C) Requires manual intervention
- D) Drops all pending events

### Question 35

**What is a standby replica in Kafka Streams?**

- A) A backup Kafka broker
- B) A task that maintains warm state for faster failover
- C) An inactive consumer
- D) A read-only topic replica

### Question 36

**What is a subtopology in Kafka Streams?**

- A) A nested topic structure
- B) A portion of topology separated by repartitioning
- C) A secondary processing pipeline
- D) A backup topology

### Question 37

**What does the aggregate() operation require?**

- A) Only input and output topics
- B) An initializer, adder function, and state store configuration
- C) External database connection
- D) Windowing parameters only

### Question 38

**What is the purpose of TopologyTestDriver?**

- A) Performance benchmarking
- B) Unit testing stream processing logic without Kafka brokers
- C) Load balancing topologies
- D) Production deployment tool

### Question 39

**What paradigm does stream processing fill between request-response and batch?**

- A) Immediate millisecond response
- B) Continuous nonblocking processing
- C) Scheduled hourly processing
- D) Manual trigger processing

### Question 40

**What is beaconing in the context of fraud detection?**

- A) Broadcasting alerts
- B) Malware periodically reaching out for commands
- C) Sending heartbeat messages
- D) Load balancing requests

### Question 41

**What does RocksDB provide in Kafka Streams?**

- A) Message compression
- B) Embedded persistent key-value store for local state
- C) Network protocol
- D) Schema registry

### Question 42

**What is the count() operation in Kafka Streams?**

- A) Counts total partitions
- B) Counts records per key in a grouped stream
- C) Counts brokers
- D) Counts bytes transferred

### Question 43

**When should you use stream processing over batch processing?**

- A) When processing can wait 24 hours
- B) When continuous updates are needed faster than batch cycles
- C) When data volume is small
- D) When accuracy is not important

### Question 44

**What is the purpose of the leftJoin() operation?**

- A) Joins only matching records
- B) Includes all records from left side, matching or not
- C) Joins left partitions only
- D) Sorts records to the left

### Question 45

**What determines the number of tasks in a Kafka Streams application?**

- A) Number of application instances
- B) Number of partitions in input topics
- C) Amount of available memory
- D) Number of CPU cores

### Question 46

**What is the purpose of the filter() operation?**

- A) Removes partitions
- B) Selects events matching a predicate condition
- C) Compresses data
- D) Sorts events

### Question 47

**How does Kafka Streams achieve fault tolerance?**

- A) By maintaining state in ZooKeeper
- B) By replicating data to external databases
- C) By storing state in local stores with change logs in Kafka
- D) By using RAID storage

### Question 48

**What is the Processor API in Kafka Streams?**

- A) REST API for remote access
- B) Low-level API for creating custom stream processors
- C) Configuration API
- D) Monitoring API

### Question 49

**What is a common use case for stream processing in IoT?**

- A) Static device inventory
- B) Predictive maintenance by analyzing sensor patterns
- C) One-time configuration
- D) Manual device monitoring

### Question 50

**What does the reduce() operation do?**

- A) Decreases partition count
- B) Combines values for the same key using an associative function
- C) Removes duplicate events
- D) Compresses messages

### Question 51

**What does log compaction ensure for state store topics?**

- A) Only the latest value for each key is retained
- B) All historical values are preserved
- C) Topics are deleted regularly
- D) Messages are sorted by timestamp

### Question 52

**What is the purpose of the toStream() operation on a KTable?**

- A) Compresses the table
- B) Converts table changelog into a stream of updates
- C) Exports to external database
- D) Creates a backup

### Question 53

**How can you run multiple instances of a Kafka Streams application?**

- A) Only on a YARN cluster
- B) Start multiple processes with the same APPLICATION_ID
- C) Requires Kubernetes
- D) Not possible without external coordination

### Question 54

**What is the advantage of using Kafka Streams over other frameworks?**

- A) Requires complex cluster setup
- B) Runs as a simple library in your application
- C) Only works with Hadoop
- D) Requires YARN or Mesos

### Question 55

**What happens to window results when late events arrive within the grace period?**

- A) Events are rejected
- B) Window results are recalculated and updated
- C) Events are logged but ignored
- D) Application crashes

### Question 56

**What is the purpose of the mapValues() operation?**

- A) Changes partition keys
- B) Transforms record values without changing keys
- C) Creates new partitions
- D) Sorts values

### Question 57

**What does the branch() operation do?**

- A) Creates topic branches
- B) Splits a stream into multiple streams based on predicates
- C) Merges streams
- D) Replicates a stream

### Question 58

**What is the TimestampExtractor interface used for?**

- A) System time extraction
- B) Determining event timestamp from record
- C) Broker timestamp configuration
- D) Consumer offset timestamps

### Question 59

**Why is Kafka particularly good for stream processing?**

- A) It only supports batch processing
- B) It provides reliable, replayable, ordered event streams
- C) It requires no configuration
- D) It's faster than memory

### Question 60

**What is the punctuate() method used for in Kafka Streams?**

- A) Formatting output
- B) Scheduling periodic actions independent of input events
- C) Punctuation in text processing
- D) Error handling