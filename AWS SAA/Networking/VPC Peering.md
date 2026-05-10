  
VPC Peering is a way to **connect two VPCs using the AWS private network** so they can communicate as if they are in the same network.  
  
---  
  
## 1. What is VPC Peering?  
  
- A networking connection between **two VPCs**  
- Enables private communication between VPCs  
- Works across:  
- Same AWS account  
- Different AWS accounts  
- Different AWS regions  
  
**Explanation:** VPC Peering allows isolated VPCs to talk to each other without using the public internet.  
  
---  
  
## 2. Key Requirement (CIDR)  
  
- The CIDR blocks of the VPCs **must NOT overlap**  
  
**Explanation:** If IP ranges overlap, AWS cannot route traffic correctly between the VPCs.  
  
---  
  
## 3. How VPC Peering Works  
  
When two VPCs are peered:  
  
- Traffic stays on the **AWS private network**  
- You must manually configure routing  
  
However:  
- Peering does NOT automatically enable communication  
- You must update **route tables in both VPCs**  
  
---  
  
## 4. Route Tables Requirement  
  
To enable communication:  
  
Each VPC must have a route like:  
  
- Destination: CIDR of the other VPC  
- Target: VPC Peering Connection  
  
**Explanation:** Without route table updates, the peering connection exists but no traffic can flow.  
  
---  
  
## 5. Non-Transitive Nature  
  
VPC Peering is **NOT transitive**.  
  
If you have:  
- VPC A ↔ VPC B  
- VPC B ↔ VPC C  
  
Then:  
- A can talk to B  
- B can talk to C  
- BUT A cannot talk to C automatically  
  
You must explicitly create:  
- VPC A ↔ VPC C  
  
**Explanation:** Each peering connection is independent.  
  
---  
  
## 6. Supported Scenarios  
  
VPC Peering supports:  
  
- Same AWS account  
- Different AWS accounts  
- Same region  
- Cross-region peering  
  
**Explanation:** This makes it useful for multi-account and multi-region architectures.  
  
---  
  
## 7. Security Group Referencing (Important Feature)  
  
In peered VPCs (same region, cross-account supported):  
  
- You can reference **security groups from another VPC**  
- Instead of using CIDR IP ranges  
  
**Explanation:** This simplifies security rules by allowing identity-based access instead of IP-based rules.  
  
---  
  
## 8. Limitations  
  
- No transitive routing  
- Requires manual route table updates  
- CIDR blocks must not overlap  
- One-to-one connection only (each peering is between two VPCs)  
  
---  
  
## 9. Key Points  
  
- VPC Peering connects **two VPCs privately**  
- Works across accounts and regions  
- CIDR blocks must not overlap  
- It is **NOT transitive**  
- Route tables must be updated manually  
- Security groups can be referenced across peered VPCs (same region, cross-account)