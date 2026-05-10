| Feature                     | Amazon SQS                                | Amazon SNS                               | Amazon Kinesis (Data Streams)                             |
| --------------------------- | ----------------------------------------- | ---------------------------------------- | --------------------------------------------------------- |
| **Messaging model**         | Queue (point-to-point)                    | Pub/Sub (fan-out)                        | Streaming (real-time data stream)                         |
| **Data flow direction**     | Producers → Queue → Consumers             | Producer → Topic → Multiple Subscribers  | Producers → Stream → Consumers                            |
| **Consumption pattern**     | Consumers **pull** messages               | SNS **pushes** messages to subscribers   | Consumers usually **pull**, or push via enhanced fan-out  |
| **Message delivery**        | One message processed by one consumer     | One message delivered to all subscribers | Multiple consumers can read same data (depending on mode) |
| **Data persistence**        | Messages persist until consumed or expire | No persistence after delivery attempt    | Data is persisted for replay (1–365 days)                 |
| **Message retention**       | 4 days default, up to 14 days             | No retention (stateless delivery)        | 1–365 days (configurable)                                 |
| **Ordering guarantee**      | Only with FIFO queues                     | No ordering guarantee (standard SNS)     | Ordering per shard (via partition key)                    |
| **Throughput scaling**      | Unlimited (managed service)               | Highly scalable (no provisioning)        | Requires shard provisioning or on-demand mode             |
| **Scaling model**           | Auto scaling (no setup required)          | Auto scaling                             | Manual shards or automatic on-demand scaling              |
| **Duplicate messages**      | Possible (at-least-once delivery)         | Possible (depends on subscriber)         | Possible depending on processing                          |
| **Use case**                | Decoupling applications, task queues      | Notifications, event broadcasting        | Real-time analytics, streaming data pipelines             |
| **Fan-out capability**      | Indirect (via SNS + SQS)                  | Native fan-out to many subscribers       | Limited (needs Kinesis or Firehose integration)           |
| **Consumer responsibility** | Must delete message after processing      | No deletion (push model)                 | Consumers manage checkpoints/offsets                      |
| **Replay capability**       | No                                        | No                                       | Yes (data replay supported)                               |
| **Ordering level**          | FIFO queue (optional)                     | None (except SNS FIFO topics)            | Shard-level ordering                                      |
| **Capacity control**        | Fully managed                             | Fully managed                            | Shards (provisioned) or on-demand                         |
| **Enhanced mode**           | FIFO queues available                     | FIFO topics available                    | Enhanced fan-out (push per consumer)                      |