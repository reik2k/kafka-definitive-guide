# Chapter 09 – Building Data Pipelines – Solutions and Explanations

CCDAK Practice Test Solutions
**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 9

[Back to Test](../../chapter-tests/chapter-09-test.md) | [Main README](../../README.md)

---

### Answer  1

**Correct Answer: B**

**Explanation:**
The chapter describes two main use cases: (1) Kafka as one of the two endpoints (e.g., getting data from Kafka to S3 or from MongoDB to Kafka), and (2) using Kafka as an intermediary between two systems (e.g., Twitter to Elasticsearch via Kafka).

---

### Answer  2

**Correct Answer: B**

**Explanation:**
Kafka's main value is its ability to serve as a very large, reliable buffer between various stages in the pipeline. This decouples producers and consumers, allowing different timeliness and availability requirements.

---

### Answer  3

**Correct Answer: B**

**Explanation:**
Kafka allows producers and consumers to have different timeliness and availability requirements. Kafka acts as a buffer, so producers can write in real-time while consumers process in batches, or vice versa.

---

### Answer  4

**Correct Answer: C**

**Explanation:**
Kafka provides at-least-once delivery guarantee on its own. Each event from the source will reach its destination, but retries may cause duplicates.

---

### Answer  5

**Correct Answer: B**

**Explanation:**
Kafka can achieve exactly-once delivery when combined with external data stores that have transactional models or unique keys. Kafka Connect makes this easier by providing APIs for integrating with external systems.

---

### Answer  6

**Correct Answer: B**

**Explanation:**
When producer throughput exceeds consumer throughput, data accumulates in Kafka until the consumer catches up. Kafka applies back pressure on producers by delaying acks when needed.

---

### Answer  7

**Correct Answer: C**

**Explanation:**
Kafka itself and the Connect API are completely agnostic to data formats. Producers and consumers can use any serializer, and Connect allows pluggable converters.

---

### Answer  8

**Correct Answer: B**

**Explanation:**
ETL stands for Extract-Transform-Load. The data pipeline is responsible for transforming data as it passes through.

---

### Answer  9

**Correct Answer: B**

**Explanation:**
The main drawback is that transformations in the pipeline may tie the hands of downstream users. If data is filtered or fields are removed, downstream applications have limited access to data.

---

### Answer  10

**Correct Answer: B**

**Explanation:**
ELT stands for Extract-Load-Transform. The data pipeline does minimal transformation, with the goal of making data at the target as similar as possible to the source, with transformations done at the target system.

