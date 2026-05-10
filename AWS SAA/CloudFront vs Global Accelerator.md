## 1. Similarities

- Use AWS global network
- Use edge locations
- Integrated with AWS Shield

---

## 2. CloudFront

- Caches content at edge
- Best for:
    - Static content (images, videos)
    - Dynamic HTTP content
- Responses often served **from edge (cached)**

---

## 3. Global Accelerator

- No caching
- Works with **TCP & UDP**
- Proxies traffic to backend
- Best for:
    - Non-HTTP apps (gaming, VoIP, IoT)
    - Apps needing **static IP**
    - Fast failover

---

## 4. When to Use What

### 4.1 Use CloudFront when:
- You want **caching**
- CDN for websites
- Reduce load on origin

### 4.2 Use Global Accelerator when:
- Need **static IP**
- Need **low latency for dynamic/non-HTTP traffic**
- Need **multi-region failover**
