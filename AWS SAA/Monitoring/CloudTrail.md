## CloudTrail Overview

Amazon CloudTrail provides **governance, compliance, and auditing** for AWS accounts.

- Enabled by default
- Records **all API calls** made in an AWS account
    - AWS Management Console actions
    - AWS CLI / SDK calls
    - AWS service-to-service actions
- Helps answer: **who did what, when, and from where**

### Log Destinations

CloudTrail logs can be delivered to:

- Amazon S3 (long-term storage)
- CloudWatch Logs (real-time monitoring & alerts)

You can configure trails:

- **All regions trail** (recommended for full coverage)
- **Single region trail**

---

## CloudTrail Event Types

### 1. Management Events (default)

Track management operations on AWS resources.

- Always enabled by default
- Includes both:
    - **Read events** (e.g., list users, describe instances)
    - **Write events** (e.g., create/delete resources)

Examples:

- IAM role policy attachment
- EC2 instance creation/deletion
- VPC/subnet changes

---

### 2. Data Events (high volume, optional)

Track object-level or high-frequency operations.

- Not enabled by default
- High volume → can become expensive

Examples:

- S3 object access:
    - GetObject
    - PutObject
    - DeleteObject
- Lambda invocation events

---

### 3. CloudTrail Insights Events

Used for detecting **unusual activity patterns**.

- Must be explicitly enabled (paid feature)
- Detects anomalies such as:
    - Spike in API calls
    - Unusual IAM activity
    - Resource provisioning anomalies

How it works:

- Builds a **baseline of normal activity**
- Detects deviations from baseline
- Generates Insights Events when anomalies occur

---

## CloudTrail Retention

- Default retention: **90 days in CloudTrail console**
- After 90 days, events are removed from the console

For long-term storage:

- Export to **S3 bucket**
- Analyze using **Amazon Athena**

---

## CloudTrail + EventBridge Integration

CloudTrail events can be forwarded to **Amazon EventBridge** for automation.

### Use Cases

Trigger actions based on API calls such as:

- DynamoDB table deletion → send SNS alert
- IAM AssumeRole activity → security notification
- Security Group changes → trigger alert

### Flow

1. API call is made (e.g., DeleteTable)
2. CloudTrail logs the API call
3. EventBridge receives the event
4. EventBridge rule filters specific events
5. Event is sent to a target:
    - SNS (notifications)
    - Lambda (automation)
    - SQS (queueing)

---

## CloudTrail Insights (Deep Dive)

Purpose:

- Detect unusual account activity automatically

Examples of detections:

- Burst of IAM actions
- Unexpected spikes in resource provisioning
- Service limit breaches

Output:

- Insights Events appear in:
    - CloudTrail console
    - EventBridge
    - Optional S3 delivery

---

## Summary

### CloudTrail

- Auditing & governance layer for AWS
- Logs all API activity
- 3 event types:
    - Management Events (default)
    - Data Events (optional, high volume)
    - Insights Events (anomaly detection)

### EventBridge Integration

- Enables real-time reaction to CloudTrail events
- Supports automation via:
    - SNS
    - Lambda
    - SQS
    - Step Functions