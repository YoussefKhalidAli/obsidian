# CloudWatch Agents (EC2 & On-Premises)

## Overview

CloudWatch Agents are installed on EC2 instances or on-premises servers to **send logs and/or metrics to CloudWatch**, since nothing is sent automatically by default.

---

## Why we need CloudWatch Agents

By default:

- No application logs are sent to CloudWatch Logs
- No detailed OS-level metrics (RAM, processes, swap, etc.)

To enable this:

- Install a **CloudWatch Agent** on the server
- Configure it to push logs + metrics

---

## How it works

1. Install agent on EC2 / on-prem server
2. Configure what to collect (logs, metrics)
3. Attach IAM Role (for EC2) allowing CloudWatch access
4. Agent pushes data to CloudWatch

---

## IAM Requirement

EC2 instance must have an IAM Role with permissions like:

- `cloudwatch:PutMetricData`
- `logs:PutLogEvents`
- `logs:CreateLogStream`

---

## Works on:

- EC2 instances
- On-premises servers (VMware, physical servers)
- Any Linux/Windows server

---

## Types of CloudWatch Agents

| Feature       | CloudWatch Logs Agent (Old) | CloudWatch Unified Agent (New)       |
| ------------- | --------------------------- | ------------------------------------ |
| Purpose       | Send logs only              | Send logs + metrics                  |
| Logs          | Yes                         | Yes                                  |
| Metrics       | No                          | Yes                                  |
| OS metrics    | No                          | Yes (RAM, CPU breakdown, disk, etc.) |
| Configuration | Manual                      | Can use SSM Parameter Store          |
| Status        | Deprecated                  | Recommended                          |

---

## Metrics collected by Unified Agent

### CPU Metrics (granular)
- active
- idle
- system
- user
- steal
- guest

### Disk Metrics
- free space
- used space
- disk reads/writes
- IOPS
- bytes transferred

### Memory (RAM)
- free
- used
- cached
- inactive
- total

### Network
- TCP connections
- UDP connections
- packets in/out
- bytes in/out

### Processes
- running
- sleeping
- blocked
- total processes

### Swap
- swap used
- swap free
- usage %

---

## Key Idea
- EC2 default monitoring is **basic**
- Unified Agent gives **deep system-level observability**
- Best choice for production monitoring

---

## Summary
- CloudWatch Agent = bridge between server and CloudWatch
- Unified Agent = best option (logs + full metrics)
- Requires IAM role to publish data
- Works for EC2 + on-prem servers