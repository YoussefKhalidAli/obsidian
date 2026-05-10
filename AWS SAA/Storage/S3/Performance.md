## 1. Baseline Performance

- Amazon S3 **automatically scales** to handle very high request rates.
- Typical latency:
    - **100–200 ms** to first byte.

### Request Limits (Per Prefix)

| Operation Type             | Requests per Second (per prefix) |
| -------------------------- | -------------------------------- |
| PUT / COPY / POST / DELETE | 3,500                            |
| GET / HEAD                 | 5,500                            |

## Prefix

- A **prefix** = everything between the bucket name and the object name.
### Example:
s3://my-bucket/folder1/subfolder1/file.txt
- Prefix = `folder1/subfolder1/`

### Key Insight:
- Each prefix gets **its own performance limits**.
- You can **scale performance horizontally** by using multiple prefixes.

## Scaling with Prefixes

### Example:

|Object Path|Prefix|
|---|---|
|/folder1/sub1/file|/folder1/sub1|
|/folder1/sub2/file|/folder1/sub2|
|/folder2/sub1/file|/folder2/sub1|
|/folder2/sub2/file|/folder2/sub2|

4 prefixes =  
**4 × 5,500 GET = 22,000 GET requests/sec**

---

## 2. Multi-Part Upload

### When to Use:

- Recommended: **> 100 MB**
- Required: **> 5 GB**
### How it Works:
1. Split file into parts
2. Upload parts **in parallel**
3. S3 **reassembles** the file

### Benefits:
- Faster uploads
- Better bandwidth usage
- Improved reliability

---
## 3. S3 Transfer Acceleration

Speed up uploads/downloads over long distances.

### How it Works:
1. Upload file to **nearest Edge Location**
2. Data travels via **AWS private network**
3. Delivered to S3 bucket

### Benefits:
- Faster global transfers
- Reduced latency
- Works with multi-part upload

---

## 4. Byte-Range Fetches (Parallel Downloads)

### Purpose:
Speed up **downloads** and improve resilience.
### How it Works:
- Request specific byte ranges:
    bytes=0-1000  
    bytes=1001-2000
- Download parts **in parallel**

### Benefits:
- Faster downloads
- Retry only failed parts
- Retrieve partial data (e.g., file headers)

---

## Key Takeaways

- S3 performance scales **per prefix**
- Use **multiple prefixes** for higher throughput
- Use **multi-part upload** for large files
- Use **transfer acceleration** for global users
- Use **byte-range fetches** for faster downloads