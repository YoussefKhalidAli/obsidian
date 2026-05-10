
- **Hybrid cloud =**
    - Part of infra on AWS ☁️
    - Part on-prem 🏢

## 1. Why use it?

- Gradual cloud migration
- Compliance / security constraints
- Keep steady workloads on-prem
- Use AWS for scalability (elastic workloads)

---

# 2. What is AWS Storage Gateway?

**Bridge between on-premises and AWS storage**
- Lets on-prem apps use AWS storage seamlessly
- Converts **local protocols → AWS storage APIs**

---

# 3. Storage Types in AWS (Big Picture)
- Block → EBS
- File → EFS / FSx
- Object → S3 / Glacier

 Storage Gateway mainly bridges **on-prem ↔ S3 (and Glacier)**

---

# 4. Types of Storage Gateway

## 4.1 S3 File Gateway

## 4.1.1 What it does
- Exposes **S3 as a file system**
- On-prem apps think it's a normal file share
## 4.1.2 Protocols
- NFS (Linux)
- SMB (Windows)

## 4.1.3 How it works
- File Gateway translates:
    - NFS / SMB → HTTPS → S3

## 4.1.4 Storage
- Data stored in S3 (Standard, IA, Intelligent-Tiering, etc.)
- Not directly Glacier (but can via lifecycle policy)

## 4.1.5 Key Feature
- **Local cache** → frequently accessed files are cached on-prem

## 4.1.6 Extras
- IAM roles for access
- SMB supports Active Directory authentication

## 4.1.7 Use Case
- Access S3 from on-prem as file share

---

# 4.2 Volume Gateway

## 4.2.1 What it does
- Provides **block storage (like disks)** on-prem

## 4.2.2 Protocol
- iSCSI

## 4.2.3 Backed by
- S3 + EBS snapshots

### 4.2.4 Cached Volumes
- Most data in S3
- Frequently accessed data cached locally

Use when:
- Want cloud-first storage + low latency

### 4.2.5 Stored Volumes
- Full data stored on-prem
- Backup to S3 (snapshots)

Use when:
- Need full local dataset + cloud backup

## 4.2.6 Use Case
- Backup on-prem volumes to AWS

---

# 4.3 Tape Gateway

## 4.3.1 What it does
- Replaces physical tape backups

## 4.3.2 Protocol
- iSCSI (Virtual Tape Library - VTL)

## 4.3.3 Storage
- S3 → active tapes
- Glacier / Deep Archive → archived tapes

## 4.3.4 Use Case
- Migrate legacy tape backups to cloud

---

# 4.4 Quick Comparison

|Gateway Type|Protocol|Storage Backend|Use Case|
|---|---|---|---|
|File Gateway|NFS / SMB|S3|File access to S3|
|Volume Gateway|iSCSI|S3 + EBS snapshots|Block storage backup|
|Tape Gateway|iSCSI (VTL)|S3 + Glacier|Tape backup replacement|

---

# 5. Key Points
- “Expose S3 as file system” → **File Gateway**
- “Block storage / volumes / disks” → **Volume Gateway**
- “Tape backup / VTL / legacy backup” → **Tape Gateway**

---

### 6. Cache Logic
- File Gateway → caches files
- Volume Gateway (cached mode) → caches volumes

---

### 7. Glacier Rule
- File Gateway ❌ direct Glacier
- ✔️ via lifecycle policy
