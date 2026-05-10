This section covers **specialized AWS databases** used for specific workloads beyond standard relational and NoSQL.

---

## 1. Amazon DocumentDB

Amazon DocumentDB is a **fully managed NoSQL document database** compatible with MongoDB.

**Explanation:** It is the AWS equivalent of MongoDB (like Aurora is for MySQL/PostgreSQL).

---

### Key Features

- MongoDB-compatible
- Stores **JSON-like documents**
- Fully managed & highly available
- Replicated across **3 AZs**
- Auto-scaling storage (10 GB increments)
- Handles **millions of requests/sec**

---

### Use Cases

- JSON/document-based apps
- Content management systems
- User profiles

---

### Tips

- **MongoDB → DocumentDB**
- **Document-based NoSQL → DocumentDB**
- Alternative: DynamoDB (but different model)

---

## 2. Amazon Neptune

Amazon Neptune is a **fully managed graph database**.

**Explanation:** Designed for **highly connected data** (relationships).

---

### Key Features

- Graph model (nodes + relationships)
- Replicated across **3 AZs**
- Up to **15 read replicas**
- Handles **billions of relationships**
- Millisecond query latency

---

### Use Cases

- Social networks
- Recommendation engines
- Fraud detection
- Knowledge graphs

---

### Neptune Streams

- Real-time stream of DB changes
- Ordered & no duplicates
- Accessible via REST API

**Use Cases:**

- Notifications
- Data replication
- Sync with other systems

---

### Tips

- **Graph data → Neptune**
- **Highly connected data → Neptune**

---

## 3. Amazon Keyspaces (for Apache Cassandra)

Amazon Keyspaces is a **managed Apache Cassandra database**.

**Explanation:** AWS version of Cassandra (distributed NoSQL DB).

---

### Key Features

- Serverless & fully managed
- Cassandra-compatible (CQL)
- Replication across **3 AZs**
- Single-digit ms latency
- Auto-scaling

---

### Capacity Modes

- On-Demand
- Provisioned (with auto-scaling)

---

### Use Cases

- IoT data
- Time-series workloads
- High-write applications

---

### Tips

- **Apache Cassandra → Keyspaces**
- **Distributed NoSQL → Keyspaces**

---

## 4. Amazon Timestream

Amazon Timestream is a **serverless time-series database**.

**Explanation:** Optimized for **data with timestamps**.

---

### Key Features

- Stores **time-based data**
- Scales automatically
- Handles **trillions of events/day**
- SQL querying supported
- Built-in analytics

---

### Storage Tiers

- **Memory store** → recent data (fast)
- **Magnetic store** → historical data (cheap)

---

### Use Cases

- IoT applications
- Monitoring systems
- Real-time analytics

---

### Integrations

- Ingest:
    - Kinesis
    - IoT
    - Lambda
- Query/visualize:
    - QuickSight
    - Grafana
    - SageMaker

---

### Tips

- **Time-series data → Timestream**
- **Metrics / timestamps → Timestream**

---

##  Comparison Cheat Sheet

|Use Case|Service|
|---|---|
|JSON / MongoDB|DocumentDB|
|Graph / relationships|Neptune|
|Cassandra workloads|Keyspaces|
|Time-series data|Timestream|

---

## Key Points

- **MongoDB → DocumentDB**
- **Graph → Neptune**
- **Cassandra → Keyspaces**
- **Time-series → Timestream**