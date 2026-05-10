# AWS Access Keys, CLI, and SDK

AWS provides multiple ways to access and manage resources programmatically, outside the Management Console. This includes **access keys, the CLI, and SDKs**.

---

## 1. Access Keys

- Access keys are **long-term credentials** used for programmatic access to AWS services.  
- Each IAM user can have **up to two active access keys**.  
- Composed of:
  - **Access Key ID** – public identifier  
  - **Secret Access Key** – private key used to sign requests  

**Explanation:** Access keys allow API requests to AWS without using the web console. They should be kept secret, rotated regularly, and never embedded in code or shared.

**Security Best Practices:**
- Rotate access keys periodically.  
- Delete unused keys.  
- Do **not** embed keys in code; use environment variables or AWS Secrets Manager.  
- Combine with **IAM policies** and **MFA** for extra security when needed.

---

## 2. AWS CLI (Command Line Interface)

- The AWS CLI is a **command-line tool** to manage AWS services programmatically.  
- You can use it to:
  - Launch EC2 instances  
  - Manage S3 buckets and objects  
  - Deploy CloudFormation templates  
  - Perform almost all actions available in the Management Console  

**Explanation:** CLI uses credentials (access keys or session tokens) to authenticate API requests. It is ideal for automation, scripting, and managing AWS resources efficiently.

**Key Notes:**
- Configure CLI using `aws configure` command.  
- Profiles can store multiple sets of credentials for different accounts.  
- Works across Windows, Linux, and macOS.

---

## 3. AWS SDK (Software Development Kit)

- AWS SDKs provide **language-specific libraries** to interact with AWS services.  
- Supported languages: Python (boto3), JavaScript (aws-sdk), Java, C#, Go, and more.  
- SDK handles:
  - Authentication with access keys or temporary credentials  
  - Request signing and retries  
  - Parsing API responses  

**Explanation:** SDKs simplify programming against AWS APIs and help developers integrate AWS into applications without handling raw HTTP requests. They are essential for building apps that interact with AWS services.

**Key Notes:**
- Always use **temporary credentials** via IAM roles where possible.  
- Avoid hardcoding access keys in applications.  
- Can be combined with **CLI** for scripting and automation.

---

## 4. Key Points

- **Access keys** allow programmatic access to AWS; they are sensitive and must be secured.  
- **CLI** is ideal for automation and administrative tasks.  
- **SDKs** allow developers to build applications interacting with AWS programmatically.  
- Combine access keys, CLI, SDKs, and IAM policies to **control access and enforce security**.