# 3. Kafka Producers: Writing Messages to Kafka

[< Back to Table of Contents](../README.md)

## Overview

Whether you use Kafka as a queue, message bus, or data storage platform, you will always use Kafka by creating a producer that writes data to Kafka, a consumer that reads data from Kafka, or an application that serves both roles.

For example, in a credit card transaction processing system, there will be a client application, perhaps an online store, responsible for sending each transaction to Kafka immediately when a payment is made. Another application is responsible for immediately checking this transaction against a rules engine and determining whether the transaction is approved or denied.

## Table of Contents

1. [Producer Overview](#producer-overview)
2. [Constructing a Kafka Producer](#constructing-a-kafka-producer)
3. [Sending a Message to Kafka](#sending-a-message-to-kafka)
4. [Configuring Producers](#configuring-producers)
5. [Serializers](#serializers)
6. [Partitions](#partitions)
7. [Headers](#headers)
8. [Interceptors](#interceptors)
9. [Quotas and Throttling](#quotas-and-throttling)
10. [Summary](#summary)

## Producer Overview

There are many reasons an application might need to write messages to Kafka: recording user activities for auditing or analysis, recording metrics, storing log messages, recording information from smart appliances, communicating asynchronously with other applications, buffering information before writing to a database, and much more.

Those diverse use cases also imply diverse requirements: is every message critical, or can we tolerate loss of messages? Are we OK with accidentally duplicating messages? Are there any strict latency or throughput requirements we need to support?

**Figure 3-1: High-level overview of Kafka producer components**
![Figure 3-1: Kafka Producer Components](../images/ch03/03-figure-01.png)

We start producing messages to Kafka by creating a `ProducerRecord`, which must include the topic we want to send the record to and a value. Optionally, we can also specify a key, a partition, a timestamp, and/or a collection of headers. Once we send the `ProducerRecord`, the first thing the producer will do is serialize the key and value objects to byte arrays so they can be sent over the network.

Next, if we didn't explicitly specify a partition, the data is sent to a partitioner. The partitioner will choose a partition for us, usually based on the `ProducerRecord` key. Once a partition is selected, the producer knows which topic and partition the record will go to. It then adds the record to a batch of records that will also be sent to the same topic and partition. A separate thread is responsible for sending those batches of records to the appropriate Kafka brokers.

## Constructing a Kafka Producer

The first step in writing messages to Kafka is to create a producer object with the properties you want to pass to the producer. A Kafka producer has three mandatory properties:

### bootstrap.servers

List of `host:port` pairs of brokers that the producer will use to establish initial connection to the Kafka cluster. This list doesn't need to include all brokers, since the producer will get more information after the initial connection. But it is recommended to include at least two, so in case one broker goes down, the producer will still be able to connect to the cluster.

### key.serializer

Name of a class that will be used to serialize the keys of the records we will produce to Kafka. Kafka brokers expect byte arrays as keys and values of messages. The producer will use this class to serialize the key object to a byte array. The Kafka client package includes `ByteArraySerializer`, `StringSerializer`, `IntegerSerializer`, and much more.

### value.serializer

Name of a class that will be used to serialize the values of the records we will produce to Kafka. The same way you set `key.serializer` to a name of a class that will serialize the message key object to a byte array, you set `value.serializer` to a class that will serialize the message value object.

### Creating a Producer

```java
Properties kafkaProps = new Properties();
kafkaProps.put("bootstrap.servers", "broker1:9092,broker2:9092");
kafkaProps.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
kafkaProps.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
producer = new KafkaProducer(kafkaProps);
```

## Sending a Message to Kafka

There are three primary methods of sending messages:

### Fire-and-forget

We send a message to the server and don't really care if it arrives successfully or not. Most of the time, it will arrive successfully, since Kafka is highly available and the producer will retry sending messages automatically.

### Synchronous Send

Technically, Kafka producer is always asynchronous—we send a message and the `send()` method returns a `Future` object. However, we use `get()` to wait on the `Future` and see if the `send()` was successful or not before sending the next record.

### Asynchronous Send

We call the `send()` method with a callback function, which gets triggered when it receives a response from the Kafka broker.

## Configuring Producers

The producer has a large number of configuration parameters. Here are the most important ones:

### client.id

`client.id` is a logical identifier for the client and the application it is used in. This can be any string and will be used by the brokers to identify messages sent from the client.

### acks

The `acks` parameter controls how many partition replicas must receive the record before the producer can consider the write successful.

- **acks=0**: The producer will not wait for a reply from the broker before assuming the message was sent successfully.
- **acks=1**: The producer will receive a success response from the broker the moment the leader replica receives the message.
- **acks=all**: The producer will receive a success response from the broker once all in sync replicas receive the message.

### retries and retry.backoff.ms

When the producer receives an error message from the server, the error could be transient. The value of the `retries` parameter will control how many times the producer will retry sending the message before giving up.

### linger.ms

`linger.ms` controls the amount of time to wait for additional messages before sending the current batch. Setting `linger.ms` higher than 0 means we instruct the producer to wait a few milliseconds to add additional messages to the batch before sending it to the brokers.

### buffer.memory

This config sets the amount of memory the producer will use to buffer messages waiting to be sent to brokers.

### compression.type

By default, messages are sent uncompressed. This parameter can be set to `snappy`, `gzip`, `lz4`, or `zstd`, in which case the corresponding compression algorithms will be used to compress the data before sending it to the brokers.

### batch.size

When multiple records are sent to the same partition, the producer will batch them together. This parameter controls the amount of memory in bytes that will be used for each batch.

## Serializers

The producer has mandatory serializers. Kafka includes serializers for common types like integers, byte arrays, and strings. However, you will eventually want to be able to serialize more generic records.

### Custom Serializers

You can create your own serializers by implementing the `Serializer` interface:

```java
public class CustomerSerializer implements Serializer {
    @Override
    public void configure(Map configs, boolean isKey) {
        // nothing to configure
    }

    @Override
    public byte[] serialize(String topic, Customer data) {
        // serialize Customer object to byte array
    }

    @Override
    public void close() {
        // nothing to close
    }
}
```

### Apache Avro Serialization

Apache Avro is a language-neutral data serialization format. One of the most interesting features of Avro is that when the application that is writing messages switches to a new but compatible schema, the applications reading the data can continue processing messages without requiring any change or update.

**Figure 3-2: Sequence diagram of delivery time breakdown inside Kafka producer**
![Figure 3-2: Delivery Time Breakdown](../images/ch03/03-figure-02.png)

To achieve this, we use a Schema Registry. The idea is to store all the schemas used to write data to Kafka in the registry. Then we simply store the identifier for the schema in the record we produce to Kafka. The consumers can then use the identifier to pull the record out of the Schema Registry and deserialize the data.

**Figure 3-3: Flow diagram of serialization and deserialization of Avro records**
![Figure 3-3: Avro Serialization Flow](../images/ch03/03-figure-03.png)

```java
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("key.serializer", "io.confluent.kafka.serializers.KafkaAvroSerializer");
props.put("value.serializer", "io.confluent.kafka.serializers.KafkaAvroSerializer");
props.put("schema.registry.url", schemaUrl);

Producer<String, Customer> producer = new KafkaProducer<>(props);
String topic = "customerContacts";

while (true) {
    Customer customer = CustomerGenerator.getNext();
    ProducerRecord<String, Customer> record = new ProducerRecord<>(topic, customer.getName(), customer);
    producer.send(record);
}
```

## Partitions

In previous examples, the `ProducerRecord` objects we created included a topic name, key, and value. Kafka messages are key-value pairs. Keys serve two goals: they are additional information that gets stored with the message, and they are typically also used to decide which one of the topic partitions the message will be written to.

When the key is `null` and the default partitioner is used, the record will be sent to one of the available partitions of the topic at random. A round-robin algorithm will be used to balance the messages among the partitions.

If a key exists and the default partitioner is used, Kafka will hash the key (using its own hash algorithm) and use the result to map the message to a specific partition. Since it is important that a key is always mapped to the same partition, we use all the partitions in the topic to calculate the mapping—not just the available partitions.

## Headers

Records can, in addition to key and value, also include headers. Record headers give you the ability to add some metadata about the Kafka record, without adding any extra information to the key/value pair of the record itself.

```java
ProducerRecord<String, String> record = new ProducerRecord<>("CustomerCountry", "Precision Products", "France");
record.headers().add("privacy-level", "YOLO".getBytes(StandardCharsets.UTF_8));
```

## Interceptors

Kafka's `ProducerInterceptor` includes two key methods:

- **onSend()**: This method will be called before the produced record is sent to Kafka
- **onAcknowledgement()**: This method will be called if and when Kafka responds with an acknowledgment for a send

Common use cases for producer interceptors include capturing monitoring and tracing information, enhancing the message with standard headers, and redacting sensitive information.

## Quotas and Throttling

Kafka brokers have the ability to limit the rate at which messages are produced and consumed via the quota mechanism. Kafka has three quota types: produce, consume, and request.

Producers can apply quotas to specific clients dynamically using `kafka-configs.sh`:

```bash
bin/kafka-configs --bootstrap-server localhost:9092 --alter --add-config 'producer_byte_rate=1024' --entity-name clientC --entity-type clients
```

## Summary

We began this chapter with a simple example of a producer and explored the most important producer configuration parameters. We discussed serializers, which let us control the format of the events we write to Kafka. We looked in-depth at Avro, one of many ways to serialize events but one that is very commonly used with Kafka. We concluded the chapter with a discussion of partitioning in Kafka.

Now that we know how to write events to Kafka, in [Chapter 4](../chapters/04-kafka-consumers.md) we'll learn all about consuming events from Kafka.

---

[Next: Chapter 4 - Kafka Consumers: Reading Data From Kafka >](../chapters/04-kafka-consumers.md)
