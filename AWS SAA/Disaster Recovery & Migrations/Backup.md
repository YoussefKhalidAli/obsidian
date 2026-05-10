  
## What is AWS Backup?  
- Fully managed AWS service for **centralized backup management**  
- Automates backups across multiple AWS services  
- Removes need for custom backup scripts or manual processes  
- Provides a **single place to define and monitor backup strategy**  
  
---  
  
## Supported Services (High Level)  
AWS Backup can protect many AWS resources, including:  
  
- Compute & storage:  
- Amazon EC2  
- Amazon EBS  
- Amazon S3  
- Databases:  
- Amazon RDS (all engines)  
- Aurora  
- DynamoDB  
- DocumentDB  
- Amazon Neptune  
- File & storage systems:  
- Amazon EFS  
- Amazon FSx (Lustre, Windows File Server)  
- AWS Storage Gateway (Volume Gateway)  
  
> Key idea: it covers most major AWS storage and database services.  
  
---  
  
## Key Features  
  
### 1. Centralized Backup Management  
- Manage all backups in one place (AWS Backup console)  
- Define unified backup policies instead of per-service configuration  
  
---  
  
### 2. Backup Plans  
Backup Plans define how backups behave:  
- **Schedule**: e.g. every 12 hours, daily, weekly, or cron expression  
- **Backup Window**: when backups should run  
- **Retention Period**:  
- How long backups are kept (days, months, years, or indefinite)  
- **Lifecycle rules**:  
- Move backups to cold storage after a period  
  
---  
  
### 3. On-Demand & Scheduled Backups  
- On-demand backups: manual snapshot anytime  
- Scheduled backups: automated via backup plans  
  
---  
  
### 4. Tag-Based Backups  
- Use tags to select resources for backup  
- Example concept: only backup resources tagged `Production`  
  
---  
  
### 5. Cross-Region Backup  
- Copy backups to another AWS Region  
- Used for **disaster recovery (DR)**  
  
---  
  
### 6. Cross-Account Backup  
- Backup data can be copied across AWS accounts  
- Useful for organizations with multi-account strategy (security separation)  
  
---  
  
### 7. Point-in-Time Recovery (PITR)  
- Restore data to a specific time  
- Example: supported by Aurora and other services  
- Useful for recovering from accidental deletes or corruption  
  
---  
  
## Backup Storage  
- Backups are stored in **AWS-managed Backup Vaults**  
- Under the hood, data is stored in **Amazon S3 (AWS-managed buckets)**  
- Users do not manage the underlying storage directly  
  
---  
  
## Backup Vault Lock (WORM Model)  
  
### What is it?  
- Enforces **Write Once Read Many (WORM)** policy  
  
### Behavior:  
- Once a backup is written:  
- It **cannot be deleted**  
- It **cannot be modified**  
- Retention period cannot be shortened  
  
### Protection:  
- Prevents:  
- Accidental deletion  
- Malicious deletion  
- Ransomware attacks  
- Even **root user cannot delete backups** when Vault Lock is enabled  
  
---  
  
## High-Level Flow  
1. Create a **Backup Plan**  
2. Assign AWS resources using tags or selection rules  
3. AWS Backup automatically creates backups  
4. Backups are stored in a **Backup Vault**  
5. Optionally:  
- Copy to other regions/accounts  
- Move to cold storage  
- Enforce Vault Lock  
  
---  
  
## Key Points  
- AWS Backup = centralized backup automation service  
- Uses **Backup Plans + Vaults**  
- Supports:  
- Cross-region  
- Cross-account  
- PITR (for supported services)  
- Vault Lock = immutable backups (WORM, strongest protection)  
- Backups are stored in AWS-managed S3-backed infrastructure