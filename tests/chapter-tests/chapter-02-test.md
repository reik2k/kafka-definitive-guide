# Chapter 2: Installing Kafka - CCDAK Practice Test

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 2

**CCDAK Practice Test - 60 Questions**
**Time Limit: 90 minutes**
**Passing Score: 70%**

[View Solutions](../chapter-tests-solutions/chapter-02-solutions.md) | [Main README](../../README.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

## Questions

### Question 1

**What is the recommended operating system for running Kafka in production?**

A) Windows
B) macOS
C) Linux
D) Any operating system

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-1)

### Question 2

**Which Java versions are supported by the latest versions of Kafka?**

A) Java 6 and 7
B) Java 8 and 11
C) Java 11 only
D) Any Java version

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-2)

### Question 3

**What is Apache ZooKeeper used for in a Kafka cluster?**

A) To process messages
B) To store metadata about the Kafka cluster and consumer client details
C) To produce messages
D) To consume messages

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-3)

### Question 4

**Which ZooKeeper version is mentioned as tested with Kafka?**

A) 3.4.x
B) 3.5.9
C) 4.0.x
D) 2.8.x

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-4)

### Question 5

**In a ZooKeeper ensemble, how many nodes can fail in a five-node cluster while still maintaining quorum?**

A) 1 node
B) 2 nodes
C) 3 nodes
D) 4 nodes

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-5)

### Question 6

**Why is an odd number of servers recommended for a ZooKeeper ensemble?**

A) For better performance
B) Due to the balancing algorithm used for quorum
C) To reduce costs
D) It's not recommended

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-6)

### Question 7

**What does the initLimit parameter in ZooKeeper configuration control?**

A) The client port number
B) The amount of time followers have to connect with a leader
C) The broker ID

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-7)
D) The message retention time

### Question 8

**What does the syncLimit parameter specify in ZooKeeper?**

A) The amount of time out-of-sync followers can be with the leader
B) The replication factor
C) The partition count
D) The consumer offset

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-8)

### Question 9

**What command can verify that ZooKeeper is running correctly?**

A) ping
B) srvr (four-letter command via telnet)
C) status
D) check

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-9)

### Question 10

**What is the default Kafka broker port?**

A) 8080
B) 2181
C) 9092
D) 3000

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-10)

### Question 11

**Which configuration parameter sets the unique identifier for each Kafka broker?**

A) broker.name
B) broker.id
C) server.id
D) node.id

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-11)

### Question 12

**What is the purpose of the listeners configuration in Kafka?**

A) To set the broker ID
B) To specify the URIs and ports that Kafka listens on
C) To configure ZooKeeper
D) To set retention policies

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-12)

### Question 13

**What format is used for the zookeeper.connect parameter?**

A) hostname only
B) hostname:port/path
C) IP address only
D) port number only

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-13)

### Question 14

**What is a chroot path in ZooKeeper configuration?**

A) The root user's home directory
B) A path that acts as the root directory for a Kafka cluster
C) The default data directory
D) A backup location

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-14)

### Question 15

**What is the purpose of using a chroot path for Kafka in ZooKeeper?**

A) To improve performance
B) To allow ZooKeeper ensemble sharing with other applications without conflicts
C) To increase storage
D) To reduce network traffic

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-15)

### Question 16

**What configuration specifies where Kafka persists log segments?**

A) log.file
B) log.dirs
C) data.dir
D) storage.path

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-16)

### Question 17

**How does Kafka distribute partitions when multiple log.dirs are specified?**

A) Round-robin distribution
B) Based on available disk space
C) Least-used fashion (path with least number of partitions)
D) Randomly

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-17)

### Question 18

**What is the purpose of num.recovery.threads.per.data.dir?**

A) To set consumer thread count
B) To configure threads for opening, checking, and closing log segments
C) To set producer connections
D) To configure replication threads

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-18)

### Question 19

**When should auto.create.topics.enable be set to false?**

A) In development environments
B) When managing topic creation explicitly
C) Always

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-19)
D) Never

### Question 20

**What does auto.leader.rebalance.enable control?**

A) Consumer group rebalancing
B) Topic partition leadership rebalancing
C) ZooKeeper connections
D) Message routing

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-20)

### Question 21

**What is the default number of partitions for a new topic?**

A) 0
B) 1
C) 3

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-21)
D) 10

### Question 22

**Can the number of partitions for a topic be decreased?**

A) Yes, at any time
B) No, partitions can only be increased

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-22)
C) Yes, but only if no data exists
D) Yes, with admin privileges

### Question 23

**What is the recommended minimum replication factor?**

A) 1
B) At least 1 above min.insync.replicas
C) 5
D) 10

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-23)

### Question 24

**What does the log.retention.ms parameter control?**

A) Message size
B) How long Kafka retains messages
C) Producer timeout

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-24)
D) Consumer lag

### Question 25

**What is the default retention time for Kafka messages?**

A) 1 day
B) 1 week (168 hours)

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-25)
C) 1 month
D) Infinite

### Question 26

**How is retention by time performed?**

A) By message count

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-26)
B) By examining the last modified time on log segment files
C) By consumer offset
D) By producer timestamp

### Question 27

**What does log.retention.bytes control?**

A) Total cluster storage
B) Maximum message size
C) Total bytes of messages retained per partition
D) Broker memory allocation

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-27)

### Question 28

**What is the default size for log.segment.bytes?**

A) 100 MB
B) 500 MB

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-28)
C) 1 GB
D) 10 GB

### Question 29

**When can a log segment be considered for expiration?**

A) As soon as it's created
B) While it's being written to

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-29)
C) Only after it has been closed
D) After being replicated

### Question 30

**What does min.insync.replicas ensure?**

A) Maximum replication speed
B) Minimum number of in-sync replicas for a write to be successful
C) Consumer throughput
D) Producer latency

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-30)

### Question 31

**What is the default maximum message size (message.max.bytes)?**

A) 100 KB
B) 500 KB

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-31)
C) 1 MB
D) 10 MB

### Question 32

**What must be coordinated with message.max.bytes on the broker?**

A) log.retention.ms
B) fetch.message.max.bytes on consumers

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-32)
C) num.partitions
D) broker.id

### Question 33

**Which disk type typically provides better performance for Kafka?**

A) HDD (Hard Disk Drive)
B) SSD (Solid-State Disk)
C) Network-attached storage
D) USB drives

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-33)

### Question 34

**Why is more memory beneficial for Kafka?**

A) For storing messages
B) For better page cache performance, improving consumer reads
C) For ZooKeeper connections

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-34)
D) For producer connections

### Question 35

**What is a reasonable heap size for a Kafka broker?**

A) 1 GB
B) 5 GB

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-35)
C) 50 GB
D) 100 GB

### Question 36

**Why is 10 Gb NIC recommended for Kafka?**

A) To prevent network saturation

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-36)
B) For better security
C) To reduce costs
D) It's not recommended

### Question 37

**What becomes a bottleneck when scaling Kafka to very large sizes?**

A) Network only
B) Disk only
C) CPU (for decompression and recompression)
D) Memory only

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-37)

### Question 38

**What is a good starting VM type in Microsoft Azure for smaller Kafka clusters?**

A) Standard A1
B) Standard D16s v3
C) Basic A0
D) Standard F2

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-38)

### Question 39

**What are common AWS instance types for Kafka?**

A) t2.micro and t2.small
B) m4 or r3
C) p3.xlarge

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-39)
D) g4dn.xlarge

### Question 40

**What two requirements must all brokers in a cluster meet?**

A) Same hardware and same location
B) Same zookeeper.connect and unique broker.id
C) Same IP address range and same subnet
D) Same replication factor and same partition count

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-40)

### Question 41

**What should vm.swappiness be set to for Kafka?**

A) 0
B) 1
C) 50

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-41)
D) 100

### Question 42

**Why not set vm.swappiness to 0?**

A) It causes errors
B) Starting from Linux kernel 3.5-rc1, 0 means "never swap under any circumstances"
C) It's too slow
D) It uses too much memory

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-42)

### Question 43

**What does vm.dirty_background_ratio control?**

A) Network buffer size
B) Percentage of system memory for dirty pages before flushing to disk
C) CPU allocation

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-43)
D) ZooKeeper timeout

### Question 44

**Which filesystem is recommended for Kafka log segments?**

A) FAT32
B) NTFS
C) XFS
D) exFAT

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-44)

### Question 45

**What mount option is recommended for the log segment mount point?**

A) sync
B) noatime
C) async
D) defaults

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-45)

### Question 46

**Why use the noatime mount option?**

A) To improve security
B) To prevent unnecessary disk writes from access time updates
C) To enable compression
D) To increase partition count

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-46)

### Question 47

**What should net.core.wmem_max be set to for better network performance?**

A) 131072 (128 KiB)
B) 2097152 (2 MiB)
C) 10485760 (10 MiB)
D) 65536 (64 KiB)

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-47)

### Question 48

**What garbage collector is now recommended for Kafka?**

A) Serial GC
B) Parallel GC
C) G1GC (Garbage-First)
D) CMS (Concurrent Mark Sweep)

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-48)

### Question 49

**What does MaxGCPauseMillis specify in G1GC?**

A) Maximum heap size
B) Preferred pause time for each garbage collection cycle
C) Minimum memory allocation

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-49)
D) Thread pool size

### Question 50

**What is the default MaxGCPauseMillis value?**

A) 20 ms
B) 100 ms
C) 200 ms
D) 500 ms

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-50)

### Question 51

**What configuration makes Kafka rack-aware?**

A) datacenter.id
B) broker.rack
C) rack.location
D) zone.id

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-51)

### Question 52

**Why configure broker.rack?**

A) To improve performance
B) To ensure replicas for a partition don't share the same rack
C) To reduce network traffic
D) To increase storage capacity

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-52)

### Question 53

**Should Kafka be colocated with other significant applications?**

A) Yes, always
B) No, it reduces page cache performance
C) Yes, for cost savings
D) Only in production

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-53)

### Question 54

**How many partition replicas per broker are currently recommended?**

A) 1,000
B) 4,000
C) 14,000
D) 50,000

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-54)

### Question 55

**How many partition replicas per cluster are currently recommended?**

A) 100,000
B) 200,000
C) 500,000
D) 1,000,000

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-55)

### Question 56

**What command-line option has replaced --zookeeper in Kafka CLI tools?**

A) --cluster
B) --bootstrap-server
C) --broker
D) --server

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-56)

### Question 57

**Why has the --zookeeper option been deprecated?**

A) ZooKeeper is no longer used
B) Direct broker connections are now preferred to reduce ZooKeeper dependency
C) It was causing errors
D) It's too slow

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-57)

### Question 58

**What Kafka version introduced early access to ZooKeeper-less Kafka?**

A) 2.0.0
B) 2.5.0
C) 2.8.0
D) 3.0.0

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-58)

### Question 59

**Where should consumers commit offsets?**

A) To ZooKeeper only
B) To local files
C) To Kafka itself (recommended)
D) To external databases

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-59)

### Question 60

**What happens to a log segment when it reaches the size specified by log.segment.bytes?**

A) It is deleted
B) It is closed and a new one is opened
C) It is compressed
D) It is replicated

[solution](../chapter-tests-solutions/chapter-02-solutions.md/#answer-60)

---

## Answer Key
[View detailed solutions and explanations](../chapter-tests-solutions/chapter-02-solutions.md)

---

**Note:** This practice test covers installation, configuration, hardware selection, and production considerations for Apache Kafka. Review Chapter 2 and official Kafka documentation for comprehensive preparation.