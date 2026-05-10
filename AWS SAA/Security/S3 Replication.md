  
S3 Replication allows you to **automatically copy objects from one S3 bucket to another**, either in the same region or a different region.  
  
---  
  
## 1. Replication and Encryption Types  
  
### 1.1 Unencrypted Objects  
- Replicated **by default**  
  
---  
  
### 1.2 SSE-S3 (AWS Managed Encryption)  
- Replicated **by default**  
  
**Explanation:** Since AWS manages the encryption, replication works automatically.  
  
---  
  
### 1.3 SSE-C (Customer-Provided Keys)  
- Can be replicated  
  
**Explanation:** Requires proper configuration since encryption keys are provided by the customer.  
  
---  
  
### 1.4 SSE-KMS (KMS Encryption)  
  
- **Not replicated by default**  
- Must be **explicitly enabled**  
  
---  
  
## 2. Replicating SSE-KMS Encrypted Objects  
  
To replicate SSE-KMS objects:  
  
1. Enable **replication of KMS-encrypted objects**  
2. Specify a **target KMS key** in the destination bucket  
3. Update **KMS key policy** to allow usage  
4. Create an **IAM role** for S3 replication  
  
---  
  
### What Happens During Replication  
  
- Object is **decrypted** in the source bucket  
- Then **re-encrypted** in the destination bucket using the target KMS key  
  
**Explanation:** KMS keys are region-specific, so AWS must decrypt and re-encrypt the data during replication.  
  
---  
  
## 3. Permissions Required  
  
- IAM Role must allow:  
- Read from source bucket  
- Decrypt using source KMS key  
- Encrypt using destination KMS key  
  
- KMS Key Policy must allow:  
- S3 service to use the key  
  
---  
  
## 4. KMS Throttling  
  
- Replication with KMS involves many API calls  
- May result in **KMS throttling errors**  
  
**Solution:**  
- Request higher **service quotas** for KMS  
  
---  
  
## 5. Multi-Region Keys and S3 Replication  
  
- Multi-Region KMS keys **can be used**  
- BUT S3 treats them as **independent keys**  
  
**Important:**  
- Data is still:  
- Decrypted  
- Re-encrypted  
  
**Explanation:** Even though keys share the same material, S3 does not optimize replication using Multi-Region keys.  
  
---  
  
## 6. Key Points  
  
- Unencrypted and SSE-S3 → replicated automatically  
- SSE-KMS → must be explicitly enabled  
- Replication with KMS = **decrypt + re-encrypt**  
- Requires proper IAM role and key policies  
- Multi-Region keys **do not remove re-encryption step**