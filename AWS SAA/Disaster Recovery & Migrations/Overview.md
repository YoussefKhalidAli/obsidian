  
Disaster Recovery is a key topic for AWS Solutions Architect. It focuses on how to **prepare for and recover from failures or disasters** while maintaining business continuity.  
  
---  
  
## 1. What is a Disaster?  
  
A disaster is any event that negatively impacts a company’s:  
  
- Business continuity  
- Finances  
- Availability of systems or data  
  
**Explanation:** A disaster can be anything from hardware failure, data center outage, cyberattack, or even natural disasters that take systems offline.  
  
---  
  
## 2. Disaster Recovery (DR)  
  
Disaster Recovery is the process of:  
  
- Preparing for disasters  
- Recovering systems and data after a disaster  
- Minimizing downtime and data loss  
  
**Explanation:** The goal is to ensure systems can recover quickly and with minimal data loss.  
  
---  
  
## 3. Disaster Recovery Deployment Models  
  
### 3.1 On-Premises to On-Premises  
  
- Traditional DR model between two physical data centers  
- Example: one in California, another in Seattle  
- Very expensive to maintain  
  
**Explanation:** Requires maintaining duplicate infrastructure in multiple physical locations.  
  
---  
  
### 3.2 Hybrid Cloud DR  
  
- On-premises is primary  
- AWS Cloud is used for backup or recovery  
  
**Explanation:** Combines traditional infrastructure with AWS for disaster recovery, reducing cost compared to full duplication.  
  
---  
  
### 3.3 Cloud-to-Cloud (Multi-Region DR)  
  
- Primary system in one AWS region  
- Backup system in another AWS region  
  
**Explanation:** Fully cloud-based disaster recovery using multiple regions for redundancy and high availability.  
  
---  
  
## 4. Key DR Concepts  
  
### 4.1 RPO (Recovery Point Objective)  
  
- Defines **how much data loss is acceptable**  
- Measured in time (e.g., 1 hour, 5 minutes)  
  
**Explanation:** RPO determines how far back you can recover data. It depends on backup frequency.  
  
- Lower RPO = less data loss  
- Higher RPO = more data loss  
  
---  
  
### 4.2 RTO (Recovery Time Objective)  
  
- Defines **how long it takes to recover after a disaster**  
- Measured in time (e.g., minutes, hours)  
  
**Explanation:** RTO determines downtime. It is the time between failure and full recovery.  
  
- Lower RTO = faster recovery  
- Higher RTO = longer downtime  
  
---  
  
## 5. Disaster Recovery Strategies  
  
There are 4 main DR strategies ranked from cheapest/worst recovery to most expensive/best recovery:  
  
---  
  
### 5.1 Backup and Restore  
  
- Data is backed up periodically  
- Full recovery happens only after disaster  
  
**Explanation:**  
- High RPO (more data loss possible)  
- High RTO (slow recovery)  
- Cheapest option  
  
**How it works:**  
- Backups stored in S3/Glacier  
- Restore using AMIs, snapshots, or backups  
  
---  
  
### 5.2 Pilot Light  
  
- Core critical components always running in AWS  
- Non-critical systems are launched only during disaster  
  
**Explanation:**  
- Lower RPO than backup & restore  
- Faster recovery because core system is already active  
- Only critical infrastructure runs continuously  
  
---  
  
### 5.3 Warm Standby  
  
- Scaled-down version of full system always running  
- Can be quickly scaled to full production  
  
**Explanation:**  
- Even lower RPO and RTO  
- More expensive than pilot light  
- Partially active environment always running  
  
---  
  
### 5.4 Multi-Site / Hot Site (Active-Active)  
  
- Full production environments running in multiple locations  
- Traffic can be routed to any site  
  
**Explanation:**  
- Very low RTO (seconds or minutes)  
- Very low RPO  
- Most expensive option  
- Fully redundant active systems  
  
---  
  
## 6. Strategy Comparison  
  
| Strategy | Cost | RTO | RPO | Description |  
|----------|------|-----|-----|-------------|  
| Backup & Restore | Low | High | High | Restore after failure |  
| Pilot Light | Medium | Medium | Medium | Core system always running |  
| Warm Standby | High | Low | Low | Scaled-down full system |  
| Multi-Site | Very High | Very Low | Very Low | Active-active systems |  
  
---  
  
## 7. AWS Services for Disaster Recovery  
  
### Backup & Storage  
- EBS Snapshots  
- RDS Backups  
- S3 + Lifecycle policies  
- Glacier for long-term storage  
- AWS Snowball for offline transfer  
- Storage Gateway for hybrid backup  
  
---  
  
### High Availability & Failover  
- Route 53 (DNS failover between regions)  
- Multi-AZ deployments (RDS, ElastiCache)  
- Highly available services (S3, EFS)  
  
---  
  
### Networking DR  
- Direct Connect (primary connection)  
- Site-to-Site VPN (backup connection)  
  
---  
  
### Replication  
- RDS Cross-Region Replication  
- Aurora Global Database  
- Database replication tools for hybrid systems  
  
---  
  
### Automation  
- CloudFormation (recreate infrastructure)  
- Elastic Beanstalk (managed deployments)  
- CloudWatch alarms (trigger recovery actions)  
- AWS Lambda (automation and recovery logic)  
  
---  
  
## 8. Chaos Engineering  
  
Chaos engineering is the practice of **intentionally causing failures** to test system resilience.  
  
**Explanation:**  
- Helps ensure systems recover properly during real disasters  
- Example: randomly terminating EC2 instances in production  
- Popularized by Netflix “Chaos Monkey”  
  
---  
  
## 9. Key Points  
  
- DR is about **business continuity during failures**  
- RPO = acceptable data loss  
- RTO = acceptable downtime  
- DR strategies trade off between **cost, RPO, and RTO**  
- AWS provides tools for **backup, replication, automation, and failover**  
- Best systems use **automation + multi-region design**