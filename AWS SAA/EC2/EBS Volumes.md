## 1. Elastic Block Store (EBS) Overview

**Definition:**  
EBS stands for **Elastic Block Store**. It is a **network-attached storage** that can be **attached to EC2 instances**.  

### 1.1 Key Characteristics

- **Persistence:** Data persists **even after the EC2 instance is terminated**.  
- **Single Attachment:** At the **Certified Cloud Practitioner level**, an EBS volume can only be **mounted to one instance at a time**.  
- **AZ-Bound:** EBS volumes are **tied to a specific Availability Zone (AZ)**.  
  - Example: An EBS volume in `us-east-1a` cannot attach to an EC2 instance in `us-east-1b`.  
- **Provisioned:** You must specify:  
  - **Size** (GB)  
  - **IOPS** (Input/Output operations per second, for performance)  
- **Network Drive:** Acts like a **network USB stick**; communication happens over the network (some latency possible).  

---

## 2. EBS Operations

### 2.1 Attach / Detach

- EBS volumes can be **detached from one instance and attached to another** quickly.  
- This is useful for **failover scenarios** or maintaining persistent data.  
- **Multiple EBS volumes** can be attached to a single EC2 instance.  
- Volumes can also remain **unattached** until needed.  

### 2.2 Snapshots

- Snapshots allow you to **move data across AZs or regions**.  
- Snapshots are stored in **S3**, not bound to a single AZ.  
- You can **create a new EBS volume from a snapshot** in any AZ.  

### 2.3 Delete on Termination

- Controls whether an EBS volume is **deleted when the EC2 instance is terminated**.  
- **Root Volume:** `Delete on termination` is **enabled by default**.  
- **Additional Volumes:** `Delete on termination` is **disabled by default**.  
- Can be manually enabled/disabled in the console.  .  

---
## 3. EBS Snapshots  
- **Definition:** Point-in-time **backup** of an EBS volume.  
- **Detachment not required**, but recommended for consistent backup.  
- Can **restore to another AZ** or **copy across regions** → enables migration.  
  
### Features  
1. **Snapshot Archive**  
- Move snapshot to **archive tier** → up to **75% cheaper**.  
- Restore takes **24–72 hours** → not instant.  
  
2. **Recycle Bin**  
- Deleted snapshots go to **Recycle Bin** → recoverable.  
- Retention configurable: **1 day – 1 year**.  
  
3. **Fast Snapshot Restore (FSR)**  
- Pre-initializes snapshot → **no latency on first use**.  
- Useful for **large snapshots** or fast instance creation.  
- **High cost** → use judiciously.  
  
### Practical Notes  
- Snapshots are **incremental** → only changed blocks are stored.  
- Stored in **S3-managed storage**, not directly accessible.  
- Use for **disaster recovery, backup, and migration**.

---

## 4. EBS + EC2 Layout (Diagram)

```text
Availability Zone: us-east-1a
---------------------------------
EC2 Instance 1
  ├─ EBS Volume 1 (root)
  └─ EBS Volume 2 (additional)
  
EC2 Instance 2
  └─ EBS Volume 3 (root)
  
Notes:
- Each volume tied to a single AZ.
- Root volume delete-on-termination = enabled by default.
- Additional volumes can be attached/detached as needed.
```

## 5. Use Cases
- Persist data beyond instance lifecycle
- Failover scenarios (detach & reattach to another instance)
- Multi-volume setups (database logs, application storage)
- Snapshot-based migrations across AZs or regions

## 6. Key Points
- EBS is AZ-bound, cannot attach across AZs without a snapshot.
- Delete on termination = controls whether root/additional volumes are deleted.
- Snapshots = cross-AZ / cross-region, useful for backup & recovery.
- Multiple EBS volumes can attach to a single EC2 instance, but a single EBS cannot attach to multiple instances at the CCP level.