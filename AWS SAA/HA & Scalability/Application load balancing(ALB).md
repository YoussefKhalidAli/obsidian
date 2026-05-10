## 1. What is ALB?

- **Application Load Balancer (ALB)** operates at:
  - **Layer 7 (Application Layer)**  
- Handles:
  - **HTTP / HTTPS traffic only**  
- Used to route traffic to **multiple backend applications**  

---

## 2. Key Features

- **Content-based routing**
- **Supports HTTP/2 & WebSockets**
- **SSL termination (HTTPS)**
- **Redirect support (HTTP → HTTPS)**
- **Advanced routing rules**

---

## 3. Target Groups (CORE CONCEPT)

- ALB routes traffic to **Target Groups**  
- A **Target Group = group of backend resources**

### Supported Targets:
- EC2 instances  
- Auto Scaling Groups (ASG)  
- ECS tasks (containers)  
- Lambda functions  
- Private IP addresses  

---

## 4. Routing Capabilities (VERY IMPORTANT)

### 4.1 Path-Based Routing
- Route based on URL path  

Examples:
- `/users` → Target Group A  
- `/posts` → Target Group B  

---

### 4.2 Host-Based Routing
- Route based on domain name  

Examples:
- `api.example.com` → Target Group A  
- `app.example.com` → Target Group B  

---

### 4.3 Query String / Header Routing
- Route based on:
  - Query parameters  
  - Headers  

Example:
- `?platform=mobile` → Target Group A  
- `?platform=desktop` → Target Group B  

---

## 5. Use Cases

- Microservices architecture  
- Container-based apps (ECS, Docker)  
- Applications with multiple services behind one endpoint  

> **Note:** ALB is ideal when you need **advanced routing logic**

---

## 6. Advantages over Classic Load Balancer

- One ALB can handle **multiple applications**  
- No need for multiple load balancers  
- Supports **modern features** (routing, WebSockets, HTTP/2)  

---

## 7. Health Checks

- Configured **per Target Group**  
- Determines which targets receive traffic  

- If unhealthy → **no traffic sent**  

---

## 8. Client IP Handling (IMPORTANT)

- EC2 instances **do NOT see real client IP directly**  

- ALB adds headers:

  - `X-Forwarded-For` → Client IP  
  - `X-Forwarded-Port` → Client port  
  - `X-Forwarded-Proto` → HTTP or HTTPS  

> Backend apps must read these headers to get client info  

---

## 9. Networking Behavior

- Client connects → ALB  
- ALB forwards request → EC2 using its **own private IP**  
- This is called **connection termination**  

---

## 10. Key Concepts Summary

- ALB = **Layer 7 smart routing load balancer**  
- Routes traffic based on:
  - Path  
  - Host  
  - Query  
  - Headers  
- Uses **Target Groups**  
- Supports modern architectures (microservices, containers)  
- **ALB = HTTP/HTTPS only**  
- **Supports advanced routing (path, host, query)**  
- **Uses Target Groups**  
- **Health checks per Target Group**  
- **Client IP found in X-Forwarded-For**  
- Choose ALB when:
  - You need **routing rules**
  - You have **multiple apps behind one LB**
  - You use **containers / microservices**

---