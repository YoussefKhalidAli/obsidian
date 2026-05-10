## 1. RDS

**Amazon RDS (Relational Database Service)** is a **managed database service** for databases that use **SQL (Structured Query Language)**.

Allows you to:
- Create, operate, and scale relational databases in the cloud
- Offload database management to AWS

---

## 2. Supported Database Engines

RDS supports multiple database engines:
- PostgreSQL  
- MySQL  
- MariaDB  
- Oracle  
- Microsoft SQL Server  
- IBM DB2  
- Amazon Aurora (AWS proprietary)

---

## 3. Why Use RDS?
Instead of managing a database on EC2, RDS provides:

### Managed Features
- Automated **provisioning**
- **OS patching**
- **Backups** (automatic)
- **Point-in-Time Restore**
- **Monitoring dashboards**
- **Maintenance windows**

### Scalability
- **Vertical scaling** → increase instance size  
- **Horizontal scaling** → add Read Replicas  

### High Availability & Performance
- **Multi-AZ deployments**
- **Read Replicas**

### Limitation
- No SSH access to underlying instances

---

## 4. Storage (EBS-backed)

- RDS storage is backed by **EBS**
- You must define storage size initially
- Can increase storage later

---

## 5. RDS Storage Auto Scaling

### What it does
Automatically increases storage when running low
### Conditions for scaling
- Free storage < **10%**
- Condition lasts **> 5 minutes**
- At least **6 hours since last scaling**
### Requirements
- Must define a **maximum storage limit**
### Use Case
- Unpredictable workloads
- Avoid manual intervention

---

## 6. Read Replicas (Scaling Reads)
### Purpose
- Improve **read performance**
### Key Features
- Up to **15 Read Replicas**
- Can be:
  - Same AZ
  - Cross AZ
  - Cross Region
### Networking Cost
- Same Region (even across AZ) → Free  
- Cross Region → Paid  
### Replication Type
- **Eventually consistent** (**Asynchronous replication**)
### Usage Rules
- Only **READ operations (SELECT)**
- No INSERT / UPDATE / DELETE
### Promotion
- Can be promoted to **standalone DB**
- Becomes independent
### Use Case
- Reporting / analytics workloads
- Offload reads from main DB

---

## 7. Multi-AZ (High Availability / Disaster Recovery)

### Purpose
- Provide **failover & high availability**
### Architecture
- **Primary DB (Master)**
- **Standby DB (Replica)** in another AZ
### Replication Type
- **Synchronous replication**
### Behavior
- Single **DNS endpoint**
- Automatic **failover** to standby
### Key Points
- Not used for scaling
- Standby is NOT readable until it becomes active
- Used for **disaster recovery**
### Failover Triggers
- AZ failure  
- Network failure  
- Instance/storage failure  

---

## 8. Read Replicas vs Multi-AZ

| Feature      | Read Replicas | Multi-AZ          |
| ------------ | ------------- | ----------------- |
| Purpose      | Scale reads   | High availability |
| Replication  | Asynchronous  | Synchronous       |
| Read access  | Yes           | No                |
| Write access | No            | No (standby only) |
| Failover     | Manual        | Automatic         |
| Consistency  | Eventual      | Strong            |

---
## 10. Convert Single-AZ → Multi-AZ

### Steps
- Modify DB
- Enable Multi-AZ
### What Happens Internally
1. Snapshot of primary DB
2. Restore snapshot to standby
3. Enable synchronization

Note: **Zero downtime operation**

---

## 11. RDS Custom  
  
**RDS Custom** allows you to access and customize:  
- The **operating system**  
- The **database itself**  

 ### Supported Engines:  
- Oracle  
- Microsoft SQL Server  
  
### Capabilities of RDS Custom:  
- SSH into underlying EC2 instance  
- Modify OS configurations  
- Install patches manually  
- Enable native DB features  
- Use SSM Session Manager  

### Key Differences  

| Feature       | RDS    | RDS Custom              |
| ------------- | ------ | ----------------------- |
| OS Access     | ❌ No   | ✅ Yes                   |
| SSH Access    | ❌ No   | ✅ Yes                   |
| Automation    | ✅ Full | ✅ Partial (can disable) |
| Custom Config | ❌ No   | ✅ Yes                   |
   
### Best Practices:  
- Disable automation before customization  
- Always take a **snapshot backup** before changes  
- Be careful: you can break the system

---

## 12. Summary

Amazon RDS provides:
- Fully managed relational databases
- Built-in high availability
- Read scalability
- Automated backups and maintenance

👉 Use:
- **Read Replicas** → Performance  
- **Multi-AZ** → Reliability  