# Chapter 3: Kafka Producers - Writing Messages to Kafka - Solutions
**CCDAK Practice Test Solutions**

[Back to Test](../../chapter-tests/chapter-03-test.md) | [Main README](../../README.md)

---

## Answer Key

### 1. A, B, C
**Explanation:** The three mandatory properties when creating a KafkaProducer are bootstrap.servers, key.serializer, and value.serializer. client.id and acks are optional configuration parameters.

### 2. B) 1
**Explanation:** In Apache Kafka 2.x, the default value of acks is 1, meaning the producer waits for the leader replica to acknowledge. Note: Kafka 3.0 changed this default to acks=all.

### 3. B) StringSerializer
**Explanation:** When sending String keys and values, you should use StringSerializer for both key.serializer and value.serializer.

### 4. C) The message is sent to a random partition using round-robin
**Explanation:** Starting in Kafka 2.4, when using the default partitioner with a null key, messages are sent using sticky round-robin partitioning, which fills a batch for one partition before moving to the next.

### 5. B) producer.send(record)
**Explanation:** The send() method returns a Future and sends asynchronously. Using .get() makes it synchronous.

### 6. C) Producer does not wait for any acknowledgment
**Explanation:** With acks=0, the producer sends messages without waiting for any acknowledgment from the broker, achieving maximum throughput but no delivery guarantee.

### 7. B) Message is written to all in-sync replicas
**Explanation:** acks=all ensures the message is written to all in-sync replicas (ISR), providing the strongest durability guarantee.

### 8. B) linger.ms
**Explanation:** linger.ms controls how long the producer waits for additional messages before sending the current batch.

### 9. B) Sets memory for buffering messages waiting to be sent
**Explanation:** buffer.memory configures the total amount of memory the producer uses to buffer messages waiting to be sent to brokers.

### 10. A) snappy, gzip, lz4, zstd
**Explanation:** Kafka producers support snappy, gzip, lz4, and zstd compression types.

### 11. B) Memory in bytes used for each batch
**Explanation:** batch.size controls the amount of memory in bytes (not number of messages) allocated for each batch.

### 12. A) Number of batches sent before receiving responses
**Explanation:** max.in.flight.requests.per.connection controls how many message batches the producer can send without receiving responses.

### 13. B) Messages may be reordered
**Explanation:** If retries > 0 and max.in.flight.requests.per.connection > 1, message ordering within a partition may not be preserved if retries occur.

### 14. D) Both A and B
**Explanation:** You can guarantee message ordering either by setting max.in.flight.requests.per.connection=1 OR by enabling idempotence (enable.idempotence=true), which allows up to 5 in-flight requests while maintaining order.

### 15. B) Prevents message duplication
**Explanation:** The idempotent producer prevents duplicate messages by assigning sequence numbers to records and having brokers deduplicate based on these numbers.

### 16. D) batch.size > 1000
**Explanation:** When enable.idempotence=true, you must have max.in.flight.requests.per.connection <= 5, retries > 0, and acks=all. batch.size has no specific requirement.

### 17. B) Total time from record ready to send until broker responds or client gives up
**Explanation:** delivery.timeout.ms limits the time from when a record is ready for sending until either the broker responds or the client gives up (including retries).

### 18. B) Time to wait for reply from server for each request
**Explanation:** request.timeout.ms controls how long the producer waits for a reply from the server for each individual produce request.

### 19. D) Both A and C
**Explanation:** max.block.ms controls how long the producer blocks when calling send() if the buffer is full AND when explicitly requesting metadata via partitionsFor().

### 20. B) Set delivery.timeout.ms and leave retries at default
**Explanation:** Modern best practice is to set delivery.timeout.ms to the maximum time you want to wait (e.g., 2 minutes) and leave retries at the default (virtually infinite), allowing the producer to retry for the entire timeout period.

### 21. B) "Message size too large" error
**Explanation:** "Message size too large" is a non-retriable error. The producer will not retry this error because retrying won't fix the underlying issue.

### 22. B) Logical identifier for logging and metrics
**Explanation:** client.id is a logical identifier used in logging, metrics, and quotas to identify the client application.

### 23. C) Hash of the key
**Explanation:** The default partitioner uses a hash of the key (using Kafka's murmur2 algorithm) to determine which partition to send the message to.

### 24. B) Old records stay in original partitions, new records may go to different partitions
**Explanation:** When you add partitions, the key-to-partition mapping changes for new messages, but old messages remain in their original partitions. This breaks the guarantee that all messages with the same key go to the same partition.

### 25. C) To control which partition receives specific messages
**Explanation:** A custom partitioner allows you to implement custom logic for determining which partition should receive specific messages.

### 26. B) Partitioner
**Explanation:** A custom partitioner must implement the org.apache.kafka.clients.producer.Partitioner interface.

### 27. C) Apache Avro
**Explanation:** Apache Avro is the recommended serialization format because it provides schema evolution, compatibility checking, and efficient binary encoding.

### 28. C) Schema evolution and compatibility
**Explanation:** The main advantage of Avro is schema evolution - you can change schemas over time while maintaining compatibility between old and new versions.

### 29. C) In a Schema Registry
**Explanation:** When using Avro with Kafka, schemas are typically stored in a centralized Schema Registry rather than in each message.

### 30. C) Schema identifier
**Explanation:** When you store a schema in the Schema Registry, it returns a unique schema identifier (ID) that can be used to reference that schema.

### 31. B) Schema identifier
**Explanation:** Each Avro message sent to Kafka contains only the schema identifier (not the full schema), which the consumer uses to retrieve the schema from the Schema Registry.

### 32. A) Yes, if schemas are compatible
**Explanation:** Avro supports schema evolution, allowing consumers with a new schema to read messages written with an old compatible schema.

### 33. B) New consumers will get null for that field when reading old messages
**Explanation:** When a field is removed from the schema, consumers using the new schema will receive null for that field when reading old messages that contain it (assuming proper compatibility rules).

### 34. A) Store routing metadata without parsing message body
**Explanation:** Headers allow you to store metadata (like routing information, lineage, or tracing data) without needing to parse the message body, which may be encrypted or in an unknown format.

### 35. A) String
**Explanation:** Header keys are always Strings.

### 36. C) Any serialized object
**Explanation:** Header values can be any serialized object (stored as byte arrays), similar to message values.

### 37. B) Modify producer behavior without changing application code
**Explanation:** ProducerInterceptor allows you to modify producer behavior (like capturing metrics or adding headers) without changing the application code.

### 38. B) onSend()
**Explanation:** The onSend() method is called before a record is sent to Kafka (before serialization).

### 39. B) onAcknowledgement()
**Explanation:** The onAcknowledgement() method is called when the broker responds with an acknowledgment (success or failure).

### 40. B) In the producer's main thread
**Explanation:** ProducerInterceptor callbacks execute in the producer's main thread, which is why you should avoid blocking operations in callbacks.

### 41. C) Blocking operations
**Explanation:** You should avoid blocking operations in interceptor callbacks because they execute in the producer's main thread and would delay other messages from being sent.

### 42. A) Fire-and-forget, synchronous, asynchronous
**Explanation:** The three primary methods of sending messages are fire-and-forget (send and don't check), synchronous (send and wait with .get()), and asynchronous (send with callback).

### 43. B) producer.send(record).get()
**Explanation:** Calling .get() on the Future returned by send() makes the operation synchronous by blocking until the response is received.

### 44. B) Poor performance due to waiting
**Explanation:** The main disadvantage of synchronous send is poor performance because the sending thread blocks and waits for each message to be acknowledged before sending the next one.

### 45. B) Callback
**Explanation:** A callback class must implement the org.apache.kafka.clients.producer.Callback interface.

### 46. B) BufferExhaustedException
**Explanation:** BufferExhaustedException indicates that the producer buffer is full and send() cannot proceed.

### 47. B) Messages are queued in client memory
**Explanation:** When send() is called faster than messages can be delivered, they are queued in the producer's client-side memory buffer.

### 48. B) Rate limiting of produce/consume operations
**Explanation:** Kafka quotas are used to limit the rate at which clients can produce and consume data.

### 49. A) Produce, consume, request
**Explanation:** Kafka supports three types of quotas: produce quotas (bytes/sec sent), consume quotas (bytes/sec received), and request quotas (% of broker time).

### 50. B) Bytes per second
**Explanation:** Produce and consume quotas are measured in bytes per second.

### 51. C) Broker throttles the client requests
**Explanation:** When a client exceeds its quota, the broker throttles (delays) the client's requests to bring it back within the quota limits.

### 52. B) produce-throttle-time-avg
**Explanation:** The produce-throttle-time-avg and produce-throttle-time-max metrics indicate that throttling is occurring.

### 53. B) Sticky round-robin
**Explanation:** In Kafka 2.4+, the default partitioner uses sticky round-robin for null keys, filling one partition's batch before switching to another partition.

### 54. B) Lower latency and reduced CPU usage on broker
**Explanation:** Sticky partitioning reduces latency and CPU usage because messages can be sent in fewer, larger batches rather than many small batches across partitions.

### 55. A) Maximum message size and number of messages per request
**Explanation:** max.request.size controls both the maximum size of individual messages and the maximum number of messages that can be batched in one request.

### 56. A) max.request.size and message.max.bytes
**Explanation:** The producer's max.request.size should match the broker's message.max.bytes configuration to avoid sending messages that will be rejected.

### 57. B) When producers/consumers are in different datacenters
**Explanation:** You should increase send.buffer.bytes and receive.buffer.bytes when communicating across datacenters because those network links typically have higher latency and lower bandwidth.

### 58. B) Non-retriable error that occurs before sending
**Explanation:** SerializationException is a non-retriable error that occurs before the message is sent to Kafka (during the serialization phase).

### 59. D) Both B and C
**Explanation:** Both UniformStickyPartitioner and RoundRobinPartitioner can distribute workload evenly even when keys are present, ignoring the keys for partitioning purposes.

### 60. A) Store schemas centrally to avoid storing full schema in each message
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