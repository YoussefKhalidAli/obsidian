## 1. ElastiCache Security Overview

### Redis Security
- **IAM Authentication:** Supported only for Redis.
  - IAM policies protect **AWS API-level operations**, not data inside Redis itself.
- **Redis AUTH:**  
  - Set a **password/token** during cluster creation.
  - Works together with **security groups** for extra protection.
- **In-Flight Encryption:** Supported via **SSL/TLS**.

### Memcached Security
- **SASL-Based Authentication:** Advanced mechanism for Memcached.

### Summary Patterns
- **Client EC2 → Redis:**
  - Use **Redis AUTH** + **Redis Security Group** + optional **in-flight encryption**.
  - Or leverage **IAM authentication** (for API-level security).

---

## 2. Loading Data into ElastiCache — Caching Patterns

1. **Lazy Loading**
   - Data is loaded into cache **only when not present**.
   - Cache can become **stale**.
   - Workflow:
     - Cache hit → return data.
     - Cache miss → read from DB → write to cache.

2. **Write Through**
   - Every write to database also updates the cache **immediately**.
   - Ensures **no stale data** in cache.

3. **Session Store**
   - Store user session data in cache.
   - Expire session with **TTL (Time-To-Live)**.

---

## 3. Key Takeaways

- Redis AUTH + Security Groups + SSL → strong security.
- IAM authentication → API-level control for Redis.
- Lazy loading vs Write-through → caching strategies.
- TTL → manage session expiration.
- Sorted Sets → real-time leaderboards in Redis.
- Caching is **hard**, mainly due to **invalidation and consistency**.