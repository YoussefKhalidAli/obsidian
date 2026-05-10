# Amazon EC2 (Elastic Compute Cloud)

Amazon EC2 is a IAAS that provides **virtual servers (instances)** in the cloud to run applications.

---

## 1. EC2 Sizing and Configuration (Overview)

When launching an EC2 instance, you choose basic configuration options:

- **Instance Type** – defines CPU, RAM, and performance  
- **AMI (Amazon Machine Image)** – operating system and preinstalled software  
- **Storage** – EBS (persistent) or Instance Store (temporary)  
- **Networking** – VPC, subnet, IP address  
- **Security** – Security Groups (firewall) and Key Pair (login)  
- **IAM Role** – permissions for the instance to access AWS services  

**Explanation:** These settings define the **capacity, connectivity, and security** of your EC2 instance.

---

## 2. EC2 User Data

User Data is a **script that automatically runs when an EC2 instance boots for the first time**.

### 2.1 Purpose

User Data is used to **automate instance setup** so that servers are ready without manual configuration.

**Explanation:** Instead of logging into the instance and installing software manually, you define everything in a script that runs at launch.

---

### 2.2 How It Works

- You provide a script when launching the EC2 instance  
- The script runs **at boot time**  
- It runs with **root/administrator privileges**  
- By default, it runs **only once on first launch**  
- If the instance is stopped and started again → script does **not run again**  
- Can be configured to run on every boot, but this is **not default behavior**  

**Explanation:** This allows you to fully configure the instance automatically during startup.

---

### 2.3 Supported Script Types

- **Linux** → Bash scripts  
- **Windows** → PowerShell scripts  

---

### 2.4 Common Use Cases

- Install software (e.g., web servers, Docker)  
- Update the OS  
- Download application code from GitHub or S3  
- Start services automatically  
- Configure environment variables or system settings  

**Explanation:** User Data is mainly used for **bootstrapping** (initial setup of the instance).

---

### 2.5 Logging and Debugging

- Output of the script is stored in log files on the instance  
- Useful for troubleshooting if something fails during startup  

---

### 2.6 Important Notes

- Runs with **root privileges** → full system access  
- Should be **idempotent** (safe to run multiple times if needed)  
- Avoid putting **sensitive data** directly in the script  
- Often used with automation tools (e.g., Auto Scaling)

---

## Summary

- EC2 = virtual server in the cloud  
- Configuration defines performance, networking, and security  
- User Data = **automated startup script for instance initialization**  
- Runs once at launch and is used for **bootstrapping servers**