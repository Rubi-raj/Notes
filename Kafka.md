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
