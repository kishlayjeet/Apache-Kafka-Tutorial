# Apache Kafka

Apache Kafka is a high-throughput distributed streaming platform used for building real-time data pipelines and streaming applications. It is designed to handle high volume, high throughput, and low latency data streams.In this tutorial, we will learn the basic and advanced concepts of Apache Kafka, and how to get started with it.

![Apache Kafka](https://imgur.com/N9yMh5B.png)

- [Introduction to Apache Kafka](#)
  - [Basic Concepts](#basic-concepts)
- [Installation](#installation)
- [Creating a Topic](#creating-a-topic)
- [Producing and Consuming Messages](#producing-and-consuming-messages)
- [Advanced Concepts](#advanced-concepts)
  - [Replication](#replication)
  - [Offsets](#offsets)
  - [Consumer Groups](#consumer-groups)
  - [Transactions](#transactions)
  - [Connectors](#connectors)
- [Producing and Consuming Advanced Messages](#producing-and-consuming-advanced-messages)
- [Cheat Sheet](#cheat-sheet)
- [Conclusion](#conclusion)

## Basic Concepts

### Topics

A topic is a category or feed name to which messages are published. Topics are multi-subscriber, which means a topic can have zero, one, or many consumers that subscribe to the data written to it.

### Producers

Producers are the applications that write data to topics.

### Consumers

Consumers are the applications that read data from topics.

### Brokers

A Kafka cluster is composed of one or more servers, each of which is called a broker.

### Partitions

Topics are split into a number of partitions, which allows for parallelism when consuming the data. Each partition is an ordered, immutable sequence of records that is continually appended to.

## Installation

Before installing Kafka, make sure that you have installed Java and ZooKeeper on your machine. You can download the latest version of Kafka from the official website. Once downloaded, extract the files, and then follow the below steps:

### Start the ZooKeeper service by running the following command in the Kafka directory:

#### ~ Linux

```bash
 bin/zookeeper-server-start.sh config/zookeeper.properties
```

#### ~ Mac M1

```bash
 zookeeper-server-start /opt/homebrew/etc/kafka/zookeeper.properties
```

### Start the Kafka service by running the following command in the Kafka directory:

#### ~ Linux

```bash
 bin/kafka-server-start.sh config/server.properties
```

#### ~ Mac M1

```bash
 kafka-server-start /opt/homebrew/etc/kafka/server.properties
```

## Creating a Topic

To create a topic, follow these steps:

1. Open a command prompt and navigate to the Kafka directory.
2. Run the following command to create a new topic:

#### ~ Linux

```bash
 bin/kafka-topics.sh --create --zookeeper localhost:9092 --replication-factor 1 --partitions 1 --topic <topic_name>
```

#### ~ Mac M1

```bash
 kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic <topic_name>
```

## Producing and Consuming Messages

### To produce messages, run the following command in the Kafka directory:

#### ~ Linux

```bash
 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic <topic_name>
```

#### ~ Mac M1

```bash
 kafka-console-producer --broker-list localhost:9092 --topic <topic_name>
```

### To consume messages, run the following command in the Kafka directory:

#### ~ Linux

```bash
 bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic <topic_name> --from-beginning
```

#### ~ Mac M1

```bash
 kafka-console-consumer --bootstrap-server localhost:9092 --topic <topic_name> --from-beginning
```

## Advanced Concepts:

In addition to the basic concepts, Kafka also provides advanced features and capabilities that allow for more sophisticated data processing and management.

### Replication:

Replication is the process of keeping multiple copies of the same data to ensure data durability and high availability. Each partition can have one or more replicas, and one replica is designated as the leader for that partition. In case of a failure, the leader replica is replaced by one of the follower replicas, ensuring that the data remains available.

### Offsets:

An offset is a unique identifier of a record within a partition. It is used by consumers to keep track of their progress within a partition. Kafka stores the offsets in a special topic called `__consumer_offsets`, which is managed by Kafka itself.

### Consumer Groups:

A consumer group is a set of consumers that work together to consume a specific topic. Each consumer in a group is assigned a unique subset of the partitions in the topic. This allows for parallelism and scalability when consuming data from a topic.

### Transactions:

Kafka provides transactional support, which allows producers to send data to multiple partitions and topics as part of a single atomic operation. This ensures that the data is written to all the partitions and topics or none at all, ensuring data consistency.

### Connectors:

Kafka Connect is a framework for building and running data pipelines between Kafka and other data sources or sinks. Connectors can be used to import data from databases, files, or other messaging systems into Kafka, or to export data from Kafka to other systems.

## Producing and Consuming Advanced Messages:

To take advantage of Kafka's advanced features, you can use various command-line tools or APIs to produce and consume messages.

1. To produce messages to a specific partition, use the `--partition` flag with the `bin/kafka-console-producer.sh` command, like this:

```bash
 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic <topic_name> --partition <partition_number>
```

2. To consume messages from a specific partition, use the `--partition` and `--offset` flags with the `bin/kafka-console-consumer.sh` command, like this:

```bash
 bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic <topic_name> --partition <partition_number> --offset <offset_number>
```

3. To produce messages with a key, use the `--property` flag to set the `parse.key` and `key.separator` properties, like this:

```bash
 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic <topic_name> --property parse.key=true --property key.separator=:
```

4. To produce messages with headers, use the `--property` flag to set the `parse.key` and `key.header` properties, like this:

```bash
 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic <topic_name> --property "parse.key=true" --property "key.separator=:" --property "key.header=key"
```

## Cheat Sheet:

Here is a summary of the commands you can use to work with Kafka's advanced features:

#### ~ Produce message to specific partition:

```bash
 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic <topic_name> --partition <partition_number>
```

#### ~ Consume message from specific partition:

```bash
 bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic <topic_name> --partition <partition_number> --offset <offset_number>
```

#### ~ Produce message with key:

```bash
 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic <topic_name> --property parse.key=true --property key.separator=:
```

#### ~ Produce message with headers:

```bash
 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic <topic_name> --property "parse.key=true" --property "key.separator=:" --property "key.header=key"
```

#### ~ List all topics:

```bash
 bin/kafka-topics.sh --list --zookeeper localhost:9092
```

#### ~ Describe a topic:

```bash
 bin/kafka-topics.sh --describe --zookeeper localhost:9092 --topic <topic_name>
```

#### ~ Delete a topic:

```bash
 bin/kafka-topics.sh --delete --zookeeper localhost:9092 --topic <topic_name>
```

#### ~ List consumer groups:

```bash
 bin/kafka-consumer-groups.sh --list --bootstrap-server localhost:9092
```

#### ~ Describe a consumer group:

```bash
 bin/kafka-consumer-groups.sh --describe --bootstrap-server localhost:9092 --group <group_name>
```

#### ~ Reset consumer group offsets:

```bash
 bin/kafka-consumer-groups.sh --reset-offsets --bootstrap-server localhost:9092 --group <group_name> --topic <topic_name> --to-earliest
```

## Conclusion

In this tutorial, we have covered the basics of Apache Kafka and how to get started with it. We have covered important concepts such as topics, producers, consumers, brokers, and partitions. We have also gone over how to install Kafka and create topics, as well as how to produce and consume messages.

Additionally, we have covered some more advanced concepts such as replication, offsets, and consumer groups, as well as how to produce and consume advanced messages.

Overall, Apache Kafka is a powerful and flexible tool that can be used for a wide range of real-time data streaming and processing applications. By learning the basics of Kafka, you can start building your own data pipelines and streaming applications with confidence.

## Contributing

We welcome contributions from the community! If you have an example or improvement you'd like to contribute, please open a pull request with your changes.
