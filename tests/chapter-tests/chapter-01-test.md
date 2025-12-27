# Chapter 1: Meet Kafka - CCDAK Practice Test

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 1

**CCDAK Practice Test - 60 Questions**
**Time Limit: 90 minutes**
**Passing Score: 70%**

[View Solutions](../chapter-tests-solutions/chapter-01-solutions.md) | [Main README](../../README.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

## Questions

### Question 1

**What is the primary purpose of Apache Kafka?**

A) To serve as a relational database
B) To act as a publish/subscribe messaging system
C) To replace web servers
D) To function as a NoSQL key-value store

[solution](../chapter-tests-solutions/chapter-01-solutions.md#answer-1)

### Question 2

**In Kafka terminology, what is a message?**

A) A database row
B) An array of bytes
C) A JSON object only
D) An XML document

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-2)

### Question 3

**What is the purpose of a message key in Kafka?**

A) To encrypt the message
B) To authenticate the producer
C) To control which partition the message is written to
D) To set the message priority

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-3)

### Question 4

**What is a batch in Kafka?**

A) A single message
B) A collection of messages for the same topic and partition
C) A group of topics
D) A set of consumer groups

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-4)

### Question 5

**Why are messages written in batches to Kafka?**

A) To reduce network overhead
B) To improve message security
C) To enable message encryption
D) To support transactions only

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-5)

### Question 6

**Which serialization format is recommended for Kafka messages?**

A) Plain text only
B) Binary only
C) Apache Avro
D) CSV format

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-6)

### Question 7

**What advantage does Apache Avro provide for Kafka?**

A) Faster network speeds
B) Schema evolution with backward and forward compatibility
C) Built-in encryption
D) Automatic data validation

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-7)

### Question 8

**How are messages organized in Kafka?**

A) In databases and tables
B) In topics and partitions
C) In queues and stacks
D) In files and directories

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-8)

### Question 9

**What is a Kafka topic?**

A) A single message
B) A category for organizing messages
C) A consumer group
D) A broker instance

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-9)

### Question 10

**What is a partition in Kafka?**

A) A segment of a broker's disk
B) A single log where messages are appended
C) A consumer thread
D) A producer connection

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-10.md)

### Question 11

**Is message ordering guaranteed across all partitions in a topic?**

A) Yes, always guaranteed
B) No, only within a single partition
C) Yes, but only for keyed messages
D) No, never guaranteed

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-11)

### Question 12

**What is the purpose of multiple partitions in a topic?**

A) To provide redundancy only
B) To enable horizontal scalability
C) To encrypt messages
D) To compress data

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-12)

### Question 13

**What is a producer in Kafka?**

A) An application that reads messages
B) An application that creates new messages
C) A broker that stores messages
D) A partition that holds data

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-13)

### Question 14

**What is a consumer in Kafka?**

A) An application that writes messages
B) An application that reads messages
C) A broker that distributes messages
D) A topic that stores messages

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-14)

### Question 15

**What does a consumer offset represent?**

A) The producer's address
B) The partition's size
C) An integer value indicating the consumer's position in the partition
D) The broker's ID

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-15)

### Question 16

**Where are consumer offsets typically stored?**

A) In the producer application
B) In a local file
C) In Kafka itself
D) In an external database only

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-16)

### Question 17

**What is a consumer group?**

A) A set of producers
B) One or more consumers working together to consume a topic
C) A collection of topics
D) A group of brokers

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-17)

### Question 18

**In a consumer group, how many consumers can read from a single partition?**

A) Multiple consumers simultaneously
B) Only one consumer
C) Unlimited consumers
D) Two consumers maximum

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-18)

### Question 19

**What is a Kafka broker?**

A) A client application
B) A single Kafka server
C) A partition
D) A consumer group

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-18)

### Question 20

**What role does the cluster controller play?**

A) It stores all messages
B) It assigns partitions to brokers and monitors for broker failures
C) It consumes messages
D) It produces messages

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-20)

### Question 21

**What is the partition leader?**

A) The largest partition
B) The broker that owns a partition and handles reads/writes
C) The first partition created
D) The consumer with the highest priority

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-21)

### Question 22

**What is the purpose of partition followers?**

A) To consume messages
B) To provide redundancy by replicating the leader's data
C) To produce messages
D) To compress data

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-21)

### Question 23

**What is retention in Kafka?**

A) The time it takes to send a message
B) The durable storage of messages for a period of time
C) The number of consumers
D) The partition count

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-23)

### Question 24

**How can retention be configured in Kafka?**

A) By time period only
B) By partition size only
C) By time period or partition size
D) Retention cannot be configured

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-24)

### Question 25

**What is log compaction?**

A) Compressing all messages
B) Retaining only the last message with a specific key
C) Deleting all old messages
D) Encrypting messages

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-25)

### Question 26

**Why would you use multiple Kafka clusters?**

A) To increase message size
B) For data segregation, security isolation, and disaster recovery
C) To reduce costs only
D) To simplify configuration

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-26)

### Question 27

**What is MirrorMaker used for?**

A) To mirror screens
B) To replicate data between Kafka clusters
C) To compress messages
D) To encrypt data

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-27)

### Question 28

**How does MirrorMaker work?**

A) By copying disk files
B) By using a Kafka consumer and producer linked together
C) By database replication
D) By network mirroring

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-28)

### Question 29

**Which statement about Kafka producers is true?**

A) Kafka can only handle one producer
B) Kafka can seamlessly handle multiple producers
C) Producers cannot share topics
D) Each producer needs a separate cluster

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-29)

### Question 30

**How does Kafka handle multiple consumers?**

A) Only one consumer can read a topic
B) Multiple consumers can read without interfering with each other
C) Consumers must take turns
D) Messages are deleted after first read

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-30)

### Question 31

**What is a key benefit of Kafka's disk-based retention?**

A) Messages are lost if consumers are offline
B) Consumers can fall behind without losing data
C) Producers cannot send messages
D) Topics become read-only

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-31)

### Question 32

**What happens if a consumer in a consumer group fails?**

A) All messages are lost
B) The remaining members reassign the partitions
C) The topic is deleted
D) Producers stop sending messages

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-32)

### Question 33

**What is Kafka's scalability characteristic?**

A) Can only run on a single server
B) Flexible scalability from single broker to hundreds of brokers
C) Requires downtime for scaling
D) Limited to 10 brokers maximum

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-33)

### Question 34

**Can Kafka clusters be expanded while online?**

A) No, requires full shutdown
B) Yes, with no impact on availability
C) Only during maintenance windows
D) Only if no consumers are connected

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-34)

### Question 35

**What is Kafka Connect?**

A) A network cable
B) An API for pulling/pushing data from/to source and sink systems
C) A consumer library
D) A monitoring tool only

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-35)

### Question 36

**What is Kafka Streams?**

A) A video streaming service
B) A library for stream processing applications
C) A storage system
D) A producer API

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-36)

### Question 37

**How does Kafka fit into a data ecosystem?**

A) As the data warehouse
B) As the circulatory system carrying messages between components
C) As the primary database
D) As the UI layer

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-37)

### Question 38

**What was the original use case for Kafka at LinkedIn?**

A) Video streaming
B) User activity tracking
C) Email service
D) File storage

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-38)

### Question 39

**Which messaging pattern does Kafka use?**

A) Point-to-point only
B) Publish/subscribe (pub/sub)
C) Request-response only
D) RPC (Remote Procedure Call)

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-39)

### Question 40

**In pub/sub messaging, who is the publisher?**

A) The receiver of messages
B) The sender of messages
C) The broker only
D) The partition

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-40)

### Question 41

**What is the broker's role in pub/sub systems?**

A) To consume messages
B) To act as a central point where messages are published
C) To generate messages
D) To delete messages

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-41)

### Question 42

**What problem does Kafka solve for LinkedIn?**

A) Email delivery
B) Creating a unified platform for metrics and activity tracking
C) Video encoding
D) DNS resolution

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-42)

### Question 43

**What are the main goals Kafka was designed to achieve?**

A) Low throughput and high latency
B) Decouple producers/consumers, provide persistence, optimize throughput, allow horizontal scaling
C) Replace databases
D) Centralize all applications

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-43)

### Question 44

**What does "distributed commit log" mean?**

A) A centralized error log
B) A durable, ordered record of transactions distributed across servers
C) A deleted message archive
D) A producer configuration file

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-44)

### Question 45

**When was Kafka released as open source?**

A) 2015
B) 2005
C) Late 2010
D) 2020

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-45)

### Question 46

**When did Kafka graduate from Apache incubator?**

A) 2008
B) October 2012
C) 2015
D) 2020

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-46)

### Question 47

**Who founded Confluent?**

A) Bill Gates
B) Jay Kreps, Neha Narkhede, and Jun Rao
C) Jeff Bezos
D) Mark Zuckerberg

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-47)

### Question 48

**What company originally developed Kafka?**

A) Microsoft
B) Google
C) LinkedIn
D) Facebook

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-48)

### Question 49

**According to the chapter, what is a stream in Kafka?**

A) A single broker
B) A single topic of data regardless of partition count
C) A consumer group
D) A producer instance

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-49)

### Question 50

**What is the relationship between a partition and message ordering?**

A) No ordering guaranteed
B) Messages are ordered within a partition
C) Messages are random
D) Ordering only works with timestamps

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-50)

### Question 51

**How does Kafka achieve high performance?**

A) By limiting producers and consumers
B) By scaling producers, consumers, and brokers to handle large message streams
C) By keeping all data in memory only
D) By using single-threaded processing

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-51)

### Question 52

**What is the trade-off when using larger batches?**

A) Higher latency but better throughput
B) Lower throughput and higher latency
C) No trade-offs
D) Reduced message size

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-52)

### Question 53

**Why does Kafka use schemas?**

A) To slow down processing
B) To decouple writing and reading messages
C) To increase message size
D) To limit producers

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-53)

### Question 54

**What happens when a partition is replicated?**

A) Messages are encrypted
B) Additional brokers store copies for redundancy
C) Consumers receive duplicate messages
D) Producers send messages twice

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-54)

### Question 55

**Where must producers connect to publish messages?**

A) To any broker
B) To the partition leader
C) To the cluster controller
D) To the consumer

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-55)

### Question 56

**Can consumers fetch from partition followers?**

A) No, never allowed
B) Yes, consumers may fetch from leader or followers
C) Only on weekends
D) Only for small messages

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-56)

### Question 57

**What is a use case for Kafka mentioned in the chapter?**

A) Operating system replacement
B) Activity tracking, messaging, metrics and logging, stream processing
C) Web browser
D) Spreadsheet application


[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-57)

### Question 58

**What problem did LinkedIn face before Kafka?**

A) Too much automation
B) Fragmented systems for metrics and activity tracking with poor scalability
C) No employees
D) Too few applications

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-58)

### Question 59

**What format did LinkedIn originally use for activity tracking?**

A) JSON
B) XML
C) Binary
D) CSV

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-59)

### Question 60

**According to Jay Kreps, why is Kafka named after Franz Kafka?**

A) Deep symbolic meaning
B) Kafka was a writer, and the system is optimized for writing
C) It was a client's request
D) Random name generator

[solution](../chapter-tests-solutions/chapter-01-solutions.md/#answer-60)

---

## Answer Key
[View detailed solutions and explanations](../chapter-tests-solutions/chapter-01-solutions.md)

---

**Note:** This practice test is designed to help you prepare for the CCDAK certification exam. Make sure to review the Kafka documentation and the official Confluent study guide for comprehensive preparation.