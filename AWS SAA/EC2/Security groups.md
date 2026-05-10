# EC2 Security Groups

A Security Group is a **virtual firewall** that controls **inbound and outbound traffic** for EC2 instances.

**Explanation:** It defines which traffic is allowed to reach your instance and which traffic can leave it. It acts as the first layer of defense for your EC2 resources.

---

## 1. How Security Groups Work

- Attached to **EC2 instances** (or ENIs)  
- Control:
  - **Inbound rules** (traffic coming into the instance)  
  - **Outbound rules** (traffic leaving the instance)  

**Explanation:** Every request is evaluated against the rules. If it matches an allowed rule → traffic is allowed. Otherwise → denied.

---

## 2. Rules

Each rule contains:

- **Type** – (e.g., HTTP, SSH)  
- **Protocol** – TCP, UDP, ICMP  
- **Port Range** – e.g., 22 (SSH), 80 (HTTP)  
- **Source/Destination** – IP range or another security group  

**Explanation:** Rules define exactly **what traffic is allowed, from where, and on which ports**.

---

## 3. Key Characteristics

- **Stateful**
  - If inbound traffic is allowed → response is automatically allowed  
  - No need to create separate outbound rule for responses  

- **Default behavior**
  - All inbound traffic is **blocked**  
  - All outbound traffic is **allowed** (by default)  

- **Allow rules only**
  - You cannot create explicit deny rules  
  - Anything not allowed is automatically denied  

- **Multiple security groups**
  - An instance can have multiple security groups  
  - Rules are combined (union of all rules)  

---

## 4. Referencing Security Groups

- You can allow traffic from **another security group** instead of IP addresses  

**Explanation:** This is useful for controlling communication between instances (e.g., web server → database server) without exposing them to the internet.

---

## 5. Common Use Cases

- Allow SSH (port 22) from your IP  
- Allow HTTP (port 80) and HTTPS (port 443) from anywhere  
- Restrict database access to only application servers  

---

## 6. Key Points

- Security Group = **stateful firewall for EC2**  
- Controls **inbound and outbound traffic**  
- Default: inbound denied, outbound allowed  
- Only **Allow rules**, no Deny  
- Rules are evaluated automatically; no order matters  