Placement Groups allow you to **control how EC2 instances are placed on AWS infrastructure**.

**Explanation:** Instead of random placement, you define a strategy to optimize for **performance or availability**.

---

## 1. Types of Placement Groups

There are **3 strategies**:

- Cluster  
- Spread  
- Partition  

---

## 2. Cluster Placement Group

- Instances are placed **close together**  
- Same **Availability Zone (AZ)**  
- High-speed network between instances  

**Features:**
- Very **low latency**  
- High **throughput** (~10 Gbps+)  
- Best performance  

**Drawback:**
- **High risk** → if AZ fails, all instances fail  

**Use Case:**
- Big data processing  
- High-performance computing (HPC)  
- Applications needing **low latency + high throughput**

---

## 3. Spread Placement Group

- Instances are placed on **different hardware**  
- Can span **multiple AZs**  
- Max **7 instances per AZ per group**  

**Features:**
- **High availability**  
- Reduces risk of **simultaneous failure**  

**Drawback:**
- Limited scalability (7 instances per AZ)  

**Use Case:**
- Critical applications  
- Applications where **failure isolation is required**

---

## 4. Partition Placement Group

- Instances are grouped into **partitions (racks)**  
- Each partition is **isolated from failure**  
- Can span **multiple AZs**  
- Up to **7 partitions per AZ**  
- Each partition can have **many instances**

**Features:**
- Scales to **hundreds of instances**  
- Balanced between performance and availability  

**Explanation:**  
Each partition = separate hardware rack → failure in one partition does not affect others.

**Use Case:**
- Big data systems:
  - Hadoop  
  - Cassandra  
  - Kafka  

---

## 5. Key Differences

| Feature        | Cluster              | Spread                     | Partition                     |
|----------------|---------------------|----------------------------|-------------------------------|
| Placement      | Close together       | Separate hardware          | Groups (partitions/racks)     |
| AZ Scope       | Single AZ            | Multiple AZs               | Multiple AZs                  |
| Performance    | Highest              | Low                        | Medium                        |
| Availability   | Low                  | High                       | High                          |
| Scalability    | High                 | Limited (7 per AZ)         | Very high (100s instances)    |

---

## 6. Key Points

- Cluster → **performance (low latency)**  
- Spread → **high availability (isolation)**  
- Partition → **scalable + failure isolation**  
- Spread limit → **7 instances per AZ**  
- Partition → **up to 7 partitions per AZ**  
- Cluster → **single AZ only**