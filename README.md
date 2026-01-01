# Kafka: The Definitive Guide, 2nd Edition
 
## Complete Markdown Version with All Chapters, Figures, and Hyperlinks

**Authors:** Gwen Shapira, Todd Palino, Rajini Sivaram, Krit Petty  
**Published by:** O'Reilly Media, Inc.  
**Source:** [O'Reilly Learning Platform](https://learning.oreilly.com/library/view/kafka-the-definitive/9781492043072/)

---

## 📖 Table of Contents

### Frontmatter
- [Foreword To The Second Edition](./chapters/foreword-second-edition.md)
- [Foreword To The First Edition](./chapters/foreword-first-edition.md)
- [Preface](./chapters/preface.md)

### Main Chapters

1. **[Chapter 1: Meet Kafka](./chapters/01-meet-kafka.md)**
    1. [Publish/Subscribe Messaging](./chapters/01-meet-kafka.md#publishsubscribe-messaging)
    2. [Enter Kafka](./chapters/01-meet-kafka.md#enter-kafka)
    3. [Why Kafka?](./chapters/01-meet-kafka.md#why-kafka)
    4. [The Data Ecosystem](./chapters/01-meet-kafka.md#the-data-ecosystem)
    5. [Kafka's Origin](./chapters/01-meet-kafka.md#kafkas-origin)
    6. [Getting Started with Kafka](./chapters/01-meet-kafka.md#getting-started-with-kafka)

2. **[Chapter 2: Installing Kafka](./chapters/02-installing-kafka.md)**
    1. [Environment Setup](./chapters/02-installing-kafka.md#environment-setup)
        - [Choosing an Operating System](./chapters/02-installing-kafka.md#choosing-an-operating-system)
        - [Installing Java](./chapters/02-installing-kafka.md#installing-java)
        - [Installing ZooKeeper](./chapters/02-installing-kafka.md#installing-zookeeper)
    2. [Installing a Kafka Broker](./chapters/02-installing-kafka.md#installing-a-kafka-broker)
    3. [Configuring the Broker](./chapters/02-installing-kafka.md#configuring-the-broker)
    4. [Selecting Hardware](./chapters/02-installing-kafka.md#selecting-hardware)
    5. [Kafka in the Cloud](./chapters/02-installing-kafka.md#kafka-in-the-cloud)
    6. [Configuring Kafka Clusters](./chapters/02-installing-kafka.md#configuring-kafka-clusters)
    7. [Production Concerns](./chapters/02-installing-kafka.md#production-concerns)

3. **[Chapter 3: Kafka Producers - Writing Messages To Kafka](./chapters/03-kafka-producers.md)**
    1. [Producer Overview](./chapters/03-kafka-producers.md#producer-overview)
    2. [Constructing a Kafka Producer](./chapters/03-kafka-producers.md#constructing-a-kafka-producer)
    3. [Sending a Message to Kafka](./chapters/03-kafka-producers.md#sending-a-message-to-kafka)
    4. [Configuring Producers](./chapters/03-kafka-producers.md#configuring-producers)
    5. [Serializers](./chapters/03-kafka-producers.md#serializers)
    6. [Partitions](./chapters/03-kafka-producers.md#partitions)
    7. [Headers](./chapters/03-kafka-producers.md#headers)
    8. [Interceptors](./chapters/03-kafka-producers.md#interceptors)
    9. [Quotas and Throttling](./chapters/03-kafka-producers.md#quotas-and-throttling)
    10. [Summary](./chapters/03-kafka-producers.md#summary)

4. **[Chapter 4: Kafka Consumers - Reading Data From Kafka](./chapters/04-kafka-consumers.md)**
    - [Kafka Consumer Concepts](./chapters/04-kafka-consumers.md#kafka-consumer-concepts)
    - [Consumers and Consumer Groups](./chapters/04-kafka-consumers.md#consumers-and-consumer-groups)
    - [Consumer Groups and Partition Rebalance](./chapters/04-kafka-consumers.md#consumer-groups-and-partition-rebalance)
    - [Static Group Membership](./chapters/04-kafka-consumers.md#static-group-membership)
    - [Creating a Kafka Consumer](./chapters/04-kafka-consumers.md#creating-a-kafka-consumer)
    - [Subscribing to Topics](./chapters/04-kafka-consumers.md#subscribing-to-topics)
    - [The Poll Loop](./chapters/04-kafka-consumers.md#the-poll-loop)
    - [Thread Safety](./chapters/04-kafka-consumers.md#thread-safety)
    - [Configuring Consumers](./chapters/04-kafka-consumers.md#configuring-consumers)
    - [Commits and Offsets](./chapters/04-kafka-consumers.md#commits-and-offsets)
    - [Automatic Commit](./chapters/04-kafka-consumers.md#automatic-commit)
    - [Commit Current Offset](./chapters/04-kafka-consumers.md#commit-current-offset)
    - [Asynchronous Commit](./chapters/04-kafka-consumers.md#asynchronous-commit)
    - [Combining Synchronous and Asynchronous Commits](./chapters/04-kafka-consumers.md#combining-synchronous-and-asynchronous-commits)
    - [Committing a Specified Offset](./chapters/04-kafka-consumers.md#committing-a-specified-offset)
    - [Rebalance Listeners](./chapters/04-kafka-consumers.md#rebalance-listeners)
    - [Consuming Records with Specific Offsets](./chapters/04-kafka-consumers.md#consuming-records-with-specific-offsets)
    - [But How Do We Exit?](./chapters/04-kafka-consumers.md#but-how-do-we-exit)
    - [Deserializers](./chapters/04-kafka-consumers.md#deserializers)
    - [Custom Deserializers](./chapters/04-kafka-consumers.md#custom-deserializers)
    - [Using Avro Deserialization with Kafka Consumer](./chapters/04-kafka-consumers.md#using-avro-deserialization-with-kafka-consumer)
    - [Standalone Consumer: Why and How to Use a Consumer Without a Group](./chapters/04-kafka-consumers.md#standalone-consumer-why-and-how-to-use-a-consumer-without-a-group)
    - [Summary](./chapters/04-kafka-consumers.md#summary)

5. **[Chapter 5: Managing Apache Kafka Programmatically](./chapters/05-managing-kafka.md)**
    - [AdminClient Overview](./chapters/05-managing-kafka.md#adminclient-overview)
        - [Asynchronous and Eventually Consistent API](./chapters/05-managing-kafka.md#asynchronous-and-eventually-consistent-api)
        - [Options](./chapters/05-managing-kafka.md#options)
        - [Flat Hierarchy](./chapters/05-managing-kafka.md#flat-hierarchy)
    - [Additional Notes](./chapters/05-managing-kafka.md#additional-notes)
    - [AdminClient Lifecycle: Creating, Configuring, and Closing](./chapters/05-managing-kafka.md#adminclient-lifecycle-creating-configuring-and-closing)
    - [Essential Topic Management](./chapters/05-managing-kafka.md#essential-topic-management)
    - [Configuration Management](./chapters/05-managing-kafka.md#configuration-management)
    - [Consumer Group Management](./chapters/05-managing-kafka.md#consumer-group-management)
    - [Cluster Metadata](./chapters/05-managing-kafka.md#cluster-metadata)
    - [Advanced Admin Operations](./chapters/05-managing-kafka.md#advanced-admin-operations)
    - [Testing](./chapters/05-managing-kafka.md#testing)
    - [Summary](./chapters/05-managing-kafka.md#summary)

6. **[Chapter 6: Kafka Internals](./chapters/06-kafka-internals.md)**
    - [Kafka controller](#kafka-controller)
    - [Cluster Membership](#cluster-membership)
    - [The Controller](#the-controller)
        - [KRaft: Kafka’s New Raft-Based Controller](#kraft-kafkas-new-raft-based-controller)
    - [Replication](#replication)
    - [Request Processing](#request-processing)
        - [Produce Requests](#produce-requests)
        - [Fetch Requests](#fetch-requests)
        - [Other Requests](#other-requests)
    - [Physical Storage](#cluster-metadata)
        - [Tiered Storage](#tiered-storage)
        - [Partition Allocation](#partition-allocation)
        - [File Management](#file-management)
        - [File Format](#file-format)
        - [Indexes](#indexes)
        - [Compaction](#compaction)
        - [How Compaction Works](#how-compaction-works)
        - [Deleted Events](#deleted-events)
        - [When Are Topics Compacted?](#when-are-topics-compacted)
    - [Summary](#summary)

7. **[Chapter 7: Reliable Data Delivery](./chapters/07-reliable-data-delivery.md)**

8. **[Chapter 8: Exactly-Once Semantics](./chapters/08-exactly-once-semantics.md)**

9. **[Chapter 9: Building Data Pipelines](./chapters/09-building-data-pipelines.md)**
    1. [Introduction](./chapters/08-exactly-once-semantics.md#introduction)
    2. [Putting Data Integration in Context](./chapters/08-exactly-once-semantics.md#putting-data-integration-in-context)
    3. [Considerations When Building Data Pipelines](./chapters/08-exactly-once-semantics.md#considerations-when-building-data-pipelines)
        - [Timeliness](./chapters/08-exactly-once-semantics.md#timeliness)
        - [Reliability](#reliability)
        - [High and Varying Throughput](./chapters/08-exactly-once-semantics.md#high-and-varying-throughput)
        - [Data Formats](./chapters/08-exactly-once-semantics.md#data-formats)
        - [Transformations](./chapters/08-exactly-once-semantics.md#transformations)
        - [Security](./chapters/08-exactly-once-semantics.md#security)
        - [Failure Handling](./chapters/08-exactly-once-semantics.md#failure-handling)
        - [Coupling and Agility](./chapters/08-exactly-once-semantics.md#coupling-and-agility)
    4. [When to Use Kafka Connect Versus Producer and Consumer](./chapters/08-exactly-once-semantics.md#when-to-use-kafka-connect-versus-producer-and-consumer)
    5. [Kafka Connect](./chapters/08-exactly-once-semantics.md#kafka-connect)
        - [Running Kafka Connect](./chapters/08-exactly-once-semantics.md#running-kafka-connect)
        - [Connector Example: File Source and File Sink](./chapters/08-exactly-once-semantics.md#connector-example-file-source-and-file-sink)
        - [Connector Example: MySQL to Elasticsearch](./chapters/08-exactly-once-semantics.md#connector-example-mysql-to-elasticsearch)
        - [Single Message Transformations](./chapters/08-exactly-once-semantics.md#single-message-transformations)
        - [A Deeper Look at Kafka Connect](./chapters/08-exactly-once-semantics.md#a-deeper-look-at-kafka-connect)
    6. [Alternatives to Kafka Connect](./chapters/08-exactly-once-semantics.md#alternatives-to-kafka-connect)
        - [Ingest Frameworks for Other Datastores](./chapters/08-exactly-once-semantics.md#ingest-frameworks-for-other-datastores)
        - [GUI-Based ETL Tools](./chapters/08-exactly-once-semantics.md#gui-based-etl-tools)
        - [Stream Processing Frameworks](./chapters/08-exactly-once-semantics.md#stream-processing-frameworks)
    7. [Summary](./chapters/08-exactly-once-semantics.md#summary)

10. **[Chapter 10: Cross-Cluster Data Mirroring](./chapters/10-cross-cluster-mirroring.md)**
    1. [Use Cases of Cross-Cluster Mirroring](./chapters/10-cross-cluster-mirroring.md#use-cases-of-cross-cluster-mirroring)
    2. [Multicluster Architectures](./chapters/10-cross-cluster-mirroring.md#multicluster-architectures)
        - [Some Realities of Cross-Datacenter Communication](./chapters/10-cross-cluster-mirroring.md#some-realities-of-cross-datacenter-communication)
        - [Hub-and-Spoke Architecture](./chapters/10-cross-cluster-mirroring.md#hub-and-spoke-architecture)
        - [Active-Active Architecture](./chapters/10-cross-cluster-mirroring.md#active-active-architecture)
        - [Active-Standby Architecture](./chapters/10-cross-cluster-mirroring.md#active-standby-architecture)
        - [Stretch Clusters](./chapters/10-cross-cluster-mirroring.md#stretch-clusters)
    3. [Apache Kafka's MirrorMaker](./chapters/10-cross-cluster-mirroring.md#apache-kafkas-mirrormaker)
        - [Configuring MirrorMaker](./chapters/10-cross-cluster-mirroring.md#configuring-mirrormaker)
        - [Multicluster Replication Topology](./chapters/10-cross-cluster-mirroring.md#multicluster-replication-topology)
        - [Securing MirrorMaker](./chapters/10-cross-cluster-mirroring.md#securing-mirrormaker)
        - [Deploying MirrorMaker in Production](./chapters/10-cross-cluster-mirroring.md#deploying-mirrormaker-in-production)
        - [Tuning MirrorMaker](./chapters/10-cross-cluster-mirroring.md#tuning-mirrormaker)
    4. [Other Cross-Cluster Mirroring Solutions](./chapters/10-cross-cluster-mirroring.md#other-cross-cluster-mirroring-solutions)
        - [Uber uReplicator](./chapters/10-cross-cluster-mirroring.md#uber-ureplicator)
        - [LinkedIn Brooklin](./chapters/10-cross-cluster-mirroring.md#linkedin-brooklin)
        - [Confluent Cross-Datacenter Mirroring Solutions](./chapters/10-cross-cluster-mirroring.md#confluent-cross-datacenter-mirroring-solutions)
    5. [Summary](./chapters/10-cross-cluster-mirroring.md#summary)

11. **[Chapter 11: Securing Kafka](./chapters/11-securing-kafka.md)**
    1. [Locking Down Kafka](./chapters/11-securing-kafka.md#locking-down-kafka)
    2. [Security Protocols](./chapters/11-securing-kafka.md#security-protocols)
        - [TLS/SSL](./chapters/11-securing-kafka.md#tlsssl)
    3. [Authentication](./chapters/11-securing-kafka.md#authentication)
        - [SSL](./chapters/11-securing-kafka.md#ssl)
        - [SASL](./chapters/11-securing-kafka.md#sasl)
        - [Delegation Tokens](./chapters/11-securing-kafka.md#delegation-tokens)
        - [Reauthentication](./chapters/11-securing-kafka.md#reauthentication)
        - [Security Updates Without Downtime](./chapters/11-securing-kafka.md#security-updates-without-downtime)
    4. [Encryption](./chapters/11-securing-kafka.md#encryption)
        - [End-to-End Encryption](./chapters/11-securing-kafka.md#end-to-end-encryption)
    5. [Authorization](./chapters/11-securing-kafka.md#authorization)
        - [AclAuthorizer](./chapters/11-securing-kafka.md#aclauthorizer)
        - [Customizing Authorization](./chapters/11-securing-kafka.md#customizing-authorization)
    6. [Auditing](./chapters/11-securing-kafka.md#auditing)
    7. [Securing ZooKeeper](./chapters/11-securing-kafka.md#securing-zookeeper)
        - [SASL](./chapters/11-securing-kafka.md#sasl-1)
        - [SSL](./chapters/11-securing-kafka.md#ssl-1)
        - [Authorization](./chapters/11-securing-kafka.md#authorization-1)
    8. [Securing the Platform](./chapters/11-securing-kafka.md#securing-the-platform)
        - [Password Protection](./chapters/11-securing-kafka.md#password-protection)
    9. [Summary](./chapters/11-securing-kafka.md#summary)

12. **[Chapter 12: Administering Kafka](./chapters/12-administering-kafka.md)**
    - [Topic Operations](./chapters/12-administering-kafka.md#topic-operations)
        - [Creating a New Topic](./chapters/12-administering-kafka.md#creating-a-new-topic)
        - [Listing All Topics in a Cluster](./chapters/12-administering-kafka.md#listing-all-topics-in-a-cluster)
        - [Describing Topic Details](./chapters/12-administering-kafka.md#describing-topic-details)
        - [Adding Partitions](./chapters/12-administering-kafka.md#adding-partitions)
        - [Reducing Partitions](./chapters/12-administering-kafka.md#reducing-partitions)
        - [Deleting a Topic]./chapters/12-administering-kafka.md#deleting-a-topic)
    - [Consumer Groups](./chapters/12-administering-kafka.md#consumer-groups)
        - [List and Describe Groups](./chapters/12-administering-kafka.md#list-and-describe-groups)
        - [Delete Group](./chapters/12-administering-kafka.md#delete-group)
        - [Offset Management](./chapters/12-administering-kafka.md#offset-management)
    - [Dynamic Configuration Changes](./chapters/12-administering-kafka.md#dynamic-configuration-changes)
        - [Overriding Topic Configuration Defaults](./chapters/12-administering-kafka.md#overriding-topic-configuration-defaults)
        - [Overriding Client and User Configuration Defaults](./chapters/12-administering-kafka.md#overriding-client-and-user-configuration-defaults)
        - [Overriding Broker Configuration Defaults](./chapters/12-administering-kafka.md#overriding-broker-configuration-defaults)
        - [Describing Configuration Overrides](./chapters/12-administering-kafka.md#describing-configuration-overrides)
        - [Removing Configuration Overrides](./chapters/12-administering-kafka.md#removing-configuration-overrides)
    - [Producing and Consuming](./chapters/12-administering-kafka.md#producing-and-consuming)
        - [Console Producer](./chapters/12-administering-kafka.md#console-producer)
        - [Console Consumer](./chapters/12-administering-kafka.md#console-consumer)
    - [Partition Management](./chapters/12-administering-kafka.md#partition-management)
        - [Preferred Replica Election](./chapters/12-administering-kafka.md#preferred-replica-election)
        - [Changing a Partition's Replicas](./chapters/12-administering-kafka.md#changing-a-partitions-replicas)
        - [Dumping Log Segments](./chapters/12-administering-kafka.md#dumping-log-segments)
        - [Replica Verification](./chapters/12-administering-kafka.md#replica-verification)
    - [Other Tools](./chapters/12-administering-kafka.md#other-tools)
    - [Unsafe Operations](./chapters/12-administering-kafka.md#unsafe-operations)
        - [Moving the Cluster Controller](./chapters/12-administering-kafka.md#moving-the-cluster-controller)
        - [Removing Topics to Be Deleted](./chapters/12-administering-kafka.md#removing-topics-to-be-deleted)
        - [Deleting Topics Manually](./chapters/12-administering-kafka.md#deleting-topics-manually)
    - [Summary](./chapters/12-administering-kafka.md#summary)

13. **[Chapter 13: Monitoring Kafka](./chapters/13-monitoring-kafka.md)**
    - [Metric Basics](./chapters/13-monitoring-kafka.md#metric-basics)
        - [Where Are the Metrics?](./chapters/13-monitoring-kafka.md#where-are-the-metrics)
        - [What Metrics Do I Need?](./chapters/13-monitoring-kafka.md#what-metrics-do-i-need)
        - [Application Health Checks](./chapters/13-monitoring-kafka.md#application-health-checks)
    - [Service-Level Objectives](./chapters/13-monitoring-kafka.md#service-level-objectives)
        - [Service-Level Definitions](./chapters/13-monitoring-kafka.md#service-level-definitions)
        - [What Metrics Make Good SLIs?](./chapters/13-monitoring-kafka.md#what-metrics-make-good-slis)
        - [Using SLOs in Alerting](./chapters/13-monitoring-kafka.md#using-slos-in-alerting)
    - [Kafka Broker Metrics](./chapters/13-monitoring-kafka.md#kafka-broker-metrics)
        - [Diagnosing Cluster Problems](./chapters/13-monitoring-kafka.md#diagnosing-cluster-problems)
        - [The Art of Under-Replicated Partitions](./chapters/13-monitoring-kafka.md#the-art-of-under-replicated-partitions)
        - [Broker Metrics](./chapters/13-monitoring-kafka.md#broker-metrics)
        - [Topic and Partition Metrics](./chapters/13-monitoring-kafka.md#topic-and-partition-metrics)
        - [JVM Monitoring](./chapters/13-monitoring-kafka.md#jvm-monitoring)
        - [OS Monitoring](./chapters/13-monitoring-kafka.md#os-monitoring)
        - [Logging](./chapters/13-monitoring-kafka.md#logging)
    - [Client Monitoring](./chapters/13-monitoring-kafka.md#client-monitoring)
        - [Producer Metrics](./chapters/13-monitoring-kafka.md#producer-metrics)
        - [Consumer Metrics](./chapters/13-monitoring-kafka.md#consumer-metrics)
        - [Quotas](./chapters/13-monitoring-kafka.md#quotas)
    - [Lag Monitoring](./chapters/13-monitoring-kafka.md#lag-monitoring)
    - [End-to-End Monitoring](./chapters/13-monitoring-kafka.md#end-to-end-monitoring)
    - [Summary](./chapters/13-monitoring-kafka.md#summary)

14. **[Chapter 14: Stream Processing](./chapters/14-stream-processing.md)**
    - [What Is Stream Processing?](./chapters/14-stream-processing.md#what-is-stream-processing)
    - [Stream Processing Concepts](./chapters/14-stream-processing.md#stream-processing-concepts)
        - [Topology](./chapters/14-stream-processing.md#topology)
        - [Time](./chapters/14-stream-processing.md#time)
        - [State](./chapters/14-stream-processing.md#state)
        - [Stream-Table Duality](./chapters/14-stream-processing.md#stream-table-duality)
        - [Time Windows](./chapters/14-stream-processing.md#time-windows)
        - [Processing Guarantees](./chapters/14-stream-processing.md#processing-guarantees)
    - [Stream Processing Design Patterns](./chapters/14-stream-processing.md#stream-processing-design-patterns)
        - [Single-Event Processing](./chapters/14-stream-processing.md#single-event-processing)
        - [Processing with Local State](./chapters/14-stream-processing.md#processing-with-local-state)
        - [Multiphase Processing/Repartitioning](./chapters/14-stream-processing.md#multiphase-processing-repartitioning)
        - [Processing with External Lookup: Stream-Table Join](./chapters/14-stream-processing.md#processing-with-external-lookup-stream-table-join)
        - [Table-Table Join](./chapters/14-stream-processing.md#table-table-join)
        - [Streaming Join](./chapters/14-stream-processing.md#streaming-join)
        - [Out-of-Sequence Events](./chapters/14-stream-processing.md#out-of-sequence-events)
        - [Reprocessing](./chapters/14-stream-processing.md#reprocessing)
        - [Interactive Queries](./chapters/14-stream-processing.md#interactive-queries)
    - [Kafka Streams by Example](./chapters/14-stream-processing.md#kafka-streams-by-example)
        - [Word Count](./chapters/14-stream-processing.md#word-count)
        - [Stock Market Statistics](./chapters/14-stream-processing.md#stock-market-statistics)
        - [ClickStream Enrichment](./chapters/14-stream-processing.md#clickstream-enrichment)
    - [Kafka Streams: Architecture Overview](./chapters/14-stream-processing.md#kafka-streams-architecture-overview)
        - [Building a Topology](./chapters/14-stream-processing.md#building-a-topology)
        - [Optimizing a Topology](./chapters/14-stream-processing.md#optimizing-a-topology)
        - [Testing a Topology](./chapters/14-stream-processing.md#testing-a-topology)
        - [Scaling a Topology](./chapters/14-stream-processing.md#scaling-a-topology)
        - [Surviving Failures](./chapters/14-stream-processing.md#surviving-failures)
    - [Stream Processing Use Cases](./chapters/14-stream-processing.md#stream-processing-use-cases)
    - [How to Choose a Stream Processing Framework](./chapters/14-stream-processing.md#how-to-choose-a-stream-processing-framework)
    - [Summary](./chapters/14-stream-processing.md#summary)

### Appendices

- **[Appendix A: Installing Kafka On Other Operating Systems](./chapters/appendix-a-installing-kafka-other-os.md)**
- **[Appendix B: Additional Kafka Tools](./chapters/appendix-b-additional-kafka-tools.md)**
- **[Index](./chapters/index.md)**

---

## 🎯 Quick Links

- **Getting Started:** Start with [Chapter 1: Meet Kafka](./chapters/01-meet-kafka.md) to understand Kafka concepts
- **Setup Guide:** Jump to [Chapter 2: Installing Kafka](./chapters/02-installing-kafka.md) to install Kafka
- **Producer Development:** See [Chapter 3: Kafka Producers](./chapters/03-kafka-producers.md) for writing messages
- **Consumer Development:** See [Chapter 4: Kafka Consumers](./chapters/04-kafka-consumers.md) for reading messages
- **Production Deployment:** Read [Chapter 7: Reliable Data Delivery](./chapters/07-reliable-data-delivery.md)
- **Security:** Check [Chapter 11: Securing Kafka](./chapters/11-securing-kafka.md)
- **Monitoring:** See [Chapter 13: Monitoring Kafka](./chapters/13-monitoring-kafka.md)

---

## 📊 Features

- ✅ All 14 chapters in Markdown format
- ✅ All diagrams and figures included
- ✅ Internal hyperlinks between chapters
- ✅ Cross-references with page links
- ✅ Code examples and best practices
- ✅ Comprehensive index
- ✅ Easy navigation

---

## 📂 Repository Structure

```
kafka-definitive-guide/
├── README.md
├── chapters/
│   ├── 01-meet-kafka.md
│   ├── 02-installing-kafka.md
│   ├── 03-kafka-producers.md
│   ├── 04-kafka-consumers.md
│   ├── 05-managing-kafka.md
│   ├── 06-kafka-internals.md
│   ├── 07-reliable-data-delivery.md
│   ├── 08-exactly-once-semantics.md
│   ├── 09-building-data-pipelines.md
│   ├── 10-cross-cluster-mirroring.md
│   ├── 11-securing-kafka.md
│   ├── 12-administering-kafka.md
│   ├── 13-monitoring-kafka.md
│   ├── 14-stream-processing.md
│   ├── appendix-a-installing-other-os.md
│   ├── appendix-b-additional-tools.md
│   ├── foreword-first-edition.md
│   ├── foreword-second-edition.md
│   ├── index.md
│   └── preface.md
└── test/
│   ├── chapter-tests/
│   │   ├── chapter-01-test.md/
│   │   ├── chapter-02-test.md/
│   │   ├── ...
│   │   └── chapter-14-test.md/
│   └── chapter-tests-solutions/
│       ├── chapter-01-solutions.md/
│       ├── chapter-02-solutions.md/
│       ├── ...
│       └── chapter-14-solutions.md/
│ 
└── images/
    ├── ch01/
    ├── ch02/
    ├── ...
    └── ch14/

```

---

## 🔗 Cross-Chapter Links

Throughout the documentation, you'll find links to related chapters:
- When Chapter 3 mentions "As detailed in [Chapter 7](./chapters/07-reliable-data-delivery.md)..."
- Chapter references use relative links for easy navigation
- All figures are embedded with alt text for accessibility

---

## 📝 How to Use This Repository

1. **Start Here:** Begin with [README](./README.md) (this file)
2. **Beginner Path:** Read [Chapter 1](./chapters/01-meet-kafka.md) → [Chapter 2](./chapters/02-installing-kafka.md) → [Chapter 3](./chapters/03-kafka-producers.md)
3. **Deep Dive:** Follow chapters in order for comprehensive understanding
4. **Reference:** Use the index to find specific topics across all chapters
5. **Search:** Use GitHub's search function (press `/`) to find topics within the repository

---

## ℹ️ About This Version

This is a markdown adaptation of "Kafka: The Definitive Guide, 2nd Edition" for reference and educational purposes. All content has been converted to Markdown format with proper formatting, links, and image references.

**Note:** This repository is a study resource. For the official publication, visit [O'Reilly Media](https://www.oreilly.com/).

---

## 🤝 Contributing

If you find errors or have suggestions for improvements:
1. Open an Issue with details
2. Submit a Pull Request with corrections
3. Help improve documentation quality

---

## 📄 License

This content is derived from "Kafka: The Definitive Guide, 2nd Edition" published by O'Reilly Media. Please refer to the book's copyright and licensing information.

---

**Last Updated:** December 2025  
**Repository:** [github.com/reik2k/kafka-definitive-guide](https://github.com/reik2k/kafka-definitive-guide)


