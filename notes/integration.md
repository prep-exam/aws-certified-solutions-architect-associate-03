Here’s the information on AWS Application Integration services formatted in Markdown:

---

### <span style="color:blue">Application Integration</span>

#### <span style="color:green">SQS (Amazon Simple Queue Service)</span>

- **Type:** Fully managed message queuing service
- **Specifications:**
  - **Standard Queue:**
    - Unlimited number of messages
    - Default retention period: 4 days, max: 14 days
    - Maximum message size: 256KB
    - Unlimited throughput and low latency (<10ms for publish and receive)
    - Potential for duplicate messages (At-least-once delivery)
    - Potential for out-of-order messages (best-effort ordering)
  
- **Operations:**
  - Messages are polled in batches (up to 10 messages) and deleted post-processing. Unprocessed messages remain in the queue and may be processed multiple times.
  - Producers and consumers must have permissions to send and receive messages (Queue Access Policy).
  - **Message Visibility Timeout:** When a message is being processed, it becomes invisible to other consumers for the timeout period.
  - **Dead-Letter Queue (DLQ):** Stores messages that fail to process multiple times and exceed the maximum receives threshold.
  - **Temporary Queue Client:** Implement SQS Request-Response System.
  - **Message Delay:** Messages can be delayed up to 15 minutes. Set using Delivery Delay at the queue level or DelaySeconds parameter at the message level.
  - **Long Polling:** Reduces empty responses by setting ReceiveMessageWaitTimeSeconds to a value greater than zero, allowing Amazon SQS to wait until a message is available.
  - **FIFO Queues:** Guarantees ordering and exactly-once processing with limited throughput (up to 300 msg/s without batching, 3000 msg/s with batching). FIFO queue names must end with `.fifo`. Standard SQS cannot be converted to FIFO SQS.

- **Use Case:**
  - CloudWatch uses a custom metric to monitor `(SQS queue length / Number of EC2 instances)`, triggering ASG to auto scale EC2 instances based on the number of messages in the queue.

#### <span style="color:green">SNS (Amazon Simple Notification Service)</span>

- **Type:** Pub/Sub messaging service
- **Specifications:**
  - **Topics:** Up to 100,000 topics
  - **Subscriptions:** Up to 12,500,000 subscriptions per topic
  - **Subscribers:** Kinesis Data Firehose, SQS, HTTP, HTTPS, Lambda, Email, Email-JSON, SMS Messages, Mobile Notifications
  - **Subscription Filter Policy:** JSON policy for sending filtered messages to specific subscribers.

- **Patterns:**
  - **Fan-Out Pattern:** One SNS topic with multiple SQS subscribers. For example, send all order messages to an SNS topic and route filtered messages based on order status to three different application services using SQS.

#### <span style="color:green">Amazon MQ</span>

- **Type:** Managed message broker service
- **Specification:** Amazon-managed Apache ActiveMQ
- **Use Case:** Migrate existing message brokers using MQTT protocol to AWS.

---

Certainly! Here's a Markdown table comparing the different AWS Application Integration services:

---

### <span style="color:blue">Application Integration Services Comparison</span>

| Feature                         | <span style="color:green">**SQS (Amazon Simple Queue Service)**</span>                                                                                                                                                               | <span style="color:green">**SNS (Amazon Simple Notification Service)**</span>                                                                                                                              | <span style="color:green">**Amazon MQ**</span>                                                                                     |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| **Service Type**                 | Managed Message Queue                                                                                                                                                       | Managed Pub/Sub Messaging Service                                                                                                                                 | Managed Message Broker                                                                                                      |
| **Message Retention**            | Default: 4 days, Max: 14 days                                                                                                                                                 | Not applicable (Messages are pushed to subscribers immediately)                                                                                           | Not applicable                                                                                                              |
| **Message Size**                 | Up to 256KB                                                                                                                                                                | Not applicable (Handled by subscribers)                                                                                                                        | Not applicable                                                                                                              |
| **Throughput**                   | Unlimited throughput and low latency (<10ms)                                                                                                                                 | High throughput and low latency                                                                                                                               | Depends on the broker configuration and instance size                                                                        |
| **Message Ordering**             | Best-effort ordering (Standard Queue)                                                                                                                                        | Not applicable (Messages are published to subscribers without ordering)                                                                                   | Maintains message ordering if configured properly (depends on broker setup)                                                 |
| **Message Duplication**          | Possible (At-least-once delivery)                                                                                                                                           | Not applicable (Message duplication is handled by subscribers)                                                                                             | Managed by the broker                                                                                                      |
| **Visibility Timeout**           | Yes, for preventing other consumers from processing the same message during processing                                                                                     | Not applicable                                                                                                                                                | Not applicable                                                                                                              |
| **Dead-Letter Queue (DLQ)**       | Yes, to handle messages that fail to process                                                                                                                                 | Not applicable                                                                                                                                                | Not applicable                                                                                                              |
| **Message Delay**                | Yes, up to 15 minutes                                                                                                                                                        | Not applicable                                                                                                                                                | Not applicable                                                                                                              |
| **Long Polling**                 | Yes, reduces empty responses by waiting for messages                                                                                                                         | Not applicable                                                                                                                                                | Not applicable                                                                                                              |
| **FIFO Support**                 | Yes, for exactly-once processing and ordering (FIFO queue names must end with `.fifo`)                                                                                     | Not applicable                                                                                                                                                | Not applicable                                                                                                              |
| **Subscriptions**                | Not applicable                                                                                                                                                             | Up to 100,000 topics and 12,500,000 subscriptions per topic                                                                                                 | Not applicable                                                                                                              |
| **Subscription Filters**         | Not applicable                                                                                                                                                             | Yes, allows filtering messages to specific subscribers using JSON policies                                                                                 | Not applicable                                                                                                              |
| **Fan-Out Pattern**              | Not applicable                                                                                                                                                             | Yes, one topic with multiple subscribers, e.g., send filtered messages to different services                                                               | Not applicable                                                                                                              |
| **Integration with Other Services** | Works with Lambda, EC2, and more. Can be used for triggering Lambda functions or EC2 instances.                                                                                 | Works with Lambda, SQS, HTTP, HTTPS, and more. Can trigger Lambda functions or send messages to SQS queues.                                              | Used for integrating with existing message brokers and applications, migrating existing brokers to AWS.                      |
| **Use Case Example**             | Auto-scaling based on SQS queue length and EC2 instance count                                                                                                                | Distributing notifications to multiple services or endpoints                                                                                              | Migrating from existing Apache ActiveMQ brokers to AWS                                                                        |

---

This table outlines the primary differences and features of each service. Let me know if you need any more details or additional comparisons!