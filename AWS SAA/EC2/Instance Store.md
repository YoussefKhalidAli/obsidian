## 1. Definition
- **Instance Store** is **ephemeral storage** physically attached to the host server running your EC2 instance.  
- Provides **temporary block-level storage** for your instance.  
- Not network-attached like EBS → very low latency.  

---

## 2. Key Features
- **Ephemeral:** Data is lost if the instance is **stopped, terminated, or fails**.  
- **High IOPS and low latency:** Because storage is physically attached.  
- **Size:** Depends on the instance type (some instances have multiple instance store volumes).  
- **No snapshots:** Cannot create snapshots like EBS.  

---

## 3. Use Cases
- **Temporary storage:** Caching, buffers, scratch data, session storage.  
- **High-performance workloads:** Big data processing (Hadoop temporary data), log processing.  
- **Non-critical data:** Where persistence is not required.  

---

## 4. Limitations
- **Data persistence:** Lost if instance stops or terminates.  
- **Region/Availability Zone bound:** Only available in certain instance types and AZs.  
- **Cannot detach/move:** Unlike EBS, instance store cannot be detached and reattached.  
- **Backup:** Need to use external solutions (like S3 or EBS) to persist data.  

---

## 5. Comparison with EBS
| Feature            | EBS                          | Instance Store                    |
|-------------------|-----------------------------|----------------------------------|
| **Persistence**    | Persistent                  | Ephemeral (lost on stop/terminate) |
| **Attachment**     | Network-attached            | Local to host                    |
| **Snapshots**      | Yes                         | No                               |
| **Use Cases**      | Root volume, persistent data | Temp files, cache, scratch data  |
| **Availability**   | Any AZ                      | Only supported instance types/AZ |

---

## 6. Key Points
- Use **Instance Store** for **temporary high-speed storage**.  
- Always **backup critical data** elsewhere (EBS or S3).  
- Often paired with **EBS root volume** to combine persistence with high-speed scratch storage.