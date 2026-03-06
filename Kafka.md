<p align="center">
  <img src="https://files.svgcdn.io/logos/kafka.svg" width="175" height="100">
</p>

# What is Kafka ?

Apache Kafka is a **distributed streaming platform** used for building real-time data pipelines and applications, acting
as a high-throughput, low-latency platform for handling real-time data feeds.

## What is DLT ?

DLT stands for Dead Letter Topic, means If a message is not able to consume by consumer it send to DLT.

### Modules

| Name                | Description                                        |
|---------------------|----------------------------------------------------|
| **Producer**        | Publish a Message/Events                           |
| **Consumer**        | Consuming a Message/Events                         |
| **Broker**          | Distributed System (Available in multiple servers) |
| **Cluster**         | Kafka Server                                       |
| **Topic**           | Like Queue                                         |
| **Partitions**      | Spliting a Topic into multiple Partitions.         |
| **Offset**          | Index of the Messages called Offset number.        |
| **Consumer Groups** | Grouping the Consumers.                            |
| **Zookeeper**       | Managing a Kafka                                   |

### Elaborated:-

| Producer              | An application that publishes data (messages) to Kafka topics. It optimizes, serializes, and balances messages across partitions. |
|:----------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| **Consumer**          | An application that subscribes to Kafka topics and reads messages from partitions, typically within a consumer group.             |
| **Broker**            | A Kafka server that manages message storage and handles read/write requests. Brokers work together to form a Kafka cluster.       |
| **Topic**             | A logical channel that organizes messages. Producers write to topics, and consumers subscribe to them.                            |
| **Partition**         | A sub-division of a topic that enables parallel processing. Each partition is replicated across brokers for fault tolerance.      |
| **ZooKeeper / KRaft** | Coordinates and manages Kafka brokers and clusters, ensuring fault tolerance and leader elections for partitions.                 |
| **Replication**       | Ensures copies of partitions are maintained across different brokers to enhance fault tolerance and availability.                 |
| **Consumer Group**    | A group of consumers sharing the workload of processing messages from partitions of a topic, ensuring parallelism.                |
| **Leader**            | The broker responsible for handling all reads and writes for a partition. Each partition has one leader at any time.              |
| **Follower**          | Brokers that replicate data from the leader broker for redundancy and failover purposes.                                          |

---

Kafka is not a Queue it's a Log.
Topic is a durable log of events.
Log is a append only file, it append logs at end of the file.

Why Kafka is fast ?

Sequential I/O
Append only log as a primary Data structure

1. What is Replication factor in Kafka?
2. What is Leader/Follower concept in Kafka?

Kafka Retention Policy ?

Two Settings:

1. retention.ms (default 7 days) - how long to keep a message
2. retention.bytes (default 1GB) - when to start purging based on size

Kafka Data Structure

	1. Kafka stores a Events/Message in LOG.
	2. LOG is an ordered sequence of Events/Message.
	2. LOG is an ordered sequence of immutable Records.
	3. Topic is an ordered collection of Events/Message that stored in a Durable way.
	4. Events/Message are immutable.
	5. Logs. Not queues. (Kafka doesn't have queue. A topic is not a queue its a LOG)

Kafka Topic contains:

* Headers
* Key
* Value
* Timestamp

Log retention and compaction

Two Settings:

1. retention.ms (default 7 days) - how long to keep a message
2. retention.bytes (default 1GB) - when to start purging based on size

## Partitions:

1. Partitions are multiple log files inside one Topic.
2. Producing message if partition dosent specified, on round-robin message assigned to the partitions
3. Single Topic log splited into multiple logs called Partition.
4. If the message dosen't have key, the messages are distributed Round Robin across Partitions.
5. Kafka guarantees ordering only inside a partition.

## Brokers:

	1. A single Kafka server instance that stores data and serves client requests.
	2. Brokers are a Part of Kafka cluster, an instance ruuning in a single machine or pod.

## Replication:

1. Kafka uses **Leader–Follower** replication at partition level.
2. Each partition has exactly **one Leader and zero or more Followers**.
3. **All writes📝 happen only on the Leader** and Followers replicate data from the Leader.
4. If a Leader fails🔥, **Kafka elects a new Leader from the In-Sync Replicas (ISR)**.
5. By default, **consumers read from the Leader replica**.
6. Durability depends on replication factor, min.insync.replicas, and producer acks configuration.

## Producers:

1. Producers are client applications that publish (write) events to Kafka topics.
2. Kafka stores data as byte arrays, so producers use serializers to convert objects into bytes. Built-in serializers
   exist for primitive types like String, Integer, Long, Double, etc.
3. Kafka has built in serializers for primitive types, thinks like integer, long, double, string.
4. The producer client determines the target partition using a partitioner.
    - If a key is provided, it hashes the key to select a partition.
    - If no key is provided, it uses round-robin.

## Consumers:

1. Consumers are client applications that **subscribe to topics** and read records from assigned partitions.
2. **Consumers commit offsets** to Kafka (stored in `__consumer_offsets`) to track progress.
3. In Java, messages are represented as `ConsumerRecord` objects containing key, value, topic, partition, offset,
   timestamp, and headers.
4. KafkaConsumer is not thread-safe and should be used by a single thread.
5. Within a consumer group, each partition is consumed by only one consumer. Across different groups, the same message
   can be consumed multiple times independently.
6. `group.id` is required for coordinated partition assignment and parallel consumption within a consumer group.

## Schema Registry:

* It supports **JSON Schema, Avro, protobuf** Serialization formats.

## Kafka Connect:

* Kafka Connect is a integration API, really integrated with subsystem.

## Kafka Stream Processing:
