## What are IAM Conditions?  
  
IAM Conditions are **extra rules inside IAM policies** that control **when a permission is allowed or denied**.  
  
They are used in:  
- IAM user/group/role policies  
- Resource-based policies (S3, etc.)  
- Endpoint policies  
- Organization SCPs  
  
Think of them as:    
**“Allow/Deny only IF a condition is true”**  
  
---  
  
## Basic Structure  
  
A condition block looks like:  
  
```json  
"Condition": {  
  "ConditionOperator": {  
    "ConditionKey": "Value"  
  }  
}

```
---

## Common IAM Condition Keys

## 1. aws:SourceIp

### Purpose:

Restrict access based on **client IP address**
### Use case:

Allow AWS access only from a company network
### Example:

- Allow only from corporate IP ranges
- Deny all other traffic
### Key idea:
Controls **where the request is coming from**

---

## 2. aws:RequestedRegion

### Purpose:
Restrict AWS API calls by **region**

### Use case:
- Block usage of services in specific regions
- Enforce compliance / cost control
### Example:

Deny EC2, RDS, DynamoDB in:
- eu-central-1
- eu-west-1

### Key idea:
 Controls **which AWS region can be used**

---

## 3. ec2:ResourceTag / aws:PrincipalTag

### Purpose:
Control access using **tags**
### Two types:

#### ec2:ResourceTag
- Refers to **resource (EC2 instance) tags**
- Example:
    - `Project = DataAnalytics`

#### aws:PrincipalTag
- Refers to **IAM user/role tags**
- Example:
    - `Department = Data`

### Use case:
Only allow:

- users from a department
- accessing properly tagged resources

### Key idea:
Controls **who can access what based on tags**

---

## 4. aws:MultiFactorAuthPresent

### Purpose:

Require **MFA authentication**

### Use case:

- Allow EC2 stop/terminate only if MFA is enabled
### Example behavior:
- MFA = false → DENY sensitive actions
- MFA = true → ALLOW actions

### Key idea:
Controls **security level of the login session**

---

## 5. S3 Bucket Conditions (ARN-based permissions)

### Bucket-level permissions:

arn:aws:s3:::bucket-name
Example:
- `ListBucket` applies to the **bucket itself**

---

### Object-level permissions:

arn:aws:s3:::bucket-name/*
Example:
- `GetObject`
- `PutObject`
- `DeleteObject`
### Key idea:
Bucket ARN ≠ Object ARN

---

## 6. aws:PrincipalOrgID

### Purpose:

Restrict access to **AWS Organization members only**

### Use case:
- Allow only accounts inside your AWS Organization
- Block external AWS accounts

### Example:
S3 bucket allows access only if:
- request comes from same AWS Organization ID
### Key idea:

Controls **cross-account / organizational access**

---
## Summary Table

|Condition Key|Controls|Use Case|
|---|---|---|
|aws:SourceIp|Client IP|Restrict access to corporate network|
|aws:RequestedRegion|AWS Region|Block/allow regions|
|ec2:ResourceTag|Resource tags|Control access to tagged resources|
|aws:PrincipalTag|User tags|Role/department-based access|
|aws:MultiFactorAuthPresent|MFA status|Enforce MFA security|
|aws:PrincipalOrgID|AWS org membership|Restrict cross-account access|
|S3 ARN rules|Bucket vs objects|Control bucket/object permissions|

---

## Key Points
- Conditions ALWAYS add **extra security filtering**
- Most common patterns:
    - IP restriction → `aws:SourceIp`
    - MFA enforcement → `aws:MultiFactorAuthPresent`
    - Organization access → `aws:PrincipalOrgID`
- S3 trick:
    - Bucket = `bucket-name`
    - Objects = `bucket-name/*`