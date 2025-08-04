
>[!note]- Post-Processing
>## Key Insights and Information from the AWS SNS Transcript:
>
>**What is SNS?**
>
>* Simple Notification Service (SNS) is a highly available, durable, and secure pub-sub messaging service on AWS.
>* It's publicly accessible, meaning it can be reached from anywhere with network connectivity to public AWS endpoints.
>* SNS coordinates the sending and delivery of messages (payloads up to 256KB) to various subscribers.
>
>**SNS Architecture:**
>
>* **Topics:** The core entity in SNS, where messages are controlled and configured.
>* **Publishers:** Entities (APIs, CloudWatch, EC2, etc.) that send messages to a topic.
>* **Subscribers:** Entities (HTTP endpoints, email addresses, SQS queues, Lambda functions, mobile push notifications) that receive messages from a topic. 
>    * Subscribers can be configured with filters to receive only relevant messages.
>* **Fan-out Architecture:** A single SNS topic can have multiple SQS queues as subscribers, allowing for distributing a single message to multiple related workloads.
>
>**SNS Functionality:**
>
>* **Delivery Status:**  Supports confirmation of message delivery status for certain subscriber types (HTTP/HTTPS endpoints, Lambda, SQS).
>* **Delivery Retry:**  Ensures reliable message delivery with retry mechanisms.
>* **High Availability and Scalability:**  Regionally resilient, scalable within a region, and highly available even with availability zone failures.
>* **Server-Side Encryption (SSE):**  Allows for on-disk encryption of data stored by SNS.
>* **Cross-Account Access:**  Topics can be used across AWS accounts with resource policies (topic policies) controlling access permissions.
>
>**Importance of SNS:**
>
>* Foundational service for developing application architectures within AWS.
>* Extensively used in various AWS products and services (CloudWatch, CloudFormation, Auto-Scaling groups).
>* Understanding SNS architecture is crucial for AWS certification exams and practical project deployments.
>
>
>
>This summary provides a concise overview of the key concepts and features of AWS SNS as discussed in the transcript.
>

- Public AWS service - network connectivity with Public Endpoint
- Coordinates the sending and delivery of messages
- Messages are <= 256KB payloads
- SNS Topics are the base entity of SNS - permissions and configuration
- A publisher sends message to a TOPIC
- TOPICS have Subscribers which receive messages
	- like HTTP/s, Email, SQS, Mobile Push, SMS Messages and Lambda
- SNS used across AWS for notifications (like CloudWatch and CloudFormation)
- AWS services and API (publishers) can send SNS messages into a topic, and then consumers can receive these messages
- We can add a filter so that consumers can only see relevant messages from the topic
- Fanout architecture = SNS topic with multiple SQS queues as subscriber
- Delivery Status (HTTP, Lambda, SQS, ...)
- Delivery Retries (reliable delivery)
- HA and Scalable (Region)
- Server Side Encryption (SSE)
- Cross-Account via TOPIC Policy