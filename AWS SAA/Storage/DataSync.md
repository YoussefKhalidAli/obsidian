## 1. What it is

A managed service used to **transfer and synchronize large amounts of data**:
- Between **on-premises and AWS**
- Between **AWS services**
- From **other clouds to AWS**

---

## 2. Supported Destinations
- Amazon S3 (all storage classes, including Glacier)
- Amazon EFS
- Amazon FSx

---

## 3. Supported Sources
- On-premises systems via:
    - NFS
    - SMB
    - HDFS
- Other cloud storage
- AWS storage services

---

## 4. Key Characteristics
### 4.1 Data Transfer
- High speed: up to **10 Gbps per task**
- Bandwidth can be limited if needed

### 4.2 Scheduling
- Not continuous replication
- Runs on a **schedule**:
    - Hourly
    - Daily
    - Weekly

---

## 5. Metadata & Permissions

- Preserves:
    - File permissions
    - Ownership
    - Timestamps
- Supports:
    - NFS (POSIX)
    - SMB permissions

---

## 6. DataSync Agent

### 6.1 Where it runs
- Installed near the data source
### 6.2 Role
- Connects to local storage
- Transfers data securely to AWS DataSync service
### 6.3 When required
- Needed when source is:
    - On-premises
    - Other cloud
## 6.4 No Agent Required
- When transferring **within AWS**:
    - S3 ↔ EFS
    - S3 ↔ FSx
    - EFS ↔ FSx

## 6.5 Direction of Sync
- One-way or two-way:
    - On-prem → AWS
    - AWS → on-prem
    - AWS ↔ AWS

## 6.6 Special Case: Limited Network
- Use AWS Snowcone
    - Comes with DataSync agent pre-installed
    - Move data physically, then sync into AWS

---

## 7. Common Use Cases
- Large-scale data migration
- Periodic data synchronization
- Backup and restore workflows
- Moving data between AWS storage services

---
## 8. Summary Points

- Fast, scheduled data transfer service
- Works across on-prem, AWS, and other clouds
- Preserves file metadata and permissions
- Requires agent for non-AWS sources
- No agent needed for AWS-to-AWS transfers