## 1. What is EBS Encryption?
- EBS encryption secures your data using **AWS KMS (Key Management Service)**.  
- Uses **AES-256 encryption standard**.  
- Encryption and decryption are handled **automatically (transparent to user)**.  

---

## 2. What Gets Encrypted?

When an EBS volume is encrypted:

- **Data at rest** (stored on disk) → encrypted  
- **Data in transit** (between EC2 and EBS) → encrypted  
- **Snapshots** → encrypted  
- **Volumes created from snapshots** → encrypted  

> Encryption applies **end-to-end automatically**.

---

## 3. Performance Impact
- **Negligible impact on performance/latency**  
- Recommended to **always enable encryption** unless there's a specific reason not to  

---

## 4. Encryption Behavior

### 4.1 New Volumes
- You can enable encryption when **creating a volume**  
- Can choose a **KMS key** (default or custom)

### 4.2 Snapshots
- Snapshot inherits encryption state:
  - From **encrypted volume → encrypted snapshot**
  - From **unencrypted volume → unencrypted snapshot**

---

## 5. Encrypting an Unencrypted Volume

EBS volumes **cannot be encrypted directly after creation**.  
You must follow this process:

### Step-by-Step:
1. Create a **snapshot** of the unencrypted volume  
2. **Copy the snapshot** and enable encryption (choose KMS key)  
3. Create a **new EBS volume** from the encrypted snapshot  
4. Attach the new encrypted volume to the EC2 instance  

---

## 6. Shortcut Method (Important)

- When creating a volume from a snapshot:
  - You can **enable encryption directly** during volume creation  
  - No need to manually copy snapshot first  

> This is the **fastest way** in real scenarios.

---

## 7. Key Concepts

| Concept | Explanation |
|--------|------------|
| KMS | Manages encryption keys |
| AES-256 | Encryption algorithm used |
| Transparent encryption | No manual encryption/decryption needed |
| Immutable encryption | Cannot encrypt existing volume directly |

---

## 8. Key Points

- Encryption is **handled automatically** by AWS  
- Must use **snapshot → copy → new volume** to encrypt existing volume  
- **All data paths are encrypted** (at rest + in transit)  
- Encryption uses **KMS keys**  
- **Always prefer encrypted volumes** in best practices  