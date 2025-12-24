# Chapter 3: Kafka Producers - Writing Messages to Kafka
**CCDAK Practice Test - 60 Questions**

[Back to Main README](../../README.md) | [Solutions](../chapter-tests-solutions/chapter-03-solutions.md)

---

## Instructions
- This test covers Chapter 3: Kafka Producers from the Kafka Definitive Guide
- Answer all 60 questions
- Each question has only one correct answer unless otherwise specified
- Solutions are available in the solutions folder

---

### 1. Which of the following are mandatory properties when creating a KafkaProducer? (Select all that apply)
A) bootstrap.servers
B) key.serializer
C) value.serializer
D) client.id
E) acks

### 2. What is the default value of the 'acks' parameter in Apache Kafka 2.x?
A) 0
B) 1
C) all
D) -1

### 3. Which serializer should you use when sending String keys and values?
A) ByteArraySerializer
B) StringSerializer
C) IntegerSerializer
D) AvroSerializer

### 4. What happens when you send a ProducerRecord with a null key using the default partitioner?
A) An exception is thrown
B) The message is rejected by the broker
C) The message is sent to a random partition using round-robin
D) The message is always sent to partition 0

### 5. Which method sends messages to Kafka asynchronously?
A) producer.send(record).get()
B) producer.send(record)
C) producer.sendAsync(record)
D) producer.publish(record)

### 6. What does acks=0 mean?
A) Producer waits for leader acknowledgment
B) Producer waits for all in-sync replicas
C) Producer does not wait for any acknowledgment
D) Producer waits for majority of replicas

### 7. What does acks=all guarantee?
A) Message is written to leader only
B) Message is written to all in-sync replicas
C) Message is written to all replicas
D) Message is written to majority of replicas

### 8. Which configuration controls how long the producer will wait for additional messages before sending the current batch?
A) batch.size
B) linger.ms
C) buffer.memory
D) max.block.ms

### 9. What is the purpose of the buffer.memory configuration?
A) Sets the batch size
B) Sets memory for buffering messages waiting to be sent
C) Sets memory for receiving responses
D) Sets memory for serialization

### 10. Which compression types are supported by Kafka producers?
A) snappy, gzip, lz4, zstd
B) snappy, gzip, zip, tar
C) gzip, bzip2, lz4, zstd
D) snappy, deflate, lz4, zstd

### 11. What does batch.size control?
A) Number of messages per batch
B) Memory in bytes used for each batch
C) Time to wait before sending a batch
D) Number of batches per partition

### 12. What does max.in.flight.requests.per.connection control?
A) Number of batches sent before receiving responses
B) Maximum number of connections
C) Maximum number of partitions
D) Maximum number of topics

### 13. If retries > 0 and max.in.flight.requests.per.connection > 1, what can happen?
A) Messages may be duplicated
B) Messages may be reordered
C) Messages may be lost
D) Producer will crash

### 14. How can you guarantee message ordering with retries enabled?
A) Set max.in.flight.requests.per.connection=1
B) Set enable.idempotence=true
C) Set acks=0
D) Both A and B

### 15. What does enable.idempotence=true do?
A) Prevents message loss
B) Prevents message duplication
C) Improves throughput
D) Reduces latency

### 16. Which configuration is NOT required when enable.idempotence=true?
A) max.in.flight.requests.per.connection <= 5
B) retries > 0
C) acks=all
D) batch.size > 1000

### 17. What is the purpose of delivery.timeout.ms?
A) Timeout for network requests
B) Total time from record ready to send until broker responds or client gives up
C) Timeout for serialization
D) Timeout for partitioning

### 18. What is the purpose of request.timeout.ms?
A) Total delivery timeout
B) Time to wait for reply from server for each request
C) Time to wait for batch to fill
D) Time to wait for buffer space

### 19. What does max.block.ms control?
A) Time producer blocks when calling send() if buffer is full
B) Time to wait for acknowledgment
C) Time to wait for metadata
D) Both A and C

### 20. What is the recommended approach for configuring retries in modern Kafka?
A) Set retries to a specific number
B) Set delivery.timeout.ms and leave retries at default
C) Disable retries completely
D) Set retry.backoff.ms to a high value

### 21. Which error type will NOT be retried by the producer?
A) Connection error
B) "Message size too large" error
C) "Not leader for partition" error
D) Timeout error

### 22. What is the purpose of client.id?
A) Unique identifier for authentication
B) Logical identifier for logging and metrics
C) Partition key
D) Consumer group identifier

### 23. When using the default partitioner with a key, how is the partition determined?
A) Random selection
B) Round-robin
C) Hash of the key
D) Sequential assignment

### 24. What happens if you add partitions to a topic when using key-based partitioning?
A) All keys are automatically remapped
B) Old records stay in original partitions, new records may go to different partitions
C) All data is rebalanced
D) The producer throws an exception

### 25. What is the purpose of a custom partitioner?
A) To encrypt data
B) To compress data
C) To control which partition receives specific messages
D) To serialize data

### 26. Which interface must a custom partitioner implement?
A) Serializer
B) Partitioner
C) Producer
D) Interceptor

### 27. What is the recommended serialization format for Kafka producers?
A) Custom serializers
B) JSON
C) Apache Avro
D) XML

### 28. What is the main advantage of using Apache Avro over custom serializers?
A) Faster serialization
B) Smaller message size
C) Schema evolution and compatibility
D) Easier implementation

### 29. Where is the Avro schema typically stored when using Kafka?
A) In each message
B) In the producer configuration
C) In a Schema Registry
D) In ZooKeeper

### 30. What does the Schema Registry return when you store a schema?
A) Schema name
B) Schema version
C) Schema identifier
D) Schema content

### 31. What is stored in each Avro message sent to Kafka?
A) Complete schema
B) Schema identifier
C) Schema version
D) Schema name

### 32. Can you read Avro messages written with an old schema using a new compatible schema?
A) Yes, if schemas are compatible
B) No, schemas must match exactly
C) Only if you reprocess all data
D) Only with special deserializers

### 33. What happens when a field is removed from an Avro schema?
A) Old messages cannot be read
B) New consumers will get null for that field when reading old messages
C) An exception is thrown
D) The field is automatically migrated

### 34. What is the purpose of ProducerRecord headers?
A) Store routing metadata without parsing message body
B) Compress the message
C) Encrypt the message
D) Partition the message

### 35. What type are header keys in ProducerRecord?
A) String
B) byte[]
C) Integer
D) Object

### 36. What type are header values in ProducerRecord?
A) String only
B) byte[] only
C) Any serialized object
D) Integer only

### 37. What is the purpose of ProducerInterceptor?
A) Encrypt messages
B) Modify producer behavior without changing application code
C) Improve performance
D) Handle errors

### 38. Which method is called before a record is sent to Kafka?
A) onAcknowledgement()
B) onSend()
C) beforeSend()
D) interceptSend()

### 39. Which method is called when Kafka responds with an acknowledgment?
A) onComplete()
B) onAcknowledgement()
C) afterSend()
D) onResponse()

### 40. Where do ProducerInterceptor callbacks execute?
A) In a separate thread
B) In the producer's main thread
C) In the broker thread
D) In a thread pool

### 41. What should you avoid doing in a ProducerInterceptor callback?
A) Logging
B) Counting messages
C) Blocking operations
D) Accessing metadata

### 42. What are the three primary methods of sending messages?
A) Fire-and-forget, synchronous, asynchronous
B) Fast, slow, retry
C) Direct, indirect, cached
D) Batch, single, stream

### 43. How do you send a message synchronously?
A) producer.send(record)
B) producer.send(record).get()
C) producer.sendSync(record)
D) producer.send(record).await()

### 44. What is the main disadvantage of synchronous send?
A) Higher error rate
B) Poor performance due to waiting
C) More complex code
D) Requires more memory

### 45. What interface must a callback class implement?
A) ProducerCallback
B) Callback
C) SendCallback
D) ResponseCallback

### 46. Which exception indicates the producer buffer is full?
A) BufferFullException
B) BufferExhaustedException
C) OutOfMemoryException
D) TimeoutException

### 47. What happens when send() is called faster than messages can be delivered?
A) Messages are dropped
B) Messages are queued in client memory
C) An exception is thrown immediately
D) Producer automatically throttles

### 48. What are Kafka quotas used for?
A) Partition assignment
B) Rate limiting of produce/consume operations
C) Topic creation limits
D) Consumer group limits

### 49. What types of quotas does Kafka support?
A) Produce, consume, request
B) Read, write, delete
C) Network, disk, CPU
D) Topic, partition, message

### 50. How are produce and consume quotas measured?
A) Messages per second
B) Bytes per second
C) Requests per second
D) Batches per second

### 51. What happens when a client exceeds its quota?
A) Messages are rejected
B) Client is disconnected
C) Broker throttles the client requests
D) Producer crashes

### 52. Which metrics indicate throttling is occurring?
A) send-rate
B) produce-throttle-time-avg
C) batch-size-avg
D) compression-rate

### 53. What is the recommended default partitioner behavior for null keys in Kafka 2.4+?
A) Random
B) Sticky round-robin
C) Sequential
D) Hash-based

### 54. What is the benefit of sticky partitioning for null keys?
A) Better message ordering
B) Lower latency and reduced CPU usage on broker
C) Higher throughput for keyed messages
D) Automatic rebalancing

### 55. What does max.request.size control?
A) Maximum message size and number of messages per request
B) Maximum batch size
C) Maximum buffer size
D) Maximum number of partitions

### 56. What should match between producer and broker configurations?
A) max.request.size and message.max.bytes
B) batch.size and buffer.memory
C) linger.ms and request.timeout.ms
D) acks and replication.factor

### 57. When should you increase send.buffer.bytes and receive.buffer.bytes?
A) When using compression
B) When producers/consumers are in different datacenters
C) When using Avro serialization
D) When using transactions

### 58. What type of error is SerializationException?
A) Retriable error
B) Non-retriable error that occurs before sending
C) Broker error
D) Network error

### 59. Which partitioner can be used to evenly distribute workload even when keys are present?
A) DefaultPartitioner
B) UniformStickyPartitioner
C) RoundRobinPartitioner
D) Both B and C

### 60. What is the purpose of using a Schema Registry with Avro?
A) Store schemas centrally to avoid storing full schema in each message
B) Validate messages before sending
C) Compress schemas
D) Encrypt schemas

---

## Scoring Guide
- 54-60 correct: Excellent understanding of Kafka Producers
- 48-53 correct: Good understanding, review weak areas
- 42-47 correct: Moderate understanding, more study needed
- Below 42: Significant review required

---

[Back to Test](../../chapter-tests/chapter-03-test.md) | [Main README](../../README.md)