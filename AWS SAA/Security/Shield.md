  
AWS Shield is a service used to **protect AWS applications from DDoS (Distributed Denial of Service) attacks**.  
  
---  
  
## 1. What is a DDoS Attack?  
  
- Distributed Denial of Service (DDoS)  
- Attack where **many machines flood a system with traffic**  
  
**Explanation:**  
- Goal is to **overwhelm infrastructure**  
- Prevent real users from accessing the service  
- Uses large numbers of compromised devices (botnets)  
  
---  
  
## 2. AWS Shield Standard  
  
- **Free service**  
- Automatically enabled for all AWS customers  
  
### Protection includes:  
- SYN flood attacks  
- UDP floods  
- Reflection attacks  
- Layer 3 (Network layer) attacks  
- Layer 4 (Transport layer) attacks  
  
**Explanation:**  
Provides **baseline DDoS protection** for AWS resources without any configuration.  
  
---  
  
## 3. AWS Shield Advanced  
  
- **Paid service (~$3000/month per organization)**  
- Provides **enhanced DDoS protection**  
  
### Protects against:  
- More sophisticated DDoS attacks  
- Application-aware attacks (Layer 7)  
  
---  
  
### Supported Services:  
- EC2  
- Elastic Load Balancing (ALB/NLB/CLB)  
- CloudFront  
- AWS Global Accelerator  
- Route 53  
  
---  
  
## 4. Key Features of Shield Advanced  
  
### 1. 24/7 DDoS Response Team (DRT)  
- Direct access to AWS security experts during attacks  
  
---  
  
### 2. Cost Protection  
- Protects against **unexpected scaling costs caused by DDoS attacks**  
  
---  
  
### 3. Automatic Layer 7 Mitigation  
- Works with AWS WAF  
- Automatically:  
  - Creates  
  - Evaluates  
  - Deploys WAF rules  
  
**Explanation:**  
Helps block **application-layer attacks (HTTP/HTTPS)** without manual rule creation.  
  
---  
  
## 5. Shield vs Shield Advanced  
  
| Feature | Shield Standard | Shield Advanced |  
|--------|----------------|----------------|  
| Cost | Free | Paid |  
| Layer 3/4 protection | Yes | Yes |  
| Layer 7 protection | No | Yes (via WAF integration) |  
| DDoS Response Team | No | Yes |  
| Cost protection | No | Yes |  
  
---  
  
## 6. Key Points  
  
- Protects against **DDoS attacks**  
- Shield Standard is **automatic and free**  
- Shield Advanced adds:  
  - Advanced protection  
  - WAF integration  
  - 24/7 expert support  
  - Cost protection  
- Works across major AWS edge and compute services