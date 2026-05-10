Amazon S3 supports multiple encryption methods to secure data **at rest** and **in transit**.

---

## 1. Server-Side Encryption (SSE)
Encryption is handled by AWS **after the object is uploaded**.

### 1.1 SSE-S3 (Default)
- Uses **S3-managed keys**
- Encryption type: **AES-256**
- Enabled by default for new buckets and objects

**Header:**
`x-amz-server-side-encryption: AES256`

**Characteristics:**
- AWS manages keys
- No user control over keys
- Simplest option

### 1.2 SSE-KMS
- Uses **AWS Key Management Service (KMS)**
- Customer controls encryption keys

**Header:**
`x-amz-server-side-encryption: aws:kms`

**Characteristics:**
- Full control over keys
- Key usage is logged in CloudTrail
- Requires permissions to use the KMS key

**Important:**
- Subject to **KMS API limits (TPS)**
- High request rates can lead to throttling

### 1.3 SSE-C (Customer-Provided Keys)
- Customer provides encryption key in request

**Characteristics:**
- AWS does not store the key
- Key must be provided with every request
- Requires HTTPS

**Important:**
- If the key is lost, the data is unrecoverable

## 2. Client-Side Encryption

- Data is encrypted **before uploading to S3**
- Decryption happens on the client side

**Characteristics:**
- Full control over encryption process
- AWS never sees unencrypted data
- Requires client-side implementation

---

## 3. Encryption Comparison

| Feature        | SSE-S3 | SSE-KMS          | SSE-C    | Client-Side |
| -------------- | ------ | ---------------- | -------- | ----------- |
| Key Management | AWS    | AWS KMS          | Customer | Customer    |
| Key Control    | No     | Yes              | Yes      | Yes         |
| Ease of Use    | Easy   | Medium           | Hard     | Hard        |
| Audit          | No     | Yes (CloudTrail) | No       | Depends     |

---

## 4. Encryption in Transit (SSL/TLS)

- Protects data while being transferred
- Two endpoints:
    - HTTP → Not secure
    - HTTPS → Secure
- **Best Practice:**
	- Always use HTTPS

---

## 5. Enforcing HTTPS with Bucket Policy

To block unencrypted (HTTP) access:
```
{  
  "Effect": "Deny",  
  "Action": "s3:GetObject",  
  "Resource": "arn:aws:s3:::example-bucket/*",  
  "Condition": {  
    "Bool": {  
      "aws:SecureTransport": "false"  
    }  
  }  
}
```

**Result:**
- Denies all HTTP requests
- Allows only HTTPS access

> **Note:** Bucket policies are evaluated before "Default Encryption"
## 6. Key Takeaways

- SSE-S3 is the default and simplest option
- SSE-KMS provides control and auditing
- SSE-C requires managing your own keys
- Client-side encryption gives full control
- HTTPS should always be enforced
- Bucket policies can enforce secure access