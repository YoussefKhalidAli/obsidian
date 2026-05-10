## 1. Definition
- An **AMI** is a **template** for creating EC2 instances.  
- It includes:
  - **OS** (e.g., Linux, Windows)  
  - **Application server or software stack**  
  - **EBS snapshots of root volumes**  
  - Optional **launch permissions** and **block device mappings**  

- Purpose: Quickly launch pre-configured EC2 instances.

---

## 2. Types of AMIs
1. **Amazon-provided AMIs**
   - Official, maintained by AWS.  
   - Examples: Amazon Linux, Ubuntu, Windows Server.

2. **Marketplace AMIs**
   - Provided by **third-party vendors**.  
   - May include paid software or additional services.

3. **Custom (User-created) AMIs**
   - Created from your **existing EC2 instance**.  
   - Can include custom configurations, applications, and settings.  
   - Useful for **scaling** or **disaster recovery**.

---

## 3. Features
- **Region-specific:** AMIs exist in a specific AWS region.  
  - Can be **copied** to another region.  
- **Launch permissions:** Control who can use your AMI (private or shared).  
- **EBS-backed or Instance Store-backed:**
  - **EBS-backed:** Root volume is EBS → can stop/start instances.  
  - **Instance Store-backed:** Root volume is ephemeral → lost on stop/termination.

---

## 4. Lifecycle
- **Create:** From an existing instance or snapshot.  
- **Launch:** Use AMI to create one or multiple EC2 instances.  
- **Update:** Cannot modify an AMI; must create a **new AMI** if changes are needed.  
- **Delete:** Deregister the AMI to prevent further use.  
  - Optional: delete associated snapshots to save storage costs.  

---

## 5. Key Points
- AMI is **region-bound** → copy to use in another region.  
- Can **pre-install software** and configure instances → saves setup time.  
- Custom AMIs are great for **scaling identical workloads**.  
- Understand **EBS vs Instance Store-backed AMIs** for instance stop/start behavior.  

---

## 6. Golden AMI

A **Golden AMI** is **not a different AWS resource** — it’s a **best practice / concept**.

| AMI                        | Golden AMI                                   |
| -------------------------- | -------------------------------------------- |
| Any image you create       | A **carefully prepared, standardized image** |
| Might be raw or incomplete | Fully configured and tested                  |
| Used ad hoc                | Used as a **base for all deployments**       |
| No guarantees              | Secure, patched, consistent                  |

## 7. Summary
| Feature        | Key Notes                                                  |
| -------------- | ---------------------------------------------------------- |
| **Definition** | Template for EC2 instances including OS, apps, and volumes |
| **Types**      | Amazon-provided, Marketplace, Custom                       |
| **Backed By**  | EBS or Instance Store                                      |
| **Region**     | Region-specific, can be copied across regions              |
| **Use Cases**  | Fast instance launch, scaling, disaster recovery           |