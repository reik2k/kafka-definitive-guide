# Chapter 1: Meet Kafka - Solutions
CCDAK Practice Test Solutions
**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 1

[Back to Test](../../chapter-tests/chapter-01-test.md) | [Main README](../../README.md)

---

## Answer Key

### Answer 1

1. B) To act as a publish/subscribe messaging system


**Explanation:** 

*Apache Kafka was designed as a publish/subscribe messaging system to handle data pipelines. It allows publishers to send messages and subscribers to receive them without direct coupling.*

### Answer 2

2. B) An array of bytes

**Explanation:** 

*In Kafka, a message is simply an array of bytes. Kafka doesn't impose any specific format or meaning on the message content.*


### Answer 3

3. C) To control which partition the message is written to

**Explanation:** 

*Message keys are used to determine which partition a message is written to. Messages with the same key are always written to the same partition (if partition count doesn't change).*


### Answer 4

4. B) A collection of messages for the same topic and partition

**Explanation:** 

*A batch is a collection of messages that are produced to the same topic and partition, written together for efficiency.*


### Answer 5

5. A) To reduce network overhead

**Explanation:** 

*Batching messages reduces network overhead by collecting multiple messages together instead of sending each one individually across the network.*


### Answer 6

6. C) Apache Avro

**Explanation:** 

*Apache Avro is the recommended serialization format. It provides compact serialization, schema separation from payloads, strong typing, and schema evolution with backward and forward compatibility.*


### Answer 7

7. B) Schema evolution with backward and forward compatibility

**Explanation:** 

*Avro provides robust schema evolution, allowing schemas to change over time while maintaining backward and forward compatibility.*


### Answer 8

8. B) In topics and partitions

**Explanation:** 

*Kafka organizes messages into topics, which are further divided into partitions for scalability and parallelism.*


### Answer 9

9. B) A category for organizing messages

**Explanation:** 

*A topic is a category or feed name to which messages are published. It's analogous to a database table or folder in a filesystem.*


### Answer 10

10. B) A single log where messages are appended

**Explanation:** 

*A partition is a single log where messages are written in an append-only fashion and read in order from beginning to end.*


### Answer 11

11. B) No, only within a single partition

**Explanation:** 

*Message ordering is guaranteed only within a single partition, not across all partitions in a topic.*


### Answer 12

12. B) To enable horizontal scalability

**Explanation:** 

*Multiple partitions allow a topic to be scaled horizontally across multiple servers, providing performance beyond what a single server can deliver.*


### Answer 13

13. B) An application that creates new messages

**Explanation:** 

*Producers are client applications that create and ## **Question $1** new messages to Kafka topics.*


### Answer 14

14. B) An application that reads messages

**Explanation:** 

*Consumers are client applications that subscribe to topics and read messages in the order they were produced.*


### Answer 15

15. C) An integer value indicating the consumer's position in the partition

**Explanation:** 

*The offset is an integer value that continually increases and indicates which messages the consumer has already consumed.*


### Answer 16

16. C) In Kafka itself

**Explanation:** 

*Consumer offsets are typically stored in Kafka itself, allowing consumers to stop and restart without losing their place.*


### Answer 17

17. B) One or more consumers working together to consume a topic

**Explanation:** 

*A consumer group consists of one or more consumers that work together to consume a topic, ensuring that each partition is consumed by only one member.*


### Answer 18

18. B) Only one consumer

**Explanation:** 

*In a consumer group, each partition is consumed by only one consumer at a time. This is called ownership of the partition.*


### Answer 19

19. B) A single Kafka server

**Explanation:** 

*A broker is a single Kafka server that receives messages from producers and serves consumers.*


### Answer 20

20. B) It assigns partitions to brokers and monitors for broker failures

**Explanation:** 

*The cluster controller is responsible for administrative operations including partition assignment and monitoring broker health.*


### Answer 21

21. B) The broker that owns a partition and handles reads/writes

**Explanation:** 

*The partition leader is the broker that owns a specific partition and handles all reads and writes for that partition.*


### Answer 22

22. B) To provide redundancy by replicating the leader's data

**Explanation:** 

*Partition followers replicate the leader's data to provide redundancy, allowing them to take over if the leader fails.*


### Answer 23

23. B) The durable storage of messages for a period of time

**Explanation:** 

*Retention is the durable storage of messages in Kafka for a configured period of time or until a size limit is reached.*


### Answer 24

24. C) By time period or partition size

**Explanation:** 

*Retention can be configured either by time period (e.g., 7 days) or by partition size (e.g., 1 GB).*


### Answer 25

25. B) Retaining only the last message with a specific key

**Explanation:** 

*Log compaction means Kafka retains only the last message produced with a specific key, useful for changelog-type data.*


### Answer 26

26. B) For data segregation, security isolation, and disaster recovery

**Explanation:** 

*Multiple clusters are used for segregating data types, isolating security requirements, and supporting multiple datacenters for disaster recovery.*


### Answer 27

27. B) To replicate data between Kafka clusters

**Explanation:** 

*MirrorMaker is a tool used for replicating data from one Kafka cluster to another.*


### Answer 28

28. B) By using a Kafka consumer and producer linked together

**Explanation:** 

*MirrorMaker works by consuming messages from one cluster and producing them to another cluster.*


### Answer 29

29. B) Kafka can seamlessly handle multiple producers

**Explanation:** 

*Kafka can handle multiple producers simultaneously, whether they're using many topics or the same topic.*


### Answer 30

30. B) Multiple consumers can read without interfering with each other

**Explanation:** 

*Kafka is designed for multiple consumers to read any single stream of messages without interfering with each other.*


### Answer 31

31. B) Consumers can fall behind without losing data

**Explanation:** 

*Disk-based retention means consumers can fall behind in processing without losing data, as messages are durably stored.*


### Answer 32

32. B) The remaining members reassign the partitions

**Explanation:** 

*If a consumer fails, the remaining members of the consumer group will reassign the partitions to take over for the missing member.*


### Answer 33

33. B) Flexible scalability from single broker to hundreds of brokers

**Explanation:** 

*Kafka offers flexible scalability, allowing systems to start with a single broker and expand to hundreds of brokers as needed.*


### Answer 34

34. B) Yes, with no impact on availability

**Explanation:** 

*Kafka clusters can be expanded while online with no impact on the overall system availability.*


### Answer 35

35. B) An API for pulling/pushing data from/to source and sink systems

**Explanation:** 

*Kafka Connect is an API that assists with pulling data from source systems into Kafka and pushing data from Kafka to sink systems.*


### Answer 36

36. B) A library for stream processing applications

**Explanation:** 

*Kafka Streams provides a library for developing scalable and fault-tolerant stream processing applications.*


### Answer 37

37. B) As the circulatory system carrying messages between components

**Explanation:** 

*Kafka provides the circulatory system for the data ecosystem, carrying messages between various infrastructure components.*


### Answer 38

38. B) User activity tracking

**Explanation:** 

*The original use case for Kafka at LinkedIn was user activity tracking on their website.*


### Answer 39

39. B) ## **Question $1**/subscribe (pub/sub)

**Explanation:** 

*Kafka uses the ## **Question $1**/subscribe messaging pattern where publishers send messages and subscribers receive them.*


### Answer 40

40. B) The sender of messages

**Explanation:** 

*In pub/sub messaging, the publisher is the sender or producer of messages.*


### Answer 41

41. B) To act as a central point where messages are published

**Explanation:** 

*The broker serves as a central point where messages are published and from which subscribers can receive them.*


### Answer 42

42. B) Creating a unified platform for metrics and activity tracking

**Explanation:** 

*Kafka solved LinkedIn's problem of having fragmented systems for metrics collection and user activity tracking.*


### Answer 43

43. B) Decouple producers/consumers, provide persistence, optimize throughput, allow horizontal scaling

**Explanation:** 

*Kafka was designed to decouple producers and consumers, provide message persistence, optimize for high throughput, and allow horizontal scaling.*


### Answer 44

44. B) A durable, ordered record of transactions distributed across servers

**Explanation:** 

*A distributed commit log is a durable, ordered record of all transactions that can be replayed and is distributed across multiple servers.*


### Answer 45

45. C) Late 2010

**Explanation:** 

*Kafka was released as an open source project on GitHub in late 2010.*


### Answer 46

46. B) October 2012

**Explanation:** 

*Apache Kafka graduated from the Apache incubator in October 2012.*


### Answer 47

47. B) Jay Kreps, Neha Narkhede, and Jun Rao

**Explanation:** 

*Confluent was founded by Jay Kreps, Neha Narkhede, and Jun Rao in the fall of 2014.*


### Answer 48

48. C) LinkedIn

**Explanation:** 

*Apache Kafka was originally developed at LinkedIn to solve their data pipeline challenges.*


### Answer 49

49. B) A single topic of data regardless of partition count

**Explanation:** 

*A stream is considered to be a single topic of data, regardless of how many partitions it has.*


### Answer 50

50. B) Messages are ordered within a partition

**Explanation:** 

*Messages are written and read in order within a single partition, ensuring ordering at the partition level.*


### Answer 51

51. B) By scaling producers, consumers, and brokers to handle large message streams

**Explanation:** 

*Kafka achieves high performance by allowing all components (producers, consumers, and brokers) to scale out to handle very large message streams.*


### Answer 52

52. A) Higher latency but better throughput

**Explanation:** 

*Larger batches provide better throughput (more messages per unit time) but at the cost of higher latency (longer propagation time for individual messages).*


### Answer 53

53. B) To decouple writing and reading messages

**Explanation:** 

*Schemas allow writing and reading messages to be decoupled, as messages can be understood without tight coordination between producers and consumers.*


### Answer 54

54. B) Additional brokers store copies for redundancy

**Explanation:** 

*When a partition is replicated, additional brokers (followers) store copies of the partition's data for redundancy and fault tolerance.*


### Answer 55

55. B) To the partition leader

**Explanation:** 

*Producers must connect to the partition leader to ## **Question $1** messages, as only the leader handles writes.*


### Answer 56

56. B) Yes, consumers may fetch from leader or followers

**Explanation:** 

*Consumers can fetch messages from either the partition leader or one of the followers.*


### Answer 57

57. B) Activity tracking, messaging, metrics and logging, stream processing

**Explanation:** 

*The chapter mentions multiple use cases including activity tracking, messaging, metrics and logging, commit logs, and stream processing.*


### Answer 58

58. B) Fragmented systems for metrics and activity tracking with poor scalability

**Explanation:** 

*Before Kafka, LinkedIn had fragmented, poorly scalable systems for collecting metrics and tracking user activity.*


### Answer 59

59. B) XML

**Explanation:** 

*LinkedIn originally used XML format for activity tracking, which was computationally expensive to parse and had inconsistent formatting.*


### Answer 60

60. B) Kafka was a writer, and the system is optimized for writing

**Explanation:** 

*Jay Kreps named it after Franz Kafka because he thought using a writer's name made sense for a system optimized for writing. He also mentioned the name sounded cool for an open source project.*


---

## Study Tips

### Key Concepts to Master:
1. **Message Structure**: Understand messages, keys, batches, and schemas
2. **Architecture**: Know the roles of topics, partitions, producers, consumers, and brokers
3. **Consumer Groups**: Understand how partition ownership works
4. **Scalability**: How Kafka achieves horizontal scaling
5. **Retention**: Different retention policies and log compaction
6. **Replication**: Leader/follower model and fault tolerance

### Related CCDAK Topics:
- Producer API and configuration (Chapter 3)
- Consumer API and configuration (Chapter 4)
- Partition assignment strategies
- Offset management
- Serialization and deserialization

---

[Back to Test](../../chapter-tests/chapter-01-test.md) | [Main README](../../README.md)