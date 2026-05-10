## 1. Definitions

### Scalability
- Ability of a system to **handle increased load by adapting**.  
- Two types:
  - **Vertical Scaling (Scale Up/Down)**
  - **Horizontal Scaling (Scale Out/In)**  

### High Availability (HA)
- Ability of a system to **remain operational even if part of the system fails**.  
- Achieved by running across **multiple data centers / Availability Zones (AZs)**.  

> **Important:** Scalability ≠ High Availability (but often used together)

---

## 2. Vertical Scalability (Scale Up / Down)

### Definition
- Increase or decrease the **size/power of a single instance**.  

### Example
- EC2: `t2.micro → t2.large`  
- Call center: upgrade a **junior operator → senior operator**  

### Characteristics
- No change in number of instances  
- Limited by **hardware constraints**  
- Simpler to implement  

### Use Cases
- Databases (RDS)  
- Caching (ElastiCache)  
- Non-distributed systems  

---

## 3. Horizontal Scalability (Scale Out / In)

### Definition
- Increase or decrease the **number of instances**.  

### Example
- Add more EC2 instances behind a load balancer  
- Call center: **hire more operators**  

### Characteristics
- Requires **distributed system design**  
- Practically unlimited scaling  
- More complex architecture  

### AWS Terms
- **Scale Out:** Add instances  
- **Scale In:** Remove instances  

### Use Cases
- Web applications  
- Microservices  
- Cloud-native systems  

---

## 4. High Availability (HA)

### Definition
- System runs across **multiple AZs/data centers** to survive failures  

### Goal
- **No downtime** if one AZ fails  

### Example
- Call center in **two cities**  
- If one fails → other continues  

### AWS Implementation
- **Multi-AZ deployments**  
- **Load Balancers (ALB/ELB)**  
- **Auto Scaling Groups (ASG)**  

---

## 5. Types of High Availability

### 5.1 Active-Active
- All instances are **running and serving traffic**  
- Example:
  - Multiple EC2 instances behind a load balancer  
- **Best performance + availability**

### 5.2 Active-Passive
- One instance is **active**, another is **standby**  
- Example:
  - RDS Multi-AZ  
- Failover occurs when primary fails  

---

## 6. Key Differences

| Feature            | Vertical Scaling        | Horizontal Scaling        | High Availability            |
|--------------------|------------------------|---------------------------|------------------------------|
| What changes       | Instance size          | Number of instances       | Deployment across AZs        |
| Limit              | Hardware limit         | Practically unlimited     | Depends on architecture      |
| Complexity         | Low                    | Medium/High               | Medium                       |
| Example            | Bigger EC2             | More EC2 instances        | Multi-AZ setup               |

---

## 7. Relationship Between Concepts

- Horizontal scaling → often used with **High Availability**  
- Vertical scaling → does **not** provide HA  
- HA requires **redundancy across AZs**  

---

## 8. AWS Examples

- **Vertical Scaling:** Change EC2 instance type  
- **Horizontal Scaling:** Auto Scaling Group (ASG)  
- **High Availability:**  
  - Multi-AZ RDS  
  - Multi-AZ EC2 with Load Balancer  

---

## 9. Key Points

- **Vertical = bigger instance**  
- **Horizontal = more instances**  
- **High Availability = multiple AZs**  

- If question says:
  - “Handle more traffic” → **Horizontal scaling**  
  - “Improve performance of single instance” → **Vertical scaling**  
  - “Survive AZ failure” → **High Availability**  

- Best practice:
  - Combine **Horizontal Scaling + High Availability**  

---