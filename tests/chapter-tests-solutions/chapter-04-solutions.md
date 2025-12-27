# Chapter 4: Kafka Consumers - Reading Data from Kafka - Solutions
CCDAK Practice Test Solutions
**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 4

[Back to Test](../../chapter-tests/chapter-04-test.md) | [Main README](../../README.md)

---

## Answer Key

### Answer 1

1. A) bootstrap.servers, key.deserializer, value.deserializer

**Explanation:** 

*These are the three mandatory properties. group.id is commonly used but not strictly mandatory.*


### Answer 2

2. B) The extra consumers will be idle and receive no messages

**Explanation:** 

*If there are more consumers than partitions, the extra consumers will remain idle with no partition assignments.*


### Answer 3

3. B) Each consumer reads from 2 partitions

**Explanation:** 

*With 4 partitions and 2 consumers, partitions are evenly distributed, giving each consumer 2 partitions.*


### Answer 4

4. B) Reassigning partitions to consumers in a group

**Explanation:** 

*Rebalance is the process of reassigning partition ownership when consumers join/leave or topics change.*


### Answer 5

5. B) Eager and cooperative

**Explanation:** 

*Kafka has two rebalance types: eager (stop-the-world) and cooperative (incremental).*


### Answer 6

6. B) Cooperative only reassigns a subset of partitions and allows continued consumption

**Explanation:** 

*Cooperative rebalancing is incremental and avoids the complete pause that occurs with eager rebalancing.*


### Answer 7

7. A) By sending heartbeats to the group coordinator

**Explanation:** 

*Consumers send heartbeats via a background thread to maintain group membership.*


### Answer 8

8. B) The group coordinator considers it dead and triggers a rebalance

**Explanation:** 

*When heartbeats stop for longer than session.timeout.ms, the consumer is considered dead and rebalancing occurs.*


### Answer 9

9. B) Consumers with unique group.instance.id that retain partitions across restarts

**Explanation:** 

*Static members maintain their partition assignments across restarts without triggering rebalances.*


### Answer 10

10. A) consumer.subscribe()

**Explanation:** 

*The subscribe() method is used to subscribe to one or more topics.*


### Answer 11

11. B) Yes, for matching multiple topic names

**Explanation:** 

*You can use Pattern.compile() to subscribe to topics matching a regular expression.*


### Answer 12

12. B) The main loop where consumers continuously poll Kafka for data

**Explanation:** 

*The poll loop is the core of consumer processing, continuously fetching and processing records.*


### Answer 13

13. C) ConsumerRecords collection

**Explanation:** 

*poll() returns a ConsumerRecords object containing multiple ConsumerRecord items.*


### Answer 14

14. B) Consumer is considered dead and evicted from the group

**Explanation:** 

*If poll() isn't called within max.poll.interval.ms, the consumer is deemed non-responsive and removed.*


### Answer 15

15. B) No, one consumer per thread is the rule

**Explanation:** 

*KafkaConsumer is not thread-safe. Each consumer must run in its own thread.*


### Answer 16

16. B) Minimum data broker sends before responding to consumer

**Explanation:** 

*fetch.min.bytes sets the minimum amount of data the broker waits to accumulate before responding.*


### Answer 17

17. A) Maximum time to wait for fetch.min.bytes of data

**Explanation:** 

*fetch.max.wait.ms limits how long the broker waits before responding, even if fetch.min.bytes isn't reached.*


### Answer 18

18. C) 50 MB

**Explanation:** 

*The default fetch.max.bytes is 50 MB.*


### Answer 19

19. B) Maximum records returned by a single poll()

**Explanation:** 

*max.poll.records limits the number of records returned in one poll() call.*


### Answer 20

20. B) heartbeat.interval.ms should be lower, typically 1/3 of session.timeout.ms

**Explanation:** 

*Heartbeat interval must be lower than session timeout, typically set to one-third.*


### Answer 21

21. C) 10 seconds

**Explanation:** 

*The default session.timeout.ms is 10 seconds (10000 ms).*


### Answer 22

22. B) Deadlocked main thread while background thread sends heartbeats

**Explanation:** 

*max.poll.interval.ms detects when the main thread is stuck processing while heartbeats continue.*


### Answer 23

23. B) Behavior when consumer starts with no valid offset

**Explanation:** 

*auto.offset.reset determines what offset to use when there's no committed offset or it's invalid.*


### Answer 24

24. A) latest, earliest, none

**Explanation:** 

*Valid values are: latest (newest records), earliest (oldest records), or none (throw exception).*


### Answer 25

25. B) Whether consumer automatically commits offsets

**Explanation:** 

*enable.auto.commit controls whether offsets are committed automatically during poll().*


### Answer 26

26. B) 5 seconds

**Explanation:** 

*The default auto.commit.interval.ms is 5000 milliseconds (5 seconds).*


### 27. A, B, C, E (Range, RoundRobin, Sticky, CooperativeSticky)
**Explanation:** 

*Kafka provides Range, RoundRobin, Sticky, and CooperativeSticky assignment strategies. Random is not a standard strategy.*


### Answer 28

28. B) Range

**Explanation:** 

*Range assigns consecutive partitions from each topic to consumers.*


### Answer 29

29. D) CooperativeSticky

**Explanation:** 

*CooperativeSticky is the only strategy that supports cooperative (incremental) rebalancing.*


### Answer 30

30. B) Fetching from closest replica

**Explanation:** 

*client.rack enables rack-aware replica selection for fetching from the closest replica.*


### Answer 31

31. B) Updating current position in partition

**Explanation:** 

*Offset commit updates the consumer's current position (last processed offset) in a partition.*


### Answer 32

32. B) In __consumer_offsets topic

**Explanation:** 

*Committed offsets are stored in the internal __consumer_offsets topic.*


### Answer 33

33. B) Messages are processed twice

**Explanation:** 

*If committed offset < last processed, messages between them will be reprocessed after rebalance.*


### Answer 34

34. B) Messages between offsets are missed

**Explanation:** 

*If committed offset > last processed, messages between them will not be consumed.*


### Answer 35

35. B) Every auto.commit.interval.ms during poll()

**Explanation:** 

*With auto-commit enabled, offsets are committed at regular intervals during poll() calls.*


### Answer 36

36. B) Cannot eliminate duplicate messages during rebalance

**Explanation:** 

*Auto-commit can cause duplicates if rebalance happens between processing and the next commit.*


### Answer 37

37. B) Commits latest offset from poll() and blocks until complete

**Explanation:** 

*commitSync() commits synchronously, blocking until the broker responds.*


### Answer 38

38. B) It retries until success or unrecoverable error

**Explanation:** 

*commitSync() automatically retries on retriable errors.*


### Answer 39

39. B) Better throughput, doesn't block

**Explanation:** 

*commitAsync() doesn't block waiting for broker response, improving throughput.*


### Answer 40

40. B) Later commits may have already succeeded, causing order issues

**Explanation:** 

*Retrying failed commits could succeed out of order, potentially committing older offsets after newer ones.*


### Answer 41

41. A) Use commitAsync() in loop, commitSync() before shutdown

**Explanation:** 

*This pattern uses async commits normally for performance, sync on shutdown to ensure final commit succeeds.*


### Answer 42

42. B) Yes, by passing a map of partitions and offsets

**Explanation:** 

*Both commitSync() and commitAsync() can accept a map of specific offsets to commit.*


### Answer 43

43. B) ConsumerRebalanceListener

**Explanation:** 

*Implement ConsumerRebalanceListener to receive rebalance notifications.*


### Answer 44

44. B) Before losing ownership of partitions

**Explanation:** 

*onPartitionsRevoked() is called before the consumer gives up partitions during rebalance.*


### Answer 45

45. B) After partitions are assigned but before consumption starts

**Explanation:** 

*onPartitionsAssigned() is called after assignment but before poll() starts returning records.*


### Answer 46

46. B) Exceptional cases with cooperative rebalancing where partitions were reassigned without revocation

**Explanation:** 

*onPartitionsLost() handles exceptional cooperative rebalance scenarios.*


### Answer 47

47. B) Starts reading from beginning of specified partitions

**Explanation:** 

*seekToBeginning() resets offset to the earliest available offset for specified partitions.*


### Answer 48

48. B) Starts consuming only new messages from specified partitions

**Explanation:** 

*seekToEnd() moves offset to the end, so only new messages will be consumed.*


### Answer 49

49. B) Call consumer.wakeup() from another thread, then consumer.close()

**Explanation:** 

*wakeup() interrupts poll(), then close() cleanly shuts down the consumer.*


### Answer 50

50. B) WakeupException

**Explanation:** 

*wakeup() causes poll() to throw WakeupException.*


### Answer 51

51. B) Yes, it's the only thread-safe consumer method

**Explanation:** 

*wakeup() is specifically designed to be called from a different thread safely.*


### Answer 52

52. B) Serializer and deserializer for the data

**Explanation:** 

*The producer's serializer must match the consumer's deserializer for the data format.*


### Answer 53

53. B) Standard formats like Avro, Thrift, or Protobuf

**Explanation:** 

*Standard serialization formats provide schema evolution and better compatibility than custom deserializers.*


### Answer 54

54. B) schema.registry.url

**Explanation:** 

*KafkaAvroDeserializer needs schema.registry.url to retrieve schemas.*


### Answer 55

55. B) Use assign() with specific partitions

**Explanation:** 

*Standalone consumers use assign() to manually assign specific partitions.*


### Answer 56

56. B) No, it's one or the other

**Explanation:** 

*A consumer can either subscribe to topics OR assign partitions, but not both simultaneously.*


### Answer 57

57. B) Finds GroupCoordinator, joins group, receives partition assignment

**Explanation:** 

*The first poll() handles all group coordination before returning records.*


### Answer 58

58. B) How long committed offsets are retained after group becomes empty

**Explanation:** 

*offsets.retention.minutes controls how long Kafka retains offsets for inactive consumer groups.*


### Answer 59

59. B) 7 days

**Explanation:** 

*The default offsets.retention.minutes is 10080 minutes (7 days).*


### Answer 60

60. B) max.partition.fetch.bytes

**Explanation:** 

*max.partition.fetch.bytes controls the maximum bytes returned per partition (default 1 MB).*


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