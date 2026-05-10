## What is Amazon MSK?

Amazon Managed Streaming for Apache Kafka (MSK) is a **fully managed service that runs Apache Kafka on AWS**.

Kafka is an open-source platform used for **real-time data streaming**, similar in purpose to Amazon Kinesis.

MSK allows you to:
- Create Kafka clusters
- Update clusters
- Delete clusters
- Without managing the underlying infrastructure manually

---

## What is Apache Kafka?

Apache Kafka is a distributed streaming platform used to:

- Ingest real-time data
- Store streaming data
- Process streaming data

---

## Kafka Architecture

A Kafka cluster is composed of:

### 1. Brokers
- Servers that store and manage data
- Handle read/write operations

### 2. Topics
- Logical channels where data is sent
- Data is organized into topics

### 3. Partitions
- Each topic is split into partitions for scalability
- Enables parallel processing

### 4. Producers
- Applications that send data into Kafka topics

### 5. Consumers
- Applications that read data from Kafka topics

---

## How MSK Works

Amazon MSK manages:

- Kafka broker nodes
- ZooKeeper nodes (for cluster coordination)
- Scaling and recovery
- Deployment across multiple Availability Zones (up to 3 AZs)
- Storage using Amazon EBS volumes

---

## MSK Serverless

Amazon MSK also offers a **serverless mode** where:

- You do not provision or manage capacity
- AWS automatically scales compute and storage
- You pay only for usage

---

## MSK vs Kinesis Data Streams

| Feature | Amazon Kinesis Data Streams | Amazon MSK (Kafka) |
|----------|----------------------------|--------------------|
| Core concept | Shards | Topics + Partitions |
| Scaling | Shard split/merge | Add partitions only |
| Remove capacity | Yes (merge shards) | No |
| Message retention | Limited (hours to days, configurable) | Long-term (as long as EBS storage allows) |
| Max message size | ~1 MB (default) | Configurable (e.g., 10 MB+) |
| Encryption in transit | Yes | TLS or plaintext |
| Storage model | Managed by Kinesis | EBS-backed Kafka cluster |

---

## Scaling Differences

### Kinesis
- Scale by splitting or merging shards

### Kafka (MSK)
- Scale by adding partitions only
- Cannot reduce partitions

---

## Data Retention

- Kinesis: limited retention period
- MSK: long-term retention (can exceed 1 year depending on EBS storage)

---

## Data Flow

### Producers
Send data into Kafka topics.

### Kafka Topics
Store streaming data in partitions across brokers.

### Consumers
Read and process data from topics.

---

## Integration Options (Consumers)

Amazon MSK can integrate with:

- Amazon Managed Service for Apache Flink (real-time processing)
- AWS Glue Streaming ETL (Spark Streaming)
- AWS Lambda (event-driven processing)
- Amazon EC2 (custom Kafka consumers)
- Amazon ECS / EKS (container-based consumers)
- Amazon S3, EMR, SageMaker, RDS (downstream analytics/storage)

---

## Key Features

- Fully managed Kafka clusters
- High availability across multiple AZs
- Automatic failure recovery
- EBS-backed storage
- Optional serverless deployment

---

## Key Points

- MSK = Managed Kafka on AWS
- Alternative to Kinesis Data Streams
- Uses topics and partitions (not shards)
- Cannot reduce partitions (only increase)
- Supports long-term data retention
- Runs across multiple AZs for high availability
- Integrates with Flink, Glue, Lambda, and EC2 consumers