# Chapter 4: Kafka Consumers - Reading Data from Kafka - Solutions
**CCDAK Practice Test Solutions**

[Back to Test](../../chapter-tests/chapter-04-test.md) | [Main README](../../README.md)

---

## Answer Key

## **Question 1**
**Explanation:** These are the three mandatory properties. group.id is commonly used but not strictly mandatory.

## **Question 2**
**Explanation:** If there are more consumers than partitions, the extra consumers will remain idle with no partition assignments.

## **Question 3**
**Explanation:** With 4 partitions and 2 consumers, partitions are evenly distributed, giving each consumer 2 partitions.

## **Question 4**
**Explanation:** Rebalance is the process of reassigning partition ownership when consumers join/leave or topics change.

## **Question 5**
**Explanation:** Kafka has two rebalance types: eager (stop-the-world) and cooperative (incremental).

## **Question 6**
**Explanation:** Cooperative rebalancing is incremental and avoids the complete pause that occurs with eager rebalancing.

## **Question 7**
**Explanation:** Consumers send heartbeats via a background thread to maintain group membership.

## **Question 8**
**Explanation:** When heartbeats stop for longer than session.timeout.ms, the consumer is considered dead and rebalancing occurs.

## **Question 9**
**Explanation:** Static members maintain their partition assignments across restarts without triggering rebalances.

## **Question 10**
**Explanation:** The subscribe() method is used to subscribe to one or more topics.

## **Question 11**
**Explanation:** You can use Pattern.compile() to subscribe to topics matching a regular expression.

## **Question 12**
**Explanation:** The poll loop is the core of consumer processing, continuously fetching and processing records.

## **Question 13**
**Explanation:** poll() returns a ConsumerRecords object containing multiple ConsumerRecord items.

## **Question 14**
**Explanation:** If poll() isn't called within max.poll.interval.ms, the consumer is deemed non-responsive and removed.

## **Question 15**
**Explanation:** KafkaConsumer is not thread-safe. Each consumer must run in its own thread.

## **Question 16**
**Explanation:** fetch.min.bytes sets the minimum amount of data the broker waits to accumulate before responding.

## **Question 17**
**Explanation:** fetch.max.wait.ms limits how long the broker waits before responding, even if fetch.min.bytes isn't reached.

## **Question 18**
**Explanation:** The default fetch.max.bytes is 50 MB.

## **Question 19**
**Explanation:** max.poll.records limits the number of records returned in one poll() call.

## **Question 20**
**Explanation:** Heartbeat interval must be lower than session timeout, typically set to one-third.

## **Question 21**
**Explanation:** The default session.timeout.ms is 10 seconds (10000 ms).

## **Question 22**
**Explanation:** max.poll.interval.ms detects when the main thread is stuck processing while heartbeats continue.

## **Question 23**
**Explanation:** auto.offset.reset determines what offset to use when there's no committed offset or it's invalid.

## **Question 24**
**Explanation:** Valid values are: latest (newest records), earliest (oldest records), or none (throw exception).

## **Question 25**
**Explanation:** enable.auto.commit controls whether offsets are committed automatically during poll().

## **Question 26**
**Explanation:** The default auto.commit.interval.ms is 5000 milliseconds (5 seconds).

### 27. A, B, C, E (Range, RoundRobin, Sticky, CooperativeSticky)
**Explanation:** Kafka provides Range, RoundRobin, Sticky, and CooperativeSticky assignment strategies. Random is not a standard strategy.

## **Question 28**
**Explanation:** Range assigns consecutive partitions from each topic to consumers.

## **Question 29**
**Explanation:** CooperativeSticky is the only strategy that supports cooperative (incremental) rebalancing.

## **Question 30**
**Explanation:** client.rack enables rack-aware replica selection for fetching from the closest replica.

## **Question 31**
**Explanation:** Offset commit updates the consumer's current position (last processed offset) in a partition.

## **Question 32**
**Explanation:** Committed offsets are stored in the internal __consumer_offsets topic.

## **Question 33**
**Explanation:** If committed offset < last processed, messages between them will be reprocessed after rebalance.

## **Question 34**
**Explanation:** If committed offset > last processed, messages between them will not be consumed.

## **Question 35**
**Explanation:** With auto-commit enabled, offsets are committed at regular intervals during poll() calls.

## **Question 36**
**Explanation:** Auto-commit can cause duplicates if rebalance happens between processing and the next commit.

## **Question 37**
**Explanation:** commitSync() commits synchronously, blocking until the broker responds.

## **Question 38**
**Explanation:** commitSync() automatically retries on retriable errors.

## **Question 39**
**Explanation:** commitAsync() doesn't block waiting for broker response, improving throughput.

## **Question 40**
**Explanation:** Retrying failed commits could succeed out of order, potentially committing older offsets after newer ones.

## **Question 41**
**Explanation:** This pattern uses async commits normally for performance, sync on shutdown to ensure final commit succeeds.

## **Question 42**
**Explanation:** Both commitSync() and commitAsync() can accept a map of specific offsets to commit.

## **Question 43**
**Explanation:** Implement ConsumerRebalanceListener to receive rebalance notifications.

## **Question 44**
**Explanation:** onPartitionsRevoked() is called before the consumer gives up partitions during rebalance.

## **Question 45**
**Explanation:** onPartitionsAssigned() is called after assignment but before poll() starts returning records.

## **Question 46**
**Explanation:** onPartitionsLost() handles exceptional cooperative rebalance scenarios.

## **Question 47**
**Explanation:** seekToBeginning() resets offset to the earliest available offset for specified partitions.

## **Question 48**
**Explanation:** seekToEnd() moves offset to the end, so only new messages will be consumed.

## **Question 49**
**Explanation:** wakeup() interrupts poll(), then close() cleanly shuts down the consumer.

## **Question 50**
**Explanation:** wakeup() causes poll() to throw WakeupException.

## **Question 51**
**Explanation:** wakeup() is specifically designed to be called from a different thread safely.

## **Question 52**
**Explanation:** The producer's serializer must match the consumer's deserializer for the data format.

## **Question 53**
**Explanation:** Standard serialization formats provide schema evolution and better compatibility than custom deserializers.

## **Question 54**
**Explanation:** KafkaAvroDeserializer needs schema.registry.url to retrieve schemas.

## **Question 55**
**Explanation:** Standalone consumers use assign() to manually assign specific partitions.

## **Question 56**
**Explanation:** A consumer can either subscribe to topics OR assign partitions, but not both simultaneously.

## **Question 57**
**Explanation:** The first poll() handles all group coordination before returning records.

## **Question 58**
**Explanation:** offsets.retention.minutes controls how long Kafka retains offsets for inactive consumer groups.

## **Question 59**
**Explanation:** The default offsets.retention.minutes is 10080 minutes (7 days).

## **Question 60**
**Explanation:** max.partition.fetch.bytes controls the maximum bytes returned per partition (default 1 MB).

---

## Study Tips

### Key Concepts to Master:
1. **Consumer Groups**: Partition assignment, rebalancing (eager vs cooperative), group coordination
2. **Configuration**: Mandatory properties, fetch settings, timeouts (session, heartbeat, poll interval)
3. **Offset Management**: Commits (auto, sync, async, specific), offset storage, reset behavior
4. **Poll Loop**: poll() mechanics, thread safety, shutdown procedures
5. **Partition Assignment**: Strategies (Range, RoundRobin, Sticky, CooperativeSticky)
6. **Rebalance Listeners**: onPartitionsRevoked, onPartitionsAssigned, onPartitionsLost
7. **Seek Operations**: seekToBeginning, seekToEnd, seek to specific offsets
8. **Deserialization**: Standard formats (Avro), Schema Registry integration
9. **Standalone Consumers**: Manual partition assignment with assign()
10. **Consumer Lifecycle**: Startup, operation, shutdown (wakeup, close)

### Related CCDAK Topics:
- Consumer API patterns and best practices
- Offset commit strategies for reliability
- Rebalance handling and optimization
- Performance tuning (fetch sizes, poll intervals)
- Consumer monitoring and metrics
- Error handling and recovery
- Schema evolution with Avro
- Multi-threaded consumer applications

---

[Back to Test](../../chapter-tests/chapter-04-test.md) | [Main README](../../README.md)