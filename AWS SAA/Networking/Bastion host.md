  
A Bastion Host is an **EC2 instance placed in a public subnet** that acts as a **secure entry point** to access EC2 instances located in private subnets.  
  
---  
  
## 1. Purpose of a Bastion Host  
  
- Used to access **private EC2 instances** that do not have direct internet access  
- Acts as a **bridge (jump server)** between the internet and private network  
- Allows secure SSH access into private resources  
  
**Explanation:** Since private EC2 instances are not reachable from the internet, the bastion host provides a controlled way to reach them without exposing them publicly.  
  
---  
  
## 2. Architecture Idea  
  
- Users are on the **public internet**  
- Bastion host is in a **public subnet**  
- Private EC2 instances are in a **private subnet**  
- All resources are inside the same **VPC**  
  
**Explanation:** The bastion host is the only entry point exposed to the internet, while private instances remain isolated.  
  
---  
  
## 3. How Access Works  
  
1. User connects to the **bastion host via SSH**  
2. From the bastion host, user connects to the **private EC2 instance via SSH**  
3. Communication happens entirely inside the VPC after the first hop  
  
**Explanation:** The bastion host is a two-step access method: internet → bastion → private instance.  
  
---  
  
## 4. Security Groups Configuration  
  
### 4.1 Bastion Host Security Group  
  
- Allows **SSH (port 22)** access from:  
- A restricted set of public IPs (e.g., corporate IP range)  
- Should NOT allow open access from `0.0.0.0/0`  
  
**Explanation:** The bastion host is exposed to the internet, so it must be tightly restricted to prevent unauthorized access.  
  
---  
  
### 4.2 Private EC2 Security Group  
  
- Allows **SSH (port 22)** access from:  
- The **bastion host security group** OR  
- The bastion host private IP  
  
**Explanation:** Private instances only trust traffic coming from the bastion host, not from the internet directly.  
  
---  
  
## 5. Key Security Principle  
  
- Bastion host is the **only publicly accessible machine**  
- Private EC2 instances are **never exposed to the internet**  
- Access is controlled using **security groups and SSH rules**  
  
**Explanation:** This design minimizes attack surface by limiting direct exposure of internal resources.  
  
---  
  
## 6. Key Points  
  
- Bastion host = EC2 instance in a **public subnet**  
- Used as a **jump server for SSH access**  
- Private instances remain **non-internet accessible**  
- Bastion security group must be **highly restricted**  
- Private instance security group allows access only from bastion host