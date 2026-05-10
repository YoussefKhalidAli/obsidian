## 1. What is RDS Proxy?

- **Definition:** Fully managed, highly available database proxy for RDS and Aurora.
- **Purpose:** Acts as an intermediary between your application and the RDS/Aurora database instance.
- **Key Functionality:**
  - Pools and shares database connections.
  - Reduces the number of direct connections to the database instance.
  - Improves database efficiency by reducing CPU, memory usage, and connection overhead.

---

## 2. Why Use RDS Proxy?

- **Connection Pooling:**
  - Instead of every application opening a connection to the RDS instance:
    - Applications connect to the **RDS Proxy**.
    - Proxy pools connections → fewer direct connections to the database.
  - **Benefits:**
    - Reduces stress on database resources (CPU, RAM).
    - Minimizes open connections and timeouts.

- **Failover Handling:**
  - RDS Proxy is **highly available** across multiple AZs.
  - Automatically handles failover from primary to standby database instance.
  - Reduces failover time by up to **66%** for both RDS and Aurora.
  - Applications don’t need to manage failover logic—they just connect to the proxy.

- **Serverless & Auto-scaling:**
  - Fully managed, scales automatically with workload.
  - No capacity planning required.

---

## 3. Supported Databases

- **Engines Supported:**
  - MySQL
  - PostgreSQL
  - MariaDB
  - Microsoft SQL Server
  - Aurora MySQL
  - Aurora PostgreSQL
- **Code Changes:** Not required in the application—just point your app to the RDS Proxy endpoint.

---

## 4. Security Features

- **IAM Authentication:**
  - Enforces IAM authentication for database access.
  - Credentials can be securely stored in **AWS Secrets Manager**.

- **VPC-only Access:**
  - RDS Proxy is **never publicly accessible**.
  - Only accessible from within the VPC → enhances security.

---

## 5. Integration with Lambda Functions

- **Problem without Proxy:**
  - Lambda functions can scale quickly (hundreds or thousands of instances).
  - Each function opens a direct connection → can overwhelm database with open connections → timeouts and failures.

- **Solution with RDS Proxy:**
  - Lambda functions connect to RDS Proxy.
  - Proxy pools connections → fewer direct connections to the database instance.
  - Handles rapid scaling of Lambda functions efficiently.

---

## 6. Summary

| Feature                     | RDS Proxy Details                                           |
|-------------------------------|------------------------------------------------------------|
| Primary Function             | Connection pooling and failover handling                  |
| Failover Improvement         | Reduces failover time by up to 66%                        |
| Database Engines Supported   | MySQL, PostgreSQL, MariaDB, SQL Server, Aurora MySQL/PostgreSQL |
| Security                     | IAM authentication + VPC-only access                     |
| Auto-scaling                 | Fully managed, serverless, scales automatically          |
| Use Case                     | Applications with many connections, e.g., Lambda functions |
| Application Code Change      | Not required                                              |
