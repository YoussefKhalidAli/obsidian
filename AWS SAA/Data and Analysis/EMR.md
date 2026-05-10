Amazon EMR is a managed service used to run **big data processing frameworks** such as Hadoop and Spark on AWS.
It simplifies the creation and management of **large-scale distributed data processing clusters**.

---

## 1. What is EMR?

- EMR = Elastic MapReduce
- Used to process **large volumes of data**
- Built on top of **EC2 clusters**
- Automatically manages:
    - Provisioning
    - Configuration
    - Scaling
    - Cluster management

---

## 2. When to Use EMR

Use EMR when working with:

- Big data processing
- Data transformation pipelines
- Machine learning at scale
- Web indexing
- Log processing and analytics

---

## 3. Key Technologies Supported

EMR comes pre-packaged with big data tools:

- Apache Hadoop
- Apache Spark
- Apache HBase
- Apache Flink
- Presto

---

## 4. EMR Architecture (Cluster Components)

An EMR cluster is made of multiple EC2 instances with different roles:

---

### 4.1 Master Node

- Manages the cluster
- Coordinates all tasks
- Tracks cluster health
- Required for every cluster
- Must be **long-running**

---

### 4.2 Core Nodes

- Run tasks (data processing)
- Store data (HDFS storage)
- Required for cluster operation
- Must be **long-running**

---

### 4.3 Task Nodes

- Only run processing tasks
- Do NOT store data
- Optional
- Can be added/removed dynamically
- Often use **Spot Instances**

---

## 5. Instance Purchasing Options

### 5.1 On-Demand Instances

- Reliable and predictable
- Never terminated by AWS
- Higher cost

---

### 5.2 Reserved Instances

- Requires **1-year commitment**
- Significant cost savings
- Best for stable workloads

**Best suited for:**

- Master Nodes
- Core Nodes

---

### 5.3 Spot Instances

- Very low cost
- Can be interrupted by AWS
- Best for fault-tolerant workloads

**Best suited for:**

- Task Nodes

---

## 6. Cluster Types

### 6.1 Long-Running Cluster

- Always active
- Used for continuous processing
- Uses Reserved or On-Demand instances

---

### 6.2 Transient Cluster

- Created for a specific job
- Automatically terminated after completion
- Cost-efficient for batch processing

---

## 7. EMR Key Benefits

- Fully managed big data infrastructure
- Easy scaling of EC2 clusters
- Integrated with Spot Instances for cost savings
- Pre-installed big data frameworks
- Reduces complexity of Hadoop/Spark setup

---

## 8. Key Points

- EMR = Managed Hadoop/Spark cluster service
- Built on EC2 instances
- Three node types:
    - Master (control)
    - Core (compute + storage)
    - Task (compute only)
- Spot instances = Task nodes
- Reserved instances = Core/Master nodes
- Supports both long-running and transient clusters