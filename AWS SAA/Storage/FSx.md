## What is Amazon FSx?
- Fully managed service to run **high-performance file systems on AWS**
    - **RDS → databases**
    - **FSx → file systems**

Supports popular third-party file systems:
- Windows File Server
- Lustre
- NetApp ONTAP
- OpenZFS

---

# 1. FSx for Windows File Server

## 1.1 Features

- Fully managed **Windows file share**
- Protocol: **SMB**
- File system: **NTFS**
- Integrates with **Microsoft Active Directory**
- Supports:
    - ACLs (permissions)
    - User quotas
- Can be mounted on:
    - Windows
    - Linux EC2
- Integrates with on-prem via **DFS (Distributed File System)**

## 1.2 Performance
- Millions of IOPS
- Tens of GB/s throughput
- Hundreds of PB storage

## 1.3 Storage Options
- SSD → low latency workloads (DB, analytics)
- HDD → cheaper (home dirs, CMS)

## 1.4 Extras
- Multi-AZ support
- Daily backups to S3
- Access from on-prem (VPN / Direct Connect)

---

# 2. FSx for Lustre

## What is Lustre?
- Distributed file system for:
    - **HPC (High Performance Computing)**
    - Machine Learning
    - Big data workloads
	- HPC = FSx for Lustre

## 1.1 Use Cases
- Video processing
- Financial modeling
- EDA (engineering workloads)

## 1.2 Performance
- Hundreds of GB/s throughput
- Millions of IOPS
- Sub-ms latency

## 1.3 Storage
- SSD → low latency, random I/O
- HDD → large sequential workloads

## 1.4 S3 Integration (VERY IMPORTANT)
- Read data from S3 as file system
- Write results back to S3

## 1.5 Deployment Types
### 1.5.1 Scratch File System

- Temporary
- No replication
- 6x faster
- Cheapest

Use case:
- Short-term processing

### 1.5.2 Persistent File System
- Long-term storage
- Data replicated (within same AZ)
- Self-healing

Use case:
- Critical / sensitive data
### 1.5.3 Key Rule
- **Scratch = speed**
- **Persistent = durability**

---

# 3. FSx for NetApp ONTAP

##  What is it?
- Managed **NetApp ONTAP** file system

## 3.1 Protocols
- NFS
- SMB
- iSCSI
 Very flexible

## 3.2 Use Case
- Migrate existing **ON-PREM NAS / ONTAP workloads to AWS**

## 3.3 Features
- Auto scaling (grow/shrink)
- Snapshots & replication
- Compression + **deduplication**
- Point-in-time cloning

---

# 4. FSx for OpenZFS

## What is it?
- Managed **ZFS file system**

## 4.1 Protocol
- NFS only

## 4.2 Use Case
- Migrate ZFS workloads to AWS

## 4.3 Performance
- Up to 1M IOPS
- < 0.5 ms latency

## 4.4 Features
- Snapshots
- Compression
- Point-in-time cloning

> No deduplication (important difference from ONTAP)


# 5. Quick Comparison

|FSx Type|Protocols|Best For|Key Feature|
|---|---|---|---|
|Windows|SMB|Windows apps, AD integration|NTFS + AD|
|Lustre|POSIX (HPC)|ML / HPC|S3 integration|
|ONTAP|NFS/SMB/iSCSI|Enterprise NAS migration|Dedup + clone|
|OpenZFS|NFS|ZFS workloads|High performance|

---

# 6. Key Points

- **HPC / ML / Big data → FSx Lustre**
- **Windows + AD → FSx Windows**
- **Dedup + cloning → FSx ONTAP**
- **ZFS workload → FSx OpenZFS**
- **Temporary fast storage → Lustre Scratch**
- **Durable storage → Lustre Persistent**