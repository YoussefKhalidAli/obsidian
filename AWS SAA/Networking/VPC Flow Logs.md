  
VPC Flow Logs are a feature that allows you to **capture metadata about IP traffic** going to and from network interfaces in your VPC.  
  
They help you **monitor, troubleshoot, and analyze network traffic** in AWS.  
  
---  
  
## 1. What VPC Flow Logs Capture  
  
VPC Flow Logs record **information about network traffic**, not the actual packets.  
  
They capture metadata such as:  
- Source IP address  
- Destination IP address  
- Source port  
- Destination port  
- Protocol  
- Action (ACCEPT or REJECT)  
- Traffic status  
  
**Explanation:** Flow Logs do not capture the content of the traffic, only information about the traffic flow.  
  
---  
  
## 2. Scope (Where You Can Enable Flow Logs)  
  
Flow Logs can be enabled at different levels:  
  
- **VPC level** → captures all traffic in the VPC  
- **Subnet level** → captures traffic in a specific subnet  
- **Network Interface (ENI) level** → captures traffic for a specific instance or service  
  
**Explanation:** This allows flexibility depending on whether you want broad or detailed network monitoring.  
  
---  
  
## 3. Where Flow Logs Are Sent  
  
VPC Flow Logs can be delivered to:  
  
- Amazon S3 (for storage and analysis)  
- Amazon CloudWatch Logs (for monitoring and log analysis)  
- Amazon Kinesis Data Firehose (for streaming to other services)  
  
**Explanation:** You choose the destination depending on whether you want storage, real-time monitoring, or streaming analytics.  
  
---  
  
## 4. Use Cases  
  
- Troubleshooting network connectivity issues  
- Detecting rejected traffic  
- Identifying security threats (e.g., port scans, suspicious IPs)  
- Analyzing traffic patterns and usage  
- Monitoring application behavior  
  
**Explanation:** Flow Logs are mainly used for **network visibility and security analysis**.  
  
---  
  
## 5. Flow Log Fields (High-Level)  
  
Key fields include:  
- Source and destination IP → identifies communication endpoints  
- Source and destination ports → identifies service or application  
- Action → whether traffic was allowed or denied  
- Protocol → type of network communication (TCP, UDP, etc.)  
  
**Explanation:** These fields help determine **what traffic happened, where it came from, and whether it was allowed**.  
  
---  
  
## 6. Security Group vs NACL Troubleshooting  
  
Flow Logs are useful for identifying whether issues come from **Security Groups or NACLs**:  
  
- **Security Groups are stateful**  
- If inbound traffic is allowed, return traffic is automatically allowed  
  
- **Network ACLs are stateless**  
- Inbound and outbound rules are evaluated separately  
  
### Interpretation Rules:  
  
- If inbound is **REJECTED** → could be Security Group or NACL  
- If inbound is **ACCEPTED** but outbound is **REJECTED** → must be a **NACL issue**  
- If outbound is **REJECTED** → could be SG or NACL  
  
**Explanation:** Because Security Groups are stateful, inconsistencies between inbound and outbound traffic usually point to NACL misconfiguration.  
  
---  
  
## 7. Querying Flow Logs  
  
You can analyze Flow Logs using:  
  
- Amazon Athena (SQL queries on S3 logs)  
- CloudWatch Logs Insights (real-time querying)  
  
**Explanation:** This allows you to search and analyze traffic patterns using SQL-like queries or log queries.  
  
---  
  
## 8. Advanced Analytics and Monitoring  
  
Flow Logs can be integrated with other AWS services:  
  
- CloudWatch Contributor Insights  
- Identifies top IPs or traffic contributors  
  
- CloudWatch Alarms  
- Detects unusual traffic patterns (e.g., SSH/RDP spikes)  
  
- SNS Notifications  
- Sends alerts when suspicious activity is detected  
  
- Amazon QuickSight  
- Visualizes traffic data for reporting  
  
**Explanation:** These integrations help transform raw logs into actionable security and performance insights.  
  
---  
  
## 9. Key Points  
  
- Captures **network traffic metadata only (not packet content)**  
- Works at **VPC, subnet, or ENI level**  
- Helps with **security, troubleshooting, and monitoring**  
- Can detect **malicious activity like port scanning**  
- Supports integration with **S3, CloudWatch, and Kinesis**  
- Useful for diagnosing **Security Group vs NACL issues**