## Overview

Amazon S3 provides **multiple layers of security** to control access:

1. **User-Based (IAM Policies)**
2. **Resource-Based (Bucket Policies)**
3. **ACLs (Access Control Lists)**
4. **Encryption**
5. **Block Public Access (Safety Layer)**

---

## 1. User-Based Security (IAM Policies)

- Applied to:
  - IAM Users
  - IAM Roles
  - IAM Groups
- Defines:
  - What actions are allowed/denied
  - On which resources

### Example Actions:
- `s3:GetObject`
- `s3:PutObject`
- `s3:ListBucket`

Used when:
- Controlling access **within your AWS account**

---

## 2. Resource-Based Security (Bucket Policies)

### What is a Bucket Policy?
- A **JSON policy attached to an S3 bucket**
- Controls access at the **bucket level**

### Example Policy (Public Read Access)

```json
{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::example-bucket/*"
}
```

### Breakdown

|Field|Meaning|
|---|---|
|Effect|Allow or Deny|
|Principal|Who (user/account)|
|Action|What operation|
|Resource|Which bucket/objects|

### Common Use Cases
- Make bucket public
- Restrict access
- Cross-account access
- Enforce encryption

---

## 3. Access Control Lists (ACLs)

### Types:

|Type|Description|
|---|---|
|Object ACL|Applied to individual objects|
|Bucket ACL|Applied to bucket|

### Important Notes

- Legacy feature
- Less flexible than bucket policies
- Can be **disabled**

Modern best practice:

> Use **Bucket Policies instead of ACLs**

---

## 4. Encryption
- Protects data at rest
- Can be enforced via:
    - Bucket Policy
    - Default encryption settings

 Example use:
- Force all uploads to be encrypted

---

## 5. Access Decision Logic

An IAM principal (user/role) can access S3 if:

Allowed by IAM Policy/Role **OR** Bucket Policy  
**AND** no **explicit DENY** exists

### Rule Priority

Explicit DENY > Allow

---

## 6. Access Scenarios

### 6.1 Public Access (Website)

User (Internet) → Bucket Policy → S3 Bucket

- Bucket policy allows `Principal = *`
- Used for:
    - Static websites
    - Public assets

### 6.2 IAM User Access

IAM User → IAM Policy → S3 Bucket
- Controlled via IAM permissions

### 6.3 EC2 Instance Access

EC2 → IAM Role → S3 Bucket
- Uses IAM Role (NOT IAM user)

### 6.4 Cross-Account Access

Other Account IAM User → Bucket Policy → S3

- Bucket policy explicitly allows external account

## 6.5 Block Public Access (IMPORTANT)

- A **safety feature** to prevent accidental public exposure
- Denies all public access to S3 regardless of resource policy or IAM policy/role

### Behavior
- Overrides:
    - Bucket policies
    - ACLs

Even if bucket policy says "public":

> Access is blocked if this setting is ON


### Best Practice
- Keep **Block Public Access ON**
- Only disable when absolutely necessary

---

## 7. MFA Delete

MFA = Multi-Factor Authentication
- Requires users to generate a **time-based code** on a device
    - Mobile app (e.g., Google Authenticator)
    - Hardware MFA device
- The code must be provided when performing certain sensitive operations in S3

## 7.1 When is MFA Required?

MFA is required for **highly destructive actions**:
- **Permanently deleting an object version**
- **Suspending versioning on a bucket**

MFA is **not required** for:
- Enabling versioning
- Listing deleted versions

## 7.2 Prerequisites
- Versioning must be **enabled** on the bucket
- Only the **(root account)** can enable or disable MFA Delete

> **Note:** Only the root user can delete if **MFA Delete** is enabled


---

## 8. Pre-Signed URLs
Pre-signed URLs allow **temporary access** to private S3 objects without making them public.

### 8.1 What They Are

- A URL generated via:
    - **S3 Console** (up to 12 hours expiration)
    - **AWS CLI**
    - **SDKs** (up to 168 hours expiration)
- The URL **inherits the permissions** of the user who generated it
- Can be used for **GET** (download) or **PUT** (upload) operations


### 8.2 How It Works
1. The bucket owner or authorized user generates a **pre-signed URL** for an object
2. The URL includes:
    - Permissions of the generator
    - Expiration time
3. The URL is shared with a target user
4. Target user can access the object directly using the URL until it expires

### 8.3 Use Cases
- Temporary download access for **private files**
- Allow logged-in users to download premium content
- Dynamically provide access to an **ever-changing list of users**
- Temporary upload access for a specific object without exposing the bucket

### 8.4 Key Points
- Keeps the **S3 bucket private**
- Access is **time-limited**
- Works for **both downloads and uploads**
- Does **not require changing bucket policies**

---
## 9. S3 Glacier Vault Lock

- Purpose: **Lock a Glacier vault** to prevent deletion or modification
- Steps:
    1. Create a **Vault Lock Policy** for the vault
    2. **Lock the policy** to prevent future edits
- Once locked:
    - Policy **cannot be changed or deleted**
    - Objects stored in the vault **cannot be deleted**
    - Even **administrators or AWS** cannot override it
- Use Case: Legal compliance, regulatory retention

---

## 10. S3 Object Lock

- Works at the **individual object level**
- Requires **Versioning enabled** on the bucket
- Purpose: Block **object versions** from deletion or modification for a **retention period**

### 2.1 Retention Modes

|Mode|Description|Who Can Override|
|---|---|---|
|Compliance|Strict; object versions **cannot be overwritten or deleted**, including root user|No one|
|Governance|Restrictive; most users cannot delete or modify, **but admins with IAM permissions** can override|Admin users with permissions|

- **Retention period** must be set for both modes
- Retention can be **extended**, but Compliance mode cannot be shortened

### 2.2 Legal Hold

- Protects an object **indefinitely**, independent of retention period
- Requires **S3 `PutObjectLegalHold` IAM permission**
- Can be applied or removed by users with the correct permissions
- Use Case: Legal investigations or critical data protection

---

## 11. Key Points

- IAM policies = **user-based**
- Bucket policies = **resource-based**
- ACLs = **legacy (avoid)**
- Access requires:
    - Allow + no explicit deny
- Block Public Access:
    - Overrides everything
- Use IAM Roles for EC2 (not IAM users)
- Bucket policies enable:
    - Public access
    - Cross-account access

---

## 12. Summary Table

|Method|Scope|Use Case|
|---|---|---|
|IAM Policy|User/Role|Internal access|
|Bucket Policy|Bucket|Public / cross-account|
|ACL|Object/Bucket|Legacy|
|Encryption|Object|Data protection|
|Block Public Access|Bucket/Account|Prevent leaks|
