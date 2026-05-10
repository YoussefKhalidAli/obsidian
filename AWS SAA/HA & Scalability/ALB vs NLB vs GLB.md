# Comparison of AWS Load Balancers: ALB vs NLB vs GWLB

---

## 1. Application Load Balancer (ALB)

- **Layer:** 7 (Application Layer)
- **Protocols:** HTTP, HTTPS, WebSocket
- **Primary Use Case:** Routing traffic for web applications, microservices, and container-based workloads.
- **Key Features:**
  - Supports **path-based routing** (e.g., /users, /posts)
  - Supports **host-based routing** (e.g., one.example.com, other.example.com)
  - Handles **query string and header-based routing**
  - SSL/TLS termination
  - Can route to:
    - EC2 instances
    - ECS tasks
    - Lambda functions
    - Private IPs
- **Best For:** Microservices, containerized apps, dynamic routing, HTTP/HTTPS traffic.

---

## 2. Network Load Balancer (NLB)

- **Layer:** 4 (Transport Layer)
- **Protocols:** TCP, UDP, TLS
- **Primary Use Case:** High-performance, ultra-low latency traffic; static IP requirements.
- **Key Features:**
  - Can handle **millions of requests per second**
  - **Ultra-low latency**
  - Provides **static IP per AZ** (can assign Elastic IPs)
  - Health checks supported for **TCP, HTTP, HTTPS**
  - Can route to:
    - EC2 instances
    - Private IP addresses
    - Application Load Balancers (for combined use)
- **Best For:** High-performance TCP/UDP applications, IP-based access, static IP needs.

---

## 3. Gateway Load Balancer (GWLB)

- **Layer:** 3 (Network Layer)
- **Protocols:** GENEVE (port 6081)
- **Primary Use Case:** Deploying, scaling, and managing network security appliances.
- **Key Features:**
  - Acts as **transparent gateway** for network traffic
  - Distributes traffic to **third-party appliances** (firewalls, IDS/IPS, DPI)
  - Traffic inspection and filtering before reaching apps
  - Can route to:
    - EC2 instances (appliances)
    - Private IP addresses
- **Best For:** Centralized network security, inspection, firewalling, intrusion detection.

---

## 4. Summary Table

| Feature       | ALB                          | NLB                           | GWLB                          |
| ------------- | ---------------------------- | ----------------------------- | ----------------------------- |
| Layer         | 7 (Application)              | 4 (Transport)                 | 3 (Network)                   |
| Protocols     | HTTP, HTTPS, WebSocket       | TCP, UDP, TLS                 | GENEVE (6081)                 |
| Use Case      | Web apps, microservices      | High performance TCP/UDP      | Network security appliances   |
| Health Checks | HTTP, HTTPS                  | TCP, HTTP, HTTPS              | N/A (appliance dependent)     |
| Routing       | Path, host, query, header    | IP/Port                       | Traffic through appliances    |
| Static IP     | No                           | Yes                           | No                            |
| Target Groups | EC2, ECS, Lambda, IPs        | EC2, IPs, ALB                 | EC2 appliances, IPs           |
