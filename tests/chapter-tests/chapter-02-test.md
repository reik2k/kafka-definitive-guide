# Chapter 2: Installing Kafka - CCDAK Practice Test

**Total Questions: 60**  
**Time Limit: 90 minutes**  
**Passing Score: 70%**

[View Solutions](../chapter-tests-solutions/chapter-02-solutions.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

## Questions

### 1. What is the recommended operating system for running Kafka in production?
A) Windows  
B) macOS  
C) Linux  
D) Any operating system

### 2. Which Java versions are supported by the latest versions of Kafka?
A) Java 6 and 7  
B) Java 8 and 11  
C) Java 11 only  
D) Any Java version

### 3. What is Apache ZooKeeper used for in a Kafka cluster?
A) To process messages  
B) To store metadata about the Kafka cluster and consumer client details  
C) To produce messages  
D) To consume messages

### 4. Which ZooKeeper version is mentioned as tested with Kafka?
A) 3.4.x  
B) 3.5.9  
C) 4.0.x  
D) 2.8.x

### 5. In a ZooKeeper ensemble, how many nodes can fail in a five-node cluster while still maintaining quorum?
A) 1 node  
B) 2 nodes  
C) 3 nodes  
D) 4 nodes

### 6. Why is an odd number of servers recommended for a ZooKeeper ensemble?
A) For better performance  
B) Due to the balancing algorithm used for quorum  
C) To reduce costs  
D) It's not recommended

### 7. What does the initLimit parameter in ZooKeeper configuration control?
A) The client port number  
B) The amount of time followers have to connect with a leader  
C) The broker ID  
D) The message retention time

### 8. What does the syncLimit parameter specify in ZooKeeper?
A) The amount of time out-of-sync followers can be with the leader  
B) The replication factor  
C) The partition count  
D) The consumer offset

### 9. What command can verify that ZooKeeper is running correctly?
A) ping  
B) srvr (four-letter command via telnet)  
C) status  
D) check

### 10. What is the default Kafka broker port?
A) 8080  
B) 2181  
C) 9092  
D) 3000

### 11. Which configuration parameter sets the unique identifier for each Kafka broker?
A) broker.name  
B) broker.id  
C) server.id  
D) node.id

### 12. What is the purpose of the listeners configuration in Kafka?
A) To set the broker ID  
B) To specify the URIs and ports that Kafka listens on  
C) To configure ZooKeeper  
D) To set retention policies

### 13. What format is used for the zookeeper.connect parameter?
A) hostname only  
B) hostname:port/path  
C) IP address only  
D) port number only

### 14. What is a chroot path in ZooKeeper configuration?
A) The root user's home directory  
B) A path that acts as the root directory for a Kafka cluster  
C) The default data directory  
D) A backup location

### 15. What is the purpose of using a chroot path for Kafka in ZooKeeper?
A) To improve performance  
B) To allow ZooKeeper ensemble sharing with other applications without conflicts  
C) To increase storage  
D) To reduce network traffic

### 16. What configuration specifies where Kafka persists log segments?
A) log.file  
B) log.dirs  
C) data.dir  
D) storage.path

### 17. How does Kafka distribute partitions when multiple log.dirs are specified?
A) Round-robin distribution  
B) Based on available disk space  
C) Least-used fashion (path with least number of partitions)  
D) Randomly

### 18. What is the purpose of num.recovery.threads.per.data.dir?
A) To set consumer thread count  
B) To configure threads for opening, checking, and closing log segments  
C) To set producer connections  
D) To configure replication threads

### 19. When should auto.create.topics.enable be set to false?
A) In development environments  
B) When managing topic creation explicitly  
C) Always  
D) Never

### 20. What does auto.leader.rebalance.enable control?
A) Consumer group rebalancing  
B) Topic partition leadership rebalancing  
C) ZooKeeper connections  
D) Message routing

### 21. What is the default number of partitions for a new topic?
A) 0  
B) 1  
C) 3  
D) 10

### 22. Can the number of partitions for a topic be decreased?
A) Yes, at any time  
B) No, partitions can only be increased  
C) Yes, but only if no data exists  
D) Yes, with admin privileges

### 23. What is the recommended minimum replication factor?
A) 1  
B) At least 1 above min.insync.replicas  
C) 5  
D) 10

### 24. What does the log.retention.ms parameter control?
A) Message size  
B) How long Kafka retains messages  
C) Producer timeout  
D) Consumer lag

### 25. What is the default retention time for Kafka messages?
A) 1 day  
B) 1 week (168 hours)  
C) 1 month  
D) Infinite

### 26. How is retention by time performed?
A) By message count  
B) By examining the last modified time on log segment files  
C) By consumer offset  
D) By producer timestamp

### 27. What does log.retention.bytes control?
A) Total cluster storage  
B) Maximum message size  
C) Total bytes of messages retained per partition  
D) Broker memory allocation

### 28. What is the default size for log.segment.bytes?
A) 100 MB  
B) 500 MB  
C) 1 GB  
D) 10 GB

### 29. When can a log segment be considered for expiration?
A) As soon as it's created  
B) While it's being written to  
C) Only after it has been closed  
D) After being replicated

### 30. What does min.insync.replicas ensure?
A) Maximum replication speed  
B) Minimum number of in-sync replicas for a write to be successful  
C) Consumer throughput  
D) Producer latency

### 31. What is the default maximum message size (message.max.bytes)?
A) 100 KB  
B) 500 KB  
C) 1 MB  
D) 10 MB

### 32. What must be coordinated with message.max.bytes on the broker?
A) log.retention.ms  
B) fetch.message.max.bytes on consumers  
C) num.partitions  
D) broker.id

### 33. Which disk type typically provides better performance for Kafka?
A) HDD (Hard Disk Drive)  
B) SSD (Solid-State Disk)  
C) Network-attached storage  
D) USB drives

### 34. Why is more memory beneficial for Kafka?
A) For storing messages  
B) For better page cache performance, improving consumer reads  
C) For ZooKeeper connections  
D) For producer connections

### 35. What is a reasonable heap size for a Kafka broker?
A) 1 GB  
B) 5 GB  
C) 50 GB  
D) 100 GB

### 36. Why is 10 Gb NIC recommended for Kafka?
A) To prevent network saturation  
B) For better security  
C) To reduce costs  
D) It's not recommended

### 37. What becomes a bottleneck when scaling Kafka to very large sizes?
A) Network only  
B) Disk only  
C) CPU (for decompression and recompression)  
D) Memory only

### 38. What is a good starting VM type in Microsoft Azure for smaller Kafka clusters?
A) Standard A1  
B) Standard D16s v3  
C) Basic A0  
D) Standard F2

### 39. What are common AWS instance types for Kafka?
A) t2.micro and t2.small  
B) m4 or r3  
C) p3.xlarge  
D) g4dn.xlarge

### 40. What two requirements must all brokers in a cluster meet?
A) Same hardware and same location  
B) Same zookeeper.connect and unique broker.id  
C) Same IP address range and same subnet  
D) Same replication factor and same partition count

### 41. What should vm.swappiness be set to for Kafka?
A) 0  
B) 1  
C) 50  
D) 100

### 42. Why not set vm.swappiness to 0?
A) It causes errors  
B) Starting from Linux kernel 3.5-rc1, 0 means "never swap under any circumstances"  
C) It's too slow  
D) It uses too much memory

### 43. What does vm.dirty_background_ratio control?
A) Network buffer size  
B) Percentage of system memory for dirty pages before flushing to disk  
C) CPU allocation  
D) ZooKeeper timeout

### 44. Which filesystem is recommended for Kafka log segments?
A) FAT32  
B) NTFS  
C) XFS  
D) exFAT

### 45. What mount option is recommended for the log segment mount point?
A) sync  
B) noatime  
C) async  
D) defaults

### 46. Why use the noatime mount option?
A) To improve security  
B) To prevent unnecessary disk writes from access time updates  
C) To enable compression  
D) To increase partition count

### 47. What should net.core.wmem_max be set to for better network performance?
A) 131072 (128 KiB)  
B) 2097152 (2 MiB)  
C) 10485760 (10 MiB)  
D) 65536 (64 KiB)

### 48. What garbage collector is now recommended for Kafka?
A) Serial GC  
B) Parallel GC  
C) G1GC (Garbage-First)  
D) CMS (Concurrent Mark Sweep)

### 49. What does MaxGCPauseMillis specify in G1GC?
A) Maximum heap size  
B) Preferred pause time for each garbage collection cycle  
C) Minimum memory allocation  
D) Thread pool size

### 50. What is the default MaxGCPauseMillis value?
A) 20 ms  
B) 100 ms  
C) 200 ms  
D) 500 ms

### 51. What configuration makes Kafka rack-aware?
A) datacenter.id  
B) broker.rack  
C) rack.location  
D) zone.id

### 52. Why configure broker.rack?
A) To improve performance  
B) To ensure replicas for a partition don't share the same rack  
C) To reduce network traffic  
D) To increase storage capacity

### 53. Should Kafka be colocated with other significant applications?
A) Yes, always  
B) No, it reduces page cache performance  
C) Yes, for cost savings  
D) Only in production

### 54. How many partition replicas per broker are currently recommended?
A) 1,000  
B) 4,000  
C) 14,000  
D) 50,000

### 55. How many partition replicas per cluster are currently recommended?
A) 100,000  
B) 200,000  
C) 500,000  
D) 1,000,000

### 56. What command-line option has replaced --zookeeper in Kafka CLI tools?
A) --cluster  
B) --bootstrap-server  
C) --broker  
D) --server

### 57. Why has the --zookeeper option been deprecated?
A) ZooKeeper is no longer used  
B) Direct broker connections are now preferred to reduce ZooKeeper dependency  
C) It was causing errors  
D) It's too slow

### 58. What Kafka version introduced early access to ZooKeeper-less Kafka?
A) 2.0.0  
B) 2.5.0  
C) 2.8.0  
D) 3.0.0

### 59. Where should consumers commit offsets?
A) To ZooKeeper only  
B) To local files  
C) To Kafka itself (recommended)  
D) To external databases

### 60. What happens to a log segment when it reaches the size specified by log.segment.bytes?
A) It is deleted  
B) It is closed and a new one is opened  
C) It is compressed  
D) It is replicated

---

## Answer Key
[View detailed solutions and explanations](../chapter-tests-solutions/chapter-02-solutions.md)

---

**Note:** This practice test covers installation, configuration, hardware selection, and production considerations for Apache Kafka. Review Chapter 2 and official Kafka documentation for comprehensive preparation.