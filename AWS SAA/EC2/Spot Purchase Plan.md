# EC2 Spot Instances (Deep Dive)

Spot Instances allow you to use **unused AWS capacity at a very low cost**.

- Up to **~90% discount** compared to On-Demand  
- Can be **interrupted at any time**  

---

## 1. How Spot Instances Work

- You define a **maximum price (max price)** you are willing to pay  
- AWS sets a **current spot price** based on supply and demand  

**Behavior:**
- If **spot price ≤ max price** → instance runs  
- If **spot price > max price** → instance is interrupted  

**Explanation:** You are essentially bidding for spare capacity. As long as your bid is higher than the current price, you keep the instance.

---

## 2. Interruption Behavior

When a Spot Instance is about to be interrupted:

- You get a **2-minute warning (grace period)**  

### Options:

1. **Stop the instance** (persistent)
   - Saves state (EBS-backed only)  
   - Can restart later when price drops  

1. **Terminate the instance** (non-persistent)
   - Instance is deleted  
   - Start fresh next time  

**Explanation:** Choose based on whether your workload needs to preserve state.

---

## 3. Spot Block (Fixed Duration)

- Reserve a Spot Instance for **1 to 6 hours**  
- **No interruption during the block period (almost always)**  

**Explanation:** Useful when you need short-term reliability but still want Spot pricing.

---

## 4. Spot Pricing Behavior

- Prices **vary over time** based on:
  - Supply (available capacity)  
  - Demand  

- Prices also vary across:
  - **Availability Zones (AZs)**  
  - Instance types  

**Key Insight:**
- Setting a **higher max price** increases chances of keeping the instance  
- Setting a **low max price** may result in frequent interruptions  

---

## 5. Spot Instance Requests

A Spot Request defines:

- Number of instances  
- Max price  
- Launch configuration (AMI, type, etc.)  
- Validity period  
- Request type  

---

### 5.1 Request Types

#### One-Time Request
- Runs once when fulfilled  
- Does NOT relaunch instances if interrupted  

#### Persistent Request
- Keeps trying to maintain desired capacity  
- If instance stops → AWS **automatically relaunches it**  

**Explanation:** Persistent requests ensure continuous capacity, but can relaunch instances unexpectedly.

---

## 6. Termination Rules (VERY IMPORTANT)

To fully stop Spot Instances:

1. **Cancel the Spot Request first**  
2. Then **terminate the instances**

**Explanation:**  
- If you terminate instances first → AWS may relaunch them (persistent request)  
- Canceling request prevents new launches  

---

## 7. Spot Instance Pools

A **Spot Instance Pool** is a group of Spot Instances that share the same:

- Instance type (e.g., m5.large)  
- Availability Zone (AZ)  
- Operating system  

**Explanation:** Each unique combination of instance type + AZ = one pool.

---

## How Pools Work

- Each pool has:
  - Its own **Spot price**  
  - Its own **available capacity**  

- Prices and capacity **vary between pools**

**Example:**
- m5.large in us-east-1a → Pool A  
- m5.large in us-east-1b → Pool B  
- c5.large in us-east-1a → Pool C  

Each of these is a **separate pool** with different pricing and availability.

---

## Why Pools Matter

Spot Instances are interrupted when:
- The pool **runs out of capacity**, OR  
- The price **exceeds your max price**

**Explanation:** Some pools are more stable than others, so choosing the right pool reduces interruptions.

---

## 8. Spot Fleet

A Spot Fleet allows you to **launch multiple Spot Instances across different configurations**.

- Can include:
  - Multiple instance types  
  - Multiple AZs  
  - Optional On-Demand instances  

**Goal:** Meet a **target capacity** at the lowest cost  

---

### 8.1 Allocation Strategies

- **Lowest Price**
  - Chooses cheapest pool  
  - Best for cost optimization  

- **Diversified**
  - Spreads across multiple pools  
  - Improves availability  

- **Capacity Optimized**
  - Chooses pool with most available capacity  
  - Reduces interruptions  

- **Price-Capacity Optimized**
  - **Chooses from pool with highest capacity and then chooses lowest price**
  - Balance between cost and availability  
  - **Best choice for most workloads**

---

## 9. When to Use Spot Instances

**Good For:**
- Batch processing  
- Data analysis  
- Image/video processing  
- Distributed workloads  
- Fault-tolerant systems  

**Not Suitable For:**
- Critical applications  
- Databases  
- Stateful systems without recovery  

---

## 10. Key Points

- Up to **90% cheaper** than On-Demand  
- Can be **terminated anytime**  
- **2-minute warning before interruption**  
- Persistent requests can **auto-relaunch instances**  
- Always **cancel request before terminating instances**  
- Spot Fleet = multiple instance types + AZs for optimization  
- Best strategy: **price-capacity optimized**

---