> [!note]- AI
> #### Query vs. Scan: Core Differences
> - **Query:** This is the most efficient way to retrieve data from a DynamoDB table. It requires you to provide a specific **partition key value**. You can optionally refine the results by providing a condition on the **sort key**, such as `equals`, `begins with`, or `between` a range of values. A query operation is highly targeted and consumes RCUs only for the items that match the key condition in a single partition.
> - **Scan:** This is the least efficient and most flexible operation. A `Scan` operation reads **every single item** in the table or a secondary index. It does not require a primary key value and can be used to filter on any attribute. Because it reads the entire table, it is much slower and more expensive than a query, especially on large tables.
> #### Addressing Scan Objections
> - **Objection: Scan is expensive from a capacity perspective.**
>     - **Response:** This objection is correct. A `Scan` operation is highly inefficient because it must consume read capacity to read every item in the table to find a match. This makes it a very expensive operation in terms of consumed capacity units and can quickly use up all the provisioned throughput for your table. For this reason, a `Scan` should be avoided for high-traffic or latency-sensitive applications.
> - **Objection: Scan consumes entire table capacity despite filtering.**
>     - **Response:** This objection is also correct. The `FilterExpression` is a post-processing step. DynamoDB first reads every single item from the table, consuming the full read capacity for all items. It then applies the filter to the retrieved items and discards any that do not match. The capacity consumed is based on the total number of items read, not the number of items returned. This is why a `Scan` is so costly and should be used with caution.
> #### Definitions
> - **Scan Operation:** A DynamoDB `Scan` operation returns one or more items and their attributes by accessing every item in a table or a secondary index. It is a full table read that does not require any specific key values.
> - **Scan Operation Attribute Filtering:** This refers to the process of applying a `FilterExpression` to a `Scan` operation. The filter is applied after the operation has read all the items from the table, to narrow down the final result set. The filtering process itself does not consume additional RCUs, but because it happens after the full table read, the entire read capacity of the table is still consumed.
> #### Best Practices
> - **Prefer Query:** Always use a `Query` operation over a `Scan` whenever possible. Design your table schemas and indexes (Global Secondary Indexes) based on your access patterns so that you can use a `Query` for your most frequent lookups.
> - **Scan Use Cases:** A `Scan` is best used for infrequent, administrative tasks on small tables, such as exporting data or running reports, where its inefficiency is not a major concern.
> - **Performance:** You can improve the performance of a `Scan` on a large table by using a **parallel scan**, where you divide the table into multiple segments and scan them concurrently. However, this will consume even more capacity from your table.

Reading and Writing
- On-demand = unknown, unpredictable, low admin
	- pay per million R or W, but can be almost 5x cost as provisioned
- Provisioned= RCU and WCU set on a per table basis
	- every operation consumes at least 1 RCU/WCU
	- 1 RCU is 1x4KB read operation per second 
	- 1 WCU is 1x1KB write operations per second
- Every table has a RCU and WCU burst pool (300 seconds) - relying on this is dangerous
Query
- Start with one partition key value
- Query accepts a single PK value and optionally a SK or range. Capacity consumed is the size of all returned items. Further filtering discards data, capacity is still consumed. Can only query on PK or PK and SK
- Always more efficient to pull back more data in one query rather than two separate ones
	- If we retrieve an item that's 2.5K and 1.5K = 4K then it would use 1 RCU
	- Or if we retrieved these two items separately then it would use 1 RCU per operation
- Can query specific attributes you want to return, still charged for whole item
Scan
- Least efficient operation within DynamoDB, but most flexible
- SCAN moves through a table consuming the capacity of every item. You have complete control on what data is selected, any attributes can be used and any filters applied but SCAN consumes capacity for every ITEM scanned through
	- Billed for every read, which is reading every single item in the table.