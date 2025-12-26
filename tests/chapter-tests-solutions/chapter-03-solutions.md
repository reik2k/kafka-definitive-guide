# Chapter 3: Kafka Producers - Writing Messages to Kafka - Solutions
**CCDAK Practice Test Solutions**

[Back to Test](../../chapter-tests/chapter-03-test.md) | [Main README](../../README.md)

---

## Answer Key

## **Question 1**
**Explanation:** The three mandatory properties when creating a KafkaProducer are bootstrap.servers, key.serializer, and value.serializer. client.id and acks are optional configuration parameters.

## **Question 2**
**Explanation:** In Apache Kafka 2.x, the default value of acks is 1, meaning the producer waits for the leader replica to acknowledge. Note: Kafka 3.0 changed this default to acks=all.

## **Question 3**
**Explanation:** When sending String keys and values, you should use StringSerializer for both key.serializer and value.serializer.

## **Question 4**
**Explanation:** Starting in Kafka 2.4, when using the default partitioner with a null key, messages are sent using sticky round-robin partitioning, which fills a batch for one partition before moving to the next.

## **Question 5**
**Explanation:** The send() method returns a Future and sends asynchronously. Using .get() makes it synchronous.

## **Question 6**
**Explanation:** With acks=0, the producer sends messages without waiting for any acknowledgment from the broker, achieving maximum throughput but no delivery guarantee.

## **Question 7**
**Explanation:** acks=all ensures the message is written to all in-sync replicas (ISR), providing the strongest durability guarantee.

## **Question 8**
**Explanation:** linger.ms controls how long the producer waits for additional messages before sending the current batch.

## **Question 9**
**Explanation:** buffer.memory configures the total amount of memory the producer uses to buffer messages waiting to be sent to brokers.

## **Question 10**
**Explanation:** Kafka producers support snappy, gzip, lz4, and zstd compression types.

## **Question 11**
**Explanation:** batch.size controls the amount of memory in bytes (not number of messages) allocated for each batch.

## **Question 12**
**Explanation:** max.in.flight.requests.per.connection controls how many message batches the producer can send without receiving responses.

## **Question 13**
**Explanation:** If retries > 0 and max.in.flight.requests.per.connection > 1, message ordering within a partition may not be preserved if retries occur.

## **Question 14**
**Explanation:** You can guarantee message ordering either by setting max.in.flight.requests.per.connection=1 OR by enabling idempotence (enable.idempotence=true), which allows up to 5 in-flight requests while maintaining order.

## **Question 15**
**Explanation:** The idempotent producer prevents duplicate messages by assigning sequence numbers to records and having brokers deduplicate based on these numbers.

## **Question 16**
**Explanation:** When enable.idempotence=true, you must have max.in.flight.requests.per.connection <= 5, retries > 0, and acks=all. batch.size has no specific requirement.

## **Question 17**
**Explanation:** delivery.timeout.ms limits the time from when a record is ready for sending until either the broker responds or the client gives up (including retries).

## **Question 18**
**Explanation:** request.timeout.ms controls how long the producer waits for a reply from the server for each individual produce request.

## **Question 19**
**Explanation:** max.block.ms controls how long the producer blocks when calling send() if the buffer is full AND when explicitly requesting metadata via partitionsFor().

## **Question 20**
**Explanation:** Modern best practice is to set delivery.timeout.ms to the maximum time you want to wait (e.g., 2 minutes) and leave retries at the default (virtually infinite), allowing the producer to retry for the entire timeout period.

## **Question 21**
**Explanation:** "Message size too large" is a non-retriable error. The producer will not retry this error because retrying won't fix the underlying issue.

## **Question 22**
**Explanation:** client.id is a logical identifier used in logging, metrics, and quotas to identify the client application.

## **Question 23**
**Explanation:** The default partitioner uses a hash of the key (using Kafka's murmur2 algorithm) to determine which partition to send the message to.

## **Question 24**
**Explanation:** When you add partitions, the key-to-partition mapping changes for new messages, but old messages remain in their original partitions. This breaks the guarantee that all messages with the same key go to the same partition.

## **Question 25**
**Explanation:** A custom partitioner allows you to implement custom logic for determining which partition should receive specific messages.

## **Question 26**
**Explanation:** A custom partitioner must implement the org.apache.kafka.clients.producer.Partitioner interface.

## **Question 27**
**Explanation:** Apache Avro is the recommended serialization format because it provides schema evolution, compatibility checking, and efficient binary encoding.

## **Question 28**
**Explanation:** The main advantage of Avro is schema evolution - you can change schemas over time while maintaining compatibility between old and new versions.

## **Question 29**
**Explanation:** When using Avro with Kafka, schemas are typically stored in a centralized Schema Registry rather than in each message.

## **Question 30**
**Explanation:** When you store a schema in the Schema Registry, it returns a unique schema identifier (ID) that can be used to reference that schema.

## **Question 31**
**Explanation:** Each Avro message sent to Kafka contains only the schema identifier (not the full schema), which the consumer uses to retrieve the schema from the Schema Registry.

## **Question 32**
**Explanation:** Avro supports schema evolution, allowing consumers with a new schema to read messages written with an old compatible schema.

## **Question 33**
**Explanation:** When a field is removed from the schema, consumers using the new schema will receive null for that field when reading old messages that contain it (assuming proper compatibility rules).

## **Question 34**
**Explanation:** Headers allow you to store metadata (like routing information, lineage, or tracing data) without needing to parse the message body, which may be encrypted or in an unknown format.

## **Question 35**
**Explanation:** Header keys are always Strings.

## **Question 36**
**Explanation:** Header values can be any serialized object (stored as byte arrays), similar to message values.

## **Question 37**
**Explanation:** ProducerInterceptor allows you to modify producer behavior (like capturing metrics or adding headers) without changing the application code.

## **Question 38**
**Explanation:** The onSend() method is called before a record is sent to Kafka (before serialization).

## **Question 39**
**Explanation:** The onAcknowledgement() method is called when the broker responds with an acknowledgment (success or failure).

## **Question 40**
**Explanation:** ProducerInterceptor callbacks execute in the producer's main thread, which is why you should avoid blocking operations in callbacks.

## **Question 41**
**Explanation:** You should avoid blocking operations in interceptor callbacks because they execute in the producer's main thread and would delay other messages from being sent.

## **Question 42**
**Explanation:** The three primary methods of sending messages are fire-and-forget (send and don't check), synchronous (send and wait with .get()), and asynchronous (send with callback).

## **Question 43**
**Explanation:** Calling .get() on the Future returned by send() makes the operation synchronous by blocking until the response is received.

## **Question 44**
**Explanation:** The main disadvantage of synchronous send is poor performance because the sending thread blocks and waits for each message to be acknowledged before sending the next one.

## **Question 45**
**Explanation:** A callback class must implement the org.apache.kafka.clients.producer.Callback interface.

## **Question 46**
**Explanation:** BufferExhaustedException indicates that the producer buffer is full and send() cannot proceed.

## **Question 47**
**Explanation:** When send() is called faster than messages can be delivered, they are queued in the producer's client-side memory buffer.

## **Question 48**
**Explanation:** Kafka quotas are used to limit the rate at which clients can produce and consume data.

## **Question 49**
**Explanation:** Kafka supports three types of quotas: produce quotas (bytes/sec sent), consume quotas (bytes/sec received), and request quotas (% of broker time).

## **Question 50**
**Explanation:** Produce and consume quotas are measured in bytes per second.

## **Question 51**
**Explanation:** When a client exceeds its quota, the broker throttles (delays) the client's requests to bring it back within the quota limits.

## **Question 52**
**Explanation:** The produce-throttle-time-avg and produce-throttle-time-max metrics indicate that throttling is occurring.

## **Question 53**
**Explanation:** In Kafka 2.4+, the default partitioner uses sticky round-robin for null keys, filling one partition's batch before switching to another partition.

## **Question 54**
**Explanation:** Sticky partitioning reduces latency and CPU usage because messages can be sent in fewer, larger batches rather than many small batches across partitions.

## **Question 55**
**Explanation:** max.request.size controls both the maximum size of individual messages and the maximum number of messages that can be batched in one request.

## **Question 56**
**Explanation:** The producer's max.request.size should match the broker's message.max.bytes configuration to avoid sending messages that will be rejected.

## **Question 57**
**Explanation:** You should increase send.buffer.bytes and receive.buffer.bytes when communicating across datacenters because those network links typically have higher latency and lower bandwidth.

## **Question 58**
**Explanation:** SerializationException is a non-retriable error that occurs before the message is sent to Kafka (during the serialization phase).

## **Question 59**
**Explanation:** Both UniformStickyPartitioner and RoundRobinPartitioner can distribute workload evenly even when keys are present, ignoring the keys for partitioning purposes.

## **Question 60**
**Explanation:** The Schema Registry stores schemas centrally, allowing messages to contain only a small schema ID instead of the full schema, significantly reducing message size.

---

## Study Tips

### Key Concepts to Master:
1. **Producer Configuration**: Bootstrap servers, serializers, acks levels, timeout settings
2. **Reliability Settings**: Idempotence, retries, delivery.timeout.ms, in-flight requests
3. **Partitioning**: Default partitioner behavior, custom partitioners, key-based routing
4. **Serialization**: Avro vs custom serializers, Schema Registry integration
5. **Performance Tuning**: Batching (batch.size, linger.ms), compression, buffering
6. **Advanced Features**: Headers, interceptors, callbacks
7. **Quotas**: Types (produce, consume, request), throttling behavior

### Related CCDAK Topics:
- Producer API usage patterns
- Error handling and retry strategies  
- Schema management with Schema Registry
- Performance optimization techniques
- Producer monitoring and metrics
- Idempotent and transactional producers

---

[Back to Test](../../chapter-tests/chapter-03-test.md) | [Main README](../../README.md)