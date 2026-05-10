  
VPC Traffic Mirroring is a **network security and monitoring feature** that allows you to **copy (mirror) network traffic from ENIs without affecting the original traffic flow**.  
  
---  
  
## 1. Purpose  
  
- Capture network traffic in a VPC  
- Inspect traffic for:  
- Security analysis  
- Threat detection  
- Network troubleshooting  
- Do this in a **non-intrusive way**  
  
**Explanation:** The original EC2 instance continues working normally while a duplicate of its traffic is sent elsewhere for inspection.  
  
---  
  
## 2. How It Works  
  
Traffic Mirroring works by defining two main components:  
  
### 1. Source  
- The **Elastic Network Interface (ENI)** you want to monitor  
- Represents the traffic source (e.g., EC2 instance ENI)  
  
---  
  
### 2. Target  
- Where mirrored traffic is sent  
- Can be:  
- Another ENI (security appliance)  
- A Network Load Balancer (NLB)  
  
---  
  
## 3. Optional Filter  
  
- You can define filters to:  
- Capture all traffic  
- Capture only specific traffic (e.g., ports, protocols)  
  
**Explanation:** This helps reduce unnecessary data by only mirroring relevant traffic.  
  
---  
  
## 4. Architecture Example  
  
- EC2 instance generates network traffic  
- Traffic flows normally to:  
- Internet  
- Other AWS services  
- At the same time:  
- A copy of that traffic is mirrored  
- Sent to a **Network Load Balancer**  
- Forwarded to a group of EC2 instances running security tools  
  
**Explanation:** The EC2 instance is unaware that its traffic is being copied.  
  
---  
  
## 5. Key Characteristics  
  
- Non-intrusive (does not affect original traffic)  
- Works at the **ENI level**  
- Supports multiple source ENIs  
- Can send mirrored traffic to:  
- Security appliances  
- Monitoring systems  
  
---  
  
## 6. Requirements  
  
- Source and target must be:  
- In the same VPC  
- OR in different VPCs connected via VPC Peering  
  
---  
  
## 7. Use Cases  
  
- Network security inspection  
- Intrusion detection systems (IDS)  
- Threat monitoring  
- Troubleshooting network issues  
- Deep packet inspection  
  
---  
  
## 8. Key Points  
  
- Copies traffic from ENIs (not replacing it)  
- Does NOT interrupt normal traffic flow  
- Sends mirrored traffic to analysis tools  
- Uses Network Load Balancer or ENIs as targets  
- Works for security and debugging purposes