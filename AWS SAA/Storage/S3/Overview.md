**Amazon S3 (Simple Storage Service)** is a **scalable object storage service** in AWS.
- Designed for **infinite scalability**
- Highly durable and available
- Core building block of many AWS services

Used by:
- Websites
- Applications
- AWS services internally

---

## 1. Common Use Cases
Amazon S3 is used for:
- Backup & Storage (files, disks, etc.)
- Disaster Recovery (cross-region backups)
- Archival (using S3 Glacier)
- Static Website Hosting
- Media Hosting (images, videos)
- Data Lakes & Big Data Analytics
- Hybrid Cloud Storage
- Software Distribution (updates, downloads)

## Real-World Examples
- Nasdaq → stores 7 years of data in S3 Glacier
- Sysco → runs analytics on S3 data

---

## 2. Buckets
- A **container for objects (files)**
- Similar to a **top-level directory**

## 2.1 Directory Buckets (S3 Express One Zone)
- A **special type of S3 bucket** used exclusively with **S3 Express One Zone**
- Unlike standard S3 buckets:
    - Data is stored in a **single Availability Zone**
    - Optimized for **very high performance and low latency**

### 2.2 Key Properties
- Must have a **globally unique name**
- Defined at a **region level**
- Looks global, but **actually regional**

### 2.3 Naming Rules
- 3–63 characters
- Lowercase letters and numbers only
- No uppercase or underscores
- Must NOT look like an IP address
- Must start with:
    - lowercase letter OR number

## 2.4 account regional namespaces
With this feature, you can predictably name and create general purpose buckets in your own account regional namespace by appending your account’s unique suﬃx in your requested bucket name.

---

## 3. Objects
### What is an Object?
- A **file stored in S3**
- Includes:
    - Data (content)
    - Metadata
    - Key (path)

### 3.1 Object Key
The **key = full path of the object**

Example:  
`my-folder/another-folder/file.txt`

Breakdown:
- Prefix: `my-folder/another-folder/`
- Object Name: `file.txt`

### 3.2 Important Note
- S3 has **NO real folders**
- Folders are just part of the **key name**

Everything is just a **string (key)**
## 3.3 Object Size Limits

|Property|Value|
|---|---|
|Max object size|5 TB|
|Single upload limit|5 GB|
|Multipart upload required|> 5 GB|

### 3.4 Multipart Upload
- Required for large files (>5 GB)
- File is split into parts and uploaded in parallel

Example:
- 5 TB file → uploaded in multiple chunks

## 3.5 Object Components
### 3.5.1 Data (Value)
- Actual file content

### 3.5.2 Metadata
- Key-value pairs
- Can be:
    - System-defined
    - User-defined

Example:  
`Content-Type: image/png`

### 3.5.3 Tags
- Up to **10 key-value pairs**
- Used for:
    - Security
    - Lifecycle rules
    - Billing

### 3.5.4 Version ID (Optional)
- Available if **versioning is enabled** (Bucket level)
- Helps track multiple versions of the same object
- Allows reverting to older state based on version number (Old versions are set as _deleted_ not actually deleted)
- Any file not versioned prior to enabling versioning will have version _null_
- If versioning is suspended old versions are not deleted (It just stops counting)

---

## 4. Requester Pays
- Owner pays for storage by default
- If enabled:
    - **Requester pays for requests & downloads**
- Requires requester to have an AWS account

---

## 5. S3 Batch Operations

### What is it?
**S3 Batch Operations** allow you to perform **bulk operations on many S3 objects with a single request**.

### Common Use Cases
- Modify **object metadata/properties** in bulk
- Copy objects between buckets
- **Encrypt all unencrypted objects**
- Update **ACLs or tags**
- Restore multiple objects from **S3 Glacier**
- Invoke a **Lambda function** on each object

### How It Works
A **Batch Job** consists of:
- **List of objects**
- **Operation to perform**
- Optional parameters

### Why Use Batch Operations Instead of Scripts?
- Built-in **retry handling**
- **Progress tracking**
- **Completion notifications**
- **Automatic reporting**
- No need to manage custom scripts

### How to Generate Object List
1. Use **S3 Inventory**
    - Generates a list of objects in a bucket
2. Use **Athena**
    - Query and filter objects
3. Pass filtered list to:
    - **S3 Batch Operations**

### Flow
S3 Inventory → Athena (filter) → Batch Operation → Execute Action

### Example
- Find all **unencrypted objects**
- Use:
    - S3 Inventory + Athena
- Then:
    - Run Batch Operation to **encrypt all objects**

---

## 6. Key Concepts

- S3 = **object storage**, not file system
- Buckets are:
    - **Globally unique**
    - **Region-specific**
- Objects:
    - Identified by **keys**
    - Max size = **5 TB**
- No real folders → only **prefixes**
- Multipart upload required for files > 5 GB
- Batch Operations = **bulk management at scale**

---

## 7. Summary

|Component|Description|
|---|---|
|Bucket|Container for objects|
|Object|File stored in S3|
|Key|Full path of object|
|Prefix|“Folder-like” structure|
|Metadata|Info about object|
|Tags|Key-value labels|
|Version ID|Object version tracking|
|Batch Operations|Bulk actions on objects|