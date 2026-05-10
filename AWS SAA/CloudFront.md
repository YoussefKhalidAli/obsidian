### What is CloudFront?
**Amazon CloudFront** is a **Content Delivery Network (CDN)** that:
- Caches content at **edge locations worldwide**
- Improves **read performance**
- Reduces **latency**
- Enhances **user experience**

---

## 1. Key Benefits
- **Low Latency**
    - Content served from nearest edge location
- **High Performance**
    - Cached content reduces load on origin
- **Global Distribution**
    - 200+ edge locations worldwide
- **Security**
    - Built-in **DDoS protection**
    - Integrates with:
        - AWS Shield
        - Web Application Firewall (WAF)

---

## 2. How CloudFront Works

### Flow
1. User sends request → nearest **edge location**
2. Edge location checks cache:
    - **Cache Hit** → return content immediately
    - **Cache Miss** → fetch from origin
3. Response is:
    - Returned to user
    - Cached at edge for future requests

---

## 3. Origins in CloudFront
CloudFront supports multiple origin types:

### 3.1 S3 Bucket (Most Common)
- Used for:
    - Static content (images, videos, files)
- Can restrict access using:
    - **Origin Access Control (OAC)** (recommended)
    - Replaces older **OAI**

### 3.2 Custom Origin (HTTP Backend)
- Application Load Balancer (ALB)
- EC2 instances
- S3 Static Website (must enable website hosting)
- Any HTTP server

---

## 5. CloudFront + S3 Security

To restrict direct access to S3:
- Use **Origin Access Control (OAC)**
- Update **S3 bucket policy** to allow only CloudFront

---

## 6. Uploading via CloudFront

- CloudFront can also handle **uploads to S3**
- Called **ingress traffic**

---

## 7. CloudFront vs S3 Cross-Region Replication

| Feature     | CloudFront                  | S3 Cross-Region Replication     |
| ----------- | --------------------------- | ------------------------------- |
| Type        | CDN (caching)               | Data replication                |
| Scope       | Global (all edge locations) | Specific regions only           |
| Performance | Very low latency            | Low latency in selected regions |
| Data Type   | Best for static content     | Best for dynamic content        |
| Caching     | Yes                         | No                              |
| Updates     | Based on cache TTL          | Near real-time                  |
| Use Case    | Global content delivery     | Data redundancy & DR            |

---

## 8. Cloudfront to ec2

- Direct
	- EC2's must be public, because there is no **VPC** connectivity to Cloudfront
	- Must allow public IP's of all edge locations through the EC2's security group
- Indirect (ALB)
	- EC2's can be private, because there is **VPC*** connectivity to ALB
	- ALB must be public
	- Must allow public IP's of all edge locations through the ALB's security group

---

## 9. Geographic Access
Manage access to Cloudfront from specific countries

- Whitelist:
	- Allow certain countries only
- Blacklist
	- Block certain countries

---

## 10. Pricing

- Every Country has it's own pricing
![[CloudFront_pricing.png]]

- Price classes
	- Price class all
		- All regions
		- Best performance
		- Most expensive
	- Price class 200
		- Most regions
		- Excludes the most expensive ones
	- Price class 100
		- The least expensive regions

![[CloudFront_Price_Class.png]]


---

## 11. Cache Invalidation
Tell Cloudfront to invalidate the cache at the edge locations

### Usecase
- Invalidate the cache after updating important files, so the user sees up to date information

---

## 9. Key Concepts

- CloudFront = **global caching layer**
- Uses **edge locations** to serve content faster
- Works with:
    - S3
    - ALB
    - EC2
    - Any HTTP backend
- Improves:
    - Performance
    - Availability
    - Security

---

## 10. Summary

| Concept       | Description                       |
| ------------- | --------------------------------- |
| CloudFront    | AWS CDN service                   |
| Edge Location | Cache server near users           |
| Origin        | Source of content (S3, ALB, etc.) |
| Cache Hit     | Served from edge                  |
| Cache Miss    | Fetched from origin               |
| OAC           | Secures S3 origin access          |