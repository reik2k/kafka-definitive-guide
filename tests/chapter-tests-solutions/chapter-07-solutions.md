# Chapter 7: Reliable Data Delivery — Solutions
CCDAK Practice Test Solutions
**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 7

[Back to Test](../../chapter-tests/chapter-07-test.md) | [Main README](../../README.md)

---

## Answer Key

### Answer 1: 

**B) A property of the entire system**


**Explanation:** Reliability is a property of a system, not of a single component. Building a reliable system requires coordination among Kafka administrators, Linux administrators, network/storage administrators, and application developers.

### Answer 2: 

**B) Atomicity, Consistency, Isolation, Durability**


**Explanation:** ACID stands for Atomicity, Consistency, Isolation, and Durability—the standard reliability guarantee for relational databases.

### Answer 3: 

**B) Within a partition only**


**Explanation:** Kafka provides order guarantee of messages within a partition. If message B was written after message A in the same partition, B will have a higher offset and consumers will read B after A.

### Answer 4: 

**C) When written to all in-sync replicas**


**Explanation:** Messages are considered "committed" when written to the partition on all its in-sync replicas (but not necessarily flushed to disk).

### Answer 5: 

**B) Only messages that are committed**


**Explanation:** Consumers can only read messages that are committed (written to all in-sync replicas).

### Answer 6: 

**C) Has active ZooKeeper session, fetches messages, and has no lag**


**Explanation:** A replica is in-sync if it has an active ZooKeeper session (heartbeat in last 6s), fetched messages from leader in last 10s, and caught up with no lag in last 10s.

### Answer 7: 

**D) 30 seconds**


**Explanation:** The default replica.lag.time.max.ms is 30 seconds in Kafka 2.5.0+ (increased from 10 seconds to improve resilience).

### Answer 8: 

**B) zookeeper.session.timeout.ms**


**Explanation:** zookeeper.session.timeout.ms controls how long a broker can stop sending heartbeats before ZooKeeper considers it dead.

### Answer 9: 

**C) 18 seconds**


**Explanation:** In version 2.5.0, zookeeper.session.timeout.ms was increased from 6 seconds to 18 seconds for better stability in cloud environments.

### Answer 10: 

**B) replica.lag.time.max.ms**


**Explanation:** replica.lag.time.max.ms controls how long a follower can be inactive or behind before being considered out of sync.

### Answer 11: 

**C) 3**


**Explanation:** The default replication factor is 3, meaning each partition is replicated three times on three different brokers.

### Answer 12: 

**B) N-1**


**Explanation:** A replication factor of N allows losing N-1 brokers while still being able to read and write data to the topic.

### Answer 13: 

**B) default.replication.factor**


**Explanation:** default.replication.factor is the broker-level configuration for automatically created topics.

### Answer 14: 

**A) replication.factor**


**Explanation:** replication.factor is the topic-level configuration for setting replication.

### Answer 15: 

**B) min.insync.replicas**


**Explanation:** min.insync.replicas sets the minimum number of in-sync replicas required for producers to write successfully.

### Answer 16: 

**B) Brokers reject produce requests**


**Explanation:** With min.insync.replicas=2 and only 1 replica in sync, brokers reject produce requests with NotEnoughReplicasException.

### Answer 17: 

**B) NotEnoughReplicasException**


**Explanation:** When insufficient replicas are in sync, producers receive NotEnoughReplicasException.

### Answer 18: 

**B) Electing an out-of-sync replica as leader**


**Explanation:** Unclean leader election allows an out-of-sync replica to become leader when no in-sync replicas are available.

### Answer 19: 

**B) false**


**Explanation:** By default, unclean.leader.election.enable is false, preventing data loss from out-of-sync leaders.

### Answer 20: 

**B) Data loss and inconsistencies**


**Explanation:** Unclean leader election risks data loss (messages not replicated to new leader) and consumer inconsistencies.

### Answer 21: 

**B) Ensuring replicas spread across racks for availability**


**Explanation:** broker.rack ensures replicas for a partition are spread across multiple racks for higher availability.

### Answer 22: 

**A) Number of messages before sync to disk**


**Explanation:** flush.messages controls the maximum number of messages not synced to disk before forcing a flush.

### Answer 23: 

**B) Three replicas on separate machines is safer than disk sync**


**Explanation:** Having three replicas on separate racks/zones is safer than forcing disk sync on the leader, since simultaneous failures are unlikely.

### Answer 24: 

**B) 0, 1, all**


**Explanation:** The three producer acks settings are 0 (no ack), 1 (leader only), and all (all in-sync replicas).

### Answer 25: 

**A) No acknowledgment needed**


**Explanation:** acks=0 means messages are considered written if successfully sent over the network, with no broker acknowledgment.

### Answer 26: 

**B) Wait for leader only**


**Explanation:** acks=1 means the leader sends acknowledgment after writing the message to its partition data file.

### Answer 27: 

**B) Wait for all in-sync replicas**


**Explanation:** acks=all means the leader waits for all in-sync replicas to receive the message before acknowledging.

### Answer 28: 

**C) acks=all**


**Explanation:** acks=all provides the strongest durability guarantee by ensuring messages are replicated to all in-sync replicas.

### Answer 29: 

**D) MAX_INT (effectively infinite)**


**Explanation:** The default number of producer retries is MAX_INT (effectively infinite), controlled by delivery.timeout.ms.

### Answer 30: 

**A) delivery.timeout.ms**


**Explanation:** delivery.timeout.ms configures the maximum time for delivery attempts, within which the producer will retry.

### Answer 31: 

**A) Prevents duplicates from retries**


**Explanation:** enable.idempotence=true causes the producer to include information that helps brokers skip duplicate messages from retries.

### Answer 32: 

**B) Only retriable errors**


**Explanation:** Producers can automatically retry only retriable errors like LEADER_NOT_AVAILABLE, not errors like INVALID_CONFIG.

### Answer 33: 

**B) LEADER_NOT_AVAILABLE**


**Explanation:** LEADER_NOT_AVAILABLE is a retriable error—a new broker may be elected and the retry could succeed.

### Answer 34: 

**C) INVALID_CONFIG**


**Explanation:** INVALID_CONFIG is a non-retriable error—retrying won't change the configuration issue.

### Answer 35: 

**B) Which messages have been processed (offsets)**


**Explanation:** Consumers must track which messages have been processed by committing offsets to avoid losing messages.

### Answer 36: 

**B) An offset the consumer sent to Kafka acknowledging processing**


**Explanation:** A committed offset is an offset the consumer sent to Kafka to acknowledge it processed all messages up to that offset.

### Answer 37: 

**B) What consumer does when no valid offset exists**


**Explanation:** auto.offset.reset controls consumer behavior when starting without a valid offset (e.g., first start or offset expired).

### Answer 38: 

**B) earliest and latest**


**Explanation:** The two options for auto.offset.reset are earliest (start from beginning) and latest (start from end).

### Answer 39: 

**B) Start from the beginning of the partition**


**Explanation:** auto.offset.reset=earliest causes the consumer to start from the beginning when no valid offset exists.

### Answer 40: 

**B) Start from the end of the partition**


**Explanation:** auto.offset.reset=latest causes the consumer to start at the end of the partition, minimizing duplicates but risking message loss.

### Answer 41: 

**B) Whether consumer automatically commits offsets**


**Explanation:** enable.auto.commit determines if the consumer automatically commits offsets on a schedule.

### Answer 42: 

**B) 5 seconds**


**Explanation:** The default auto.commit.interval.ms is 5 seconds.

### Answer 43: 

**C) Messages may be processed twice**


**Explanation:** If a consumer crashes after reading but before committing, another consumer will re-process those messages.

### Answer 44: 

**B) Messages may be lost**


**Explanation:** Committing offsets before processing means if the consumer crashes, those messages are marked as processed but weren't actually processed.

### Answer 45: 

**B) After processing messages**


**Explanation:** Offsets should always be committed after messages are processed to avoid losing messages.

### Answer 46: 

**A) Performance vs. duplicates in event of crash**


**Explanation:** Commit frequency balances performance overhead against the number of duplicate messages processed after a crash.

### Answer 47: 

**B) pause()**


**Explanation:** The pause() method temporarily stops the consumer from fetching messages from specified partitions.

### Answer 48: 

**B) Commit offsets**


**Explanation:** Before partitions are revoked during rebalance, the application should commit offsets to avoid reprocessing.

### Answer 49: 

**B) Through idempotent producers and transactional writes**


**Explanation:** Kafka achieves exactly-once semantics through idempotent producers (preventing retry duplicates) and transactional writes.

### Answer 50: 

**B) VerifiableProducer and VerifiableConsumer**


**Explanation:** VerifiableProducer and VerifiableConsumer are tools in org.apache.kafka.tools for validating reliability.

### Answer 51: 

**B) Produces numbered sequence of messages**


**Explanation:** VerifiableProducer produces a sequence of messages containing numbers, printing success or error for each.

### Answer 52: 

**B) Consumes and prints events in order with commit info**


**Explanation:** VerifiableConsumer consumes events and prints them in order along with commit and rebalance information.

### Answer 53: 

**B) Leader election during production/consumption**


**Explanation:** Testing leader election during active production/consumption is important for validating system continues without data loss.

### Answer 54: 

**B) Consumer lag**


**Explanation:** Consumer lag indicates how far the consumer is from the latest message committed to the partition.

### Answer 55: 

**B) Difference between latest offset and consumer position**


**Explanation:** Consumer lag is the difference between the latest committed offset in the partition and the consumer's current position.

### Answer 56: 

**B) FailedProduceRequestsPerSec**


**Explanation:** kafka.server:type=BrokerTopicMetrics,name=FailedProduceRequestsPerSec tracks failed produce requests.

### Answer 57: 

**B) FailedFetchRequestsPerSec**


**Explanation:** kafka.server:type=BrokerTopicMetrics,name=FailedFetchRequestsPerSec tracks failed fetch requests.

### Answer 58: 

**B) Burrow**


**Explanation:** Burrow is a consumer lag checker by LinkedIn that makes monitoring lag easier than traditional alerts.

### Answer 59: 

**C) 0.10.0**


**Explanation:** Starting with version 0.10.0, all Kafka messages include a timestamp indicating when the event was produced.

### Answer 60: 

**B) Trade-offs with availability, throughput, latency, and costs**


**Explanation:** Reliability involves trade-offs with availability, throughput, latency, and hardware/storage costs.

---

## Study Tips

### Key Concepts to Master:
1. **Reliability Guarantees:** Message order, committed messages, consumer-only reads
2. **Replication:** In-sync replicas, replica lag, ZooKeeper sessions
3. **Broker Configuration:** Replication factor, min.insync.replicas, unclean leader election
4. **Producer Reliability:** acks settings, retries, idempotence, error handling
5. **Consumer Reliability:** Offset management, auto.offset.reset, commit strategies
6. **Validation:** VerifiableProducer/Consumer, testing scenarios, monitoring

### Related CCDAK Topics:
- Reliability trade-offs and system design
- Producer and consumer configuration for reliability
- Offset management and commit strategies
- Monitoring consumer lag and failed requests
- Testing reliability under failure conditions
- Idempotent producers and exactly-once semantics

---

[Back to Test](../../chapter-tests/chapter-07-test.md) | [Main README](../../README.md)