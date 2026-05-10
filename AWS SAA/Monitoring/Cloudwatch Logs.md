  
## 1. Overview  
Amazon CloudWatch Logs is a managed service used to **store, monitor, and analyze application and system logs**.  
  
It is commonly used for:  
- Application logs  
- Infrastructure logs  
- Security logs  
- Audit logs  
  
---  
  
## 2. Core Structure  
  
### Log Groups  
- A **log group** is a container for logs  
- Usually represents an application or service  
- Example:  
  - `/aws/ec2/my-app`  
  - `/aws/lambda/payment-service`  
  
### Log Streams  
- A **log stream** is a sequence of log events  
- Represents:  
  - A single EC2 instance  
  - A container  
  - A Lambda execution environment  
- Each log stream belongs to exactly one log group  
  
---  
  
## 3. Log Retention  
  
You can define how long logs are stored:  
  
| Option | Description |  
|-------|-------------|  
| Never expire | Logs stored indefinitely |  
| 1 day → 10 years | Custom retention period |  
  
---  
  
## 4. Log Sources (Where logs come from)  
  
CloudWatch Logs can ingest logs from many AWS services:  
  
### Common sources:  
- EC2 (via CloudWatch Agent / Unified Agent)  
- Lambda functions  
- ECS containers  
- Elastic Beanstalk  
- API Gateway  
- Route 53 (DNS queries)  
- VPC Flow Logs  
- CloudTrail (filtered events)  
  
---  
  
## 5. Log Collection Methods  
  
| Method | Description |  
|-------|-------------|  
| CloudWatch Agent | Installed on EC2 to push logs |  
| Unified CloudWatch Agent | Replaces legacy agent (recommended) |  
| SDK | Custom application logging |  
| AWS Services integration | Native log forwarding (Lambda, ECS, etc.) |  
  
---  
  
## 6. Log Encryption  
  
- Logs are encrypted **by default**  
- Supports optional **KMS encryption (customer-managed keys)**  
  
---  
  
## 7. CloudWatch Logs Insights  
  
### What it is  
A **query engine** for analyzing log data.  
  
### Key features:  
- SQL-like query language  
- Filter logs by time range  
- Aggregate and sort data  
- Detect fields automatically  
- Visualize query results  
  
### Use cases:  
- Find errors in logs  
- Analyze request patterns  
- Debug applications  
- Security investigation  
  
### Important note:  
- ❗ Not real-time  
- Works on **historical log data only**  
  
---  
  
## 8. Exporting and Streaming Logs  
  
### A. Batch Export (S3)  
- Logs exported to Amazon S3  
- Asynchronous (can take hours)  
- API: `CreateExportTask`  
- Not real-time  
  
---  
  
### B. Subscription Filters (Real-time)  
  
Used for **real-time log streaming**  
  
#### Destinations:  
- Kinesis Data Streams  
- Kinesis Data Firehose  
- AWS Lambda  
- OpenSearch Service  
  
#### Features:  
- Near real-time delivery  
- Filter logs before sending  
- Cross-account streaming support  
  
---  
  
## 9. Cross-Account Log Streaming Architecture  
  
### Components:  
- Source account (log producer)  
- Destination account (log consumer)  
- Subscription filter  
- Destination (Kinesis / Firehose / Lambda)  
  
### Flow:

CloudWatch Logs (Account A)  
→ Subscription Filter  
→ Destination (Account B Kinesis Stream)  
→ Firehose / S3 / OpenSearch

  
### Required setup:  
- Destination access policy  
- IAM role in destination account  
- Cross-account permissions (role assumption)  
  
---  
  
## 10. Log Aggregation Use Cases  
  
- Centralized logging across multiple AWS accounts  
- Security monitoring across environments  
- Enterprise-wide log analytics  
- Multi-region log consolidation  
  
---  
  
## 11. Key Differences  
  
| Feature | Export to S3 | Subscription Filter |  
|--------|-------------|---------------------|  
| Speed | Batch (slow) | Near real-time |  
| Use case | Archival | Streaming / analytics |  
| Destination | S3 only | Kinesis, Lambda, OpenSearch |  
| Latency | Hours | Seconds |  
  
---  
  
## 12. Mental Model  

Application / AWS Service  
↓  
Log Stream  
↓  
Log Group  
↓  
CloudWatch Logs  
↙ ↘  
S3 Export Subscription (Real-time)

  
---  
  
## 13. Key Points  
  
- Log Group = application-level container  
- Log Stream = instance/container logs  
- Logs Insights = query engine (not real-time)  
- Subscription filters = real-time streaming  
- Export to S3 = batch processing only  
- Logs are encrypted by default