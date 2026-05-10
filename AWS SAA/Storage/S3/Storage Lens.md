## 1. What is S3 Storage Lens?

**S3 Storage Lens** is a service used to:
- Understand
- Analyze
- Optimize

---

## 2. Key Capabilities
- Detect **anomalies**
- Identify **cost savings opportunities**
- Enforce **data protection best practices**
- Provide **centralized visibility** across:
    - Organization
    - Accounts
    - Regions
    - Buckets
    - Prefixes
- Reports can be exported to S3 in:
    - CSV
    - Parquet


---

## 3. Data Aggregation Levels
Storage Lens can aggregate metrics at:
- Organization level
- Account level
- Region level
- Bucket level
- Prefix level

---

## 4. Dashboards
### 4.1 Default Dashboard
- Automatically created
- Covers:
    - Multiple accounts
    - Multiple regions
- Shows:
    - Total storage
    - Object count
    - Average object size
    - Usage trends
- Cannot be deleted
- Can be **disabled**

### 4.2 Custom Dashboards

- You can create your own dashboards
- Filter by:
    - Region
    - Account
    - Bucket
    - Storage class

---

## 5. Types of Metrics

### 5.1 Summary Metrics
- Total storage (bytes)
- Object count

 Use Case:
- Detect unused or fast-growing buckets

### 5.2 Cost Optimization Metrics

- Non-current version storage
- Incomplete multipart uploads

 Use Case:
- Reduce storage costs
- Clean unused data
- Move data to cheaper storage classes

### 5.3 Data Protection Metrics
- Versioning enabled buckets
- MFA delete enabled
- SSE-KMS encryption usage
- Replication rules

Use Case:
- Identify non-compliant buckets

---

### 5.4 Access Management Metrics
- Ownership settings

Use Case:
- Understand access configuration

### 5.5 Event Metrics
- S3 Event Notifications usage

### 5.6 Performance Metrics
- Transfer Acceleration usage

### 5.7 Activity Metrics
- GET requests
- PUT requests
- Data transfer (bytes)

### 5.8 HTTP Status Code Metrics
- 200 OK
- 403 Forbidden

Use Case:
- Analyze errors and access patterns

---

## 6. Free vs Advanced Metrics

| Feature                    | Free        | Advanced (Paid) |
| -------------------------- | ----------- | --------------- |
| Enabled by default         | ✅           | ❌               |
| Metrics                    | Basic (~28) | Detailed        |
| Data retention             | 14 days     | 15 months       |
| Activity metrics           | ❌           | ✅               |
| Prefix-level metrics       | ❌           | ✅               |
| Cost optimization insights | Basic       | Advanced        |
| Data protection insights   | Basic       | Advanced        |
| CloudWatch integration     | ❌           | ✅               |

---

## 7. Key Takeaways

- Centralized S3 analytics across **entire organization**
- Default dashboard = **multi-account + multi-region**
- Helps with:
    - Cost optimization
    - Security compliance
    - Usage analysis
- Advanced metrics = **paid but more powerful**
- Data can be exported for further analysis