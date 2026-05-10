## 1. Problem It Solves
- App deployed in **one region**
- Users are **global**
- Traffic goes over **public internet**  
    → many hops  
    → higher latency  
    → less reliability

Goal: **Reduce latency + improve reliability**

---

## 2. Key Idea

Get traffic into **AWS network ASAP**

Instead of:
User → Public Internet → App (many hops)
Use:
User → Nearest Edge Location → AWS Private Network → App

---

## 3. Unicast vs Anycast

### 3.1 Unicast (Normal)

- 1 IP → 1 server
- Request goes to **specific server**

### 3.2 Anycast (Important!)
- Same IP on multiple servers
- User routed to **nearest server**
Used by Global Accelerator

---

## 4. How Global Accelerator Works
- Provides **2 static Anycast IPs**
- User connects to these IPs
- Traffic goes to **nearest AWS Edge Location**
- Then travels via **AWS private network** to backend

---

## 5. Supported Targets
Works with:
- EC2
- Elastic IP
- ALB (Application Load Balancer)
- NLB (Network Load Balancer)
- Public or Private resources

---

## 6. Key Benefits

### 6.1 Performance
- Lower latency (AWS backbone)
- Fewer hops
- Intelligent routing

### 6.2 High Availability
- Health checks
- Automatic failover (< 1 min)

### 6.3 Global Setup
- Can route to **multiple regions**

### 6.4 Security
- Only **2 static IPs** to whitelist
- Built-in DDoS protection via Shield

## 6.5 No Caching
- Every request goes to backend
- Unlike CloudFront
