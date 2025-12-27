# Chapter 09 – Building Data Pipelines – CCDAK Practice Test

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 9

**CCDAK Practice Test - 60 Questions**
**Time Limit: 90 minutes**  
**Passing Score: 70%**

[Link to Solutions](../../chapter-tests-solutions/chapter-09-solutions.md) | [Main README](../../README.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

### Question 1

**What are the two main use cases for building data pipelines with Apache Kafka?**


- A. Real-time analytics and batch processing
- B. Kafka as one of two endpoints and Kafka as an intermediary between systems
- C. Stream processing and database replication
- D. Message queuing and event sourcing

---

### Question 2

**What is the main value Kafka provides to data pipelines?**


- A. Built-in data transformation
- B. Ability to serve as a very large, reliable buffer between pipeline stages
- C. Automatic schema management
- D. Machine learning capabilities

---

### Question 3

**How does Kafka help decouple producers and consumers in a pipeline?**


- A. By requiring identical timeliness requirements
- B. By allowing different timeliness and availability requirements
- C. By synchronizing all operations
- D. By enforcing strict ordering

---

### Question 4

**What delivery guarantee can Kafka provide on its own?**


- A. Exactly-once only
- B. At-most-once only
- C. At-least-once
- D. No guarantees

---

### Question 5

**When can Kafka pipelines achieve exactly-once delivery?**


- A. Never possible
- B. When combined with external stores that have transactional models or unique keys
- C. Always by default
- D. Only with single partitions

---

### Question 6

**How does Kafka handle varying throughput in pipelines?**


- A. Rejects excess messages
- B. Uses Kafka as buffer allowing producers and consumers to work independently
- C. Requires manual scaling only
- D. Automatically reduces producer rate

---

### Question 7

**Which data formats does Kafka and Connect API support?**


- A. Only JSON
- B. Only Avro
- C. Completely agnostic to data formats
- D. Only primitive types

---

### Question 8

**What does ETL stand for?**


- A. Execute-Transfer-Load
- B. Extract-Transform-Load
- C. Evaluate-Test-Launch
- D. Export-Transform-Link

---

### Question 9

**What is the main drawback of ETL approach?**


- A. Too slow
- B. Transformations may limit downstream applications' access to data
- C. Requires too much storage
- D. Only works with one source

---

### Question 10

**What does ELT stand for?**


- A. Execute-Load-Test
- B. Extract-Load-Transform
- C. Evaluate-Link-Transfer
- D. Export-Launch-Track

---

### Question 11

**What is a Single Message Transformation (SMT) in Kafka Connect?**


- A. Complex aggregations
- B. Simple transformations on records while copying
- C. Multi-record joins
- D. Schema migrations

---

### Question 12

**Which framework handles complex transformations with joins and aggregations?**


- A. Kafka Connect SMTs
- B. Kafka Streams
- C. Plain consumers
- D. Kafka brokers

---

### Question 13

**What authentication method does Kafka support?**


- A. OAuth2 only
- B. SASL
- C. Kerberos only
- D. No authentication

---

### Question 14

**Where is it recommended to store connector credentials?**


- A. Configuration files
- B. Source code
- C. External secret management system like HashiCorp Vault
- D. Environment variables only

---

### Question 15

**How can Kafka help with failure recovery in pipelines?**


- A. Automatic rollback
- B. Can store events for long periods allowing replay
- C. Immediate error correction
- D. Manual intervention only

---

### Question 16

**What is the risk of building ad hoc pipelines for each system pair?**


- A. Higher performance
- B. Creates complex, expensive-to-maintain integration mess
- C. Better security
- D. Simpler architecture

---

### Question 17

**What happens when schema metadata is lost in pipelines?**


- A. Better performance
- B. Tight coupling between source and destination software
- C. Automatic evolution
- D. Improved flexibility

---

### Question 18

**When should you use Kafka client APIs (Producer/Consumer)?**


- A. Never
- B. When you can modify application code and want to push/pull data
- C. Only for testing
- D. Only for monitoring

---

### Question 19

**When should you use Kafka Connect?**


- A. For datastores you didn't write and whose code you can't modify
- B. Only for small data
- C. Only for development
- D. Never in production

---

### Question 20

**What advantages does Kafka Connect provide over writing custom apps?**


- A. Only REST API
- B. Configuration management, offset storage, parallelization, error handling, standard management
- C. Only documentation
- D. No real advantages

---

### Question 21

**What is a Kafka Connect worker?**


- A. A broker process
- B. Container process that executes connectors and tasks
- C. A consumer group
- D. A topic partition

---

### Question 22

**How do Kafka Connect workers handle worker failures?**


- A. Manual restart required
- B. Automatically reassign connectors and tasks to remaining workers
- C. Data is lost
- D. System shutdown

---

### Question 23

**What does a Source connector do?**


- A. Writes data from Kafka to external systems
- B. Reads data from external systems into Kafka
- C. Monitors broker health
- D. Manages topics

---

### Question 24

**What does a Sink connector do?**


- A. Reads from external systems
- B. Writes data from Kafka to external systems
- C. Creates topics
- D. Compresses data

---

### Question 25

**Which modes does Kafka Connect support?**


- A. Single mode only
- B. Standalone and Distributed
- C. Master and Slave
- D. Primary and Secondary

---

### Question 26

**What is the advantage of Distributed mode?**


- A. Simpler configuration only
- B. Fault tolerance, scalability, and automatic rebalancing
- C. Lower latency only
- D. Less memory usage

---

### Question 27

**Which internal topic stores connector configurations?**


- A. `__consumer_offsets`
- B. `connect-configs` (or config.storage.topic)
- C. `__transaction_state`
- D. `connect-status`

---

### Question 28

**What configuration specifies where to find connector plug-ins?**


- A. `connector.path`
- B. `plugin.path`
- C. `lib.path`
- D. `classpath`

---

### Question 29

**What do converters do in Kafka Connect?**


- A. Convert topic names
- B. Convert between Connect's data format and the format stored in Kafka
- C. Convert broker addresses
- D. Convert partition numbers

---

### Question 30

**Which converters are available?**


- A. Only JSON
- B. JSON, Avro, Protobuf, and JSON Schema
- C. Only Avro
- D. Only String

---

### Question 31

**What are the three responsibilities of a Connector?**


- A. Read data, write data, transform data
- B. Determine task count, split work between tasks, pass configurations to tasks
- C. Monitor brokers, create topics, manage partitions
- D. Validate schemas, compress data, encrypt messages

---

### Question 32

**What are Tasks responsible for?**


- A. Configuration management
- B. Getting data in and out of Kafka
- C. Monitoring workers
- D. Managing schemas

---

### Question 33

**How does Kafka Connect handle offset storage for source connectors?**


- A. Manual management required
- B. Workers automatically store offsets in internal Kafka topic
- C. Stored in ZooKeeper
- D. Not stored

---

### Question 34

**What configuration controls maximum tasks for a connector?**


- A. `max.tasks`
- B. `tasks.max`
- C. `num.tasks`
- D. `task.count`

---

### Question 35

**How do you create a connector?**


- A. Edit broker configuration
- B. Use REST API to POST connector configuration
- C. Restart Kafka cluster
- D. Modify ZooKeeper nodes

---

### Question 36

**Which SMT can remove sensitive fields?**


- A. FilterField
- B. MaskField
- C. RemoveField
- D. HideField

---

### Question 37

**What does the Cast SMT do?**


- A. Removes fields
- B. Changes data type of a field
- C. Filters messages
- D. Routes to different topics

---

### Question 38

**What does the Flatten SMT do?**


- A. Compresses data
- B. Transforms nested structure to flat one
- C. Removes duplicates
- D. Sorts fields

---

### Question 39

**Which SMT can route messages to different topics?**


- A. TopicRouter
- B. RegexRouter
- C. RouteTransform
- D. TopicChanger

---

### Question 40

**What is Debezium?**


- A. A Kafka broker implementation
- B. Change data capture connector project
- C. A monitoring tool
- D. A schema registry

---

### Question 41

**Why is Debezium better than JDBC source for databases?**


- A. It's not better
- B. Reads directly from transaction logs - more efficient and accurate
- C. Easier configuration
- D. Works offline

---

### Question 42

**How does Connect handle dead letter queues?**


- A. Doesn't support them
- B. Can route corrupt messages to special topic via `error.tolerance` configuration
- C. Automatically deletes bad messages
- D. Sends to ZooKeeper

---

### Question 43

**What is the `group.id` configuration for Connect workers?**


- A. Identifies the Kafka cluster
- B. Identifies workers that are part of same Connect cluster
- C. Identifies consumer group
- D. Identifies topic

---

### Question 44

**How do you start a Connect worker in distributed mode?**


- A. `connect-standalone.sh`
- B. `connect-distributed.sh`
- C. `kafka-server-start.sh`
- D. `connect-cluster.sh`

---

### Question 45

**What happens when you add a new worker to a Connect cluster?**


- A. Manual rebalancing required
- B. Automatic rebalancing of connectors and tasks
- C. Cluster restart needed
- D. Nothing

---

### Question 46

**Which API does Connect use for connector management?**


- A. RPC
- B. REST API
- C. gRPC
- D. WebSockets

---

### Question 47

**How can you check available connector plug-ins?**


- A. Read config files
- B. GET request to /connector-plugins endpoint
- C. Check ZooKeeper
- D. Restart workers

---

### Question 48

**What is Standalone mode used for?**


- A. Production deployments
- B. Testing and cases where connectors need to run on specific machines
- C. High availability
- D. Large scale deployments

---

### Question 49

**Which topic stores connector offsets in distributed mode?**


- A. `__consumer_offsets`
- B. `offset.storage.topic` (e.g., `connect-offsets`)
- C. `__transaction_state`
- D. `kafka-offsets`

---

### Question 50

**What is Confluent Hub?**


- A. A Kafka broker
- B. Repository of connectors and other Kafka components
- C. A monitoring tool
- D. A cloud service only

---

### Question 51

**Why shouldn't you use FileStream connectors in production?**


- A. They're too fast
- B. Limited functionality and no reliability guarantees
- C. They're deprecated
- D. They require special licenses

---

### Question 52

**What alternatives exist to Kafka Connect for data integration?**


- A. No alternatives
- B. Flume, Logstash, NiFi, StreamSets, Talend
- C. Only custom code
- D. Only Kafka Streams

---

### Question 53

**When might you use Flume instead of Connect?**


- A. Never
- B. When building Hadoop-centric system where Kafka is just one input
- C. Always
- D. For real-time processing

---

### Question 54

**What is the main concern with GUI-based ETL tools?**


- A. Too simple
- B. Can be heavy and complex for simple Kafka integration
- C. Not available
- D. Too expensive always

---

### Question 55

**Can stream processing frameworks write to external systems?**


- A. No
- B. Yes, most support reading from Kafka and writing to other systems
- C. Only with Connect
- D. Only with custom code

---

### Question 56

**What is the most important feature of any data integration solution?**


- A. Speed
- B. Ability to deliver all messages under all failure conditions
- C. Cost
- D. Ease of use

---

### Question 57

**How should you place connector JARs in plugin.path?**


- A. All in top-level directory
- B. Each connector in its own subdirectory with dependencies
- C. Mixed together
- D. In Kafka lib folder

---

### Question 58

**What does Connect's data model include?**


- A. Only binary data
- B. Data objects and schemas describing the data
- C. Only JSON
- D. Only strings

---

### Question 59

**How does JDBC source determine new records?**


- A. Always reads everything
- B. Uses timestamp columns or incrementing primary keys
- C. Random selection
- D. Manual triggers

---

### Question 60

**What is the benefit of preserving schema in pipelines?**


- A. None
- B. Allows schema evolution and reduces coupling between systems
- C. Increases data size
- D. Slows processing

---

**End of Test**

**Total Questions:** 60

**Good luck with your CCDAK preparation!**7
