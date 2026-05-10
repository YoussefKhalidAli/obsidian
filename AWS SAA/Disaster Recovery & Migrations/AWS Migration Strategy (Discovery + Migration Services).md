## 1. Two Ways to Move to the Cloud  
When moving workloads to AWS, there are two main approaches:  
  
### A. Greenfield (Start Fresh)  
- Build new systems directly in AWS  
- No migration needed  
- Use AWS-native architecture from the beginning  
  
### B. Migration (Lift & Shift / Modernization)  
- Move existing on-premises infrastructure to AWS  
- Requires planning, discovery, and migration tools  
  
---  
  
## 2. AWS Application Discovery Service (ADS)  
  
### Purpose  
- Helps you **understand your existing on-prem infrastructure before migration**  
- Collects data about servers and dependencies  
  
---  
  
### What it collects  
- Server utilization:  
- CPU usage  
- Memory usage  
- Disk usage  
- System inventory  
- Application dependencies (which systems talk to each other)  
  
---  
  
### Why it is important  
- Helps decide:  
- What to migrate first  
- How complex migration will be  
- Which applications depend on others  
  
---  
  
## 3. Discovery Methods  
  
### A. Agentless Discovery (AWS Connector)  
- No software installed inside servers  
- Uses a connector appliance  
- Collects:  
- VM configuration  
- Performance history  
- Basic resource usage  
  
✔ Good for quick overview  
❌ Less detailed  
  
---  
  
### B. Agent-Based Discovery (AWS Discovery Agent)  
- Installed directly on servers  
- Collects deeper insights:  
- Running processes  
- Network connections  
- Detailed system configuration  
- Real-time performance data  
  
✔ Best for dependency mapping  
✔ More accurate migration planning  
  
---  
  
## 4. AWS Migration Hub  
- Central dashboard for migration tracking  
- Displays data from:  
- Application Discovery Service  
- Migration tools (like MGN, DMS, SMS)  
- Purpose:  
- Single place to monitor migration progress  
  
---  
  
## 5. AWS Application Migration Service (MGN)  
  
### What it is  
- Main AWS service for **lifting and shifting servers to AWS**  
- Formerly known as **CloudEndure Migration**  
  
---  
  
### Purpose  
- Rehosting (lift-and-shift) migration  
- Moves:  
- Physical servers  
- Virtual machines  
- Other cloud workloads → AWS EC2  
  
---  
  
## 6. How MGN Works  
  
### Step 1: Install Replication Agent  
- Installed on on-prem servers  
- Continuously captures disk changes  
  
---  
  
### Step 2: Continuous Replication  
- Data is continuously replicated to AWS  
- Creates:  
- Staging EC2 instances  
- EBS volumes (replica storage)  
  
---  
  
### Step 3: Staging Environment  
- Lightweight EC2 instances run in AWS  
- Keeps data in sync with on-prem systems  
  
---  
  
### Step 4: Cutover (Go Live)  
- When ready:  
- Switch from on-prem → AWS  
- Launch production-sized EC2 instances  
- Attach final EBS volumes  
- Minimal downtime migration  
  
---  
  
## 7. Key Benefits of MGN  
- Very low downtime migration  
- Supports many OS and platforms  
- Automates replication process  
- Reduces need for complex manual migration work  
- Cost-efficient compared to custom migration solutions  
  
---  
  
## 8. Quick Summary  
  
### Discovery Phase  
- **Application Discovery Service (ADS)** → Collect server + dependency data  
- **Migration Hub** → View and track everything  
  
### Migration Phase  
- **AWS MGN** → Actual server migration (lift & shift)  
  
---  
  
## 9. Key Concept Flow  
1. Discover infrastructure (ADS)  
2. Analyze dependencies (Migration Hub)  
3. Replicate servers (MGN agent)  
4. Cutover to AWS (EC2 production)