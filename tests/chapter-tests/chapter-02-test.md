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

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#1.-c)-linux)

### Question 2

**Which Java versions are supported by the latest versions of Kafka?**

A) Java 6 and 7  
B) Java 8 and 11  
C) Java 11 only  
D) Any Java version

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#2.-b)-java-8-and-11)

### Question 3

**What is Apache ZooKeeper used for in a Kafka cluster?**

A) To process messages  
B) To store metadata about the Kafka cluster and consumer client details  
C) To produce messages  
D) To consume messages

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#3.-b)-to-store-metadata-about-the-kafka-cluster-and-consumer-client-details)

### Question 4

**Which ZooKeeper version is mentioned as tested with Kafka?**

A) 3.4.x  
B) 3.5.9  
C) 4.0.x  
D) 2.8.x

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#4.-b)-3.5.9)

### Question 5

**In a ZooKeeper ensemble, how many nodes can fail in a five-node cluster while still maintaining quorum?**

A) 1 node  
B) 2 nodes  
C) 3 nodes  
D) 4 nodes

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#5.-c)-3-nodes)

### Question 6

**Why is an odd number of servers recommended for a ZooKeeper ensemble?**

A) For better performance  
B) Due to the balancing algorithm used for quorum  
C) To reduce costs  
D) It's not recommended

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#6.-b)-due-to-the-balancing-algorithm-used-for-quorum)

### Question 7

**What does the initLimit parameter in ZooKeeper configuration control?**

A) The client port number  
B) The amount of time followers have to connect with a leader  
C) The broker ID  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#7.-b)-the-amount-of-time-followers-have-to-connect-with-a-leader)
D) The message retention time

### Question 8

**What does the syncLimit parameter specify in ZooKeeper?**

A) The amount of time out-of-sync followers can be with the leader  
B) The replication factor  
C) The partition count  
D) The consumer offset

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#8.-a)-the-amount-of-time-out-of-sync-followers-can-be-with-the-leader)

### Question 9

**What command can verify that ZooKeeper is running correctly?**

A) ping  
B) srvr (four-letter command via telnet)  
C) status  
D) check

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#9.-d)-check)

### Question 10

**What is the default Kafka broker port?**

A) 8080  
B) 2181  
C) 9092  
D) 3000

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#10.-c)-9092)

### Question 11

**Which configuration parameter sets the unique identifier for each Kafka broker?**

A) broker.name  
B) broker.id  
C) server.id  
D) node.id

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#11.-b)-broker.id)

### Question 12

**What is the purpose of the listeners configuration in Kafka?**

A) To set the broker ID  
B) To specify the URIs and ports that Kafka listens on  
C) To configure ZooKeeper  
D) To set retention policies

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#12.-b)-to-specify-the-uris-and-ports-that-kafka-listens-on)

### Question 13

**What format is used for the zookeeper.connect parameter?**

A) hostname only  
B) hostname:port/path  
C) IP address only  
D) port number only

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#13.-b)-hostnamepor tpath)

### Question 14

**What is a chroot path in ZooKeeper configuration?**

A) The root user's home directory  
B) A path that acts as the root directory for a Kafka cluster  
C) The default data directory  
D) A backup location

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#14.-c)-the-default-data-directory)

### Question 15

**What is the purpose of using a chroot path for Kafka in ZooKeeper?**

A) To improve performance  
B) To allow ZooKeeper ensemble sharing with other applications without conflicts  
C) To increase storage  
D) To reduce network traffic

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#15.-b)-to-allow-zookeeper-ensemble-sharing-with-other-applications-without-conflicts)

### Question 16

**What configuration specifies where Kafka persists log segments?**

A) log.file  
B) log.dirs  
C) data.dir  
D) storage.path

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#16.-c)-data.dir)

### Question 17

**How does Kafka distribute partitions when multiple log.dirs are specified?**

A) Round-robin distribution  
B) Based on available disk space  
C) Least-used fashion (path with least number of partitions)  
D) Randomly

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#17.-b)-based-on-available-disk-space)

### Question 18

**What is the purpose of num.recovery.threads.per.data.dir?**

A) To set consumer thread count  
B) To configure threads for opening, checking, and closing log segments  
C) To set producer connections  
D) To configure replication threads

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#18.-b)-to-configure-threads-for-opening-checking-and-closing-log-segments)

### Question 19

**When should auto.create.topics.enable be set to false?**

A) In development environments  
B) When managing topic creation explicitly  
C) Always  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#19.-b)-when-managing-topic-creation-explicitly)
D) Never

### Question 20

**What does auto.leader.rebalance.enable control?**

A) Consumer group rebalancing  
B) Topic partition leadership rebalancing  
C) ZooKeeper connections  
D) Message routing

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#20.-b)-topic-partition-leadership-rebalancing)

### Question 21

**What is the default number of partitions for a new topic?**

A) 0  
B) 1  
C) 3  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#21.-b)-1)
D) 10

### Question 22

**Can the number of partitions for a topic be decreased?**

A) Yes, at any time  
B) No, partitions can only be increased  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#22.-c)-yes-but-only-if-no-data-exists)
C) Yes, but only if no data exists  
D) Yes, with admin privileges

### Question 23

**What is the recommended minimum replication factor?**

A) 1  
B) At least 1 above min.insync.replicas  
C) 5  
D) 10

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#23.-c)-5)

### Question 24

**What does the log.retention.ms parameter control?**

A) Message size  
B) How long Kafka retains messages  
C) Producer timeout  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#24.-b)-how-long-kafka-retains-messages)
D) Consumer lag

### Question 25

**What is the default retention time for Kafka messages?**

A) 1 day  
B) 1 week (168 hours)  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#25.-b)-1-week-168-hours)
C) 1 month  
D) Infinite

### Question 26

**How is retention by time performed?**

A) By message count  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#26.-b)-by-examining-the-last-modified-time-on-log-segment-files)
B) By examining the last modified time on log segment files  
C) By consumer offset  
D) By producer timestamp

### Question 27

**What does log.retention.bytes control?**

A) Total cluster storage  
B) Maximum message size  
C) Total bytes of messages retained per partition  
D) Broker memory allocation

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#27.-c)-total-bytes-of-messages-retained-per-partition)

### Question 28

**What is the default size for log.segment.bytes?**

A) 100 MB  
B) 500 MB  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#28.-d)-10-gb)
C) 1 GB  
D) 10 GB

### Question 29

**When can a log segment be considered for expiration?**

A) As soon as it's created  
B) While it's being written to  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#29.-c)-only-after-it-has-been-closed)
C) Only after it has been closed  
D) After being replicated

### Question 30

**What does min.insync.replicas ensure?**

A) Maximum replication speed  
B) Minimum number of in-sync replicas for a write to be successful  
C) Consumer throughput  
D) Producer latency

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#30.-b)-minimum-number-of-in-sync-replicas-for-a-write-to-be-successful)

### Question 31

**What is the default maximum message size (message.max.bytes)?**

A) 100 KB  
B) 500 KB  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#31.-c)-1-mb)
C) 1 MB  
D) 10 MB

### Question 32

**What must be coordinated with message.max.bytes on the broker?**

A) log.retention.ms  
B) fetch.message.max.bytes on consumers  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#32.-b)-fetch.message.max.bytes-on-consumers)
C) num.partitions  
D) broker.id

### Question 33

**Which disk type typically provides better performance for Kafka?**

A) HDD (Hard Disk Drive)  
B) SSD (Solid-State Disk)  
C) Network-attached storage  
D) USB drives

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#33.-b)-ssd-solid-state-disk)

### Question 34

**Why is more memory beneficial for Kafka?**

A) For storing messages  
B) For better page cache performance, improving consumer reads  
C) For ZooKeeper connections  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#34.-b)-for-better-page-cache-performance-improving-consumer-reads)
D) For producer connections

### Question 35

**What is a reasonable heap size for a Kafka broker?**

A) 1 GB  
B) 5 GB  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#35.-b)-5-gb)
C) 50 GB  
D) 100 GB

### Question 36

**Why is 10 Gb NIC recommended for Kafka?**

A) To prevent network saturation  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#36.-a)-to-prevent-network-saturation)
B) For better security  
C) To reduce costs  
D) It's not recommended

### Question 37

**What becomes a bottleneck when scaling Kafka to very large sizes?**

A) Network only  
B) Disk only  
C) CPU (for decompression and recompression)  
D) Memory only

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#37.-b)-disk-only)

### Question 38

**What is a good starting VM type in Microsoft Azure for smaller Kafka clusters?**

A) Standard A1  
B) Standard D16s v3  
C) Basic A0  
D) Standard F2

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#38.-a)-standard-a1)

### Question 39

**What are common AWS instance types for Kafka?**

A) t2.micro and t2.small  
B) m4 or r3  
C) p3.xlarge  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#39.-a)-t2.micro-and-t2.small)
D) g4dn.xlarge

### Question 40

**What two requirements must all brokers in a cluster meet?**

A) Same hardware and same location  
B) Same zookeeper.connect and unique broker.id  
C) Same IP address range and same subnet  
D) Same replication factor and same partition count

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#40.-d)-same-replication-factor-and-same-partition-count)

### Question 41

**What should vm.swappiness be set to for Kafka?**

A) 0  
B) 1  
C) 50  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#41.-b)-1)
D) 100

### Question 42

**Why not set vm.swappiness to 0?**

A) It causes errors  
B) Starting from Linux kernel 3.5-rc1, 0 means "never swap under any circumstances"  
C) It's too slow  
D) It uses too much memory

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#42.-b)-starting-from-linux-kernel-3.5-rc1-0-means-never-swap-under-any-circumstances)

### Question 43

**What does vm.dirty_background_ratio control?**

A) Network buffer size  
B) Percentage of system memory for dirty pages before flushing to disk  
C) CPU allocation  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#43.-b)-percentage-of-system-memory-for-dirty-pages-before-flushing-to-disk)
D) ZooKeeper timeout

### Question 44

**Which filesystem is recommended for Kafka log segments?**

A) FAT32  
B) NTFS  
C) XFS  
D) exFAT

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#44.-c)-xfs)

### Question 45

**What mount option is recommended for the log segment mount point?**

A) sync  
B) noatime  
C) async  
D) defaults

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#45.-b)-noatime)

### Question 46

**Why use the noatime mount option?**

A) To improve security  
B) To prevent unnecessary disk writes from access time updates  
C) To enable compression  
D) To increase partition count

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#46.-b)-to-prevent-unnecessary-disk-writes-from-access-time-updates)

### Question 47

**What should net.core.wmem_max be set to for better network performance?**

A) 131072 (128 KiB)  
B) 2097152 (2 MiB)  
C) 10485760 (10 MiB)  
D) 65536 (64 KiB)

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#47.-a)-131072-128-kib)

### Question 48

**What garbage collector is now recommended for Kafka?**

A) Serial GC  
B) Parallel GC  
C) G1GC (Garbage-First)  
D) CMS (Concurrent Mark Sweep)

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#48.-c)-g1gc-garbage-first)

### Question 49

**What does MaxGCPauseMillis specify in G1GC?**

A) Maximum heap size  
B) Preferred pause time for each garbage collection cycle  
C) Minimum memory allocation  

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#49.-b)-preferred-pause-time-for-each-garbage-collection-cycle)
D) Thread pool size

### Question 50

**What is the default MaxGCPauseMillis value?**

A) 20 ms  
B) 100 ms  
C) 200 ms  
D) 500 ms

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#50.-c)-200-ms)

### Question 51

**What configuration makes Kafka rack-aware?**

A) datacenter.id  
B) broker.rack  
C) rack.location  
D) zone.id

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#51.-b)-broker.rack)

### Question 52

**Why configure broker.rack?**

A) To improve performance  
B) To ensure replicas for a partition don't share the same rack  
C) To reduce network traffic  
D) To increase storage capacity

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#52.-b)-to-ensure-replicas-for-a-partition-dont-share-the-same-rack)

### Question 53

**Should Kafka be colocated with other significant applications?**

A) Yes, always  
B) No, it reduces page cache performance  
C) Yes, for cost savings  
D) Only in production

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#53.-d)-only-in-production)

### Question 54

**How many partition replicas per broker are currently recommended?**

A) 1,000  
B) 4,000  
C) 14,000  
D) 50,000

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#54.-c)-14000)

### Question 55

**How many partition replicas per cluster are currently recommended?**

A) 100,000  
B) 200,000  
C) 500,000  
D) 1,000,000

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#55.-b)-200000)

### Question 56

**What command-line option has replaced --zookeeper in Kafka CLI tools?**

A) --cluster  
B) --bootstrap-server  
C) --broker  
D) --server

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#56.-d)-server)

### Question 57

**Why has the --zookeeper option been deprecated?**

A) ZooKeeper is no longer used  
B) Direct broker connections are now preferred to reduce ZooKeeper dependency  
C) It was causing errors  
D) It's too slow

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#57.-b)-direct-broker-connections-are-now-preferred-to-reduce-zookeeper-dependency)

### Question 58

**What Kafka version introduced early access to ZooKeeper-less Kafka?**

A) 2.0.0  
B) 2.5.0  
C) 2.8.0  
D) 3.0.0

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#58.-c)-2.8.0)

### Question 59

**Where should consumers commit offsets?**

A) To ZooKeeper only  
B) To local files  
C) To Kafka itself (recommended)  
D) To external databases

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#59.-c)-to-kafka-itself-recommended)

### Question 60

**What happens to a log segment when it reaches the size specified by log.segment.bytes?**

A) It is deleted  
B) It is closed and a new one is opened  
C) It is compressed  
D) It is replicated

[solution](../solutions/chapter-tests/chapter-02-solutions.md/#60.-b)-it-is-closed-and-a-new-one-is-opened)

---

## Answer Key
[View detailed solutions and explanations](../chapter-tests-solutions/chapter-02-solutions.md)

---

**Note:** This practice test covers installation, configuration, hardware selection, and production considerations for Apache Kafka. Review Chapter 2 and official Kafka documentation for comprehensive preparation.