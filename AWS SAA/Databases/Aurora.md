## 1. What is Aurora?

Amazon Aurora is a **cloud-native relational database** built by AWS.

- Compatible with:
  - MySQL
  - PostgreSQL
- Proprietary (not open-source)
- Uses standard drivers → easy migration

---
## 2. Distributed Storage Architecture

![[Aurora_architecture.png]]

Aurora stores data in a highly resilient way:
- Data split into blocks
- Each block replicated **6 times**
- Across **3 Availability Zones**
### Quorum Model:
- Writes require **4/6 copies**
- Reads require **3/6 copies**
### Benefits:
- Fault tolerance
- High availability
- Self-healing storage
- No single point of failure

---

## 3. Why Aurora is Faster

### 1. No replication overhead
- Writes go directly to distributed storage
### 2. Shared storage for replicas
- No need to copy data between instances
### 3. Distributed I/O
- Storage layer handles heavy operations

---

## 4. Aurora Cluster Architecture

Aurora works as a **cluster**, not a single DB.
### Components:

#### 5.1 Writer (Primary Instance)
- Handles writes
- Only one at a time

#### 5.2 Read Replicas
- Handle read traffic
- Up to 15 replicas

#### 5.3 Shared Storage Layer
- Used by all instances
- Auto-scaling & replicated

---

## 5. Endpoints (Important)

### Writer Endpoint
- Points to current master
- Used for writes
- Automatically updated after failover

### Reader Endpoint
- Connects to read replicas
- Load balances connections

⚠️ Load balancing is **per connection**, not per query

---

## 6. Read Scaling

- Up to **15 read replicas**
- Replica lag typically **< 10 ms**
- Supports auto scaling

---

## 7. Failover

- Automatic failover (~30 seconds or less)
- Any replica can become master

### Why fast?
- Replicas already use same storage
- No data sync needed

---
## 8. Replica Auto Scaling

Aurora supports **automatic read replica scaling**, which is key for handling unpredictable or heavy read workloads.

### How it works:
- Metrics like **CPU usage, memory, or connections** are monitored.
- When read traffic increases, **Aurora automatically adds read replicas**.
- When traffic decreases, unused replicas are **removed automatically**.
- The **reader endpoint automatically updates** to include new replicas.
- Benefits:
  - Reduces CPU/memory bottlenecks.
  - Maintains performance without manual intervention.
  - Saves cost by only using replicas when needed.

---

## 9. Custom Endpoints

Aurora allows **custom endpoints** to manage subsets of replicas for specialized workloads.

### Use Cases:
- Some replicas have more powerful instance types (e.g., db.r5.2xlarge vs db.r3.large).
- Assign these replicas to analytical workloads.
- Example:  
  - You have 5 read replicas:
    - 2 are large instances for analytics  
    - 3 are standard for normal application reads
  - Create a **custom endpoint** for the 2 large replicas.
- Benefits:
  - Targeted queries on high-performance nodes.
  - Optimizes resource usage.
  - Reader endpoint may still exist but is **not used for specialized workloads**.

---

## 10. Aurora Serverless

Aurora Serverless allows **compute capacity to scale automatically** based on workload.

### How it works:
1. No need to provision database instances upfront.
2. Aurora automatically **spins up new instances** when demand increases.
3. When traffic decreases, instances are automatically **removed**.
4. Billing is based on **actual usage per second**, not idle time.

### Ideal Scenarios:
- Applications with intermittent traffic.
- Testing environments.
- Development environments where cost efficiency is important.

### Architecture:
- Clients connect via **Aurora proxy fleet**.
- The proxy abstracts multiple backend instances.
- Aurora automatically manages scaling behind the scenes.

---

## 11. Aurora Global Database

Aurora supports **cross-region replication** for global apps and disaster recovery.

### Architecture:
- **Primary Region**: read/write.
- **Secondary Regions**: read-only replicas for global access.

### Key Features:
- Data replication lag **< 1 second**.
- Supports up to **10 secondary regions**.
- Each secondary region can have **up to 16 read replicas**.
- Failover to another region in **< 1 minute** (RTO).

### Benefits:
- Low-latency read access globally.
- Disaster recovery with minimal downtime.
- Ideal for multi-region SaaS or enterprise applications.

---

## 12. Backtrack

Aurora offers **Backtrack**, which allows you to rewind your database to a previous point in time **without restoring from a snapshot**.

### Features:
- Time-travel rollback (seconds or minutes ago).
- Does not rely on manual backups.
- Useful for:
  - Mistaken deletes
  - Application errors
  - Failed transactions
- Example:
  - Current time: 3:00 PM
  - User wants to restore data to 2:55 PM → Aurora Backtrack can instantly roll back.

---

## 13. Aurora Machine Learning Integration

Aurora can integrate with **AWS Machine Learning services** for predictive analytics.

### How it works:
- SQL query triggers Aurora to send data to **SageMaker** or **Amazon Comprehend**.
- ML model returns prediction directly in SQL query results.
- Example Use Cases:
  - Fraud detection
  - Product recommendations
  - Sentiment analysis
  - Targeted ads

### Benefits:
- No need to export data or build separate pipelines.
- Directly use ML predictions inside database queries.
- Supports both batch and real-time predictions.

---

## 14. Babelfish for Aurora PostgreSQL

Babelfish allows Aurora PostgreSQL to **understand T-SQL queries from SQL Server applications**.

### Purpose:
- Migrate SQL Server applications to Aurora PostgreSQL **without rewriting code**.

### How it works:
- Application uses **SQL Server client driver**.
- Aurora PostgreSQL with Babelfish **translates T-SQL → PostgreSQL internally**.
- Application behaves as if it’s still connected to SQL Server.

### Benefits:
- Reduces migration time and complexity.
- Supports existing T-SQL queries and stored procedures.
- Ideal for enterprises with legacy SQL Server apps moving to AWS.

---
## 15. Core Difference from RDS

### RDS:
- Instance-based
- Each instance has its own storage
- Replication between instances

### Aurora:
- Cluster-based
- Shared distributed storage
- No traditional replication between instances

 Aurora separates:
- **Compute (DB instances)**
- **Storage (distributed system)**

---

## 16. Key Takeaways

- **Storage**:
  - Shared, distributed, self-healing, auto-expanding
- **Cluster**:
  - One writer (master)
  - Up to 15 read replicas
- **Endpoints**:
  - Writer endpoint → always points to master
  - Reader endpoint → load balances across read replicas
  - Custom endpoints → subset of replicas for special workloads
- **High availability**:
  - Automatic failover
  - 6-way replicated storage
  - Multi-AZ & Global DB options
- **Advanced Features**:
  - Serverless
  - Replica auto-scaling
  - Backtrack
  - Aurora Machine Learning
  - Babelfish (for SQL Server migrations)