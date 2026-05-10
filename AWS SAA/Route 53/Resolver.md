## 1. What is Route 53 Resolver?

- The **Route 53 Resolver** is the DNS service inside your VPC.
- It automatically resolves:
  - **Private Hosted Zones**
  - **Public DNS records**
  - **Internal AWS resource DNS (EC2, etc.)**

### Default Behavior:
- EC2 instances query the **VPC resolver**
- Resolver answers:
  - AWS internal domains
  - Route 53 records (public + private)

---

## 2. Why Do We Need Resolver Endpoints?

By default:
- AWS DNS ↔ AWS resources only

But in real-world scenarios:
- You may have **on-premises infrastructure**
- You need **Hybrid DNS**

### Goal:
- Allow DNS resolution:
  - **On-prem → AWS**
  - **AWS → On-prem**

---

## 3. Hybrid DNS Architecture

Requires:
- Network connectivity:
  - **VPN** OR
  - **Direct Connect**

---

## 4. Resolver Endpoints

### 4.1 Inbound Endpoint (On-Prem → AWS)

- Allows **on-premises DNS servers** to resolve AWS domains

#### Flow:
1. On-prem server queries DNS (e.g., `app.aws.internal`)
2. Query goes to on-prem DNS resolver
3. Resolver forwards query to **Inbound Endpoint**
4. Route 53 Resolver resolves using:
   - Private Hosted Zone
   - AWS DNS
5. Response returned to on-prem server

#### Use Case:
- Access AWS resources using **private DNS names**

---

### 4.2 Outbound Endpoint (AWS → On-Prem)

- Allows AWS resources to resolve **on-prem DNS**

#### Flow:
1. EC2 queries DNS (e.g., `db.onprem.local`)
2. Route 53 Resolver receives query
3. Forwards to **Outbound Endpoint**
4. Query sent to on-prem DNS resolver
5. Response returned to EC2

#### Use Case:
- Access **on-prem resources using DNS names**

---

## 5. Key Differences

| Feature | Inbound Endpoint | Outbound Endpoint |
|--------|----------------|------------------|
| Direction | On-Prem → AWS | AWS → On-Prem |
| Who initiates query | On-prem DNS | AWS (EC2, etc.) |
| Purpose | Resolve AWS private domains | Resolve on-prem domains |

---

## 6. Important Concepts

- Requires:
  - **VPN or Direct Connect**
- Works with:
  - **Private Hosted Zones**
- Enables:
  - **Hybrid Cloud DNS resolution**

---

## 7. Key Points

- On-prem needs to resolve AWS DNS → **Inbound Endpoint**
- AWS needs to resolve on-prem DNS → **Outbound Endpoint**
- Hybrid DNS always requires:
  - **Resolver endpoints + network connectivity**

---

## 8. Quick Memory Trick

- **Inbound = Into AWS**
- **Outbound = Out of AWS**