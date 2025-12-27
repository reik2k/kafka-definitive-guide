# Chapter 08 – Exactly-Once Semantics – Solutions
CCDAK Practice Test Solutions
**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 8

[Back to Test](../../chapter-tests/chapter-08-test.md) | [Main README](../../README.md)

---

### Answer  1

**Correct Answer: C**

**Explanation:**
Idempotent producers ensure that even if the client retries sends, the broker deduplicates them so each record is written only once to the log. This prevents duplicate records from appearing in the log due to network issues or producer retries.

---

### Answer  2

**Correct Answer: C**

**Explanation:**
When a transactional ID is configured, the client enables idempotence automatically. Modern Kafka clients do not require a separate `enable.idempotence` flag when using transactions.

---

### Answer  3

**Correct Answer: A**

**Explanation:**
Idempotent producers require:
- `acks=all`: Ensures all in-sync replicas acknowledge the write
- `retries > 0`: Allows the producer to retry on failures
- `max.in.flight.requests.per.connection <= 5`: Maintains ordering while allowing pipelining

---

### Answer  4

**Correct Answer: B**

**Explanation:**
The PID (Producer ID) uniquely identifies the producer instance so the broker can track sequence numbers per partition and drop duplicate records based on sequence number detection.

---

### Answer  5

**Correct Answer: C**

**Explanation:**
The transaction coordinator manages transaction state and writes metadata into an internal transaction log topic (`__transaction_state`). It tracks the status of all ongoing transactions.

---

### Answer  6

**Correct Answer: C**

**Explanation:**
The transactional ID ties a logical producer across restarts, enabling fencing of stale producers and associating transactions with that logical instance. This ensures only one producer with a given transactional ID can be active at a time.

---

### Answer  7

**Correct Answer: B**

**Explanation:**
For EOS (Exactly-Once Semantics), consumers typically use `read_committed` isolation level so they only see committed transactional records plus non-transactional ones, avoiding uncommitted or aborted records.

---

### Answer  8

**Correct Answer: B**

**Explanation:**
`read_committed` hides uncommitted and aborted transactional records, exposing only:
- Committed transactional messages
- Non-transactional messages

This ensures consumers only process finalized data.

---

### Answer  9

**Correct Answer: B**

**Explanation:**
EOS read-process-write requires transactions that include the input offsets and all output records so the entire operation is atomic. This ensures that processing is done exactly once even in the face of failures.

---

### Answer  10

**Correct Answer: B**

**Explanation:**
Kafka Streams wraps the input read, state updates, and output writes in a single Kafka transaction to achieve atomicity. All operations either succeed together or fail together.

---

### Answer  11

**Correct Answer: B**

**Explanation:**
`isolation.level=read_committed` ensures consumers do not see uncommitted or aborted transactional messages. This is the key configuration for consuming transactional data safely.

---

### Answer  12

**Correct Answer: B**

**Explanation:**
Aborted transactional records remain in the log physically but are never returned to `read_committed` consumers. The broker filters them out automatically.

---

### Answer  13

**Correct Answer: B**

**Explanation:**
EOS for producers uses the idempotent producer combined with transactions to guarantee atomic, duplicate-free writes. Both features work together to provide exactly-once semantics.

---

### Answer  14

**Correct Answer: B**

**Explanation:**
`initTransactions()` registers the transactional ID with the cluster, obtains a PID (Producer ID), and prepares the producer for transactional work. This must be called before any transaction can begin.

---

### Answer  15

**Correct Answer: B**

**Explanation:**
`beginTransaction()` marks the start of a new transaction. Subsequent sends and offset additions belong to that transaction until it is committed or aborted.

---

### Answer  16

**Correct Answer: C**

**Explanation:**
`sendOffsetsToTransaction()` adds consumed offsets to the ongoing transaction so they commit atomically with output records. This is essential for exactly-once processing in consumer-producer patterns.

---

### Answer  17

**Correct Answer: B**

**Explanation:**
Offsets and output records commit together, ensuring that if a failure occurs, either both are visible or neither, avoiding duplicates or data loss in the pipeline. This atomicity is the foundation of EOS.

---

### Answer  18

**Correct Answer: C**

**Explanation:**
After commit, transactional messages become visible to both:
- `read_committed` consumers (only after commit)
- `read_uncommitted` consumers (potentially before commit)

---

### Answer  19

**Correct Answer: C**

**Explanation:**
If the producer fails, the transaction coordinator may time out and abort the transaction, hiding those records from `read_committed` consumers, while `read_uncommitted` consumers can still see them.

---

### Answer  20

**Correct Answer: B**

**Explanation:**
Kafka's EOS only covers operations inside Kafka. External systems (databases, file systems, etc.) require special integration to extend EOS beyond Kafka, such as using two-phase commit protocols or application-level coordination.

---

### Answer  21

**Correct Answer: B**

**Explanation:**
Committing offsets before writes can cause data loss or duplicates on failure, so that pattern is unsafe for EOS. The correct pattern is to include both offset commits and output writes in the same transaction.

---

### Answer  22

**Correct Answer: B**

**Explanation:**
Idempotence prevents duplicate records at the broker level but does not coordinate with consumer offsets. Without transactions, end-to-end semantics still remain at-least-once.

---

### Answer  23

**Correct Answer: D**

**Explanation:**
Kafka Streams relies on changelog topics for state stores, which themselves are written transactionally when EOS is enabled. These changelog topics allow state stores to be reconstructed after failures.

---

### Answer  24

**Correct Answer: A**

**Explanation:**
Kafka Streams enables EOS using `processing.guarantee=exactly_once_v2` (or older `exactly_once_beta`), activating transactional producers and appropriate consumer behaviors.

---

### Answer  25

**Correct Answer: B**

**Explanation:**
- `at_least_once`: May emit duplicates after failures
- `exactly_once`: Guarantees no duplicates as observed within Kafka, even after failures

This is achieved through transactional coordination.

---

### Answer  26

**Correct Answer: B**

**Explanation:**
Transactions require:
- Additional coordinator traffic
- Metadata writes to transaction log
- Additional IO operations
- More complex coordination logic

All of these add overhead and may increase latency compared with at-least-once.

---

### Answer  27

**Correct Answer: C**

**Explanation:**
Transaction metadata is stored in an internal transaction state topic (`__transaction_state`) managed by the transaction coordinator. This topic is partitioned and replicated like any other Kafka topic.

---

### Answer  28

**Correct Answer: A**

**Explanation:**
If `max.in.flight.requests.per.connection` is too high (> 5), retries can reorder messages, breaking the assumptions required by idempotence and potentially causing duplicates. The value must be <= 5 for idempotent producers.

---

### Answer  29

**Correct Answer: C**

**Explanation:**
Sequence numbers are tracked per partition for each PID (Producer ID), enabling partition-level deduplication. Each (PID, partition) pair maintains its own sequence number.

---

### Answer  30

**Correct Answer: A**

**Explanation:**
`abortTransaction()` discards the in-flight transaction so `read_committed` consumers never see its records. The transaction coordinator marks the transaction as aborted in the log.

---

### Answer  31

**Correct Answer: A**

**Explanation:**
Using a stable transactional ID allows Kafka to reuse the same PID and enable fencing of older producers. This prevents zombie producers (old instances) from continuing to write after a new instance with the same ID has started.

---

### Answer  32

**Correct Answer: B**

**Explanation:**
Producer fencing ensures that once a new producer takes over a transactional ID, older producers with the same ID cannot continue to write and corrupt transactional guarantees. This is implemented through epoch numbers associated with PIDs.

---

### Answer  33

**Correct Answer: B**

**Explanation:**
A fenced producer receives fatal errors (e.g., `ProducerFencedException`) and its requests are rejected by the broker. The application must handle this by closing the producer and ensuring only one active instance.

---

### Answer  34

**Correct Answer: B**

**Explanation:**
With EOS enabled, partial outputs and offsets of an in-flight transaction are not visible to consumers. On task restart, the task reprocesses from the last committed offsets, ensuring exactly-once processing.

---

### Answer  35

**Correct Answer: A**

**Explanation:**
Kafka alone cannot guarantee EOS across external systems such as databases unless a coordinated transactional protocol (like two-phase commit or application-level idempotency) is implemented.

---

### Answer  36

**Correct Answer: B**

**Explanation:**
`read_committed` consumers buffer transactional records until the coordinator determines commit or abort status, then expose only committed ones. Uncommitted records are held back until their fate is known.

---

### Answer  37

**Correct Answer: B**

**Explanation:**
With `processing.guarantee=exactly_once_v2` and a valid `application.id`, Kafka Streams uses transactions and idempotence to provide EOS. The `application.id` is used as part of the transactional ID.

---

### Answer  38

**Correct Answer: B**

**Explanation:**
The canonical EOS pattern for manual consumer-producer applications:
1. `beginTransaction()`
2. `poll()` to consume records
3. Process the records
4. `send()` output records
5. `sendOffsetsToTransaction()` to include offsets
6. `commitTransaction()` to commit everything atomically

---

### Answer  39

**Correct Answer: B**

**Explanation:**
Without `sendOffsetsToTransaction()`, offsets and outputs are not atomically linked and can become inconsistent on failure. The offsets might be committed without the outputs, or vice versa.

---

### Answer  40

**Correct Answer: C**

**Explanation:**
`acks=all` ensures the leader waits for in-sync replicas before acknowledging, which is required by the idempotent producer for its guarantees. This ensures writes are durable before being considered successful.

---

### Answer  41

**Correct Answer: B**

**Explanation:**
Kafka's ordering and EOS guarantees are per partition, not across the entire topic or cluster. Messages within a single partition maintain their order.

---

### Answer  42

**Correct Answer: B**

**Explanation:**
Streams with EOS ensures that state store updates and outputs are committed atomically as part of each transaction. This prevents partial state updates from being visible.

---

### Answer  43

**Correct Answer: C**

**Explanation:**
Kafka Streams abstracts away manual transaction management and is the preferred API for EOS pipelines. It handles all the transaction coordination automatically.

---

### Answer  44

**Correct Answer: B**

**Explanation:**
Financial transaction processing and similar monetary operations are classic EOS use cases where duplicates are unacceptable. Banking, payments, and billing systems benefit greatly from EOS.

---

### Answer  45

**Correct Answer: B**

**Explanation:**
Enabling EOS introduces transactional overhead, which typically increases latency and resource usage compared with at-least-once. The tradeoff is stronger guarantees for higher cost.

---

### Answer  46

**Correct Answer: B**

**Explanation:**
The broker uses the tuple (PID, partition, sequence number) to detect and drop duplicate records. Each producer maintains separate sequence numbers for each partition it writes to.

---

### Answer  47

**Correct Answer: C**

**Explanation:**
`transactional.id` names the logical transactional producer instance, allowing it to maintain its identity across restarts and enabling producer fencing.

---

### Answer  48

**Correct Answer: C**

**Explanation:**
A `ProducerFencedException` is fatal. The application should close that producer and ensure only a single active instance uses that transactional ID. Often this means restarting with proper coordination.

---

### Answer  49

**Correct Answer: A**

**Explanation:**
Non-transactional producers can be part of custom EOS designs when combined with external transactional coordinators or application-level idempotency mechanisms, but Kafka alone does not guarantee EOS for them.

---

### Answer  50

**Correct Answer: A**

**Explanation:**
Transactions are built on top of idempotent producers. Idempotence is a foundation component that transactions leverage to provide the broader EOS guarantees.

---

### Answer  51

**Correct Answer: B**

**Explanation:**
With `exactly_once_v2`, Kafka Streams uses transactions and idempotent producers to guarantee EOS, coordinating reads, processing, state updates, and writes atomically.

---

### Answer  52

**Correct Answer: B**

**Explanation:**
Under EOS, Kafka Streams commits offsets as part of each transaction into the `__consumer_offsets` topic, ensuring atomicity with output records and state updates.

---

### Answer  53

**Correct Answer: A**

**Explanation:**
`transaction.timeout.ms` controls how long the coordinator waits before aborting an incomplete transaction. This prevents stuck transactions from blocking progress indefinitely.

---

### Answer  54

**Correct Answer: B**

**Explanation:**
An explicit `abortTransaction()` call by the producer, or a timeout by the transaction coordinator, leads to the transaction being marked as aborted.

---

### Answer  55

**Correct Answer: B**

**Explanation:**
`read_uncommitted` exposes all records including those from aborted and in-flight transactions, making it unsuitable for applications requiring EOS guarantees.

---

### Answer  56

**Correct Answer: C**

**Explanation:**
For at-least-once semantics, using manual `commitSync()` after processing is the straightforward pattern. This doesn't require transactions but may result in duplicates on failure.

---

### Answer  57

**Correct Answer: A**

**Explanation:**
State stores rely on changelog topics written transactionally, so intermediate state is not exposed inconsistently after failures. The changelog allows state reconstruction with exactly-once guarantees.

---

### Answer  58

**Correct Answer: B**

**Explanation:**
EOS ensures atomicity: either both offsets and output records are committed together, or neither is committed. This prevents inconsistencies after failures.

---

### Answer  59

**Correct Answer: A**

**Explanation:**
Batches in a transactional producer are associated with a single transaction. Records from different transactions are not mixed in the same batch.

---

### Answer  60

**Correct Answer: B**

**Explanation:**
A typical EOS microservice pattern uses:
- Transactional producer with a `transactional.id`
- Consumer with `isolation.level=read_committed`
- Offsets committed via `sendOffsetsToTransaction()`

This ensures end-to-end exactly-once processing.

---

## Summary

These 60 questions cover the essential concepts of exactly-once semantics in Apache Kafka:

### Key Topics Covered:
1. **Idempotent Producers**: PID, sequence numbers, deduplication
2. **Transactions**: Transactional ID, coordinators, commit/abort
3. **Consumer Integration**: `read_committed`, offset management
4. **Kafka Streams EOS**: `exactly_once_v2`, state stores, changelogs
5. **Producer Fencing**: Preventing zombie producers
6. **Configuration**: Required settings for idempotence and transactions
7. **Patterns**: Safe read-process-write patterns
8. **Limitations**: External systems, overhead considerations

### Best Practices for CCDAK:
- Understand the relationship between idempotence and transactions
- Know the required configurations for EOS
- Be familiar with transaction coordinator roles
- Understand the difference between `read_committed` and `read_uncommitted`
- Know when to use `sendOffsetsToTransaction()`
- Understand producer fencing mechanisms
- Be aware of EOS limitations with external systems

**Good luck with your CCDAK certification!**