  
A **VPC (Virtual Private Cloud)** is a logically isolated network inside AWS where you can launch AWS resources like EC2 instances.  
  
It gives you control over:  
- IP addressing  
- Subnets  
- Routing  
- Network access  
  
---  
  
## 1. VPC Overview  
  
- A VPC exists **inside a single AWS Region**  
- You can create **multiple VPCs per region**  
- Each VPC uses an **IPv4 CIDR block**  
  
**Explanation:** A VPC is your own private network in AWS, similar to a data center network, but fully virtual and isolated.  
  
---  
  
## 2. CIDR Blocks in a VPC  
  
- A VPC can have **multiple CIDR blocks (up to 5)**  
- CIDR size range:  
- Minimum: `/28` → 16 IP addresses  
- Maximum: `/16` → 65,536 IP addresses  
- Only **private IPv4 ranges** are allowed:  
- `10.0.0.0/8`  
- `172.16.0.0/12`  
- `192.168.0.0/16`  
  
**Explanation:** CIDR defines the IP range of your VPC. AWS restricts this to private IP ranges to ensure isolation from the public internet.  
  
---  
  
## 3. CIDR Design Rules  
  
- CIDR blocks must **not overlap** with:  
- Other VPCs  
- On-premises networks  
- Corporate networks  
  
**Explanation:** Overlapping IP ranges prevent network connectivity (e.g., VPC peering or VPN connections). Proper planning is required for hybrid cloud setups.  
  
---  
  
## 4. Subnets  
  
A **subnet** is a smaller IP range inside a VPC.  
  
- Each subnet is placed in **one Availability Zone**  
- Used to organize resources within a VPC  
  
---  
  
### 4.1 Reserved IP Addresses in Subnets  
  
AWS reserves **5 IP addresses per subnet**:  
  
- First IP → Network address  
- Second IP → VPC router  
- Third IP → AWS DNS  
- Fourth IP → Reserved for future use  
- Last IP → Network broadcast address (not used in AWS)  
  
**Explanation:** These addresses cannot be assigned to EC2 instances, so they reduce usable IP capacity in each subnet.  
  
---  
  
### 4.2 Subnet Sizing  
  
- Example `/24` subnet = 256 IPs  
- Minus 5 reserved IPs = 251 usable IPs  
  
**Explanation:** Always subtract 5 IPs when calculating usable capacity.  
  
---  
  
## 5. Public vs Private Subnets  
  
- **Public Subnet**  
- Has a route to an Internet Gateway  
- Instances can access the internet (if allowed)  
  
- **Private Subnet**  
- No direct route to the internet  
- Used for internal services (databases, backend systems)  
  
**Explanation:** The difference is not the subnet itself, but the **route table configuration**.  
  
---  
  
## 6. Internet Gateway (IGW)  
  
An **Internet Gateway** allows communication between a VPC and the internet.  
  
- Attached to a VPC  
- Fully managed and highly available  
- Scales automatically  
- One IGW per VPC  
  
---  
  
### 6.1 Important Rules  
  
- A VPC can only have **one Internet Gateway**  
- An Internet Gateway must be **explicitly attached to a VPC**  
- IGW alone does not provide internet access  
  
**Explanation:** The IGW is just a gateway component — it does nothing until routing is configured.  
  
---  
  
### 6.2 Route Tables Requirement  
  
To enable internet access:  
  
- You must update the **route table**  
- Add a route:  
- Destination: `0.0.0.0/0`  
- Target: Internet Gateway  
  
**Explanation:** Without route table configuration, instances cannot reach the internet even if an IGW exists.  
  
---  
  
## 7. How Internet Access Works  
  
1. EC2 instance sends traffic  
2. Route table directs traffic to IGW  
3. Internet Gateway forwards traffic to the internet  
4. Response returns through the same path  
  
**Explanation:** Internet access in AWS is controlled entirely by routing rules, not just subnet type.  
  
---  
  
## 8. Key Points  
  
- VPC = isolated virtual network in AWS  
- Subnets = subdivisions of a VPC (1 per AZ)  
- CIDR defines IP range (must not overlap)  
- 5 IPs per subnet are always reserved  
- Public subnet = route to IGW  
- Private subnet = no internet route  
- IGW requires route table configuration to work