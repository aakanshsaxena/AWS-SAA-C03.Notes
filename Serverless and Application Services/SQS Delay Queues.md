
>[!note]- Post-Processing
>## Key Insights and Information from the SQS Delay Queues Lesson:
>
>**What are Delay Queues?**
>
>* Delay queues are an SQS feature that allows you to postpone the delivery of messages to consumers.
>* Messages added to a delay queue are initially hidden ("invisible") for a specified duration (delay seconds).
>* This delay period is configurable, ranging from 0 seconds to 15 minutes.
>* Once the delay expires, the message becomes visible and available for consumers to process.
>
>**How are Delay Queues Different from Visibility Timeouts?**
>
>* **Visibility Timeout:**
>    * Applies *after* a message is received from the queue.
>    * Hides the message from further receives for a specified duration (default 30 seconds, up to 12 hours).
>    * Used for automatic reprocessing of messages that fail during processing.
>* **Delay Queue:**
>    * Hides messages *before* they are available for consumption.
>    * Delay is set at the queue level (or per message using timers, with a maximum of 15 minutes).
>    * Used to introduce a deliberate delay in message processing.
>
>**Use Cases:**
>
>* **Delay Queues:**
>    * Scheduling tasks to be executed after a certain time.
>    * Implementing "cooldown" periods between actions triggered by user events.
>* **Visibility Timeouts:**
>    * Ensuring reliable message processing by automatically retrying failed messages.
>
>**Important Notes:**
>
>* Message timers for delay configuration are not supported on FIFO queues.
>
>
>This summary provides a clear understanding of delay queues and their differences from visibility timeouts, highlighting their distinct functionalities and use cases.
>

VisibilityTimeout
- We already have a message on the queue, when it is received by a consumer, then it enters a VisbilityTimeout where it will either be processed and the message deleted, or there is some failure, the visbilityTimeout times out and then the message reappears on queue
- We can change the message visibility between 0 seconds and 12 hours, either on queue or per-message
- This allows for error handling and reprocessing
Delay Queues
- Meanwhile, delay queues mean we want there to be a delay when the message is added to queue for it to be invisible.
- So we don't want any consumers to receive the message for a set amount of time, and after our delay queue is over the message will be added to the queue.
- The message is invisble for DelaySeconds which has a min of 0, and a max of 15 minutes
- We can set message times per-message which overrides any queue setting. 
- Delay queues are not supported on FIFO Queues on SQS
