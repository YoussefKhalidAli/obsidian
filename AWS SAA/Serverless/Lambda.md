AWS Lambda is a **serverless compute service** that lets you run code **without managing servers**.
**Explanation:** You upload code, and AWS runs it automatically when triggered. You only pay when it runs.

---

## 1. Key Characteristics

- **No servers to manage**
- **Runs on demand (event-driven)**
- **Auto scaling (handles concurrency automatically)**
- **Max execution time: 15 minutes**
- **Pay per request + execution time**

**Explanation:** Unlike EC2, Lambda doesn’t run continuously → cost-efficient and scalable.

---

## 2. Supported Languages

- Node.js
- Python
- Java
- C# (.NET)
- Ruby
- Custom runtimes (e.g., Go, Rust)

**Note:** Containers are supported, but for container-heavy workloads → prefer ECS/Fargate.

---

## 3. Common Integrations (VERY IMPORTANT)

Lambda integrates with many AWS services:

- **API Gateway** → build REST APIs
- **S3** → trigger on file upload
- **DynamoDB** → trigger on data changes
- **Kinesis** → real-time processing
- **SNS / SQS** → event processing
- **EventBridge (CloudWatch Events)** → scheduled jobs

**Explanation:** Lambda is the core of **event-driven architectures**.

---

## 4. Example Use Cases

### 4.1 Serverless Image Processing

- Upload image → S3 triggers Lambda
- Lambda creates thumbnail → stores in S3

### 4.2 Serverless CRON Jobs

- EventBridge rule → triggers Lambda on schedule

**Explanation:** Replace EC2-based background jobs with serverless execution.

---

## 5. Pricing Model

- **Requests:**
    - 1M free/month
    - Then ~$0.20 per 1M requests
- **Compute Time:**
    - Based on **GB-seconds**

**Explanation:** More memory = faster execution but higher cost.

---

## 6. Important Limits
### Execution Limits

- Memory: **128 MB → 10 GB**
- Timeout: **15 minutes max**
- Environment variables: **4 KB**
- Temp storage (`/tmp`): **up to 10 GB**

### Deployment Limits

- ZIP size: **50 MB (compressed)**
- Unzipped: **250 MB**

### Concurrency

- Default: **1000 concurrent executions**

---

## 7. Concurrency & Throttling

- Lambda scales automatically → many parallel executions
- You can set **Reserved Concurrency** (limit per function)

### If limit exceeded:

- **Synchronous calls** → error (429)
- **Asynchronous calls** → retries + DLQ

**Explanation:** Prevent one function from consuming all capacity.

---

## 8. Cold Starts

- First invocation may be slow (initialization delay)

### Solution:

- **Provisioned Concurrency**
    - Pre-warms Lambda instances
    - Reduces latency

---

## 9. Lambda SnapStart

- Speeds up startup (especially Java, Python, .NET)
- Works by **snapshotting initialized state**

**Explanation:** Eliminates cold start delay → faster execution.

---

## 10. Lambda in VPC

### Default:

- Runs **outside your VPC**
- Can access public services (e.g., S3, DynamoDB)

### If placed in VPC:

- Can access:
    - RDS
    - ElastiCache
    - Internal services

**Important:** Required for private resources.

---

## 11. Lambda + RDS (Best Practice)

Problem:

- Too many Lambda connections → DB overload

Solution:

- Use **RDS Proxy**

**Benefits:**

- Connection pooling
- Better scalability
- Faster failover

---

## 12. Edge Computing

### 12.1 Lambda@Edge

- Runs at CloudFront edge locations
- Supports complex logic (Node.js, Python)

### 12.2 CloudFront Functions

- Lightweight (JavaScript only)
- Ultra-fast (<1 ms)
- Used for:
    - Header manipulation
    - URL rewrites
    - Auth checks

---

## 13. Key Takeaways

- Lambda = **serverless, event-driven compute**
- Best for:
    - Short tasks
    - APIs
    - Automation
- Not suitable for:
    - Long-running jobs (>15 min)
    - Heavy compute workloads

---

## Key Points

- **Event-driven → Lambda**
- **Short execution → Lambda**
- **No server management → Lambda**
- **Heavy containers → ECS/Fargate (NOT Lambda)**
- **Private DB access → Lambda in VPC + RDS Proxy**