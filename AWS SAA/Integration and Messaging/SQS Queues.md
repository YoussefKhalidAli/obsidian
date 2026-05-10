## 1. Core Concept
- **SQS** = Simple Queue Service.
- Provides a **queue** to decouple applications.
- Components:
    - **Producer** → sends messages to the queue.
    - **Queue** → stores messages temporarily.
    - **Consumer** → pulls and processes messages from the queue.

---

## 2. Producers
- Can be **single or multiple** producers.
- Messages can contain anything (e.g., process an order, process a video).
- Messages sent via **AWS SDK** using `SendMessage` API.
- Message stays in the queue until:
    - Consumer **receives and processes** it.
    - Consumer deletes it using `DeleteMessage`.

---

## 3. Consumers
- Applications that process messages from the queue.
- Can run on:
    - **EC2 instances** (virtual servers)
    - **On-premises servers**
    - **AWS Lambda** (serverless)
- **Polling** mechanism: consumer asks queue for messages (up to 10 messages at a time).
- After processing, messages must be **deleted** to prevent reprocessing.
- Horizontal scaling: multiple consumers can process messages in parallel.

---

## 4. SQS Characteristics

|Feature|Description|
|---|---|
|**Throughput**|Unlimited; supports high volume and high throughput.|
|**Message retention**|Default 4 days; max 14 days.|
|**Latency**|Low — <10 ms for send/receive.|
|**Message size**|≤ 1,024 KB per message.|
|**Delivery**|At least once (duplicate messages possible).|
|**Ordering**|Standard queues → best-effort ordering; duplicates possible.|

---

## 5. Scaling with Auto Scaling Groups (ASG)
- Consumers in an **ASG** can scale based on **queue length**:
    - CloudWatch metric: `ApproximateNumberOfMessages`.
    - Queue length triggers alarms → increases EC2 instances.
    - Ensures messages are processed efficiently during traffic spikes.

---

## 6. Architecture Benefits
- **Decouples application tiers**.
- Front-end and backend can scale **independently**.
- Backend instances can use specialized EC2 types (e.g., GPU instances for video processing).
- Supports robust, scalable, and flexible application designs.

---

## 7. Visibility timeout
- Amount of time message is invisible to consumers after it was consumed.
- Default is 30 seconds.
- Message could be consumed twice if not processed before timeout finishes
- If consumer needs more time to finish processing, timeout can be changed with `ChangeMessageVisibility` API call.

---

## 8. Long Polling
- When a consumer requests messages from the queue, it can optionally 'wait' for messages to arrive if there are none in the queue.
- Decreases the number of API calls to SQS.
- Increases efficiency & reduces latency.
- Wait time is between 1 to 20 seconds.
- Can be enabled at the queue level or at the API level using `WaitTimeSeconds`

---

## 9. FIFO Queues
- Ordering of messages in the queue
- 300 msgs/s without batching, 3000 with
- Removes duplicates using deduplication ID
- Order by **Message Group ID** (All messages in the same group are ordered)
- Name **must** end with `.fifo`

---

## 10. Security
- **In-flight encryption**: HTTPS API.
- **At-rest encryption**: AWS KMS.
- **Client-side encryption**: Optional, implemented by client code.
- **Access control**:
    - IAM policies → regulate SQS API access.
    - SQS access policies → similar to S3 bucket policies.
        - Useful for **cross-account access**.
        - Allows services like **SNS** or **S3** to write to SQS.

---

## 11. Use Case Example: Order Processing
- Front-end receives orders → sends message to SQS.
- Backend processing tier reads messages → processes orders (e.g., inserts into **RDS**, uploads to **S3**).
- Decouples **front-end** and **backend**:
    - Front-end isn’t slowed down by heavy processing.
    - Backend can scale independently for processing.

---
## 12. Key Points

- SQS = decoupling tool between producers and consumers.
- **Standard queues**: unlimited throughput, at-least-once delivery.
- Horizontal scaling with ASG based on **queue length**.
- Messages must be deleted after processing.
- Encryption and access control options available.