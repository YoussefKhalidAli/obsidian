## 1. CNAME Records

- **Purpose:** Map a hostname to **another hostname**.
- **Example:**  
  `app.mydomain.com → blabla.anything.com`
- **Limitations:**
  - Cannot be used for the **root domain (Zone Apex)**, e.g., `mydomain.com`.
  - Only works for **subdomains**, e.g., `something.mydomain.com`.
  - Standard DNS behavior.

---

## 2. Alias Records

- **Purpose:** AWS-specific extension to DNS.
- Map a hostname to **AWS resources**.
- **Example:**  
  `app.mydomain.com → blabla.amazonaws.com` (ALB, CloudFront, S3 Website, etc.)
- **Advantages:**
  - Can be used for **root domains** (`mydomain.com`) and subdomains.
  - **Free of charge** — no Route 53 query charges for alias records.
  - **Native health check support**.
  - Automatically handles **IP changes** of underlying AWS resources.
- **Limitations / Notes:**
  - Always type **A** (IPv4) or **AAAA** (IPv6).
  - **TTL is managed automatically** by Route 53; cannot be manually set.
  - Cannot point to EC2 public DNS names.
- **Supported Targets:**
  - Elastic Load Balancers (ALB, NLB)
  - CloudFront Distributions
  - API Gateway
  - Elastic Beanstalk Environments
  - S3 Websites (static hosting)
  - VPC Interface Endpoints
  - Global Accelerator
  - Route 53 records in the same hosted zone

---

## 3. Key Differences

| Feature                  | CNAME                     | Alias Record                  |
|---------------------------|---------------------------|-------------------------------|
| Root domain support       | ❌ No                     | ✅ Yes                        |
| Cost                      | ❌ Charged per query       | ✅ Free                        |
| AWS resource aware        | ❌ No                     | ✅ Yes                        |
| TTL                        | ✅ Customizable           | ❌ Automatic                   |
| Works with EC2 DNS        | ✅ Yes                    | ❌ No                          |
| Health checks             | ❌ No                     | ✅ Native support              |