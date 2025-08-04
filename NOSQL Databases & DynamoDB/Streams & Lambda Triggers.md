> [!note]- AI
> #### DynamoDB Streams and View Types
> - **Purpose:** A DynamoDB Stream is an ordered, time-stamped sequence of item-level modifications in a DynamoDB table. It captures all changes, including item inserts, updates, and deletes.
> - **Stream View Types:** When you enable a stream on a table, you must specify a "view type" that determines what information is written to the stream record for each modification:
>     - **`KEYS_ONLY`:** Only the primary key attributes of the item that was modified are captured. This is the simplest and most lightweight view.
>     - **`NEW_IMAGE`:** The entire item as it appears after the modification. This view is useful for seeing the final state of an item after an update or insert.
>     - **`OLD_IMAGE`:** The entire item as it appeared before the modification. This view is useful for seeing the state of an item before a change or a delete.
>     - **`NEW_AND_OLD_IMAGES`:** Both the old and new images of the item are captured. This is the most comprehensive view and allows you to see the exact changes that were made to an item's attributes by comparing the two images.
> #### DynamoDB Streams and Trigger Architecture
> - **Event-Driven Architecture:** DynamoDB Streams is a foundational component for building an event-driven, serverless architecture with DynamoDB. Instead of continuously polling for changes, you can configure the stream to act as a trigger for a compute service.
> - **AWS Lambda Integration:** The primary compute service used for this architecture is **AWS Lambda**. When a record is added to a DynamoDB stream, it acts as an event source that automatically invokes a specified Lambda function. The Lambda function receives the stream records and can perform any custom logic you define.
> - **Triggers:** This integration of a DynamoDB stream with a Lambda function is what is known as a **DynamoDB trigger**. It provides a mechanism to automatically take action in response to data changes in your table.
> #### Use Cases and Benefits
> - **Real-Time Analytics:** Streams and triggers can be used to send all data changes to a data lake or another analytics platform in real time, enabling real-time reporting and dashboards.
> - **Data Aggregation:** You can use a trigger to aggregate data in a separate table. For example, if a table stores individual product reviews, a trigger could update a summary table with the average rating and total review count.
> - **Notifications and Messaging:** Streams are ideal for messaging applications. For example, in a **group chat application**, a trigger can be used to send push notifications to other members whenever a new message item is added to the chat table, avoiding inefficient polling.
> - **Cost Efficiency:** This architecture is highly cost-effective because the Lambda function is only invoked when a data change actually occurs, so you only pay for the compute resources you use.
> #### Definitions
> - **AWS Lambda:** A serverless, event-driven compute service that runs code in response to events and automatically manages the underlying compute resources.
> - **AWS Lambda function invocation with DynamoDB streams:** The process where a new record in a DynamoDB stream automatically triggers the execution of a designated AWS Lambda function, passing the stream record as event data to the function.
> - **Group Chat Application:** A software application that enables multiple users to send and receive messages in a shared channel. It often relies on a real-time data store like DynamoDB to store chat messages.
> - **DynamoDB Streams and Trigger Architecture:** A serverless, event-driven architectural pattern where a DynamoDB stream captures data changes from a table and acts as a trigger to invoke an AWS Lambda function, which then performs custom actions based on the stream records.

- Time ordered list of ITEM CHANGES in a table
- 24-hour rolling window
- Enabled on a per table basis
- Records ISNERTSA< UPDATES AND DELETES
- Different view
View Types
- Keys_Only: Only partition keys
- New_Image: What data looks like now
- Old_Image: What data looked like before
- NEW_AND_OLD_IMAGES: Complete visibility of before and after
Trigger Concepts
- ITEM changes generate an event which contains the data which changed
- Action is taken using that data
- AWS = Streams + Lambda to trigger notifications
- Reporting & Analytics
- Aggregation, Messaging or Notification
Architecture
- Item change occurs in a table with streams enabled, stream record is added onto stream, Lambda function is invoked when stream event occurs. Function is passed the view data as an event to Lambda function