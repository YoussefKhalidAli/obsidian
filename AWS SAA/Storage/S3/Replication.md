# **Amazon S3 Replication — Clean Explanation**

## 1️. Types of replication

### CRR (Cross-Region Replication)

- Replicates objects to a **different region**
- Use cases:
    - Disaster recovery
    - Compliance
    - Lower latency for global users

### SRR (Same-Region Replication)

- Replicates objects within the **same region**
- Use cases:
    - Log aggregation
    - Data syncing between accounts
    - Dev/Test environments

---

## 2️. Core Requirements (VERY IMPORTANT)

To enable replication:

- ✅ **Versioning must be enabled** on:
    - Source bucket
    - Destination bucket
- ✅ Proper **IAM role/permissions**:
    - S3 needs permission to:
        - Read from source
        - Write to destination

---

## 3️. How replication works

- **Asynchronous**
    - Happens in the background
    - Not immediate
- **Only new objects are replicated**
    - Existing objects are NOT copied automatically
- **Batch Replications**
	- Used to To replicate old data (enable)
	- Retry failed replications
    - Backfill data
- **No chaining rule**
	- Bucket A → Bucket B
	- Bucket B → Bucket C
	- Objects from A **will NOT go to C**
---

## 5️. Delete behavior (very important nuance)

### Delete markers
- Can be replicated (optional setting)

### Permanent deletes (version ID)
-  **NOT replicated**
- Prevent accidental or malicious deletions from spreading

---

## 6. Cross-account replication

- Supported
- Common for:
    - Backup accounts
    - Security isolation
    - Multi-team setups

---
## Key Points
- Versioning is REQUIRED
- Only **new objects** replicate
- Use **Batch Replication** for old objects
- No replication chaining
- Permanent deletes are NOT replicated