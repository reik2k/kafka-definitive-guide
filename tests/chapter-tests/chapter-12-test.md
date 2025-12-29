# Chapter 12 - Administering Kafka - Test

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 12

**CCDAK Practice Test - 60 Questions**
**Time Limit: 90 minutes**  
**Passing Score: 70%**

[Link to Solutions](../../chapter-tests-solutions/chapter-12-solutions.md) | [Main README](../../README.md)

---

## Instructions
- This test follows the Confluent Certified Developer for Apache Kafka (CCDAK) exam format
- Each question has multiple choice answers
- Select the best answer for each question
- Some questions may have multiple correct answers

---

### Question 1

**Which command-line tool is used for creating, modifying, deleting, and listing topics in a Kafka cluster?**

- A) kafka-configs.sh
- B) kafka-topics.sh
- C) kafka-console-producer.sh
- D) kafka-consumer-groups.sh

### Question 2

**When creating a new topic with kafka-topics.sh, which THREE arguments are required?**

- A) --topic
- B) --replication-factor
- C) --partitions
- D) --config

### Question 3

**What is the recommended practice for topic naming in Kafka?**

- A) Use periods to separate components
- B) Start topic names with double underscores
- C) Avoid using periods in topic names
- D) Use only uppercase letters

### Question 4

**Which argument prevents an error from being returned when attempting to create a topic that already exists?**

- A) --skip-existing
- B) --if-not-exists
- C) --no-error
- D) --force

### Question 5

**What does the --under-replicated-partitions option show when describing topics?**

- A) Partitions that have no leader
- B) Partitions where one or more replicas are not in sync with the leader
- C) Partitions below minimum ISR
- D) Partitions with unavailable brokers

### Question 6

**Which option is used to show only topics that have configurations differing from cluster defaults?**

- A) --describe-config
- B) --topics-with-overrides
- C) --custom-config
- D) --non-default

### Question 7

**What happens when you attempt to reduce the number of partitions for a topic?**

- A) Partitions are deleted and data is redistributed
- B) It is not possible to reduce the number of partitions
- C) Only empty partitions can be removed
- D) Partitions are merged automatically

### Question 8

**What configuration must be set to true on brokers to allow topic deletion?**

- A) delete.topic.enable
- B) allow.topic.delete
- C) topic.deletion.enabled
- D) enable.delete.topics

### Question 9

**Why is it recommended not to delete more than one or two topics at a time?**

- A) To prevent network congestion
- B) Due to limitations in how the controller executes these operations
- C) To maintain ZooKeeper performance
- D) Because of consumer group limitations

### Question 10

**Which command is used to list consumer groups in a cluster?**

- A) kafka-consumer-groups.sh --list
- B) kafka-topics.sh --list-groups
- C) kafka-groups.sh --list
- D) kafka-configs.sh --list-consumers

### Question 11

**What field in the describe consumer group output shows the difference between consumer current offset and broker log-end offset?**

- A) OFFSET-DIFF
- B) LAG
- C) DELTA
- D) BACKLOG

### Question 12

**What must be true before you can delete a consumer group?**

- A) The group must have committed offsets
- B) All consumers in the group must be shut down
- C) The topic must be deleted first
- D) The group must be at least 1 hour old

### Question 13

**Which tool is used to dynamically modify topic, broker, client, and user configurations?**

- A) kafka-topics.sh
- B) kafka-admin.sh
- C) kafka-configs.sh
- D) kafka-settings.sh

### Question 14

**What is the format for changing a topic configuration dynamically?**

- A) kafka-configs.sh --alter --entity-type topics --entity-name <topic>
- B) kafka-topics.sh --config --topic <topic>
- C) kafka-admin.sh --modify --topic <topic>
- D) kafka-settings.sh --update --topic <topic>

### Question 15

**Which configuration key controls how long messages should be retained for a topic?**

- A) retention.time
- B) retention.ms
- C) message.retention
- D) log.retention.ms

### Question 16

**What quota configuration controls the amount of bytes a client can produce to a broker per second?**

- A) producer_bytes_rate
- B) produce.rate.limit
- C) client.produce.quota
- D) max.produce.bytes

### Question 17

**Why might throttling be unevenly enforced in poorly balanced clusters?**

- A) Network latency varies between brokers
- B) Throttling occurs on a per-broker basis
- C) ZooKeeper applies limits globally
- D) Producer clients cache throttle settings

### Question 18

**Which command-line tool is used to manually produce messages to a Kafka topic?**

- A) kafka-producer.sh
- B) kafka-send.sh
- C) kafka-console-producer.sh
- D) kafka-message-producer.sh

### Question 19

**What is the default separator between key and value when using the console producer?**

- A) Colon
- B) Comma
- C) Tab character
- D) Pipe

### Question 20

**What does the --from-beginning option do when consuming with kafka-console-consumer.sh?**

- A) Starts from the earliest offset
- B) Starts from the latest offset
- C) Starts from the first message produced today
- D) Starts from offset 0 only

### Question 21

**What internal topic stores consumer group offsets?**

- A) __consumer_state
- B) __consumer_offsets
- C) __group_metadata
- D) __offsets

### Question 22

**Which tool is used to trigger preferred replica election for partitions?**

- A) kafka-preferred-leader.sh
- B) kafka-leader-election.sh
- C) kafka-replica-election.sh
- D) kafka-partition-leader.sh

### Question 23

**What is the purpose of preferred replica election?**

- A) To select a new controller
- B) To balance leadership across brokers
- C) To increase replication factor
- D) To delete unused replicas

### Question 24

**Which tool is used to reassign partition replicas to different brokers?**

- A) kafka-partition-manager.sh
- B) kafka-reassign-partitions.sh
- C) kafka-replica-reassign.sh
- D) kafka-move-partitions.sh

### Question 25

**What are the steps involved in using kafka-reassign-partitions.sh?**

- A) Generate proposal, execute, verify
- B) Plan, apply, rollback
- C) Create, modify, confirm
- D) Analyze, execute, validate

### Question 26

**What option can be used to throttle partition reassignments to reduce cluster impact?**

- A) --rate-limit
- B) --throttle
- C) --bandwidth
- D) --slow-move

### Question 27

**How can you cancel an in-progress partition reassignment?**

- A) Delete the ZooKeeper znode manually
- B) Use --cancel option with kafka-reassign-partitions.sh
- C) Restart all brokers
- D) Use --abort with kafka-admin.sh

### Question 28

**What tool can be used to examine individual messages in a log segment?**

- A) kafka-message-reader.sh
- B) kafka-log-viewer.sh
- C) kafka-dump-log.sh
- D) kafka-segment-analyzer.sh

### Question 29

**Which option with kafka-dump-log.sh prints the actual message payload?**

- A) --show-data
- B) --print-data-log
- C) --display-payload
- D) --full-message

### Question 30

**What tool verifies that replicas for a topic's partitions are identical across the cluster?**

- A) kafka-replica-checker.sh
- B) kafka-replica-verification.sh
- C) kafka-verify-replicas.sh
- D) kafka-consistency-check.sh

### Question 31

**What is the primary risk when running replica verification?**

- A) It may corrupt data
- B) It has significant cluster impact similar to reassigning partitions
- C) It requires stopping all producers
- D) It permanently modifies offsets

### Question 32

**Where does the controller election information reside in ZooKeeper?**

- A) /admin/controller
- B) /controller/leader
- C) /brokers/controller
- D) /cluster/controller

### Question 33

**What happens when the /admin/controller znode is manually deleted?**

- A) The cluster shuts down
- B) The controller resigns and a new one is elected
- C) All brokers restart
- D) Topics are deleted

### Question 34

**Which configuration allows unclean leader elections for a topic?**

- A) unclean.leader.election.allow
- B) unclean.leader.election.enable
- C) allow.unclean.elections
- D) enable.unclean.leader

### Question 35

**What must be done before manually deleting a topic from ZooKeeper?**

- A) Stop all consumers
- B) Shut down all brokers in the cluster
- C) Delete all messages first
- D) Notify the controller

### Question 36

**What option is used with the console consumer to consume from a specific partition?**

- A) --partition
- B) --topic-partition
- C) --from-partition
- D) --partition-id

### Question 37

**Which message formatter prints only message checksums?**

- A) kafka.tools.ChecksumFormatter
- B) kafka.tools.ChecksumMessageFormatter
- C) kafka.tools.HashFormatter
- D) kafka.tools.DigestFormatter

### Question 38

**What is the recommended way to add partitions to a keyed topic?**

- A) Add partitions freely
- B) Set partition count once when created and avoid resizing
- C) Add partitions only in multiples of the current count
- D) Redistribute keys before adding partitions

### Question 39

**What does the --at-min-isr-partitions option show?**

- A) Partitions with no ISRs
- B) Partitions where ISR count exactly matches minimum ISR setting
- C) Partitions below minimum ISR
- D) Partitions with only one replica

### Question 40

**What format does the offset export produce when using --reset-offsets with --dry-run?**

- A) JSON format
- B) XML format
- C) CSV format
- D) Binary format

### Question 41

**What must consumers do before importing offsets?**

- A) Commit current offsets
- B) Stop consuming
- C) Reset their configuration
- D) Clear local cache

### Question 42

**Which configuration option specifies the minimum number of replicas that must be in sync for a partition?**

- A) min.replica.count
- B) min.insync.replicas
- C) replica.min.isr
- D) minimum.isr

### Question 43

**What is the purpose of the --additional option with kafka-reassign-partitions.sh?**

- A) Add more brokers to the cluster
- B) Add to existing reassignments without interruption
- C) Add more partitions to topics
- D) Add additional replication factor

### Question 44

**How can you use kafka-reassign-partitions.sh to change replication factor?**

- A) Use --change-replication-factor option
- B) Manually craft JSON with different replica count
- C) Use --increase-rf option
- D) It's not possible with this tool

### Question 45

**What is the safest way to remove leadership from a broker before decommissioning?**

- A) Stop the broker
- B) Delete partitions manually
- C) Use preferred replica election
- D) Restart the broker

### Question 46

**What does the --unavailable-partitions option show?**

- A) Partitions with no replicas
- B) Partitions below minimum ISR
- C) Partitions without a leader
- D) Partitions on offline brokers

### Question 47

**Which tool is deprecated in favor of kafka-leader-election.sh?**

- A) kafka-partition-election.sh
- B) kafka-preferred-replica-election.sh
- C) kafka-replica-leader.sh
- D) kafka-elect-leader.sh

### Question 48

**What property can be configured to control the compression type for a topic?**

- A) topic.compression
- B) compression.type
- C) message.compression
- D) log.compression.codec

### Question 49

**When using kafka-consumer-groups.sh --describe, what does the CLIENT-ID field represent?**

- A) The consumer group name
- B) String provided by the client identifying itself
- C) The broker ID the consumer is connected to
- D) The partition assignment identifier

### Question 50

**What happens during partition reassignment when new replicas are added?**

- A) Old replicas are immediately removed
- B) Replication factor temporarily increases while data is copied
- C) The partition becomes unavailable
- D) Messages are redistributed equally

### Question 51

**What option allows configuration changes for clients to be specified as a file?**

- A) --config-file
- B) --add-config-file
- C) --from-file
- D) --load-config

### Question 52

**What does the cleanup.policy configuration control for a topic?**

- A) How often to run log compaction
- B) Whether messages are deleted or compacted
- C) When to delete old segments
- D) The compression algorithm used

### Question 53

**Which command shows the ZooKeeper path for topic metadata?**

- A) /topics/<topic-name>
- B) /brokers/topics/<topic-name>
- C) /metadata/topics/<topic-name>
- D) /cluster/topics/<topic-name>

### Question 54

**What is the default message formatter for the console consumer?**

- A) kafka.tools.DefaultFormatter
- B) kafka.tools.DefaultMessageFormatter
- C) kafka.tools.StandardFormatter
- D) kafka.tools.BasicFormatter

### Question 55

**When does topic deletion actually occur after being marked for deletion?**

- A) Immediately
- B) After all producers stop
- C) Asynchronously when the controller notifies brokers
- D) After 24 hours

### Question 56

**What configuration determines how frequently log segments are rotated for a topic?**

- A) segment.interval
- B) segment.ms
- C) log.segment.interval
- D) rotation.ms

### Question 57

**Which option with the console producer sends messages synchronously?**

- A) --sync
- B) --synchronous
- C) --blocking
- D) --wait

### Question 58

**What does the controller_mutations_rate quota control?**

- A) The number of topic operations per second
- B) The rate of create/delete topics and create partition requests
- C) The rate of configuration changes
- D) The rate of leader elections

### Question 59

**What is the purpose of the --disable-rack-aware option with kafka-reassign-partitions.sh?**

- A) To ignore rack-aware placement constraints
- B) To disable rack monitoring
- C) To move partitions within the same rack
- D) To prioritize speed over redundancy

### Question 60

**Which field in describe topic output shows which broker is the partition leader?**

- A) LEADER-ID
- B) Leader
- C) BROKER
- D) PARTITION-LEADER