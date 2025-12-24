# Chapter 7: Reliable Data Delivery — CCDAK Practice Test

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 7

**Total Questions:** 60

[Link to Solutions](../../chapter-tests-solutions/chapter-07-solutions.md)

---

## Question 1
What does reliability mean in the context of Kafka?
A) A property of a single component
B) A property of the entire system
C) Only broker configuration
D) Only client configuration

## Question 2
What does ACID stand for?
A) Atomicity, Concurrency, Isolation, Durability
B) Atomicity, Consistency, Isolation, Durability
C) Availability, Consistency, Isolation, Durability
D) Atomicity, Consistency, Integrity, Durability

## Question 3
How does Kafka guarantee message order?
A) Globally across all partitions
B) Within a partition only
C) Within a topic only
D) No ordering guarantee

## Question 4
When are produced messages considered "committed"?
A) When sent over the network
B) When written to the leader
C) When written to all in-sync replicas
D) When flushed to disk

## Question 5
What can consumers read from Kafka?
A) All messages on any replica
B) Only messages that are committed
C) Only messages on the leader
D) All messages written to disk

## Question 6
What are the conditions for a follower replica to be in-sync?
A) Only has active ZooKeeper session
B) Only fetches messages regularly
C) Has active ZooKeeper session, fetches messages, and has no lag
D) Only replicates the latest message

## Question 7
How long can a replica be inactive before considered out of sync (default)?
A) 6 seconds
B) 10 seconds
C) 18 seconds
D) 30 seconds

## Question 8
What configuration controls ZooKeeper session timeout?
A) session.timeout.ms
B) zookeeper.session.timeout.ms
C) zk.timeout.ms
D) broker.session.timeout.ms

## Question 9
What is the default ZooKeeper session timeout in Kafka 2.5.0+?
A) 6 seconds
B) 10 seconds
C) 18 seconds
D) 30 seconds

## Question 10
What configuration controls maximum replica lag time?
A) replica.max.lag.ms
B) replica.lag.time.max.ms
C) max.replica.lag.time.ms
D) replica.timeout.ms

## Question 11
What is the default replication factor for topics?
A) 1
B) 2
C) 3
D) 5

## Question 12
With a replication factor of N, how many brokers can fail while maintaining availability?
A) N
B) N-1
C) N-2
D) N/2

## Question 13
What is the broker configuration for default replication factor?
A) replication.factor
B) default.replication.factor
C) broker.replication.factor
D) topic.replication.factor

## Question 14
What is the topic-level configuration for replication factor?
A) replication.factor
B) topic.replication.factor
C) min.replication.factor
D) default.replication.factor

## Question 15
What configuration prevents brokers from accepting writes with insufficient replicas?
A) min.replicas
B) min.insync.replicas
C) required.replicas
D) min.available.replicas

## Question 16
With 3 replicas and min.insync.replicas=2, what happens when 2 replicas fail?
A) System continues normally
B) Brokers reject produce requests
C) Consumers cannot read
D) Topic is deleted

## Question 17
What exception is thrown when not enough replicas are in sync?
A) InsufficientReplicasException
B) NotEnoughReplicasException
C) MinimumReplicasException
D) ReplicaAvailabilityException

## Question 18
What is unclean leader election?
A) Electing any available broker as leader
B) Electing an out-of-sync replica as leader
C) Electing the preferred leader
D) Automatic leader rebalancing

## Question 19
What is the default value for unclean.leader.election.enable?
A) true
B) false
C) auto
D) warn

## Question 20
What is the risk of enabling unclean leader election?
A) Slower performance
B) Data loss and inconsistencies
C) Higher CPU usage
D) More network traffic

## Question 21
What configuration is broker.rack used for?
A) Physical rack organization
B) Ensuring replicas spread across racks for availability
C) Network configuration
D) Storage configuration

## Question 22
What does flush.messages configuration control?
A) Number of messages before sync to disk
B) Message compression
C) Message batching
D) Network buffer size

## Question 23
Why does Kafka rely on page cache instead of forcing disk sync?
A) Better performance
B) Three replicas on separate machines is safer than disk sync
C) Disk sync is not supported
D) Page cache is more reliable

## Question 24
What are the three producer acks settings?
A) 0, 1, 2
B) 0, 1, all
C) none, one, all
D) 0, leader, all

## Question 25
What does acks=0 mean?
A) No acknowledgment needed
B) Wait for leader acknowledgment
C) Wait for all replicas
D) Auto-acknowledge

## Question 26
What does acks=1 mean?
A) Wait for one follower
B) Wait for leader only
C) Wait for all in-sync replicas
D) No acknowledgment

## Question 27
What does acks=all mean?
A) Wait for all brokers
B) Wait for all in-sync replicas
C) Wait for all followers
D) Wait for all partitions

## Question 28
Which acks setting provides the strongest durability guarantee?
A) acks=0
B) acks=1
C) acks=all
D) All provide same guarantee

## Question 29
What is the default number of producer retries?
A) 0
B) 3
C) 10
D) MAX_INT (effectively infinite)

## Question 30
What configuration controls maximum time for delivery attempts?
A) delivery.timeout.ms
B) max.delivery.time.ms
C) request.timeout.ms
D) send.timeout.ms

## Question 31
What does enable.idempotence=true do?
A) Prevents duplicates from retries
B) Increases performance
C) Enables compression
D) Disables retries

## Question 32
What types of errors can producers retry?
A) All errors
B) Only retriable errors
C) No errors
D) Only network errors

## Question 33
What is an example of a retriable error?
A) INVALID_CONFIG
B) LEADER_NOT_AVAILABLE
C) CORRUPT_MESSAGE
D) AUTHORIZATION_FAILED

## Question 34
What is an example of a non-retriable error?
A) NETWORK_EXCEPTION
B) LEADER_NOT_AVAILABLE
C) INVALID_CONFIG
D) REQUEST_TIMED_OUT

## Question 35
What must consumers track to avoid losing messages?
A) Message timestamps
B) Which messages have been processed (offsets)
C) Message sizes
D) Producer IDs

## Question 36
What is a committed offset?
A) A message written to all replicas
B) An offset the consumer sent to Kafka acknowledging processing
C) An offset written to disk
D) An offset in the transaction log

## Question 37
What does auto.offset.reset control?
A) Automatic offset commits
B) What consumer does when no valid offset exists
C) Offset commit frequency
D) Offset retention period

## Question 38
What are the two options for auto.offset.reset?
A) beginning and end
B) earliest and latest
C) start and finish
D) first and last

## Question 39
What does auto.offset.reset=earliest do?
A) Start from the latest message
B) Start from the beginning of the partition
C) Fail if no offset exists
D) Start from timestamp 0

## Question 40
What does auto.offset.reset=latest do?
A) Start from the beginning
B) Start from the end of the partition
C) Use the last committed offset
D) Start from the middle

## Question 41
What does enable.auto.commit control?
A) Producer commits
B) Whether consumer automatically commits offsets
C) Broker commits
D) Transaction commits

## Question 42
What is the default auto commit interval?
A) 1 second
B) 5 seconds
C) 10 seconds
D) 30 seconds

## Question 43
What happens if a consumer crashes after reading but before committing offsets?
A) No impact
B) Messages are lost
C) Messages may be processed twice
D) Partition becomes unavailable

## Question 44
What happens if a consumer commits offsets before processing messages?
A) No impact
B) Messages may be lost
C) Messages processed twice
D) Better performance

## Question 45
When should offsets be committed?
A) Before processing messages
B) After processing messages
C) During processing
D) At random intervals

## Question 46
What is the trade-off in commit frequency?
A) Performance vs. duplicates in event of crash
B) Latency vs. throughput
C) Memory vs. disk
D) CPU vs. network

## Question 47
What consumer method pauses consumption?
A) stop()
B) pause()
C) halt()
D) suspend()

## Question 48
What should be done before partitions are revoked during rebalance?
A) Nothing
B) Commit offsets
C) Clear buffers
D) Close connections

## Question 49
How does Kafka guarantee exactly-once semantics?
A) Through careful offset management
B) Through idempotent producers and transactional writes
C) Through acks=all
D) Through replication

## Question 50
What tool can validate producer and consumer reliability?
A) kafka-console-test
B) VerifiableProducer and VerifiableConsumer
C) kafka-test-suite
D) ReliabilityValidator

## Question 51
What does VerifiableProducer do?
A) Validates topic configuration
B) Produces numbered sequence of messages
C) Tests broker performance
D) Validates consumer groups

## Question 52
What does VerifiableConsumer do?
A) Validates topic schemas
B) Consumes and prints events in order with commit info
C) Tests consumer performance
D) Validates message formats

## Question 53
What is an important reliability test scenario?
A) Maximum throughput test
B) Leader election during production/consumption
C) Schema validation
D) Compression ratio test

## Question 54
What metric indicates consumer is falling behind?
A) Consumer throughput
B) Consumer lag
C) Message rate
D) Partition count

## Question 55
What is consumer lag?
A) Network latency
B) Difference between latest offset and consumer position
C) Processing time per message
D) Commit frequency

## Question 56
What broker metric shows failed produce requests?
A) ProduceRequestsPerSec
B) FailedProduceRequestsPerSec
C) ErrorRate
D) ProduceErrors

## Question 57
What broker metric shows failed fetch requests?
A) FetchRequestsPerSec
B) FailedFetchRequestsPerSec
C) ConsumerErrors
D) FetchErrors

## Question 58
What tool helps monitor consumer lag?
A) Kafka Manager
B) Burrow
C) Prometheus
D) JMX Console

## Question 59
When did Kafka start including timestamps in messages?
A) 0.8.0
B) 0.9.0
C) 0.10.0
D) 0.11.0

## Question 60
What is the relationship between reliability and other system properties?
A) No trade-offs necessary
B) Trade-offs with availability, throughput, latency, and costs
C) Only affects performance
D) Only affects costs

---

**End of Test**

[Link to Solutions](../../chapter-tests-solutions/chapter-07-solutions.md)