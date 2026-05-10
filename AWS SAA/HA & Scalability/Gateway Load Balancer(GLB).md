## 1. What is GWLB?
- **Gateway Load Balancer (GWLB)** operates at:
  - **Layer 3 (Network Layer)**  
- Used to:
  - **Deploy, scale, and manage network security appliances**  
---
## 2. Main Purpose
- Force **all network traffic** to pass through:
  - Firewalls  
  - Intrusion Detection/Prevention Systems (IDS/IPS)  
  - Deep Packet Inspection systems  
---

## 3. How It Works (Conceptually)
- All traffic is routed through the GWLB  
- GWLB forwards traffic to **security appliances**  
- Appliances:
  - Inspect / filter / modify traffic  
  - Drop or allow traffic  
- If allowed → traffic → GLB → application  
- If denied → traffic is dropped  
---

## 4. Key Features
### 4.1 Transparent Gateway
- Acts as a **single entry and exit point** for traffic  
- Applications do **not know inspection is happening**  

---

### 4.2 Load Balancing
- Distributes traffic across multiple:
  - Security appliances  

---

## 5. Target Groups
- GWLB routes traffic to **target groups of appliances**
### Supported Targets:
- EC2 instances (running security software)  
- Private IP addresses  

---

## 6. Use Cases

- Centralized firewall deployment  
- Intrusion detection / prevention  
- Network traffic monitoring  
- Security inspection layer in VPC  

---
## 7. Protocol (VERY IMPORTANT)
- Uses:
  - **GENEVE protocol**
  - Port: **6081**
---

## 8. Key Characteristics
- Works at **IP packet level (Layer 3)**  
- Requires **VPC route table configuration**  
- Transparent to applications  
- Used for **network security architectures**  

---
## 10. Key Points
- GWLB = **network security load balancer**  
- Forces traffic through **security appliances**  
- Combines:
  - **Gateway (traffic routing)**  
  - **Load balancing (distribution)**  
