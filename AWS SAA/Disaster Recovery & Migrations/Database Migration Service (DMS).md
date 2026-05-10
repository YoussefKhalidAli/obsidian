AWS DMS is a service used to **migrate databases to AWS quickly and securely** with minimal downtime.  
  
---  
  
## 1. What is AWS DMS?  
  
AWS Database Migration Service (DMS) allows you to:  
  
- Migrate databases from **on-premises to AWS**  
- Migrate between **different database engines**  
- Perform **continuous replication during migration**  
  
**Explanation:** DMS is designed to keep the source database running while data is continuously copied to the target, minimizing downtime.  
  
---  
  
## 2. Key Features of DMS  
  
- **Highly available and self-healing**  
- Source database remains **fully operational during migration**  
- Supports **homogeneous and heterogeneous migrations**  
- Uses **Change Data Capture (CDC)** for continuous replication  
  
**Explanation:** CDC allows DMS to track and replicate ongoing changes (inserts, updates, deletes) in near real time.  
  
---  
  
## 3. DMS Architecture  
  
DMS works using a **replication instance (EC2-based)**:  
  
- A DMS replication instance runs inside AWS  
- It connects to:  
- **Source database** (on-premises or AWS)  
- **Target database** (AWS or other supported service)  
- It performs:  
- Full data load (initial migration)  
- Continuous replication (CDC)  
  
**Explanation:** The replication instance is the engine that reads data from the source and writes it to the target.  
  
---  
  
## 4. Supported Sources  
  
DMS can migrate from:  
  
- On-premises databases (Oracle, SQL Server, MySQL, PostgreSQL, MariaDB, MongoDB, SAP, DB2)  
- EC2-hosted databases  
- AWS databases (RDS, Aurora, DocumentDB)  
- Azure SQL Database  
- Amazon S3 (for some use cases)  
  
**Explanation:** DMS is flexible and supports both cloud and on-premises database sources.  
  
---  
  
## 5. Supported Targets  
  
DMS can migrate to:  
  
- Amazon RDS (any supported engine)  
- Aurora  
- Redshift (analytics warehouse)  
- DynamoDB (NoSQL)  
- Amazon S3 (data lake storage)  
- Kinesis Data Streams (streaming data)  
- Apache Kafka  
- DocumentDB  
- Neptune (graph database)  
- Redis (ElastiCache)  
- Babelfish (PostgreSQL compatibility for SQL Server apps)  
  
**Explanation:** Targets include both relational and non-relational AWS services.  
  
---  
  
## 6. Homogeneous vs Heterogeneous Migration  
  
### Homogeneous Migration  
- Same database engine  
- Example: Oracle → Oracle, PostgreSQL → PostgreSQL  
  
**Explanation:** No schema conversion needed.  
  
---  
  
### Heterogeneous Migration  
- Different database engines  
- Example: Oracle → PostgreSQL, SQL Server → Aurora  
  
**Explanation:** Requires schema conversion before data migration.  
  
---  
  
## 7. AWS Schema Conversion Tool (SCT)  
  
SCT is used when migrating between **different database engines**.  
  
### What SCT does:  
- Converts database schema from source engine to target engine  
- Translates tables, indexes, views, and stored procedures where possible  
  
### When SCT is required:  
- Oracle → PostgreSQL  
- SQL Server → MySQL  
- Any cross-engine migration  
  
### When SCT is NOT required:  
- Same engine migration (e.g., PostgreSQL → RDS PostgreSQL)  
  
**Explanation:** DMS moves the data, but SCT converts the structure when engines differ.  
  
---  
  
## 8. Migration Process Flow  
  
Typical migration setup:  
  
1. SCT converts schema (if needed)  
2. Target database is created (e.g., RDS MySQL)  
3. DMS replication instance is launched  
4. DMS performs:  
- Full load (initial data copy)  
- CDC (continuous replication)  
5. Source database continues running during migration  
  
**Explanation:** This allows near-zero downtime migrations.  
  
---  
  
## 9. Multi-AZ in DMS  
  
- DMS supports **Multi-AZ deployment**  
- A standby replication instance is created in another AZ  
  
### Benefits:  
- High availability  
- Failover support  
- Reduced latency spikes  
- Protection from AZ failure  
  
**Explanation:** Multi-AZ ensures the replication process continues even if one AZ fails.  
  
---  
  
## 10. Key Points  
  
- DMS is used for **database migration with minimal downtime**  
- Uses **EC2-based replication instance**  
- Supports **homogeneous and heterogeneous migrations**  
- **CDC enables continuous replication**  
- **SCT is required only for cross-engine migrations**  
- Multi-AZ provides **high availability for replication tasks**