  
A **NAT Gateway** is a fully managed AWS service that allows **instances in private subnets to access the internet securely**, without allowing inbound internet traffic to those instances.  
  
It is the **modern replacement for NAT Instances**.  
  
---  
  
## 1. Purpose of NAT Gateway  
  
- Enables **outbound internet access** for private subnet resources  
- Blocks **inbound internet traffic** from reaching private instances  
- Used for:  
- Software updates  
- External API calls  
- Package downloads  
  
**Explanation:** NAT Gateway allows private instances to reach the internet without being directly exposed.  
  
---  
  
## 2. Key Characteristics  
  
- Fully **managed by AWS**  
- No need for EC2 management or patching  
- Automatically highly available within a single AZ  
- High performance and scalability  
- No security group configuration required  
  
**Explanation:** Unlike NAT instances, AWS handles all operational complexity for NAT Gateways.  
  
---  
  
## 3. Deployment  
  
- Created inside a **public subnet**  
- Requires an **Elastic IP address**  
- Must be used with an **Internet Gateway attached to the VPC**  
  
**Explanation:** The NAT Gateway itself sits in a public subnet and uses the Internet Gateway to reach the internet.  
  
---  
  
## 4. How NAT Gateway Works  
  
### Traffic Flow:  
1. Private EC2 sends traffic to internet  
2. Route table sends traffic to NAT Gateway  
3. NAT Gateway forwards traffic to Internet Gateway  
4. Internet responds to NAT Gateway  
5. NAT Gateway returns response to private EC2  
  
**Explanation:** NAT Gateway performs network address translation, replacing private IPs with its public Elastic IP for outbound traffic.  
  
---  
  
## 5. Route Table Requirement  
  
- Private subnet route table must include:  
- Destination: `0.0.0.0/0`  
- Target: NAT Gateway  
  
**Explanation:** This ensures all internet-bound traffic from private instances goes through the NAT Gateway.  
  
---  
  
## 6. High Availability  
  
- NAT Gateway is **highly available within a single Availability Zone**  
- It is **not automatically cross-AZ redundant**  
- Best practice:  
- Deploy **one NAT Gateway per AZ**  
  
**Explanation:** If an AZ fails, the NAT Gateway in that AZ also becomes unavailable unless another NAT Gateway exists in a different AZ.  
  
---  
  
## 7. Performance  
  
- Baseline throughput: ~5 Gbps  
- Can scale up to ~100 Gbps automatically  
  
**Explanation:** NAT Gateway is designed for high throughput workloads without manual scaling.  
  
---  
  
## 8. Security  
  
- Does NOT use security groups  
- Security is handled via:  
- Route tables  
- NACLs (Network ACLs)  
  
**Explanation:** Since it is a managed service, AWS removes the need for security group management.  
  
---  
  
## 9. Cost Model  
  
- Charged per:  
- Hour of usage  
- Amount of data processed  
  
**Explanation:** You pay for both uptime and traffic passing through the NAT Gateway.  
  
---  
  
## 10. NAT Gateway vs NAT Instance  
  
| Feature | NAT Gateway | NAT Instance |  
|--------|-------------|-------------|  
| Management | Fully managed | User managed |  
| Scalability | Automatic | Manual |  
| Availability | High (per AZ) | Not high by default |  
| Performance | Up to 100 Gbps | Depends on EC2 type |  
| Security Groups | Not required | Required |  
| Maintenance | None | User responsibility |  
| Use as Bastion Host | No | Yes (possible) |  
  
---  
  
## 11. Key Points  
  
- NAT Gateway enables **outbound internet access from private subnets**  
- Requires **Elastic IP + Internet Gateway**  
- Must be placed in a **public subnet**  
- No security group configuration required  
- Highly available within a single AZ  
- Preferred over NAT Instances in modern AWS architectures