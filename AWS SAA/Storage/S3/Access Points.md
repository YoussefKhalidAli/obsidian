S3 Access Points simplify access management for **large buckets with many users and prefixes**.

---

## 1. Problem with Traditional Bucket Policies

- Large S3 bucket with multiple types of data (e.g., finance, sales)
- Many users or groups need access to different prefixes
- Single bucket policy becomes **complex and hard to manage**

---

## 2. Solution: S3 Access Points

- **Access Points** provide **simplified, scalable access**
- Each access point has:
    - Its own **policy** (like a bucket policy)
    - Its own **DNS name**
    - Optional **VPC-only origin**

### Example Setup

| Access Point           | Prefix Access       | Policy Type |
| ---------------------- | ------------------- | ----------- |
| Finance Access Point   | finance/*           | Read/Write  |
| Sales Access Point     | sales/*             | Read/Write  |
| Analytics Access Point | finance/* + sales/* | Read-only   |

- Users access **only the data allowed** by the access point policy
- The main bucket policy can remain **simple**

---

## 3. Connection Options

- **Public Internet Access**: Access point has a DNS name to connect globally
- **VPC Access Point (Private)**: Restrict access to a **VPC**
    - Requires **VPC Endpoint**
    - VPC Endpoint has a **policy** granting access to:
        - S3 bucket
        - Access points
    - Ensures **private traffic** without going through the internet

---

## 4. Security Layers

1. **Bucket Policy** – overarching rules for the bucket
2. **Access Point Policy** – defines permissions per access point
3. **VPC Endpoint Policy** – controls private access through VPC

---
## 5. Object Lambda Access Points

### Purpose
- Modify objects **on-the-fly** as they are retrieved
- Avoid duplicating buckets or objects

### How it works
1. Create a **Lambda function** to transform the object
    - Example: redact PII, convert XML → JSON, enrich with additional data, resize or watermark images
2. Create an **S3 Object Lambda access point** on top of the S3 bucket
3. Applications access objects via the **Object Lambda access point**
    - Lambda retrieves original object
    - Applies transformation
    - Returns transformed object to the requester

### Example Use Cases

| Application    | Transformation                          |
| -------------- | --------------------------------------- |
| Analytics      | Redact PII from data                    |
| Marketing      | Enrich data with customer loyalty info  |
| Non-production | Convert XML → JSON for testing          |
| Image services | Resize and watermark images dynamically |

---

## 6. Key Benefits

- **Scales security management** for large buckets
- Users can access **specific prefixes** without complex bucket policies
- Can separate access by **group, application, or department**
- Supports **public or private (VPC) access**