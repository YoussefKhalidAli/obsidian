
## 1. Auto Scaling Group
An **Auto Scaling Group (ASG)** automatically manages a group of EC2 instances by:
- **Scaling out (adding instances)** when load increases  
- **Scaling in (removing instances)** when load decreases  
 Goal: **Maintain performance + optimize cost automatically**

---

## 2. Core Concepts

### 1. Scaling Types
- **Scale Out (Add instances)** → handle increased traffic  
- **Scale In (Remove instances)** → reduce cost when demand drops  

---

### 3. Capacity Settings

An ASG always has 3 important values:
- **Minimum capacity** → lowest number of instances (always running)
- **Desired capacity** → target number of instances
- **Maximum capacity** → upper limit (cannot exceed)

Example:
```
Min = 2  
Desired = 4  
Max = 7
```

---

## 4. Key Features

### 1. Automatic Scaling
- Adjusts number of EC2 instances dynamically
- Based on **metrics (CPU, requests, etc.)**

### 2. Health Checks & Self-Healing
- ASG continuously monitors instance health
- If an instance is **unhealthy**:
  - It is **terminated**
  - A **new instance is launched automatically**

 Health checks can come from:
- EC2 status checks
- Load balancer health checks (recommended)

---

## 5. Integration with Load Balancer
- ASG works seamlessly with ELB
- Automatically:
  - Registers new instances
  - Deregisters terminated instances
 Ensures traffic is always distributed properly

---

## 6. Cost Efficiency
- You **don’t pay for ASG itself**
- You only pay for:
  - EC2 instances
  - Attached resources (EBS, etc.)

---

## 7. Launch Template

ASG uses a **Launch Template** to create instances.

It defines:
- AMI (OS image)
- Instance type (e.g., t2.micro)
- Key pair (SSH)
- Security groups
- EBS volumes
- IAM roles
- Network/subnet
- User data scripts

---

## 8. Scaling Policies

### 8.1 Target Tracking Scaling (Recommended)
- Automatically adjusts instances to maintain a metric
- Example:
  - Keep CPU at **50%**

### 8.2 Simple Scaling
- Triggered by a CloudWatch alarm
- Example:
  - CPU > 70% → add 1 instance

### 8.3 Step Scaling
- More advanced version of simple scaling
- Scale based on severity:
  - CPU 70–80% → +1 instance
  - CPU 80–90% → +2 instances

### 4. Scheduled Scaling
- Scale based on time
- Example:
  - Increase capacity at **9 AM**
  - Decrease at **6 PM**

---

## 9. CloudWatch Integration
- ASG uses **CloudWatch Alarms** to trigger scaling
### Example:
- Metric: Average CPU
- If CPU > 70% → Scale Out
- If CPU < 30% → Scale In

---

## 10. Multi-AZ Support (High Availability)

- ASG can launch instances across **multiple Availability Zones**
- Ensures:
  - Fault tolerance
  - High availability

---

## 11. Important Behaviors

### 11.1 Instance Replacement
- Unhealthy instance → terminated → replaced automatically

### 11.2 Load Distribution
- When used with Load Balancer:
  - Traffic is automatically balanced

### 11.3 Cooldown Period
- Prevents rapid scaling actions
- Gives time for system to stabilize

---

## 12. Key Points

- **Scale Out = Add instances**
- **Scale In = Remove instances**
- Always remember:
  - **Min / Desired / Max**
- ASG + Load Balancer = **Best practice**
- ASG provides:
  - **High Availability**
  - **Fault Tolerance**
  - **Elasticity**
- Launch Template = **EC2 configuration blueprint**
