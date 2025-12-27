# Chapter 2: Installing Kafka - Solutions
CCDAK Practice Test Solutions
**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 2

[Back to Test](../../chapter-tests/chapter-02-test.md) | [Main README](../../README.md)

---

## Answer Key

### Answer 1

1. C) Linux

**Explanation:** 

*Linux is the recommended OS for the general use case when running Kafka in production. While Kafka can run on Windows, macOS, and other operating systems, Linux provides the best performance and stability.*


### Answer 2

2. B) Java 8 and 11

**Explanation:** 

*The latest versions of Kafka support both Java 8 and Java 11. These are the recommended Java versions for running Kafka.*


### Answer 3

3. B) To store metadata about the Kafka cluster and consumer client details

**Explanation:** 

*ZooKeeper is used by Kafka for storing metadata about the brokers, topics, partitions, and consumer client details. It provides centralized configuration and synchronization.*


### Answer 4

4. B) 3.5.9

**Explanation:** 

*The chapter mentions using ZooKeeper 3.5.9, which has been tested extensively with Kafka.*


### Answer 5

5. B) 2 nodes

**Explanation:** 

*In a five-node ZooKeeper ensemble, you can run with two nodes missing while still maintaining quorum (3 out of 5).*


### Answer 6

6. B) Due to the balancing algorithm used for quorum

**Explanation:** 

*An odd number of servers is recommended because ZooKeeper requires a majority (quorum) to respond to requests. This makes odd numbers more efficient.*


### Answer 7

7. B) The amount of time followers have to connect with a leader

**Explanation:** 

*initLimit specifies the amount of time to allow followers to connect with a leader, measured in tickTime units.*


### Answer 8

8. A) The amount of time out-of-sync followers can be with the leader

**Explanation:** 

*syncLimit controls how long out-of-sync followers can be with the leader, also measured in tickTime units.*


### Answer 9

9. B) srvr (four-letter command via telnet)

**Explanation:** 

*You can verify ZooKeeper is running by connecting via telnet and sending the four-letter command "srvr", which returns basic ZooKeeper information.*


### Answer 10

10. C) 9092

**Explanation:** 

*The default Kafka broker port is 9092.*


### Answer 11

11. B) broker.id

**Explanation:** 

*The broker.id configuration parameter sets the unique integer identifier for each Kafka broker in a cluster.*


### Answer 12

12. B) To specify the URIs and ports that Kafka listens on

**Explanation:** 

*The listeners configuration is a comma-separated list of URIs that specifies the interfaces and ports Kafka listens on.*


### Answer 13

13. B) hostname:port/path

**Explanation:** 

*The zookeeper.connect parameter format is hostname:port/path, where path is an optional chroot.*


### Answer 14

14. B) A path that acts as the root directory for a Kafka cluster

**Explanation:** 

*A chroot path is designated to act as the root directory for a given Kafka cluster within ZooKeeper.*


### Answer 15

15. B) To allow ZooKeeper ensemble sharing with other applications without conflicts

**Explanation:** 

*Using a chroot path allows the ZooKeeper ensemble to be shared with other applications, including other Kafka clusters, without conflicts.*


### Answer 16

16. B) log.dirs

**Explanation:** 

*The log.dirs configuration specifies where Kafka persists log segments. It's a comma-separated list of paths.*


### Answer 17

17. C) Least-used fashion (path with least number of partitions)

**Explanation:** 

*When multiple log.dirs are specified, Kafka stores partitions in a "least-used" fashion, placing new partitions in the path with the least number of partitions.*


### Answer 18

18. B) To configure threads for opening, checking, and closing log segments

**Explanation:** 

*num.recovery.threads.per.data.dir configures the thread pool used for opening partitions' log segments during startup, checking and truncating during failure recovery, and closing log segments during shutdown.*


### Answer 19

19. B) When managing topic creation explicitly

**Explanation:** 

*auto.create.topics.enable should be set to false when you are managing topic creation explicitly, whether manually or through a provisioning system.*


### Answer 20

20. B) Topic partition leadership rebalancing

**Explanation:** 

*auto.leader.rebalance.enable ensures topic leadership is balanced across brokers by enabling a background thread that checks and rebalances partition leadership.*


### Answer 21

21. B) 1

**Explanation:** 

*The num.partitions parameter defaults to one partition for new topics.*


### Answer 22

22. B) No, partitions can only be increased

**Explanation:** 

*The number of partitions for a topic can only be increased, never decreased.*


### Answer 23

23. B) At least 1 above min.insync.replicas

**Explanation:** 

*It's recommended to set the replication factor to at least 1 above min.insync.replicas. For more fault-resistant settings, RF++ (2 above min.insync.replicas) is preferable.*


### Answer 24

24. B) How long Kafka retains messages

**Explanation:** 

*log.retention.ms controls how long Kafka will retain messages by time.*


### Answer 25

25. B) 1 week (168 hours)

**Explanation:** 

*The default retention time is 168 hours, or one week, specified by log.retention.hours.*


### Answer 26

26. B) By examining the last modified time on log segment files

**Explanation:** 

*Retention by time is performed by examining the last modified time (mtime) on each log segment file on disk.*


### Answer 27

27. C) Total bytes of messages retained per partition

**Explanation:** 

*log.retention.bytes controls the total number of bytes of messages retained per partition.*


### Answer 28

28. C) 1 GB

**Explanation:** 

*The default size for log.segment.bytes is 1 GB.*


### Answer 29

29. C) Only after it has been closed

**Explanation:** 

*A log segment can only be considered for expiration after it has been closed.*


### Answer 30

30. B) Minimum number of in-sync replicas for a write to be successful

**Explanation:** 

*min.insync.replicas ensures that at least a specified number of replicas are caught up and in sync for a write to be acknowledged.*


### Answer 31

31. C) 1 MB

**Explanation:** 

*The default maximum message size (message.max.bytes) is 1000000, or 1 MB.*


### Answer 32

32. B) fetch.message.max.bytes on consumers

**Explanation:** 

*The message size on the broker must be coordinated with fetch.message.max.bytes on consumer clients, otherwise consumers may fail to fetch larger messages.*


### Answer 33

33. B) SSD (Solid-State Disk)

**Explanation:** 

*SSDs provide drastically lower seek and access times and will provide the best performance for Kafka.*


### Answer 34

34. B) For better page cache performance, improving consumer reads

**Explanation:** 

*More memory allows the system to cache log segments in the page cache, resulting in faster reads for consumers.*


### Answer 35

35. B) 5 GB

**Explanation:** 

*A broker handling 150,000 messages per second can run with a 5 GB heap. Kafka doesn't need much heap memory.*


### Answer 36

36. A) To prevent network saturation

**Explanation:** 

*At least 10 Gb NICs are recommended to prevent the network from becoming saturated, especially with replication and mirroring.*


### Answer 37

37. C) CPU (for decompression and recompression)

**Explanation:** 

*When scaling Kafka to very large sizes, CPU becomes important because brokers must decompress message batches to validate checksums and assign offsets, then recompress them.*


### Answer 38

38. B) Standard D16s v3

**Explanation:** 

*Standard D16s v3 instances are mentioned as a good choice for smaller clusters in Azure.*


### Answer 39

39. B) m4 or r3

**Explanation:** 

*The m4 and r3 instance types are common choices for Kafka in AWS.*


### Answer 40

40. B) Same zookeeper.connect and unique broker.id

**Explanation:** 

*All brokers must have the same zookeeper.connect parameter and each must have a unique broker.id.*


### Answer 41

41. B) 1

**Explanation:** 

*vm.swappiness should be set to a very low value like 1 to avoid swapping while still providing a safety net.*


### Answer 42

42. B) Starting from Linux kernel 3.5-rc1, 0 means "never swap under any circumstances"

**Explanation:** 

*The meaning of vm.swappiness=0 changed in kernel 3.5-rc1 to mean "never swap under any circumstances" rather than "do not swap unless out-of-memory".*


### Answer 43

43. B) Percentage of system memory for dirty pages before flushing to disk

**Explanation:** 

*vm.dirty_background_ratio controls the percentage of total system memory that can be filled with dirty pages before the flush background process starts writing them to disk.*


### Answer 44

44. C) XFS

**Explanation:** 

*XFS is recommended as it outperforms Ext4 for most workloads with minimal tuning required.*


### Answer 45

45. B) noatime

**Explanation:** 

*The noatime mount option prevents atime (access time) updates, which generates unnecessary disk writes.*


### Answer 46

46. B) To prevent unnecessary disk writes from access time updates

**Explanation:** 

*Setting noatime prevents the last access time from being updated every time a file is read, reducing disk writes.*


### Answer 47

47. B) 2097152 (2 MiB)

**Explanation:** 

*A reasonable setting for net.core.wmem_max (maximum send buffer) is 2097152, or 2 MiB.*


### Answer 48

48. C) G1GC (Garbage-First)

**Explanation:** 

*G1GC is now recommended for Kafka as it automatically adjusts to different workloads and provides consistent pause times.*


### Answer 49

49. B) Preferred pause time for each garbage collection cycle

**Explanation:** 

*MaxGCPauseMillis specifies the preferred pause time for each garbage collection cycle (not a fixed maximum).*


### Answer 50

50. C) 200 ms

**Explanation:** 

*The default MaxGCPauseMillis value is 200 milliseconds.*


### Answer 51

51. B) broker.rack

**Explanation:** 

*The broker.rack configuration makes Kafka rack-aware, ensuring replicas don't share the same rack.*


### Answer 52

52. B) To ensure replicas for a partition don't share the same rack

**Explanation:** 

*Configuring broker.rack ensures that replicas for a single partition do not share a rack, improving fault tolerance.*


### Answer 53

53. B) No, it reduces page cache performance

**Explanation:** 

*Kafka should not be colocated with other significant applications as it would have to share page cache, decreasing consumer performance.*


### Answer 54

54. C) 14,000

**Explanation:** 

*Currently, in a well-configured environment, it's recommended to have no more than 14,000 partition replicas per broker.*


### Answer 55

55. D) 1,000,000

**Explanation:** 

*The current recommendation is no more than 1 million replicas per cluster.*


### Answer 56

56. B) --bootstrap-server

**Explanation:** 

*The --bootstrap-server option has replaced --zookeeper in Kafka CLI tools to connect directly to brokers.*


### Answer 57

57. B) Direct broker connections are now preferred to reduce ZooKeeper dependency

**Explanation:** 

*The --zookeeper option has been deprecated because direct broker connections are now preferred, reducing dependency on ZooKeeper.*


### Answer 58

58. C) 2.8.0

**Explanation:** 

*Kafka version 2.8.0 introduced early access to a completely ZooKeeper-less Kafka.*


### Answer 59

59. C) To Kafka itself (recommended)

**Explanation:** 

*It's recommended that consumers using the latest Kafka libraries commit offsets to Kafka itself, removing the dependency on ZooKeeper.*


### Answer 60

60. B) It is closed and a new one is opened

**Explanation:** 

*Once a log segment reaches the size specified by log.segment.bytes, it is closed and a new one is opened.*


---

## Study Tips

### Key Concepts to Master:
1. **Environment Setup**: ZooKeeper configuration, Java requirements, OS recommendations
2. **Broker Configuration**: broker.id, listeners, zookeeper.connect, log.dirs
3. **Topic Configuration**: num.partitions, replication.factor, retention settings
4. **Hardware Selection**: Disk, memory, network, CPU considerations
5. **OS Tuning**: Virtual memory, disk, networking settings
6. **Production Considerations**: G1GC, rack awareness, cluster sizing

### Related CCDAK Topics:
- Kafka broker deployment and configuration
- ZooKeeper ensemble setup and management
- Performance tuning and optimization
- Production best practices
- Cloud deployment strategies

---

[Back to Test](../../chapter-tests/chapter-02-test.md) | [Main README](../../README.md)