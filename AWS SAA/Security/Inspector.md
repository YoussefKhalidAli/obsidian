  
Amazon Inspector is a **continuous security vulnerability assessment service** for AWS workloads.  
  
It automatically scans your resources to detect **security issues, misconfigurations, and software vulnerabilities**.  
  
---  
  
## 1. What Amazon Inspector Evaluates  
  
Amazon Inspector focuses on **three main resource types**:  
  
### 1. EC2 Instances  
- Scans running EC2 instances using the **AWS Systems Manager (SSM) agent**  
- Checks for:  
- **Operating system vulnerabilities**  
- **Known software vulnerabilities (CVE database)**  
- **Unintended network exposure (reachability issues)**  
  
**Explanation:** It evaluates whether your EC2 instance is exposed to security risks and whether installed software contains known vulnerabilities.  
  
---  
  
### 2. Container Images (Amazon ECR)  
- Scans Docker/container images stored in **Amazon Elastic Container Registry (ECR)**  
- Checks images before or after deployment for:  
- Known vulnerabilities in OS packages  
- Vulnerable libraries inside the container  
  
**Explanation:** This helps ensure insecure container images are detected before they are deployed into production.  
  
---  
  
### 3. AWS Lambda Functions  
- Scans Lambda functions during or after deployment  
- Analyzes:  
- Function code  
- Dependencies (libraries/packages)  
- Known vulnerabilities in included components  
  
**Explanation:** Even serverless functions can contain vulnerable dependencies, and Inspector checks them automatically.  
  
---  
  
## 2. How Amazon Inspector Works  
  
- Continuously scans supported resources  
- Uses a **vulnerability database (CVE - Common Vulnerabilities and Exposures)**  
- Automatically re-scans when:  
- New vulnerabilities are discovered  
- The CVE database is updated  
- Assigns a **risk score** to each finding for prioritization  
  
**Explanation:** Instead of a one-time scan, Inspector keeps checking your environment as new threats are discovered.  
  
---  
  
## 3. Findings and Integration  
  
Amazon Inspector produces **findings** (security issues) and integrates with other AWS services:  
  
- **AWS Security Hub**  
- Centralized view of all security findings across AWS  
  
- **Amazon EventBridge**  
- Sends findings as events  
- Allows automation (e.g., trigger alerts or remediation workflows)  
  
**Explanation:** This allows you to centralize security monitoring and automate responses to vulnerabilities.  
  
---  
  
## 4. Key Concepts  
  
- **Continuous scanning** – not a one-time check  
- **CVE database** – source of known vulnerabilities  
- **Risk scoring** – prioritizes critical issues  
- **Automated updates** – rescans when new vulnerabilities are discovered  
  
---  
  
## 5. Key Points 
- Scans:  
- EC2 instances (via SSM agent)  
- ECR container images  
- Lambda functions  
- Detects **software vulnerabilities and network exposure**  
- Uses **CVE database**  
- Integrates with **Security Hub and EventBridge**  
- Provides **continuous assessment, not manual scanning**