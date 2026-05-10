## 1. Running AWS-like OS on On-Premise
### Amazon Linux 2 AMI (on-prem usage)
- AWS provides Amazon Linux 2 as a virtual machine image.
- You can run it locally using hypervisors like:
  - VMware
  - VirtualBox
  - KVM
  - Hyper-V
- Purpose: lets you simulate AWS-compatible environments on-premise.
- Use case: testing or hybrid environments.

---

## 2. VM Import / Export
- Allows you to **move existing virtual machines into AWS EC2**.
- Also allows exporting EC2 instances back to on-premise (if needed).
- Use case:
  - Lift-and-shift migration of existing VM workloads.
  - Disaster recovery backup of on-prem VMs into AWS.
- Supports common VM formats (VMware, etc.).

---

## 3. AWS Application Discovery Service (ADS)
- Collects information from on-prem servers before migration.
- Provides:
  - Server utilization (CPU, memory, disk usage)
  - Dependency mapping (which servers talk to which)
- Use case:
  - Planning large-scale migrations.
  - Understanding infrastructure before moving to AWS.

---

## 4. AWS Migration Hub
- Central dashboard to track migration progress.
- Integrates with other migration tools (DMS, SMS, etc.).
- Use case:
  - One place to monitor all ongoing migrations.

---

## 5. AWS Database Migration Service (DMS)
- Migrates databases between:
  - On-prem → AWS
  - AWS → AWS
  - AWS → On-prem
- Supports continuous replication using **CDC (Change Data Capture)**.
- Keeps source database available during migration.
- Use cases:
  - Minimal downtime database migration.
  - Ongoing sync between systems.

---

## 6. AWS Server Migration Service (SMS)
- Migrates **entire servers (not just databases)** into AWS.
- Performs **incremental replication** of live systems.
- Converts on-prem servers into EC2 AMIs.
- Use case:
  - Ongoing replication for disaster recovery or migration waves.

---

## Summary (Quick View)
- **VM Import/Export** → Move VMs to/from EC2  
- **ADS** → Analyze on-prem environment  
- **Migration Hub** → Track migrations  
- **DMS** → Database migration + replication  
- **SMS** → Full server migration (incremental replication)  
- **Amazon Linux AMI** → Run AWS OS locally for testing/hybrid setups  