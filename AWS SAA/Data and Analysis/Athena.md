Amazon Athena is a **serverless SQL query service** used to analyze data directly in **Amazon S3** without moving it.
**Explanation:** You run SQL queries on files stored in S3 using a managed engine (Presto-based).

---

## 1. Core Concept

S3 Data → Athena → SQL Query → Results

**Explanation:** Athena queries data **in-place inside S3** (no loading into a database).

---

## 2. Key Features

- Serverless (no infrastructure)
- Uses standard SQL
- No data movement required
- Pay per data scanned
- Built on Presto engine

---

## 3. Supported Data Formats

- CSV
- JSON
- Avro
- ORC
- Parquet

**Explanation:** Works best with optimized formats like Parquet.

---

## 4. Pricing Model

- Pay per **TB of data scanned**

**Explanation:** Less data scanned = cheaper queries.

---

## 5. Common Use Cases

- Log analysis (VPC Flow Logs, CloudTrail, ALB logs)
- Business intelligence
- Ad-hoc queries
- Data analytics on S3
- Reporting dashboards

---

## 6. Performance Optimization (VERY IMPORTANT)

### 6.1 Use Columnar Formats

Best formats:

- Parquet
- ORC

**Why:**

- Only scan required columns
- Reduces cost & improves speed

---

### 6.2 Compression

- Compress files to reduce scanned data

---

### 6.3 Partitioning (VERY IMPORTANT)

Organize S3 like:

s3://bucket/year=2024/month=01/day=01/

**Why:**

- Athena only scans relevant folders
- Massive performance improvement

---

### 6.4 Avoid Small Files

- Many small files = slow queries
- Prefer large files (≥128MB)

---

## 7. Data Preparation Tools

- AWS Glue

**Use Case:**

- Convert:
    - CSV → Parquet
    - JSON → ORC

---

## 8. Federated Queries (Advanced Feature)

Allows Athena to query **outside S3**.

### How it works:

- Uses Lambda-based connectors
- AWS Lambda acts as connector layer

---

### Can query:

- Amazon DynamoDB
- Amazon RDS
- Amazon Redshift
- CloudWatch Logs
- On-prem databases

**Explanation:** Athena becomes a **unified query engine across multiple sources**.

---

## 9. Query Results Storage

- Results stored in Amazon S3
- Can be reused for analytics tools

---

## 10. Athena + QuickSight

- Amazon QuickSight connects to Athena

Flow:  
S3 → Athena → QuickSight → Dashboards

---

## Key Points

- **SQL on S3 → Athena**
- **Serverless analytics → Athena**
- **Pay per scan → Athena**
- **Best formats → Parquet / ORC**
- **Optimize cost → partitioning**
- **ETL conversion → AWS Glue**
- **Cross database queries → Federated Queries**
- **BI dashboards → QuickSight + Athena**
- **No infrastructure → Athena**