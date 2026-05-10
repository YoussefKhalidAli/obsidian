## What is AWS Snow Family?
- Collection of **secure physical devices** used for:
    1. **Data migration (offline transfer)**
    2. **Edge computing (processing data near source)**

---

# 1. Data Migration (Offline Transfer)

## 1.1 Why Snow Family?
- Network transfer is:
    - Slow (e.g., 100 TB = ~12 days on 1 Gbps)
    - Expensive
    - Limited by bandwidth
    - Unreliable (retries, instability)

 Rule:
- If transfer takes **> 1 week → use Snow devices**

## 1.2 How It Works
1. Request device from AWS
2. AWS ships device to you
3. Copy data locally onto device
4. Ship device back to AWS
5. Data loaded into S3
6. Device is wiped securely

## 1.3 Snow Devices for Migration

### 1.3.1 Snowcone
- Small & portable
- Capacity:
    - 8 TB (HDD)
    - 14 TB (SSD)
- Use cases:
    - Small data transfers
    - Remote/harsh environments

### 1.3.2 Snowball Edge
- Large device for TB–PB scale
- Types:
    - **Storage Optimized** → ~80 TB
    - **Compute Optimized** → ~28–42 TB
- Supports:
    - Block storage
    - S3-compatible storage
- Use cases:
    - Data center migration
    - Backup / disaster recovery

### 1.3.3 Snowmobile
- Physical **truck**
- Capacity:
    - 100 PB per truck
- Use case:
    - **Exabyte-scale migration**
- Highly secure:
    - GPS tracking
    - 24/7 surveillance
    - Temperature control

Use when:
- Data > **10 PB**
## 1.4 Quick Comparison

| Device     | Capacity | Use Case                |
| ---------- | -------- | ----------------------- |
| Snowcone   | ~8–14 TB | Small / edge / portable |
| Snowball   | ~80 TB   | TB–PB migration         |
| Snowmobile | ~100 PB  | Exabyte-scale transfer  |

---

# 2. Edge Computing

## What is Edge Computing?
Processing data **where it is generated**, instead of sending to cloud.

### 2.1 Examples of Edge Locations:
- Ships
- Trucks
- Mining sites
- Remote areas (no internet)

## 2.2 Why Edge Computing?
- No/limited internet
- Need real-time processing
- Reduce latency

## 2.3 Devices Used
- Snowcone
- Snowball Edge

## 2.4 Use Cases

- Data preprocessing
- Machine learning at edge
- Video transcoding
- IoT processing

## 2.5 Compute Capabilities

### Snowcone
- 2 CPU, 4 GB RAM
- Lightweight workloads
### Snowball Edge (Compute)
- ~104 vCPU
- ~416 GB RAM
- Optional GPU
- Can run:
    - EC2 instances
    - Lambda (via AWS IoT Greengrass)

---

# 3. Snow Family Features

## 3.1 Security
- Encryption
- Tamper-resistant
- Data wiped after use

## 3.2 Data Transfer Options
- Offline (shipping device)
- Online via AWS DataSync (for Snowcone)

---

## 4. Management Tool

### AWS OpsHub
- GUI tool (instead of CLI)
- Allows:
    - Device setup
    - File transfer
    - Launch EC2 instances
    - Monitor metrics

---

# 5. Key Points

- **>1 week transfer → Snowball**
- **TB scale → Snowball**
- **PB+ scale → Snowmobile**
- **Remote/edge → Snowcone / Snowball**
- **Edge computing = process locally**
- **Snowmobile = truck**