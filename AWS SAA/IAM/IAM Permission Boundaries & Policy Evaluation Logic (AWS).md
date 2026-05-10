## 1. What are IAM Permission Boundaries?  
  
IAM Permission Boundaries are an **advanced security feature** used to define the **maximum permissions** an IAM user or role can have.  
  
### Key Points  
- They apply to:  
- IAM Users  
- IAM Roles  
- They do NOT apply to IAM Groups  
- They act as a **security guardrail (maximum permission limit)**  
  
---  
  
## 2. How Permission Boundaries Work  
  
A permission boundary does NOT grant permissions.  
  
Instead:  
- Identity-based policy = what a user is allowed to do  
- Permission boundary = the *maximum allowed scope*  
  
### Final Permission Rule:  
> Effective permissions = Identity Policy ∩ Permission Boundary  
  
---  
  
## 3. Example Scenario  
  
### Permission Boundary:  
Allows only:  
- S3  
- EC2  
- CloudWatch  
  
### IAM Policy attached to user:  
- `AdministratorAccess` (full access to everything)  
  
### Result:  
User still CANNOT perform admin actions outside the boundary  
User is restricted to:  
- S3  
- EC2  
- CloudWatch  
  
Because boundary overrides the IAM policy.  
  
---  
  
## 4. Use Cases  
  
IAM Permission Boundaries are used to:  
  
- Delegate IAM permissions safely (Dev teams, self-service)  
- Prevent privilege escalation (no self-admin access)  
- Restrict specific users without affecting entire accounts  
- Work alongside AWS Organizations SCPs  
  
---  
  
## 5. IAM Policy Evaluation Logic  
  
When AWS evaluates a request, it checks multiple layers:  
  
### Evaluation Order  
  
1. **Explicit Deny (Always wins)**  
- If any policy denies → request is denied immediately  
  
2. **AWS Organizations SCP**  
- Must allow action at organization level  
- Otherwise implicit deny  
  
3. **Resource-based Policies**  
- Example: S3 bucket policy  
  
4. **Identity-based Policies**  
- Attached to user/role/group  
  
5. **Permission Boundaries**  
- Restrict maximum allowed permissions  
  
6. **Session Policies**  
- Temporary session restrictions (advanced use)  

![[IAM_Ealuation_Logic.png]]
---  
  
## 6. Core Rule of AWS Authorization  
  
> A request is allowed ONLY if:  
- No explicit deny exists  
- AND all policy layers allow it  
  
Otherwise →  Denied  
  
---  
  
## 7. Explicit Deny vs Allow Example  
  
### Policy Example:  
- Deny: `sqs:*`  
- Allow: `sqs:DeleteQueue`  
  
### Results:  
  
#### Can you create queue?  
No  
- Covered by `sqs:*` deny  
  
#### Can you delete queue?  
No  
- Even though allowed, explicit deny overrides everything  
#### Can you describe EC2?  
No  
- No allow exists → implicit deny  
  
---  
  
## 8. Summary  
  
- Permission boundaries define **maximum possible permissions**  
- IAM policies define **granted permissions**  
- Final permission is the **intersection of both**  
- **Explicit deny always wins**  
- AWS evaluates multiple layers before allowing any action