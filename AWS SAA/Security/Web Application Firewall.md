  
AWS WAF is used to **protect web applications from common web attacks at Layer 7 (HTTP/HTTPS)**.  
  
---  
  
## 1. What is AWS WAF?  
  
- Protects against **application-layer attacks**  
- Works at **Layer 7 (HTTP/HTTPS)**  
  
**Explanation:**  
- Layer 7 → HTTP/HTTPS (WAF operates here)  
- Layer 4 → TCP/UDP (NOT supported by WAF)  
  
---  
  
## 2. Supported Services (Where WAF Can Be Attached)  
  
- Application Load Balancer (ALB)  
- API Gateway  
- CloudFront  
- AppSync (GraphQL APIs)  
- Cognito User Pools  
  
**Important:**  
- ❌ NOT supported on Network Load Balancer (NLB)  
  
---  
  
## 3. Web ACL (Access Control List)  
  
- Main component of WAF  
- Contains **rules** that define how traffic is handled  
  
**Actions:**  
- Allow  
- Block  
- Count (monitor only)  
  
---  
  
## 4. WAF Rules  
  
### 1. IP-based Rules  
- Allow or block specific IPs  
- Uses **IP sets** (up to 10,000 IPs per set)  
  
---  
  
### 2. HTTP-based Rules  
- Filter based on:  
- Headers  
- Body  
- Query strings  
- URI path  
  
---  
  
### 3. Protection Against Attacks  
- SQL Injection (SQLi)  
- Cross-Site Scripting (XSS)  
  
---  
  
### 4. Size Constraints  
- Limit request size (e.g., max body size)  
  
---  
  
### 5. Geo Match  
- Allow/block requests based on **country**  
  
---  
  
### 6. Rate-Based Rules  
- Limit number of requests per IP  
  
**Example:**  
- Block IP if > 1000 requests in 5 minutes  
  
**Use case:**  
- Basic DDoS mitigation  
  
---  
  
## 5. Rule Groups  
  
- Collection of rules  
- Reusable across multiple Web ACLs  
  
**Explanation:**  
Helps organize and reuse rule sets efficiently.  
  
---  
  
## 6. Scope of WAF  
  
- **Regional** (ALB, API Gateway, etc.)  
- **Global** when used with CloudFront  
  
---  
  
## 7. Key Architecture Pattern
  
### Problem:  
- Need:  
- WAF protection  
- Fixed/static IP  
  
### Issue:  
- ALB supports WAF but has **no fixed IP**  
- NLB has fixed IP but **does NOT support WAF**  
  
---  
  
### Solution:  
  
Use:  
- **Global Accelerator + ALB + WAF**  
  
**Architecture Flow:**  
1. Client → Global Accelerator (fixed IP)  
2. Global Accelerator → ALB  
3. WAF attached to ALB  
4. ALB → EC2 / backend  
  
---  
  
## 8. Key Points  
  
- WAF protects at **Layer 7 (HTTP/HTTPS)**  
- Use Web ACLs to define rules  
- Supports:  
- IP filtering  
- Rate limiting  
- Geo blocking  
- SQLi/XSS protection  
- ❌ Not supported on NLB  
- Use **Global Accelerator + ALB** for fixed IP + WAF