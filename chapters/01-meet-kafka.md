# Chapter 1: Meet Kafka

**Back to [Table of Contents](../README.md)**

## Overview

Every enterprise is powered by data. We take information in, analyze it, manipulate it, and create more as output. Every application creates data, whether it is log messages, metrics, user activity, outgoing messages, or something else.

The faster we can move data, the more agile and responsive our organizations can be. The less effort we spend on moving data around, the more we can focus on the core business at hand. This is why the pipeline is a critical component in the data-driven enterprise. How we move the data becomes nearly as important as the data itself.

> "Any time scientists disagree, it's because we have insufficient data. Then we can agree on what kind of data to get; we get the data; and the data solves the problem. Either I'm right, or you're right, or we're both wrong. And we move on."
>
> — Neil deGrasse Tyson

---

## Table of Contents

1. [Publish/Subscribe Messaging](#publishsubscribe-messaging)
2. [Enter Kafka](#enter-kafka)
3. [Why Kafka?](#why-kafka)
4. [The Data Ecosystem](#the-data-ecosystem)
5. [Kafka's Origin](#kafkas-origin)
6. [Getting Started with Kafka](#getting-started-with-kafka)

---

## Publish/Subscribe Messaging

Before discussing the specifics of Apache Kafka, it is important for us to understand the concept of publish/subscribe messaging and why it is a critical component of data-driven applications.

**Publish/subscribe (pub/sub) messaging** is a pattern that is characterized by the sender (publisher) of a piece of data (message) not specifically directing it to a receiver. Instead, the publisher classifies the message somehow, and that receiver (subscriber) subscribes to receive certain classes of messages. Pub/sub systems often have a broker, a central point where messages are published, to facilitate this pattern.

### How It Starts

Many use cases for publish/subscribe start out the same way: with a simple message queue or interprocess communication channel.

**Figure 1-1: A single, direct metrics publisher**
![Figure 1-1](../images/ch01/figure-1-1-single-metrics-publisher.png)

For example, you create an application that needs to send monitoring information somewhere, so you open a direct connection from your application to an app that displays your metrics on a dashboard, and push metrics over that connection.

This is a simple solution to a simple problem that works when you are getting started with monitoring. Before long, you decide you would like to analyze your metrics over a longer term, and that doesn't work well in the dashboard. You start a new service that can receive metrics, store them, and analyze them. Over time, you have multiple applications publishing metrics to multiple destinations.

**Figure 1-2: Many metrics publishers, using direct connections**
![Figure 1-2](../images/ch01/figure-1-2-many-publishers-direct.png)

This architecture can become very complex, with many point-to-point connections that are hard to maintain.

### Individual Queue Systems

At the same time that you have been dealing with metrics, others in your organization have been building similar systems for logs and user activity tracking.

**Figure 1-4: Multiple publish/subscribe systems**
![Figure 1-4](../images/ch01/figure-1-4-multiple-pubsub.png)

Your company ends up maintaining multiple independent systems for different types of data, each with their own bugs and limitations.

---

## Enter Kafka

Apache Kafka was developed as a publish/subscribe messaging system designed to solve these problems. It is often described as a "distributed commit log" or "distributed streaming platform."

### Messages and Batches

The unit of data within Kafka is called a **message**. If you are approaching Kafka from a database background, you can think of this as similar to a row or a record.

A message is simply an array of bytes as far as Kafka is concerned, so the data contained within it does not have a specific format or meaning to Kafka. A message can have an optional piece of metadata, which is referred to as a **key**. The key is also a byte array and, as with the message, has no specific meaning to Kafka.

For efficiency, messages are written into Kafka in **batches**. A batch is just a collection of messages, all of which are being produced to the same topic and partition. An individual round trip across the network for each message would result in excessive overhead, and collecting messages together into a batch reduces this.

### Schemas

While messages are opaque byte arrays to Kafka itself, it is recommended that additional structure, or schema, be imposed on the message content so that it can be easily understood.

Many Kafka developers favor the use of **Apache Avro**, which is a serialization framework originally developed for Hadoop. Avro provides:
- Compact serialization format
- Schemas separate from message payloads
- Strong data typing and schema evolution
- Backward and forward compatibility

### Topics and Partitions

Messages in Kafka are categorized into **topics**. The closest analogies for a topic are a database table or a folder in a filesystem. Topics are additionally broken down into a number of **partitions**.

**Figure 1-5: Representation of a topic with multiple partitions**
![Figure 1-5](../images/ch01/figure-1-5-topic-partitions.png)

A partition is a single log. Messages are written to it in an append-only fashion and are read in order from beginning to end. Note that as a topic typically has multiple partitions, there is no guarantee of message ordering across the entire topic, just within a single partition.

Partitions are also the way that Kafka provides redundancy and scalability. Each partition can be hosted on a different server, which means that a single topic can be scaled horizontally across multiple servers.

### Producers and Consumers

**Kafka clients** are users of the system, and there are two basic types:

**Producers** create new messages. A message will be produced to a specific topic. By default, the producer will balance messages over all partitions of a topic evenly.

**Consumers** read messages. The consumer subscribes to one or more topics and reads the messages in the order in which they were produced to each partition.

Consumers keep track of which messages they have already consumed by keeping track of the **offset** of messages. The offset—an integer value that continually increases—is another piece of metadata that Kafka adds to each message as it is produced.

Consumers work as part of a **consumer group**, which is one or more consumers that work together to consume a topic.

**Figure 1-6: A consumer group reading from a topic**
![Figure 1-6](../images/ch01/figure-1-6-consumer-group.png)

### Brokers and Clusters

A single Kafka server is called a **broker**. The broker receives messages from producers, assigns offsets to them, and writes the messages to storage on disk. It also services consumers, responding to fetch requests for partitions and responding with the messages that have been published.

Kafka brokers are designed to operate as part of a **cluster**. Within a cluster of brokers, one broker will also function as the **cluster controller** (elected automatically from the live members of the cluster). The controller is responsible for administrative operations, including assigning partitions to brokers and monitoring for broker failures.

A partition is owned by a single broker in the cluster, and that broker is called the **leader** of the partition. A **replicated partition** is assigned to additional brokers, called **followers** of the partition. Replication provides redundancy of messages in the partition.

**Figure 1-7: Replication of partitions in a cluster**
![Figure 1-7](../images/ch01/figure-1-7-replication.png)

### Retention

A key feature of Apache Kafka is that of **retention**, which is the durable storage of messages for some period of time. Kafka brokers are configured with a default retention setting for topics, either:
- Retaining messages for some period of time (e.g., 7 days)
- Retaining until the partition reaches a certain size in bytes (e.g., 1 GB)

Once these limits are reached, messages are expired and deleted.

### Multiple Clusters

As Kafka deployments grow, it is often advantageous to have multiple clusters. There are several reasons why this can be useful:

- **Segregation of types of data**
- **Isolation for security requirements**
- **Multiple datacenters (disaster recovery)**

The **MirrorMaker** tool is used for replicating data to other clusters. At its core, MirrorMaker is simply a Kafka consumer and producer, linked together with a queue.

**Figure 1-8: Multiple datacenters architecture**
![Figure 1-8](../images/ch01/figure-1-8-multiple-datacenters.png)

---

## Why Kafka?

There are many choices for publish/subscribe messaging systems, so what makes Apache Kafka a good choice?

### Multiple Producers

Kafka is able to seamlessly handle multiple producers, whether those clients are using many topics or the same topic. This makes the system ideal for aggregating data from many frontend systems and making it consistent.

### Multiple Consumers

In addition to multiple producers, Kafka is designed for multiple consumers to read any single stream of messages without interfering with each other client. This is in contrast to many queuing systems where once a message is consumed by one client, it is not available to any other.

### Disk-Based Retention

Not only can Kafka handle multiple consumers, but durable message retention means that consumers do not always need to work in real time. Messages are written to disk and will be stored with configurable retention rules.

This allows for:
- Consumers can fall behind without losing data
- Maintenance can be performed on consumers with no message loss
- Data can be replayed if needed

### Scalable

Kafka's flexible scalability makes it easy to handle any amount of data. Users can start with a single broker as a proof of concept, expand to a small development cluster of three brokers, and move into production with a larger cluster of tens or even hundreds of brokers that grows over time as the data scales up.

### High Performance

All of these features come together to make Apache Kafka a publish/subscribe messaging system with excellent performance under high load. Producers, consumers, and brokers can all be scaled out to handle very large message streams with ease, while still providing subsecond message latency.

### Platform Features

The core Apache Kafka project has also added some streaming platform features:

- **Kafka Connect**: Assists with pulling data from source systems and pushing to Kafka
- **Kafka Streams**: Provides a library for developing stream processing applications

---

## The Data Ecosystem

Apache Kafka provides the circulatory system for the data ecosystem.

**Figure 1-9: A big data ecosystem**
![Figure 1-9](../images/ch01/figure-1-9-ecosystem.png)

It carries messages between the various members of the infrastructure, providing a consistent interface for all clients. When coupled with a system to provide message schemas, producers and consumers no longer require tight coupling or direct connections of any sort.

### Use Cases

#### Activity Tracking

The original use case for Kafka, as it was designed at LinkedIn, is that of user activity tracking. A website's users interact with frontend applications, which generate messages regarding actions the user is taking.

#### Messaging

Kafka is also used for messaging, where applications need to send notifications (such as emails) to users. Those applications can produce messages without needing to be concerned about formatting or how the messages will actually be sent.

#### Metrics and Logging

Kafka is ideal for collecting application and system metrics and logs. Applications publish metrics on a regular basis to a Kafka topic, and those metrics can be consumed by systems for monitoring and alerting.

#### Commit Log

Since Kafka is based on the concept of a commit log, database changes can be published to Kafka, and applications can easily monitor this stream to receive live updates as they happen.

#### Stream Processing

Another area that provides numerous types of applications is stream processing. While almost all usage of Kafka can be thought of as stream processing, the term is typically used to refer to applications that provide similar functionality to map/reduce processing in Hadoop.

---

## Kafka's Origin

Kafka was created to address the data pipeline problem at LinkedIn.

### LinkedIn's Problem

Similar to the example described above, LinkedIn had a system for collecting system and application metrics that used custom collectors and open source tools. However, the monitoring service was:
- Clunky and not scalable
- Required significant coordinated work to make changes
- Fragile and constantly breaking due to schema changes

### The Birth of Kafka

The development team at LinkedIn was led by **Jay Kreps**, with **Neha Narkhede** and **Jun Rao**. Together, they set out to create a messaging system that could meet the needs of both the monitoring and tracking systems, and scale for the future.

The primary goals were to:

1. Decouple producers and consumers by using a push-pull model
2. Provide persistence for message data within the messaging system to allow multiple consumers
3. Optimize for high throughput of messages
4. Allow for horizontal scaling of the system to grow as the data streams grew

The result was a publish/subscribe messaging system that had an interface typical of messaging systems but a storage layer more like a log-aggregation system. Combined with the adoption of Apache Avro for message serialization, Kafka was effective for handling both metrics and user-activity tracking at a scale of billions of messages per day.

### Open Source

Kafka was released as an open source project on GitHub in late 2010. As it started to gain attention in the open source community, it was proposed and accepted as an Apache Software Foundation incubator project in July of 2011. Apache Kafka graduated from the incubator in October of 2012.

Since then, it has continuously been worked on and has found a robust community of contributors and committers outside of LinkedIn. Kafka is now used in some of the largest data pipelines in the world, including those at Netflix, Uber, and many other companies.

### Commercial Engagement

In the fall of 2014, Jay Kreps, Neha Narkhede, and Jun Rao left LinkedIn to found **Confluent**, a company centered around providing development, enterprise support, and training for Apache Kafka.

### The Name

People often ask how Kafka got its name and if it signifies anything specific about the application itself. Jay Kreps offered the following insight:

> "I thought that since Kafka was a system optimized for writing, using a writer's name would make sense. I had taken a lot of lit classes in college and liked Franz Kafka. Plus the name sounded cool for an open source project."
>
> So basically there is not much of a relationship.

---

## Getting Started with Kafka

Now that we know all about Kafka and its history, we can set it up and build our own data pipeline.

**Next Chapter:** [Chapter 2: Installing Kafka](./02-installing-kafka.md)

---

**Return to [Table of Contents](../README.md)**
