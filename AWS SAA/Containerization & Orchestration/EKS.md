Amazon EKS is a fully managed service that allows you to run **Kubernetes clusters on AWS** without managing the Kubernetes control plane yourself.

**Explanation:** Kubernetes is an open-source container orchestration system used to deploy, scale, and manage containerized applications (typically Docker). EKS provides a managed AWS implementation of Kubernetes.

---

## 1. Core Concept

- EKS = Managed Kubernetes on AWS
- Uses the standard **Kubernetes API (cloud-agnostic)**
- Alternative to Amazon ECS

**Explanation:** Unlike ECS (AWS-specific), Kubernetes can run across AWS, Azure, Google Cloud, and on-premises, which makes it useful for multi-cloud or migration scenarios.

---

## 2. EKS Architecture

### 2.1 Control Plane (Managed by AWS)

- Kubernetes API server
- Cluster management
- Scheduling and orchestration

**Explanation:** AWS fully manages the control plane, including availability and scaling.

---

### 2.2 Worker Nodes (User-managed or AWS-managed)

- Run container workloads (Pods)
- Can be EC2 instances or Fargate

---

## 3. Key Kubernetes Terminology

### 3.1 Cluster

- Entire Kubernetes environment

### 3.2 Node

- EC2 instance (or Fargate runtime) that runs workloads

### 3.3 Pod

- Smallest deployable unit in Kubernetes
- Usually contains one or more containers

**Explanation:** Pods in EKS are conceptually similar to ECS tasks.

---

## 4. Compute Options in EKS

### 4.1 Managed Node Groups

- AWS manages EC2 instances for you
- Integrated with Auto Scaling Groups
- Supports On-Demand and Spot Instances

**Explanation:** Simplest EC2-based option for running Kubernetes workloads.

---

### 4.2 Self-Managed Nodes

- You manage EC2 instances yourself
- Must register nodes to the EKS cluster manually
- Can use EKS-optimized AMIs or custom AMIs

**Explanation:** Provides maximum control and customization.

---

### 4.3 AWS Fargate for EKS

- Serverless Kubernetes
- No EC2 nodes to manage
- AWS runs pods directly

**Explanation:** Best for reducing operational overhead.

---

## 5. Networking and Load Balancing

- Kubernetes services are exposed using AWS Load Balancers
    - Application Load Balancer (ALB) for HTTP/HTTPS
    - Network Load Balancer (NLB) for high performance or low-level networking

**Explanation:** External traffic is routed into Kubernetes workloads via AWS load balancers.

---

## 6. Storage in EKS

Storage is defined using Kubernetes **StorageClasses** with CSI (Container Storage Interface) drivers.

Supported storage options:

- Amazon EBS (block storage)
- Amazon EFS (shared file system)
- Amazon FSx for Lustre
- Amazon FSx for NetApp ONTAP

**Important rule:**

- Only **Amazon EFS works with Fargate in EKS**

**Explanation:** Storage is dynamically provisioned and attached to pods via Kubernetes manifests.

---

## 7. Scaling

- Worker nodes scale using Auto Scaling Groups (EC2 mode)
- Pods scale using Kubernetes scaling mechanisms (e.g., Horizontal Pod Autoscaler)
- Fargate scales automatically per pod demand

**Explanation:** Scaling can happen at both infrastructure (nodes) and application (pods) levels.

---

## 8. Key Use Cases

- Migrating existing Kubernetes workloads to AWS
- Multi-cloud or hybrid cloud Kubernetes deployments
- Standardized container orchestration across environments
- Microservices architecture using Kubernetes APIs

---

## 9. Key Points

- EKS = managed Kubernetes service on AWS
- Uses Pods instead of ECS Tasks
- Control plane is fully managed by AWS
- Supports EC2 worker nodes or Fargate (serverless)
- Uses CSI drivers for storage integration
- Highly portable (cloud-agnostic compared to ECS)