  
SSM Parameter Store is a **secure storage service for configuration data and secrets**.  
  
**Explanation:**    
It allows you to store values such as:  
- Database credentials    
- API keys    
- Configuration settings    
  
You can store them as **plain text** or **encrypted using KMS**.  
  
---  
  
## 1. Key Features  
  
- Serverless (no infrastructure to manage)    
- Scalable and highly available    
- Supports **versioning**    
- Easy access via:  
  - AWS CLI    
  - SDK    
  - API    
  
---  
  
## 2. Security  
  
- Access controlled using **IAM policies**    
- Supports encryption using **KMS**    
  
**Explanation:**    
- Plain parameters → stored as text    
- SecureString parameters → encrypted using KMS    
- Applications must have permission to:  
  - Read parameter    
  - Use the KMS key (if encrypted)    
  
---  
  
## 3. Parameter Types  
  
- **String** → plain text    
- **StringList** → comma-separated values    
- **SecureString** → encrypted using KMS    
  
---  
  
## 4. Hierarchical Structure  
  
Parameters can be organized using a **path-based hierarchy**.  
  
### Example:

/my-app/dev/db-url  
/my-app/dev/db-password  
/my-app/prod/db-url  
/my-app/prod/db-password

  
**Explanation:**    
- Makes parameters easier to organize    
- Simplifies IAM policies (grant access by path)    
  
---  
  
## 5. Access Control Example  
  
- Dev application → access `/my-app/dev/*`    
- Prod application → access `/my-app/prod/*`    
  
**Explanation:** IAM policies can restrict access to specific paths.  
  
---  
  
## 6. Integration with AWS Services  
  
- Works with:  
  - EC2 (via instance roles)    
  - Lambda    
  - CloudFormation    
  - Systems Manager    
  
**Explanation:**    
CloudFormation can reference parameters as inputs to stacks.  
  
---  
  
## 7. Versioning  
  
- Every update creates a **new version**    
  
**Explanation:**    
- You can retrieve previous versions    
- Useful for rollback    
  
---  
  
## 8. Event Notifications  
  
- Integrated with **EventBridge**    
  
**Use Cases:**  
- Notify when parameters change    
- Track expiration events    
  
---  
  
## 9. Parameter Tiers  
  
### 9.1 Standard Tier  
  
- Free    
- Max size: **4 KB**    
- No parameter policies    
  
---  
  
### 9.2 Advanced Tier  
  
- Paid (~$0.05 per parameter/month)    
- Max size: **8 KB**    
- Supports **parameter policies**    
  
---  
  
## 10. Parameter Policies (Advanced Only)  
  
### Types:  
  
- **Expiration (TTL)**    
  - Automatically delete parameter at a specific time    
  
- **Expiration Notification**    
  - Notify before parameter expires    
  
- **No Change Notification**    
  - Notify if parameter hasn't been updated for a period    
  
**Explanation:** Helps enforce security practices like **rotating secrets**.  
  
---  
  
## 11. Public Parameters  
  
- AWS provides public parameters    
  
**Example Use Case:**  
- Get latest AMI ID for a region    
  
---  
  
## 12. Integration with Secrets Manager  
  
- Parameter Store can reference **Secrets Manager secrets**    
  
**Explanation:** Allows centralized access through Parameter Store.  
  
---  
  
## 13. Example Flow  
  
1. Application requests parameter    
2. IAM checks permissions    
3. If encrypted:  
   - KMS decrypts value    
4. Parameter returned to application    
  
---  
  
## 14. Key Points  
  
- Store config and secrets securely    
- Use KMS for encryption    
- Organize using hierarchical paths    
- Control access with IAM    
- Supports versioning and event notifications    
- Advanced tier enables automation with policies