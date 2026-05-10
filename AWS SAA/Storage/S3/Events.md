## 1. What are S3 Event Notifications?  
  
S3 Event Notifications allow you to **automatically react to events happening in an S3 bucket**.  
  
> S3 **pushes events** to other AWS services  
  
---  
  
## 2. Types of Events  
  
Events are triggered when actions happen on objects:  
  
- Object Created (PUT, POST, COPY)  
- Object Removed (DELETE)  
- Object Restored (from Glacier)  
- Replication events  
  
---  
  
## 3. Event Filtering  
  
You can filter events based on:  
-  Prefix (e.g., `images/`)  
-  Suffix (e.g., `.jpg`, `.png`)  
  
 
## 3.1 Use Cases  
  
### Example: Image Processing  
User uploads image → S3 → Event → Lambda → Generate thumbnail
  
Other use cases:  
- Data processing pipelines  
- Log processing  
- Notifications  
- Automation workflows  
   
## 3.2 Event Destinations  
  
S3 can send events to:  

| Service     | Use Case                |
| ----------- | ----------------------- |
| SNS         | Notifications (fan-out) |
| SQS         | Queue processing        |
| Lambda      | Serverless processing   |
| EventBridge | Event filtering         |

## 3.3 Permissions   
S3 does **NOT use IAM roles** to send events.  
  - Instead, you must configure **resource-based policies** on the destination.  
   
### Required Policies  
  
| Destination | Required Policy |  
|------------|----------------|  
| SNS | SNS Topic Policy |  
| SQS | SQS Queue Policy |  
| Lambda | Lambda Resource Policy |  

---  
  
## 4. Event Delivery  
  
- Usually delivered in **seconds**  
- Sometimes may take:  
  - Up to **1 minute or more**  
  
Not guaranteed real-time, but near real-time  
  
---  
  
## 5. Multiple Events  
  
- You can create **multiple event notifications**  
- Each can:  
  - Have different filters  
  - Send to different destinations  

---  

## 6. Key Points  
  
- S3 events = **trigger-based automation**  
- Supported direct targets:  
  - SNS  
  - SQS  
  - Lambda  
- Permissions:  
  - Use **resource-based policies**  
- Filtering:  
  - Prefix & suffix only  
- EventBridge:  
  - Advanced routing  
  - More services  
- Delivery:  
  - Near real-time (not guaranteed instant)  
