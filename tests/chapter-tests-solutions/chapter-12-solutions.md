# Chapter 12 - Administering Kafka - Solutions and Explanations

## Question 1
**Correct Answer: B++**

**Explanation:**
kafka-topics.sh is the primary command-line tool for managing topics in a Kafka cluster. It provides options to create (--create), modify (--alter), delete (--delete), and list (--list) topics. This tool also supports describing topic details (--describe) to show partition information, replica assignments, and ISR status.

----

## Question 2
**Correct Answer: A, B, C++**

**Explanation:**
When creating a new topic, three arguments are required: --topic (the topic name), --replication-factor (number of replicas), and --partitions (number of partitions). The --config option is optional and used for setting topic-specific configuration overrides beyond cluster defaults.

----

## Question 3
**Correct Answer: C++**

**Explanation:**
It's recommended to avoid using periods in topic names because Kafka's internal metrics convert periods to underscores. For example, "topic.1" becomes "topic_1" in metrics, which can cause naming conflicts. Also, avoid starting topic names with double underscores, as Kafka reserves this convention for internal topics like __consumer_offsets.

----

## Question 4
**Correct Answer: B++**

**Explanation:**
The --if-not-exists argument prevents the command from returning an error if the topic already exists. This is useful in automation scripts where you want to create a topic but don't want the script to fail if someone else already created it. The --if-exists argument for --alter is not recommended as it silently succeeds even if the topic doesn't exist, potentially masking errors.

----

## Question 5
**Correct Answer: B++**

**Explanation:**
The --under-replicated-partitions option displays partitions where one or more replicas are not in sync with the leader. This is useful during maintenance or when diagnosing cluster issues. While some under-replication is normal during deployments or rebalancing, persistent under-replicated partitions indicate problems that need attention.

----

## Question 6
**Correct Answer: B++**

**Explanation:**
The --topics-with-overrides option filters the output to show only topics that have custom configurations different from the cluster defaults. This helps administrators identify topics with special settings like custom retention policies, compression types, or replication requirements.

----

## Question 7
**Correct Answer: B++**

**Explanation:**
It is not possible to reduce the number of partitions for a topic in Kafka. Deleting partitions would cause data loss and create inconsistencies. If you need fewer partitions, the recommended approach is to create a new topic with the desired partition count and migrate traffic to it, or delete the topic entirely and recreate it.

----

## Question 8
**Correct Answer: A++**

**Explanation:**
The delete.topic.enable configuration must be set to true on brokers to allow topic deletion. If set to false, deletion requests are ignored. This is a safety feature to prevent accidental topic deletion in production environments.

----

## Question 9
**Correct Answer: B++**

**Explanation:**
Topic deletion should be done one or two at a time due to limitations in how the controller executes deletion operations. In small clusters, deletion happens quickly, but in large clusters with many partitions, it can take longer. Attempting to delete many topics simultaneously can overwhelm the controller.

----

## Question 10
**Correct Answer: A++**

**Explanation:**
kafka-consumer-groups.sh --list displays all consumer groups in the cluster. Ad hoc consumers (like those created with kafka-console-consumer.sh) appear with names like "console-consumer-" followed by a random number.

----

## Question 11
**Correct Answer: B++**

**Explanation:**
The LAG field shows the difference between the consumer's CURRENT-OFFSET (next offset to consume) and the broker's LOG-END-OFFSET (high-water mark). A high lag value indicates the consumer is falling behind in processing messages. This metric is crucial for monitoring consumer performance and health.

----

## Question 12
**Correct Answer: B++**

**Explanation:**
Before deleting a consumer group, all consumers in that group must be shut down. If you attempt to delete a group with active members, an error "The group is not empty" will be thrown. This ensures that active consumers aren't disrupted and their offsets aren't lost unexpectedly.

----

## Question 13
**Correct Answer: C++**

**Explanation:**
kafka-configs.sh is the tool for dynamically modifying configurations for topics, brokers, clients, and users at runtime without requiring restarts. It supports four entity types: topics, brokers, users, and clients. This tool allows operations like --alter, --describe, and --delete-config.

----

## Question 14
**Correct Answer: A++**

**Explanation:**
The format for dynamically changing topic configuration is: kafka-configs.sh --alter --entity-type topics --entity-name <topic> --add-config key=value. This allows you to override cluster-level defaults for individual topics, such as retention policies or compression settings.

----

## Question 15
**Correct Answer: B++**

**Explanation:**
The retention.ms configuration key controls how long messages are retained in a topic, specified in milliseconds. For example, setting retention.ms=3600000 retains messages for 1 hour. This is a critical configuration for managing storage and data lifecycle in Kafka.

----

## Question 16
**Correct Answer: A++**

**Explanation:**
The producer_bytes_rate quota configuration controls the amount of bytes a client can produce to a single broker per second. Quotas are enforced on a per-broker basis, so the total throughput depends on partition distribution and leadership balance across brokers.

----

## Question 17
**Correct Answer: B++**

**Explanation:**
Throttling is enforced on a per-broker basis, making cluster balance critical. In a 5-broker cluster with a 10 MBps producer quota, a client could theoretically produce 50 MBps total if leadership is balanced. However, if all partition leadership is on one broker, that same client is limited to 10 MBps total.

----

## Question 18
**Correct Answer: C++**

**Explanation:**
kafka-console-producer.sh is the command-line tool for manually producing messages to Kafka topics. It reads messages from standard input (one per line by default) and supports various options like --property for configuration, key/value separation with tabs, and batch settings.

----

## Question 19
**Correct Answer: C++**

**Explanation:**
By default, the console producer uses a tab character to separate the message key from the value. If no tab is present, the key is set to null. This can be customized using the key.separator property in the LineMessageReader configuration.

----

## Question 20
**Correct Answer: A++**

**Explanation:**
The --from-beginning option makes the console consumer start consuming from the earliest available offset in the topic. Without this option, consumption begins from the latest offset, meaning only new messages produced after the consumer starts will be displayed.

----

## Question 21
**Correct Answer: B++**

**Explanation:**
The __consumer_offsets topic is an internal Kafka topic that stores consumer group offset commits. All consumer group offset information is written as messages to this topic. You can consume from it using the special formatter kafka.coordinator.group.GroupMetadataManager$OffsetsMessageFormatter to decode the offset commit messages.

----

## Question 22
**Correct Answer: B++**

**Explanation:**
kafka-leader-election.sh is the tool for triggering preferred replica election. It replaced the older kafka-preferred-replica-election.sh tool and provides more flexibility with options like --election-type (PREFERRED or UNCLEAN) and the ability to specify partitions via JSON file or command-line options.

----

## Question 23
**Correct Answer: B++**

**Explanation:**
Preferred replica election rebalances partition leadership across brokers by selecting the ideal leader (first in-sync replica in the replica list). This ensures even distribution of load after broker restarts or failures. Leadership doesn't automatically return to the preferred replica after recovery, so this operation is necessary for maintaining balance.

----

## Question 24
**Correct Answer: B++**

**Explanation:**
kafka-reassign-partitions.sh is the tool for manually reassigning partition replicas to different brokers. This multi-step tool generates reassignment proposals, executes the moves, and verifies completion. It's useful for rebalancing clusters, adjusting replication factors, or decommissioning brokers.

----

## Question 25
**Correct Answer: A++**

**Explanation:**
The three-step process is: 1) Generate a proposal using --generate with a JSON file listing topics and target brokers, 2) Execute the reassignment using --execute with the proposal JSON, and 3) Verify progress and completion using --verify with the same JSON. This process ensures safe partition migration.

----

## Question 26
**Correct Answer: B++**

**Explanation:**
The --throttle option (specified in bytes/sec) limits the bandwidth used during partition reassignments to reduce cluster impact. Partition moves use significant network and disk I/O, affecting page cache and overall performance. Throttling prevents overwhelming the cluster during large-scale reassignments.

----

## Question 27
**Correct Answer: B++**

**Explanation:**
The --cancel option with kafka-reassign-partitions.sh safely cancels in-progress reassignments. This feature was added to replace the dangerous manual ZooKeeper znode deletion method. Cancellation attempts to restore the replica set to its state before reassignment began.

----

## Question 28
**Correct Answer: C++**

**Explanation:**
kafka-dump-log.sh decodes log segment files to view individual messages without consuming them. It can print message metadata (offsets, timestamps, sizes) or full message payloads. This is invaluable for diagnosing issues with corrupted messages or examining specific log segment contents.

----

## Question 29
**Correct Answer: B++**

**Explanation:**
The --print-data-log option with kafka-dump-log.sh prints the actual message payload along with metadata like offsets, timestamps, key sizes, and checksums. Without this option, only message metadata is displayed, not the actual message content.

----

## Question 30
**Correct Answer: B++**

**Explanation:**
kafka-replica-verification.sh verifies that replicas for topic partitions are identical across the cluster. It fetches messages from all replicas in parallel, checks for consistency, and prints the maximum lag. This tool has significant cluster impact (similar to reassignments) as it must read all messages from the oldest offset.

----

## Question 31
**Correct Answer: B++**

**Explanation:**
Replica verification has significant cluster impact because it must read all messages from all replicas for verification, consuming substantial network and disk I/O resources. The impact is similar to partition reassignments. It should be used with caution and typically only when specific consistency issues are suspected.

----

## Question 32
**Correct Answer: A++**

**Explanation:**
The controller election information resides in the ZooKeeper znode at /admin/controller. This ephemeral node contains the broker ID of the current controller. When a broker becomes controller, it creates this node, and when it steps down or fails, the node is automatically deleted.

----

## Question 33
**Correct Answer: B++**

**Explanation:**
Manually deleting the /admin/controller znode forces the current controller to resign, triggering a new controller election. The cluster will then randomly select a new controller from the available brokers. This is sometimes used when troubleshooting a misbehaving controller, though it's not a normal operational task.

----

## Question 34
**Correct Answer: B++**

**Explanation:**
The unclean.leader.election.enable configuration allows replicas that are not in sync to be elected as leader, potentially resulting in data loss. This can be useful temporarily to unstick a cluster when unavoidable data loss has occurred, or for topics where some data loss is acceptable to maintain availability.

----

## Question 35
**Correct Answer: B++**

**Explanation:**
Before manually deleting a topic from ZooKeeper, all brokers in the cluster must be shut down. Modifying cluster metadata in ZooKeeper while brokers are online is extremely dangerous and can corrupt the cluster state. This is considered an unsafe operation that should only be done in emergency situations.

----

## Question 36
**Correct Answer: A++**

**Explanation:**
The --partition option allows the console consumer to consume from a specific partition ID. This is useful for debugging or when you need to inspect messages in a particular partition. It can be combined with --offset to start from a specific position within that partition.

----

## Question 37
**Correct Answer: B++**

**Explanation:**
kafka.tools.ChecksumMessageFormatter prints only message checksums, useful for verification without displaying full message content. Other available formatters include LoggingMessageFormatter (outputs to logger), NoOpMessageFormatter (consumes without output), and the default DefaultMessageFormatter.

----

## Question 38
**Correct Answer: B++**

**Explanation:**
For keyed topics, it's advisable to set the partition count once at creation and avoid resizing. Adding partitions changes the key-to-partition mapping, which can cause issues for consumers expecting consistent ordering. Messages with the same key may end up in different partitions after a partition increase.

----

## Question 39
**Correct Answer: B++**

**Explanation:**
The --at-min-isr-partitions option shows partitions where the ISR count exactly matches the minimum in-sync replicas setting. These partitions are still available but have lost all redundancy. If one more replica goes offline, they would become read-only or unavailable depending on producer settings.

----

## Question 40
**Correct Answer: C++**

**Explanation:**
The --reset-offsets with --dry-run option exports offsets in CSV format with the structure: <topic>,<partition>,<offset>. This format can be easily edited and then imported using --from-file to reset consumer group offsets to specific positions.

----

## Question 41
**Correct Answer: B++**

**Explanation:**
Before importing offsets, all consumers in the group must be stopped. If consumers are active, they will continue processing and overwrite the imported offsets with their current positions. Stopping consumers ensures the offset reset takes effect when consumers restart.

----

## Question 42
**Correct Answer: B++**

**Explanation:**
The min.insync.replicas configuration specifies the minimum number of replicas that must acknowledge a write for a produce request to succeed when acks=-1 (or "all"). This ensures data durability by requiring acknowledgment from multiple replicas before considering a write successful.

----

## Question 43
**Correct Answer: B++**

**Explanation:**
The --additional option allows you to add new reassignments to existing ones without interrupting ongoing partition moves. This enables continuous reassignment operations without waiting for previous moves to complete before starting new ones.

----

## Question 44
**Correct Answer: B++**

**Explanation:**
To change replication factor, manually craft a JSON file with the desired replica count for each partition. For example, to increase RF from 2 to 3, add a third broker ID to each partition's replica list. The tool then handles adding new replicas and removing old ones as needed.

----

## Question 45
**Correct Answer: D++**

**Explanation:**
Restarting a broker safely removes leadership from it as the broker transfers leadership to other brokers during shutdown. This distributes replication traffic across the cluster when reassigning partitions away from the broker, significantly improving performance compared to moving partitions while leadership remains on the decommissioning broker.

----

## Question 46
**Correct Answer: C++**

**Explanation:**
The --unavailable-partitions option shows partitions without a leader, indicating a serious situation where the partition is offline. These partitions cannot serve produce or consume requests until leadership is restored, typically after a broker recovery or unclean leader election.

----

## Question 47
**Correct Answer: B++**

**Explanation:**
kafka-preferred-replica-election.sh has been deprecated in favor of kafka-leader-election.sh. The new tool provides more functionality, including the ability to specify election type (PREFERRED or UNCLEAN) and better partition selection options via JSON files or command-line arguments.

----

## Question 48
**Correct Answer: B++**

**Explanation:**
The compression.type configuration controls the compression algorithm used by the broker when writing message batches to disk. Valid values include none, gzip, snappy, zstd, and lz4. This can significantly reduce storage requirements and network bandwidth usage.

----

## Question 49
**Correct Answer: B++**

**Explanation:**
The CLIENT-ID field displays the string provided by the client to identify itself. This is set by the client application and helps distinguish different consumer instances in logs and monitoring. It's different from the consumer group name and can be shared across multiple consumer groups.

----

## Question 50
**Correct Answer: B++**

**Explanation:**
During partition reassignment, the replication factor temporarily increases as new replicas are added before old ones are removed. New replicas copy all existing messages from the current leader. Once replication is complete, the controller removes the old replicas, returning the replication factor to its original size.

----

## Question 51
**Correct Answer: B++**

**Explanation:**
The --add-config-file argument allows configuration changes to be specified from a preformatted file rather than command-line arguments. This is useful for automation and managing multiple configurations consistently across environments, making it easier to maintain and version control configuration changes.

----

## Question 52
**Correct Answer: B++**

**Explanation:**
The cleanup.policy configuration determines whether messages are deleted based on retention settings (policy=delete) or compacted to keep only the latest value for each key (policy=compact). It can also be set to "delete,compact" to enable both behaviors. This fundamentally changes how Kafka handles message lifecycle.

----

## Question 53
**Correct Answer: B++**

**Explanation:**
Topic metadata in ZooKeeper is stored at /brokers/topics/<topic-name>. This path contains partition assignments, replica information, and other topic-level metadata. Brokers and clients read this information to understand topic structure and locate partition leaders.

----

## Question 54
**Correct Answer: B++**

**Explanation:**
The default message formatter is kafka.tools.DefaultMessageFormatter, which outputs raw message content. Other formatters include LoggingMessageFormatter (outputs via logger), ChecksumMessageFormatter (prints only checksums), and NoOpMessageFormatter (consumes without output).

----

## Question 55
**Correct Answer: C++**

**Explanation:**
Topic deletion is asynchronous. After marking a topic for deletion, the controller notifies brokers when it completes existing tasks. Brokers then invalidate metadata and delete log files. In large clusters with many partitions, this process can take time. Small clusters may complete deletion almost immediately.

----

## Question 56
**Correct Answer: B++**

**Explanation:**
The segment.ms configuration determines how frequently log segments are rotated for a topic, specified in milliseconds. For example, segment.ms=604800000 rotates segments weekly. Combined with segment.bytes, this controls when new log segments are created, affecting retention, compaction, and storage management.

----

## Question 57
**Correct Answer: A++**

**Explanation:**
The --sync option causes the console producer to send messages synchronously, waiting for each message to be acknowledged before sending the next one. This ensures message ordering and delivery confirmation but reduces throughput compared to asynchronous (batched) sending.

----

## Question 58
**Correct Answer: B++**

**Explanation:**
The controller_mutations_rate quota controls the rate at which create topics, create partitions, and delete topics requests are accepted. The rate is accumulated by the number of partitions created or deleted. This prevents overwhelming the controller with too many simultaneous topology changes.

----

## Question 59
**Correct Answer: A++**

**Explanation:**
The --disable-rack-aware option overrides rack-aware placement constraints during partition reassignment. This may be necessary when rack-aware settings prevent achieving the desired partition distribution due to rack capacity or availability limitations. Use with caution as it can reduce fault tolerance.

----

## Question 60
**Correct Answer: B++**

**Explanation:**
The Leader field in describe topic output shows which broker (by ID) is the partition leader. Each partition line displays: Topic, Partition ID, Leader (broker ID), Replicas (list of broker IDs), and Isr (in-sync replica broker IDs). This information is crucial for understanding partition distribution and health.