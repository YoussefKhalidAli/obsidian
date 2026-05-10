## 1. Overview of Route 53

- **Amazon Route 53** is:
  - Highly available
  - Scalable
  - Fully managed
  - **Authoritative DNS**: You control the DNS records.

- **Purpose:**
  - Maps human-readable domain names (e.g., `example.com`) to IP addresses (`54.22.33.44`).
  - Acts as a **domain registrar**: You can register domain names.
  - Health checks for resources.
  - AWS SLA: **100% availability**.

- **Name Origin:**  
  Port **53** is the standard port for DNS services → hence "Route 53".

---

## 2. DNS Records in Route 53

Each DNS record contains:
- **Domain/Subdomain**: e.g., `example.com` or `www.example.com`
- **Record type**: A, AAAA, CNAME, NS
- **Value**: e.g., IP address or target hostname
- **Routing policy**: How Route 53 responds to queries
- **TTL (Time to Live)**: Duration the record is cached at DNS resolvers

### Important Record Types

| Record Type | Purpose |
|------------|---------|
| **A**      | Maps a hostname to an **IPv4** address |
| **AAAA**   | Maps a hostname to an **IPv6** address |
| **CNAME**  | Maps a hostname to **another hostname** (cannot be used at zone apex) |
| **NS**     | Name servers of the hosted zone, control how traffic is routed |

> **Note:** You cannot create CNAME for the **zone apex** (`example.com`), but can for subdomains (`www.example.com`).

---

## 3. Hosted Zones

- **Definition:** Container of DNS records for a domain and its subdomains.
- **Types:**
  1. **Public Hosted Zone**
     - Accessible by **anyone on the internet**.
     - Example: `mypublicdomain.com`
  2. **Private Hosted Zone**
     - Only accessible from **within your VPC**.
     - Example: `application1.company.internal`
     - Useful for private resources like EC2 instances or internal databases.

- **Example Private Hosted Zone Flow:**
  1. `webapp.example.internal` → EC2 instance 1
  2. `api.example.internal` → EC2 instance 2
  3. `database.example.internal` → RDS database
  - Each internal resource resolves through the private hosted zone using **private IPs** (e.g., `10.0.0.10`).

---

## 4. Costs

- **Hosted zones:** $0.50 per month per zone
- **Domain registration:** Starts around $12 per year

---

## 5. Key Points

- Public hosted zone → queries from the internet
- Private hosted zone → queries **only** from resources inside your VPC
- Record types: **A, AAAA, CNAME, NS**
- Zone apex restrictions: CNAME cannot be used