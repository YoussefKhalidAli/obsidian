  
A Site-to-Site VPN is a **secure, encrypted connection over the public internet** between an on-premises network (corporate data center) and an AWS VPC.  
  
---  
  
## 1. Purpose  
  
- Connect **on-premises network ↔ AWS VPC**  
- Extend corporate network into AWS securely  
- Use **encryption over the public internet**  
  
**Explanation:** Even though traffic travels over the internet, it is encrypted, so it behaves like a private connection between both networks.  
  
---  
  
## 2. Main Components  
  
### Customer Gateway (CGW)  
- Located on the **on-premises (customer) side**  
- Can be:  
  - Physical device (router/firewall)  
  - Software-based VPN device  
- Identified by an **IP address (public or NAT public IP)**  
  
**Explanation:** This represents your corporate network endpoint in the VPN connection.  
  
---  
  
### Virtual Private Gateway (VGW)  
- Located on the **AWS side**  
- Attached to a **VPC**  
- Acts as a **VPN concentrator**  
  
**Explanation:** This is the AWS endpoint that connects your VPC to the on-premises network.  
  
---  
  
## 3. How the Connection Works  
  
- A VPN tunnel is created between:  
  - CGW (on-premises)  
  - VGW (AWS VPC)  
- Traffic is:  
  - **Encrypted**  
  - Sent over the **public internet**  
- Once established, both networks can communicate as if they are directly connected  
  
---  
  
## 4. Customer Gateway IP Scenarios  
  
### Public IP Scenario  
- CGW has a public IP address  
- This IP is used to establish the VPN connection  
  
### Private IP Scenario (Behind NAT)  
- CGW is behind a NAT device  
- NAT device must have a **public IP**  
- VPN connection uses the **public IP of the NAT device**  
  
**Explanation:** AWS always needs a reachable public IP to establish the VPN tunnel.  
  
---  
  
## 5. Route Propagation  
  
- Required to make VPN traffic work correctly in the VPC  
- Automatically adds VPN routes into route tables  
  
**Explanation:** Without route propagation, AWS will not know how to send traffic to the on-premises network.  
  
---  
  
## 6. Security Group Consideration  
  
- Security Groups control inbound/outbound traffic to EC2  
- If you want to ping (ICMP) EC2 from on-premises:  
  - You must allow **ICMP inbound traffic** in the Security Group  
  
**Explanation:** VPN only connects networks. Security Groups still control whether traffic is allowed to reach the instance.  
  
---  
  
## 7. AWS VPN CloudHub  
  
- Used to connect **multiple on-premises sites together via AWS VPN**  
- Uses a **hub-and-spoke model**  
  - AWS VGW = hub  
  - Multiple customer gateways = spokes  
  
**Explanation:** Instead of each site connecting directly to each other, they connect through AWS using VPN connections.  
  
### Key Characteristics:  
- Uses multiple Site-to-Site VPN connections  
- All traffic goes through AWS VGW  
- Enables communication between different on-premises locations  
- Still uses the public internet (encrypted VPN tunnels)  
  
---  
  
## 8. Key Points  
  
- Site-to-Site VPN connects **on-premises ↔ AWS VPC**  
- Uses **Customer Gateway (CGW)** and **Virtual Private Gateway (VGW)**  
- Traffic is **encrypted over the internet**  
- Requires **route propagation** for proper routing  
- Security Groups still control access to EC2 instances  
- CloudHub allows **multi-site VPN connectivity through AWS**