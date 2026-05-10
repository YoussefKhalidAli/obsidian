# AWS IAM: Users and Groups

## 1. Root Account
The **root account** is the **original account created when you sign up for AWS**.

### Characteristics:
- Has **full access to all AWS services and resources**
- Controlled by the **email + password** used during signup
- Not restricted by IAM policies

### Best Practices:
- **Do NOT use root account for daily tasks**
- Enable **MFA (Multi-Factor Authentication)**
- Use it only for:
  - Account setup
  - Billing changes
  - Critical account-level operations

---

## 2. IAM User
An **IAM User** represents an **individual person or application** that needs access to AWS.

### Characteristics:
- Has **long-term credentials**:
  - Username & password (for console)
  - Access keys (for CLI/API)
- Permissions are defined using **IAM policies**

### Key Points:
- Each user should represent **one entity**
- Permissions should follow **least privilege principle**

---

## 3. IAM Group
An **IAM Group** is a **collection of users**.

### Purpose:
- Simplifies permission management
- Assign permissions once to the group instead of each user

### Example:
- `Developers` group → access to dev resources  
- `Admins` group → full access  

---
## 4. IAM Roles

IAM Roles are **identities that you can create in AWS** with specific permissions, similar to users, but **not associated with a single person**. Roles allow **temporary access** to AWS resources.

---

### Purpose of Roles

Roles are used when you need to **grant permissions to entities that are not permanent users**:

- **AWS services** – e.g., EC2 instances assume a role to access S3 or DynamoDB.  
- **Users from other accounts** – allows cross-account access without sharing long-term credentials.  
- **Federated users** – external identities (like corporate Active Directory users or Google Workspace) can assume roles.  
- **Temporary access** – instead of creating permanent IAM users, you can grant short-term access to resources.

**Explanation:** Roles decouple **permissions from a specific user**, which is safer and more flexible. Entities assume the role when they need access, and stop having it when they are done.


### How Roles Work

- A role has **policies attached** that define permissions.  
- Entities **assume** the role temporarily using AWS Security Token Service (STS).  
- When assuming a role, AWS issues **temporary security credentials** (Access Key ID, Secret Access Key, and Session Token).  
- These credentials automatically **expire after a defined time**.  

**Explanation:** This mechanism ensures that no permanent credentials are exposed and that access is limited in time and scope.

---

### Key Features of Roles

- **No permanent credentials** – unlike IAM users, roles don’t have passwords or long-term keys.  
- **Temporary access** – helps enforce least privilege and reduces security risks.  
- **Cross-account access** – a role can be assumed by users, services, or accounts outside your AWS account.  
- **Service roles** – AWS services (like Lambda, EC2, ECS) use roles to access other AWS resources securely.  
- **Federation support** – external identities can temporarily assume roles without creating AWS users.  

**Explanation:** Roles are ideal for granting **controlled, temporary, and auditable access**, making them central to secure AWS architecture.

### Key Points

- Roles **grant temporary access** with permissions defined in attached policies.  
- Roles are **used by services, federated users, and cross-account scenarios**.  
- Using roles enhances security by avoiding permanent credentials.  
- Understanding roles is essential for IAM management and for designing **secure, least-privilege access** in AWS.

---

## 5. Differences Between Users and Roles

| Feature | IAM User | IAM Role |
|---------|----------|----------|
| Associated with a person | Yes | No |
| Long-term credentials | Yes | No |
| Temporary credentials | No | Yes (via STS) |
| Can be assumed by AWS services | No | Yes |
| Can be assumed by external/federated users | No | Yes |

**Explanation:** Users are permanent identities for people. Roles are **temporary, flexible identities** that can be assumed by people, services, or external accounts.

---

## 6. Relationships and Rules

### User Membership Rules:
- A user **can belong to one or more groups**
- A user **can exist without being in any group**
- Users inherit permissions from **all groups they belong to**

### Group Rules:
- Groups **cannot contain other groups**
- Groups only contain **users**

### Multiple Groups Behavior  
  
When a user is in multiple groups:  
- All permissions are **combined (union of policies)**  
- AWS evaluates all attached policies together     

#### Conflict Rules 
##### Case 1: Allow vs Allow  
- Permissions are combined  
- User gets **all allowed actions**  
  
##### Case 2: Allow vs No Permission  
- User gets the **allowed action**  
- No conflict here  
  
##### Case 3: Allow vs Explicit Deny  
- **Explicit Deny wins**  
- User is **DENIED access**

---
## 7. Features
### Service is global
### multi-session support: Allows use of multiple users in the same browser using different windows
---

## Summary

- Root account = full access, avoid daily use  
- User = individual identity  
- Group = collection of users  

### Rules:
- User → can be in multiple groups  
- User → can be in no group  
- Group → cannot be inside another group  