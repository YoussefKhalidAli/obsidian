S3 Access Logs provide a way to **audit and track all requests** made to your S3 buckets.

---

## 1. Purpose
- Record **all requests** to your S3 bucket:
    - Authorized or denied
    - Any account
- Logs are stored as **objects in another S3 bucket**
- Useful for **audit, compliance, and analysis**

---

## 2. How It Works
1. Enable **access logging** on your S3 bucket
2. All requests are logged into a **target bucket** in the **same AWS region**
3. Logs follow a **specific format** (can be referenced via AWS documentation)
4. Logged data can be analyzed using tools like **Amazon Athena**

---

## 3. Important Notes / Best Practices

- **Never use the same bucket** as both the logging bucket and the monitored bucket
    - This causes a **logging loop**, which will continuously generate logs for the logs themselves
    - Can lead to **exponential growth** and unnecessary cost
- Always use a **separate target bucket** for storing access logs

---

## 4. Use Cases

- Audit and monitor bucket access
- Track unauthorized access attempts
- Analyze usage patterns
- Integrate with analytics tools (e.g., Athena) for deeper insights