# Chapter 6: Kafka Internals — CCDAK Practice Test

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 6

**CCDAK Practice Test - 60 Questions**
**Time Limit: 90 minutes**  
**Passing Score: 70%**

[Link to Solutions](../../chapter-tests-solutions/chapter-06-solutions.md) | [Main README](../../README.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

### Question 1

**What system does Kafka use to maintain the list of brokers in a cluster?**

A) Consul
B) etcd
C) Apache ZooKeeper
D) Redis

### Question 2

**What type of node does a broker create in ZooKeeper when it starts?**

A) Persistent node
B) Ephemeral node
C) Sequential node
D) Temporary node

### Question 3

**What happens when a broker loses connectivity to ZooKeeper?**

A) The broker continues operating normally
B) The ephemeral node is automatically removed
C) Other brokers are immediately shut down
D) The broker ID is permanently deleted

### Question 4

**Which broker becomes the controller in a Kafka cluster?**

A) The broker with the highest ID
B) The first broker that starts in the cluster
C) The broker with the most resources
D) A randomly selected broker

### Question 5

**What is the controller's primary responsibility?**

A) Processing all produce requests
B) Electing partition leaders
C) Managing consumer groups
D) Storing cluster metadata

### Question 6

**How does the controller create itself in ZooKeeper?**

A) By creating a persistent node
B) By creating an ephemeral node called /controller
C) By updating broker configuration
D) By sending a request to all brokers

### Question 7

**What happens when other brokers try to create the controller node?**

A) They succeed and become co-controllers
B) They receive a "node already exists" exception
C) The cluster rejects them
D) They automatically become followers

### Question 8

**What is the purpose of the controller epoch number?**

A) To track uptime
B) To prevent split-brain scenarios with zombie controllers
C) To count the number of partitions
D) To measure performance

### Question 9

**When does a new controller get elected?**

A) Every hour automatically
B) When the current controller loses connectivity to ZooKeeper
C) When any broker restarts
D) When a new topic is created

### Question 10

**What is KRaft?**

A) A new compression algorithm
B) Kafka's new Raft-based controller replacing ZooKeeper
C) A monitoring tool
D) A consumer group protocol

### Question 11

**What are the two types of replicas in Kafka?**

A) Primary and Secondary
B) Master and Slave
C) Leader and Follower
D) Active and Passive

### Question 12

**Which replica handles all produce requests for a partition?**

A) Any available replica
B) The follower replica
C) The leader replica
D) All replicas simultaneously

### Question 13

**What is the main job of follower replicas?**

A) To serve all consumer requests
B) To replicate messages from the leader
C) To process produce requests
D) To manage partition assignment

### Question 14

**When can consumers read from follower replicas?**

A) Never
B) Only during leader failure
C) When configured with client.rack and appropriate broker settings
D) Always by default

### Question 15

**What feature allows consuming from follower replicas?**

A) KIP-300
B) KIP-392
C) KIP-500
D) KIP-631

### Question 16

**How do follower replicas stay in sync with the leader?**

A) By sending Produce requests
B) By sending Fetch requests
C) By reading from ZooKeeper
D) By polling a sync API

### Question 17

**What determines if a replica is considered in-sync?**

A) Network latency
B) Disk space available
C) Whether it has requested messages recently and is caught up
D) CPU utilization

### Question 18

**What configuration controls how long a replica can be inactive before being out of sync?**

A) replica.timeout.ms
B) replica.lag.time.max.ms
C) replica.sync.timeout.ms
D) replica.max.lag.ms

### Question 19

**What is the default value for replica.lag.time.max.ms?**

A) 5 seconds
B) 10 seconds
C) 30 seconds
D) 60 seconds

### Question 20

**What is a preferred leader?**

A) The replica with the most data
B) The replica that was leader when the topic was created
C) The replica on the broker with most resources
D) Any in-sync replica

### Question 21

**What configuration enables automatic preferred leader rebalancing?**

A) leader.rebalance.enable
B) auto.leader.rebalance.enable
C) preferred.leader.enable
D) leader.auto.rebalance

### Question 22

**What protocol does Kafka use for broker communication?**

A) HTTP
B) gRPC
C) Binary protocol over TCP
D) WebSockets

### Question 23

**How are client requests processed by brokers?**

A) In random order
B) By priority
C) In the order they were received
D) Asynchronously with no order guarantee

### Question 24

**What are the three main request types from clients?**

A) Start, Stop, Status
B) Metadata, Produce, Fetch
C) Connect, Send, Receive
D) Read, Write, Delete

### Question 25

**What must producers and consumers do before sending produce/fetch requests?**

A) Register with ZooKeeper
B) Send a metadata request to discover partition leaders
C) Authenticate with all brokers
D) Create a session

### Question 26

**What error occurs when a produce request is sent to a non-leader broker?**

A) InvalidBrokerException
B) NotLeaderForPartitionException
C) WrongBrokerException
D) LeaderNotFoundException

### Question 27

**How often do clients refresh metadata by default?**

A) Every 30 seconds
B) Every 60 seconds
C) Controlled by metadata.max.age.ms
D) Never, only when errors occur

### Question 28

**What does acks=1 mean for a produce request?**

A) Wait for all replicas to acknowledge
B) Wait for just the leader to acknowledge
C) Don't wait for any acknowledgment
D) Wait for one follower to acknowledge

### Question 29

**What does acks=all mean?**

A) Wait for the leader only
B) Wait for all brokers in the cluster
C) Wait for all in-sync replicas
D) Don't wait for acknowledgment

### Question 30

**Where are produce requests stored while waiting for all replicas to replicate?**

A) Request queue
B) Memory buffer
C) Purgatory
D) Response queue

### Question 31

**What is Kafka's zero-copy optimization used for?**

A) Producing messages
B) Sending messages from broker to consumers
C) Replication
D) Compression

### Question 32

**Why can clients set a lower boundary on fetch request data?**

A) To save bandwidth
B) To reduce CPU and network utilization on low-traffic topics
C) To improve compression
D) To increase throughput

### Question 33

**Which messages are available for consumers to read?**

A) All messages on the leader
B) Only messages replicated to all in-sync replicas
C) Only messages older than 1 second
D) All messages on any replica

### Question 34

**What is the high-water mark?**

A) Maximum partition size
B) The offset of the last message replicated to all in-sync replicas
C) The maximum number of consumers
D) Memory usage threshold

### Question 35

**What is a fetch session cache?**

A) Local consumer message cache
B) A cache storing partition lists to minimize metadata overhead
C) ZooKeeper connection cache
D) Leader election cache

### Question 36

**How many request types does Kafka protocol currently handle?**

A) 10
B) 25
C) 61
D) 100

### Question 37

**What is the basic storage unit of Kafka?**

A) Message
B) Batch
C) Partition replica
D) Topic

### Question 38

**What configuration defines directories for partition storage?**

A) data.dirs
B) log.dirs
C) storage.dirs
D) partition.dirs

### Question 39

**What is tiered storage in Kafka?**

A) Using different disk types
B) Configuring local and remote storage tiers
C) RAID configuration
D) Multi-datacenter replication

### Question 40

**What are the two tiers in Kafka's tiered storage?**

A) Hot and Cold
B) Local and Remote
C) Primary and Secondary
D) Fast and Slow

### Question 41

**What is typically stored in the remote tier?**

A) Active segments
B) Completed log segments
C) Index files only
D) Consumer offsets

### Question 42

**What is the main benefit of tiered storage?**

A) Faster writes
B) Better compression
C) Scaling storage independent of memory and CPU
D) Reduced network usage

### Question 43

**How does Kafka allocate partitions to brokers when creating a topic?**

A) Randomly
B) By available disk space
C) Round-robin with rack awareness
D) All partitions on one broker

### Question 44

**How does Kafka decide which directory to use for new partitions?**

A) Round-robin
B) Available disk space
C) Directory with fewest partitions
D) Randomly

### Question 45

**What are partition segments split by?**

A) Size or time limit
B) Number of messages
C) Consumer groups
D) Compression ratio

### Question 46

**What is the default segment size?**

A) 512 MB
B) 1 GB
C) 2 GB
D) 5 GB

### Question 47

**What is an active segment?**

A) The segment being written to
B) Any segment with messages
C) Segments with consumers reading
D) Recently created segments

### Question 48

**Can active segments be deleted?**

A) Yes, after 24 hours
B) No, never
C) Yes, if empty
D) Only during maintenance

### Question 49

**What message format version is current as of Kafka 0.11+?**

A) v0
B) v1
C) v2
D) v3

### Question 50

**What is the advantage of message batching?**

A) Faster processing
B) Better compression and reduced overhead
C) Simpler code
D) Guaranteed ordering

### Question 51

**What tool can be used to examine partition segments?**

A) kafka-console-consumer
B) kafka-topics.sh
C) DumpLogSegment
D) kafka-log-viewer

### Question 52

**What are the two types of indexes Kafka maintains?**

A) Hash and Tree
B) Offset-to-file and Timestamp-to-offset
C) Primary and Secondary
D) Forward and Reverse

### Question 53

**What happens if an index becomes corrupted?**

A) Data is lost
B) It gets regenerated from the log segment
C) Kafka fails to start
D) Manual recovery required

### Question 54

**What are the two retention policies for topics?**

A) Time and Size
B) Delete and Compact
C) Active and Passive
D) Local and Remote

### Question 55

**What does log compaction retain?**

A) All messages
B) Messages from the last hour
C) The most recent value for each key
D) Only messages with null values

### Question 56

**What are the two portions of a compacted log?**

A) Old and New
B) Clean and Dirty
C) Active and Inactive
D) Primary and Backup

### Question 57

**What is a tombstone message?**

A) A message with a null value used to delete a key
B) A corrupted message
C) The last message in a partition
D) An expired message

### Question 58

**What percentage of dirty records triggers compaction by default?**

A) 25%
B) 50%
C) 75%
D) 90%

### Question 59

**What configuration can guarantee minimum time before compaction?**

A) min.compaction.time.ms
B) min.compaction.lag.ms
C) compaction.min.lag.ms
D) log.compaction.min.ms

### Question 60

**When migrating to KRaft, what happens to ZooKeeper dependencies?**

A) They remain required
B) They are completely removed
C) They become optional
D) They are only needed for migration

---

**End of Test**

[Link to Solutions](../../chapter-tests-solutions/chapter-06-solutions.md)