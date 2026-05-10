Amazon OpenSearch Service is a **distributed search and analytics engine** used for **full-text search, log analytics, and observability**.
**Explanation:** It is mainly used to add **powerful search capabilities (including partial matching)** on top of application data.

---

## 1. Core Concept

- Search + analytics engine
- Built for **fast text search and log analysis**
- Successor of Elasticsearch service

---

## 2. Key Feature: Full-Text Search

Unlike databases like DynamoDB:

- Supports partial matches
- Searches across multiple fields
- Relevance-based search results

**Example:**

- Search “iph” → returns “iPhone”

---

## 3. Common Use Cases

- Application search (product search, websites)
- Log analytics
- Monitoring and observability
- Security analytics
- Real-time dashboards

---

## 4. Deployment Modes

### 4.1 Managed Cluster

- You provision actual nodes
- You manage scaling configuration
- Traditional infrastructure model

---

### 4.2 Serverless Mode

- Fully managed scaling
- No infrastructure management
- AWS handles capacity automatically

---

## 5. Query Language

- Uses OpenSearch query DSL (JSON-based)
- Optional SQL support via plugin

---

## 6. Data Ingestion Sources

OpenSearch can ingest data from:

- Amazon Kinesis Data Firehose
- Amazon Kinesis Data Streams
- Amazon CloudWatch Logs
- AWS Lambda
- Custom applications

---

## 7. Security Features

- IAM authentication
- Integration with Amazon Cognito
- Encryption at rest
- Encryption in transit

---

## 8. Visualization Layer

- OpenSearch Dashboards (like Kibana)
- Used for:
    - Charts
    - Dashboards
    - Log visualization

---

## 9. Common Architecture Patterns

### 9.1 DynamoDB + OpenSearch (VERY IMPORTANT)

DynamoDB → Stream → Lambda → OpenSearch

Flow:

- Data stored in DynamoDB
- Stream triggers Lambda
- Lambda indexes data into OpenSearch
- OpenSearch handles search queries

---

### 9.2 Search + Retrieve Pattern

1. Search in OpenSearch
2. Get matching IDs
3. Fetch full data from DynamoDB

**Why:** OpenSearch = search layer, not source of truth

---

## 10. Log Ingestion Patterns

### 10.1 CloudWatch Logs → OpenSearch

- Subscription Filter → Lambda → OpenSearch  
    or
- Subscription Filter → Firehose → OpenSearch

---

### 10.2 Kinesis → OpenSearch

Option A:  
Kinesis Streams → Lambda → OpenSearch

Option B:  
Kinesis Firehose → OpenSearch

---

## 11. Firehose vs Streams

- Firehose → easier, near real-time, managed delivery
- Streams → real-time, requires Lambda consumer

---

## 12. Key Takeaways

- OpenSearch = **search engine, not database replacement**
- Best for:
    - Full-text search
    - Log analytics
    - Real-time dashboards
- Works alongside DynamoDB, S3, and Kinesis

---

## Key Points

- **Search functionality → OpenSearch**
- **Partial match search → OpenSearch**
- **Logs + dashboards → OpenSearch**
- **DynamoDB + search layer → OpenSearch**
- **Streaming ingestion → Kinesis / CloudWatch Logs**
- **Visualization → OpenSearch Dashboards**
- **Not a primary database → OpenSearch**