# Chapter 08 – Exactly-Once Semantics – CCDAK Practice Test

> **60 Questions** | Related to Apache Kafka Exactly-Once Semantics (EOS), Idempotent Producers, and Transactions

---

## Question 1
Which guarantee does the idempotent producer add beyond the standard at-least-once delivery?

- A. Messages are delivered in random order but without duplicates
- B. Messages are delivered exactly once to consumers without any duplicates in topics
- C. The broker deduplicates retried records so each record is written to the log only once
- D. Consumers automatically commit offsets in a transaction

---

## Question 2
Which configuration enables the idempotent producer in modern Kafka clients?

- A. `enable.idempotent=true`
- B. `enable.idempotence=true`
- C. `enable.idempotence` is enabled automatically when using transactional APIs
- D. `acks=all`

---

## Question 3
Which three conditions are required for the idempotent producer to function correctly?

- A. `acks=all`, `retries > 0`, `max.in.flight.requests.per.connection <= 5`
- B. `acks=1`, `retries=0`, `enable.auto.commit=false`
- C. `acks=all`, `retries=0`, `max.in.flight.requests.per.connection > 5`
- D. `acks=0`, `retries > 0`, `max.in.flight.requests.per.connection <= 1`

---

## Question 4
What is the main purpose of a Producer ID (PID) in Kafka?

- A. To identify partitions uniquely
- B. To identify a producer instance to enable deduplication of records
- C. To identify consumer groups
- D. To identify transactional coordinators

---

## Question 5
Which component is responsible for maintaining the state of a transaction in Kafka?

- A. Group coordinator
- B. Controller broker
- C. Transaction coordinator
- D. Log cleaner

---

## Question 6
What is the role of a transactional ID in a Kafka application?

- A. It identifies a consumer group
- B. It identifies a set of partitions that the producer writes to
- C. It identifies a logical producer instance participating in transactions across restarts
- D. It identifies the schema used by the producer

---

## Question 7
In an exactly-once processing pipeline using Kafka Streams, which isolation level do consuming applications typically rely on?

- A. `read_uncommitted`
- B. `read_committed`
- C. `read_committed` only for compacted topics
- D. `read_uncommitted` for transactional topics

---

## Question 8
What does the `read_committed` isolation level guarantee for consumers?

- A. Consumers can see both committed and uncommitted transactional messages
- B. Consumers see only committed records from successful transactions and non-transactional records
- C. Consumers see only non-transactional records
- D. Consumers can read only from internal topics

---

## Question 9
Which of the following is required to achieve end-to-end exactly-once semantics with Kafka Streams in a read-process-write topology?

- A. Idempotent producers only
- B. Transactions spanning input reads, processing, and output writes
- C. At-most-once offset commits
- D. Disabling consumer groups

---

## Question 10
Which of the following best describes the phrase "read-process-write as a single atomic operation" in Kafka Streams?

- A. The input read, state update, and output write occur in the same thread
- B. The input read, state update, and output write are performed within a single Kafka transaction
- C. The input read and output write share the same partition key
- D. The input read and output write are always synchronous

---

## Question 11
Which configuration is essential for a Kafka consumer to avoid seeing uncommitted transactional messages?

- A. `enable.auto.commit=false`
- B. `isolation.level=read_committed`
- C. `auto.offset.reset=latest`
- D. `fetch.min.bytes` set to a positive value

---

## Question 12
What happens to messages in an aborted transaction when a consumer uses `read_committed`?

- A. They are delivered but marked as aborted
- B. They are skipped and never returned to the consumer
- C. They are redelivered in a later batch
- D. They are compacted immediately

---

## Question 13
Which Kafka feature is required to provide exactly-once semantics for a transactional producer?

- A. Log compaction
- B. Idempotent producer and transactions
- C. Rack awareness
- D. Quotas

---

## Question 14
In a transactional application, what is the purpose of `initTransactions()` in the producer?

- A. It starts the transaction and sends the first message
- B. It registers the transactional ID and obtains a PID from the transaction coordinator
- C. It commits the transaction
- D. It resets producer metrics

---

## Question 15
What is the purpose of calling `beginTransaction()` on a Kafka producer?

- A. To register the producer with the broker
- B. To start a new transaction scope for subsequent send operations
- C. To commit offsets
- D. To flush any pending messages

---

## Question 16
Which method must be used to include consumer offsets within a transaction?

- A. `commitSync()`
- B. `commitAsync()`
- C. `sendOffsetsToTransaction()`
- D. `flush()`

---

## Question 17
What is the main benefit of including offsets in the same transaction as output records?

- A. It reduces network overhead
- B. It provides atomicity between output data and offset commits
- C. It speeds up compaction
- D. It reduces disk usage on brokers

---

## Question 18
When a transaction is committed, what happens to the records written as part of that transaction?

- A. They are visible only to the producer
- B. They become visible to `read_uncommitted` consumers only
- C. They become visible to both `read_committed` and `read_uncommitted` consumers
- D. They remain invisible until the topic is compacted

---

## Question 19
What happens if a producer fails after writing records but before committing the transaction?

- A. The records are immediately visible to all consumers
- B. The transaction is automatically committed
- C. The transaction may eventually be aborted by the transaction coordinator, hiding those records from `read_committed` consumers
- D. The records are deleted from the log

---

## Question 20
Which of the following is a limitation of exactly-once semantics in Kafka?

- A. It only works for compacted topics
- B. It does not cover external systems outside Kafka unless they are integrated transactionally
- C. It only works when there is a single broker
- D. It requires disabling replication

---

## Question 21
In an application reading from Kafka, processing, then writing back to Kafka, which pattern is unsafe for exactly-once semantics?

- A. Read, process, write, then commit offsets transactionally
- B. Read, process, commit offsets, then write output
- C. Use Kafka Streams with EOS enabled
- D. Use `sendOffsetsToTransaction()`

---

## Question 22
What is the impact of setting `enable.idempotence=true` without using transactions?

- A. You get end-to-end exactly-once semantics automatically
- B. You get producer-side deduplication, but consumer offset handling can still be at-least-once
- C. Consumers will switch to `read_committed` automatically
- D. Transactions are enabled implicitly

---

## Question 23
Which internal topic is used by Kafka Streams to support EOS and state management?

- A. `__consumer_offsets`
- B. `__transaction_state`
- C. `__consumer_transactions`
- D. Changelog topics for state stores

---

## Question 24
In Kafka Streams, which configuration enables exactly-once semantics?

- A. `processing.guarantee=exactly_once_v2` (or `exactly_once_beta` in older versions)
- B. `enable.idempotence=true`
- C. `isolation.level=read_committed`
- D. `enable.eos=true`

---

## Question 25
What is the main difference between `at_least_once` and `exactly_once` processing guarantees in Kafka Streams?

- A. `at_least_once` requires transactions; `exactly_once` does not
- B. `at_least_once` may produce duplicates on failures; `exactly_once` avoids duplicates even after failures
- C. `exactly_once` is always faster than `at_least_once`
- D. `at_least_once` is only for stateless processing

---

## Question 26
Why might exactly-once processing have higher overhead than at-least-once?

- A. Requires more replication
- B. Requires transactional coordination, additional IO, and more metadata
- C. Requires larger partitions
- D. Requires additional ZooKeeper nodes

---

## Question 27
In Kafka, where are transactional metadata and status stored?

- A. In ZooKeeper
- B. In the controller's memory only
- C. In an internal topic managed by the transaction coordinator
- D. In the file system of producers

---

## Question 28
What is a typical symptom if `max.in.flight.requests.per.connection` is set too high with idempotent producers?

- A. Increased throughput but also possible reordering and duplicates
- B. Reduced throughput but guaranteed ordering
- C. Complete loss of messages
- D. Transactions cannot be started

---

## Question 29
Which of the following is true about idempotent producers and partitions?

- A. The producer sequence numbers are tracked per topic
- B. The producer sequence numbers are tracked per producer only
- C. The producer sequence numbers are tracked per partition
- D. The producer sequence numbers are tracked per consumer group

---

## Question 30
In a transactional producer, what is the effect of `abortTransaction()`?

- A. It rolls back the current transaction, making all messages invisible to `read_committed` consumers
- B. It commits the current transaction
- C. It closes the producer
- D. It deletes the topic

---

## Question 31
Why is it recommended to use a stable transactional ID across restarts of the same application instance?

- A. To reuse the same PID and allow fencing of older producers
- B. To enable log compaction
- C. To reduce replication latency
- D. To avoid schema evolution issues

---

## Question 32
What is producer fencing in Kafka?

- A. Preventing producers from writing to unauthorized topics
- B. Preventing an older producer instance with the same transactional ID from continuing to write after a newer instance starts
- C. Preventing consumers from reading internal topics
- D. Preventing producers from writing to compacted topics

---

## Question 33
Which behavior occurs when an older fenced producer attempts to continue using a transactional ID?

- A. Its writes are accepted but flagged
- B. The broker drops its requests and raises errors
- C. The broker merges its PID with the new producer
- D. The transaction is committed automatically

---

## Question 34
In a Kafka Streams application with EOS, what happens if a task crashes in the middle of processing a batch?

- A. Partial output may be visible
- B. No output or offset commits from the failed transaction become visible; the task is restarted and reprocesses from the last committed position
- C. All in-flight records are lost permanently
- D. The topology stops permanently

---

## Question 35
Which of the following guarantees does Kafka NOT provide, even with EOS?

- A. Exactly-once processing across Kafka and an external database without special integration
- B. Exactly-once processing within Kafka Streams
- C. Exactly-once processing for a transactional producer writing to Kafka
- D. Exactly-once visibility for `read_committed` consumers within Kafka

---

## Question 36
When using `read_committed`, how does a consumer treat records from ongoing (uncommitted) transactions?

- A. They are returned but marked as pending
- B. They are buffered but not returned until commit or abort is known
- C. They are permanently skipped
- D. They are returned immediately as normal records

---

## Question 37
Which configuration is necessary for Kafka Streams to use transactions under the `exactly_once` guarantee?

- A. `processing.guarantee=at_least_once`
- B. `processing.guarantee=exactly_once_v2` and a valid `application.id`
- C. `enable.auto.commit=true`
- D. `auto.offset.reset=earliest`

---

## Question 38
In a manual producer–consumer application (not Kafka Streams), which sequence ensures EOS between reading from one topic and writing to another?

- A. `poll()`, process, `send()`, then `commitSync()`
- B. `beginTransaction()`, `poll()`, process, `send()` outputs, `sendOffsetsToTransaction()`, `commitTransaction()`
- C. `poll()`, process, `commitAsync()`, `send()` outputs
- D. `poll()`, `beginTransaction()`, `commitTransaction()`, `send()` outputs

---

## Question 39
What happens if `sendOffsetsToTransaction()` is not called in a transactional application?

- A. Offsets are still committed atomically
- B. Offsets and outputs may become inconsistent in case of failures
- C. Consumers cannot read from the input topic
- D. Transactions cannot be committed

---

## Question 40
Why is it important that `acks=all` is used with idempotent producers?

- A. To ensure low latency
- B. To ensure the leader broker alone acknowledges writes
- C. To ensure that writes are replicated and acknowledged fully before being considered successful
- D. To enable log compaction

---

## Question 41
Which guarantee does Kafka's EOS rely on to preserve ordering?

- A. Global ordering across all partitions
- B. Ordering within a partition
- C. Ordering within a topic across brokers
- D. Ordering within a consumer group

---

## Question 42
A CCDAK-style scenario describes a microservice that consumes from topic A, updates a state store, and produces to topic B using Kafka Streams EOS. Which statement is correct?

- A. Duplicates may still occur on topic B
- B. The state store and outputs are updated atomically per transaction
- C. Offsets are not committed
- D. Consumers must use `read_uncommitted`

---

## Question 43
Which API is most convenient for implementing EOS without manually managing transactions?

- A. The plain Java consumer API
- B. The AdminClient API
- C. Kafka Streams API
- D. The older high-level consumer API

---

## Question 44
In the context of CCDAK, which use case is a typical motivation for exactly-once semantics?

- A. Logging debug events
- B. Financial transaction processing
- C. Sending marketing emails
- D. Caching static content

---

## Question 45
What is a potential downside of enabling EOS in Kafka Streams?

- A. State stores are no longer supported
- B. Higher latency and overhead due to transactional commits
- C. Producers cannot be idempotent
- D. Replication is disabled

---

## Question 46
How does Kafka deduplicate messages from an idempotent producer at the broker?

- A. By checking the message key only
- B. By using a combination of PID, partition, and sequence number
- C. By hashing the message value
- D. By comparing timestamps

---

## Question 47
Which of the following best describes "transactional.id" configuration on a producer?

- A. Identifies the cluster
- B. Identifies the topic
- C. Identifies the logical transactional producer instance
- D. Identifies the consumer group

---

## Question 48
What is the recommended action if a transactional producer receives a fatal error like `ProducerFencedException`?

- A. Ignore and continue sending messages
- B. Retry the same transaction with the same producer
- C. Close the producer and create a new one with a new transactional ID or ensure only one instance uses that ID
- D. Restart brokers

---

## Question 49
Which of the following is true about non-transactional producers and EOS?

- A. They can still be exactly-once when combined with external coordination
- B. They automatically provide EOS for reads and writes in Kafka Streams
- C. They cannot participate in EOS at all
- D. They are only at-most-once

---

## Question 50
For CCDAK, which of the following best characterizes the relationship between idempotence and transactions?

- A. Transactions depend on idempotence; idempotence is a building block for EOS
- B. Idempotence depends on transactions
- C. They are unrelated features
- D. Transactions disable idempotence

---

## Question 51
What is the effect of setting `processing.guarantee=exactly_once_v2` compared to `at_least_once` in Kafka Streams?

- A. Offsets are committed more frequently
- B. Streams uses transactions and idempotent producers to guarantee EOS
- C. Streams disables changelog topics
- D. Streams performs stateless processing only

---

## Question 52
In Kafka Streams EOS, how are offsets committed?

- A. Through `commitSync()` on the underlying consumer
- B. As part of the transaction to the `__consumer_offsets` topic
- C. Using ZooKeeper ephemeral nodes
- D. They are not committed

---

## Question 53
What does the transaction coordinator use to time out long-running or stuck transactions?

- A. `transaction.timeout.ms`
- B. `session.timeout.ms`
- C. `request.timeout.ms`
- D. `linger.ms`

---

## Question 54
Which of the following actions can cause a transaction to be aborted?

- A. Producer calling `flush()`
- B. Producer calling `abortTransaction()`
- C. Consumer calling `commitSync()`
- D. AdminClient deleting a topic

---

## Question 55
What is true about consuming from a transactional topic with `isolation.level=read_uncommitted`?

- A. The consumer will only see committed transactions
- B. The consumer may see records from aborted or in-flight transactions
- C. The consumer will see no records
- D. The consumer will fail with an error

---

## Question 56
If an application requires at-least-once semantics only, what is the simplest approach for committing offsets?

- A. Use `read_committed` and transactions
- B. Use `enable.auto.commit=true` and idempotent producer
- C. Use manual `commitSync()` after processing
- D. Do not commit offsets at all

---

## Question 57
In a CCDAK exam question describing a join of two topics with Streams EOS, which property ensures that intermediate state is not corrupted on failures?

- A. State stores backed by transactional changelog topics
- B. Using `auto.offset.reset=earliest`
- C. Using compacted topics only
- D. Using `acks=0`

---

## Question 58
What does EOS guarantee when a failure occurs after output records are written but before offsets are committed in a transactional application?

- A. Records remain visible but offsets are lost
- B. Either both offsets and records are committed or neither is committed
- C. Offsets are committed but records are lost
- D. Records are duplicated

---

## Question 59
For producers using transactions, which statement about batching is correct?

- A. All records in a producer batch must belong to the same transaction
- B. A single batch can contain records from different transactions but is tagged accordingly
- C. Batching is disabled in transactional producers
- D. Batching is only allowed for compacted topics

---

## Question 60
Which of the following describes a correct high-level pattern for an EOS-enabled microservice using the plain Java API?

- A. Non-transactional producer, auto-commit consumer
- B. Transactional producer with `transactional.id`, consumer with `read_committed`, and offsets sent via `sendOffsetsToTransaction()`
- C. Idempotent producer only, consumer with `read_uncommitted`
- D. At-most-once producer and consumer

---

## End of Test

**Total Questions:** 60

**Good luck with your CCDAK preparation!**