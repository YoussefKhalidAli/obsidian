AWS provides several tools to help **audit, monitor, and improve the security** of your IAM users, roles, and overall account.

---

## 1. IAM Credentials Report

- A **global account-level report** that lists all IAM users and their credentials status.  
- Includes information such as:
  - Password last used  
  - Password last changed  
  - Access keys (active/inactive)  
  - Access key last used  
  - MFA status  

**Explanation:** This report helps you quickly identify **security risks**, such as unused users, old passwords, or users without MFA enabled.

---

## 2. IAM Access Advisor (Last Used)

- Shows **service permissions granted to a user or role** and **when those services were last accessed**.  

**Explanation:** Helps identify **unused permissions**, allowing you to apply the **least privilege principle** by removing unnecessary access.

---

## 3. IAM Access Analyzer

IAM Access Analyzer helps you **identify resources that can be accessed from outside your AWS account**, such as public or cross-account access.

- Continuously analyzes **resource-based policies** (not identity-based policies)
- Detects if a resource is accessible by:
  - Another AWS account  
  - The public
- Generates **findings (alerts)** when such access is detected

**Explanation:** Instead of manually checking policies, Access Analyzer automatically scans them and tells you if something is exposed.

### How It Works

1. You create an **Access Analyzer** in a region  
2. AWS scans supported resources and their policies  
3. If a resource allows external access → a **finding is generated**  

### Supported Resources

Access Analyzer works with resources that support **resource-based policies**, such as:

- S3 buckets  
- IAM roles (trust policies)  
- KMS keys  
- Lambda functions  

### Types of Findings

- **Public Access**
  - Resource is accessible by anyone (`*`)
- **Cross-Account Access**
  - Resource is accessible by another AWS account

**Explanation:** These findings help you quickly identify **unintended exposure**.

### Example Scenario

- An S3 bucket policy allows access to `"Principal": "*"`  
- Access Analyzer will flag this as **public access**  

- An IAM role trust policy allows another account to assume it  
- Access Analyzer will flag this as **cross-account access**

### Why It Matters

- Prevents **data leaks** (e.g., public S3 buckets)  
- Helps enforce **least privilege**  
- Improves **security auditing and compliance**  

**Explanation:** Many AWS security incidents happen بسبب misconfigured policies. Access Analyzer helps detect these issues early.

---

## 4. Key Points

- IAM Credentials Report → **audit user credentials and security status**  
- Access Advisor → **identify unused permissions**  
- Access Analyzer → **detect external/public access**  
- CloudTrail → **track and log all activity**  

These tools help enforce **security best practices**, including least privilege, auditing, and monitoring.