
>[!note]- Post-Processing
>## Key Insights and Information from the SQS Queue Transcript:
>
>**1.  FIFO vs. Standard SQS Queues:**
>
>*   **FIFO (First-In, First-Out):** 
>    *   Like a single-lane highway, messages are processed in the order they arrive.
>    *   Performance is limited to 300 messages per second (without batching) and 3000 per second (with batching).
>    *   Guarantees exactly once processing, meaning each message is delivered only once.
>    *   Requires a "FIFO" suffix in the queue name.
>    *   **Ideal Use Cases:** Workflow-based order processing, command ordering, sequential calculations.
>
>*   **Standard:**
>    *   Like a multi-lane highway, messages can be processed concurrently.
>    *   Handles a theoretically infinite number of transactions per second.
>    *   No rigid message ordering guarantee (best-effort).
>    *   Guarantees at least once message delivery (messages may be delivered multiple times).
>    *   **Ideal Use Cases:** Decoupling application components, batch processing.
>
>**2. Performance Trade-offs:**
>
>*   FIFO queues prioritize message order over high throughput.
>*   Standard queues prioritize high throughput over strict message order.
>
>**3.  Additional Points:**
>
>*   High throughput mode for FIFO queues is currently in preview.
>*   Applications using standard queues must be able to handle potential duplicate message deliveries.
>
>
>This information should help you understand the key differences between standard and FIFO SQS queues and choose the right one for your needs.
>

- We can think of Standard as a multi lane highway while FIFO is a single lane highway
- Standard is scalable to as wide as required, and near unlimited TPS. But, there is no rigid preservation of message order, and there could on occasion be more than one copy of a message
- Standard is best for decoupling, worker pools, batch for future processing
- Meanwhile, FIFO can handle 300 TPS w/o batching, and 3000 TPS with
- It also must have .fifo suffix
- However, message order is strictly preserved (hence FIFO) and duplicates are removed.
- This is better for workflow ordering, command ordering, price adjustments
