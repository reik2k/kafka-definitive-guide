# Chapter 2: Installing Kafka - Solutions

[Back to Test](../../chapter-tests/chapter-02-test.md)

---

## Answer Key

## **Question 1**
**Explanation:** Linux is the recommended OS for the general use case when running Kafka in production. While Kafka can run on Windows, macOS, and other operating systems, Linux provides the best performance and stability.

## **Question 2**
**Explanation:** The latest versions of Kafka support both Java 8 and Java 11. These are the recommended Java versions for running Kafka.

## **Question 3**
**Explanation:** ZooKeeper is used by Kafka for storing metadata about the brokers, topics, partitions, and consumer client details. It provides centralized configuration and synchronization.

## **Question 4**
**Explanation:** The chapter mentions using ZooKeeper 3.5.9, which has been tested extensively with Kafka.

## **Question 5**
**Explanation:** In a five-node ZooKeeper ensemble, you can run with two nodes missing while still maintaining quorum (3 out of 5).

## **Question 6**
**Explanation:** An odd number of servers is recommended because ZooKeeper requires a majority (quorum) to respond to requests. This makes odd numbers more efficient.

## **Question 7**
**Explanation:** initLimit specifies the amount of time to allow followers to connect with a leader, measured in tickTime units.

## **Question 8**
**Explanation:** syncLimit controls how long out-of-sync followers can be with the leader, also measured in tickTime units.

## **Question 9**
**Explanation:** You can verify ZooKeeper is running by connecting via telnet and sending the four-letter command "srvr", which returns basic ZooKeeper information.

## **Question 10**
**Explanation:** The default Kafka broker port is 9092.

## **Question 11**
**Explanation:** The broker.id configuration parameter sets the unique integer identifier for each Kafka broker in a cluster.

## **Question 12**
**Explanation:** The listeners configuration is a comma-separated list of URIs that specifies the interfaces and ports Kafka listens on.

## **Question 13**
**Explanation:** The zookeeper.connect parameter format is hostname:port/path, where path is an optional chroot.

## **Question 14**
**Explanation:** A chroot path is designated to act as the root directory for a given Kafka cluster within ZooKeeper.

## **Question 15**
**Explanation:** Using a chroot path allows the ZooKeeper ensemble to be shared with other applications, including other Kafka clusters, without conflicts.

## **Question 16**
**Explanation:** The log.dirs configuration specifies where Kafka persists log segments. It's a comma-separated list of paths.

## **Question 17**
**Explanation:** When multiple log.dirs are specified, Kafka stores partitions in a "least-used" fashion, placing new partitions in the path with the least number of partitions.

## **Question 18**
**Explanation:** num.recovery.threads.per.data.dir configures the thread pool used for opening partitions' log segments during startup, checking and truncating during failure recovery, and closing log segments during shutdown.

## **Question 19**
**Explanation:** auto.create.topics.enable should be set to false when you are managing topic creation explicitly, whether manually or through a provisioning system.

## **Question 20**
**Explanation:** auto.leader.rebalance.enable ensures topic leadership is balanced across brokers by enabling a background thread that checks and rebalances partition leadership.

## **Question 21**
**Explanation:** The num.partitions parameter defaults to one partition for new topics.

## **Question 22**
**Explanation:** The number of partitions for a topic can only be increased, never decreased.

## **Question 23**
**Explanation:** It's recommended to set the replication factor to at least 1 above min.insync.replicas. For more fault-resistant settings, RF++ (2 above min.insync.replicas) is preferable.

## **Question 24**
**Explanation:** log.retention.ms controls how long Kafka will retain messages by time.

## **Question 25**
**Explanation:** The default retention time is 168 hours, or one week, specified by log.retention.hours.

## **Question 26**
**Explanation:** Retention by time is performed by examining the last modified time (mtime) on each log segment file on disk.

## **Question 27**
**Explanation:** log.retention.bytes controls the total number of bytes of messages retained per partition.

## **Question 28**
**Explanation:** The default size for log.segment.bytes is 1 GB.

## **Question 29**
**Explanation:** A log segment can only be considered for expiration after it has been closed.

## **Question 30**
**Explanation:** min.insync.replicas ensures that at least a specified number of replicas are caught up and in sync for a write to be acknowledged.

## **Question 31**
**Explanation:** The default maximum message size (message.max.bytes) is 1000000, or 1 MB.

## **Question 32**
**Explanation:** The message size on the broker must be coordinated with fetch.message.max.bytes on consumer clients, otherwise consumers may fail to fetch larger messages.

## **Question 33**
**Explanation:** SSDs provide drastically lower seek and access times and will provide the best performance for Kafka.

## **Question 34**
**Explanation:** More memory allows the system to cache log segments in the page cache, resulting in faster reads for consumers.

## **Question 35**
**Explanation:** A broker handling 150,000 messages per second can run with a 5 GB heap. Kafka doesn't need much heap memory.

## **Question 36**
**Explanation:** At least 10 Gb NICs are recommended to prevent the network from becoming saturated, especially with replication and mirroring.

## **Question 37**
**Explanation:** When scaling Kafka to very large sizes, CPU becomes important because brokers must decompress message batches to validate checksums and assign offsets, then recompress them.

## **Question 38**
**Explanation:** Standard D16s v3 instances are mentioned as a good choice for smaller clusters in Azure.

## **Question 39**
**Explanation:** The m4 and r3 instance types are common choices for Kafka in AWS.

## **Question 40**
**Explanation:** All brokers must have the same zookeeper.connect parameter and each must have a unique broker.id.

## **Question 41**
**Explanation:** vm.swappiness should be set to a very low value like 1 to avoid swapping while still providing a safety net.

## **Question 42**
**Explanation:** The meaning of vm.swappiness=0 changed in kernel 3.5-rc1 to mean "never swap under any circumstances" rather than "do not swap unless out-of-memory".

## **Question 43**
**Explanation:** vm.dirty_background_ratio controls the percentage of total system memory that can be filled with dirty pages before the flush background process starts writing them to disk.

## **Question 44**
**Explanation:** XFS is recommended as it outperforms Ext4 for most workloads with minimal tuning required.

## **Question 45**
**Explanation:** The noatime mount option prevents atime (access time) updates, which generates unnecessary disk writes.

## **Question 46**
**Explanation:** Setting noatime prevents the last access time from being updated every time a file is read, reducing disk writes.

## **Question 47**
**Explanation:** A reasonable setting for net.core.wmem_max (maximum send buffer) is 2097152, or 2 MiB.

## **Question 48**
**Explanation:** G1GC is now recommended for Kafka as it automatically adjusts to different workloads and provides consistent pause times.

## **Question 49**
**Explanation:** MaxGCPauseMillis specifies the preferred pause time for each garbage collection cycle (not a fixed maximum).

## **Question 50**
**Explanation:** The default MaxGCPauseMillis value is 200 milliseconds.

## **Question 51**
**Explanation:** The broker.rack configuration makes Kafka rack-aware, ensuring replicas don't share the same rack.

## **Question 52**
**Explanation:** Configuring broker.rack ensures that replicas for a single partition do not share a rack, improving fault tolerance.

## **Question 53**
**Explanation:** Kafka should not be colocated with other significant applications as it would have to share page cache, decreasing consumer performance.

## **Question 54**
**Explanation:** Currently, in a well-configured environment, it's recommended to have no more than 14,000 partition replicas per broker.

## **Question 55**
**Explanation:** The current recommendation is no more than 1 million replicas per cluster.

## **Question 56**
**Explanation:** The --bootstrap-server option has replaced --zookeeper in Kafka CLI tools to connect directly to brokers.

## **Question 57**
**Explanation:** The --zookeeper option has been deprecated because direct broker connections are now preferred, reducing dependency on ZooKeeper.

## **Question 58**
**Explanation:** Kafka version 2.8.0 introduced early access to a completely ZooKeeper-less Kafka.

## **Question 59**
**Explanation:** It's recommended that consumers using the latest Kafka libraries commit offsets to Kafka itself, removing the dependency on ZooKeeper.

## **Question 60**
**Explanation:** Once a log segment reaches the size specified by log.segment.bytes, it is closed and a new one is opened.

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