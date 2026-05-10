  
AWS Direct Connect is a **dedicated private network connection** between your on-premises data center and AWS.  
  
---  
  
## 1. Overview  
  
- Provides a **dedicated physical connection** to AWS  
- Connects **on-premises network ↔ AWS VPC**  
- Does NOT use the public internet  
- Requires an AWS Direct Connect location  
  
**Explanation:** Instead of sending traffic over the internet, Direct Connect uses a private line for more consistent and reliable networking.  
  
---  
  
## 2. Core Components  
  
### Virtual Private Gateway (VGW)  
- AWS-side VPN/Direct Connect endpoint  
- Attached to a VPC  
- Used for **private VPC access**  
  
---  
  
### Direct Connect Location  
- Physical AWS facility where connectivity is established  
- Contains networking equipment used to connect customers to AWS  
  
---  
  
### Customer Router (On-Premises)  
- Router/firewall in your data center  
- Connects your internal network to AWS Direct Connect  
  
---  
  
## 3. Virtual Interfaces (VIFs)  
  
### Private Virtual Interface (Private VIF)  
- Used to access **private AWS resources**  
- Connects to:  
  - Virtual Private Gateway (VGW)  
- Used for:  
  - EC2 in private subnets  
  - VPC resources  
  
---  
  
### Public Virtual Interface (Public VIF)  
- Used to access **public AWS services**  
- Examples:  
  - S3  
  - DynamoDB  
- Does NOT go through VGW  
- Connects directly to AWS public endpoints  
  
---  
  
## 4. Key Benefits  
  
- Higher bandwidth than VPN  
- Lower latency and more consistent performance  
- Reduced data transfer costs (compared to internet-based transfer)  
- Better for large-scale data transfer and hybrid architectures  
  
**Explanation:** Direct Connect is mainly used when performance, stability, and large data transfer are important.  
  
---  
  
## 5. Use Cases  
  
- Hybrid cloud architectures (on-prem + AWS)  
- Big data transfers  
- Real-time applications needing stable latency  
- Enterprise network integration  
  
---  
  
## 6. Connection Types  
  
### Dedicated Connection  
- Physical Ethernet port dedicated to a single customer  
- Speeds: 1 Gbps, 10 Gbps, 100 Gbps  
- Requested directly from AWS  
- Provisioned at a Direct Connect location  
  
---  
  
### Hosted Connection  
- Provided by AWS partners  
- Flexible bandwidth options (e.g., 50 Mbps to 10 Gbps)  
- Can be adjusted (add/remove capacity)  
  
---  
  
## 7. Setup Time
  
- Direct Connect is **not instant**  
- Can take **weeks (often > 1 month)** to provision  
  
**Explanation:** For short-term needs, Direct Connect is NOT the right solution.  
  
---  
  
## 8. Encryption  
  
- Direct Connect is **NOT encrypted by default**  
- It is private, but not encrypted  
  
### Optional Encryption  
- You can combine:  
  - Direct Connect + VPN (IPsec tunnel)  
- This adds **encryption over the private link**  
  
---  
  
## 9. Direct Connect Gateway  
  
Used to connect **multiple VPCs and/or multiple regions**.  
  
- Central hub for Direct Connect connections  
- Allows access to:  
  - Multiple VPCs  
  - Different AWS regions  
- Works with Private VIFs and VGWs  
  
**Explanation:** Without it, a Direct Connect connection is limited to a single region/VPC setup.  
  
---  
  
## 10. Resiliency Architectures  
  
### 1. High Resiliency (Standard Redundancy)  
- Multiple Direct Connect connections  
- Different locations or routers  
- Provides backup connectivity  
  
---  
  
### 2. Maximum Resiliency  
- Multiple Direct Connect locations  
- Multiple independent connections per location  
- Fully redundant architecture  
  
**Explanation:** Maximum resiliency ensures no single failure point (location or connection).  
  
---  
  
## 11. Key Points  
  
- Direct Connect = **private dedicated connection (NOT internet-based)**  
- Uses:  
  - VGW (AWS side)  
  - Customer router (on-prem side)  
- Private VIF → VPC access  
- Public VIF → AWS public services  
- Takes long time to provision  
- Not encrypted by default (VPN can be added)  
- Direct Connect Gateway supports multi-region/VPC access  
- High and maximum resiliency architectures are important