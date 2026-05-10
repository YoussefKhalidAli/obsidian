## 1. What is AWS Config?  
  
AWS Config is a **resource auditing and compliance tracking service**.  
  
It allows you to:  
- Record configuration changes of AWS resources over time  
- Evaluate resources against compliance rules  
- Detect misconfigurations (security, governance, best practices)  
  
### Example questions AWS Config can answer:  
- Is there unrestricted SSH access in security groups?  
- Are S3 buckets publicly accessible?  
- Did an ALB configuration change over time?  
  
---  
  
## 2. Key Capabilities  
  
### Configuration History  
- Tracks changes to AWS resources over time  
- Stores historical configurations  
- Can be queried later (e.g., using Athena)  
  
### Compliance Monitoring  
- Evaluates resources against rules  
- Shows compliant / non-compliant status  
- Sends alerts for violations  
  
---  
  
## 3. AWS Config Rules  
  
AWS Config uses rules to evaluate resources.  
  
### Types of rules:  
  
#### 1. AWS Managed Rules  
- Predefined rules (75+ available)  
- Example:  
- Ensure EBS volumes are encrypted  
- Ensure S3 buckets are not public  
  
#### 2. Custom Rules  
- Created using AWS Lambda  
- Example:  
- Ensure EC2 instances are t2.micro in dev accounts  
- Ensure EBS volumes are gp2 or gp3  
  
---  
  
## 4. Rule Evaluation Types  
  
### Triggered by Configuration Changes  
- Runs when a resource changes  
- Example: EBS volume type changes → re-evaluate  
  
### Periodic Evaluation  
- Runs on schedule (e.g., every 2 hours)  
- Checks all resources continuously  
  
---  
  
## 5. Important Concept: Config ≠ Enforcement  
  
AWS Config:  
- Does NOT block actions  
- Does NOT enforce security rules  
  
Instead:  
- Detects misconfiguration  
- Reports compliance status  
  
👉 IAM is still responsible for enforcement.  
  
---  
  
## 6. Remediation (Auto-Fix)  
  
AWS Config can trigger automatic remediation using:  
  
### AWS Systems Manager (SSM) Automation Documents  
  
Example:  
- Detect IAM access keys older than 90 days  
- Mark as non-compliant  
- Trigger SSM document:  
- `RevokeUnusedIAMUserCredentials`  
  
### Remediation Flow:  
1. Resource becomes non-compliant  
2. Config triggers remediation action  
3. SSM Automation runs  
4. Optionally retries (e.g., 5 times)  
  
You can also:  
- Trigger Lambda functions for custom remediation logic  
  
---  
  
## 7. Notifications & Integrations  
  
AWS Config integrates with:  
  
### Amazon SNS  
- Send notifications (email, Slack via integration)  
- Can filter specific events  
  
### Amazon EventBridge  
- React to configuration changes  
- Route events to:  
- Lambda  
- SQS / SNS  
- Step Functions  
- Event-driven workflows  
  
---  
  
## 8. Cross-Service Integration  
  
AWS Config works with:  
- **CloudTrail** → API activity tracking  
- **EventBridge** → event routing  
- **SSM Automation** → remediation  
- **Athena** → querying config history  
  
---  
  
## 9. Multi-Region & Multi-Account  
  
- AWS Config is **regional**  
- Must be enabled per region  
- Can aggregate data into a central account  
  
Use cases:  
- Organization-wide compliance dashboard  
- Central security auditing  
  
---  
  
## 10. Pricing Considerations  
  
AWS Config can become expensive:  
  
- Per configuration item recorded  
- Per rule evaluation  
  
Always enable selectively in production environments  
  
---  
  
## 11. Summary  
  
AWS Config helps you:  
- Track AWS resource configuration changes  
- Evaluate compliance using rules  
- Detect misconfigurations  
- Trigger notifications and remediation  
  
### Key takeaway:  
> AWS Config is for **visibility and compliance**, not enforcement.