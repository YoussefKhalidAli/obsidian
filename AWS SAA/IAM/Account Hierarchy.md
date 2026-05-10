AWS uses a hierarchy to organize and manage resources across multiple accounts using **AWS Organizations**.

---

## 1. Root (Management Account)

- The **main AWS account** that creates the organization  
- Also called the **management account**  
- Has full control over all accounts in the organization  

**Explanation:** This is the top-level account that manages billing, policies, and account structure.

---

## 2. AWS Organizations

- A service used to **centrally manage multiple AWS accounts**  
- Allows:
  - Consolidated billing  
  - Centralized policy management  
  - Account grouping  

**Explanation:** Instead of managing accounts separately, Organizations lets you control everything from one place.

---

## 3. Organizational Units (OUs)

- Logical groups of accounts within an organization  

**Examples:**
- Dev OU  
- Test OU  
- Prod OU  

**Explanation:** OUs help organize accounts and apply policies to multiple accounts at once.

---

## 4. Member Accounts

- Individual AWS accounts inside the organization  
- Used to isolate workloads, teams, or environments  

**Explanation:** Each account is independent (own resources, limits), but still governed by the organization.

---

## 5. Service Control Policies (SCPs)

- Policies applied at:
  - Organization level  
  - OU level  
  - Account level  

- Define **maximum permissions** allowed  

**Explanation:** SCPs do NOT grant permissions — they only **restrict what accounts can do**, even if IAM allows it.

---

## 6. Hierarchy Structure

Root (Management Account)  
│ 
├── Management Account  
│ └── Root User (Account Root)  
│  
├── Member Account A  
│ └── Root User (Account Root)  
│
├── OU (e.g., Production)  
│ ├── Account A  
│ ├── Account B  
│  
├── OU (e.g., Development)  
│ ├── Account C  
│ ├── Account D


---

## 7. Key Points

- Root (Management Account) controls the organization  
- Organizations = central management + billing  
- OUs = group accounts logically  
- Accounts = isolation boundary  
- SCPs = **restrict permissions (not grant)**  
- Policies flow **top-down** (Root → OU → Account)  