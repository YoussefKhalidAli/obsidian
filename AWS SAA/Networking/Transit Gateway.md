  
AWS Transit Gateway is a **network hub service** that simplifies complex VPC networking by providing a **central point to connect multiple VPCs and on-premises networks**.  
  
---  
  
## 1. Problem It Solves  
  
Without Transit Gateway:  
- Multiple VPCs require **many VPC peering connections**  
- On-premises connectivity requires:  
  - Site-to-Site VPN  
  - Direct Connect  
  - Direct Connect Gateway  
- This creates a **complex, hard-to-manage network mesh**  
  
**Explanation:** As the number of VPCs grows, managing individual connections becomes inefficient and unscalable.  
  
---  
  
## 2. What Transit Gateway Does  
  
- Acts as a **central hub (hub-and-spoke model)**  
- Connects:  
  - Multiple VPCs  
  - On-premises networks  
  - Site-to-Site VPN connections  
  - Direct Connect (via Direct Connect Gateway)  
  
**Explanation:** Instead of connecting everything to everything, everything connects to one central router-like service.  
  
---  
  
## 3. Key Concept: Transitive Routing  
  
- VPCs connected to Transit Gateway can communicate with each other **through the gateway**  
- No need for direct VPC peering  
  
**Explanation:** This is called *transitive connectivity* — traffic can pass through the Transit Gateway to reach other networks.  
  
---  
  
## 4. Core Components  
  
### Transit Gateway (TGW)  
- Central routing hub  
- Regional AWS service  
  
---  
  
### Attachments  
- VPC attachment → connects VPCs  
- VPN attachment → connects on-prem via Site-to-Site VPN  
- Direct Connect attachment → connects via Direct Connect Gateway  
  
---  
  
### Route Tables  
- Control **which networks can communicate**  
- Define allowed traffic paths between attachments  
  
**Explanation:** Route tables in Transit Gateway act as traffic control policies.  
  
---  
  
## 5. Multi-Account and Multi-Region Support  
  
- Supports **AWS Resource Access Manager (RAM)** for sharing across accounts  
- Supports **cross-region peering between Transit Gateways**  
  
**Explanation:** This allows building global network architectures across multiple AWS accounts and regions.  
  
---  
  
## 6. Direct Connect + Transit Gateway  
  
- Direct Connect Gateway connects to Transit Gateway  
- Enables:  
  - On-prem → TGW → multiple VPCs  
  - Cross-account VPC access via one Direct Connect link  
  
**Explanation:** One Direct Connect connection can serve multiple VPCs and accounts through Transit Gateway.  
  
---  
  
## 7. Site-to-Site VPN + Transit Gateway  
  
- VPN connections attach to Transit Gateway instead of a single VPC  
- Allows multiple VPCs to be reachable through one VPN setup  
  
---  
  
## 8. ECMP (Equal-Cost Multi-Path Routing)  
  
- Used to **increase VPN throughput**  
- Splits traffic across multiple equal-cost paths (tunnels)  
  
### How it works:  
- Each Site-to-Site VPN connection has **2 tunnels**  
- With Transit Gateway:  
  - Multiple VPN connections can be used simultaneously  
  - More tunnels = more bandwidth  
  
**Explanation:** ECMP allows AWS to load balance traffic across multiple VPN tunnels for higher performance.  
  
---  
  
## 9. Performance Differences  
  
### VPN to VGW (without TGW)  
- Single VPC connection  
- ~1.5 Gbps max throughput  
  
---  
  
### VPN to Transit Gateway  
- Multiple VPCs via single hub  
- Uses ECMP across multiple tunnels  
- Can scale up to higher throughput (~2.5 Gbps per connection, more with multiple VPNs)  
  
---  
  
## 10. Key Features  
  
- Simplifies complex network architectures  
- Hub-and-spoke model  
- Supports:  
  - VPCs  
  - VPN  
  - Direct Connect  
- Route-based traffic control  
- Cross-account networking support  
- Cross-region peering support  
  
---  
  
## 11. Direct Connect Sharing (Multi-Account)  
  
- Direct Connect → Direct Connect Gateway → Transit Gateway  
- Transit Gateway shares connectivity across:  
  - Multiple VPCs  
  - Multiple AWS accounts  
  
**Explanation:** One physical Direct Connect link can be reused across many environments.  
  
---  
  
## 12. Key Points  
  
- Transit Gateway = **network hub for AWS networking**  
- Eliminates need for complex VPC peering mesh  
- Supports:  
  - VPC attachments  
  - VPN attachments  
  - Direct Connect via DX Gateway  
- Uses **route tables for segmentation**  
- Enables **ECMP for VPN performance scaling**  
- Supports **multi-account and multi-region architectures**