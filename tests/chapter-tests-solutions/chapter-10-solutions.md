# Chapter 10 – Cross-Cluster Data Mirroring – Solutions and Explanations

> **Answer Key with Detailed Explanations** | CCDAK Preparation Material

---

## Question 1
**Correct Answer: B**

**Explanation:**
In Kafka terminology, replication refers to the copying of data between brokers within the same cluster to provide redundancy and fault tolerance. Mirroring, on the other hand, refers to copying data between different Kafka clusters. This distinction is important for understanding how Kafka handles data at different architectural levels. Apache Kafka's built-in cross-cluster replicator is called MirrorMaker.

---

## Question 2
**Correct Answer: B**

**Explanation:**
The hub-and-spoke architecture is designed for scenarios where data is produced in multiple regional datacenters and some consumers need access to the entire dataset. It allows applications in each datacenter to process data locally, while a central datacenter receives mirrored data from all regional datacenters for company-wide analytics. This is ideal for use cases like price optimization based on regional supply and demand.

---

## Question 3
**Correct Answer: C**

**Explanation:**
The main limitation of hub-and-spoke architecture is that processors in one regional datacenter cannot access data from another regional datacenter. This can be problematic in scenarios like a bank where a user visits a branch in a different city than their home branch - the visiting branch would either need to interact with a remote cluster or have no access to the user's information.

---

## Question 4
**Correct Answer: B**

**Explanation:**
Consuming from remote datacenters is safer than producing to them because if a network partition occurs, the records remain safe in the source Kafka brokers until communications resume. With remote producing, there's a risk of accidental data loss if events are already consumed but the producer can't connect due to network issues. This is the safest form of cross-cluster communication.

---

## Question 5
**Correct Answer: B**

**Explanation:**
Active-active architecture provides the ability to serve users from nearby datacenters with full functionality, offering performance benefits without sacrificing data availability. It also provides redundancy - if one datacenter becomes unavailable, users can be redirected to another datacenter with simple network redirects, making it the most transparent type of failover.

---

## Question 6
**Correct Answer: C**

**Explanation:**
To prevent endless mirroring loops in active-active architecture, each logical topic gets a separate physical topic per datacenter with the datacenter name as a prefix (e.g., NYC.users and SF.users). MirrorMaker mirrors NYC.users from NYC to SF and SF.users from SF to NYC, ensuring each event is mirrored only once. Consumers use pattern subscriptions like *.users to consume all user events.

---

## Question 7
**Correct Answer: B**

**Explanation:**
The main challenge with active-active architecture is handling conflicts when data is read and updated asynchronously in multiple locations. This includes technical challenges like preventing endless mirroring loops, but more importantly, maintaining data consistency between datacenters. Applications must handle scenarios where users write to one datacenter and read from another before replication completes, or where conflicting updates occur in different datacenters simultaneously.

---

## Question 8
**Correct Answer: B**

**Explanation:**
In active-standby architecture, the standby cluster typically does nothing except wait for a disaster, representing a waste of resources. Since disasters should be rare, most of the time the cluster sits idle. Some organizations try to mitigate this by using a smaller DR cluster or shifting read-only workloads to it, but this is risky as the minimally-sized cluster may not hold up during an emergency.

---

## Question 9
**Correct Answer: B**

**Explanation:**
Recovery Point Objective (RPO) defines the maximum amount of time for which data may be lost as a result of a disaster. It determines how much data loss is acceptable to the business. Low RPO requires real-time mirroring with low latencies, and RPO=0 requires synchronous replication. This metric is critical for disaster recovery planning.

---

## Question 10
**Correct Answer: A**

**Explanation:**
Recovery Time Objective (RTO) defines the maximum amount of time before all services must resume after a disaster occurs. The lower the RTO, the more important it is to avoid manual processes and application restarts, as very low RTO can only be achieved with automated failover. This metric determines how quickly you need to restore operations after a disaster.

---

## Question 11
**Correct Answer: B**

**Explanation:**
The auto offset reset option uses the `auto.offset.reset` configuration to determine where consumers should start reading when they don't have a previously committed offset. Consumers can either start from the beginning of available data (handling duplicates) or skip to the end (potentially missing events). This is the simplest failover method but may result in data loss or duplicate processing.

---

## Question 12
**Correct Answer: B**

**Explanation:**
Offsets can diverge between primary and DR clusters due to several factors: 1) Different mirroring start times - if mirroring starts after data retention has already removed early records from the primary, the first offset numbers won't match; 2) Producer retries can cause the same message to be written with different offsets in each cluster. These divergences make offset-based failover challenging.

---

## Question 13
**Correct Answer: B**

**Explanation:**
The `kafka-consumer-groups` tool provides time-based offset reset functionality (added in version 0.11.0). It can reset consumer offsets for groups based on timestamps using the `--to-datetime` option. This allows failover to a specific point in time, which is often easier to explain and more predictable than other offset translation methods.

---

## Question 14
**Correct Answer: B**

**Explanation:**
A stretch cluster is a single Kafka cluster installed across multiple datacenters, as opposed to multiple separate clusters. It uses Kafka's normal replication mechanism to keep brokers in sync across datacenters, potentially with synchronous replication. This is fundamentally different from multicluster scenarios that require mirroring tools.

---

## Question 15
**Correct Answer: B**

**Explanation:**
Stretch clusters require at least three datacenters because ZooKeeper requires an odd number of nodes and remains available only if a majority of nodes are available. With two datacenters, one will always contain a majority, so if it fails, ZooKeeper becomes unavailable. With three datacenters, losing one still leaves a majority available in the remaining two, keeping both ZooKeeper and Kafka operational.

---

## Question 16
**Correct Answer: B**

**Explanation:**
The main advantage of stretch clusters is that synchronous replication is possible. Using rack definitions, `min.insync.replicas`, and `acks=all`, you can ensure writes are acknowledged only after being written to brokers in multiple datacenters. This provides 100% data synchronization between sites, which is often a legal requirement for certain types of businesses.

---

## Question 17
**Correct Answer: C**

**Explanation:**
MirrorMaker 2.0, introduced in Kafka version 2.4.0, is based on the Kafka Connect framework. This new architecture overcomes many shortcomings of earlier MirrorMaker versions, including stop-the-world rebalance issues. It uses Connect's REST API for centralized management and automated task distribution, reducing administrative overhead.

---

## Question 18
**Correct Answer: B**

**Explanation:**
A replication flow in MirrorMaker defines the configuration of a directional data flow from a source cluster to a target cluster. Multiple replication flows can be defined to create complex topologies like hub-and-spoke, active-active, or active-standby architectures. Each flow is identified by source->target notation (e.g., NYC->LON).

---

## Question 19
**Correct Answer: B**

**Explanation:**
In MirrorMaker configuration, topics for mirroring are specified using regular expressions. For example, `prod.*` would mirror all topics starting with "prod", or `.*` would mirror all topics. A separate topic exclusion list can also be specified to exclude topics that don't require mirroring. This provides flexible topic selection without manual listing.

---

## Question 20
**Correct Answer: C**

**Explanation:**
The default naming strategy for mirrored topics in MirrorMaker is to prefix the target topic name with the source cluster alias. For example, a topic named "orders" from the NYC datacenter would be mirrored as "NYC.orders" in the target datacenter. This naming convention is critical for preventing replication cycles in active-active architectures.

---

## Question 21
**Correct Answer: B**

**Explanation:**
Prefixing target topics with the source cluster alias prevents replication cycles in active-active mode. When topics are mirrored from NYC to LON and LON to NYC, the prefix distinction ensures MirrorMaker doesn't endlessly mirror the same events back and forth. Only local topics (without remote prefixes) are replicated, so NYC.orders in LON won't be mirrored back to NYC.

---

## Question 22
**Correct Answer: C**

**Explanation:**
The `tasks.max` configuration limits the maximum number of tasks that the MirrorMaker connector may use. The default is 1, but a minimum of 2 is recommended for production. Higher values increase parallelism when replicating many topic partitions, improving throughput and reducing latency.

---

## Question 23
**Correct Answer: B**

**Explanation:**
SSL or SASL_SSL is recommended for securing cross-datacenter traffic in MirrorMaker. SSL encrypts all data in transit between datacenters, which is critical for production environments. SASL_SSL combines encryption with authentication. The security protocol should match the broker listener configuration in both source and target clusters.

---

## Question 24
**Correct Answer: B**

**Explanation:**
MirrorMaker requires Topic:Read permission on the source cluster to consume from source topics. On the target cluster, it needs Topic:Create permission to create mirror topics and Topic:Write permission to produce to them. Additional permissions are needed for offset migration, ACL migration, and configuration synchronization.

---

## Question 25
**Correct Answer: B**

**Explanation:**
MirrorMaker should typically be deployed in the target datacenter, consuming data remotely from the source. This is safer because if network connectivity is lost, events remain safe in the source cluster. With remote producing, there's a risk of losing consumed events if the producer can't connect. Remote consuming is the safest form of cross-cluster communication.

---

## Question 26
**Correct Answer: B**

**Explanation:**
Consuming remotely is preferred because if a network connection fails, the data remains safely stored in the source Kafka brokers and can be consumed once connectivity is restored. There's no risk of data loss. With remote producing, if events have already been consumed but the producer loses connection before acknowledgment, those events could potentially be lost, making it a riskier approach.

---

## Question 27
**Correct Answer: B**

**Explanation:**
The `replication-latency-ms` metric measures the time interval between when a record was timestamped and when it was successfully produced to the target cluster. This metric is crucial for detecting if the target is not keeping up with the source in a timely manner. Sustained increases in this latency may indicate insufficient capacity.

---

## Question 28
**Correct Answer: C**

**Explanation:**
MirrorMaker 2.0 allocates partitions to tasks evenly without using Kafka's consumer group-management protocol. This avoids latency spikes caused by rebalances when new topics or partitions are added. Events from each partition in the source cluster are mirrored to the same partition in the target cluster, preserving semantic partitioning and maintaining event ordering.

---

## Question 29
**Correct Answer: B**

**Explanation:**
The `errors.tolerance=none` configuration ensures MirrorMaker fails fast when it cannot send events to the target cluster. This is typically safer than continuing operations and risking data loss. Combined with `acks=all` and sufficient retries on the producer side, this configuration helps maintain data integrity during network issues.

---

## Question 30
**Correct Answer: C**

**Explanation:**
In active-active topology, endless mirroring loops are prevented by using cluster alias prefixes for remote topics. MirrorMaker doesn't replicate topics that already have a remote datacenter prefix. For example, if NYC.users exists in LON, it won't be mirrored back to NYC, as it's already identified as originating from NYC. Only local topics (without prefixes) are replicated.

---

## Question 31
**Correct Answer: B**

**Explanation:**
uReplicator is Uber's solution to address MirrorMaker's rebalancing issues at very large scale. It replaces the Kafka consumer group coordination with Apache Helix for partition assignment, avoiding the stop-the-world rebalances that occurred when topics were added or MirrorMaker instances were bounced. This significantly reduced mirroring latency and improved stability.

---

## Question 32
**Correct Answer: B**

**Explanation:**
uReplicator uses Apache Helix as a central (but highly available) controller to manage topic lists and partition assignments. The Helix consumer takes partition assignments from the Apache Helix controller rather than through consumer group coordination, avoiding rebalances. Administrators use a REST API to add topics to the Helix-managed list.

---

## Question 33
**Correct Answer: C**

**Explanation:**
Brooklin is LinkedIn's distributed service that provides a generic data ingestion framework capable of streaming data between heterogeneous source and target systems, including Kafka. It's used for multiple use cases: data bridges, change data capture (CDC), and cross-cluster mirroring. LinkedIn uses Brooklin to mirror trillions of messages daily.

---

## Question 34
**Correct Answer: B**

**Explanation:**
Cluster Linking's key feature is offset-preserving replication across clusters, using the same protocol as intra-cluster replication. This enables seamless client migration without offset translation needs. Topic configuration, partitions, consumer offsets, and ACLs are all kept synchronized, enabling failover with low RTO and eliminating the offset divergence issues of traditional mirroring.

---

## Question 35
**Correct Answer: B**

**Explanation:**
Multi-Region Clusters (MRC) in Confluent Platform combine synchronous and asynchronous replication. It uses synchronous replication within a region and asynchronous replication between regions to achieve both low latency and high durability. Operators can configure replica placement constraints to ensure replicas are spread across regions while observers provide asynchronous cross-region replication.

---

## Question 36
**Correct Answer: B**

**Explanation:**
Observers in Confluent Server are asynchronous replicas that don't join the In-Sync Replica (ISR) set. They have no impact on producers using `acks=all` but can still deliver records to consumers. This allows MRC to benefit from fast local writes with synchronous replication within a region while providing data redundancy across regions through observers.

---

## Question 37
**Correct Answer: B**

**Explanation:**
The most critical metric for failover monitoring is the lag between source and target cluster offsets. This shows how far behind the DR cluster is from the primary. In a busy system with 1 million messages per second and 5ms lag, the DR cluster could be 5,000 messages behind. Monitoring this lag ensures it never falls too far behind, which is essential for disaster recovery planning.

---

## Question 38
**Correct Answer: B**

**Explanation:**
The recommended minimum value for `tasks.max` in production MirrorMaker is 2. While the default is 1, having at least 2 tasks provides better fault tolerance and parallelism. When replicating many topic partitions, higher values should be used to increase parallelism and improve throughput, but 2 is the baseline for production deployments.

---

## Question 39
**Correct Answer: B**

**Explanation:**
The `max.in.flight.requests.per.connection` configuration can significantly increase throughput when message order is not critical. Limiting it to 1 guarantees ordering but means each request must be acknowledged before the next is sent, reducing throughput especially with high latency. The default value of 5 allows multiple in-flight requests, dramatically improving throughput when ordering isn't required.

---

## Question 40
**Correct Answer: A**

**Explanation:**
Increasing `linger.ms` introduces a small amount of latency but allows batches to fill up more completely before sending. If monitoring shows the producer consistently sends partially empty batches (batch-size-avg lower than configured batch.size), increasing linger.ms lets the producer wait a few milliseconds for batches to fill, significantly improving throughput at the cost of slightly higher latency.

---

## Question 41
**Correct Answer: B**

**Explanation:**
If fetch-size metrics (fetch-size-avg and fetch-size-max) are close to the configured `fetch.max.bytes`, the consumer is reading as much data as it's allowed in each request. Increasing `fetch.max.bytes` allows the consumer to read more data per request, reducing the number of fetch requests needed and improving throughput, assuming you have available memory to buffer the additional data.

---

## Question 42
**Correct Answer: B**

**Explanation:**
Wide Area Networks (WANs) typically have far lower available bandwidth than local networks within a datacenter, and bandwidth costs are significantly higher. Additionally, higher latencies make it more challenging to utilize all available bandwidth. These characteristics are why cross-datacenter communication requires careful architectural planning and why bandwidth is often the main bottleneck for mirroring.

---

## Question 43
**Correct Answer: A**

**Explanation:**
Offset translation maintains a mapping between offsets in the primary and DR clusters, stored in an external data store or Kafka topic. When offsets diverge due to duplicates or different start times, this mapping allows proper failover. Modern mirroring solutions like MirrorMaker 2.0 use Kafka topics for storing offset translation metadata, recording mappings whenever the offset difference changes.

---

## Question 44
**Correct Answer: B**

**Explanation:**
A canary process sends test events periodically (typically every minute) to a special topic in the source cluster and verifies they arrive at the destination cluster within an acceptable timeframe. This provides end-to-end verification that mirroring is working correctly. If events don't arrive on time, it can indicate MirrorMaker is lagging or unavailable, providing an additional monitoring layer.

---

## Question 45
**Correct Answer: B**

**Explanation:**
Burrow, developed by LinkedIn, provides more sophisticated lag analysis than kafka-consumer-groups. While kafka-consumer-groups shows current lag, Burrow monitors lag trends and uses algorithms to determine whether the lag represents a real problem or just normal fluctuations. This reduces false alerts and provides better insight into consumer health.

---

## Question 46
**Correct Answer: B**

**Explanation:**
Deploying MirrorMaker in the source datacenter should be considered when cross-datacenter traffic requires encryption but local traffic does not. Consumers take a significant performance hit with SSL encryption due to extra data copying, affecting both consumers and brokers. Deploying at source allows consuming unencrypted data locally while producing encrypted to remote, minimizing the SSL performance impact.

---

## Question 47
**Correct Answer: B**

**Explanation:**
The main risk of remote producing is that events could be lost if a network partition occurs after consumption but before the producer receives acknowledgment. Even with retries configured, network issues can cause data loss. This is why remote consuming is recommended - if the consumer can't connect, events remain safe in the source cluster until connectivity is restored.

---

## Question 48
**Correct Answer: B**

**Explanation:**
Active-active architecture supports failover with minimal manual intervention because each datacenter has full functionality. Users can be redirected to another datacenter using simple network redirects (typically DNS changes) without complex application restarts or data recovery procedures. Both datacenters actively serve users, making failover transparent and fast.

---

## Question 49
**Correct Answer: B**

**Explanation:**
In stretch clusters, `min.insync.replicas` combined with `acks=all` and rack definitions ensures that events are written to a minimum number of replicas across multiple datacenters before being acknowledged. This configuration enables synchronous replication across datacenters, providing 100% data synchronization between sites, which is often required for regulatory compliance.

---

## Question 50
**Correct Answer: B**

**Explanation:**
In MirrorMaker 2.0 (based on Kafka Connect), consumer tasks are responsible for reading from the source cluster. Each task contains both a consumer and producer pair. The Connect framework assigns these tasks to different worker nodes, with each consumer task reading from assigned partitions in the source cluster and its paired producer writing to the target cluster.

---

## Question 51
**Correct Answer: B**

**Explanation:**
Using Kafka Connect framework provides MirrorMaker with centralized management via REST API and automated task distribution across worker nodes. This eliminates manual work of figuring out how many streams to run per instance and handles task rebalancing automatically. Connect's existing infrastructure reduces the number of clusters to manage and provides consistent operational patterns.

---

## Question 52
**Correct Answer: B**

**Explanation:**
Configuration prefixes in MirrorMaker allow hierarchical configuration with cluster-specific and flow-specific settings. Prefixes like {cluster}.{config}, {source_cluster}.consumer.{config}, and {source_cluster}->{target_cluster}.{config} enable precise control over different components. More specific prefixed configurations have higher precedence than less specific or non-prefixed configurations.

---

## Question 53
**Correct Answer: B**

**Explanation:**
The 2.5 DC architecture is a popular stretch cluster model with two full datacenters running both Kafka and ZooKeeper, plus a third "0.5" datacenter with just one ZooKeeper node. This third ZooKeeper node provides quorum if one full datacenter fails, ensuring ZooKeeper (and thus Kafka) remains available. This is more cost-effective than three full datacenters.

---

## Question 54
**Correct Answer: A**

**Explanation:**
According to the chapter, mirroring solutions currently don't support transactions. This means if related events in multiple topics should be processed together (like sales and line items), during failover some events might arrive at the DR site while others don't, leading to inconsistencies. Applications must be designed to handle these scenarios after failover.

---

## Question 55
**Correct Answer: B**

**Explanation:**
During unplanned failover, some data loss is expected because all mirroring solutions are asynchronous. In a busy system with mirroring lag of even just 5 milliseconds, thousands of messages could be lost during unplanned failover. Planned failover can avoid this by stopping the primary and waiting for mirroring to complete, but unplanned disasters don't allow this luxury.

---

## Question 56
**Correct Answer: B**

**Explanation:**
Increasing TCP buffer sizes (net.core.rmem_default, rmem_max, wmem_default, wmem_max, optmem_max) and enabling automatic window scaling (net.ipv4.tcp_window_scaling=1) can significantly improve cross-datacenter bandwidth utilization. These TCP stack optimizations should be combined with Kafka producer/consumer buffer size configurations (send.buffer.bytes, receive.buffer.bytes) for optimal performance.

---

## Question 57
**Correct Answer: B**

**Explanation:**
On the target cluster, MirrorMaker needs Topic:Write permission to produce to target topics and Topic:Create permission to create mirror topics that don't yet exist. Additional permissions include Topic:Alter to add partitions, Topic:AlterConfigs to update configuration, Group:Read to commit offsets, and Cluster:Alter to update ACLs.

---

## Question 58
**Correct Answer: C**

**Explanation:**
Failover procedures should be practiced at least quarterly according to best practices. A plan that works today may stop working after an upgrade or when new use cases are introduced. Strong SRE teams practice even more frequently than quarterly. Netflix's Chaos Monkey represents the extreme, randomly causing disasters to ensure constant preparedness.

---

## Question 59
**Correct Answer: B**

**Explanation:**
Record headers, introduced in Apache Kafka version 0.11.0, enable events to be tagged with their originating datacenter. This header information can be used to avoid endless mirroring loops and allow separate processing of events from different datacenters. Headers provide a standard way to include metadata about event origin without requiring custom structured data formats.

---

## Question 60
**Correct Answer: B**

**Explanation:**
The `--clusters` option when starting MirrorMaker specifies the target cluster for that particular MirrorMaker process. This is useful when using a shared configuration file containing the full replication topology - different MirrorMaker processes in different datacenters can use the same config file but specify their local target cluster, simplifying configuration management and avoiding conflicts.

---