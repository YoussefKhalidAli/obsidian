Amazon DynamoDB is a **fully managed, serverless NoSQL database** designed for **high performance and massive scale**.

**Explanation:** Unlike traditional databases, DynamoDB automatically scales and delivers **single-digit millisecond latency**.

---

## 1. Key Characteristics

- Fully managed (no servers, no maintenance)
- Highly available (multi-AZ replication)
- NoSQL (schema-less)
- Auto-scaling built-in
- Integrated with IAM for security

**Explanation:** DynamoDB is optimized for **scalability, speed, and flexibility**.

---

## 2. Core Concepts

### 2.1 Tables, Items, Attributes

- **Table** → collection of data
- **Item** → row
- **Attribute** → column (flexible)

**Important:**

- No fixed schema
- Attributes can change per item

---

### 2.2 Primary Key

Two types:

1. **Partition Key (PK)**
    - Unique identifier
2. **Composite Key (PK + Sort Key)**
    - Enables sorting and grouping

**Explanation:** Key design is critical for performance.

---

### 2.3 Data Types

- Scalar: String, Number, Boolean, Binary
- Document: List, Map
- Set types

---

### 2.4 Limits

- Max item size: **400 KB**

**Explanation:** Not suitable for large files → use S3 instead.

---

## 3. Capacity Modes (VERY IMPORTANT)

### 3.1 Provisioned Mode

- Define:
    - **RCU** (Read Capacity Units)
    - **WCU** (Write Capacity Units)
- Supports **Auto Scaling**

**Use Cases:**

- Predictable workloads
- Cost optimization

---

### 3.2 On-Demand Mode

- No capacity planning
- Auto scales instantly
- Pay per request

**Use Cases:**

- Unpredictable traffic
- Sudden spikes

---

## 4. Table Classes

- **Standard** → frequent access
- **Infrequent Access (IA)** → lower cost for rarely used data

---

## 5. When to Use DynamoDB

- Massive scale (millions of requests/sec)
- Flexible schema
- Low latency (real-time apps)

**Explanation:** Ideal for modern, high-performance applications.

---

# Advanced Features

---

## 6. DynamoDB Accelerator (DAX)

DynamoDB Accelerator is an **in-memory cache for DynamoDB**.

- Microsecond latency
- Fully managed
- No code changes required

**Use Case:**

- Read-heavy workloads

**Important:**

- Used specifically with DynamoDB
- Not a replacement for ElastiCache

---

## 7. DynamoDB Streams

- Captures changes:
    - INSERT
    - UPDATE
    - DELETE
- Retention: **24 hours**

**Use Cases:**

- Trigger AWS Lambda
- Real-time analytics
- Event-driven architecture

---

## 8. Streams with Kinesis

Instead of native streams, you can use:

- Amazon Kinesis Data Streams

**Benefits:**

- Up to **1 year retention**
- More consumers
- Advanced processing

---

## 9. Global Tables

- Multi-region replication
- **Active-Active** setup
- Low latency worldwide

**Requirement:**

- Uses DynamoDB Streams internally

**Use Case:**

- Global applications

---

## 10. Time To Live (TTL)

- Automatically deletes expired items

**Use Cases:**

- Session data
- Temporary data
- Compliance (auto-delete after X time)

---

## 11. Backups & Recovery

### 11.1 Point-In-Time Recovery (PITR)

- Continuous backup (up to 35 days)
- Restore to any point

### 11.2 On-Demand Backup

- Manual backups
- Stored until deleted

**Important:**

- Restore always creates a **new table**

---

## 12. DynamoDB + S3 Integration

### Export to S3

- Requires PITR
- No impact on performance

**Use Cases:**

- Analytics (Athena)
- Archiving

---

### Import from S3

- Formats: CSV, JSON, ION
- Creates a **new table**

---

## 13. Key Takeaways

- DynamoDB = **serverless NoSQL at massive scale**
- Best for:
    - High throughput apps
    - Flexible schema
    - Low latency systems

---

## Key Points

- **Need flexible schema → DynamoDB**
- **Need massive scale → DynamoDB**
- **Unpredictable traffic → On-Demand mode**
- **Read-heavy → DAX**
- **Event-driven → Streams + Lambda**
- **Global app → Global Tables**
- **Temporary data → TTL**
- **Large files → NOT DynamoDB (use S3)**