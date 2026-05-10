# Network Load Balancer (NLB) Cheat Sheet

---
## 1. What is NLB?
- **Network Load Balancer (NLB)** operates at:
  - **Layer 4 (Transport Layer)**  
- Handles:
  - **TCP**
  - **UDP**
  - **TLS**
---

## 2. Key Features
- **Ultra-high performance**
  - Handles **millions of requests per second**  
- **Ultra-low latency**
  - Much faster than ALB  
- **Static IP support**
  - One **static IP per AZ**  
  - Can assign **Elastic IPs**  
---
## 3. When to Use NLB
- Need **extreme performance**  
- Need **low latency**  
- Need **TCP/UDP support**  
- Need **static IP addresses**  
---
## 4. Static IP (VERY IMPORTANT)
- NLB provides:
  - **Fixed IP per Availability Zone**  
- Can attach:
  - **Elastic IPs (EIP)**  
### Use Case
- Applications that require:
  - Whitelisted IPs  
  - Fixed endpoints  

---

## 5. Target Groups
- NLB routes traffic to **Target Groups**
### Supported Targets:
- EC2 instances  
- Private IP addresses  
- Load Balancers
---
### Important Notes
- IP targets must be:
  - **Private IPs only**  
- Can include:
  - EC2 instances  
  - On-premises servers (via private IP)  
---
## 6. Hybrid Architecture
- NLB can front:
  - EC2 instances  
  - On-prem servers  
- Can also be placed **in front of an ALB**
### Why combine NLB + ALB?
- NLB → provides **static IP + performance**  
- ALB → provides **advanced HTTP routing**  
---

## 7. Health Checks
- Supported protocols:
  - TCP  
  - HTTP  
  - HTTPS  
- Determines if targets are healthy  
- Unhealthy targets → **no traffic sent**  

---
## 9. Key Points
- NLB = **high performance, low latency load balancer**  
- Works with **TCP/UDP traffic**  
- Supports **static IPs (Elastic IPs)**  
- Can route to **EC2 or private IPs**  
- Can be combined with ALB  

---

## 10. Tips

- **TCP/UDP → NLB**  
- **Need static IP → NLB**  
- **High performance → NLB**  
- **Low latency → NLB**  

- Use ALB when:
  - HTTP routing needed  

- Use NLB when:
  - Performance or networking requirements are critical  

---