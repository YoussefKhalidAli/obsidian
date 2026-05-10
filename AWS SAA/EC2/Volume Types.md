## 1. Introduction
EBS volumes come in **six main types**, grouped as SSD and HDD:

| Category | Volume Types | Characteristics |
|----------|--------------|----------------|
| **General Purpose SSD** | gp2, gp3 | Balance between price and performance for most workloads |
| **Provisioned IOPS SSD** | io1, io2, io2 Block Express | High-performance, low-latency, mission-critical workloads |
| **Throughput Optimized HDD** | st1 | Low-cost HDD for frequently accessed, throughput-intensive workloads |
| **Cold HDD** | sc1 | Lowest cost HDD for infrequently accessed workloads |

> Note:** Only gp2, gp3, io1, and io2 can be used as **boot volumes**. st1 and sc1 **cannot**.

---

## 2. General Purpose SSD (gp2 & gp3)

### gp2
- **Older generation**, cost-effective storage with low latency.  
- **Size:** 1 GB – 16 TB  
- **IOPS:** Linked to volume size (3 IOPS per GB, bursts up to 3,000 IOPS)  
- **Throughput:** Up to 250 MB/s  
- **Use Cases:** Boot volumes, virtual desktops, development & test environments.  

### gp3
- **Newer generation**, allows **independent scaling** of IOPS and throughput.  
- **Baseline IOPS:** 3,000  
- **Max IOPS:** 16,000 (can increase independently from size)  
- **Throughput:** 125 MB/s baseline, up to 1,000 MB/s  
- **Use Cases:** Same as gp2, but with predictable performance and scaling flexibility.

> **Key Difference:** gp2 → IOPS linked to size; gp3 → IOPS and throughput independent.

---

## 3. Provisioned IOPS SSD (io1 & io2 / io2 Block Express)

### io1
- **High-performance SSD** for mission-critical workloads.  
- **Size:** 4 GB – 16 TB  
- **Max IOPS:** 64,000 (Nitro EC2)  
- **IOPS:** Can be provisioned independently from size.  
- **Use Cases:** Databases requiring consistent, high IOPS.

### io2 / io2 Block Express
- **Next-gen high-performance SSD**  
- **Size:** Up to 64 TB  
- **Sub-millisecond latency**  
- **Max IOPS:** 256,000  
- **IOPS-to-GB ratio:** 1,000:1  
- **Supports Multi-Attach:** Can attach to multiple EC2 instances simultaneously for clustered applications.  
- **Use Cases:** Large-scale databases, mission-critical applications requiring extreme performance.

---
## 4. Multi-Attach Feature  
- **Definition:** Allows a **single io2 or io2 Block Express EBS volume** to be attached to **multiple EC2 instances simultaneously**.  
- **Limit:** Up to 16 EC2 Nitro instances per volume.  
- **Use Case:**  
	- High availability clusters  
	- Distributed databases like **Oracle RAC**, **SQL Server Always On**, or **Hadoop**  
	- Applications that need **shared access to a single data volume**  
  
> **Important:** Only **io2/io2 Block Express** volumes support Multi-Attach. Not supported for gp2, gp3, st1, sc1, or io1.

---
## 5. HDD Volumes (st1 & sc1)

### st1 – Throughput Optimized HDD
- **Use Cases:** Big data, data warehouses, log processing.  
- **Size:** Up to 16 TB  
- **Throughput:** Max 500 MB/s  
- **IOPS:** Max 500  
- Cannot be boot volumes.

### sc1 – Cold HDD
- **Use Cases:** Archive or infrequently accessed data.  
- **Size:** Up to 16 TB  
- **Throughput:** Max 250 MB/s  
- **IOPS:** Max 250  
- Lowest cost option.  

> **Tip:** HDD volumes are **throughput-optimized**, not latency-optimized. Use SSD for low-latency workloads.

---

## 6. Summary of When to Use
| Volume Type | Use Case |
|------------|---------|
| gp2 / gp3 | General workloads, boot volumes, dev/test, small-medium databases |
| io1 / io2 | Mission-critical DBs, workloads needing sustained IOPS |
| st1 | Big data, log processing, throughput-intensive workloads |
| sc1 | Archive data, infrequently accessed, low-cost storage |

---

## 7. Key Points
- **gp2 → bursts linked to size**, gp3 → IOPS and throughput **independent**  
- **io1/io2** → for high IOPS, critical workloads, support multi-attach (io2 only)  
- **st1/sc1** → HDD, cannot be boot volumes, focus on throughput  
- **Maximum IOPS over 32,000 requires EC2 Nitro with io1 or io2**  