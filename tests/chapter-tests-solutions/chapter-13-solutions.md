# Chapter 13 - Monitoring Kafka - Solutions
CCDAK Practice Test Solutions
**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 13

[Back to Test](../../chapter-tests/chapter-13-test.md) | [Main README](../../README.md)

### Answer  1

**D) HTTP endpoints**

Kafka brokers expose metrics through JMX (Java Management Extensions), not through REST API, Java Management Extensions (JMX), gRPC, or HTTP endpoints. JMX is the standard monitoring interface for Java applications, and Kafka exposes a comprehensive set of metrics through JMX MBeans that can be accessed by monitoring tools.

----

### Answer  2

**B) A metric that describes one aspect of service reliability**

A Service-Level Indicator (SLI) is a specific metric that measures one aspect of service reliability, such as latency, throughput, or availability. It's not a contract (that's an SLA), not a target value (that's an SLO), and not an agreement between services. SLIs are the foundation for defining service level objectives.

----

### Answer  3

**A) A metric combined with a target value and time frame**

A Service-Level Objective (SLO) combines an SLI with a target value and time frame, such as "99.9% of requests should complete in under 100ms." It's not a contract with penalties (that's an SLA), not an operational agreement, and not just a single measurement. SLOs define the reliability goals for a service.

----

### Answer  4

**C) Quantile metrics**

Quantile metrics (like p95, p99) are typically NOT a good choice for SLIs because they cannot be aggregated across multiple instances. Counter metrics, latency percentiles (when calculated correctly), and availability measurements work better as they can be properly aggregated and are more actionable.

----

### Answer  5

**B) Under-replicated partitions**

Under-replicated partitions is the primary metric to monitor for cluster health as it indicates replication issues. Partition count, leader count, and offline partitions provide information but under-replicated partitions directly indicates when replicas are falling behind and the cluster is at risk.

----

### Answer  6

**B) Whether the broker is currently the controller (0 or 1)**

The active controller count metric indicates whether a specific broker is currently acting as the cluster controller (value of 1) or not (value of 0). Only one broker in the cluster should have this metric set to 1 at any time. This is critical for monitoring controller elections.

----

### Answer  7

**D) 0 during normal operations**

The active controller count across the entire cluster should always be exactly 1 during normal operations, but per broker it should be 0 for all brokers except the controller. Having 0 across all brokers or multiple brokers with value 1 indicates controller election problems.

----

### Answer  8

**A) Percentage of time request handlers are idle**

The request handler idle ratio measures the percentage of time that request handler threads are idle and available to process new requests. A low value indicates the broker is heavily loaded, while a high value indicates available capacity.

----

### Answer  9

**D) Below 5%**

An idle ratio below 5% typically indicates a performance problem, meaning request handlers are busy 95% or more of the time. This suggests the broker is overloaded and may need additional capacity or load balancing.

----

### Answer  10

**D) All topics produce rate**

The "All topics produce rate" metric shows the rate at which producers are sending data to the broker across all topics. "All topics messages out" measures consumption, "All topics bytes in" measures data volume, and "All topics fetch rate" measures fetch requests.

----

### Answer  11

**B) Number of partitions where one or more replicas are not in sync**

The under-replicated partitions metric measures the number of partitions where one or more replicas are not in the in-sync replica set (ISR). This is a critical metric for monitoring cluster health. A non-zero value indicates that some replicas are falling behind and replication is not keeping up.

----

### Answer  12

**B) Fetch follower max lag**

Fetch follower max lag indicates that a follower broker is having trouble keeping up with the leader. This metric measures the maximum lag in number of messages between the follower and the leader. High values indicate replication problems and potential under-replicated partitions.

----

### Answer  13

**C) Combine broker, client, and end-to-end monitoring**

The recommended approach for monitoring Kafka is to combine broker metrics, client-side metrics, and end-to-end monitoring. This provides a complete view of the system's health from multiple perspectives. Relying on only one source of metrics provides an incomplete picture.

----

### Answer  14

**B) Number of partitions allocated to the topic**

The partition count metric for a topic indicates how many partitions are allocated to that specific topic. This is a static configuration value that determines the topic's parallelism level. It's not related to message count, consumer count, or replication factor.

----

### Answer  15

**A) Network processor average idle**

Network processor average idle shows the percentage of time the network thread pool is idle. This metric indicates how busy the network threads are. A low value indicates high network load, while the inverse (utilization) would show how busy they are.

----

### Answer  16

**A) Frequency and duration of flushing log segments to disk**

The log flush rate and time metric measures how frequently and how long it takes to flush log segments from the page cache to disk. This is important for understanding disk I/O performance and ensuring durability settings are working correctly.

----

### Answer  17

**B) Under-replicated partitions**

Under-replicated partitions is the key metric to monitor for detecting broker failures. When a broker fails, its partitions become under-replicated because the replicas on that broker are no longer available. A sudden spike in this metric often indicates broker problems.

----

### Answer  18

**B) Difference between last produced offset and last committed offset**

Consumer lag is the difference between the last produced offset (log end offset) and the last committed offset by the consumer. It indicates how far behind the consumer is from the latest messages. High lag means the consumer is falling behind producers.

----

### Answer  19

**B) kafka-consumer-groups**

The kafka-consumer-groups command-line tool can be used to monitor consumer group lag. It displays information about consumer groups including current offsets, log end offsets, and lag for each partition. This is a standard tool provided with Kafka.

----

### Answer  20

**A) Number of fetch requests waiting to be completed**

The fetch request purgatory size metric indicates the number of fetch requests that are delayed and waiting to be completed. Fetch requests can be delayed when there isn't enough data to satisfy the minimum fetch size or maximum wait time hasn't elapsed yet.

----

### Answer  21

**A) Number of produce requests delayed until replication completes**

The produce request purgatory size tracks the number of produce requests that are delayed and waiting for replication to complete. When acks=all is configured, produce requests must wait until all in-sync replicas have acknowledged the write before responding to the producer.

----

### Answer  22

**A) Leader election rate**

The leader election rate metric indicates the total number of leader elections per second across the cluster. This includes both clean and unclean elections. A high rate can indicate instability in the cluster with brokers going up and down frequently.

----

### Answer  23

**B) Election of a leader that is not in the ISR, potentially causing data loss**

An unclean leader election occurs when a leader is elected from a replica that is not in the in-sync replica set (ISR). This can happen when all ISR members are unavailable and unclean.leader.election.enable is set to true. This can result in data loss as the new leader may not have all committed messages.

----

### Answer  24

**A) Messages in per second**

The messages in per second metric shows the number of messages produced per second to a broker. This is a key throughput metric for understanding producer traffic. Bytes in measures data volume, produce requests measures request count, and records produced rate is similar but at different granularity.

----

### Answer  25

**A) Data sent from broker to consumers**

The bytes out per second metric measures the amount of data sent from the broker to consumers and follower replicas. This includes both consumer fetch traffic and replication traffic. It's a key metric for monitoring consumer throughput and network bandwidth usage.

----

### Answer  26

**A) Log cleaner recopy percent**

The log cleaner recopy percent metric is useful for monitoring log compaction performance. It indicates what percentage of log data must be copied during compaction. Higher values mean more work for the cleaner thread, potentially indicating inefficient compaction.

----

### Answer  27

**A) Rate at which replicas fall out of sync**

The ISR shrink rate metric indicates the rate at which replicas are removed from the in-sync replica set. A high shrink rate suggests that replicas are frequently falling behind, which can indicate performance issues with follower brokers or network problems.

----

### Answer  28

**A) Consumer lag**

Consumer lag is the primary metric to monitor for identifying slow consumers. It directly measures how far behind the consumer is from the latest messages in each partition. Growing lag over time indicates the consumer cannot keep up with the producer rate.

----

### Answer  29

**A) To identify broker overload and request backlog**

The request queue size metric indicates how many requests are waiting to be processed by the broker. A large or growing queue size suggests the broker is overloaded and cannot process incoming requests fast enough, leading to increased latency.

----

### Answer  30

**A) Produce request remote time**

Produce request remote time measures the time spent waiting for sufficient replicas (followers) to acknowledge the write before completing the produce request. This is relevant when acks=all. High values indicate replication delays.

----

### Answer  31

**A) Time from request received to response sent**

The total time metric for produce requests measures the complete end-to-end time from when the request is received by the broker until the response is sent back to the producer. This includes queue time, processing time, replication time, and response queue time.

----

### Answer  32

**C) 9999**

Port 9999 is commonly used as the default JMX port to expose Kafka broker metrics. Port 9092 is the default Kafka protocol port, 2181 is ZooKeeper, and 8080 is commonly used for HTTP services. The JMX port can be configured via JMX_PORT environment variable.

----

### Answer  33

**A) To track disk usage and plan capacity**

Monitoring partition size helps track disk usage per partition and broker, which is essential for capacity planning. By understanding how quickly partitions grow, operators can predict when additional disk space or data retention policy changes will be needed.

----

### Answer  34

**A) Offline partitions count**

The offline partitions count metric specifically indicates the number of partitions that have no leader and are therefore unavailable. This is more severe than under-replicated partitions, as offline partitions cannot serve read or write requests at all.

----

### Answer  35

**A) Broker disconnecting from ZooKeeper coordination service**

ZooKeeper session expiration indicates that a broker has disconnected from the ZooKeeper coordination service. This can happen due to network issues, long GC pauses, or ZooKeeper overload. When a broker's session expires, it must re-register and may trigger controller elections.

----

### Answer  36

**A) Network processor average idle percent**

The network processor average idle percent metric helps identify network performance issues. Low idle percentage indicates that network threads are busy and may be a bottleneck. This is distinct from CPU, memory, or disk metrics which measure other resource types.

----

### Answer  37

**A) Number of records consumed per second**

The records consumed rate metric on the consumer side measures the number of records the consumer is processing per second. This is a key throughput metric for understanding consumer performance and detecting slowdowns in consumption rate.

----

### Answer  38

**A) Error rate**

The error rate metric indicates the rate of failed produce requests. This includes various errors such as timeouts, invalid requests, or broker errors. Monitoring this helps identify producer or broker issues affecting message delivery.

----

### Answer  39

**A) To detect failed disk or corrupted log directories**

The log directory offline count metric indicates how many log directories have failed or become inaccessible. This can happen due to disk failures, file system corruption, or I/O errors. Kafka can continue operating with remaining healthy disks, but capacity is reduced.

----

### Answer  40

**A) Poll idle ratio**

The poll idle ratio metric indicates the fraction of time the consumer spends waiting in the poll() loop versus processing messages. A high value suggests the consumer is spending most of its time waiting for messages, while a low value indicates the consumer is actively processing.

----

### Answer  41

**A) Average time taken to complete fetch requests**

The fetch latency average metric measures the average time taken to complete fetch requests from consumers or follower replicas. This includes time spent waiting for data, reading from disk, and network transmission. High values indicate slow fetch performance.

----

### Answer  42

**A) Record send rate and batch size average**

Producer batching effectiveness can be measured by looking at the record send rate combined with batch size average. Larger batch sizes with consistent send rates indicate efficient batching. This reduces the number of requests and improves throughput.

----

### Answer  43

**A) To track leadership rebalancing across brokers**

The preferred replica election metric tracks the process of rebalancing partition leadership back to the preferred replicas. This ensures even distribution of leadership load across brokers. Regular preferred leader elections help maintain cluster balance.

----

### Answer  44

**A) Buffer total bytes and buffer available bytes**

The buffer total bytes and buffer available bytes metrics show the amount of memory allocated for buffering messages in the producer and the amount currently available. Low available buffer can cause producers to block when sending messages.

----

### Answer  45

**A) Maximum lag across all partitions assigned to a consumer**

The records lag max metric indicates the maximum lag in number of records across all partitions assigned to a consumer. This helps identify the worst-case lag situation for a consumer, which is important for understanding if any partitions are falling significantly behind.

----

### Answer  46

**A) Prometheus and Grafana**

Prometheus and Grafana are commonly used together for collecting and visualizing Kafka metrics. Prometheus scrapes JMX metrics via exporters, stores time-series data, and Grafana provides dashboards and visualization. Apache Spark, Kafka Streams, and Flink are data processing frameworks.

----

### Answer  47

**A) Rate at which connections are being closed**

The connection close rate metric indicates how frequently connections are being closed. A high rate might indicate connection instability, client restarts, or network issues. Monitoring this helps identify connectivity problems between clients and brokers.

----

### Answer  48

**A) Log size and disk usage per broker**

Monitoring log size and disk usage per broker helps ensure the cluster has sufficient disk space. Tracking disk growth trends allows operators to predict when additional storage will be needed and prevents disk space exhaustion, which can cause broker failures.

----

### Answer  49

**A) To detect delays in processing controller events**

The controller queue size metric indicates how many controller events are waiting to be processed. A large queue suggests the controller is overloaded and cannot keep up with cluster state changes like partition reassignments or leader elections. This can slow down administrative operations.

----

### Answer  50

**A) Buffer exhausted rate**

The buffer exhausted rate metric indicates how often producers are blocked because the buffer memory is exhausted. When buffer.memory is full and max.block.ms hasn't expired, the producer must wait. High values suggest the producer is sending faster than the broker can handle.

----

### Answer  51

**A) Maximum time taken to respond to heartbeat requests**

The heartbeat response time max metric measures the maximum time taken by the group coordinator to respond to consumer heartbeat requests. High values can indicate coordinator overload or network issues. If heartbeats take too long, consumers may be kicked out of the group.

----

### Answer  52

**A) Compression ratio**

The compression ratio metric indicates the effectiveness of message compression. It shows the ratio between compressed and uncompressed message size. Higher ratios mean better compression, which reduces network bandwidth and disk usage. This is important for optimizing resource utilization.

----

### Answer  53

**A) To track the number of partitions managed by the broker**

The replica manager partition count metric tracks how many partitions a broker is managing (both as leader and follower). This helps ensure partitions are evenly distributed across brokers. Uneven distribution can lead to hotspots and resource imbalance.

----

### Answer  54

**A) Rebalance latency and rebalance rate**

Rebalance latency and rebalance rate metrics should be monitored to detect consumer group rebalancing. High rebalance rates indicate frequent group membership changes, which can impact consumer performance. High latency means rebalances are taking a long time to complete.

----

### Answer  55

**A) Average size of requests in bytes**

The request size average metric indicates the average size of requests in bytes. This helps understand the typical payload size being sent to brokers. Large request sizes might indicate batch configuration opportunities or potential network bottlenecks.

----

### Answer  56

**A) Time from message production to consumption**

End-to-end latency measures the complete time from when a message is produced until it is consumed and processed. This is the most important metric for understanding the true performance experienced by the application. It includes broker latency, replication time, and consumer processing.

----

### Answer  57

**A) Partition count per broker and bytes in/out per broker**

To identify if brokers are properly balanced, monitor partition count per broker and bytes in/out per broker. These metrics reveal whether leadership and data load are evenly distributed. Significant imbalances can lead to some brokers being overloaded while others are underutilized.

----

### Answer  58

**A) To track time taken to commit offsets to Kafka**

The commit latency metric tracks how long it takes for consumers to commit their offsets to Kafka. High commit latency can indicate coordinator overload or network issues. Slow commits can impact exactly-once semantics and consumer recovery time.

----

### Answer  59

**A) ISR expansion rate**

The ISR expansion rate metric indicates the rate at which replicas are being added back to the in-sync replica set. This typically happens when a lagging replica catches up with the leader. A balanced ISR shrink/expansion rate indicates stable replication.

----

### Answer  60

**A) Maximum time a follower replica is behind the leader**

The replica lag time max metric measures the maximum time (in milliseconds) that a follower replica is behind the leader. This is different from message count lag and provides a time-based view of replication delays. High values indicate slow replication.