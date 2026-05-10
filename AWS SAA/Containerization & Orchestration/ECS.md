## **Core Idea**

Amazon ECS is a **container orchestration service** used to run Docker containers on AWS without managing the container runtime yourself.

You define:

- What to run (container image + configuration)
- How much CPU/RAM is needed
- How many copies to run

ECS handles placement and execution of containers on infrastructure.

---

## **ECS Architecture Basics**

### **Cluster**

An ECS Cluster is a logical grouping of compute resources that run containers.

### **Task**

A Task is a running instance of a container (or group of containers defined together).

### **Task Definition**

A blueprint that defines:

- Container image
- CPU / memory
- Ports
- Environment variables
- IAM roles

---

## **Launch Types**

ECS supports two main ways to run containers.

---

# **1. EC2 Launch Type**

## **Concept**

You manage the infrastructure yourself.

ECS runs containers on **EC2 instances that you provision and maintain**.

---

## **How it works**

- You create an ECS cluster
- You launch EC2 instances into the cluster
- Each EC2 instance runs an **ECS agent**
- The agent registers the instance with ECS
- ECS places containers (tasks) on these instances

---

## **Responsibility model**

You manage:

- EC2 instances
- Scaling capacity
- Patching and updates

ECS manages:

- Container placement
- Task lifecycle

---

## **Key point**

Containers run **on your EC2 instances**, not abstracted.

---

# **2. Fargate Launch Type**

## **Concept**

Fargate is **serverless container execution**.

You do NOT manage EC2 instances at all.

---

## **How it works**

- You define a task (CPU, memory, image)
- ECS runs it on AWS-managed infrastructure
- You don’t see or manage the servers

---

## **Scaling**

- You scale by increasing the number of tasks
- No infrastructure management required

---

## **Key point**

Fargate = “just run containers” without thinking about servers.

---

# **IAM Roles in ECS**

## **1. EC2 Instance Role (Instance Profile)**

Used only in **EC2 launch type**.

### Who uses it?

The **ECS agent on the EC2 instance**

### What it allows:

- Pull container images from ECR
- Send logs to CloudWatch Logs
- Interact with ECS service
- Access Secrets Manager / SSM Parameter Store

### Key idea:

This role belongs to the **EC2 instance**, not the container.

---

## **2. ECS Task Role**

Used in **both EC2 and Fargate**

### Who uses it?

The **container itself (task)**

### Why it exists

Each task can have its own permissions.

### Example:

- Task A → access S3
- Task B → access DynamoDB

### Key idea:

This is the **correct way to give permissions to containers**

---

## **takeaway**

- Instance role = EC2 host permissions
- Task role = container permissions (VERY important)

---

# **Load Balancer Integration**

ECS services are commonly exposed via load balancers.

---

## **Application Load Balancer (ALB)**

- Most common choice
- Supports HTTP/HTTPS
- Works with EC2 and Fargate
- Supports routing rules (path/host-based)

---

## **Network Load Balancer (NLB)**

Used when:

- Very high performance / throughput
- Low-level TCP/UDP traffic
- PrivateLink integration

---

## **Classic Load Balancer**

- Legacy
- Not recommended
- Limited features
- Not ideal for modern ECS usage

---

## **Key idea**

ALB is the default for most ECS workloads.

---

# **Storage / Persistence in ECS**

Containers are ephemeral, so persistence requires external storage.

---

## **Amazon EFS (Elastic File System)**

### Why EFS is used:

- Fully managed file system
- Multi-AZ shared storage
- Works with EC2 and Fargate

---

## **How it works in ECS**

- ECS tasks mount EFS volume
- Multiple tasks can access the same data
- Data persists independently of container lifecycle

---

## **Use cases**

- Shared uploads
- Persistent application data
- Multi-container collaboration
- Stateful workloads in containers

---

## **Key combo**

Fargate + EFS = fully serverless compute + persistent storage

---

# **Key Points**

- ECS = Docker container orchestration service
- Two launch types:
    - EC2 → you manage servers
    - Fargate → serverless containers
- Two IAM roles:
    - Instance role → EC2 host permissions
    - Task role → container permissions
- ALB is the default load balancer
- EFS is the main storage option for shared persistence
- Fargate + ECS + EFS = common modern architecture