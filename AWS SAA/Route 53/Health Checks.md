
## 1. Overview

- **Route 53 Health Checks** monitor the health of your applications/endpoints.
- Used to:
  - Detect failures
  - Enable **failover routing**
  - Improve **high availability**

---

## 2. Types of Health Checks

### 2.1 Endpoint Health Check

Monitors a **public endpoint** (IP or domain).

#### Configuration:
- **Target:**
  - IP address OR domain name
- **Protocol & Port:**
  - HTTP / HTTPS / TCP
  - Example: Port 80 (HTTP)
- **Path:**
  - `/` → root
  - `/health` → common for real apps

#### Advanced Settings:
- **Request Interval:**
  - Standard: 30 seconds (cheaper)
  - Fast: 10 seconds (more expensive)
- **Failure Threshold:**
  - Number of failed checks before marking unhealthy
- **String Matching (optional):**
  - Check response content (first 5120 bytes)
- **Latency Measurement:**
  - Enables latency graphs
- **Invert Health Check:**
  - Healthy ↔ Unhealthy (reverse logic)
- **Regions:**
  - Use AWS recommended health checker locations
- **CloudWatch Alarm:**
  - Optional alerts on failure

---

## 3. How It Works (Real Scenario)

- You create health checks for multiple EC2 instances:
  - US-East-1
  - AP-Southeast-1
  - EU-Central-1

- If one instance becomes unreachable:
  - Example: **Security Group blocks port 80**
  - Result:
    - Health check → ❌ Unhealthy
    - Error → Connection timeout

---

## 4. Health Check Failure Example

- Cause: Firewall (Security Group) blocks traffic
- Result:
  - Health check cannot connect
  - Status → **Unhealthy**
  - Error message → Timeout / connection failure

---

## 5. Calculated Health Checks

- Combine multiple health checks into **one logical check**

### Use Cases:
- Require:
  - **ALL healthy (AND)**
  - **AT LEAST ONE healthy (OR)**
  - **Custom threshold (e.g., 2 of 3 healthy)**

### Example:
- 3 endpoints
- Rule: Healthy only if **all 3 are healthy**
- If 1 fails → overall health = ❌ Unhealthy

---

## 6. CloudWatch-Based Health Checks

- Monitor a **CloudWatch Alarm** instead of an endpoint

### Use Case:
- Check health of:
  - Private EC2 instances
  - Internal services (not publicly accessible)

### Flow:
1. CloudWatch monitors metric (CPU, memory, etc.)
2. Alarm changes state (OK / ALARM)
3. Route 53 health check follows alarm state

---

## 7. Key Limitations

- Endpoint health checks require:
  - **Publicly accessible endpoints**
- Private resources:
  - Must use **CloudWatch-based health checks**

---

## 8. Key Points

- Health checks monitor **endpoint availability**
- Failures often caused by:
  - Security Groups
  - Network issues
- Types:
  - Endpoint
  - Calculated
  - CloudWatch-based
- Calculated checks = **combine multiple checks**
- Used with Route 53 routing policies (e.g., failover)