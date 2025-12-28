# Chapter 13: Monitoring Kafka

## TABLE OF CONTENTS

- [Metric Basics](#metric-basics)
  - [Where Are the Metrics?](#where-are-the-metrics)
  - [What Metrics Do I Need?](#what-metrics-do-i-need)
  - [Application Health Checks](#application-health-checks)
- [Service-Level Objectives](#service-level-objectives)
  - [Service-Level Definitions](#service-level-definitions)
  - [What Metrics Make Good SLIs?](#what-metrics-make-good-slis)
  - [Using SLOs in Alerting](#using-slos-in-alerting)
- [Kafka Broker Metrics](#kafka-broker-metrics)
  - [Diagnosing Cluster Problems](#diagnosing-cluster-problems)
  - [The Art of Under-Replicated Partitions](#the-art-of-under-replicated-partitions)
  - [Broker Metrics](#broker-metrics)
  - [Topic and Partition Metrics](#topic-and-partition-metrics)
  - [JVM Monitoring](#jvm-monitoring)
  - [OS Monitoring](#os-monitoring)
  - [Logging](#logging)
- [Client Monitoring](#client-monitoring)
  - [Producer Metrics](#producer-metrics)
  - [Consumer Metrics](#consumer-metrics)
  - [Quotas](#quotas)
- [Lag Monitoring](#lag-monitoring)
- [End-to-End Monitoring](#end-to-end-monitoring)
- [Summary](#summary)

The Apache Kafka applications have numerous measurements for their operation—so many, in fact, that it can easily become confusing as to what is important to watch and what can be set aside. They provide a detailed view into every operation in the broker, but they can also make you the bane of whoever is responsible for managing your monitoring system.

This chapter will detail the most critical metrics to monitor all the time and how to respond to them. We'll also describe some of the more important metrics to have on hand when debugging problems.

## Metric Basics

Before getting into the specific metrics provided by the Kafka broker and clients, let's discuss the basics of how to monitor Java applications and some best practices around monitoring and alerting.

### Where Are the Metrics?

All of the metrics exposed by Kafka can be accessed via the Java Management Extensions (JMX) interface. The easiest way to use them in an external monitoring system is to use a collection agent provided by your monitoring system and attach it to the Kafka process.

> **FINDING THE JMX PORT**
>
> To aid with configuring applications that connect to JMX on the Kafka broker directly, the broker sets the configured JMX port in the broker information that is stored in ZooKeeper. However, remote JMX is disabled by default in Kafka for security reasons. If you are going to enable it, you must properly configure security for the port.

**Table 13-1: Metric sources**

| Category | Description |
|----------|-------------|
| Application metrics | These are the metrics you get from Kafka itself, from the JMX interface. |
| Logs | Text or structured data that requires more processing. |
| Infrastructure metrics | Metrics from systems in front of Kafka but within the request path. |
| Synthetic clients | Data from external tools like Kafka Monitor that simulate client behavior. |
| Client metrics | Metrics exposed by the Kafka clients that connect to your cluster. |

### What Metrics Do I Need?

The specific metrics that are important to you depends on what you intend to do with them. A broker internals developer will have far different needs than a site reliability engineer who is running a Kafka deployment.

#### Alerting or debugging?

A metric that is destined for alerting is useful for a very short period of time. These metrics will be consumed by automation that responds to known problems. Data that is primarily for debugging has a longer time horizon because you are frequently diagnosing problems that have existed for some time.

> **HISTORICAL METRICS**
>
> There is a third type of data that you will need eventually: historical data on your application. The most common use for historical data is for capacity management purposes. These metrics will need to be stored for a very long period of time, measured in years.

#### Automation or humans?

If the metrics are consumed by automation, they should be very specific. On the other hand, if the metrics will be consumed by humans, presenting a large number of metrics will be overwhelming.

### Application Health Checks

No matter how you collect metrics from Kafka, you should make sure that you have a way to also monitor the overall health of the application process via a simple health check. This can be done in two ways:

- An external process that reports whether the broker is up or down
- Alerting on the lack of metrics being reported by the Kafka broker

## Service-Level Objectives

One area of monitoring that is especially critical for infrastructure services is that of service-level objectives, or SLOs. This is how we communicate to our clients what level of service they can expect.

### Service-Level Definitions

**Service-level indicator (SLI)**: A metric that describes one aspect of a service's reliability. It should be closely aligned with your client's experience.

**Service-level objective (SLO)**: Combines an SLI with a target value. The SLO should also include a time frame that it is measured over. For example, 99% of requests to the web server must return a 2xx, 3xx, or 4xx response over 7 days.

**Service-level agreement (SLA)**: A contract between a service provider and a client. It usually includes several SLOs, as well as details about how they are measured and reported.

**Table 13-2: Types of SLIs**

| Type | Description |
|------|-------------|
| Availability | Is the client able to make a request and get a response? |
| Latency | How quickly is the response returned? |
| Quality | Does the response include a proper response? |
| Security | Are the request and response appropriately protected? |
| Throughput | Can the client get enough data, fast enough? |

### What Metrics Make Good SLIs?

In general, the metrics for your SLIs should be gathered using something external to the Kafka brokers. Your clients do not care if you think your service is running correctly; it is their experience (in aggregate) that matters. This means that infrastructure metrics are OK, synthetic clients are good, and client-side metrics are probably the best for most of your SLIs.

### Using SLOs in Alerting

SLOs should inform your primary alerts. The reason for this is that the SLOs describe problems from your customers' point of view, and those are the ones that you should be concerned about first. The best way to approach using SLOs for alerting is to observe the rate at which you are burning through your SLO over its timeframe.

## Kafka Broker Metrics

There are many Kafka broker metrics. Many of them are low-level measurements, added by developers when investigating a specific issue. The most common ones provide the information needed to run Kafka on a daily basis.

> **WHO WATCHES THE WATCHERS?**
>
> Many organizations use Kafka for collecting application metrics, system metrics, and logs. If you use this same system for monitoring Kafka itself, it is very likely that you will never know when Kafka is broken because the data flow for your monitoring system will be broken as well.

### Diagnosing Cluster Problems

When it comes to problems with a Kafka cluster, there are three major categories:

- Single-broker problems
- Overloaded clusters
- Controller problems

Issues with individual brokers are, by far, the easiest to diagnose and respond to. These will show up as outliers in the metrics for the cluster.

> **PREFERRED REPLICA ELECTIONS**
>
> The first step before trying to diagnose a problem further is to ensure that you have run a preferred replica election recently. Kafka brokers do not automatically take partition leadership back (unless auto leader rebalance is enabled) after they have released leadership.

### The Art of Under-Replicated Partitions

One of the most popular metrics to use when monitoring Kafka is under-replicated partitions. This single measurement provides insight into a number of problems with the Kafka cluster.

**Table 13-3: Under-replicated partitions metric**

| Metric name | Under-replicated partitions |
|-------------|-----------------------------|
| JMX MBean | `kafka.server:type=ReplicaManager,name=UnderReplicatedPartitions` |
| Value range | Integer, zero or greater |

> **THE URP ALERTING TRAP**
>
> The under-replicated partitions (URP) metric should be your primary alerting metric because of how many problems it describes. However, this approach has problems. The URP metric can frequently be nonzero for benign reasons. For this reason, we no longer recommend the use of URP for alerting. Instead, you should depend on SLO-based alerting to detect unknown problems.

Example of listing under-replicated partitions:

```bash
# kafka-topics.sh --bootstrap-server kafka1.example.com:9092/kafka-cluster \
  --describe --under-replicated
Topic: topicOne  Partition: 5    Leader: 1    Replicas: 1,2 Isr: 1
Topic: topicOne  Partition: 6    Leader: 3    Replicas: 2,3 Isr: 3
```

### Broker Metrics

In addition to under-replicated partitions, there are other metrics that are present at the overall broker level that should be monitored.

#### Active controller count

The active controller count metric indicates whether the broker is currently the controller for the cluster. The metric will either be 0 or 1. At all times, only one broker should be the controller.

**Table 13-5: Active controller count**

| Metric name | Active controller count |
|-------------|-------------------------|
| JMX MBean | `kafka.controller:type=KafkaController,name=ActiveControllerCount` |
| Value range | Zero or one |

#### Request handler idle ratio

Kafka uses two thread pools for handling all client requests: network threads and request handler threads. The request handler idle ratio metric indicates the percentage of time the request handlers are not in use.

**Table 13-7: Request handler idle ratio**

| Metric name | Request handler average idle percentage |
|-------------|------------------------------------------|
| JMX MBean | `kafka.server:type=KafkaRequestHandlerPool,name=RequestHandlerAvgIdlePercent` |
| Value range | Float, between zero and one inclusive |

#### All topics bytes in/out

The all topics bytes in rate is useful as a measurement of how much message traffic your brokers are receiving from producing clients. This is a good metric to trend over time.

**Table 13-8: All topics bytes in**

| Metric name | Bytes in per second |
|-------------|---------------------|
| JMX MBean | `kafka.server:type=BrokerTopicMetrics,name=BytesInPerSec` |
| Value range | Rates as doubles, count as integer |

### Topic and Partition Metrics

In larger clusters these can be numerous. However, they are quite useful for debugging specific issues with a client.

**Table 13-16: Metrics for each topic**

| Name | JMX MBean |
|------|-----------|  
| Bytes in rate | `kafka.server:type=BrokerTopicMetrics,name=BytesInPerSec,topic=TOPICNAME` |
| Bytes out rate | `kafka.server:type=BrokerTopicMetrics,name=BytesOutPerSec,topic=TOPICNAME` |
| Messages in rate | `kafka.server:type=BrokerTopicMetrics,name=MessagesInPerSec,topic=TOPICNAME` |

### JVM Monitoring

For the JVM, the critical thing to monitor is the status of garbage collection (GC).

**Table 13-18: G1 garbage collection metrics**

| Name | JMX MBean |
|------|-----------|  
| Full GC cycles | `java.lang:type=GarbageCollector,name=G1 Old Generation` |
| Young GC cycles | `java.lang:type=GarbageCollector,name=G1 Young Generation` |

### OS Monitoring

For CPU utilization, you will want to look at the system load average at the very least. Disk is by far the most important subsystem when it comes to Kafka. All messages are persisted to disk, so the performance of Kafka depends heavily on the performance of the disks.

### Logging

By simply logging all messages at the `INFO` level, you will capture a significant amount of important information about the state of the broker. It is useful to separate a couple of loggers from this:

- `kafka.controller` at `INFO` level
- `kafka.server.ClientQuotaManager` at `INFO` level
- `kafka.log.LogCleaner`, `kafka.log.Cleaner`, and `kafka.log.LogCleanerManager` at `DEBUG` level

## Client Monitoring

All applications need monitoring. Those that instantiate a Kafka client have metrics specific to the client that should be captured.

### Producer Metrics

The Kafka producer client has greatly compacted the metrics available by making them available as attributes on a small number of JMX MBeans.

**Table 13-19: Kafka producer metric MBeans**

| Name | JMX MBean |
|------|-----------|  
| Overall producer | `kafka.producer:type=producer-metrics,client-id=CLIENTID` |
| Per-broker | `kafka.producer:type=producer-node-metrics,client-id=CLIENTID,node-id=node-BROKERID` |
| Per-topic | `kafka.producer:type=producer-topic-metrics,client-id=CLIENTID,topic=TOPICNAME` |

Key producer metrics to monitor:

- `record-error-rate`: Should always be zero
- `request-latency-avg`: Average produce request latency
- `outgoing-byte-rate`: Bytes per second produced
- `record-send-rate`: Messages per second produced

### Consumer Metrics

The consumer provides metrics beans for overall consumer, fetch manager, per-topic, per-broker, and coordinator.

**Table 13-20: Kafka consumer metric MBeans**

| Name | JMX MBean |
|------|-----------|  
| Overall consumer | `kafka.consumer:type=consumer-metrics,client-id=CLIENTID` |
| Fetch manager | `kafka.consumer:type=consumer-fetch-manager-metrics,client-id=CLIENTID` |
| Per-topic | `kafka.consumer:type=consumer-fetch-manager-metrics,client-id=CLIENTID,topic=TOPICNAME` |
| Per-broker | `kafka.consumer:type=consumer-node-metrics,client-id=CLIENTID,node-id=node-BROKERID` |
| Coordinator | `kafka.consumer:type=consumer-coordinator-metrics,client-id=CLIENTID` |

Key consumer metrics:

- `fetch-latency-avg`: Average fetch request latency
- `bytes-consumed-rate`: Bytes per second consumed
- `records-consumed-rate`: Messages per second consumed

### Quotas

Apache Kafka has the ability to throttle client requests. The metrics that must be monitored are shown below.

**Table 13-21: Quota metrics**

| Client | Bean name |
|--------|-----------|  
| Consumer | `kafka.consumer:type=consumer-fetch-manager-metrics,client-id=CLIENTID`, attribute `fetch-throttle-time-avg` |
| Producer | `kafka.producer:type=producer-metrics,client-id=CLIENTID`, attribute `produce-throttle-time-avg` |

## Lag Monitoring

For Kafka consumers, the most important thing to monitor is the consumer lag. The preferred method of consumer lag monitoring is to have an external process that can watch both the state of the partition on the broker and the state of the consumer.

One way to monitor consumer groups and reduce complexity is to use Burrow. This is an open source application that provides consumer status monitoring by calculating a single status for each group saying whether the consumer group is working properly, falling behind, or is stalled or stopped entirely.

## End-to-End Monitoring

Another type of external monitoring that is recommended is an end-to-end monitoring system. Xinfra Monitor (formerly Kafka Monitor) continually produces and consumes data from a topic that is spread across all brokers in a cluster. It measures the availability of both produce and consume requests on each broker, as well as the total produce to consume latency.

## Summary

Monitoring is a key aspect of running Apache Kafka properly. In this chapter we covered:

- The basics of how to monitor Java applications and Kafka specifically
- Service-level objectives (SLOs) and their role in alerting
- A subset of the numerous metrics available in the Kafka broker
- Java and OS monitoring
- Logging best practices
- Monitoring available in the Kafka client libraries, including quota monitoring
- External monitoring systems for consumer lag and end-to-end cluster availability

While certainly not an exhaustive list of the metrics that are available, this chapter reviewed the most critical ones to keep an eye on.

## External Resources

- [Site Reliability Engineering](https://oreil.ly/bPBxC)
- [The Site Reliability Workbook](https://oreil.ly/qSmOc)
- [Cruise Control](https://oreil.ly/rLybu)
- [LinkedIn Engineering - kafka-tools repository](https://oreil.ly/8ilPw)
- [Chef](https://www.chef.io/)
- [Puppet](https://puppet.com/)
- [Burrow](https://oreil.ly/supY1)
- [LinkedIn Engineering blog - Burrow](http://bit.ly/2sanKZb)
- [Xinfra Monitor (Kafka Monitor)](https://oreil.ly/QqXD9)
