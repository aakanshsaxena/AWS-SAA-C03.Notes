
>[!note]- Post-Processing
>## Key Insights and Information from the SQS Lesson:
>
>**What is SQS?**
>
>* Simple Queue Service (SQS) is a managed message queuing service offered by AbleUS.
>* It's publicly accessible and can be used within private VPCs with connectivity.
>* SQS is highly available and performant by design.
>
>**Types of Queues:**
>
>* **Standard Queues:** Best effort order delivery, messages might be received out of order.
>* **FIFO Queues:** Guarantee message order.  
>
>**Message Size and Dead Letter Queues:**
>
>* Messages can be up to 256 kilobytes.
>* Larger data can be stored elsewhere (e.g., S3) and linked within the message.
>* Dead Letter Queues handle problematic messages (e.g., those repeatedly failed).
>
>**Architectural Benefits:**
>
>* **Decoupling:** Separates application components, allowing them to work independently.
>* **Scaling:** Auto-scaling groups can scale based on queue length, enabling dynamic workload management.
>* **Fault Tolerance:** Visibility timeout ensures messages are reprocessed if a client fails.
>
>**Example Architectures:**
>
>* **Basic Worker Pool:**
>    * Web application adds messages to SQS queue.
>    * Worker pool auto-scales based on queue length.
>    * Workers process messages, retrieve data from S3, perform tasks, and delete messages.
>* **Fanout Architecture (SNS & SQS):**
>    * One SNS topic receives an event (e.g., object upload to S3).
>    * Multiple SQS queues subscribe to the topic, each handling a specific task (e.g., different video sizes).
>    * Auto-scaling groups for each queue scale independently based on workload.
>
>**Exam Tip:**
>
>* **Fanout architecture** is a key concept for the exam. Remember the use of SNS topics and multiple SQS queues for independent scaling and processing.
>
>
>
>Let me know if you have any other questions about the transcript!
>

>[!note]- Post-Processing
>## Key Insights and Information about SQS from the Transcript:
>
>**Types of Queues:**
>
>* **Standard Queues:**
>    * Like a multi-lane highway - high scalability.
>    * Guarantee at least once delivery.
>    * No order guarantee, messages can be delivered out of order and duplicates are possible.
>* **FIFO Queues:**
>    * Like a single-lane road - limited scalability.
>    * Guarantee exactly once delivery and message order (first in, first out).
>    * Performance: 3000 messages/second with batching, 300 messages/second without.
>
>**SQS Specifics:**
>
>* **Requests vs. Messages:**
>    * A request is a single interaction with SQS.
>    * One request can retrieve 0-10 messages (up to 64KB total).
>* **Polling Methods:**
>    * **Short Polling:**
>        * Consumes a request even if no messages are available.
>        * Inefficient for keeping queues near empty.
>    * **Long Polling:**
>        * Waits for messages up to 20 seconds.
>        * More efficient, uses fewer requests.
>* **Cost Considerations:**
>    * SQS is less cost-effective with frequent short polling.
>* **Data Retention:**
>    * Messages can live in a queue for up to 14 days.
>* **Encryption:**
>    * **Encryption at Rest:** Server-side encryption using KMS.
>    * **Encryption in Transit:** Data is encrypted by default.
>
>**Access Control:**
>
>* **Identity Policies:** Control access from within the same account.
>* **Queue Policies:** Control access from external accounts.
>    * Act like resource policies used for S3 buckets or SQS topics.
>
>
>
>**Overall:**
>
>The transcript emphasizes the importance of understanding the differences between standard and FIFO queues in SQS. It highlights the efficiency benefits of long polling over short polling and provides details about data retention, encryption, and access control mechanisms within SQS.
>

- Public, fully managed, HA queues - standard or FIFO (FIFO guarantees order)
- Messages up to 256KB in size, you can provide a link to a S3 bucket for larger data
- Received messages are hidden (VisbilityTimeout) and then either reappear (retry) or explicitly deleted
- Dead-letter queues can be used for problem messages
- ASGs can scale and Lambdas invoke based on queue length
- Standard = at-least-once, FIFO = exactly-once
- FIFO - 3,000 msg/second with batching or up to 300 messages per second without
- Billed for SQS based on requests (1 request = 1-10 messages up to 64KB total)
- We can use either short term or long polling.
	- Ideally, use long polling because each request from short polling is instant and if we don't have any messages in queues we are charged still for the request and we would need to keep short polling going -> higher costs
	- Long polling has a waitTimeSeconds before we access the queue -> less requests -> less cost
- Encryption at rest and in transit is through KMS
- Access to queues can be through roles or queue policy
CatTube Architecture
- We can have an ASG for the web pool (any web requests), that uploads the original media file to our master S3 bucket and then creates a SNS topic. From here we can create SQS queues for each resolution that the video needs to be transcoded to, and then have ASG's for each resolution before sending them back to our transcoded S3 bucket and to the user.




