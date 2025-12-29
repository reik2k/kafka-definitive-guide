# Chapter 4: Kafka Consumers - Reading Data from Kafka

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 4

**CCDAK Practice Test - 60 Questions**
**Time Limit: 90 minutes**  
**Passing Score: 70%**

[Back to Main README](../../README.md) | [Solutions](../chapter-tests-solutions/chapter-04-solutions.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

### Question 1

**What are the three mandatory properties when creating a KafkaConsumer?**

- A) bootstrap.servers, key.deserializer, value.deserializer
- B) bootstrap.servers, group.id, key.deserializer
- C) group.id, key.deserializer, value.deserializer
- D) bootstrap.servers, group.id, auto.offset.reset

### Question 2

**What happens when you add more consumers to a consumer group than there are partitions?**

- A) The extra consumers will share partitions with existing consumers
- B) The extra consumers will be idle and receive no messages
- C) An exception is thrown
- D) Partitions are automatically created

### Question 3

**If a topic has 4 partitions and a consumer group has 2 consumers, how many partitions will each consumer typically read from?**

- A) Each consumer reads from all 4 partitions
- B) Each consumer reads from 2 partitions
- C) One consumer reads 3 partitions, the other reads 1
- D) It's randomly distributed

### Question 4

**What is a rebalance?**

- A) Redistributing messages within a partition
- B) Reassigning partitions to consumers in a group
- C) Creating new partitions
- D) Compacting old messages

### Question 5

**What are the two types of rebalances?**

- A) Fast and slow
- B) Eager and cooperative
- C) Manual and automatic
- D) Sync and async

### Question 6

**What is the main difference between eager and cooperative rebalances?**

- A) Eager is faster
- B) Cooperative only reassigns a subset of partitions and allows continued consumption
- C) Eager is more reliable
- D) Cooperative requires manual intervention

### Question 7

**How do consumers maintain group membership?**

- A) By sending heartbeats to the group coordinator
- B) By polling continuously
- C) By committing offsets
- D) By subscribing to topics

### Question 8

**What happens if a consumer stops sending heartbeats?**

- A) Nothing, it continues consuming
- B) The group coordinator considers it dead and triggers a rebalance
- C) The consumer is permanently removed
- D) Messages are lost

### Question 9

**What is static group membership?**

- A) A group that never rebalances
- B) Consumers with unique group.instance.id that retain partitions across restarts
- C) A group with fixed number of consumers
- D) A deprecated feature

### Question 10

**What method is used to subscribe to topics?**

- A) consumer.subscribe()
- B) consumer.connect()
- C) consumer.join()
- D) consumer.attach()

### Question 11

**Can you subscribe to topics using a regular expression?**

- A) No, only explicit topic names
- B) Yes, for matching multiple topic names
- C) Only in newer versions
- D) Yes, but it's deprecated

### Question 12

**What is the poll loop?**

- A) A loop that checks consumer health
- B) The main loop where consumers continuously poll Kafka for data
- C) A configuration parameter
- D) A background thread

### Question 13

**What does consumer.poll(timeout) return?**

- A) A single ConsumerRecord
- B) A list of topics
- C) ConsumerRecords collection
- D) A Future object

### Question 14

**What happens if poll() is not called within max.poll.interval.ms?**

- A) Nothing
- B) Consumer is considered dead and evicted from the group
- C) Consumer automatically reconnects
- D) Messages are lost

### Question 15

**Can you safely use the same consumer from multiple threads?**

- A) Yes, consumers are thread-safe
- B) No, one consumer per thread is the rule
- C) Only for reading, not committing
- D) Yes, but with synchronization

### Question 16

**What does fetch.min.bytes control?**

- A) Minimum message size
- B) Minimum data broker sends before responding to consumer
- C) Minimum batch size
- D) Minimum buffer size

### Question 17

**What does fetch.max.wait.ms control?**

- A) Maximum time to wait for fetch.min.bytes of data
- B) Maximum time between polls
- C) Maximum time for heartbeats
- D) Maximum time for commits

### Question 18

**What is the default value of fetch.max.bytes?**

- A) 1 MB
- B) 10 MB
- C) 50 MB
- D) 100 MB

### Question 19

**What does max.poll.records control?**

- A) Maximum records per partition
- B) Maximum records returned by a single poll()
- C) Maximum records per topic
- D) Maximum records per consumer

### Question 20

**How are session.timeout.ms and heartbeat.interval.ms related?**

- A) They're independent
- B) heartbeat.interval.ms should be lower, typically 1/3 of session.timeout.ms
- C) They must be equal
- D) session.timeout.ms must be lower

### Question 21

**What is the default session.timeout.ms?**

- A) 1 second
- B) 3 seconds
- C) 10 seconds
- D) 30 seconds

### Question 22

**What does max.poll.interval.ms detect?**

- A) Network failures
- B) Deadlocked main thread while background thread sends heartbeats
- C) Broker failures
- D) Message corruption

### Question 23

**What does auto.offset.reset control?**

- A) How often offsets are reset
- B) Behavior when consumer starts with no valid offset
- C) Automatic offset commit interval
- D) Default offset value

### Question 24

**What are the valid values for auto.offset.reset?**

- A) latest, earliest, none
- B) beginning, end, error
- C) start, stop, reset
- D) auto, manual, default

### Question 25

**What does enable.auto.commit control?**

- A) Automatic topic subscription
- B) Whether consumer automatically commits offsets
- C) Automatic rebalancing
- D) Automatic deserialization

### Question 26

**What is the default auto.commit.interval.ms?**

- A) 1 second
- B) 5 seconds
- C) 10 seconds
- D) 30 seconds

### Question 27

**What are the available partition assignment strategies? (Select all that apply)**

- A) Range
- B) RoundRobin
- C) Sticky
- D) Random
- E) CooperativeSticky

### Question 28

**Which assignment strategy assigns consecutive partitions from each topic?**

- A) RoundRobin
- B) Range
- C) Sticky
- D) CooperativeSticky

### Question 29

**Which assignment strategy supports cooperative rebalancing?**

- A) Range
- B) RoundRobin
- C) Sticky
- D) CooperativeSticky

### Question 30

**What does client.rack configuration enable?**

- A) Physical rack identification
- B) Fetching from closest replica
- C) Rack-aware partitioning
- D) Disaster recovery

### Question 31

**What is an offset commit?**

- A) Writing messages to Kafka
- B) Updating current position in partition
- C) Subscribing to topics
- D) Rebalancing partitions

### Question 32

**Where are committed offsets stored?**

- A) In consumer memory
- B) In __consumer_offsets topic
- C) In ZooKeeper
- D) In each partition

### Question 33

**What happens if committed offset is smaller than last processed offset?**

- A) Messages are lost
- B) Messages are processed twice
- C) Consumer crashes
- D) Automatic correction occurs

### Question 34

**What happens if committed offset is larger than last processed offset?**

- A) Messages are duplicated
- B) Messages between offsets are missed
- C) Consumer rebalances
- D) Offsets are automatically corrected

### Question 35

**With enable.auto.commit=true, when are offsets committed?**

- A) After each message
- B) Every auto.commit.interval.ms during poll()
- C) On consumer close only
- D) Never

### Question 36

**What is the main drawback of automatic commits?**

- A) Performance overhead
- B) Cannot eliminate duplicate messages during rebalance
- C) Requires manual configuration
- D) Only works with new consumers

### Question 37

**What does commitSync() do?**

- A) Commits asynchronously
- B) Commits latest offset from poll() and blocks until complete
- C) Commits only on rebalance
- D) Commits specific offsets

### Question 38

**What happens if commitSync() fails?**

- A) It returns false
- B) It retries until success or unrecoverable error
- C) Consumer shuts down
- D) Offsets are lost

### Question 39

**What is the advantage of commitAsync() over commitSync()?**

- A) More reliable
- B) Better throughput, doesn't block
- C) Automatic retries
- D) Simpler to use

### Question 40

**Why doesn't commitAsync() automatically retry?**

- A) Performance reasons
- B) Later commits may have already succeeded, causing order issues
- C) It's not implemented
- D) Security concerns

### Question 41

**What pattern combines commitAsync() and commitSync()?**

- A) Use commitAsync() in loop, commitSync() before shutdown
- B) Always use both together
- C) Alternate between them
- D) Use commitSync() in loop, commitAsync() on shutdown

### Question 42

**Can you commit specific offsets instead of the latest?**

- A) No, only latest offset
- B) Yes, by passing a map of partitions and offsets
- C) Only with manual assignment
- D) Only in standalone mode

### Question 43

**What interface do you implement for rebalance notifications?**

- A) RebalanceHandler
- B) ConsumerRebalanceListener
- C) PartitionListener
- D) GroupListener

### Question 44

**When is onPartitionsRevoked() called?**

- A) When getting new partitions
- B) Before losing ownership of partitions
- C) After rebalance completes
- D) On consumer startup

### Question 45

**When is onPartitionsAssigned() called?**

- A) Before losing partitions
- B) After partitions are assigned but before consumption starts
- C) During rebalance
- D) On consumer close

### Question 46

**What is onPartitionsLost() used for?**

- A) Error handling
- B) Exceptional cases with cooperative rebalancing where partitions were reassigned without revocation
- C) Partition deletion
- D) Network failures

### Question 47

**What does seekToBeginning() do?**

- A) Resets all offsets
- B) Starts reading from beginning of specified partitions
- C) Deletes messages
- D) Rebalances consumer group

### Question 48

**What does seekToEnd() do?**

- A) Stops consuming
- B) Starts consuming only new messages from specified partitions
- C) Closes consumer
- D) Commits offsets

### Question 49

**How do you cleanly shut down a consumer?**

- A) Just stop the poll loop
- B) Call consumer.wakeup() from another thread, then consumer.close()
- C) Kill the process
- D) Call consumer.shutdown()

### Question 50

**What exception does wakeup() cause poll() to throw?**

- A) InterruptedException
- B) WakeupException
- C) ConsumerException
- D) ShutdownException

### Question 51

**Is consumer.wakeup() thread-safe?**

- A) No
- B) Yes, it's the only thread-safe consumer method
- C) Only with synchronization
- D) Only in new versions

### Question 52

**What must match between producer and consumer?**

- A) Configuration
- B) Serializer and deserializer for the data
- C) Thread count
- D) Poll timeout

### Question 53

**For custom objects, what's recommended instead of custom deserializers?**

- A) JSON only
- B) Standard formats like Avro, Thrift, or Protobuf
- C) Always use String
- D) Binary format

### Question 54

**When using KafkaAvroDeserializer, what additional configuration is needed?**

- A) avro.schema
- B) schema.registry.url
- C) avro.enabled
- D) serialization.format

### Question 55

**In standalone consumer mode, how do you assign partitions?**

- A) Use subscribe()
- B) Use assign() with specific partitions
- C) Use connect()
- D) Use join()

### Question 56

**Can a consumer both subscribe to topics and assign partitions?**

- A) Yes, both at the same time
- B) No, it's one or the other
- C) Only in standalone mode
- D) Only with configuration change

### Question 57

**What happens during the first poll() call?**

- A) Returns empty
- B) Finds GroupCoordinator, joins group, receives partition assignment
- C) Only connects to broker
- D) Throws exception

### Question 58

**What is the purpose of offsets.retention.minutes (broker config)?**

- A) How long messages are retained
- B) How long committed offsets are retained after group becomes empty
- C) Consumer timeout
- D) Rebalance timeout

### Question 59

**What is the default offsets.retention.minutes?**

- A) 1 day
- B) 7 days
- C) 30 days
- D) Forever

### Question 60

**What controls how many bytes per partition are returned in poll()?**

- A) fetch.max.bytes
- B) max.partition.fetch.bytes
- C) partition.fetch.size
- D) max.poll.bytes

---

## Scoring Guide
- 54-60 correct: Excellent understanding of Kafka Consumers
- 48-53 correct: Good understanding, review weak areas
- 42-47 correct: Moderate understanding, more study needed
- Below 42: Significant review required

---

[Back to Test](../../chapter-tests/chapter-04-test.md) | [Main README](../../README.md)