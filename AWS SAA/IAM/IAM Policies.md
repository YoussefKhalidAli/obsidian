IAM policies are JSON documents that define **permissions** for users, groups, or roles. They control **who can do what on which resources**.

---

## 1. Inheritance

- Users inherit permissions from **all groups** they belong to.  
- Policies can be attached to:
  - Users
  - Groups
  - Roles  
- **Explicit Deny always overrides any Allow**, even if inherited.

**Example**:  
- User `Alice` is in groups `Developers` and `Admins`  
- Alice will have **all permissions allowed** by both groups unless there’s an explicit Deny

**Explanation:** A user's effective permissions are the combination of all permissions from their groups and directly attached policies. If any policy explicitly denies an action, the user cannot perform it even if another policy allows it. This makes understanding inheritance critical when managing permissions.

---

## 2. Policy Structure

IAM policies are structured as JSON documents with a top-level **Version**, **Id**, and **Statement** array.  

- **Version** – Specifies the policy language version. The current standard is `"2012-10-17"`. It defines the syntax rules for the policy.  
- **Id** – Optional identifier to track or reference the policy.  
- **Statement** – An array of permission rules. Each statement defines a specific set of permissions.

---

### Statement Fields

Each statement inside the policy contains:

- **Sid (Statement ID)** – Optional identifier for the statement. Useful to track or reference individual statements.  
- **Effect** – Either `"Allow"` or `"Deny"`. `"Allow"` grants permission, `"Deny"` explicitly denies permission. **Explicit Deny overrides any Allow**, even if another policy grants it.  
- **Principal** – Specifies **who the policy applies to**. Required for resource-based policies, optional for identity-based policies (attached to users, groups, or roles).  
- **Action** – Defines which actions are allowed or denied, e.g., `"s3:GetObject"` or `"ec2:StartInstances"`. `"*"` means all actions. Actions not listed are implicitly denied.  
- **Resource** – Specifies which resources the actions apply to, e.g., `"arn:aws:s3:::example-bucket/*"`. Actions are limited to these resources; anything not listed is implicitly denied.

---
## 3. Example

```json
{
  "Version": "2012-10-17",
  "Id": "PolicyID123",
  "Statement": [
    {
      "Sid": "Stmt1",
      "Effect": "Allow",
      "Principal": {"AWS": "arn:aws:iam::123456789012:user/Alice"},
      "Action": ["s3:GetObject"],
      "Resource": ["arn:aws:s3:::example-bucket/*"]
    }
  ]
}
```

---

## 4. Key Points

- Policies are **additive** across users, groups, and roles.  
- The default behavior is **deny**, so permissions must be explicitly allowed.  
- **Explicit Deny overrides Allow**.  
- Always follow the **least privilege principle**: grant only the permissions that are necessary.  
- Understanding policy structure and inheritance is essential for effective permissions management and for scenarios.

---