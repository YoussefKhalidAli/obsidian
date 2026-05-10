  
## 1. What is IAM Identity Center?  
  
AWS IAM Identity Center (formerly **AWS Single Sign-On / AWS SSO**) is a centralized authentication service that provides:  
  
- 🔐 One login for multiple AWS accounts  
- 🔐 Access to business cloud applications (SaaS)  
- 🔐 Single sign-on (SSO) for AWS console access  
- 🔐 Optional access to EC2 Windows instances  
  
---  
  
## 2. Key Idea  
  
> One identity → multiple AWS accounts & applications  
  
Instead of managing many IAM users per account, users log in once and gain access everywhere based on permissions.  
  
---  
  
## 3. Supported Identity Sources  
  
IAM Identity Center supports two identity stores:  
  
### 1. Built-in Identity Store  
- Users and groups managed directly in AWS  
- Simple setup for small/medium environments  
  
### 2. External Identity Providers  
- Active Directory (AD)  
- Okta  
- OneLogin  
- Any SAML 2.0 provider  
  
---  
  
## 4. Login Flow  
  
1. User opens IAM Identity Center portal  
2. Enters username + password (or SSO login)  
3. Selects AWS account or application  
4. Gets redirected into:  
- AWS Console (specific account)  
- Business application (SAML-based)  
- EC2 Windows session (if configured)  
  
---  
  
## 5. AWS Organizations Integration  
  
IAM Identity Center works with AWS Organizations:  
  
- Centralized management from the **management account**  
- Works across:  
- Development OU  
- Production OU  
- Multiple AWS accounts  
  
---  
  
## 6. Permission Sets  
  
Permission Sets define **what a user can do in AWS accounts**.  
  
### Think of it as:  
> IAM policies + role templates for SSO users  
  
### Example Permission Sets:  
- AdminAccess (Dev accounts)  
- ReadOnlyAccess (Prod accounts)  
- DatabaseAdminAccess (RDS/Aurora access)  
  
---  
  
## 7. How Access Works
  
### Step-by-step:  
  
1. User logs into Identity Center  
2. User belongs to a **group** (e.g., Developers)  
3. Group is assigned a **Permission Set**  
4. Permission Set is assigned to an **AWS account (or OU)**  
5. AWS automatically creates an **IAM role**  
6. User assumes role when accessing account  
  
---  
  
## 8. Example Setup  
  
### Users:  
- Bob  
- Alice  
  
### Group:  
- Developers  
  
### Setup:  
- Developers → assigned Admin Permission Set → Dev OU  
- Developers → assigned ReadOnly Permission Set → Prod OU  
  
### Result:  
- In Dev → full access  
- In Prod → read-only access  
  
---  
  
## 9. Multi-Account Access  
  
IAM Identity Center allows:  
  
- Central access across multiple AWS accounts  
- Different permissions per account  
- No need for separate IAM users per account  
  
---  
  
## 10. Attribute-Based Access Control (ABAC)  
  
ABAC enables **dynamic permissions based on user attributes**.  
  
### Attributes examples:  
- Department (Dev, Finance)  
- Role (Junior, Senior)  
- Cost Center  
- Region  
  
### Benefit:  
- Define permission sets once  
- Control access using tags/attributes instead of multiple policies  
  
---  
  
## 11. Key Benefits  
  
- Single sign-on across AWS + SaaS apps  
- Centralized access control for organizations  
- Easier multi-account management  
- Reduced IAM user complexity  
- Supports modern identity providers  
  
---  
  
## 12. Key Points  
  
- IAM Identity Center = **SSO for AWS Organizations**  
- Uses **permission sets (not IAM users per account)**  
- Works with **SAML 2.0 providers**  
- Enables **multi-account access**  
- Replaces AWS SSO (old name)  
  
---  
  
## 13. Summary  
  
IAM Identity Center provides:  
  
- One login → multiple AWS accounts  
- Centralized identity management  
- Permission sets instead of IAM users per account  
- Integration with external identity providers  
- Attribute-based access control for advanced security