## What is Elastic Beanstalk?

**Amazon Elastic Beanstalk** is a **Platform as a Service (PaaS)** that allows you to deploy and manage applications without handling the underlying infrastructure.
- You upload your code
- AWS automatically provisions:
  - EC2 instances
  - Load Balancer (ELB)
  - Auto Scaling Group (ASG)
  - Optional RDS database

Focus only on **application code**, not infrastructure.

---

## Why Use Beanstalk?

Without Beanstalk, you must:
- Manually configure servers
- Set up load balancing
- Configure scaling
- Monitor health

With Beanstalk:
- Automated provisioning
- Built-in scaling
- Health monitoring
- Easy deployments
- Centralized management

---
## Pricing

- Beanstalk itself = **FREE**
- You pay for:
  - EC2
  - Load Balancer
  - RDS
  - Storage

---

## Core Components

### 1. Application
- Logical container for all resources
- Includes environments, versions, configurations

### 2. Application Version
- A specific version of your code
- Example:
  - v1 → initial release
  - v2 → updated version

### 3. Environment
- Infrastructure running your app
- Runs **only one version at a time**
Examples:
- dev
- test
- prod

### 4. Environment Lifecycle

Create App → Upload Version → Launch Environment → Deploy → Update Versions

## Environment Types (Tiers)

### Web Server Environment

Standard web architecture:
Client → Load Balancer → EC2 (Auto Scaling)

- Handles HTTP requests
- Used for web apps and APIs

---

### Worker Environment

Used for background processing:
Producer → SQS Queue → Worker EC2 Instances

- No direct user traffic
- Processes:
  - Background jobs
  - Async tasks

Scaling based on:
- Number of messages in SQS

---

### Combined Architecture
Web Tier → SQS → Worker Tier

Example:
- User uploads image → Web tier → SQS → Worker resizes image

---

## Deployment Modes

### Single Instance (Development)

- One EC2 instance
- Optional RDS
- Elastic IP

✔️ Low cost  
❌ No high availability  

---

### High Availability (Production)

- Load Balancer
- Auto Scaling Group
- Multiple Availability Zones
- Optional Multi-AZ RDS

✔️ Fault tolerant  
✔️ Scalable  

---

## Deployment Strategies

| Strategy | Description | Downtime |
|----------|------------|---------|
| All-at-once | Replace all instances at once | Yes |
| Rolling | Update instances in batches | Minimal |
| Rolling + additional batch | Extra capacity during update | No |
| Immutable | New instances first, then switch | No |
| Blue/Green | New environment swap | No |

---

## Supported Platforms

- Node.js
- Python
- Java (SE, Tomcat)
- .NET (Linux & Windows)
- PHP
- Ruby
- Go
- Docker (single & multi-container)

---

## What Beanstalk Manages

- Infrastructure provisioning
- Load balancing
- Auto scaling
- Health monitoring
- OS patching
- Deployment orchestration

---

## What You Manage

- Application code
- Optional configuration settings

---

## Key Points

- Beanstalk = **PaaS**
- Free service (pay for underlying resources)
- Supports:
  - Web tier
  - Worker tier (uses SQS)
- Uses:
  - EC2
  - ELB
  - ASG
  - RDS
- One environment = one application version
- Multiple environments allowed
- Supports multiple deployment strategies

---

## When to Use Beanstalk

Use it when:
- You want fast deployment
- You don’t want to manage infrastructure
- You need auto scaling and high availability quickly

Avoid it when:
- You need full infrastructure control