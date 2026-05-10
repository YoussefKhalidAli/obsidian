  
AWS provides two main layers of network security in a VPC:  
- Security Groups (instance level)  
- Network ACLs (subnet level)  
  
---  
  
## 1. Security Groups  
  
Security Groups act as a **virtual firewall at the EC2 instance level**.  
  
### Key Characteristics  
- Attached to **EC2 instances (ENI level)**  
- **Stateful**  
- Only **ALLOW rules**  
- Automatically allows return traffic  
  
### Stateful (important concept)  
- If inbound traffic is allowed → return traffic is automatically allowed  
- No need to define outbound rules for responses  
  
### Behavior  
- Evaluates all rules together  
- If at least one rule allows traffic → it is allowed  
- Otherwise → denied  
  
---  
  
## 2. Network ACLs (NACLs)  
  
NACLs act as a **firewall at the subnet level**.  
  
### Key Characteristics  
- Applied to **subnets**  
- One NACL per subnet (default or custom)  
- **Stateless**  
- Supports **ALLOW and DENY rules**  
  
### Stateless (important concept)  
- Inbound and outbound traffic are evaluated separately  
- Return traffic must also be explicitly allowed  
  
---  
  
## 3. Security Groups vs NACLs (Core Difference)  
  
| Feature | Security Group | NACL |  
|----------|---------------|------|  
| Level | Instance | Subnet |  
| Type | Stateful | Stateless |  
| Rules | Allow only | Allow + Deny |  
| Return traffic | Automatically allowed | Must be explicitly allowed |  
| Evaluation | All rules considered | First match wins |  
  
---  
  
## 4. Traffic Flow (How they work together)  
  
When a request enters a subnet:  
  
### Inbound traffic  
1. NACL inbound rules are evaluated first  
2. If allowed → traffic enters subnet  
3. Security Group inbound rules are evaluated  
4. If allowed → reaches EC2 instance  
  
### Outbound response  
1. Security Group automatically allows return traffic (stateful)  
2. NACL outbound rules are evaluated (stateless requirement)  
3. Response leaves subnet if allowed  
  
---  
  
## 5. Rule Evaluation Order (NACL)  
  
- Rules are numbered from **1 to 32,000**  
- Lower number = higher priority  
- **First matching rule wins**  
- Last rule is `*` (implicit deny)  
  
### Default behavior  
- New NACLs deny everything by default (until rules are added)  
  
---  
  
## 6. Default NACL  
  
- Automatically created with every VPC  
- Allows **all inbound and outbound traffic**  
- Associated with all subnets unless replaced  
  
---  
  
## 7. NACL Use Case  
  
NACLs are useful for:  
- Blocking a **specific IP address at subnet level**  
- Adding an extra layer of security before traffic reaches instances  
  
---  
  
## 8. Ephemeral Ports (Very Important Concept)  
  
### What are ephemeral ports?  
Ephemeral ports are **temporary ports used by clients for outgoing connections**.  
  
When a client connects to a server:  
- Server uses a fixed port (e.g., 80, 443, 3306)  
- Client uses a **random temporary port (ephemeral port)**  
  
---  
  
### Why they exist  
- Allow return traffic from server → client  
- Each connection gets a temporary source port  
  
---  
  
### Typical ranges  
- Windows: 49152 – 65535  
- Linux: ~32768 – 65535  
  
---  
  
## 9. Why Ephemeral Ports matter in NACLs  
  
Because NACLs are stateless:  
  
When a DB responds to a client:  
- Response uses client’s ephemeral port  
  
So NACL must allow:  
- Inbound AND outbound traffic on **ephemeral port ranges**  
  
Otherwise:  
- Return traffic will be blocked  
  
---  
  
## 10. Example Flow (Simplified)  
  
Client → Database:  
- Outbound: client → DB port (e.g. 3306)  
- Inbound: DB → client ephemeral port  
  
Both directions must be allowed in:  
- Security Group (stateful handles return automatically)  
- NACL (must explicitly allow both directions)  
  
---  
  
## 11. Key Points  
  
- Security Groups = instance level firewall  
- NACLs = subnet level firewall  
- Security Groups are stateful  
- NACLs are stateless  
- NACLs require explicit inbound + outbound rules  
- Ephemeral ports are critical for return traffic  
- First match wins in NACLs