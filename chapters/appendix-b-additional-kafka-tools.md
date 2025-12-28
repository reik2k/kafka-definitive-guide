# Appendix B. Additional Kafka Tools

## TABLE OF CONTENTS
- [Comprehensive Platforms](#comprehensive-platforms)
- [Cluster Deployment and Management](#cluster-deployment-and-management)
- [Monitoring and Data Exploration](#monitoring-and-data-exploration)
- [Client Libraries](#client-libraries)
- [Stream Processing](#stream-processing)
- [External Resources](#external-resources)

---

The Apache Kafka community has created a robust ecosystem of tools and platforms that make the task of running and using Kafka far easier. While this is by no means an exhaustive list, several of the more popular tools are presented here to help get you started.

## CAVEAT EMPTOR

While the authors are affiliated with some of the companies and projects that are included in this list, neither they nor O'Reilly specifically endorse one tool over others. Please be sure to do your own research on the suitability of these platforms and tools for the work that you need to do.

## Comprehensive Platforms

Several companies offer fully integrated platforms for working with Apache Kafka. This includes managed deployments of all components, such that you can focus on using Kafka and not on how to run it. This can present an ideal solution for use cases where resources are not available (or you do not want to dedicate them) for learning how to properly operate Kafka and the infrastructure required around it. Several also provide tools, such as schema management, REST interfaces, and in some cases client library support, so that you can be assured components interoperate correctly.

### Confluent Cloud

**Description:** It's only fitting that the company created by some of the original developers to develop and support Kafka provides a managed solution. Confluent Cloud combines a number of must-have tools—including schema management, clients, a RESTful interface, and monitoring—into a single offering. It's available on all three major cloud platforms (AWS, Microsoft Azure, and Google Cloud Platform) and is backed with support provided by a sizable portion of the core Apache Kafka contributors employed by Confluent. Many of the components that are included in the platform, such as the Schema Registry and the REST proxy, are available as standalone tools under the Confluent Community License, which does restrict some use cases.

### Aiven

**Description:** Aiven provides managed solutions for many data platforms, including Kafka. To support this, it has developed Karapace, which is a schema registry and a REST proxy, both API-compatible with Confluent's components but supported under the Apache 2.0 license, which does not restrict use cases. In addition to the three major cloud providers, Aiven also supports DigitalOcean and UpCloud.

### CloudKarafka

**Description:** CloudKarafka focuses on providing a managed Kafka solution with integrations for popular infrastructure services (such as DataDog or Splunk). It supports the use of Confluent's Schema Registry and REST proxy with its platform, but only the 5.0 version prior to the license changes by Confluent. CloudKarafka provides its services on both AWS and Google Cloud Platform.

### Amazon Managed Streaming for Apache Kafka (Amazon MSK)

**Description:** Amazon also provides its own managed Kafka platform, supported only on AWS. Schema support is provided through integration with AWS Glue, while a REST proxy is not directly supported. Amazon promotes the use of community tools (such as Cruise Control, Burrow, and Confluent's REST proxy) but does not directly support them. As such, MSK is somewhat less integrated than other offers, but can still provide a core Kafka cluster.

### Azure HDInsight

**Description:** Microsoft also provides a managed platform for Kafka in HDInsight, which also supports Hadoop, Spark, and other big data components. Similar to MSK, HDInsight focuses on the core Kafka cluster, leaving many of the other components (including a schema registry and REST proxy) up to the user to provide. Some third parties have provided templates for performing these deployments, but they are not supported by Microsoft.

### Cloudera

**Description:** Cloudera has been a fixture in the Kafka community since the early days and provides managed Kafka as the stream data component of its overall Customer Data Platform (CDP) product. CDP focuses on more than just Kafka, however, and it operates in the public cloud environments as well as providing private options.

## Cluster Deployment and Management

When running Kafka outside of a managed platform, you will need several things to assist you with running the cluster properly. This includes help with provisioning and deployment, balancing data, and visualizing your clusters.

### Strimzi

**Description:** Strimzi provides Kubernetes operators for deploying Kafka clusters to make it easier to set up Kafka in a Kubernetes environment. It does not provide managed services but instead makes it easy for you to get up and running in a cloud, whether public or private. It also provides the Strimzi Kafka Bridge, which is a REST proxy implementation supported under the Apache 2.0 license. At this time, Strimzi does not have support for a schema registry, due to concerns about licenses.

### AKHQ

**Description:** AKHQ is a GUI for managing and interacting with Kafka clusters. It supports configuration management, including users and ACLs, and provides some support for components like the Schema Registry and Kafka Connect as well. It also provides tools for working with data in the cluster as an alternative to the console tools.

### JulieOps

**Description:** JulieOps (formerly Kafka Topology Builder) provides for automated management of topics and ACLs using a GitOps model. More than viewing the state of the current configuration, JulieOps provides a means for declarative configuration and change control of topics, schemas, ACLs, and more over time.

### Cruise Control

**Description:** Cruise Control is LinkedIn's answer to how to manage hundreds of clusters with thousands of brokers. This tool began as a solution to automated rebalancing of data in clusters but has evolved to include anomaly detection and administrative operations, such as adding and removing brokers. For anything more than a testing cluster, it is a must-have for any Kafka operator.

### Conduktor

**Description:** While not open source, Conduktor is a popular desktop tool for managing and interacting with Kafka clusters. It supports many of the managed platforms (including Confluent, Aiven, and MSK) and many different components (such as Connect, kSQL, and Streams). It also allows you to interact with data in the clusters, as opposed to using the console tools. A free license is provided for development use that works with a single cluster.

## Monitoring and Data Exploration

A critical part to running Kafka is to ensure that your cluster and your clients are healthy. Like many applications, Kafka exposes numerous metrics and other telemetry, but making sense of it can be challenging. Many of the larger monitoring platforms (such as Prometheus) can easily fetch metrics from Kafka brokers and clients. There are also a number of tools available to assist with making sense of all the data.

### Xinfra Monitor

**Description:** Xinfra Monitor (formerly Kafka Monitor) was developed by LinkedIn to monitor availability of Kafka clusters and brokers. It does this by using a set of topics to generate synthetic data through the cluster and measuring latency, availability, and completeness. It's a valuable tool for measuring your Kafka deployment's health without requiring direct interaction with your clients.

### Burrow

**Description:** Burrow is another tool originally created by LinkedIn, which provides holistic monitoring of consumer lag within Kafka clusters. It provides a view into the health of the consumers without needing to directly interact with them. Burrow is actively supported by the community and has its own ecosystem of tools to connect it with other components.

### Kafka Dashboard

**Description:** For those who use DataDog for monitoring, it provides an excellent Kafka Dashboard to give you a head start on integrating Kafka clusters into your monitoring stack. It is designed to provide a single-pane view of your Kafka cluster, simplifying the view of many metrics.

### Streams Explorer

**Description:** Streams Explorer is a tool for visualizing the flow of data through applications and connectors in a Kubernetes deployment. While it heavily relies on structuring your deployments using either Kafka Streams or Faust through bakdata's tools, it can then provide an easily comprehensible view of those applications and their metrics.

### kcat

**Description:** Kcat (formerly kafkacat) is a much-loved alternative to the console producer and consumer that are part of the core Apache Kafka project. It is small, fast, and written in C, so it does not have JVM overhead. It also supports limited views into cluster status by showing metadata output for the cluster.

## Client Libraries

The Apache Kafka project provides client libraries for Java applications, but one language is never enough. There are many implementations of the Kafka client out there, with popular languages such as Python, Go, and Ruby having several options. In addition, REST proxies (such as those from Confluent, Strimzi, or Karapace) can cover a variety of use cases. Here are a few client implementations that have stood the test of time.

### librdkafka

**Description:** librdkafka is a C library implementation of the Kafka client that is regarded as one of the best-performing libraries available. So good, in fact, that Confluent supports clients for Go, Python, and .NET that it created as wrappers around librdkafka. It is licensed simply under the two-clause BSD license, which makes it easy to use in any application.

### Sarama

**Description:** Shopify created the Sarama client as a native Golang implementation. It's released under the MIT license.

### kafka-python

**Description:** kafka-python is another native client implementation, this time in Python. It's released under the Apache 2.0 license.

## Stream Processing

While the Apache Kafka project includes Kafka Streams for building applications, it's not the only choice out there for stream processing of data from Kafka.

### Samza

**Description:** Apache Samza is a framework for stream processing that was specifically designed for Kafka. While it predates Kafka Streams, it was developed by many of the same people, and as a result the two share many concepts. However, unlike Kafka Streams, Samza runs on Yarn and provides a full framework for applications to run in.

### Spark

**Description:** Spark is another Apache project oriented toward batch processing of data. It handles streams by considering them to be fast microbatches. This means the latency is a little higher, but fault tolerance is simply handled through reprocessing batches, and Lambda architecture is easy. It also has the benefit of wide community support.

### Flink

**Description:** Apache Flink is specifically oriented toward stream processing and operates with very low latency. Like Samza, it supports Yarn but also works with Mesos, Kubernetes, or standalone clusters. It also supports Python and R with provided high-level APIs.

### Beam

**Description:** Apache Beam doesn't provide stream processing directly but instead promotes itself as a unified programming model for both batch and stream processing. It utilizes platforms like Samza, Spark, and Flink as runners for components in an overall processing pipeline.

## External Resources

- [Confluent Cloud](https://www.confluent.io/confluent-cloud)
- [Confluent Community License](https://oreil.ly/lAFga)
- [Aiven](https://aiven.io/)
- [Karapace](https://karapace.io/)
- [Apache 2.0 License](https://oreil.ly/a96F0)
- [DigitalOcean](https://www.digitalocean.com/)
- [UpCloud](https://upcloud.com/)
- [CloudKarafka](https://www.cloudkarafka.com/)
- [Amazon MSK](https://aws.amazon.com/msk)
- [AWS Glue](https://oreil.ly/hvjoV)
- [Azure HDInsight](https://azure.microsoft.com/en-us/services/hdinsight)
- [Cloudera Kafka](https://www.cloudera.com/products/open-source/apache-hadoop/apache-kafka.html)
- [Strimzi](https://strimzi.io/)
- [AKHQ](https://akhq.io/)
- [JulieOps (GitHub)](https://github.com/kafka-ops/julie)
- [Cruise Control (GitHub)](https://github.com/linkedin/cruise-control)
- [Conduktor](https://www.conduktor.io/)
- [Xinfra Monitor (GitHub)](https://github.com/linkedin/kafka-monitor)
- [Burrow (GitHub)](https://github.com/linkedin/burrow)
- [Burrow Ecosystem Tools](https://oreil.ly/yNPRQ)
- [Kafka Dashboard - DataDog](https://www.datadoghq.com/dashboards/kafka-dashboard)
- [Streams Explorer (GitHub)](https://github.com/bakdata/streams-explorer)
- [kcat (GitHub)](https://github.com/edenhill/kafkacat)
- [Prometheus](https://prometheus.io/)
- [librdkafka (GitHub)](https://github.com/edenhill/librdkafka)
- [Two-clause BSD License](https://oreil.ly/dLoe8)
- [Sarama (GitHub)](https://github.com/Shopify/sarama)
- [MIT License](https://oreil.ly/sajdS)
- [kafka-python (GitHub)](https://github.com/dpkp/kafka-python)
- [Apache Samza](https://samza.apache.org/)
- [Apache Spark](https://spark.apache.org/)
- [Apache Flink](https://flink.apache.org/)
- [Apache Beam](https://beam.apache.org/)