AWS Glue is a **fully managed, serverless ETL (Extract, Transform, Load) service** used to prepare data for analytics.

---

## 1. What is AWS Glue?

- Serverless ETL service
- Used to:
    - Extract data from sources
    - Transform data (clean, enrich, convert formats)
    - Load data into destinations

---

## 2. Main Use Cases

AWS Glue is commonly used for:

- Data migration (S3 → Redshift)
- Data transformation pipelines
- Converting data formats (CSV → Parquet)
- Preparing data for analytics services (Athena, Redshift)
- Building data lakes

---

## 3. ETL Workflow

Typical Glue pipeline:

1. **Extract**
    - Data from:
        - S3
        - RDS
        - DynamoDB
        - JDBC databases
2. **Transform**
    - Filter data
    - Clean data
    - Add or modify columns
    - Convert formats (e.g., CSV → Parquet)
3. **Load**
    - Output to:
        - Amazon S3
        - Amazon Redshift
        - Other destinations

---

## 4. Why Parquet Format Matters

- Columnar storage format
- Optimized for analytics (especially Athena)

### Benefits:

- Faster queries
- Lower cost (reads only required columns)
- Better compression

### Example Use Case:

- Convert CSV files in S3 → Parquet using Glue → Query with Athena efficiently

---

## 5. AWS Glue Data Catalog

Central metadata repository for AWS data sources.

### What it stores:

- Databases
- Tables
- Schemas
- Column definitions
- Data types

---

### Data Crawlers

Glue Crawlers:

- Automatically scan data sources
- Infer schema and structure
- Populate the Data Catalog

### Supported Sources:

- Amazon S3
- Amazon RDS
- Amazon DynamoDB
- JDBC databases (on-prem or external)

---

## 6. Why Data Catalog is Important

Used by multiple AWS services:

- Amazon Athena
- AWS Glue ETL jobs
- Amazon Redshift Spectrum
- Amazon EMR

It acts as a **central metadata layer**.

---

## 7. Glue ETL Job Automation

Common architecture:

- S3 event triggers upload
- Event sent to:
    - Lambda OR EventBridge
- Triggers Glue ETL job
- Data is processed and stored in destination

---

## 8. Glue Features

### 8.1 Glue Job Bookmarks

- Prevents reprocessing of already processed data
- Tracks job state between runs

---

### 8.2 AWS Glue DataBrew

- Visual tool for data cleaning
- No coding required
- Pre-built transformations

---

### 8.3 AWS Glue Studio

- Visual interface for building ETL pipelines
- Create, run, and monitor jobs

---

### 8.4 Glue Streaming ETL

- Real-time ETL processing
- Built on Apache Spark Structured Streaming

### Data Sources:

- Amazon Kinesis Data Streams
- Apache Kafka
- Amazon MSK (Managed Kafka)

---

## 9. Key Points

- AWS Glue = serverless ETL service
- Used for data preparation and transformation
- Core components:
    - ETL Jobs
    - Data Catalog
    - Crawlers
- Converts data into analytics-friendly formats (e.g., Parquet)
- Integrates with Athena, Redshift, EMR
- Supports both batch and streaming ETL
- Event-driven ETL pipelines are common (S3 → Lambda/EventBridge → Glue)