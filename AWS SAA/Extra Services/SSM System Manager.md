  
AWS Systems Manager provides a set of tools to **manage, automate, and maintain infrastructure at scale** (EC2 instances and on-premises servers).  
  
All of these features rely on the **SSM Agent** running on the managed instance.  
  
---  
  
## 1. Run Command  
  
Run Command allows you to **execute scripts or commands on multiple managed instances at once**.  
  
### How it works  
- You send a command from AWS Systems Manager  
- The command is executed via the **SSM Agent**  
- It runs on:  
  - EC2 instances  
  - On-premises servers (registered with SSM)  
- No SSH or port 22 required  
  
**Explanation:** Run Command replaces manual SSH-based execution. It allows centralized, secure execution of commands across fleets of servers.  
  
### Output and Monitoring  
- Command output can be sent to:  
  - Amazon S3  
  - CloudWatch Logs  
- Execution status includes:  
  - In progress  
  - Success  
  - Failed  
- Notifications can be sent to **Amazon SNS**  
  
**Explanation:** This enables centralized logging and alerting for all command executions.  
  
### Automation Integration  
- Can be triggered manually or via **Amazon EventBridge**  
  
**Explanation:** This allows event-driven automation (e.g., run a command when something changes in AWS).  
  
---  
  
## 2. Patch Manager  
  
Patch Manager is used to **automate OS and software patching** for managed instances.  
  
### What it does  
- Installs:  
  - Operating system updates  
  - Security patches  
  - Application updates  
- Supports:  
  - EC2 instances  
  - On-premises servers  
  - Linux, Windows, macOS  
  
**Explanation:** It removes the need to manually maintain and patch servers.  
  
### Patch Methods  
- On-demand patching (immediate execution)  
- Scheduled patching using **Maintenance Windows**  
  
**Explanation:** You can either patch immediately or schedule patching during safe time windows.  
  
### Patch Compliance  
- Scans instances for missing patches  
- Generates compliance reports  
  
**Explanation:** Helps ensure all systems are up-to-date and secure.  
  
### Patch Execution  
- Uses the document: `AWS-RunPatchBaseline`  
  
**Explanation:** This is the standard SSM document used to apply patch baselines across instances.  
  
---  
  
## 3. Maintenance Windows  
  
Maintenance Windows define **when automated tasks are allowed to run**.  
  
### What they include  
- Schedule (when the window runs)  
- Duration (how long it stays open)  
- Target instances  
- Tasks to execute  
  
**Explanation:** This ensures system maintenance happens only during approved time periods.  
  
### Use Cases  
- OS patching  
- Software updates  
- Driver updates  
- System maintenance tasks  
  
**Explanation:** Prevents disruption by running maintenance during off-peak hours.  
  
---  
  
## 4. Automation  
  
Automation is used to **automate operational tasks across AWS resources**.  
  
### What it does  
- Executes predefined workflows called **Runbooks**  
- Runbooks are SSM documents that define steps  
  
### Common Use Cases  
- Restarting multiple instances  
- Creating AMIs  
- Creating EBS snapshots  
- Managing AWS resources (e.g., RDS snapshots)  
  
**Explanation:** Automation removes manual operational work by executing repeatable workflows.  
  
### Triggers  
Automation can be triggered by:  
- AWS Console  
- AWS CLI / SDK  
- EventBridge  
- Maintenance Windows  
- AWS Config  
  
**Explanation:** This allows both manual and fully automated infrastructure management.  
  
---  
  
## 5. AWS Config Integration  
  
- AWS Config monitors resource compliance  
- If a resource is non-compliant:  
  - It can trigger **SSM Automation**  
  
**Explanation:** This enables automatic remediation when configuration drift or violations are detected.  
  
---  

## 6. Default Host Configuration Management
 Automatically enables Systems Manager (SSM) management on EC2 instances across an account or organization.

- installs/configures the SSM agent prerequisites
- attaches the required permissions
- registers instances as “managed instances”
- does this **at scale without manually touching each instance**

---
## 7. Key Points  
  
- Run Command → Execute commands on multiple instances without SSH    
- Patch Manager → Automate OS and security patching    
- Maintenance Windows → Schedule when maintenance tasks run    
- Automation → Run predefined workflows (Runbooks)    
- AWS Config → Trigger automated remediation    
- All features rely on **SSM Agent + IAM role**