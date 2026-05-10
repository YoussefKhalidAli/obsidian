# Amazon Managed Service for Apache Flink

## What is it?

Amazon Managed Service for Apache Flink is a fully managed service for running **Apache Flink applications on AWS**.

It was previously called:
- Amazon Kinesis Data Analytics for Apache Flink

Now it is renamed to:
- Amazon Managed Service for Apache Flink

---

## What is Apache Flink?

Apache Flink is an open-source framework used for:

- Real-time stream processing
- Event-driven applications
- Continuous data transformations

It supports programming in:

- Java
- Scala
- SQL

---

## Core Idea

The service allows you to run Flink applications without managing infrastructure.

AWS handles:

- Cluster provisioning
- Scaling
- High availability
- Fault tolerance
- Backups (via checkpoints and snapshots)

---

## Data Sources

Amazon Managed Service for Apache Flink can process streaming data from:

- Amazon Kinesis Data Streams
- Amazon MSK (Managed Kafka)

---

## Important Exam Point

It **cannot read directly from Amazon Kinesis Data Firehose**.

This is a common exam trick.

---

## How It Works

1. Data streams into a source (Kinesis or Kafka/MSK)
2. Flink application processes the stream in real time
3. Output is sent to downstream systems (e.g., S3, databases, analytics tools)

---

## Key Features

### 1. Fully Managed
- No need to manage servers or clusters
- AWS handles scaling and infrastructure

### 2. Real-Time Processing
- Processes data continuously as it arrives

### 3. Flexible Transformations
You can:
- Filter data
- Aggregate streams
- Join streams
- Perform complex event processing

### 4. Fault Tolerance
- Uses checkpoints and snapshots
- Allows recovery from failures

---

## When to Use It

Use Amazon Managed Service for Apache Flink when you need:

- Real-time analytics
- Stream processing
- Event-driven applications
- Continuous data transformations

---

## Key Points

- Used for real-time stream processing
- Based on Apache Flink
- Supports Java, Scala, SQL
- Reads from Kinesis Data Streams and MSK
- Does NOT read from Kinesis Data Firehose
- Fully managed (no infrastructure management)