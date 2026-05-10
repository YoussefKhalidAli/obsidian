## 1. Overview

Routing policies define **how Route 53 responds to DNS queries**.

They do **NOT route traffic directly**, but instead:
- Return **different IPs/targets** based on rules

---

## 2. Types of Routing Policies

### 2.1 Simple Routing
- Single resource
- No health checks (by default)
- Can return multiple IPs (random)

---

### 2.2 Weighted Routing
- Split traffic based on **weights**
- Example:
  - Server A → 70%
  - Server B → 30%

---

### 2.3 Failover Routing
- Active-Passive setup
- Requires **health checks**
- If primary fails → traffic goes to secondary

---

### 2.4 Latency-Based Routing
- Routes users to **lowest latency region**
- Based on AWS network latency (not distance)

---

### 2.5 Geolocation Routing
- Routes based on **user location (country/continent)**
- You explicitly define mapping

---

### 2.6 Geoproximity Routing
- Routes based on **distance to resources**
- Allows **bias adjustment** (shift traffic)

---

### 2.7 Multi-Value Answer Routing
- Returns multiple healthy IPs
- Works like **simple load balancing with health checks**

---

## 3. Comparison Table — Geo vs Geoproximity vs Latency

| Feature | Geolocation Routing | Geoproximity Routing | Latency Routing |
|--------|--------------------|---------------------|-----------------|
| Based on | User **location (country/region)** | **Distance** between user & resource | **Network latency** |
| Configuration | Manual mapping (you define regions) | Automatic + optional **bias** | Automatic |
| Bias Control | ❌ No | ✅ Yes (increase/decrease traffic) | ❌ No |
| Use Case | Compliance, regional content | Traffic shaping across regions | Best performance |
| Example | Users in Egypt → Cairo server | Push more traffic to EU even if farther | Route to fastest AWS region |
| Precision | Country/continent level | Geographic distance | Real-time latency |

---

## 4. Comparison Table — Multiple Values vs Multi-Value Routing

| Feature | Simple Record (Multiple Values) | Multi-Value Routing |
|--------|--------------------------------|---------------------|
| Returns multiple IPs | ✅ Yes | ✅ Yes |
| Health checks | ❌ Not supported | ✅ Supported |
| Removes unhealthy instances | ❌ No | ✅ Yes |
| Load balancing | Basic (client-side) | Improved (filters unhealthy) |
| Max responses | All records | Up to 8 healthy records |
| Use case | Basic DNS response | Lightweight load balancing |

---

## 5. Key Notes

- **Latency routing ≠ geographic proximity**
  - Uses AWS network performance, not distance

- **Geolocation vs Geoproximity**
  - Geolocation = **rules you define**
  - Geoproximity = **distance + bias tuning**

- **Multi-value routing**
  - Not a replacement for ELB
  - Just improves DNS-level availability

---