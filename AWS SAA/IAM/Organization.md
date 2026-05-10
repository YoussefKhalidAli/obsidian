## 1. What is AWS Organizations?  
  
AWS Organizations is a **global account management service** that lets you centrally manage multiple AWS accounts.  
  
### Key idea:  
> One master account controls multiple member accounts.  
  
---  
  
## 2. Account Types  
  
### Management Account  
- The main/root account of the organization  
- Creates and manages the organization  
- Handles consolidated billing  
- Has **full administrative control**  
  
### Member Accounts  
- Created or invited into the organization  
- Can only belong to **one organization**  
- Used for workloads, environments, teams, etc.  
  
---  
  
## 3. Consolidated Billing  
  
AWS Organizations provides:  
- Single billing for all accounts  
- One payment method (management account)  
- Aggregated usage → cost savings  
  
### Benefits:  
- Volume discounts (EC2, S3, etc.)  
- Shared pricing benefits across accounts  
- Savings Plans / Reserved Instances shared across accounts  
  
---  
  
## 4. Organizational Units (OUs)  
  
OUs are **logical groupings of accounts** inside an organization.  
  
### Root OU  
- Top-level container  
- Contains all accounts and sub-OUs  
  
### Example structure:

Root OU  
├── Management Account  
├── Prod OU  
│ ├── Account A  
│ ├── HR OU  
│ │ └── Account B  
│ └── Finance OU  
│ └── Account C

  
---  
  
## 5. Ways to Organize OUs  
  
You can structure OUs by:  
### Business units  
- Sales  
- Finance  
- Retail  
  
### Environment  
- Dev  
- Test  
- Prod  
  
### Projects  
- Project A  
- Project B  
  
You can mix and match freely.  
  
---  
  
## 6. Key Benefits of AWS Organizations  
  
### Security  
- Strong isolation between accounts (stronger than VPC isolation)  
- Reduced blast radius  
  
### Governance  
- Enforce standards (tags, policies)  
- Centralized control  
  
### Centralized logging  
- CloudTrail logs to a central S3 bucket  
- CloudWatch Logs aggregation  
  
### Cross-account access  
- Easy role-based administration across accounts  
  
---  
  
## 7. Service Control Policies (SCPs)  
  
SCPs are **organization-level permission boundaries**.  
  
> They do NOT grant permissions — they only restrict them.  
  
### Important rule:  
- IAM = grants permissions  
- SCP = limits maximum permissions  
  
---  
  
## 8. SCP Behavior  
  
### Explicit Deny wins always  
If SCP denies a service → it is blocked even if IAM allows it.  
  
---  
  
## 9. SCP Scope  
  
SCPs can be applied to:  
- Root OU  
- Specific OUs  
- Individual accounts  
  
### Exception:  
- SCPs do NOT restrict the Management Account  
  
---  
  
## 10. Example SCP Effects  
  
### Scenario structure:  
- Root OU → Full AWS access SCP  
- Prod OU → Deny Redshift  
- HR OU → Deny Lambda  
- Finance OU → inherits Prod restrictions  
  
---  
  
### Account behaviors:  
  
#### Account A (Prod OU)  
- Cannot use Redshift  
- Everything else allowed  
  
#### Account B (HR OU)  
- Redshift blocked (from Prod OU)  
- Lambda blocked (from HR OU)  
- Everything else allowed  
  
#### Account C (Finance OU)  
- Redshift blocked  
- Everything else allowed  
  
#### Management Account  
- Always full access (no SCP restriction)  
  
---  
  
## 11. SCP Strategies  
  
### Block List (Deny-based)  
- Allow everything first  
- Then explicitly deny services  
  
Example:  
- Allow all  
- Deny DynamoDB  
  
---  
  
### Allow List (Most secure)  
- Deny everything by default  
- Only allow specific services  
  
Example:  
- Allow EC2  
- Allow CloudWatch  
- Everything else denied  
  
---  
  
## 12. Key Takeaways
  
- AWS Organizations = multi-account management  
- OU = logical grouping of accounts  
- SCP = permission boundary (NOT grant)  
- Explicit deny always wins  
- Management account is always special (full access)  
- Best practice: use multi-account strategy for isolation