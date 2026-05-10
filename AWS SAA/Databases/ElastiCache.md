## 1. What is Amazon ElastiCache?

- **Definition:** Fully managed in-memory caching service.
- **Supported Engines:**
  - **Redis** (advanced features, persistence, replication)
  - **Memcached** (simple, distributed caching)
- **Purpose:**
  - Reduces load on databases for **read-intensive workloads**.
  - Enables **high-performance, low-latency data retrieval**.
  - Helps make applications **stateless** by storing state in the cache.

---

## 2. Application Architecture Example

- **Components:** Application → ElastiCache → RDS Database
- **Workflow:**
  1. Application queries ElastiCache first.
  2. If data exists (cache hit), return cached result.
  3. If data doesn’t exist (cache miss), query database.
  4. Store fetched database result back in cache.
- **Benefits:**
  - Reduces database load.
  - Improves performance and scalability.
- Development overhead 
  - Must implement a **cache invalidation strategy** to ensure only fresh, correct data is returned.
  - Change to application code is necessary
 
---

## 3. Making Applications Stateless

- **Problem:** User session data is typically stored in memory of application instance.
- **Solution:** Store session data in ElastiCache.
- **Benefit:**  
  - User can switch between application instances without losing session.
  - Application becomes **stateless**.
  
---

## 4. Redis vs Memcached

| Feature                       | Redis                                   | Memcached                            |
|--------------------------------|----------------------------------------|-------------------------------------|
| High Availability             | Multi-AZ with auto-failover            | No built-in replication/HA          |
| Read Scaling                   | Read replicas                           | Sharding across nodes               |
| Data Durability                | AOF persistence, backups               | Serverless Memcached has backup, not standard nodes |
| Data Structures                | Strings, sets, sorted sets, hashes     | Simple key-value                     |
| Use Case Example               | Leaderboards, analytics, session store | Simple caching, partitioned data    |
| Performance Architecture       | Single-threaded per node (replication) | Multi-threaded, sharded nodes       |

- **Redis:**  
  - Offers **replication** for high availability.
  - Supports **persistence** (AOF), backup & restore.
  - Advanced data structures → ideal for leaderboards, counters, queues.
- **Memcached:**  
  - Uses **sharding** → distributes data across nodes.
  - Multi-threaded → better raw throughput.
  - No replication → cache loss possible if a node fails.

---

## 5. Key Points

- ElastiCache is for **read-heavy workloads** to reduce database load.
- Make applications stateless by storing session or state in the cache.
- **Cache hit/miss logic** is fundamental to caching strategies.
- **Redis** → replication, persistence, complex data types.  
- **Memcached** → simple, sharded, multi-threaded, no replication.
- Application **code changes** are required to integrate caching.