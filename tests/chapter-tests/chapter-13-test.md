# Chapter 13 - Monitoring Kafka - Test

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 13

**CCDAK Practice Test - 60 Questions**
**Time Limit: 90 minutes**  
**Passing Score: 70%**

[Link to Solutions](../../chapter-tests-solutions/chapter-13-solutions.md) | [Main README](../../README.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

### Question 1

**What interface do Kafka brokers use to expose metrics?**

- A) REST API
- B) Java Management Extensions (JMX)
- C) gRPC
- D) HTTP endpoints

### Question 2

**What is a Service-Level Indicator (SLI)?**

- A) A contract between service provider and client
- B) A metric that describes one aspect of service reliability
- C) A target value for a metric
- D) An agreement between internal services

### Question 3

**What is a Service-Level Objective (SLO)?**

- A) A metric combined with a target value and time frame
- B) A contract with penalties for non-performance
- C) An operational agreement between teams
- D) A single measurement of availability

### Question 4

**Which of the following is typically NOT a good choice for an SLI?**

- A) Availability measurements
- B) Latency percentiles
- C) Quantile metrics
- D) Counter of events within thresholds

### Question 5

**What is the primary metric to monitor for cluster health that indicates replication issues?**

- A) Partition count
- B) Under-replicated partitions
- C) Leader count
- D) Offline partitions

### Question 6

**What does the active controller count metric indicate?**

- A) Number of controllers in the cluster
- B) Whether the broker is currently the controller (0 or 1)
- C) How many partitions the controller manages
- D) The controller's uptime

### Question 7

**What should the active controller count be across the entire cluster?**

- A) Equal to the number of brokers
- B) Always exactly 1
- C) At least 2 for high availability
- D) 0 during normal operations

### Question 8

**What does the request handler idle ratio metric measure?**

- A) Percentage of time request handlers are idle
- B) Number of idle threads
- C) Average request processing time
- D) Network thread utilization

### Question 9

**What idle ratio percentage typically indicates a performance problem?**

- A) Below 50%
- B) Below 20%
- C) Below 80%
- D) Below 5%

### Question 10

**Which metric shows the rate at which producers are sending data to the broker?**

- A) All topics messages out
- B) All topics bytes in
- C) All topics fetch rate
- D) All topics produce rate

### Question 11

**What does the under-replicated partitions metric measure?**

- A) Total number of partitions in the cluster
- B) Number of partitions where one or more replicas are not in sync
- C) Number of partitions with offline replicas
- D) Average replication factor

### Question 12

**Which metric indicates that a broker is having trouble keeping up with the leader?**

- A) Messages in per second
- B) Fetch follower max lag
- C) Network processor average idle
- D) Request queue size

### Question 13

**What is the recommended approach for monitoring Kafka cluster health?**

- A) Monitor only broker JMX metrics
- B) Monitor only client-side metrics
- C) Combine broker, client, and end-to-end monitoring
- D) Rely solely on log file analysis

### Question 14

**What does the partition count metric for a topic indicate?**

- A) Number of messages in the topic
- B) Number of partitions allocated to the topic
- C) Number of consumers subscribed to the topic
- D) Replication factor of the topic

### Question 15

**Which metric shows the percentage of time the network thread pool is busy?**

- A) Network processor average idle
- B) Request handler average idle
- C) Network processor utilization
- D) Thread pool saturation

### Question 16

**What does the log flush rate and time metric measure?**

- A) Frequency and duration of flushing log segments to disk
- B) Rate of producing messages to logs
- C) Speed of log compaction
- D) Time to replicate logs across brokers

### Question 17

**Which metric should you monitor to detect broker failures?**

- A) Messages in per second
- B) Under-replicated partitions
- C) Consumer lag
- D) Log size

### Question 18

**What is consumer lag in Kafka?**

- A) Time taken to process a message
- B) Difference between last produced offset and last committed offset
- C) Network latency between consumer and broker
- D) Time between poll() calls

### Question 19

**Which tool can be used to monitor consumer group lag from the command line?**

- A) kafka-console-consumer
- B) kafka-consumer-groups
- C) kafka-topics
- D) kafka-configs

### Question 20

**What does the fetch request purgatory size metric indicate?**

- A) Number of fetch requests waiting to be completed
- B) Size of messages being fetched
- C) Number of consumers connected
- D) Rate of fetch requests per second

### Question 21

**What does the produce request purgatory size metric track?**

- A) Number of produce requests delayed until replication completes
- B) Size of messages being produced
- C) Number of producers connected
- D) Rate of produce requests per second

### Question 22

**Which metric indicates the total number of leader elections per second?**

- A) Leader election rate
- B) Unclean leader election rate
- C) Controller election rate
- D) Partition reassignment rate

### Question 23

**What is an unclean leader election?**

- A) Election of a leader from in-sync replicas
- B) Election of a leader that is not in the ISR, potentially causing data loss
- C) Election triggered by broker restart
- D) Election during controlled shutdown

### Question 24

**Which metric shows the number of messages produced per second to a broker?**

- A) Messages in per second
- B) Bytes in per second
- C) Produce requests per second
- D) Records produced rate

### Question 25

**What does the bytes out per second metric measure?**

- A) Data sent from broker to consumers
- B) Data received by broker from producers
- C) Replication traffic between brokers
- D) Network overhead

### Question 26

**Which metric is useful for monitoring the performance of log compaction?**

- A) Log cleaner recopy percent
- B) Log flush rate
- C) Log segment count
- D) Log end offset

### Question 27

**What does the ISR (In-Sync Replica) shrink rate metric indicate?**

- A) Rate at which replicas fall out of sync
- B) Rate of partition reassignments
- C) Rate of broker failures
- D) Rate of topic deletions

### Question 28

**Which metric should you monitor to identify slow consumers?**

- A) Consumer lag
- B) Fetch request rate
- C) Poll interval
- D) Heartbeat rate

### Question 29

**What is the purpose of monitoring the request queue size metric?**

- A) To identify broker overload and request backlog
- B) To count total requests processed
- C) To measure request size
- D) To track failed requests

### Question 30

**Which metric indicates the time spent waiting for sufficient replicas before completing a produce request?**

- A) Produce request remote time
- B) Produce request response time
- C) Replication lag
- D) ISR expansion rate

### Question 31

**What does the total time metric for produce requests measure?**

- A) Time from request received to response sent
- B) Only network transmission time
- C) Only disk write time
- D) Only replication time

### Question 32

**Which JMX port is commonly used to expose Kafka broker metrics?**

- A) 9092
- B) 2181
- C) 9999
- D) 8080

### Question 33

**What is the purpose of monitoring the partition size metric?**

- A) To track disk usage and plan capacity
- B) To count number of messages
- C) To measure replication factor
- D) To monitor consumer throughput

### Question 34

**Which metric indicates the number of offline partitions in the cluster?**

- A) Offline partitions count
- B) Under-replicated partitions
- C) ISR shrink rate
- D) Inactive partition count

### Question 35

**What does the ZooKeeper session expiration metric indicate?**

- A) Broker disconnecting from ZooKeeper coordination service
- B) Consumer group rebalancing
- C) Topic deletion
- D) Partition reassignment

### Question 36

**Which metric helps identify network performance issues?**

- A) Network processor average idle percent
- B) CPU usage
- C) Memory utilization
- D) Disk IOPS

### Question 37

**What does the records consumed rate metric measure on the consumer side?**

- A) Number of records consumed per second
- B) Size of records in bytes
- C) Consumer lag
- D) Fetch latency

### Question 38

**Which metric indicates the rate of failed produce requests?**

- A) Error rate
- B) Failed fetch request per second
- C) Timeout count
- D) Rejected requests

### Question 39

**What is the purpose of monitoring the log directory offline count?**

- A) To detect failed disk or corrupted log directories
- B) To count deleted topics
- C) To measure log compaction speed
- D) To track partition count

### Question 40

**Which consumer metric should you monitor to ensure the consumer is actively polling?**

- A) Poll idle ratio
- B) Fetch rate
- C) Records consumed
- D) Lag

### Question 41

**What does the fetch latency average metric measure?**

- A) Average time taken to complete fetch requests
- B) Network round-trip time
- C) Disk read time only
- D) Consumer processing time

### Question 42

**Which metric indicates producer batching effectiveness?**

- A) Record send rate and batch size average
- B) Request rate
- C) Compression ratio
- D) Buffer available bytes

### Question 43

**What is the purpose of the preferred replica election metric?**

- A) To track leadership rebalancing across brokers
- B) To count total replicas
- C) To measure replication lag
- D) To monitor consumer rebalancing

### Question 44

**Which metric shows the amount of memory used for buffering messages?**

- A) Buffer total bytes and buffer available bytes
- B) Heap memory usage
- C) Page cache utilization
- D) Network buffer size

### Question 45

**What does the records lag max metric indicate?**

- A) Maximum lag across all partitions assigned to a consumer
- B) Average lag
- C) Total number of unconsumed messages
- D) Time since last poll

### Question 46

**Which tool is commonly used for collecting and visualizing Kafka metrics?**

- A) Prometheus and Grafana
- B) Apache Spark
- C) Kafka Streams
- D) Apache Flink

### Question 47

**What does the connection close rate metric indicate?**

- A) Rate at which connections are being closed
- B) Number of active connections
- C) Connection timeout rate
- D) Maximum connections allowed

### Question 48

**Which metric helps identify if the cluster has sufficient disk space?**

- A) Log size and disk usage per broker
- B) Message count
- C) Partition count
- D) Replication factor

### Question 49

**What is the purpose of monitoring the controller queue size?**

- A) To detect delays in processing controller events
- B) To count total brokers
- C) To measure topic creation rate
- D) To track consumer groups

### Question 50

**Which producer metric indicates blocking due to buffer exhaustion?**

- A) Buffer exhausted rate
- B) Send rate
- C) Request latency
- D) Batch size average

### Question 51

**What does the heartbeat response time max metric measure for consumers?**

- A) Maximum time taken to respond to heartbeat requests
- B) Average heartbeat interval
- C) Number of heartbeats sent
- D) Session timeout duration

### Question 52

**Which metric indicates the effectiveness of message compression?**

- A) Compression ratio
- B) Batch size
- C) Request size
- D) Network throughput

### Question 53

**What is the purpose of the replica manager partition count metric?**

- A) To track the number of partitions managed by the broker
- B) To count consumer groups
- C) To measure replication lag
- D) To monitor topic count

### Question 54

**Which metric should you monitor to detect consumer group rebalancing?**

- A) Rebalance latency and rebalance rate
- B) Fetch rate
- C) Commit rate
- D) Poll rate

### Question 55

**What does the request size average metric indicate?**

- A) Average size of requests in bytes
- B) Number of requests per second
- C) Request processing time
- D) Queue depth

### Question 56

**What does the end-to-end latency metric measure in Kafka monitoring?**

- A) Time from message production to consumption
- B) Network latency only
- C) Broker processing time
- D) Consumer processing time

### Question 57

**Which metric helps identify if brokers are properly balanced?**

- A) Partition count per broker and bytes in/out per broker
- B) Topic count
- C) Consumer group count
- D) Replication factor

### Question 58

**What is the purpose of monitoring the commit latency metric for consumers?**

- A) To track time taken to commit offsets to Kafka
- B) To measure message processing time
- C) To monitor fetch latency
- D) To track rebalance duration

### Question 59

**Which metric indicates the rate at which ISR expands?**

- A) ISR expansion rate
- B) Replication rate
- C) Leader election rate
- D) Partition creation rate

### Question 60

**What does the replica lag time max metric measure?**

- A) Maximum time a follower replica is behind the leader
- B) Average lag across all replicas
- C) Number of out-of-sync replicas
- D) Replication throughput