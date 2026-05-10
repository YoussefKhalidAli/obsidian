  
Amazon GuardDuty is a **threat detection service** that continuously monitors AWS accounts and workloads for **malicious or suspicious activity**.  
  
---  
  
## 1. Purpose  
  
- Detect **security threats automatically**  
- Identify **anomalies and unusual behavior**  
- Provide **security findings** without manual setup  
  
**Explanation:**  
GuardDuty is a managed security service that uses **machine learning and threat intelligence** to detect attacks in your AWS environment.  
  
---  
  
## 2. How GuardDuty Works  
  
GuardDuty uses:  
  
- Machine Learning (ML)  
- Anomaly detection  
- AWS threat intelligence feeds  
- Third-party security data  
  
**Explanation:**  
It compares normal behavior vs unusual behavior to detect potential threats.  
  
---  
  
## 3. Easy Setup  
  
- One-click enablement  
- No software installation required  
- Includes a **30-day free trial**  
  
---  
  
## 4. Data Sources Analyzed  
  
GuardDuty continuously analyzes multiple AWS logs.  
  
---  
  
### 4.1 Always Enabled Sources  
  
#### 1. CloudTrail Logs  
- Detects unusual API activity  
- Examples:  
- Unauthorized IAM actions  
- Suspicious resource creation  
  
Includes:  
- Management events (e.g., create VPC, create IAM user)  
- Data events (e.g., S3 object access)  
  
---  
  
#### 2. VPC Flow Logs  
- Monitors network traffic  
- Detects:  
- Unusual IP communication  
- Suspicious outbound traffic  
- Port scanning behavior  
  
---  
  
#### 3. DNS Logs  
- Detects abnormal DNS activity  
- Example:  
- EC2 instance sending encoded data via DNS (data exfiltration)  
  
---  
  
### 4.2 Optional Data Sources  
  
- S3 data events  
- EBS volume activity  
- Lambda network activity  
- RDS & Aurora login events  
- EKS audit logs and runtime monitoring  
  
---  
  
## 5. Findings  
  
GuardDuty generates **findings** when suspicious activity is detected.  
  
### Example findings:  
- Compromised EC2 instance  
- Cryptocurrency mining activity  
- Unauthorized API calls  
- Data exfiltration attempts  
  
---  
  
## 6. Cryptocurrency Attack Detection  
  
GuardDuty can detect:  
- Crypto mining malware  
- Unauthorized compute usage for mining  
  
**Explanation:**  
This is a commonly tested use case.  
  
---  
  
## 7. Event Integration (EventBridge)  
  
When a finding is generated:  
  
1. GuardDuty sends an event to **Amazon EventBridge**  
2. EventBridge routes the event using rules  
3. Actions can be triggered:  
- AWS Lambda (automation)  
- SNS (notifications)  
- SQS (queue processing)  
  
---  
  
## 8. Key Features Summary  
  
- Fully managed threat detection service  
- Uses ML + threat intelligence  
- No manual configuration required  
- Continuously monitors AWS environment  
- Detects:  
- Network attacks  
- API abuse  
- Malware activity  
- Data exfiltration  
- Crypto mining  
  
---  
  
## 9. Key Points  
  
- Uses CloudTrail + VPC Flow Logs + DNS logs by default  
- Generates **security findings**  
- Integrates with EventBridge for automation  
- Can detect cryptocurrency mining attacks  
- No agents or software installation required