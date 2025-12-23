# Chapter 5: Managing Apache Kafka Programmatically

## Overview

There are many CLI and GUI tools for managing Kafka, but there are also times when you want to execute administrative commands from within your client application. Creating new topics on demand based on user input or data is an especially common use case.

Apache Kafka added the AdminClient in version 0.11 to provide a programmatic API for administrative functionality:
- Listing, creating, and deleting topics
- Describing the cluster
- Managing ACLs
- Modifying configuration

## AdminClient Overview

### Asynchronous and Eventually Consistent API

Kafka's AdminClient is asynchronous. Each method returns immediately after delivering a request to the cluster controller, and each method returns one or more `Future` objects. 

- `Future` objects are the result of asynchronous operations
- Kafka's AdminClient wraps `Future` objects into `Result` objects
- The `Futures` that AdminClient APIs return are considered complete when the controller state has been fully updated
- This property is called **eventual consistency**: eventually every broker will know about every topic

### Options

Every method in AdminClient takes as an argument an `Options` object that is specific to that method:
- `listTopics` method takes the `ListTopicsOptions` object
- `describeCluster` takes `DescribeClusterOptions`
- All methods have `timeoutMs`: controls how long the client will wait for a response

### Flat Hierarchy

All admin operations are implemented in `KafkaAdminClient` directly. Benefits:
- One JavaDoc to search
- IDE autocomplete will be quite handy
- No need to wonder about namespaces

## AdminClient Lifecycle

### Creating an AdminClient

```java
Properties props = new Properties();
props.put(AdminClientConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
AdminClient admin = AdminClient.create(props);
// TODO: Do something useful with AdminClient
admin.close(Duration.ofSeconds(30));
```

### Closing the AdminClient

- The `close` method accepts a timeout parameter
- Once you call `close`, you can't call any other methods
- The client will wait for responses until the timeout expires
- Calling `close` without a timeout implies the client will wait indefinitely

## Essential Topic Management

### Listing Topics

```java
ListTopicsResult topics = admin.listTopics();
topics.names().get().forEach(System.out::println);
```

### Describing Topics

Check if a topic exists and create it if needed:

```java
DescribeTopicsResult demoTopic = admin.describeTopics(TOPIC_LIST);
try {
  topicDescription = demoTopic.values().get(TOPIC_NAME).get();
  System.out.println("Description of demo topic:" + topicDescription);
} catch (ExecutionException e) {
  // Topic doesn't exist
}
```

### Creating Topics

```java
CreateTopicsResult newTopic = admin.createTopics(Collections.singletonList(
  new NewTopic(TOPIC_NAME, NUM_PARTITIONS, REP_FACTOR)));
```

### Deleting Topics

```java
admin.deleteTopics(TOPIC_LIST).all().get();
```

**WARNING**: Deletion of topics is final—there is no recycle bin or trash can. Deleting the wrong topic could mean unrecoverable loss of data.

## Configuration Management

### Describing Configuration

```java
ConfigResource configResource = new ConfigResource(ConfigResource.Type.TOPIC, TOPIC_NAME);
DescribeConfigsResult configsResult = admin.describeConfigs(Collections.singleton(configResource));
Config configs = configsResult.all().get().get(configResource);

// Print nondefault configs
configs.entries().stream()
  .filter(entry -> !entry.isDefault())
  .forEach(System.out::println);
```

### Modifying Configuration

```java
ConfigEntry compaction = new ConfigEntry(TopicConfig.CLEANUP_POLICY_CONFIG, 
  TopicConfig.CLEANUP_POLICY_COMPACT);

Collection<AlterConfigOp> configOp = new ArrayList<>();
configOp.add(new AlterConfigOp(compaction, AlterConfigOp.OpType.SET));

Map<ConfigResource, Collection<AlterConfigOp>> alterConf = new HashMap<>();
alterConf.put(configResource, configOp);
admin.incrementalAlterConfigs(alterConf).all().get();
```

## Consumer Group Management

### Exploring Consumer Groups

```java
admin.listConsumerGroups().valid().get().forEach(System.out::println);
```

### Describing Consumer Groups

```java
ConsumerGroupDescription groupDescription = admin
  .describeConsumerGroups(CONSUMER_GRP_LIST)
  .describedGroups().get(CONSUMER_GROUP).get();
System.out.println("Description of group " + CONSUMER_GROUP + ":" + groupDescription);
```

### Getting Consumer Group Offsets

```java
Map<TopicPartition, OffsetAndMetadata> offsets = admin
  .listConsumerGroupOffsets(CONSUMER_GROUP)
  .partitionsToOffsetAndMetadata().get();
```

### Calculating Lag

```java
Map<TopicPartition, OffsetSpec> requestLatestOffsets = new HashMap<>();
for(TopicPartition tp: offsets.keySet()) {
  requestLatestOffsets.put(tp, OffsetSpec.latest());
}

Map<TopicPartition, ListOffsetsResult.ListOffsetsResultInfo> latestOffsets = 
  admin.listOffsets(requestLatestOffsets).all().get();

for (Map.Entry<TopicPartition, OffsetAndMetadata> e: offsets.entrySet()) {
  long committedOffset = e.getValue().offset();
  long latestOffset = latestOffsets.get(e.getKey()).offset();
  long lag = latestOffset - committedOffset;
  System.out.println("Lag: " + lag);
}
```

### Modifying Consumer Group Offsets

```java
Map<TopicPartition, OffsetAndMetadata> resetOffsets = new HashMap<>();
for (Map.Entry<TopicPartition, ListOffsetsResult.ListOffsetsResultInfo> e: 
  earliestOffsets.entrySet()) {
  resetOffsets.put(e.getKey(), new OffsetAndMetadata(e.getValue().offset()));
}

try {
  admin.alterConsumerGroupOffsets(CONSUMER_GROUP, resetOffsets).all().get();
} catch (ExecutionException e) {
  if (e.getCause() instanceof UnknownMemberIdException) {
    System.out.println("Check if consumer group is still active.");
  }
}
```

## Cluster Metadata

```java
DescribeClusterResult cluster = admin.describeCluster();
System.out.println("Connected to cluster " + cluster.clusterId().get());
System.out.println("The brokers in the cluster are:");
cluster.nodes().get().forEach(node -> System.out.println(" * " + node));
System.out.println("The controller is: " + cluster.controller().get());
```

## Advanced Admin Operations

### Adding Partitions to a Topic

```java
Map<String, NewPartitions> newPartitions = new HashMap<>();
newPartitions.put(TOPIC_NAME, NewPartitions.increaseTo(NUM_PARTITIONS+2));
admin.createPartitions(newPartitions).all().get();
```

### Deleting Records from a Topic

```java
Map<TopicPartition, RecordsToDelete> recordsToDelete = new HashMap<>();
for (Map.Entry<TopicPartition, ListOffsetsResult.ListOffsetsResultInfo> e: 
  olderOffsets.entrySet()) {
  recordsToDelete.put(e.getKey(), RecordsToDelete.beforeOffset(e.getValue().offset()));
}
admin.deleteRecords(recordsToDelete).all().get();
```

### Leader Election

#### Preferred Leader Election
Each partition has a replica designated as the preferred leader. By default, Kafka checks every five minutes if the preferred leader replica is indeed the leader.

#### Unclean Leader Election
If the leader replica becomes unavailable and other replicas are not eligible, unclean leader election can restore availability but causes data loss.

```java
Set<TopicPartition> electableTopics = new HashSet<>();
electableTopics.add(new TopicPartition(TOPIC_NAME, 0));
try {
  admin.electLeaders(ElectionType.PREFERRED, electableTopics).all().get();
} catch (ExecutionException e) {
  if (e.getCause() instanceof ElectionNotNeededException) {
    System.out.println("All leaders are preferred already");
  }
}
```

### Reassigning Replicas

```java
Map<TopicPartition, Optional<NewPartitionReassignment>> reassignment = new HashMap<>();
reassignment.put(new TopicPartition(TOPIC_NAME, 0), 
  Optional.of(new NewPartitionReassignment(Arrays.asList(0,1))));
reassignment.put(new TopicPartition(TOPIC_NAME, 1), 
  Optional.of(new NewPartitionReassignment(Arrays.asList(1))));
reassignment.put(new TopicPartition(TOPIC_NAME, 2), 
  Optional.of(new NewPartitionReassignment(Arrays.asList(1,0))));
reassignment.put(new TopicPartition(TOPIC_NAME, 3), Optional.empty());

admin.alterPartitionReassignments(reassignment).all().get();
```

## Testing AdminClient

Apache Kafka provides `MockAdminClient` for testing without running an actual Kafka cluster.

```java
@Before
public void setUp() {
  Node broker = new Node(0,"localhost",9092);
  this.admin = spy(new MockAdminClient(Collections.singletonList(broker), broker));
  
  // Mock unimplemented methods
  AlterConfigsResult emptyResult = mock(AlterConfigsResult.class);
  doReturn(KafkaFuture.completedFuture(null)).when(emptyResult).all();
  doReturn(emptyResult).when(admin).incrementalAlterConfigs(any());
}
```

## Summary

AdminClient is a useful tool for:
- **Application developers**: Creating topics on the fly and validating topic configuration
- **Operators and SREs**: Creating automation around Kafka and recovering from incidents

Key methods covered:
- Topic management
- Configuration management
- Consumer group management
- Advanced operations like partitioning, leader election, and replica reassignment
