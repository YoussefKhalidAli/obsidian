## **Core Idea**

Amazon Kinesis Data Streams is a **real-time data streaming service** used to ingest, store, and process data as it is generated.

The key concept is **real-time processing**, meaning data is handled immediately as it arrives rather than being stored and processed later in batches.

---

## **What “Streaming Data” Means**

Streaming data is continuously generated data such as:

- Website clickstreams (user clicks, page views)
- IoT device data (sensors, connected devices)
- Application logs and metrics
- Financial transactions
- Gaming events

This data is valuable because it can be processed **instantly for analytics, monitoring, or reactions**.

---

## **Architecture Overview**

### **1. Producers (Data Sources)**

Producers send data into Kinesis Data Streams.

Examples:

- Custom applications (you write code for this)
- Kinesis Agent installed on servers (for logs/metrics)
- IoT devices or web applications

Producers push data **continuously in real time**.

---

### **2. Kinesis Data Stream**

This is the core service that:

- Receives streaming data
- Stores it temporarily
- Makes it available for multiple consumers

Important behavior:

- Data is **persisted (not immediately consumed and deleted)**
- Data can be **replayed by consumers**

---

### **3. Consumers (Processing Systems)**

Consumers read and process the data in real time.

Examples:

- Custom applications (you write code)
- AWS Lambda functions
- Amazon Managed Service for Apache Flink (stream analytics)
- Amazon Kinesis Data Firehose (delivery to storage systems)

---

## **Key Features**

### **Data Retention**

- Default: 24 hours
- Maximum: up to 365 days

Because data is stored temporarily:

- Consumers can **reprocess or replay data**
- Data is automatically deleted after retention period

### **Data Size Limits**

- Each record can be up to **10 MB**
- Best practice: many small real-time events, not large files
## **Ordering**

- Ordering is guaranteed **within a shard using a partition key**
- Same partition key → ordered stream of events

### **Security**

- Encryption in transit (HTTPS)
- Encryption at rest (AWS KMS)

---

## **Kinesis Producer & Consumer Libraries**

### **KPL (Kinesis Producer Library)**

Used to optimize producers:

- Efficient batching
- Higher throughput ingestion

### **KCL (Kinesis Client Library)**

Used to optimize consumers:

- Manages shard consumption
- Handles scaling and checkpointing

---

## **Shards (Very Important Concept)**

A **shard** is the basic throughput unit of Kinesis Data Streams.

### **Capacity per shard**

- Ingest:
    - 1 MB/sec OR 1000 records/sec
- Read:
    - 2 MB/sec

### **Scaling**

- More shards = more throughput
- Example:
    - 10 shards → 10 MB/sec ingestion capacity

### **Provisioned Mode**

- You manually choose number of shards
- You pay per shard per hour
- You scale up/down manually

---

## **On-Demand Mode**

No manual shard management.

### **How it works**

- AWS automatically scales based on traffic
- Baseline capacity:
    - ~4,000 records/sec or 4 MB/sec ingestion
- Scaling based on past usage patterns (up to ~30 days)

### **Billing**

- Pay per data volume ingested and processed
- No need to manage shards

---

## **Kinesis Data Streams vs Batch Systems**

|Feature|Kinesis Data Streams|
|---|---|
|Processing type|Real-time|
|Storage|Temporary (retained)|
|Reprocessing|Yes (replay possible)|
|Scaling|Shards or on-demand|
|Use case|Streaming analytics, real-time reactions|

---

## **Key Points**

- Use Kinesis Data Streams when you see:
    - “real-time data”
    - “streaming analytics”
    - “clickstream / IoT / logs”
- Data is:
    - stored temporarily
    - replayable
- Throughput depends on:
    - number of shards
- Consumers:
    - Lambda
    - Flink
    - custom apps
    - Firehose (for delivery)
- Partition key controls ordering