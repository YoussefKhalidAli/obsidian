# EC2 Instance Purchasing Options

EC2 provides different purchasing options to **optimize cost based on workload type**.

---

## 1. On-Demand Instances

- Pay **per use** (per second for Linux/Windows, per hour for others)  
- No upfront cost  
- No long-term commitment  
- Highest cost option  

**Explanation:** Best for workloads that are unpredictable or short-term since you pay only for what you use without committing ahead of time.

**Use Case:**
- Short-term workloads  
- Unpredictable applications  
- Applications that cannot be interrupted  

---

## 2. Reserved Instances (RI)

- Commitment: **1 year or 3 years**  
- Up to **~72% discount** compared to On-Demand  
- Reserve specific attributes:
  - Instance type  
  - Region  
  - OS  
  - Tenancy  

- Payment options:
  - No upfront  
  - Partial upfront  
  - All upfront (max discount)

**Explanation:** Ideal for long-term, predictable workloads where you know the instance type and usage ahead of time. Discounts increase with longer commitments and upfront payment.

**Use Case:**
- Long-term, steady workloads (e.g., databases)

---

### 2.1 Convertible Reserved Instances

- Can change:
  - Instance type  
  - Instance family  
  - OS  
  - Tenancy  

- Lower discount (~66%) due to flexibility  

**Explanation:** Offers flexibility to adjust instances as your needs evolve, while still providing cost savings.

**Use Case:**
- Long-term workloads with changing requirements  

---

## 3. Savings Plans

- Commitment: **1 or 3 years**  
- Up to **~70% discount**  
- Commit to **spending amount ($/hour)** instead of instance type  

- Flexible across:
  - Instance size  
  - OS  
  - Tenancy  

- Locked to:
  - Instance family  
  - Region  

**Explanation:** Provides cost savings similar to RIs but with more flexibility in instance sizes, OS, and tenancy as long as you commit to a specific spending level.

**Use Case:**
- Long-term workloads with flexibility needs  

---

## 4. Spot Instances

- Up to **~90% discount** (cheapest option)  
- Can be **terminated at any time** if price exceeds your bid  

**Explanation:** Extremely cost-efficient, but instances can be interrupted, so only suitable for workloads that can handle disruption.

**Use Case:**
- Batch jobs  
- Data processing  
- Distributed workloads  
- Fault-tolerant applications  

**Not Suitable For:**
- Critical applications  
- Databases  

---

## 5. Dedicated Hosts

- **Physical server dedicated to you**  
- Full control over instance placement  
- Most expensive option  

**Explanation:** Provides full visibility and control over physical servers, useful for licensing requirements or strict compliance regulations.

**Use Case:**
- Compliance requirements  
- Bring Your Own License (BYOL)  
- Licensing based on cores/sockets  

---

## 6. Dedicated Instances

- Instances run on **dedicated hardware**  
- No other customers share the hardware  
- No control over physical server  

**Explanation:** Guarantees isolation at the hardware level but does not provide access to the underlying server. Slightly cheaper than Dedicated Hosts.

**Difference from Dedicated Hosts:**
- Dedicated Instance → no shared hardware  
- Dedicated Host → full control of physical server  

---

## 7. Capacity Reservations

- Reserve capacity in a **specific AZ**  
- No time commitment  
- **No discount** (charged at On-Demand rates)  
- Pay even if you don’t use it  

**Explanation:** Ensures that instances can always be launched in a specific AZ, ideal for critical workloads that need guaranteed capacity.

**Use Case:**
- Need guaranteed capacity in a specific AZ  
- Short-term, critical workloads  

---

## 8. Summary
- On-Demand → short-term, flexible, expensive  
- Reserved → long-term, steady, high discount  
- Convertible RI → flexible long-term, lower discount  
- Savings Plan → flexible usage commitment  
- Spot → cheapest, can be interrupted  
- Dedicated Host → full physical server control (compliance/licensing)  
- Dedicated Instance → no shared hardware  
- Capacity Reservation → guarantee capacity, no discount  

---

## 9. Quick Decision Guide

- Unpredictable → On-Demand  
- Long-term stable → Reserved Instances  
- Long-term flexible → Savings Plan  
- Fault-tolerant → Spot  
- Compliance / licensing → Dedicated Host  
- Guaranteed capacity → Capacity Reservation  