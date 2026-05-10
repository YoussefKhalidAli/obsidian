Amazon QuickSight is a **serverless, cloud-based Business Intelligence (BI) service** used to create **interactive dashboards and visualizations** from data.

---

## 1. What is Amazon QuickSight?

- A **serverless BI service**
- Used to build **interactive dashboards**
- Connects to multiple data sources
- Fully managed and automatically scales

---

## 2. Key Features

- Serverless (no infrastructure management)
- Fast and scalable dashboards
- Pay-per-session pricing model
- Can be embedded into web applications
- Supports ad-hoc data exploration and visualization

---

## 3. Use Cases

- Business analytics and reporting
- Data visualization dashboards
- Ad-hoc data analysis
- Business intelligence insights
- KPI and performance tracking

---

## 4. Data Sources Integration

Amazon QuickSight can connect to:

### AWS Data Sources

- Amazon RDS
- Amazon Aurora
- Amazon Redshift
- Amazon Athena (S3-based queries)
- Amazon S3
- Amazon OpenSearch Service
- Amazon Timestream

---

### Third-Party SaaS Sources

- Salesforce
- Jira
- Other supported SaaS applications

---

### On-Premises / External Databases

- Teradata
- JDBC-compatible databases

---

### File-Based Imports

- CSV
- Excel
- JSON
- TSV
- Log files (CLF format)

---

## 5. SPICE Engine

SPICE = **Super-fast, Parallel, In-memory Calculation Engine**

### Key Points:

- Used when data is **imported into QuickSight**
- Provides **in-memory processing**
- Enables **fast dashboard performance**
- Does NOT apply when directly querying external databases

---

## 6. Analysis vs Dashboard

### 6.1 Analysis

- Workspace for building visualizations
- Used to create charts, filters, and metrics
- Editable and interactive
- Can be shared

---

### 6.2 Dashboard

- Read-only snapshot of an analysis
- Preserves:
    - Filters
    - Layout
    - Visualizations
- Used for sharing insights

---

## 7. Users and Groups

### Key Points:

- QuickSight has its own **internal users and groups**
- These are NOT IAM users

### Availability:

|Feature|Edition|
|---|---|
|Users|Standard + Enterprise|
|Groups|Enterprise only|

---

## 8. Security Features

### Column-Level Security (CLS)

- Available in **Enterprise edition**
- Restricts access to specific columns
- Useful for sensitive data control

---

## 9. Sharing Model

- You publish dashboards or analyses
- Share with:
    - Specific users
    - Groups
- Users can view dashboards based on permissions

---

## 10. Key Takeaways

- QuickSight = **serverless BI dashboard service**
- Uses **SPICE engine for in-memory speed**
- Connects to AWS, SaaS, and on-prem data sources
- Dashboards = read-only views
- Analysis = editable workspace
- Users/groups are **native to QuickSight (not IAM)**
- Enterprise edition adds advanced security like CLS