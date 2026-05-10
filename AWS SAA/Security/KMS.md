  
AWS KMS is a service used to **create and manage encryption keys** in AWS.  
  
**Explanation:** Instead of managing encryption keys yourself, AWS KMS handles key storage, security, and usage. You use KMS to **encrypt and decrypt data** across AWS services.  
  
---  
  
## 1. Core Concepts  
  
- KMS manages **encryption keys for you**  
- Integrated with **IAM** for access control  
- Integrated with **CloudTrail** for auditing  
  
**Explanation:**  
- IAM controls **who can use the keys**  
- CloudTrail logs **every API call made using KMS keys**  
  
---  
  
## 2. Integration with AWS Services  
  
KMS is integrated with many AWS services:  
  
- EBS (volume encryption)  
- S3 (object encryption)  
- RDS (database encryption)  
- SSM, Lambda, and more  
  
**Explanation:** When you enable encryption in these services, they usually use **KMS keys behind the scenes**.  
  
---  
  
## 3. Using KMS Directly  
  
- You can call KMS using:  
- AWS CLI  
- SDK  
- API  
  
**Explanation:**  
You can encrypt sensitive data (like secrets) before storing it:  
- Store encrypted data in code or environment variables  
- Never store secrets in plain text  
  
---  
  
## 4. Types of KMS Keys  
  
### 4.1 Symmetric Keys (Most Common)  
  
- Single key used for **both encryption and decryption**  
- Used by AWS services  
- You **never see the actual key**  
  
**Explanation:** You only interact with the key through KMS APIs.  
  
---  
  
### 4.2 Asymmetric Keys  
  
- Two keys:  
- **Public key** → encrypt  
- **Private key** → decrypt  
- Public key can be downloaded  
- Private key **never leaves KMS**  
  
**Use Case:**  
- Encrypt data outside AWS, decrypt inside AWS  
- Digital signing and verification  
  
---  
  
## 5. Types of Keys by Ownership  
  
### 5.1 AWS Owned Keys  
  
- Fully managed by AWS  
- Not visible to you  
- Used automatically by some services  
  
---  
  
### 5.2 AWS Managed Keys  
  
- Created and managed by AWS (per service)  
- Format: `aws/service-name`  
- Example: `aws/s3`, `aws/ebs`  
  
**Explanation:** Easy to use, but less control.  
  
---  
  
### 5.3 Customer Managed Keys (CMK)  
  
- Created and managed by you  
- Full control over:  
- Permissions  
- Rotation  
- Policies  
  
**Explanation:** Used when you need **fine-grained control or compliance**.  
  
---  
  
## 6. Key Rotation  
  
- AWS Managed Keys → automatically rotated every 1 year  
- Customer Managed Keys → optional automatic rotation (1 year)  
- Imported keys → must be rotated manually  
  
---  
  
## 7. Pricing  
  
- ~$1/month per customer-managed key  
- Charged per API usage (~$0.03 per 10,000 requests)  
  
---  
  
## 8. KMS Key Policies  
  
KMS keys use **key policies** to control access.  
  
- Similar to resource-based policies (like S3 bucket policy)  
- Required to allow access to the key  
  
### Types:  
  
- **Default policy**  
- Allows IAM policies in the account to control access  
  
- **Custom policy**  
- Explicitly defines:  
- Who can use the key  
- Who can manage the key  
  
**Explanation:**  
Without a key policy → **no one can use the key**, even if IAM allows it.  
  
---  
  
## 9. Cross-Account Access  
  
- Possible using **custom key policies**  
- Used for:  
- Sharing encrypted snapshots  
- Cross-account data access  
  
**Explanation:** You must allow the external account in the key policy.  
  
---  
  
## 10. Regional Scope  
  
- KMS keys are **region-specific**  
- Cannot be directly used across regions  
  
**Explanation:**  
To move encrypted data between regions:  
1. Create snapshot (still encrypted)  
2. Copy snapshot to another region  
3. Re-encrypt with a new KMS key in target region  
  
---  
  
## 11. Key Points  
  
- KMS manages **encryption keys securely**  
- Integrated with IAM and CloudTrail  
- Default for encryption in many AWS services  
- Supports **symmetric and asymmetric keys**  
- Keys are **region-specific**  
- Key policies are required for access