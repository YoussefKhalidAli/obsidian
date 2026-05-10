## 1. What is it?

- Fully managed service to **transfer files into/out of AWS**
- Uses **traditional file transfer protocols**
- Works with:
    - **Amazon S3**
    - **Amazon EFS**

---

## 2. Why use it?

When:
- You **DON’T want to use S3 APIs**
- You **DON’T want NFS (EFS directly)**
- You want **legacy protocols (FTP, SFTP, FTPS)**

---

# 3. Supported Protocols

|Protocol|Encryption|Notes|
|---|---|---|
|FTP|❌ No|Legacy, insecure|
|FTPS|✅ Yes|FTP over SSL|
|SFTP|✅ Yes|Secure (SSH-based)|

**tip:**
- If security matters → **SFTP or FTPS**
- Avoid FTP unless explicitly mentioned

---

# 4. How it Works
1. Users connect via:
    - FTP / FTPS / SFTP endpoint
2. Transfer Family service:
    - Authenticates user
    - Uses IAM role
3. Data stored in:
    - S3 bucket OR EFS file system

---

## 5. Key Idea

It acts as a **protocol translator**:
- FTP/SFTP/FTPS → S3/EFS

---

# 6. Architecture Components
- Managed endpoint (FTP/SFTP/FTPS)
- IAM role (access S3/EFS)
- Backend storage (S3 or EFS)
- Optional DNS via Amazon Route 53

---

#  7. Authentication Options
- Service-managed users
- Or external systems:
    - Microsoft Active Directory
    - LDAP
    - Okta
    - Amazon Cognito
    - Custom providers

---

# 8. Pricing
- Per endpoint (hourly)
- Per GB transferred

---

# 9. Use Cases
- File sharing with partners
- Legacy system integration
- CRM / ERP data exchange
- Public dataset distribution

---

# 10. Transfer Family vs Storage Gateway

|Feature|Transfer Family|Storage Gateway|
|---|---|---|
|Purpose|File transfer|Hybrid storage|
|Protocols|FTP/SFTP/FTPS|NFS/SMB/iSCSI|
|Backend|S3 / EFS|S3 / Glacier|
|Use case|Upload/download files|Extend storage|

---
