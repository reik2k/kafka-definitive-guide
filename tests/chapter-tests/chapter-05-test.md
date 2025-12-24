# Chapter 5: Managing Apache Kafka Programmatically — CCDAK Practice Test

**Based on:** Kafka: The Definitive Guide, 2nd Edition, Chapter 5

**Total Questions:** 60

[Link to Solutions](../../chapter-tests-solutions/chapter-05-solutions.md)

---

## Question 1
What is the primary purpose of the Kafka AdminClient?
A) To produce messages to topics
B) To consume messages from topics
C) To programmatically manage Kafka administrative tasks
D) To configure broker JVM settings

## Question 2
Which version of Apache Kafka introduced the AdminClient?
A) 0.8
B) 0.9
C) 0.10
D) 0.11

## Question 3
What design pattern does the AdminClient API follow?
A) Synchronous and blocking
B) Asynchronous with Future objects
C) Event-driven callbacks
D) Publisher-subscriber

## Question 4
What object type does each AdminClient method return?
A) CompletableFuture
B) Result objects wrapping Future objects
C) Observable streams
D) Promise objects

## Question 5
What does "eventual consistency" mean in the context of AdminClient operations?
A) Operations are guaranteed to succeed eventually
B) All brokers will know about changes eventually, but not immediately
C) Data will be consistent within 1 second
D) Only the controller needs to be updated

## Question 6
What is the mandatory configuration parameter when creating an AdminClient?
A) client.id
B) bootstrap.servers
C) request.timeout.ms
D) security.protocol

## Question 7
What happens when you call close() on an AdminClient without a timeout?
A) The client closes immediately
B) An exception is thrown
C) The client waits for all ongoing operations to complete
D) All operations are cancelled

## Question 8
What does the timeoutMs option control in AdminClient methods?
A) How long the broker waits to respond
B) How long the client waits for a response before throwing TimeoutException
C) Network socket timeout
D) Connection establishment timeout

## Question 9
Which brokers handle AdminClient operations that modify cluster state (create, delete, alter)?
A) Any available broker
B) The least-loaded broker
C) The controller
D) All brokers simultaneously

## Question 10
Which brokers handle AdminClient operations that read cluster state (list, describe)?
A) Only the controller
B) The least-loaded broker
C) The oldest broker in the cluster
D) Random broker selection

## Question 11
What method is used to create an AdminClient instance?
A) new AdminClient()
B) AdminClient.create(props)
C) AdminClient.newInstance(props)
D) AdminClientFactory.create(props)

## Question 12
What happens if you call AdminClient methods after calling close()?
A) Methods execute normally
B) You cannot call any other methods
C) Methods are queued for later execution
D) A warning is logged

## Question 13
What is the purpose of client.dns.lookup configuration?
A) To disable DNS resolution
B) To handle DNS aliases and multiple IP addresses
C) To cache DNS results
D) To specify custom DNS servers

## Question 14
When should you use client.dns.lookup=resolve_canonical_bootstrap_servers_only?
A) When using multiple data centers
B) When using DNS aliases with SASL authentication
C) When using SSL encryption
D) When brokers are behind NAT

## Question 15
When should you use client.dns.lookup=use_all_dns_ips?
A) When using a single broker
B) When brokers are behind load balancers with multiple IPs
C) When using Kerberos authentication
D) When running in containers

## Question 16
What is the default value for request.timeout.ms in AdminClient?
A) 30 seconds
B) 60 seconds
C) 120 seconds
D) 300 seconds

## Question 17
What method returns a list of all topics in the cluster?
A) admin.getTopics()
B) admin.listTopics()
C) admin.describeTopics()
D) admin.fetchTopics()

## Question 18
What does listTopics() return?
A) A List<String> of topic names
B) A Set<String> of topic names
C) A ListTopicsResult object wrapping Future collections
D) A Map<String, TopicDescription>

## Question 19
How do you wait for the listTopics() result to complete?
A) Call wait() on the result
B) Call get() on the Future
C) Call await() on the result
D) Call complete() on the result

## Question 20
What method describes specific topics with detailed information?
A) admin.getTopicDetails()
B) admin.describeTopics()
C) admin.topicInfo()
D) admin.inspectTopics()

## Question 21
What information does TopicDescription contain?
A) Only partition count
B) Partitions, leader, replicas, and in-sync replicas
C) Only topic configuration
D) Consumer group offsets

## Question 22
What exception is thrown when describing a topic that doesn't exist?
A) TopicNotFoundException
B) UnknownTopicOrPartitionException
C) NoSuchTopicException
D) InvalidTopicException

## Question 23
How do you create a new topic using AdminClient?
A) admin.createTopic()
B) admin.newTopic()
C) admin.createTopics()
D) admin.addTopic()

## Question 24
What object represents a new topic to be created?
A) Topic
B) NewTopic
C) TopicConfiguration
D) TopicDefinition

## Question 25
When creating a topic, what happens if you don't specify partition count?
A) The topic creation fails
B) Defaults to 1 partition
C) Broker defaults are used
D) Random partition count is assigned

## Question 26
What method deletes topics?
A) admin.deleteTopic()
B) admin.removeTopics()
C) admin.deleteTopics()
D) admin.dropTopics()

## Question 27
What happens to data when a topic is deleted?
A) Data is moved to a recycle bin
B) Data is permanently lost with no recovery option
C) Data is archived for 30 days
D) Data can be recovered within 24 hours

## Question 28
How can you execute AdminClient operations without blocking?
A) Use async() method
B) Use whenComplete() on the Future
C) Use execute() with callback
D) Set blocking=false in options

## Question 29
What method describes topic configuration?
A) admin.getConfig()
B) admin.describeConfigs()
C) admin.listConfigs()
D) admin.topicConfig()

## Question 30
What object represents a resource whose configuration you want to describe?
A) Resource
B) ConfigResource
C) Configuration
D) ResourceConfig

## Question 31
What types of ConfigResource are available?
A) Only TOPIC
B) TOPIC and BROKER
C) TOPIC, BROKER, and BROKER_LOGGER
D) TOPIC, BROKER, CONSUMER, and PRODUCER

## Question 32
How can you identify non-default configurations?
A) Check the source field
B) Use isDefault() method
C) Compare with documentation
D) Check the modified timestamp

## Question 33
What method modifies topic or broker configuration?
A) admin.alterConfigs()
B) admin.updateConfigs()
C) admin.incrementalAlterConfigs()
D) Both A and C

## Question 34
What are the AlterConfigOp operation types?
A) SET and DELETE only
B) SET, DELETE, APPEND, SUBTRACT
C) ADD, REMOVE, UPDATE
D) CREATE, UPDATE, DELETE

## Question 35
When would you use APPEND operation type?
A) For any configuration change
B) For configurations with List type
C) For string configurations
D) For integer configurations

## Question 36
What method lists all consumer groups?
A) admin.getConsumerGroups()
B) admin.listConsumerGroups()
C) admin.describeGroups()
D) admin.fetchGroups()

## Question 37
What does the valid() method do on listConsumerGroups() result?
A) Validates group configurations
B) Returns only groups without errors
C) Filters active groups
D) Checks group permissions

## Question 38
What method provides detailed information about consumer groups?
A) admin.getGroupDetails()
B) admin.describeConsumerGroups()
C) admin.inspectGroups()
D) admin.groupInfo()

## Question 39
What information is included in ConsumerGroupDescription?
A) Only member count
B) Members, hosts, partitions, assignment algorithm, coordinator
C) Only partition assignments
D) Only consumer lag

## Question 40
What method retrieves committed offsets for a consumer group?
A) admin.getOffsets()
B) admin.listConsumerGroupOffsets()
C) admin.describeOffsets()
D) admin.fetchGroupOffsets()

## Question 41
How many consumer groups can listConsumerGroupOffsets() accept at once?
A) Unlimited
B) One consumer group only
C) Up to 10 groups
D) Up to 100 groups

## Question 42
What does OffsetSpec.latest() return?
A) The most recent committed offset
B) The offset of the last message in the partition
C) The current consumer position
D) The earliest available offset

## Question 43
What does OffsetSpec.forTimestamp() do?
A) Returns the offset for exact timestamp match
B) Returns offset of record written on or after specified timestamp
C) Returns timestamp of specific offset
D) Converts offset to timestamp

## Question 44
What method modifies committed offsets for a consumer group?
A) admin.updateOffsets()
B) admin.setOffsets()
C) admin.alterConsumerGroupOffsets()
D) admin.commitOffsets()

## Question 45
When can you modify consumer group offsets?
A) Anytime
B) Only when consumer group is active
C) Only when consumer group is inactive
D) Only during maintenance windows

## Question 46
What exception is thrown when trying to modify offsets for an active group?
A) GroupActiveException
B) UnknownMemberIdException
C) IllegalStateException
D) OffsetModificationException

## Question 47
What should you consider before resetting consumer group offsets to beginning?
A) Available disk space
B) Impact on stored state in stream applications
C) Network bandwidth
D) Broker memory

## Question 48
What method retrieves cluster metadata?
A) admin.getCluster()
B) admin.describeCluster()
C) admin.clusterInfo()
D) admin.listCluster()

## Question 49
What information does describeCluster() return?
A) Only broker count
B) Cluster ID, brokers, and controller
C) Only topic count
D) Only partition distribution

## Question 50
What method adds partitions to a topic?
A) admin.addPartitions()
B) admin.expandTopic()
C) admin.createPartitions()
D) admin.increasePartitions()

## Question 51
When specifying partition count in createPartitions(), what number do you provide?
A) Number of partitions to add
B) Total number of partitions after expansion
C) Percentage increase
D) New partition IDs

## Question 52
What is a risk of adding partitions to a topic with keyed messages?
A) Data loss
B) Messages with same key may go to different partitions
C) Performance degradation
D) Increased latency

## Question 53
What method deletes records from a topic?
A) admin.removeRecords()
B) admin.purgeRecords()
C) admin.deleteRecords()
D) admin.truncate()

## Question 54
What does deleteRecords() actually do?
A) Physically deletes records from disk
B) Marks records as deleted and makes them inaccessible
C) Archives records
D) Compresses records

## Question 55
What are the two types of leader election?
A) Automatic and Manual
B) Preferred and Unclean
C) Primary and Secondary
D) Fast and Slow

## Question 56
What is a preferred leader?
A) The broker with most resources
B) A designated replica that should be leader for balanced distribution
C) The first broker in the cluster
D) The broker closest to producers

## Question 57
What is the consequence of unclean leader election?
A) Slower performance
B) Data loss
C) Increased network traffic
D) Higher CPU usage

## Question 58
What method triggers leader election?
A) admin.electLeader()
B) admin.rebalanceLeaders()
C) admin.electLeaders()
D) admin.triggerElection()

## Question 59
What method reassigns partition replicas?
A) admin.moveReplicas()
B) admin.reassignPartitions()
C) admin.alterPartitionReassignments()
D) admin.relocatePartitions()

## Question 60
What class is available for testing AdminClient operations without a real cluster?
A) TestAdminClient
B) MockAdminClient
C) FakeAdminClient
D) AdminClientSimulator

---

**End of Test**

[Link to Solutions](../../chapter-tests-solutions/chapter-05-solutions.md)