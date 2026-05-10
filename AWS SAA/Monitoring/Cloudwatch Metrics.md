## 1. Overview  
Amazon CloudWatch is a monitoring and observability service that collects **metrics, logs, and events** from AWS resources and applications.  
  
A **metric** is a time-ordered set of data points that represents a variable you want to monitor (e.g., CPU usage, disk reads, network traffic).  
  
---  
  
## 2. CloudWatch Metrics Basics  
  
### What metrics are  
- A metric is a **time-based value** (always includes a timestamp)  
- Examples:  
  - EC2: `CPUUtilization`, `NetworkIn`, `DiskReadOps`  
  - S3: `BucketSizeBytes`, `NumberOfObjects`  
  
### Key concepts  
  
| Concept | Description |  
|--------|-------------|  
| Namespace | Logical container for metrics (e.g., `AWS/EC2`, `AWS/S3`) |  
| Metric | The variable being measured (e.g., CPU usage) |  
| Dimension | Attribute that identifies the metric (e.g., InstanceId) |  
| Timestamp | Each metric data point is time-based |  
  
---  
  
## 3. Dimensions  
  
- Dimensions are **filters / labels** for metrics  
- Used to uniquely identify a metric  
- Example:  
  - `InstanceId = i-123456`  
  - `Environment = prod`  
  
✔ Up to **30 dimensions per metric**  
  
---  
  
## 4. Dashboards  
  
- CloudWatch allows you to create **dashboards**  
- Dashboards help visualize multiple metrics in one place  
- Useful for:  
  - System health monitoring  
  - Performance tracking  
  - Business KPIs  
  
---  
  
## 5. Custom Metrics  
  
### What they are  
- Metrics you define yourself (not AWS default ones)  
  
### Use cases  
- Memory usage on EC2 (not provided by default)  
- Application-specific metrics (e.g., "orders per second")  
  
---  
  
## 6. Metric Streaming  
  
CloudWatch metrics can be streamed in near real-time to external systems.  
  
### Destinations:  
- Amazon Kinesis Data Firehose  
- Amazon S3 → Athena / Redshift / OpenSearch  
- Third-party tools:  
  - Datadog  
  - New Relic  
  - Splunk  
  - Dynatrace  
  
### Benefits:  
- Near real-time analytics  
- Centralized monitoring across systems  
  
---  
  
## 7. Data Collection Frequency  
  
| Monitoring Type | Frequency |  
|----------------|----------|  
| Basic monitoring | 5 minutes |  
| Detailed monitoring | 1 minute |  
  
---  
  
## 8. Key Features Summary  
  
- Fully managed monitoring service  
- Time-based metrics for AWS services  
- Supports custom metrics  
- Visualization through dashboards  
- Supports streaming to analytics systems  
- Filtering by region, namespace, and dimension  
  
---  
  
## 9. Important Exam Points  
  
- Metrics are **time-based**  
- Each AWS service has its own **namespace**  
- Dimensions help uniquely identify metrics  
- Custom metrics require manual publishing  
- Detailed monitoring = 1-minute intervals (paid feature)  
  
---  
  
## 10. Simple Mental Model  
AWS Service → Namespace → Metric → Dimension → Timestamped Data
  
Example:
EC2 → AWS/EC2 → CPUUtilization → InstanceId=i-123 → time series values
