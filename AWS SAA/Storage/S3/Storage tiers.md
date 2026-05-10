# 1. Core Concepts: Durability vs Availability

## Durability

Durability refers to **how likely your data is to be lost permanently**.
- Amazon S3 provides **99.999999999% (11 nines) durability**
- This is **the same across all storage classes**
- Achieved by storing data redundantly across multiple devices and facilities

---

## Availability

Availability refers to **how often you can successfully access your data**.
- Varies by storage class
- Lower availability → cheaper cost
- Measured as a percentage over a year

Example:
- 99.99% ≈ ~53 minutes downtime/year
- 99.9% ≈ ~8.7 hours downtime/year

---

# 2. Overview of S3 Storage Classes

S3 storage classes are designed around three trade-offs:
- Cost
- Access frequency
- Retrieval latency

---

# 3. S3 Standard (General Purpose)

## Characteristics
- Designed for **frequent access**
- Stored across **multiple Availability Zones**
- **Low latency and high throughput**
- **No retrieval cost**
- **No minimum storage duration**
- 99.99% Availability
## Use cases
- Web applications
- Content distribution
- Big data analytics
- Active datasets

> Note: There is always a small cost per *request* on every tier, so no retrieval cost just means you don't pay for bandwidth

---

# 4. S3 Standard-Infrequent Access (Standard-IA)

## Characteristics
- Designed for **infrequently accessed data**
- Still requires **fast retrieval (milliseconds)**
- Stored across **multiple AZs**
- **Lower storage cost**
- **Retrieval cost applies**
- 99.99% Availability
- 30 Days minimum storage duration

## Use cases
- Backups
- Disaster recovery
- Long-term but occasionally accessed data

---

# 5. S3 One Zone-Infrequent Access (One Zone-IA)

## Characteristics

- Same as Standard-IA, but:
    - Stored in **only one AZ**
- Lower cost than Standard-IA
- **Data loss possible if AZ fails**
- 99.5% Availability
- 30 Days minimum storage duration
## Use cases
- Secondary backups
- Re-creatable data
- Temporary data storage

---

# 6. Glacier Storage Classes (Archival)

All Glacier classes:
- Designed for **archiving**
- Lower storage cost
- **Retrieval cost applies**
- Higher retrieval latency (except Instant Retrieval)

## 6.1 Glacier Instant Retrieval

## Characteristics
- Archive storage with **millisecond access**
- Cheaper than Standard-IA
- 90 Days minimum storage duration

## Use cases
- Data accessed rarely but must be retrieved instantly
- Medical images, archives with occasional access

## 6.2 Glacier Flexible Retrieval (formerly Glacier)

## Characteristics

- Lower cost than Instant Retrieval
- 90 Days minimum storage duration
- Multiple retrieval speeds:

| Mode      | Retrieval Time |
| --------- | -------------- |
| Expedited | 1–5 minutes    |
| Standard  | 3–5 hours      |
| Bulk      | 5–12 hours     |

## Use cases
- Backups
- Archival data where delays are acceptable

## 6.3 Glacier Deep Archive

## Characteristics

- 180 Days minimum storage duration
- **Lowest storage cost**
- Longest retrieval times

|Mode|Retrieval Time|
|---|---|
|Standard|~12 hours|
|Bulk|~48 hours|
## Use cases
- Long-term archives (years)
- Compliance data
- Data rarely accessed

---
# 7. Express One Zone

## Overview

- **High-performance S3 storage class**
- Designed for **very low latency and very high request rates**
- Data is stored in a **single Availability Zone (AZ)**

## Key Characteristics

- Uses a special type of bucket called a **Directory Bucket**
    - Different from standard S3 buckets
    - Data is **not distributed across multiple AZs**
    - You must **choose the AZ explicitly**
    - 99.95% Availability
- **Performance**
    - Supports **hundreds of thousands of requests per second**
    - **Single-digit millisecond latency**
    - Up to **10x faster than S3 Standard**
- **Cost**
    - Can be up to **50% cheaper than S3 Standard** (for certain workloads)

---

# 7. S3 Intelligent-Tiering

## Characteristics

- Automatically moves objects between tiers based on access patterns
- Eliminates need to manually choose storage class
- Small monitoring fee applies
- No retrieval charges for frequent tiers

## Internal tiers

| Tier                           | When used                   |
| ------------------------------ | --------------------------- |
| Frequent Access                | Default                     |
| Infrequent Access              | After ~30 days of no access |
| Archive Instant                | After ~90 days              |
| Archive Access (optional)      | Configurable                |
| Deep Archive Access (optional) | Configurable                |

## Use cases
- Unknown or unpredictable access patterns
- Applications where access frequency changes over time

---

# 8. Lifecycle Policies

S3 Lifecycle rules allow automatic movement of objects between classes.

Example:

- Day 0 → Standard
- Day 30 → Standard-IA
- Day 90 → Glacier
- Day 365 → Deep Archive

This is used for **cost optimization**.

---

# 9. Key Comparison Table

|Storage Class|Access Pattern|Availability|AZs|Retrieval Time|Cost|Min Duration|
|---|---|---|---|---|---|---|
|Standard|Frequent|99.99%|Multi-AZ|ms|High|None|
|Standard-IA|Infrequent|99.9%|Multi-AZ|ms|Medium|30 days|
|One Zone-IA|Infrequent|99.5%|Single AZ|ms|Lower|30 days|
|Glacier Instant|Rare|High|Multi-AZ|ms|Lower|90 days|
|Glacier Flexible|Rare|High|Multi-AZ|Minutes–Hours|Low|90 days|
|Deep Archive|Very rare|High|Multi-AZ|Hours–Days|Lowest|180 days|
|Intelligent-Tiering|Variable|High|Multi-AZ|Depends|Medium|None|

---

# 10. Decision Logic

- Frequent access → Standard
- Infrequent but immediate access → Standard-IA
- Infrequent + can lose AZ → One Zone-IA
- Rare + instant retrieval needed → Glacier Instant
- Rare + okay with hours delay → Glacier Flexible
- Very rare + cheapest → Deep Archive
- Unknown access pattern → Intelligent-Tiering

---

# 11. Common Pitfalls

1. All storage classes have the same durability
2. Glacier is not always slow (Instant Retrieval exists)
3. IA classes charge for retrieval
4. One Zone-IA sacrifices AZ redundancy
5. Intelligent-Tiering adds monitoring cost

---

# 12. Final Summary

S3 storage classes are designed to optimize **cost vs access frequency vs retrieval speed**, while maintaining the same high durability across all classes. The correct choice depends entirely on how often data is accessed and how quickly it must be retrieved.