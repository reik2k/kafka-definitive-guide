# Chapter 10 – Cross-Cluster Data Mirroring – Test | CCDAK Preparation Material

---

## Question 1
What is the primary difference between replication and mirroring in Kafka?
A) Replication is synchronous while mirroring is asynchronous
B) Replication occurs within a cluster while mirroring occurs between clusters
C) Replication is faster than mirroring
D) Mirroring requires ZooKeeper while replication does not

---

## Question 2
Which use case would benefit most from a hub-and-spoke architecture?
A) Active-active disaster recovery
B) Regional data collection with central analytics
C) Real-time bidirectional data synchronization
D) Single datacenter high availability

---

## Question 3
What is the main drawback of the hub-and-spoke architecture?
A) High cost of implementation
B) Complex configuration requirements
C) Processors in one regional datacenter cannot access data from another
D) Poor performance characteristics

---

## Question 4
In cross-cluster communication, why is it recommended to consume from remote datacenters rather than produce to them?
A) Consuming uses less bandwidth
B) If network partition occurs, events remain safe in the source cluster
C) Producing requires more authentication
D) Consumer configuration is simpler

---

## Question 5
What is the benefit of an active-active architecture?
A) Lowest cost implementation
B) Users can be served from nearby datacenters with full functionality
C) Simplest configuration
D) No risk of data conflicts

---

## Question 6
How does active-active architecture handle the challenge of avoiding endless mirroring loops?
A) Using time-based filtering
B) Implementing message deduplication
C) Giving each logical topic a separate topic per datacenter (e.g., NYC.users, SF.users)
D) Disabling auto-replication

---

## Question 7
What is a major challenge with active-active architecture?
A) High latency between datacenters
B) Handling conflicts when data is read and updated asynchronously in multiple locations
C) Excessive bandwidth consumption
D) Limited scalability

---

## Question 8
In an active-standby architecture, what is the main disadvantage?
A) Complex failover procedures
B) Waste of resources as the standby cluster sits idle
C) Poor data consistency
D) Limited throughput capacity

---

## Question 9
What is the Recovery Point Objective (RPO)?
A) The maximum time all services must resume after disaster
B) The maximum amount of time for which data may be lost
C) The average replication lag
D) The time required to restart applications

---

## Question 10
What is the Recovery Time Objective (RTO)?
A) The maximum time before all services must resume after disaster
B) The maximum acceptable data loss period
C) The time to replicate all data
D) The network round-trip time

---

## Question 11
Which failover option uses the `auto.offset.reset` configuration?
A) Offset translation
B) Auto offset reset
C) Time-based failover
D) Replicate offsets topic

---

## Question 12
Why might offsets in the primary and DR clusters diverge?
A) Different partition counts
B) Producer retries and different start times for mirroring
C) Network latency differences
D) Consumer group mismatches

---

## Question 13
What tool can be used for time-based offset reset during failover?
A) kafka-topics
B) kafka-consumer-groups
C) kafka-configs
D) kafka-reassign-partitions

---

## Question 14
What is a stretch cluster in Kafka?
A) Multiple clusters in the same datacenter
B) A single cluster installed across multiple datacenters
C) A cluster with extended retention policies
D) A cluster with increased partition count

---

## Question 15
Why do stretch clusters require at least three datacenters?
A) For load balancing
B) To ensure ZooKeeper maintains a quorum if one datacenter fails
C) To improve network performance
D) For regulatory compliance

---

## Question 16
What is the main advantage of stretch clusters over active-standby architecture?
A) Lower cost
B) Synchronous replication is possible with proper configuration
C) Easier configuration
D) Better performance

---

## Question 17
Which MirrorMaker version is based on Kafka Connect framework?
A) MirrorMaker 1.0
B) MirrorMaker 1.5
C) MirrorMaker 2.0
D) MirrorMaker 3.0

---

## Question 18
What is a replication flow in MirrorMaker?
A) The rate of data transfer
B) A directional configuration from source to target cluster
C) The sequence of topic replication
D) A consumer group assignment

---

## Question 19
In MirrorMaker configuration, how are topics specified for mirroring?
A) By exact names only
B) Using regular expressions
C) Through API calls
D) Automatically detected

---

## Question 20
What is the default naming strategy for mirrored topics in MirrorMaker?
A) Add timestamp suffix
B) Add version number
C) Prefix with source cluster alias (e.g., NYC.orders)
D) Keep the same name

---

## Question 21
Why does MirrorMaker prefix target topics with source cluster alias?
A) To improve performance
B) To prevent replication cycles in active-active mode
C) For better organization
D) To comply with naming standards

---

## Question 22
What does the `tasks.max` configuration control in MirrorMaker?
A) Maximum number of topics to mirror
B) Maximum number of partitions per task
C) Maximum number of tasks the connector may use
D) Maximum throughput limit

---

## Question 23
Which security protocol is recommended for cross-datacenter traffic in MirrorMaker?
A) PLAINTEXT
B) SSL or SASL_SSL
C) SASL_PLAINTEXT
D) KERBEROS

---

## Question 24
What ACL permission does MirrorMaker need on the source cluster?
A) Topic:Write
B) Topic:Read
C) Topic:Delete
D) Cluster:Create

---

## Question 25
Where should MirrorMaker typically be deployed?
A) In the source datacenter
B) In the target datacenter
C) In a separate third datacenter
D) In both source and target datacenters

---

## Question 26
Why is consuming remotely preferred over producing remotely in cross-datacenter setups?
A) Better throughput
B) If connection fails, data remains safe in source cluster
C) Lower latency
D) Simpler authentication

---

## Question 27
What metric shows the time between record timestamp and successful production to target cluster?
A) record-age-ms
B) replication-latency-ms
C) byte-rate
D) checkpoint-latency-ms

---

## Question 28
How does MirrorMaker allocate partitions to tasks?
A) Using Kafka consumer group protocol
B) Random assignment
C) Evenly without using consumer group protocol
D) Based on partition size

---

## Question 29
What configuration ensures MirrorMaker fails fast when it cannot send events?
A) acks=all
B) errors.tolerance=none
C) retries=0
D) fail.fast=true

---

## Question 30
In an active-active topology, how do you prevent the same event from being mirrored endlessly?
A) Set TTL on messages
B) Use message deduplication
C) Remote topics use cluster alias prefix and MirrorMaker doesn't replicate remote topics
D) Implement circular prevention algorithm

---

## Question 31
Which tool developed by Uber addresses MirrorMaker rebalancing issues?
A) Kafka Streams
B) uReplicator
C) Brooklin
D) Confluent Replicator

---

## Question 32
What does uReplicator use for partition assignment?
A) Kafka consumer protocol
B) Apache Helix
C) ZooKeeper directly
D) Custom algorithm

---

## Question 33
Which LinkedIn tool provides a generic data ingestion framework?
A) uReplicator
B) Burrow
C) Brooklin
D) Kafka Connect

---

## Question 34
What is a key feature of Confluent's Cluster Linking?
A) Topic compression
B) Offset-preserving replication across clusters
C) Automatic scaling
D) Built-in encryption

---

## Question 35
Which Confluent feature uses synchronous and asynchronous replication combined?
A) MirrorMaker 2.0
B) Multi-Region Clusters (MRC)
C) Confluent Replicator
D) Schema Registry

---

## Question 36
What are observers in Confluent Server?
A) Monitoring tools
B) Asynchronous replicas that don't join ISR
C) Consumer group members
D) Admin clients

---

## Question 37
For effective failover monitoring, what should be checked for MirrorMaker?
A) CPU usage only
B) Lag between source and target cluster offsets
C) Memory consumption
D) Network bandwidth

---

## Question 38
What is the recommended minimum value for `tasks.max` in production MirrorMaker?
A) 1
B) 2
C) 4
D) 8

---

## Question 39
Which producer configuration can increase MirrorMaker throughput when message order is not critical?
A) linger.ms
B) max.in.flight.requests.per.connection
C) batch.size
D) buffer.memory

---

## Question 40
What happens if you set `linger.ms` higher in MirrorMaker's producer?
A) Increases latency but allows batches to fill up
B) Decreases throughput
C) Improves compression ratio only
D) Reduces memory usage

---

## Question 41
What consumer configuration should be increased if fetch-size metrics are close to fetch.max.bytes?
A) fetch.min.bytes
B) fetch.max.bytes
C) session.timeout.ms
D) max.poll.records

---

## Question 42
In cross-datacenter communication, what is a characteristic of Wide Area Networks (WANs)?
A) High bandwidth and low latency
B) Lower bandwidth and higher costs compared to local networks
C) Unlimited bandwidth
D) No latency differences

---

## Question 43
Which configuration can help with failover by maintaining offset mapping between clusters?
A) Offset translation
B) Auto offset reset
C) Partition reassignment
D) Consumer group coordination

---

## Question 44
What is the purpose of a canary in MirrorMaker monitoring?
A) Load testing
B) Sending test events periodically to verify end-to-end mirroring
C) Measuring network latency
D) Monitoring CPU usage

---

## Question 45
Which tool can provide more sophisticated lag analysis than kafka-consumer-groups?
A) Kafka Manager
B) Burrow
C) Confluent Control Center
D) Cruise Control

---

## Question 46
When should you consider deploying MirrorMaker in the source datacenter?
A) Always for better performance
B) When cross-datacenter traffic requires encryption but local traffic does not
C) To reduce network costs
D) For simpler configuration

---

## Question 47
What is the main risk of remote producing in cross-datacenter setup?
A) Higher latency
B) Events could be lost if network partition occurs before acknowledgment
C) Authentication complexity
D) Lower throughput

---

## Question 48
Which architecture pattern supports failover with minimal manual intervention?
A) Hub-and-spoke
B) Active-active
C) Active-standby
D) Stretch cluster

---

## Question 49
What does the `min.insync.replicas` configuration ensure in stretch clusters?
A) Minimum consumer lag
B) Events are written to minimum number of replicas before acknowledgment
C) Minimum throughput
D) Minimum number of partitions

---

## Question 50
In MirrorMaker, which component is responsible for reading from the source cluster?
A) Producer
B) Consumer task
C) Admin client
D) Coordinator

---

## Question 51
What is the benefit of using Kafka Connect framework for MirrorMaker 2.0?
A) Better performance only
B) Centralized management via REST API and automated task distribution
C) Lower memory usage
D) Simplified network configuration

---

## Question 52
Why are configuration prefixes important in MirrorMaker?
A) To organize files
B) To specify cluster-specific and flow-specific configurations
C) For better logging
D) To improve performance

---

## Question 53
What is the 2.5 DC architecture?
A) 2.5 times the normal cluster size
B) Two full datacenters with a third mini datacenter for ZooKeeper quorum
C) A cluster with 2.5 second latency
D) 2 datacenters with 5 brokers each

---

## Question 54
Which mirroring solution should NOT support transactions according to the chapter?
A) MirrorMaker
B) Cluster Linking
C) Multi-Region Clusters
D) All of the above

---

## Question 55
What happens during unplanned failover in terms of data?
A) No data loss ever
B) Some data loss is expected due to asynchronous mirroring
C) Complete data loss
D) Only metadata is lost

---

## Question 56
What TCP tuning can help increase effective bandwidth for cross-datacenter mirroring?
A) Decrease buffer sizes
B) Increase TCP buffer sizes and enable window scaling
C) Disable TCP timestamps
D) Reduce MTU size

---

## Question 57
Which ACL permission does MirrorMaker need on the target cluster to create topics?
A) Topic:Read
B) Topic:Write and Topic:Create
C) Cluster:Admin
D) Topic:Delete

---

## Question 58
How often should failover procedures be practiced according to best practices?
A) Once a year
B) Every six months
C) At least quarterly
D) Only during actual disasters

---

## Question 59
What feature introduced in Kafka 0.11.0 helps track event origin in cross-datacenter setups?
A) Topic tags
B) Record headers
C) Event metadata
D) Origin attributes

---

## Question 60
In MirrorMaker, what does the `--clusters` option specify when starting the process?
A) List of all available clusters
B) The target cluster for the MirrorMaker process
C) Maximum number of clusters
D) Cluster priority order

---