When deploying multiple applications, **services need to communicate** to share data or trigger actions. Communication patterns fall into two categories:

---

## 1. Synchronous Communication
- Applications **talk directly** to one another.
- Example:
    - Buying service → Shipping service
- Pros:
    - Immediate processing
- Cons:
    - Can cause **overload** if one service gets a traffic spike
    - Tightly coupled architecture
- Use case caution:
    - Sudden spikes in traffic (e.g., video encoding 1,000 videos at once) can cause outages.

---
## 2. Asynchronous (Event-Based) Communication
- Applications **do not communicate directly**.
- Instead, they use **middleware** like queues or topics.
- Example:
    - Buying service → puts message in a queue
    - Shipping service → reads from queue independently
- Pros:
    - Decoupled architecture
    - Services can **scale independently**
    - Handles unpredictable workloads better
- Common AWS services for asynchronous messaging:
    - **SQS** → Queue model
    - **SNS** → Pub/Sub model
    - **Kinesis** → Real-time streaming, big data workloads

---

## 3. Key Advantages of Asynchronous Messaging
- Avoids blocking downstream services
- Middleware layer can **absorb traffic spikes**
- Applications remain independent
- AWS services used scale automatically and reliably

---
## 4. Summary
- **Synchronous** → direct, immediate, tightly coupled, can fail under spikes
- **Asynchronous** → indirect via middleware, decoupled, scalable, resilient
- Middleware options:
    - **SQS** → reliable message queuing
    - **SNS** → pub/sub notifications
    - **Kinesis** → real-time streaming