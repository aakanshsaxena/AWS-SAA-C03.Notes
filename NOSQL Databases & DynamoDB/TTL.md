> [!note]- AI
> #### DynamoDB Time to Live (TTL)
> - **Purpose:** The TTL feature allows you to define a timestamp on an item to determine when it is no longer needed. DynamoDB then automatically deletes the item from your table and indexes shortly after the expiration timestamp, without any extra cost or performance impact on your table.
> - **TTL Configuration:** To use TTL, you must:
>     1. Enable TTL on the table.
>     2. Specify a single attribute name (e.g., `ttl_expiration`) that DynamoDB will use to track the expiration date.
>     3. For each item you want to expire, set the value of this attribute to a numerical timestamp in **seconds since the Unix epoch (January 1, 1970)**.
> - **Deletion Process:**
>     - **Expiration:** When an item's TTL timestamp is in the past, it is considered expired. Expired items are still queryable and scannable.
>     - **Deletion:** A background process runs continuously on every table partition to find and delete expired items. This process uses a table's spare capacity and does not consume provisioned throughput. The deletion is not instantaneous and can take up to a few days.
>     - **Deletion Event:** The deletion of an item by TTL is a system-level `DELETE` event. This event can be captured by a DynamoDB Stream.
> #### TTL and Streams Integration
> - **Capturing Events:** When TTL is enabled and a DynamoDB Stream is configured on the table, a `REMOVE` event is written to the stream whenever an item is deleted by the TTL process. This event contains the old image of the item that was deleted.
> - **TTL Processors Stream Configuration:** This refers to the architectural pattern of configuring a Lambda function to be invoked by a DynamoDB Stream. This Lambda function acts as a **TTL processor**, which can perform "housekeeping" tasks in response to a TTL deletion event. For example, the Lambda function could archive the deleted item to an S3 bucket or send a notification.
> - **Benefits:** This event-driven architecture is highly efficient and avoids the need for manual cleanup scripts or costly cron jobs. It is ideal for cleaning up stale data, managing sessions, or enforcing regulatory data retention policies.
> #### Definitions
> - **Expired Items in TTL context:** Items that have a `TTL` attribute value that is less than the current Unix epoch time. These items are marked for deletion by a background process but may still be present in the table and appear in read, query, and scan operations until they are permanently deleted.
> - **Streams Configured on the table:** This refers to enabling a DynamoDB Stream, which is an ordered sequence of all item-level modifications. The stream captures changes (inserts, updates, and deletes, including TTL deletions) and stores them for up to 24 hours.
> - **TTL Processors Stream Configuration:** The architectural pattern of configuring a consumer (such as an AWS Lambda function) to read and process `REMOVE` events from a DynamoDB Stream. This allows you to perform custom actions, such as archiving data or sending notifications, whenever an item is automatically deleted by TTL.
> - **Table Auditing:** The process of monitoring and recording database activities to ensure data integrity, detect suspicious activity, and maintain compliance. With DynamoDB, this can be implemented by enabling `CloudTrail` data events or by using `DynamoDB Streams` to capture and log every change made to items in a table.

- Timestamp for automatic delete of items
- When TTL is enabled on a table a specific attribute is selected for TTL
- Per-partition process periodically runs, checking the current time (in seconds since epoch) to the value in the TTL attribute
- Items where the TTL attribute is older than the current time are set to expire
- Another per-partition background process scans for expired item and removes them from table and indexes and a delete is added to streams if enabled
- A stream of TTL deletions can be enabled (24hr window)