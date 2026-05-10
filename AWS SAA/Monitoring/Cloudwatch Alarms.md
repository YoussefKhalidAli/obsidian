# CloudWatch Alarms

## Overview

CloudWatch Alarms monitor **metrics and trigger actions** when thresholds are breached.

They are used for:

- Notifications
- Auto-scaling actions
- EC2 recovery actions

---

## Alarm States

|State|Meaning|
|---|---|
|**OK**|Metric is within threshold (no issue)|
|**INSUFFICIENT_DATA**|Not enough data to evaluate alarm|
|**ALARM**|Threshold has been breached|

---

## Key Concepts

### Period

- Time window used to evaluate metric
- Can be:
    - 10 seconds (high-resolution metrics)
    - 30 seconds
    - 60+ seconds (default)
- Used for averaging, min/max, sampling, etc.

---

## Alarm Targets (Actions)

CloudWatch alarms can trigger:

### EC2 Actions

- Stop instance
- Terminate instance
- Reboot instance
- Recover instance

---

### Auto Scaling Actions

- Scale out (add instances)
- Scale in (remove instances)

---

### SNS Notifications

- Send alert to Amazon SNS
- SNS can trigger:
    - Lambda functions
    - Email / SMS
    - HTTP endpoints

---

## Composite Alarms

### Definition

A **composite alarm** combines multiple alarms into one logical condition.

Instead of relying on one metric → you combine multiple alarms.

---

### Logic Supported

- AND
- OR

### Example

|Alarm|Metric|
|---|---|
|Alarm A|CPU utilization|
|Alarm B|Disk IOPS|

### Composite rule:

- Trigger only if:
    - CPU is HIGH **AND**
    - IOPS is HIGH

OR

- CPU HIGH AND Network LOW (custom logic)

### Why composite alarms are useful

- Reduces alarm noise
- Avoids false positives
- Allows advanced logic

---

## EC2 Instance Recovery Alarm

### Monitors:

- **Status Check (Instance-level)** → OS / VM health
- **System Status Check** → underlying hardware

---

### What happens on recovery:
- EC2 instance is moved to healthy hardware
- Keeps:
    - Private IP
    - Public IP
    - Elastic IP
    - Metadata
    - Placement group

### Optional:

- Send SNS notification when recovery happens

---

## CloudWatch Logs + Alarms Integration

You can create alarms from:

- Log Metric Filters (e.g., "ERROR" count)

### Example:

If logs contain too many `"ERROR"` entries:  
→ Trigger CloudWatch Alarm  
→ Send SNS notification

---

## Testing Alarms

### CLI command:

aws cloudwatch set-alarm-state

### Use case:

- Force alarm into ALARM state
- Test notifications & automation
- Validate infrastructure reactions

---

## Summary

- Alarms = metric-based triggers
- 3 states: OK, INSUFFICIENT_DATA, ALARM
- Can trigger:
    - EC2 actions
    - Auto Scaling
    - SNS notifications
- Composite alarms = multi-condition logic
- Can integrate with logs + metric filters
- Can be manually tested via CLI