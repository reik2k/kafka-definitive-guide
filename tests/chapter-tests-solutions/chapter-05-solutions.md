# Chapter 5: Managing Apache Kafka Programmatically — Solutions

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 5

[Back to Test](../../chapter-tests/chapter-05-test.md) | [Main README](../../README.md)

---

## Answer Key

### Question 1: C) To programmatically manage Kafka administrative tasks
**Explanation:** AdminClient provides a programmatic API for administrative functionality like listing, creating, deleting topics, managing ACLs, and modifying configuration.

### Question 2: D) 0.11
**Explanation:** Apache Kafka added the AdminClient in version 0.11 to provide programmatic API for administrative tasks.

### Question 3: B) Asynchronous with Future objects
**Explanation:** AdminClient is asynchronous. Each method returns immediately after delivering a request and returns Future objects.

### Question 4: B) Result objects wrapping Future objects
**Explanation:** AdminClient wraps Future objects into Result objects, which provide methods to wait for operations and helper methods for common follow-up operations.

### Question 5: B) All brokers will know about changes eventually, but not immediately
**Explanation:** Kafka's metadata propagation from controller to brokers is asynchronous. Futures complete when the controller state is updated, but not every broker may be aware of the new state immediately.

### Question 6: B) bootstrap.servers
**Explanation:** The only mandatory configuration is the URI for your cluster (bootstrap.servers): a comma-separated list of brokers to connect to.

### Question 7: C) The client waits for all ongoing operations to complete
**Explanation:** Calling close() without a timeout means the client will wait as long as it takes for all ongoing operations to complete.

### Question 8: B) How long the client waits for a response before throwing TimeoutException
**Explanation:** The timeoutMs option controls how long the client will wait for a response from the cluster before throwing a TimeoutException.

### Question 9: C) The controller
**Explanation:** All operations that modify the cluster state (create, delete, alter) are handled by the controller.

### Question 10: B) The least-loaded broker
**Explanation:** Operations that read the cluster state (list, describe) can be handled by any broker and are directed to the least-loaded broker.

### Question 11: B) AdminClient.create(props)
**Explanation:** The static create() method takes a Properties object with configuration and returns an AdminClient instance.

### Question 12: B) You cannot call any other methods
**Explanation:** Once you call close(), you can't call any other methods and send any more requests.

### Question 13: B) To handle DNS aliases and multiple IP addresses
**Explanation:** client.dns.lookup configuration handles use cases involving DNS aliases and single DNS names that map to multiple IP addresses.

### Question 14: B) When using DNS aliases with SASL authentication
**Explanation:** Use resolve_canonical_bootstrap_servers_only when using DNS aliases with SASL to prevent authentication failures due to name mismatches.

### Question 15: B) When brokers are behind load balancers with multiple IPs
**Explanation:** Use use_all_dns_ips when brokers are behind load balancers with multiple IP addresses to ensure client doesn't miss benefits of highly available load balancing.

### Question 16: C) 120 seconds
**Explanation:** The default value for request.timeout.ms is 120 seconds (quite long, but some operations like consumer group management can take a while).

### Question 17: B) admin.listTopics()
**Explanation:** admin.listTopics() returns a list of all topics in the cluster.

### Question 18: C) A ListTopicsResult object wrapping Future collections
**Explanation:** listTopics() returns a ListTopicsResult object, which is a thin wrapper over a collection of Futures.

### Question 19: B) Call get() on the Future
**Explanation:** Calling get() on the Future causes the executing thread to wait until the server responds or you get a timeout exception.

### Question 20: B) admin.describeTopics()
**Explanation:** describeTopics() provides detailed information about specific topics.

### Question 21: B) Partitions, leader, replicas, and in-sync replicas
**Explanation:** TopicDescription contains a list of all partitions and for each partition: which broker is the leader, a list of replicas, and a list of in-sync replicas.

### Question 22: B) UnknownTopicOrPartitionException
**Explanation:** When describing a topic that doesn't exist, the server sends UnknownTopicOrPartitionException as the cause of ExecutionException.

### Question 23: C) admin.createTopics()
**Explanation:** admin.createTopics() creates new topics (note the plural form).

### Question 24: B) NewTopic
**Explanation:** NewTopic object represents a new topic to be created, with name, partitions, replicas, and configuration.

### Question 25: C) Broker defaults are used
**Explanation:** When creating a topic, if number of partitions and replicas are not specified, the defaults configured on the Kafka brokers will be used.

### Question 26: C) admin.deleteTopics()
**Explanation:** admin.deleteTopics() deletes topics (accepts a list of topic names).

### Question 27: B) Data is permanently lost with no recovery option
**Explanation:** In Kafka, deletion of topics is final—there is no recycle bin to rescue deleted topics. Deleting the wrong topic could mean unrecoverable loss of data.

### Question 28: B) Use whenComplete() on the Future
**Explanation:** Instead of using blocking get(), you can use whenComplete() to construct a function that will be called when the Future completes.

### Question 29: B) admin.describeConfigs()
**Explanation:** admin.describeConfigs() describes configuration for ConfigResources (topics, brokers, etc.).

### Question 30: B) ConfigResource
**Explanation:** ConfigResource represents a resource whose configuration you want to describe or modify (with type TOPIC, BROKER, or BROKER_LOGGER).

### Question 31: C) TOPIC, BROKER, and BROKER_LOGGER
**Explanation:** ConfigResource types include TOPIC, BROKER, and BROKER_LOGGER.

### Question 32: B) Use isDefault() method
**Explanation:** Each configuration entry has an isDefault() method that indicates which configs were modified vs default values.

### Question 33: D) Both A and C
**Explanation:** Both alterConfigs() and incrementalAlterConfigs() can modify configuration. incrementalAlterConfigs() is newer and supports more operation types.

### Question 34: B) SET, DELETE, APPEND, SUBTRACT
**Explanation:** The four AlterConfigOp operation types are: SET (sets value), DELETE (removes and resets to default), APPEND, and SUBTRACT.

### Question 35: B) For configurations with List type
**Explanation:** APPEND and SUBTRACT apply only to configurations with List type, allowing adding/removing values without sending the entire list.

### Question 36: B) admin.listConsumerGroups()
**Explanation:** admin.listConsumerGroups() lists all consumer groups in the cluster.

### Question 37: B) Returns only groups without errors
**Explanation:** The valid() method returns a collection containing only consumer groups that the cluster returned without errors.

### Question 38: B) admin.describeConsumerGroups()
**Explanation:** admin.describeConsumerGroups() provides detailed information about consumer groups.

### Question 39: B) Members, hosts, partitions, assignment algorithm, coordinator
**Explanation:** ConsumerGroupDescription contains group members, their identifiers and hosts, partitions assigned to them, the assignment algorithm, and the group coordinator host.

### Question 40: B) admin.listConsumerGroupOffsets()
**Explanation:** admin.listConsumerGroupOffsets() retrieves committed offsets for a consumer group.

### Question 41: B) One consumer group only
**Explanation:** Unlike describeConsumerGroups(), listConsumerGroupOffsets() only accepts a single consumer group, not a collection.

### Question 42: B) The offset of the last message in the partition
**Explanation:** OffsetSpec.latest() returns the offset of the last message in the partition.

### Question 43: B) Returns offset of record written on or after specified timestamp
**Explanation:** OffsetSpec.forTimestamp() returns the offset of the record written on or immediately after the specified timestamp.

### Question 44: C) admin.alterConsumerGroupOffsets()
**Explanation:** admin.alterConsumerGroupOffsets() modifies committed offsets for a consumer group.

### Question 45: C) Only when consumer group is inactive
**Explanation:** Kafka will prevent you from modifying offsets while the consumer group is active to prevent overriding offsets that consumers won't know about.

### Question 46: B) UnknownMemberIdException
**Explanation:** Attempting to modify offsets for an active group throws UnknownMemberIdException because it appears as if a non-member client is committing offsets.

### Question 47: B) Impact on stored state in stream applications
**Explanation:** If the consumer maintains state (like stream processing apps), resetting offsets without appropriately modifying stored state can cause issues like double-counting.

### Question 48: B) admin.describeCluster()
**Explanation:** admin.describeCluster() retrieves cluster metadata.

### Question 49: B) Cluster ID, brokers, and controller
**Explanation:** describeCluster() returns the cluster identifier (GUID), list of broker nodes, and which broker is the controller.

### Question 50: C) admin.createPartitions()
**Explanation:** admin.createPartitions() adds partitions to existing topics.

### Question 51: B) Total number of partitions after expansion
**Explanation:** When expanding topics, you specify the total number of partitions the topic will have after partitions are added, not the number of new partitions.

### Question 52: B) Messages with same key may go to different partitions
**Explanation:** Adding partitions breaks the key-to-partition mapping. Messages with the same key that were previously going to the same partition may now go to different partitions.

### Question 53: C) admin.deleteRecords()
**Explanation:** admin.deleteRecords() marks records as deleted and makes them inaccessible.

### Question 54: B) Marks records as deleted and makes them inaccessible
**Explanation:** deleteRecords() marks records with specified offsets as deleted and makes them inaccessible to consumers. Full cleanup from disk happens asynchronously.

### Question 55: B) Preferred and Unclean
**Explanation:** The two types of leader election are Preferred leader election and Unclean leader election.

### Question 56: B) A designated replica that should be leader for balanced distribution
**Explanation:** Each partition has a replica designated as the preferred leader. Using preferred leaders ensures balanced leader distribution across brokers.

### Question 57: B) Data loss
**Explanation:** Unclean leader election causes data loss—all events written to the old leader and not replicated to the new leader will be lost.

### Question 58: C) admin.electLeaders()
**Explanation:** admin.electLeaders() triggers leader election (note the plural form).

### Question 59: C) admin.alterPartitionReassignments()
**Explanation:** admin.alterPartitionReassignments() provides fine-grain control over the placement of every replica for a partition.

### Question 60: B) MockAdminClient
**Explanation:** MockAdminClient is a test class that allows testing AdminClient operations without running an actual Kafka cluster.

---

## Study Tips

### Key Concepts to Master:
1. **AdminClient Lifecycle:** Create, configure, close operations
2. **Asynchronous Operations:** Future objects, Result wrappers, whenComplete() patterns
3. **Topic Management:** List, describe, create, delete operations
4. **Configuration Management:** ConfigResource types, alter operations (SET, DELETE, APPEND, SUBTRACT)
5. **Consumer Group Management:** List, describe, offset management, reset procedures
6. **Advanced Operations:** Partition expansion, record deletion, leader election, replica reassignment

### Related CCDAK Topics:
- AdminClient API usage and patterns
- Topic lifecycle management
- Consumer group offset management
- Configuration modification strategies
- Operational best practices for Kafka administration

---

[Back to Test](../../chapter-tests/chapter-05-test.md) | [Main README](../../README.md)