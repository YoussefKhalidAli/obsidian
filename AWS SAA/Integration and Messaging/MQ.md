## **Core Idea**

Amazon MQ is a **managed message broker service** that lets you use **traditional messaging systems and protocols in AWS** without changing your existing applications.

It exists mainly for **lift-and-shift migrations** where you already use messaging brokers on-premises.

---

## **Why Amazon MQ Exists**

AWS native messaging services:

- SQS (queue)
- SNS (pub/sub)

These use **AWS-specific APIs** and are highly scalable.

But many enterprise systems already use:

- MQTT
- AMQP
- STOMP
- OpenWire
- WSS

Instead of rewriting applications to use SQS/SNS, you can use Amazon MQ to keep existing messaging logic.

---

## **What Amazon MQ Is**

Amazon MQ is a **fully managed message broker service** based on:

- Apache ActiveMQ
- RabbitMQ

It provides:

- Queues (like SQS)
- Topics (like SNS)
- Support for open messaging protocols

---

## **Key Use Case**

Use Amazon MQ when:

- You are migrating legacy applications to AWS
- You cannot change messaging protocols
- You need compatibility with existing on-premises brokers

---

## **Architecture Characteristics**

### **Not Highly Scalable Like SQS/SNS**

- Amazon MQ runs on **broker instances (servers)**
- Scaling is limited compared to serverless services
- Requires capacity planning

---

## **High Availability (Multi-AZ Setup)**

Amazon MQ supports HA using:

### **Active / Standby Architecture**

- One broker is active (primary AZ)
- One broker is standby (secondary AZ)

### **Failover Process**

- If active broker fails → standby takes over

---

## **Data Storage (Important Detail)**

To ensure data consistency across failover:

- Amazon MQ uses **Amazon EFS (Elastic File System)** as shared storage

### **Why EFS is used**

- Shared network file system
- Mounted across multiple AZs
- Ensures both brokers see the same message data

### **Result**

- No message loss during failover
- Standby broker can continue processing seamlessly

---

## **Protocols Supported**

Amazon MQ supports traditional messaging protocols:

- MQTT
- AMQP
- STOMP
- OpenWire
- WSS

This makes it compatible with:

- Enterprise systems
- IoT messaging (MQTT)
- Legacy middleware

---

## **Queue + Topic Support**

Amazon MQ provides both:

- **Queues** → like SQS (point-to-point)
- **Topics** → like SNS (pub/sub)

All inside the same broker system.

---

## **Amazon MQ vs SQS/SNS**

|Feature|Amazon MQ|SQS / SNS|
|---|---|---|
|Type|Managed message broker|Native AWS messaging|
|Protocols|MQTT, AMQP, etc.|AWS APIs|
|Scaling|Limited (server-based)|Highly scalable (serverless)|
|Setup|More complex|Simple|
|Use case|Legacy migration|Cloud-native apps|
|HA model|Active/standby|Fully managed multi-AZ|

---

## **Key Points**
- Amazon MQ = **managed ActiveMQ/RabbitMQ broker**
- Used for **legacy migration (lift-and-shift)**
- Supports **traditional messaging protocols**
- Provides **queues + topics in one system**
- Not as scalable as SQS/SNS
- High availability uses:
    - Active/standby brokers
    - Shared **Amazon EFS storage**
- Use when you **cannot change application messaging code**