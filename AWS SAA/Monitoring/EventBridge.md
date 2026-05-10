## What is Amazon EventBridge?  
  
Amazon EventBridge (formerly **CloudWatch Events**) is a **serverless event bus** that lets you:  
  
- React to events in AWS services  
- Schedule tasks (cron jobs)  
- Route events to different targets automatically  
  
Think of it as a **central event routing system** in AWS  
  
---  
  
## Core Idea  
  
EventBridge works like this:  
1. An event happens (AWS service, app, schedule, partner system)  
2. EventBridge captures it  
3. A rule filters it  
4. The event is sent to a target  
  
---  
  
## Types of Events  
  
### 1. AWS Service Events (Default Event Bus)  
Events from AWS services like:  
- EC2 (start/stop/terminate)  
- S3 (object upload/delete)  
- CodeBuild (build success/failure)  
- IAM (root login detection)  
- CloudTrail (API calls)  
  
---  
  
### 2. Scheduled Events (Cron Jobs)  
You can schedule tasks like:  
- Every 5 minutes  
- Every hour  
- Every Monday at 8 AM  
- First day of each month  
  
Used for automation (Lambda, backups, reports, etc.)  
  
---  
  
### 3. SaaS Partner Events (Partner Event Bus)  
Events from third-party tools like:  
- Datadog  
- Zendesk  
- Auth0  
External systems push events into AWS  
  
---  
  
### 4. Custom Events (Custom Event Bus)  
Your own applications can send custom events:  
  
- Order created  
- User registered  
- Payment completed  
  
---  
  
## Event Rules  
  
Rules define:  
  
- Which events to capture (filters)  
- Where to send them (targets)  
  
### Filtering examples:  
- By service (S3 only)  
- By bucket name  
- By event type (upload, delete)  
- By pattern (JSON-based rules)  
  
---  
  
## Event Structure  
  
Events are JSON documents containing:  
  
- Event time  
- Source service  
- Resource ID  
- Region  
- User info  
- Action performed  
  
---  
  
## Targets (Destinations)  
  
EventBridge can send events to:  
  
- Lambda functions  
- SNS (notifications)  
- SQS (queues)  
- ECS tasks  
- Step Functions  
- Kinesis streams  
- CodePipeline / CodeBuild  
- AWS Batch  
- EC2 actions (start/stop/reboot)  
- SSM Automation  
  
Extremely powerful integration layer  
  
---  
  
## EventBridge Bus Types  
  
### 1. Default Event Bus  
- AWS service events  
- Most common  
  
### 2. Partner Event Bus  
- SaaS integrations  
  
### 3. Custom Event Bus  
- Your own application events  
  
---  
  
## Cross-Account Event Sharing  
  
- You can send events between AWS accounts  
- Controlled using **resource-based policies**  
- Useful for centralized event processing  
  
---  
  
## Event Archive & Replay  
  
EventBridge can:  
### Archive events  
- Store events for later use  
- Retention: configurable (days → indefinite)  
  
### Replay events  
- Re-run past events  
- Useful for debugging or fixing bugs  
  
---  
  
## Schema Registry  
  
EventBridge can automatically:  
  
- Detect event structure (schema)  
- Store schema versions  
- Generate code bindings  
  
Helps developers understand event format in advance  
  
---  
  
## Key Features Summary  
  
- Serverless event routing system  
- Real-time + scheduled events  
- Supports AWS, SaaS, and custom sources  
- Highly scalable and fully managed  
- Powerful filtering and routing rules  
  
---  
  
## Key Points 🧠  
  
- EventBridge = **CloudWatch Events (old name)**  
- Use it for:  
- Event-driven architecture  
- Scheduling cron jobs  
- AWS service integrations  
- Supports:  
- Default, Partner, Custom buses  
- Targets include:  
- Lambda, SNS, SQS, Step Functions  
- CloudTrail + EventBridge = **monitor API calls**  
- Archive + Replay = **debugging production issues**  
  
---  
  
## Summary  
  
EventBridge is AWS’s **central event routing service** that enables:  
  
- Event-driven automation  
- System decoupling  
- Real-time integrations across AWS and external systems  
  
If something happens anywhere in AWS, EventBridge can react to it.