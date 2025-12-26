59
# Chapter 1: Meet Kafka - CCDAK Practice Test

**Total Questions: 60**  
**Time Limit: 90 minutes**  
**Passing Score: 70%**

[View Solutions](../solutions/chapter-tests/chapter-01-solutions.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

## Questions

### 1. What is the primary purpose of Apache Kafka?
A) To serve as a relational database  
B) To act as a publish/subscribe messaging system  
C) To replace web servers  
D) To function as a NoSQL key-value store

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#1.-b-to-act-as-a-publish-subscribe-messaging-system)

### 2. In Kafka terminology, what is a message?
A) A database row  
B) An array of bytes  
C) A JSON object only  
D) An XML document

[solution](../solutions/chapter-tests/chapter-01-solutions.md#2-b-an-array-of-bytes)

### 3. What is the purpose of a message key in Kafka?
A) To encrypt the message  
B) To authenticate the producer  
C) To control which partition the message is written to  
D) To set the message priority

[solution](../solutions/chapter-tests/chapter-01-solutions.md#3-c-to-control-which-partition-the-message-is-written-to)

### 4. What is a batch in Kafka?
A) A single message  
B) A collection of messages for the same topic and partition  
C) A group of topics  
D) A set of consumer groups

[solution](../solutions/chapter-tests/chapter-01-solutions.md#4-b-a-collection-of-messages-for-the-same-topic-and-partition)

### 5. Why are messages written in batches to Kafka?
A) To reduce network overhead  
B) To improve message security  
C) To enable message encryption  
D) To support transactions only

### 6. Which serialization format is recommended for Kafka messages?
A) Plain text only  
B) Binary only  
C) Apache Avro  
D) CSV format

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#6.-c)-apache-avro)

### 7. What advantage does Apache Avro provide for Kafka?
A) Faster network speeds  
B) Schema evolution with backward and forward compatibility  
C) Built-in encryption  
D) Automatic data validation

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#7.-b)-schema-evolution-with-backward-and-forward-compatibility)

### 8. How are messages organized in Kafka?
A) In databases and tables  
B) In topics and partitions  
C) In queues and stacks  
D) In files and directories

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#8.-b)-in-topics-and-partitions)

### 9. What is a Kafka topic?
A) A single message  
B) A category for organizing messages  
C) A consumer group  
D) A broker instance

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#9.-b)-a-category-for-organizing-messages)

### 10. What is a partition in Kafka?
A) A segment of a broker's disk  
B) A single log where messages are appended  
C) A consumer thread  
D) A producer connection

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#10.-b)-a-single-log-where-messages-are-appended)

### 11. Is message ordering guaranteed across all partitions in a topic?
A) Yes, always guaranteed  
B) No, only within a single partition  
C) Yes, but only for keyed messages  
D) No, never guaranteed

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#11.-b)-no-only-within-a-single-partition)

### 12. What is the purpose of multiple partitions in a topic?
A) To provide redundancy only  
B) To enable horizontal scalability  
C) To encrypt messages  
D) To compress data

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#12.-b)-to-enable-horizontal-scalability)

### 13. What is a producer in Kafka?
A) An application that reads messages  
B) An application that creates new messages  
C) A broker that stores messages  
D) A partition that holds data

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#13.-b)-an-application-that-creates-new-messages)

### 14. What is a consumer in Kafka?
A) An application that writes messages  
B) An application that reads messages  
C) A broker that distributes messages  
D) A topic that stores messages

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#14.-b)-an-application-that-reads-messages)

### 15. What does a consumer offset represent?
A) The producer's address  
B) The partition's size  
C) An integer value indicating the consumer's position in the partition  
D) The broker's ID

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#15.-c)-an-integer-value-indicating-the-consumers-position-in-the-partition)

### 16. Where are consumer offsets typically stored?
A) In the producer application  
B) In a local file  
C) In Kafka itself  
D) In an external database only

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#16.-c)-in-kafka-itself)

### 17. What is a consumer group?
A) A set of producers  
B) One or more consumers working together to consume a topic  
C) A collection of topics  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#17.-b)-one-or-more-consumers-working-together-to-consume-a-topic)
D) A group of brokers

### 18. In a consumer group, how many consumers can read from a single partition?
A) Multiple consumers simultaneously  
B) Only one consumer  
C) Unlimited consumers  
D) Two consumers maximum

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#18.-b)-only-one-consumer)

### 19. What is a Kafka broker?
A) A client application  
B) A single Kafka server  
C) A partition  
D) A consumer group

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#19.-b)-a-single-kafka-server)

### 20. What role does the cluster controller play?
A) It stores all messages  
B) It assigns partitions to brokers and monitors for broker failures  
C) It consumes messages  
D) It produces messages

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#20.-b)-it-assigns-partitions-to-brokers-and-monitors-for-broker-failures)

### 21. What is the partition leader?
A) The largest partition  
B) The broker that owns a partition and handles reads/writes  
C) The first partition created  
D) The consumer with the highest priority

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#21.-b)-the-broker-that-owns-a-partition-and-handles-readswrites)

### 22. What is the purpose of partition followers?
A) To consume messages  
B) To provide redundancy by replicating the leader's data  
C) To produce messages  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#22.-b)-to-provide-redundancy-by-replicating-the-leaders-data)
D) To compress data

### 23. What is retention in Kafka?
A) The time it takes to send a message  
B) The durable storage of messages for a period of time  
C) The number of consumers  
D) The partition count

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#23.-b)-the-durable-storage-of-messages-for-a-period-of-time)

### 24. How can retention be configured in Kafka?
A) By time period only  
B) By partition size only  
C) By time period or partition size  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#24.-c)-by-time-period-or-partition-size)
D) Retention cannot be configured

### 25. What is log compaction?
A) Compressing all messages  
B) Retaining only the last message with a specific key  
C) Deleting all old messages  
D) Encrypting messages

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#25.-c)-deleting-all-old-messages)

### 26. Why would you use multiple Kafka clusters?
A) To increase message size  
B) For data segregation, security isolation, and disaster recovery  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#26.-b)-for-data-segregation-security-isolation-and-disaster-recovery)
C) To reduce costs only  
D) To simplify configuration

### 27. What is MirrorMaker used for?
A) To mirror screens  
B) To replicate data between Kafka clusters  
C) To compress messages  
D) To encrypt data

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#27.-b)-to-replicate-data-between-kafka-clusters)

### 28. How does MirrorMaker work?
A) By copying disk files  
B) By using a Kafka consumer and producer linked together  
C) By database replication  
D) By network mirroring

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#28.-b)-by-using-a-kafka-consumer-and-producer-linked-together)

### 29. Which statement about Kafka producers is true?
A) Kafka can only handle one producer  
B) Kafka can seamlessly handle multiple producers  
C) Producers cannot share topics  
D) Each producer needs a separate cluster

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#29.-b)-kafka-can-seamlessly-handle-multiple-producers)

### 30. How does Kafka handle multiple consumers?
A) Only one consumer can read a topic  
B) Multiple consumers can read without interfering with each other  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#30.-b)-multiple-consumers-can-read-without-interfering-with-each-other)
C) Consumers must take turns  
D) Messages are deleted after first read

### 31. What is a key benefit of Kafka's disk-based retention?
A) Messages are lost if consumers are offline  
B) Consumers can fall behind without losing data  
C) Producers cannot send messages  
D) Topics become read-only

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#31.-b)-consumers-can-fall-behind-without-losing-data)

### 32. What happens if a consumer in a consumer group fails?
A) All messages are lost  
B) The remaining members reassign the partitions  
C) The topic is deleted  
D) Producers stop sending messages

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#32.-b)-the-remaining-members-reassign-the-partitions)

### 33. What is Kafka's scalability characteristic?
A) Can only run on a single server  
B) Flexible scalability from single broker to hundreds of brokers  
C) Requires downtime for scaling  
D) Limited to 10 brokers maximum

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#33.-b)-flexible-scalability-from-single-broker-to-hundreds-of-brokers)

### 34. Can Kafka clusters be expanded while online?
A) No, requires full shutdown  
B) Yes, with no impact on availability  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#34.-b)-yes-with-no-impact-on-availability)
C) Only during maintenance windows  
D) Only if no consumers are connected

### 35. What is Kafka Connect?
A) A network cable  
B) An API for pulling/pushing data from/to source and sink systems  
C) A consumer library  
D) A monitoring tool only

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#35.-b)-an-api-for-pullingpushing-data-fromto-source-and-sink-systems)

### 36. What is Kafka Streams?
A) A video streaming service  
B) A library for stream processing applications  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#36.-b)-a-library-for-stream-processing-applications)
C) A storage system  
D) A producer API

### 37. How does Kafka fit into a data ecosystem?
A) As the data warehouse  
B) As the circulatory system carrying messages between components  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#37.-b)-as-the-circulatory-system-carrying-messages-between-components)
C) As the primary database  
D) As the UI layer

### 38. What was the original use case for Kafka at LinkedIn?
A) Video streaming  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#38.-b)-user-activity-tracking)
B) User activity tracking  
C) Email service  
D) File storage

### 39. Which messaging pattern does Kafka use?
A) Point-to-point only  
B) Publish/subscribe (pub/sub)  
C) Request-response only  
D) RPC (Remote Procedure Call)

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#39.-b)-publishsubscribe-pubsub)

### 40. In pub/sub messaging, who is the publisher?
A) The receiver of messages  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#40.-b)-the-sender-of-messages)
B) The sender of messages  
C) The broker only  
D) The partition

### 41. What is the broker's role in pub/sub systems?
A) To consume messages  
B) To act as a central point where messages are published  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#41.-b)-to-act-as-a-central-point-where-messages-are-published)
C) To generate messages  
D) To delete messages

### 42. What problem does Kafka solve for LinkedIn?
A) Email delivery  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#42.-b)-creating-a-unified-platform-for-metrics-and-activity-tracking)
B) Creating a unified platform for metrics and activity tracking  
C) Video encoding  
D) DNS resolution

### 43. What are the main goals Kafka was designed to achieve?
A) Low throughput and high latency  
B) Decouple producers/consumers, provide persistence, optimize throughput, allow horizontal scaling  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#43.-b)-decouple-producersconsumers-provide-persistence-optimize-throughput-allow-horizontal-scaling)
C) Replace databases  
D) Centralize all applications

### 44. What does "distributed commit log" mean?
A) A centralized error log  
B) A durable, ordered record of transactions distributed across servers  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#44.-b)-a-durable-ordered-record-of-transactions-distributed-across-servers)
C) A deleted message archive  
D) A producer configuration file

### 45. When was Kafka released as open source?
A) 2015  
B) 2005  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#45.-c)-late-2010)
C) Late 2010  
D) 2020

### 46. When did Kafka graduate from Apache incubator?
A) 2008  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#46.-b)-october-2012)
B) October 2012  
C) 2015  
D) 2020

### 47. Who founded Confluent?
A) Bill Gates  
B) Jay Kreps, Neha Narkhede, and Jun Rao  
C) Jeff Bezos  
D) Mark Zuckerberg

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#47.-b)-jay-kreps-neha-narkhede-and-jun-rao)

### 48. What company originally developed Kafka?
A) Microsoft  
B) Google  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#48.-c)-linkedin)
C) LinkedIn  
D) Facebook

### 49. According to the chapter, what is a stream in Kafka?
A) A single broker  
B) A single topic of data regardless of partition count  
C) A consumer group  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#49.-b)-a-single-topic-of-data-regardless-of-partition-count)
D) A producer instance

### 50. What is the relationship between a partition and message ordering?
A) No ordering guaranteed  
B) Messages are ordered within a partition  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#50.-b)-messages-are-ordered-within-a-partition)
C) Messages are random  
D) Ordering only works with timestamps

### 51. How does Kafka achieve high performance?
A) By limiting producers and consumers  
B) By scaling producers, consumers, and brokers to handle large message streams  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#51.-b)-by-scaling-producers-consumers-and-brokers-to-handle-large-message-streams)
C) By keeping all data in memory only  
D) By using single-threaded processing

### 52. What is the trade-off when using larger batches?
A) Higher latency but better throughput  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#52.-b)-lower-throughput-and-higher-latency)
B) Lower throughput and higher latency  
C) No trade-offs  
D) Reduced message size

### 53. Why does Kafka use schemas?
A) To slow down processing  
B) To decouple writing and reading messages  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#53.-b)-to-decouple-writing-and-reading-messages)
C) To increase message size  
D) To limit producers

### 54. What happens when a partition is replicated?
A) Messages are encrypted  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#54.-b)-additional-brokers-store-copies-for-redundancy)
B) Additional brokers store copies for redundancy  
C) Consumers receive duplicate messages  
D) Producers send messages twice

### 55. Where must producers connect to publish messages?
A) To any broker  
B) To the partition leader  
C) To the cluster controller  
D) To the consumer

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#55.-b)-to-the-partition-leader)

### 56. Can consumers fetch from partition followers?
A) No, never allowed  
B) Yes, consumers may fetch from leader or followers  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#56.-b)-yes-consumers-may-fetch-from-leader-or-followers)
C) Only on weekends  
D) Only for small messages

### 57. What is a use case for Kafka mentioned in the chapter?
A) Operating system replacement  
B) Activity tracking, messaging, metrics and logging, stream processing  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#57.-b)-activity-tracking-messaging-metrics-and-logging-stream-processing)
C) Web browser  
D) Spreadsheet application

### 58. What problem did LinkedIn face before Kafka?
A) Too much automation  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#58.-b)-fragmented-systems-for-metrics-and-activity-tracking-with-poor-scalability)
B) Fragmented systems for metrics and activity tracking with poor scalability  
C) No employees  
D) Too few applications

### 59. What format did LinkedIn originally use for activity tracking?
A) JSON  
B) XML  
C) Binary  
D) CSV

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#59.-a)-json)

### 60. According to Jay Kreps, why is Kafka named after Franz Kafka?
A) Deep symbolic meaning  
B) Kafka was a writer, and the system is optimized for writing  
C) It was a client's request  

[solution](../solutions/chapter-tests/chapter-01-solutions.md/#60.-b)-kafka-was-a-writer-and-the-system-is-optimized-for-writing)
D) Random name generator

---

## Answer Key
[View detailed solutions and explanations](../solutions/chapter-tests/chapter-01-solutions.md)

---

**Note:** This practice test is designed to help you prepare for the CCDAK certification exam. Make sure to review the Kafka documentation and the official Confluent study guide for comprehensive preparation.