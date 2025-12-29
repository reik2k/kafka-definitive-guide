# Chapter 12: Administering Kafka

## TABLE OF CONTENTS

- [Topic Operations](#topic-operations)
  - [Creating a New Topic](#creating-a-new-topic)
  - [Listing All Topics in a Cluster](#listing-all-topics-in-a-cluster)
  - [Describing Topic Details](#describing-topic-details)
  - [Adding Partitions](#adding-partitions)
  - [Reducing Partitions](#reducing-partitions)
  - [Deleting a Topic](#deleting-a-topic)
- [Consumer Groups](#consumer-groups)
  - [List and Describe Groups](#list-and-describe-groups)
  - [Delete Group](#delete-group)
  - [Offset Management](#offset-management)
- [Dynamic Configuration Changes](#dynamic-configuration-changes)
  - [Overriding Topic Configuration Defaults](#overriding-topic-configuration-defaults)
  - [Overriding Client and User Configuration Defaults](#overriding-client-and-user-configuration-defaults)
  - [Overriding Broker Configuration Defaults](#overriding-broker-configuration-defaults)
  - [Describing Configuration Overrides](#describing-configuration-overrides)
  - [Removing Configuration Overrides](#removing-configuration-overrides)
- [Producing and Consuming](#producing-and-consuming)
  - [Console Producer](#console-producer)
  - [Console Consumer](#console-consumer)
- [Partition Management](#partition-management)
  - [Preferred Replica Election](#preferred-replica-election)
  - [Changing a Partition's Replicas](#changing-a-partitions-replicas)
  - [Dumping Log Segments](#dumping-log-segments)
  - [Replica Verification](#replica-verification)
- [Other Tools](#other-tools)
- [Unsafe Operations](#unsafe-operations)
  - [Moving the Cluster Controller](#moving-the-cluster-controller)
  - [Removing Topics to Be Deleted](#removing-topics-to-be-deleted)
  - [Deleting Topics Manually](#deleting-topics-manually)
- [Summary](#summary)

Managing a Kafka cluster requires additional tooling to perform administrative changes to topics, configurations, and more. Kafka provides several command-line interface (CLI) utilities that are useful for making administrative changes to your clusters. The tools are implemented in Java classes, and a set of scripts are provided natively to call those classes properly. While these tools provide basic functions, you may find they are lacking for more complex operations or are unwieldy to use at larger scales. This chapter will describe only the basic tools that are available as part of the Apache Kafka open source project.

> **AUTHORIZING ADMIN OPERATIONS**
>
> While Apache Kafka implements authentication and authorization to control topic operations, default configurations do not restrict the use of these tools. This means that these CLI tools can be used without any authentication required, which will allow operations such as topic changes to be executed with no security check or audit. Always ensure that access to this tooling on your deployments is restricted to administrators only to prevent unauthorized changes.

## Topic Operations

The `kafka-topics.sh` tool provides easy access to most topic operations. It allows you to create, modify, delete, and list information about topics in the cluster. While some topic configurations are possible through this command, they have been deprecated, and it is recommended to use the more robust method of using the `kafka-config.sh` tool for configuration changes.

To use the `kafka-topics.sh` command, you must provide the cluster connection string and port through the `--bootstrap-server` option. In the examples that follow, the cluster connect string is being run locally on one of the hosts in the Kafka cluster, and we will be using `localhost:9092`.

> **CHECK THE VERSION**
>
> Many of the command-line tools for Kafka have a dependency on the version of Kafka running to operate correctly. This includes some commands that may store data in ZooKeeper rather than connecting to the brokers themselves. For this reason, it is important to make sure the version of the tools that you are using matches the version of the brokers in the cluster. The safest approach is to run the tools on the Kafka brokers themselves, using the deployed version.

### Creating a New Topic

When creating a new topic through the `--create` command, there are several required arguments to create a new topic in a cluster. These arguments must be provided when using this command even though some of them may have broker-level defaults configured already. Here is a list of the three required arguments:

- `--topic`: The name of the topic that you wish to create.
- `--replication-factor`: The number of replicas of the topic to maintain within the cluster.
- `--partitions`: The number of partitions to create for the topic.

> **GOOD TOPIC NAMING PRACTICES**
>
> Topic names may contain alphanumeric characters, underscores, dashes, and periods; however, it is not recommended to use periods in topic names. Internal metrics inside of Kafka convert period characters to underscore characters (e.g., "topic.1" becomes "topic_1" in metrics calculations), which can result in conflicts in topic names.
>
> Another recommendation is to avoid using a double underscore to start your topic name. By convention, topics internal to Kafka operations are created with a double underscore naming convention (like the `__consumer_offsets` topic). As such it is not recommended to have topic names that begin with the double underscore naming convention to prevent confusion.

Creating a new topic is simple:

```bash
# kafka-topics.sh --bootstrap-server <hostname>:<port> --create --topic <topic name> --replication-factor <integer> --partitions <integer>
#
```

For example, create a topic named "my-topic" with eight partitions that have two replicas each:

```bash
# kafka-topics.sh --bootstrap-server localhost:9092 --create \
  --topic my-topic --replication-factor 2 --partitions 8
Created topic "my-topic".
#
```

### Listing All Topics in a Cluster

The `--list` command lists all topics in a cluster. The list is formatted with one topic per line, in no particular order.

```bash
# kafka-topics.sh --bootstrap-server localhost:9092 --list
__consumer_offsets
my-topic
other-topic
```

### Describing Topic Details

It is also possible to get detailed information on one or more topics in the cluster. The output includes the partition count, topic configuration overrides, and a listing of each partition with its replica assignments.

```bash
# kafka-topics.sh --boostrap-server localhost:9092 --describe --topic my-topic
Topic: my-topic PartitionCount: 8 ReplicationFactor: 2 Configs: segment.bytes=1073741824
Topic: my-topic Partition: 0 Leader: 1 Replicas: 1,0 Isr: 1,0
Topic: my-topic Partition: 1 Leader: 0 Replicas: 0,1 Isr: 0,1
Topic: my-topic Partition: 2 Leader: 1 Replicas: 1,0 Isr: 1,0
Topic: my-topic Partition: 3 Leader: 0 Replicas: 0,1 Isr: 0,1
Topic: my-topic Partition: 4 Leader: 1 Replicas: 1,0 Isr: 1,0
Topic: my-topic Partition: 5 Leader: 0 Replicas: 0,1 Isr: 0,1
Topic: my-topic Partition: 6 Leader: 1 Replicas: 1,0 Isr: 1,0
Topic: my-topic Partition: 7 Leader: 0 Replicas: 0,1 Isr: 0,1
#
```

The `--describe` command also has several useful options for filtering the output:

- `--topics-with-overrides`: This will describe only the topics that have configurations that differ from the cluster defaults.
- `--under-replicated-partitions`: This shows all partitions where one or more of the replicas are not in sync with the leader.
- `--at-min-isr-partitions`: This shows all partitions where the number of replicas exactly match the setting for minimum in-sync replicas (ISRs).
- `--under-min-isr-partitions`: This shows all partitions where the number of ISRs is below the configured minimum.
- `--unavailable-partitions`: This shows all topic partitions without a leader.

### Adding Partitions

It is sometimes necessary to increase the number of partitions for a topic. The most common reason to increase the partition count is to horizontally scale a topic across more brokers by decreasing the throughput for a single partition.

```bash
# kafka-topics.sh --bootstrap-server localhost:9092 \
  --alter --topic my-topic --partitions 16
#
```

> **ADJUSTING KEYED TOPICS**
>
> *Topics that are produced with keyed messages can be very difficult to add partitions to from a consumer's point of view. This is because the mapping of keys to partitions will change when the number of partitions is changed. For this reason, it is advisable to set the number of partitions for a topic that will contain keyed messages once, when the topic is created, and avoid resizing the topic.*

### Reducing Partitions

It is not possible to reduce the number of partitions for a topic. Deleting a partition from a topic would cause part of the data in that topic to be deleted as well, which would be inconsistent from a client point of view.

### Deleting a Topic

Even a topic with no messages uses cluster resources such as disk space, open filehandles, and memory. If a topic is no longer needed, it can be deleted to free up these resources. To perform this action, the brokers in the cluster must be configured with the `delete.topic.enable` option set to `true`.

> **DATA LOSS AHEAD**
>
> Deleting a topic will also delete all its messages. This is not a reversible operation. Make sure it is executed carefully.

```bash
# kafka-topics.sh --bootstrap-server localhost:9092 \
  --delete --topic my-topic
Note: This will have no impact if delete.topic.enable is not set
to true.
#
```

## Consumer Groups

Consumer groups are coordinated groups of Kafka consumers consuming from topics or multiple partitions of a single topic. The `kafka-consumer-groups.sh` tool helps manage and gain insight into the consumer groups that are consuming from topics in the cluster.

### List and Describe Groups

To list consumer groups, use the `--bootstrap-server` and `--list` parameters:

```bash
# kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list
console-consumer-95554
console-consumer-9581
my-consumer
#
```

For any group listed, you can get more details by changing the `--list` parameter to `--describe` and adding the `--group` parameter:

```bash
# kafka-consumer-groups.sh --bootstrap-server localhost:9092 \
  --describe --group my-consumer
GROUP TOPIC PARTITION CURRENT-OFFSET LOG-END-OFFSET LAG CONSUMER-ID HOST CLIENT-ID
my-consumer my-topic 0 2 4 2 consumer-1-029af89c-873c-4751-a720-cefd41a669d6 /127.0.0.1 consumer-1
my-consumer my-topic 1 2 3 1 consumer-1-029af89c-873c-4751-a720-cefd41a669d6 /127.0.0.1 consumer-1
my-consumer my-topic 2 2 3 1 consumer-2-42c1abd4-e3b2-425d-a8bb-e1ea49b29bb2 /127.0.0.1 consumer-2
#
```

**Table 12-1: Fields provided for group named "my-consumer"**

| Field | Description |
|-------|-------------|
| GROUP | The name of the consumer group. |
| TOPIC | The name of the topic being consumed. |
| PARTITION | The ID number of the partition being consumed. |
| CURRENT-OFFSET | The next offset to be consumed by the consumer group for this topic partition. |
| LOG-END-OFFSET | The current high-water mark offset from the broker for the topic partition. |
| LAG | The difference between the consumer Current-Offset and the broker Log-End-Offset. |
| CONSUMER-ID | A generated unique consumer-id based on the provided client-id. |
| HOST | Address of the host the consumer group is reading from. |
| CLIENT-ID | String provided by the client identifying the client. |

### Delete Group

Deletion of consumer groups can be performed with the `--delete` argument. This will remove the entire group, including all stored offsets for all topics that the group is consuming:

```bash
# kafka-consumer-groups.sh --bootstrap-server localhost:9092 --delete --group my-consumer
Deletion of requested consumer groups ('my-consumer') was successful.
#
```

### Offset Management

In addition to displaying and deleting the offsets for a consumer group, it is also possible to retrieve the offsets and store new offsets in a batch. This is useful for resetting the offsets for a consumer when there is a problem.

#### Export offsets

To export offsets from a consumer group to a CSV file, use the `--reset-offsets` argument with the `--dry-run` option:

```bash
# kafka-consumer-groups.sh --bootstrap-server localhost:9092 \
  --export --group my-consumer --topic my-topic \
  --reset-offsets --to-current --dry-run > offsets.csv
# cat offsets.csv
my-topic,0,8905
my-topic,1,8915
my-topic,2,9845
my-topic,3,8072
my-topic,4,8008
my-topic,5,8319
my-topic,6,8102
my-topic,7,12739
#
```

#### Import offsets

The import offset tool takes the file produced by exporting offsets and uses it to set the current offsets for the consumer group:

> **STOP CONSUMERS FIRST**
>
> *Before performing this step, all consumers in the group must be stopped. They will not read the new offsets if they are written while the consumer group is active.*

```bash
# kafka-consumer-groups.sh --bootstrap-server localhost:9092 \
  --reset-offsets --group my-consumer \
  --from-file offsets.csv --execute
TOPIC PARTITION NEW-OFFSET
my-topic 0 8905
my-topic 1 8915
my-topic 2 9845
my-topic 3 8072
my-topic 4 8008
my-topic 5 8319
my-topic 6 8102
my-topic 7 12739
#
```

## Dynamic Configuration Changes

There is a plethora of configurations for topics, clients, brokers, and more that can be updated dynamically during runtime without having to shut down or redeploy a cluster. The `kafka-configs.sh` is the main tool for modifying these configs.

### Overriding Topic Configuration Defaults

There are many configurations that are set by default for topics that are defined in the static broker configuration files. With dynamic configurations, we can override the cluster-level defaults for individual topics.

The format of the command to change a topic configuration is:

```bash
kafka-configs.sh --bootstrap-server localhost:9092 \
  --alter --entity-type topics --entity-name <topic name> \
  --add-config <key>=<value>[,<key>=<value>...]
```

For example, setting the retention for the topic named "my-topic" to 1 hour (3,600,000 ms):

```bash
# kafka-configs.sh --bootstrap-server localhost:9092 \
  --alter --entity-type topics --entity-name my-topic \
  --add-config retention.ms=3600000
Updated config for topic: "my-topic".
#
```

**Table 12-2: Valid keys for topics**

| Configuration key | Description |
|-------------------|-------------|
| `cleanup.policy` | If set to `compact`, the messages in this topic will be discarded and only the most recent message with a given key is retained. |
| `compression.type` | The compression type used by the broker when writing message batches for this topic to disk. |
| `delete.retention.ms` | How long, in milliseconds, deleted tombstones will be retained for this topic. |
| `max.message.bytes` | The maximum size of a single message for this topic, in bytes. |
| `min.insync.replicas` | The minimum number of replicas that must be in sync for a partition of the topic to be considered available. |
| `retention.bytes` | The amount of messages, in bytes, to retain for this topic. |
| `retention.ms` | How long messages should be retained for this topic, in milliseconds. |
| `segment.bytes` | The amount of messages, in bytes, that should be written to a single log segment. |
| `segment.ms` | How frequently, in milliseconds, the log segment for each partition should be rotated. |

### Overriding Client and User Configuration Defaults

For Kafka clients and users, there are only a few configurations that can be overridden, which are all essentially types of quotas. Two of the more common configurations to change are the bytes/sec rates allowed for producers and consumers with a specified client ID on a per-broker basis.

**Table 12-3: The configurations (keys) for clients**

| Configuration key | Description |
|-------------------|-------------|
| `consumer_bytes_rate` | The amount of messages, in bytes, that a single client ID is allowed to consume from a single broker in one second. |
| `producer_bytes_rate` | The amount of messages, in bytes, that a single client ID is allowed to produce to a single broker in one second. |
| `controller_mutations_rate` | The rate at which mutations are accepted for the create topics request, the create partitions request, and the delete topics request. |
| `request_percentage` | The percentage per quota window for requests from the user or client. |

### Overriding Broker Configuration Defaults

Broker- and cluster-level configs will primarily be configured statically in the cluster configuration files, but there is a plethora of configs that can be overridden during runtime without needing to redeploy Kafka. A few important configs worth pointing out specifically are:

- `min.insync.replicas`: Adjusts the minimum number of replicas that need to acknowledge a write.
- `unclean.leader.election.enable`: Allows replicas to be elected as leader even if it results in data loss.
- `max.connections`: The maximum number of connections allowed to a broker at any time.

### Describing Configuration Overrides

All configuration overrides can be listed using the `kafka-config.sh` tool:

```bash
# kafka-configs.sh --bootstrap-server localhost:9092 \
  --describe --entity-type topics --entity-name my-topic
Configs for topics:my-topic are
retention.ms=3600000
#
```

### Removing Configuration Overrides

Dynamic configurations can be removed entirely, which will cause the entity to revert back to the cluster defaults:

```bash
# kafka-configs.sh --bootstrap-server localhost:9092 \
  --alter --entity-type topics --entity-name my-topic \
  --delete-config retention.ms
Updated config for topic: "my-topic".
#
```

## Producing and Consuming

While working with Kafka, you will often find it is necessary to manually produce or consume some sample messages. Two utilities are provided to help with this, `kafka-console-consumer.sh` and `kafka-console-producer.sh`.

### Console Producer

The `kakfa-console-producer.sh` tool can be used to write messages into a Kafka topic in your cluster. By default, messages are read one per line, with a tab character separating the key and the value.

```bash
# kafka-console-producer.sh --bootstrap-server localhost:9092 --topic my-topic
>Message 1
>Test Message 2
>Test Message 3
>Message 4
>^D
#
```

It is possible to pass normal producer configuration options to the console producer using the `--producer-property` option.

### Console Consumer

The `kafka-console-consumer.sh` tool provides a means to consume messages out of one or more topics in your Kafka cluster. The messages are printed in standard output, delimited by a new line.

As in other commands, the connection string to the cluster will be the `--bootstrap-server` option:

```bash
# kafka-console-consumer.sh --bootstrap-server localhost:9092 \
  --whitelist 'my.*' --from-beginning
Message 1
Test Message 2
Test Message 3
Message 4
^C
#
```

**Table 12-4: Message formatter properties**

| Property | Description |
|----------|-------------|
| `print.timestamp` | Set to `true` to display the timestamp of each message (if available). |
| `print.key` | Set to `true` to display the message key in addition to the value. |
| `print.offset` | Set to `true` to display the message offset in addition to the value. |
| `print.partition` | Set to `true` to display the topic partition a message is consumed from. |
| `key.separator` | Specify the delimiter character to use between the message key and message value when printing. |
| `line.separator` | Specify the delimiter character to use between messages. |
| `key.deserializer` | Provide a class name that is used to deserialize the message key before printing. |
| `value.deserializer` | Provide a class name that is used to deserialize the message value before printing. |

## Partition Management

A default Kafka installation also contains a few scripts for working with the management of partitions. One of these tools allows for the reelection of leader replicas; another is a low-level utility for assigning partitions to brokers.

### Preferred Replica Election

As described earlier, partitions can have multiple replicas for reliability. It is important to understand that only one of these replicas can be the leader for the partition at any given point in time. Maintaining a balance of which partition's replicas have leadership on which broker is necessary to ensure the load is spread out through a full Kafka cluster.

Leadership is defined within Kafka as the first in-sync replica in the replica list. If automatic leader balancing is not enabled, a lightweight procedure called preferred leader election can be performed using the `kafka-leader-election.sh` utility:

```bash
# kafka-leader-election.sh --bootstrap-server localhost:9092 \
  --election-type PREFERRED --all-topic-partitions
#
```

### Changing a Partition's Replicas

Occasionally it may be necessary to change the replica assignments manually for a partition. The `kafka-reassign-partitions.sh` can be used to perform this operation. This is a multistep process to generate a move set and then execute on the provided move set proposal.

To generate a set of partition moves, you must first create a file that contains a JSON object listing the topics:

```json
{
  "topics": [
    {"topic": "foo1"},
    {"topic": "foo2"}
  ],
  "version": 1
}
```

Generate a set of partition moves to move the topics listed in the file topics.json to brokers 5 and 6:

```bash
# kafka-reassign-partitions.sh --bootstrap-server localhost:9092 \
  --topics-to-move-json-file topics.json \
  --broker-list 5,6 --generate
```

To execute the proposed partition reassignment:

```bash
# kafka-reassign-partitions.sh --bootstrap-server localhost:9092 \
  --reassignment-json-file expand-cluster-reassignment.json \
  --execute
```

To check on the progress of the partition moves:

```bash
# kafka-reassign-partitions.sh --bootstrap-server localhost:9092 \
  --reassignment-json-file expand-cluster-reassignment.json \
  --verify
Status of partition reassignment:
Reassignment of partition [foo1,0] completed successfully
Reassignment of partition [foo1,1] is in progress
Reassignment of partition [foo1,2] is in progress
#
```

### Dumping Log Segments

On occasion you may have the need to read the specific content of a message. The `kafka-dump-log.sh` tool is provided to decode the log segments for a partition. This will allow you to view individual messages without needing to consume and decode them.

```bash
# kafka-dump-log.sh --files /tmp/kafka-logs/my-topic-0/00000000000000000000.log
Dumping /tmp/kafka-logs/my-topic-0/00000000000000000000.log
Starting offset: 0
baseOffset: 0 lastOffset: 0 count: 1 baseSequence: -1 lastSequence: -1
producerId: -1 producerEpoch: -1 partitionLeaderEpoch: 0
isTransactional: false isControl: false position: 0
CreateTime: 1623034799990 size: 77 magic: 2
compresscodec: NONE crc: 1773642166 isvalid: true
#
```

### Replica Verification

To validate that the replicas for a topic's partitions are the same across the cluster, you can use the `kafka-replica-verification.sh` tool for verification:

```bash
# kafka-replica-verification.sh --broker-list kafka.host1.domain.com:9092,kafka.host2.domain.com:9092 \
  --topic-white-list 'my.*'
2021-06-07 03:28:21,829: verification process is started.
2021-06-07 03:28:51,949: max lag is 0 for partition my-topic-0 at offset 4 among 1 partitions
#
```

## Other Tools

Several more tools are included in the Kafka distribution that are not covered in depth in this book that can be useful in administering your Kafka cluster for specific use cases:

- **Client ACLs**: A command-line tool, `kafka-acls.sh`, is provided for interacting with access controls for Kafka clients.
- **Lightweight MirrorMaker**: A lightweight `kafka-mirror-maker.sh` script is available for mirroring data.
- **Testing tools**: There are several other scripts used for testing Kafka or helping to perform upgrades of features. `kafka-broker-api-versions.sh` helps to easily identify different versions of usable API elements when upgrading. There are producer and consumer performance tests scripts. There is also `trogdor.sh`, which is a test framework designed to run benchmarks and other workloads.

## Unsafe Operations

There are some administrative tasks that are technically possible to do but should not be attempted except in the most extreme situations. Often this is when you are diagnosing a problem and have run out of options.

> **DANGER: HERE BE DRAGONS**
>
> The operations in this section often involve working with the cluster metadata stored in ZooKeeper directly. This can be a very dangerous operation, so you must be very careful to not modify the information in ZooKeeper directly, except as noted.

### Moving the Cluster Controller

Every Kafka cluster has a single broker that is designated as a controller. The controller has a special thread that is responsible for overseeing cluster operations in addition to normal broker work. On occasion, when troubleshooting a misbehaving cluster or broker, it may be useful to forcibly move the controller to a different broker without shutting down the host.

To forcibly move a controller, deleting the ZooKeeper znode at /admin/controller manually will cause the current controller to resign, and the cluster will randomly select a new controller.

### Removing Topics to Be Deleted

When attempting to delete a topic in Kafka, a ZooKeeper node requests that the deletion is created. Sometimes things can go wrong with this process. To "unstick" topic deletion, first delete the /admin/delete_topic/<topic name> znode. Deleting the topic ZooKeeper nodes will remove the pending requests.

### Deleting Topics Manually

If you are running a cluster with delete topics disabled, or if you find yourself needing to delete some topics outside of the normal flow of operations, it is possible to manually delete them from the cluster. This requires a full shutdown of all brokers in the cluster.

> **SHUT DOWN BROKERS FIRST**
>
> *Modifying the cluster metadata in ZooKeeper when the cluster is online is a very dangerous operation and can put the cluster into an unstable state. Never attempt to delete or modify topic metadata in ZooKeeper while the cluster is online.*

To delete a topic from the cluster:

1. Shut down all brokers in the cluster.
2. Remove the ZooKeeper path /brokers/topics/<topic name> from the Kafka cluster path.
3. Remove the partition directories from the log directories on each broker.
4. Restart all brokers.

## Summary

Running a Kafka cluster can be a daunting endeavor, with numerous configurations and maintenance tasks to keep the systems running at peak performance. In this chapter, we discussed many of the routine tasks, such as managing topic and client configurations, that you will need to handle frequently. We also covered some of the more esoteric tasks that you'll need for debugging problems, like examining log segments. Finally, we covered a few of the operations that, while not safe or routine, can be used to get you out of a sticky situation. All together, these tools will help you to manage your Kafka cluster.

As you begin to scale your Kafka clusters larger, even the use of these tools may become arduous and difficult to manage. It is highly recommended to engage with the open source Kafka community and take advantage of the many other open source projects in the ecosystem to help automate many of the tasks outlined in this chapter.

## External Resources

- [Apache Kafka website](https://kafka.apache.org/)
- [Apache Kafka documentation - Broker Configs](https://kafka.apache.org/41/configuration/broker-configs/)
