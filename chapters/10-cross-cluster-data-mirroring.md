# Chapter 10: Cross-Cluster Data Mirroring

## Table of Contents

1. [Use Cases of Cross-Cluster Mirroring](#use-cases-of-cross-cluster-mirroring)
2. [Multicluster Architectures](#multicluster-architectures)
   - [Some Realities of Cross-Datacenter Communication](#some-realities-of-cross-datacenter-communication)
   - [Hub-and-Spoke Architecture](#hub-and-spoke-architecture)
   - [Active-Active Architecture](#active-active-architecture)
   - [Active-Standby Architecture](#active-standby-architecture)
   - [Stretch Clusters](#stretch-clusters)
3. [Apache Kafka's MirrorMaker](#apache-kafkas-mirrormaker)
   - [Configuring MirrorMaker](#configuring-mirrormaker)
   - [Multicluster Replication Topology](#multicluster-replication-topology)
   - [Securing MirrorMaker](#securing-mirrormaker)
   - [Deploying MirrorMaker in Production](#deploying-mirrormaker-in-production)
   - [Tuning MirrorMaker](#tuning-mirrormaker)
4. [Other Cross-Cluster Mirroring Solutions](#other-cross-cluster-mirroring-solutions)
   - [Uber uReplicator](#uber-ureplicator)
   - [LinkedIn Brooklin](#linkedin-brooklin)
   - [Confluent Cross-Datacenter Mirroring Solutions](#confluent-cross-datacenter-mirroring-solutions)
5. [Summary](#summary)

----

## Introduction

For most of the book we discuss the setup, maintenance, and use of a single Kafka cluster. There are, however, a few scenarios in which an architecture may need more than one cluster.

In some cases, the clusters are completely separated. They belong to different departments or different use cases, and there is no reason to copy data from one cluster to another. Sometimes, different SLAs or workloads make it difficult to tune a single cluster to serve multiple use cases. Other times, there are different security requirements. Those use cases are fairly easy—managing multiple distinct clusters is the same as running a single cluster multiple times.

In other use cases, the different clusters are interdependent, and the administrators need to continuously copy data between the clusters. In most databases, continuously copying data between database servers is called **replication**. Since we've used replication to describe movement of data between Kafka nodes that are part of the same cluster, we'll call copying of data between Kafka clusters **mirroring**. Apache Kafka's built-in cross-cluster replicator is called MirrorMaker.

In this chapter, we will discuss cross-cluster mirroring of all or part of the data. We'll start by discussing some of the common use cases for cross-cluster mirroring. Then we'll show a few architectures that are used to implement these use cases and discuss the pros and cons of each architecture pattern. We'll then discuss MirrorMaker itself and how to use it. We'll share operational tips, including deployment and performance tuning. We'll finish by discussing a few alternatives to MirrorMaker.

## Use Cases of Cross-Cluster Mirroring

The following is a list of examples of when cross-cluster mirroring would be used:

**Regional and central clusters:** In some cases, the company has one or more datacenters in different geographical regions, cities, or continents. Each datacenter has its own Kafka cluster. Some applications can work just by communicating with the local cluster, but some applications require data from multiple datacenters. The classic example is a company that modifies prices based on supply and demand. This company can have a datacenter in each city, collects information about local supply and demand, and adjusts prices accordingly. All this information will then be mirrored to a central cluster where business analysts can run company-wide reports.

**High availability (HA) and disaster recovery (DR):** The applications run on just one Kafka cluster and don't need data from other locations, but you are concerned about the possibility of the entire cluster becoming unavailable for some reason. For redundancy, you'd like to have a second Kafka cluster with all the data that exists in the first cluster, so in case of emergency you can direct your applications to the second cluster and continue as usual.

**Regulatory compliance:** Companies operating in different countries may need to use different configurations and policies to conform to legal and regulatory requirements in each country. Datasets may be stored in separate clusters with strict access control, with subsets of data replicated to other clusters with wider access.

**Cloud migrations:** Many companies run their business in both an on-premises datacenter and a cloud provider. Those Kafka clusters are used by applications in each datacenter and region to transfer data efficiently between the datacenters.

**Aggregation of data from edge clusters:** Several industries generate data from small devices with limited connectivity. An aggregate cluster with high availability can be used to support analytics and other use cases for data from a large number of edge clusters.

## Multicluster Architectures

Now that we've seen a few use cases that require multiple Kafka clusters, let's look at some common architectural patterns that we've successfully used when implementing these use cases.

### Some Realities of Cross-Datacenter Communication

The following is a list of some things to consider when it comes to cross-datacenter communication:

**High latencies:** Latency of communication between two Kafka clusters increases as the distance and the number of network hops between the two clusters increase.

**Limited bandwidth:** Wide area networks (WANs) typically have far lower available bandwidth than what you'll see inside a single datacenter, and the available bandwidth can vary from minute to minute.

**Higher costs:** Regardless of whether you are running Kafka on premise or in the cloud, there are higher costs to communicate between clusters.

Apache Kafka's brokers and clients were designed, developed, tested, and tuned, all within a single datacenter. For this reason, it is not recommended to install some Kafka brokers in one datacenter and others in another datacenter.

The following principles will guide most of the architectures we'll discuss:

- No less than one cluster per datacenter
- Replicate each event exactly once between each pair of datacenters
- When possible, consume from a remote datacenter rather than produce to a remote datacenter

### Hub-and-Spoke Architecture

This architecture is intended for the case where there are multiple local Kafka clusters and one central Kafka cluster. This architecture is used when data is produced in multiple datacenters and some consumers need access to the entire dataset.

The main benefit of this architecture is that data is always produced to the local datacenter and events from each datacenter are only mirrored once—to the central datacenter. Applications that process data from a single datacenter can be located at that datacenter. Applications that need to process data from multiple datacenters will be located at the central datacenter.

The main drawback of this architecture is that processors in one regional datacenter can't access data in another.

### Active-Active Architecture

This architecture is used when two or more datacenters share some or all of the data, and each datacenter is able to both produce and consume events.

The main benefit of this architecture is the ability to serve users from a nearby datacenter, which typically has performance benefits, without sacrificing functionality due to limited availability of data. A secondary benefit is redundancy and resilience.

The main drawback of this architecture is the challenge in avoiding conflicts when data is read and updated asynchronously in multiple locations.

### Active-Standby Architecture

In some cases, the only requirement for multiple clusters is to support some kind of disaster scenario. You use one cluster for all the applications, but you want a second cluster that contains almost all the events in the original cluster that you can use if the original cluster is completely unavailable.

The benefits of this setup are simplicity in setup and the fact that it can be used in pretty much any use case. The disadvantages are waste of a good cluster and the fact that failover between Kafka clusters is much harder than it looks. The bottom line is that it is currently not possible to perform cluster failover in Kafka without either losing data or having duplicate events.

**Disaster recovery planning:** When planning for disaster recovery, it is important to consider two key metrics. **Recovery time objective (RTO)** defines the maximum amount of time before all services must resume after a disaster. **Recovery point objective (RPO)** defines the maximum amount of time for which data may be lost as a result of a disaster.

**Data loss and inconsistencies in unplanned failover:** Because Kafka's various mirroring solutions are all asynchronous, the DR cluster will not have the latest messages from the primary cluster. In planned failover, you can stop the primary cluster and wait for the mirroring process to mirror the remaining messages before failing over applications to the DR cluster.

**Start offset for applications after failover:** One of the challenging tasks in failing over to another cluster is making sure applications know where to start consuming data. Several common approaches include auto offset reset, replicate offsets topic, time-based failover, and offset translation.

### Stretch Clusters

Stretch clusters are intended to protect the Kafka cluster from failure during a datacenter outage. This is achieved by installing a single Kafka cluster across multiple datacenters. Stretch clusters are fundamentally different from other multidatacenter scenarios—it is just one cluster.

The advantages of this architecture are in the synchronous replication and that both datacenters and all brokers in the cluster are used. This architecture is limited in the type of disasters it protects against. It only protects from datacenter failures, not any kind of application or Kafka failures.

This architecture is feasible if you can install Kafka in at least three datacenters with high bandwidth and low latency between them. With three datacenters, you can easily allocate nodes so no single datacenter has a majority.

## Apache Kafka's MirrorMaker

Apache Kafka contains a tool called MirrorMaker for mirroring data between two datacenters. MirrorMaker 2.0 is the next-generation multicluster mirroring solution for Apache Kafka that is based on the Kafka Connect framework.

MirrorMaker uses a source connector to consume data from another Kafka cluster. The Connect framework assigns those tasks to different Connect worker nodes as needed. Connect also has a REST API to centrally manage the configuration for the connectors and tasks.

MirrorMaker allocates partitions to tasks evenly without using Kafka's consumer group-management protocol to avoid latency spikes. Events from each partition in the source cluster are mirrored to the same partition in the target cluster, preserving semantic partitioning and maintaining ordering of events for each partition.

### Configuring MirrorMaker

MirrorMaker is highly configurable. In addition to the cluster settings to define the topology, Kafka Connect, and connector settings, every configuration property of the underlying producer, consumers, and admin client used by MirrorMaker can be customized.

Let's look at some of MirrorMaker's configuration options:

**Replication flow:** The following example shows the configuration options for setting up an active-standby replication flow between two datacenters:

```
clusters = NYC, LON
NYC.bootstrap.servers = kafka.nyc.example.com:9092
LON.bootstrap.servers = kafka.lon.example.com:9092
NYC->LON.enabled = true
NYC->LON.topics = .*
```

**Mirror topics:** For each replication flow, a regular expression may be specified for the topic names that will be mirrored. A separate topic exclusion list may also be specified. Target topic names are automatically prefixed with the source cluster alias by default.

**Consumer offset migration:** Support for periodic migration of consumer offsets was added in 2.7.0 to automatically commit translated offsets to the target `__consumer_offsets` topic.

**Topic configuration and ACL migration:** MirrorMaker may be configured to mirror topic configuration and access control lists (ACLs) of the topics.

### Multicluster Replication Topology

Active-active topology between New York and London can be configured by enabling replication flow in both directions. MirrorMaker ensures that the same event isn't constantly mirrored back and forth between the pair of clusters since remote topics use the cluster alias as the prefix.

### Securing MirrorMaker

For production clusters, it is important to ensure that all cross-datacenter traffic is secure. MirrorMaker must be configured to use a secure broker listener in both source and target clusters, and client-side security options for each cluster must be configured. SSL should be used to encrypt all cross-datacenter traffic.

### Deploying MirrorMaker in Production

You can start MirrorMaker processes to form a dedicated MirrorMaker cluster that is scalable and fault-tolerant. MirrorMaker is completely stateless and doesn't require any disk storage. For production use, we recommend running MirrorMaker in distributed mode either as a dedicated MirrorMaker cluster or in a shared distributed Connect cluster.

If at all possible, run MirrorMaker at the target datacenter. The reason for this is that long-distance networks can be a bit less reliable than those inside a datacenter. If there is a network partition and you lose connectivity between the datacenters, having a consumer that is unable to connect to a cluster is much safer than a producer that can't connect.

When deploying MirrorMaker in production, it is important to monitor:
- Kafka Connect monitoring
- MirrorMaker metrics monitoring
- Lag monitoring
- Producer and consumer metrics monitoring
- Canary

### Tuning MirrorMaker

MirrorMaker is horizontally scalable. You will want to measure the throughput you get from MirrorMaker with a different number of connector tasks—configured with the `tasks.max` parameter. If you are running MirrorMaker across datacenters, tuning the TCP stack can help to increase the effective bandwidth.

## Other Cross-Cluster Mirroring Solutions

We looked in depth at MirrorMaker because this mirroring software arrives as part of Apache Kafka. However, MirrorMaker also has some limitations when used in practice. It is worthwhile to look at some of the alternatives to MirrorMaker and the ways they address MirrorMaker limitations and complexities.

### Uber uReplicator

Uber ran legacy MirrorMaker at very large scale, and as the number of topics and partitions grew and the cluster throughput increased, it started running into several problems. Given these issues, Uber decided to write its own MirrorMaker clone, called uReplicator. Uber decided to use Apache Helix as a central controller to manage the topic list and the partitions assigned to each uReplicator instance.

### LinkedIn Brooklin

Like Uber, LinkedIn was also using legacy MirrorMaker for transferring data between Kafka clusters. So LinkedIn built a mirroring solution on top of its data streaming system called Brooklin. Brooklin is a distributed service that can stream data between different heterogeneous data source and target systems, including Kafka.

Brooklin is a scalable distributed system designed for high reliability and has been tested with Kafka at scale. It is used to mirror trillions of messages a day and has been optimized for stability, performance, and operability.

### Confluent Cross-Datacenter Mirroring Solutions

Confluent independently developed several mirroring solutions:

**Confluent Replicator:** A mirroring tool similar to MirrorMaker that relies on the Kafka Connect framework for cluster management. Both support data replication for different topologies as well as migration of consumer offsets and topic configuration.

**Multi-Region Clusters (MRC):** Suitable for datacenters within a 50 ms latency, using a combination of synchronous and asynchronous replication to limit impact on producer performance and provide higher network tolerance.

**Cluster Linking:** Introduced in Confluent Platform 6.0, builds inter-cluster replication directly into the Confluent Server. By using the same protocol as inter-broker replication, Cluster Linking performs offset-preserving replication across clusters.

## Summary

We started the chapter by describing the reasons you may need to manage more than a single Kafka cluster and then proceeded to describe several common multicluster architectures, ranging from the simple to the very complex. We went into the details of implementing failover architecture for Kafka and compared the different options currently available. Then we proceeded to discuss the available tools. Starting with Apache Kafka's MirrorMaker, we went into many details of using it in production. We finished by reviewing alternative options that solve some of the issues you might encounter with MirrorMaker.

Whichever architecture and tools you end up using, remember that multicluster configuration and mirroring pipelines should be monitored and tested just like everything else you take into production.

----

## External Resources and Links

This chapter referenced the following external resources:

- [Confluent Control Center](https://oreil.ly/KnvVV) - Commercial tool for monitoring message counts and checksums
- [Kafka Monitoring Documentation](http://bit.ly/2sMfZWf) - Lists all available Kafka metrics
- [Uber uReplicator Blog Post](https://oreil.ly/SGItx) - Uber engineering blog describing uReplicator architecture
- [Apache Helix](https://helix.apache.org/) - Controller system used by Uber uReplicator

----

*This chapter is part of "Kafka: The Definitive Guide, 2nd Edition" by Gwen Shapira, Todd Palino, Rajini Sivaram, and Krit Petty, published by O'Reilly Media, Inc.*