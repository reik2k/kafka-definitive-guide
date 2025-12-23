# 2. Installing Kafka

[< Back to Table of Contents](../README.md)

## Overview

This chapter describes how to get started with the Apache Kafka broker, including how to set up Apache ZooKeeper, which is used by Kafka for storing metadata for the brokers. The chapter will also cover basic configuration options for Kafka deployments, as well as some suggestions for selecting the correct hardware to run the brokers on. Finally, we cover how to install multiple Kafka brokers as part of a single cluster and things you should know when using Kafka in a production environment.

## Table of Contents

1. [Environment Setup](#environment-setup)
   - [Choosing an Operating System](#choosing-an-operating-system)
   - [Installing Java](#installing-java)
   - [Installing ZooKeeper](#installing-zookeeper)
2. [Installing a Kafka Broker](#installing-a-kafka-broker)
3. [Configuring the Broker](#configuring-the-broker)
4. [Selecting Hardware](#selecting-hardware)
5. [Kafka in the Cloud](#kafka-in-the-cloud)
6. [Configuring Kafka Clusters](#configuring-kafka-clusters)
7. [Production Concerns](#production-concerns)

## Environment Setup

Before using Apache Kafka, your environment needs to be set up with a few prerequisites to ensure it runs properly. The following sections will guide you through that process.

### Choosing an Operating System

Apache Kafka is a Java application and can run on many operating systems. While Kafka is capable of being run on many OSs, including Windows, macOS, Linux, and others, Linux is the recommended OS for the general use case. The installation steps in this chapter will focus on setting up and using Kafka in a Linux environment. For information on installing Kafka on Windows and macOS, see [Appendix A](../appendices/a-installing-other-os.md).

### Installing Java

Prior to installing either ZooKeeper or Kafka, you will need a Java environment set up and functioning. Kafka and ZooKeeper work well with all OpenJDK-based Java implementations, including Oracle JDK. The latest versions of Kafka support both Java 8 and Java 11.

It is recommended to install the latest released patch version of your Java environment, as older versions may have security vulnerabilities. The installation steps will assume you have installed JDK version 11 update 10 deployed at `/usr/java/jdk-11.0.10`.

### Installing ZooKeeper

Apache Kafka uses Apache ZooKeeper to store metadata about the Kafka cluster, as well as consumer client details. ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. This book won't go into extensive detail about ZooKeeper but will limit explanations to only what is needed to operate Kafka.

**Figure 2-1: Kafka and ZooKeeper Architecture**
![Figure 2-1: Kafka and ZooKeeper](../images/ch02/figure-2-1.png)

Kafka has been tested extensively with the stable 3.5 release of ZooKeeper and is regularly updated to include the latest release. In this book, we will be using ZooKeeper 3.5.9, which can be downloaded from the [ZooKeeper website](https://zookeeper.apache.org/).

#### Standalone Server

ZooKeeper comes with a base example config file that will work well for most use cases. However, we will manually create ours with some basic settings for demo purposes in this book. The following example installs ZooKeeper with a basic configuration in `/usr/local/zookeeper`, storing its data in `/var/lib/zookeeper`:

```bash
# tar -zxf apache-zookeeper-3.5.9-bin.tar.gz
# mv apache-zookeeper-3.5.9-bin /usr/local/zookeeper
# mkdir -p /var/lib/zookeeper
# cp > /usr/local/zookeeper/conf/zoo.cfg << EOF
> tickTime=2000
> dataDir=/var/lib/zookeeper
> clientPort=2181
> EOF
# export JAVA_HOME=/usr/java/jdk-11.0.10
# /usr/local/zookeeper/bin/zkServer.sh start
JMX enabled by default
Using config: /usr/local/zookeeper/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
#
```

You can now validate that ZooKeeper is running correctly in standalone mode by connecting to the client port and sending the four-letter command `srvr`. This will return basic ZooKeeper information from the running server:

```bash
# telnet localhost 2181
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
srvr
Zookeeper version: 3.5.9-83df9301aa5c2a5d284a9940177808c01bc35cef, built on 01/06/2021 19:49 GMT
Latency min/avg/max: 0/0/0
Received: 1
Sent: 0
Connections: 1
Outstanding: 0
Zxid: 0x0
Mode: standalone
Node count: 5
Connection closed by foreign host.
#
```

#### ZooKeeper Ensemble

ZooKeeper is designed to work as a cluster, called an ensemble, to ensure high availability. Due to the balancing algorithm used, it is recommended that ensembles contain an odd number of servers (e.g., 3, 5, and so on) as a majority of ensemble members (a quorum) must be working in order for ZooKeeper to respond to requests.

> **SIZING YOUR ZOOKEEPER ENSEMBLE**
>
> Consider running ZooKeeper in a five-node ensemble. To make configuration changes to the ensemble, including swapping a node, you will need to reload nodes one at a time. If your ensemble cannot tolerate more than one node being down, doing maintenance work introduces additional risk. It is also not recommended to run more than seven nodes, as performance can start to degrade due to the nature of the consensus protocol.
>
> Additionally, if you feel that five or seven nodes aren't supporting the load due to too many client connections, consider adding additional observer nodes for help in balancing read-only traffic.

To configure ZooKeeper servers in an ensemble, they must have a common configuration that lists all servers, and each server needs a `myid` file in the data directory that specifies the ID number of the server. If the hostnames of the servers in the ensemble are `zoo1.example.com`, `zoo2.example.com`, and `zoo3.example.com`, the configuration file might look like this:

```
ticktime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
initLimit=20
syncLimit=5
server.1=zoo1.example.com:2888:3888
server.2=zoo2.example.com:2888:3888
server.3=zoo3.example.com:2888:3888
```

Configuration Parameters:

- **X**: The ID number of the server (must be unique integer)
- **hostname**: The hostname or IP address of the server
- **peerPort**: TCP port for server-to-server communication (typically 2888)
- **leaderPort**: TCP port for leader election (typically 3888)

Each server must also have a `myid` file in the dataDir containing just the server ID number.

## Installing a Kafka Broker

Once Java and ZooKeeper are configured, you are ready to install Apache Kafka. The current release can be downloaded from the [Kafka website](https://kafka.apache.org/). The examples in this chapter are shown using version 2.7.0.

The following example installs Kafka in `/usr/local/kafka`, configured to use the ZooKeeper server started previously and to store the message log segments in `/tmp/kafka-logs`:

```bash
# tar -zxf kafka_2.13-2.7.0.tgz
# mv kafka_2.13-2.7.0 /usr/local/kafka
# mkdir /tmp/kafka-logs
# export JAVA_HOME=/usr/java/jdk-11.0.10
# /usr/local/kafka/bin/kafka-server-start.sh -daemon /usr/local/kafka/config/server.properties
#
```

Once the Kafka broker is started, verify it is working by creating a test topic, producing messages, and consuming them:

**Create and verify a topic:**
```bash
# /usr/local/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --replication-factor 1 --partitions 1 --topic test
Created topic "test".
# /usr/local/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic test
Topic:test PartitionCount:1 ReplicationFactor:1 Configs:
Topic: test Partition: 0 Leader: 0 Replicas: 0 Isr: 0
#
```

**Produce messages to a test topic:**
```bash
# /usr/local/kafka/bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic test
Test Message 1
Test Message 2
^C
#
```

**Consume messages from a test topic:**
```bash
# /usr/local/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
Test Message 1
Test Message 2
^C
Processed a total of 2 messages
#
```

## Configuring the Broker

The example configuration provided with the Kafka distribution is sufficient to run a standalone server as a proof of concept, but most likely will not be sufficient for large installations. There are numerous configuration options for Kafka that control all aspects of setup and tuning.

### General Broker Parameters

#### broker.id

Every Kafka broker must have an integer identifier, which is set using the `broker.id` configuration. By default, this integer is set to `0`, but it can be any value. It is essential that the integer must be unique for each broker within a single Kafka cluster.

#### listeners

Older versions of Kafka used a simple `port` configuration, which is now deprecated. The new `listeners` config is a comma-separated list of URIs that we listen on with the listener names. An example of a legal `listeners` config is `PLAINTEXT://localhost:9092,SSL://:9091`.

#### zookeeper.connect

The location of the ZooKeeper used for storing broker metadata is set using the `zookeeper.connect` configuration parameter. The format for this parameter is a semicolon-separated list of `hostname:port/path` strings:

- **hostname**: The hostname or IP address of the ZooKeeper server
- **port**: The client port number for the server
- **/path**: An optional ZooKeeper path to use as a chroot environment for the Kafka cluster

#### log.dirs

Kafka persists all messages to disk, and these log segments are stored in the directory specified in the `log.dir` configuration. For multiple directories, use the `log.dirs` parameter (comma-separated list). The broker stores partitions in a "least-used" fashion across the specified directories.

#### num.recovery.threads.per.data.dir

Kafka uses a configurable pool of threads for handling log segments. By default, only one thread per log directory is used. As these threads are used during startup/shutdown and recovery, it is reasonable to set a larger number to parallelize operations.

#### auto.create.topics.enable

The default Kafka configuration specifies that the broker should automatically create a topic when producers write, consumers read, or clients request metadata. In many situations, this can be undesirable. If you are managing topic creation explicitly, set this to `false`.

#### delete.topic.enable

Depending on your environment and data retention guidelines, you may wish to prevent arbitrary deletions of topics by setting this flag to `false`.

### Topic Defaults

#### num.partitions

The `num.partitions` parameter determines how many partitions a new topic is created with (primarily when automatic topic creation is enabled). This parameter defaults to one partition. Keep in mind that the number of partitions for a topic can only be increased, never decreased.

When choosing the number of partitions, consider:
- Expected throughput (e.g., 100 KBps or 1 GBps?)
- Maximum throughput when consuming from a single partition
- Message ordering requirements (keyed messages)
- Number of partitions per broker and available diskspace
- IOPS limitations on VMs or disks in cloud environments

#### default.replication.factor

If auto-topic creation is enabled, this configuration sets the replication factor for new topics. It is highly recommended to set the replication factor to at least one above the `min.insync.replicas` setting, or even 2 above for better fault tolerance (RF++).

#### log.retention.ms

The most common configuration for how long Kafka will retain messages is by time. The default is specified in the configuration file using `log.retention.hours` (168 hours or one week). Other parameters allowed are `log.retention.minutes` and `log.retention.ms`. The recommended parameter is `log.retention.ms`, as the smallest unit size takes precedence if more than one is specified.

#### log.retention.bytes

Messages can also be expired based on the total number of bytes of messages retained. This value is set using the `log.retention.bytes` parameter, applied per partition. Setting the value to –1 allows for infinite retention.

#### log.segment.bytes

As messages are produced, they are appended to the current log segment. Once it reaches the size specified by `log.segment.bytes` (defaults to 1 GB), the segment is closed and a new one opens. A smaller log segment size means files must be closed and allocated more often, reducing disk write efficiency.

#### min.insync.replicas

When configuring for data durability, setting `min.insync.replicas` to 2 ensures that at least two replicas are caught up and "in sync" with the producer. Used with producer `ack` set to "all", this ensures data durability.

#### message.max.bytes

The Kafka broker limits the maximum size of a message that can be produced with `message.max.bytes` (defaults to 1 MB). Producers sending larger messages receive an error and the message is not accepted.

## Selecting Hardware

**Figure 2-2: A Simple Kafka Cluster**
![Figure 2-2: A Simple Kafka Cluster](../images/ch02/figure-2-2.png)

Selecting appropriate hardware for a Kafka broker depends on several performance-critical factors:

### Disk Throughput

Producer client performance is most directly influenced by broker disk throughput. Kafka messages must be committed to local storage, and most clients wait until at least one broker confirms message commitment. SSDs have much lower seek times and provide better performance than HDDs, though HDDs offer more capacity per unit and can be improved with multiple directories or RAID configurations.

### Disk Capacity

Capacity is determined by message retention requirements. If you receive 1 TB daily with 7 days retention, you need minimum 7 TB usable storage. Factor in at least 10% overhead for other files plus buffer for traffic fluctuations.

### Memory

For consumers reading from the end of partitions (the normal mode), messages are optimally stored in the system page cache for faster reads. Kafka itself doesn't need much heap memory (even handling 150,000 msgs/sec can run with 5 GB heap). The rest of system memory is used by page cache, benefiting Kafka by caching log segments.

### Networking

Available network throughput specifies the maximum Kafka traffic. This is complicated by inbalance between inbound and outbound network usage (multiple consumers). It's recommended to run with at least 10 Gb NICs. 1 Gb NICs are easily saturated.

### CPU

Processing power is not critical until Kafka scales very large. Most CPU requirement comes from decompressing/recompressing message batches for checksum validation and storage.

## Kafka in the Cloud

Common cloud options include Microsoft Azure, Amazon AWS, and Google Cloud Platform.

### Microsoft Azure

You can manage disks separately from VMs. Start with data retention needs, followed by producer performance. `Standard D16s v3` instances are good for smaller clusters. `D64s v4` instances have good performance for larger clusters. Use Azure Managed Disks rather than ephemeral disks for data durability.

### Amazon Web Services

Common choices are `m4` or `r3` instance types. The `m4` allows greater retention with less throughput on elastic block storage. The `r3` has better throughput with local SSD drives but limited retention capacity. The `i2` or `d2` instance types offer best of both worlds but are significantly more expensive.

## Configuring Kafka Clusters

A single broker works well for development or proof-of-concept, but multiple brokers offer significant benefits: ability to scale load across servers and replication for data loss protection.

### How Many Brokers?

Cluster size is determined by several factors:
- Disk capacity required vs. storage available per broker
- Replica capacity per broker
- CPU capacity
- Network capacity

Other considerations include partition replica limits. Current recommendations: no more than 14,000 partition replicas per broker and 1 million per cluster (in well-configured environments).

### Broker Configuration

For multiple brokers in a cluster:
1. All brokers must have the same `zookeeper.connect` configuration
2. All brokers must have unique `broker.id` values

### OS Tuning

#### Virtual Memory

Adjust swap and dirty page handling for Kafka workload:
- Set `vm.swappiness` to very low value (e.g., 1)
- Set `vm.dirty_background_ratio` to 5 (default is 10)
- Set `vm.dirty_ratio` to 60-80 (default is 20)
- Set `vm.max_map_count` to 400,000 or 600,000
- Set `vm.overcommit_memory` to 0

#### Disk

Filesystem choice impacts performance. XFS generally outperforms Ext4 for Kafka workload with minimal tuning.

Mount options:
- Set `noatime` mount option to prevent atime updates
- Use `largeio` option to improve efficiency for larger disk writes

#### Networking

Adjust Linux networking stack tuning:
- Set `net.core.wmem_default` and `net.core.rmem_default` to 131072 (128 KiB)
- Set `net.core.wmem_max` and `net.core.rmem_max` to 2097152 (2 MiB)
- Set `net.ipv4.tcp_wmem` and `net.ipv4.tcp_rmem` to "4096 65536 2048000"
- Enable TCP window scaling: `net.ipv4.tcp_window_scaling=1`
- Increase `net.ipv4.tcp_max_syn_backlog` above default of 1024
- Increase `net.core.netdev_max_backlog` to greater than default of 1000

## Production Concerns

### Garbage Collector Options

For Java 1.8 and later, use G1GC (Garbage-First Garbage Collector) instead of the default concurrent mark and sweep. Configuration for a 64 GB server with 5 GB heap:

```bash
export KAFKA_JVM_PERFORMANCE_OPTS="-server -Xmx6g -Xms6g -XX:MetaspaceSize=96m -XX:+UseG1GC -XX:MaxGCPauseMillis=20 -XX:InitiatingHeapOccupancyPercent=35 -XX:G1HeapRegionSize=16M -XX:MinMetaspaceFreeRatio=50 -XX:MaxMetaspaceFreeRatio=80 -XX:+ExplicitGCInvokesConcurrent"
/usr/local/kafka/bin/kafka-server-start.sh -daemon /usr/local/kafka/config/server.properties
```

### Datacenter Layout

For production, configure replication within the Kafka cluster and consider physical broker location in the datacenter. Use `broker.rack` configuration for rack-aware partition assignment. Best practice: each broker in a different rack with dual power connections and dual network switches.

### Colocating Applications on ZooKeeper

ZooKeeper writes are minimal (only on cluster changes). A single ensemble can serve multiple Kafka clusters using chroot paths. Don't share ensembles with other applications if possible—Kafka is sensitive to ZooKeeper latency.

## Summary

In this chapter we learned how to install Apache Kafka and ZooKeeper, select appropriate hardware, and configure a production environment. The next chapters will cover creating clients for producing messages ([Chapter 3](../chapters/03-kafka-producers.md)) and consuming those messages ([Chapter 4](../chapters/04-kafka-consumers.md)).

---

[Next: Chapter 3 - Kafka Producers: Writing Messages To Kafka >](../chapters/03-kafka-producers.md)
