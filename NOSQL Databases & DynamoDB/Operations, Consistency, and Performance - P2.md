> [!note]- AI
> #### Why is a Write Capacity Unit less than a Read Capacity Unit?
> A write capacity unit (WCU) is for 1 KB of data, while a read capacity unit (RCU) is for 4 KB of data. This difference in size reflects the fact that a write operation is fundamentally more resource-intensive than a read operation in a distributed database. A single write must be logged and replicated to multiple storage nodes to ensure durability and availability, while a read operation, especially an eventually consistent one, can be fulfilled by a single storage node. The smaller WCU unit size accounts for the higher cost and complexity of a write.
> #### Consistency Models
> - **Strongly Consistent Reads:** This model guarantees that a read operation returns the most up-to-date data, reflecting all completed write operations. This is achieved by having the read request use a single "leader" storage node, which holds the latest version of the data. While this is critical for applications that require immediate data accuracy (e.g., banking transactions), it is less scalable and costs twice as much as an eventually consistent read.
> - **Eventual Consistency:** This is a property of a distributed system where, if no new updates are made to an item, all copies of that item will eventually converge to the same value. In DynamoDB, this typically happens within a second.
> - **Eventually Consistent Reads:** This is the default read model in DynamoDB. Read requests can be fulfilled by any of the storage nodes that hold a copy of the data. This provides higher read throughput, lower latency, and is half the cost of strongly consistent reads. It is a good choice for applications where a slight data lag is acceptable, such as a social media feed or a weather app.
> #### Capacity Unit Calculations
> - **Write Capacity Units (WCU):**
>     - **Calculation:** One WCU provides enough capacity for **one 1 KB write per second**.
>     - **Example:** To write an item that is 2.5 KB in size, you need to divide the item size by the unit size (2.5 KB / 1 KB) and round up. This results in **3 WCUs per write**. If you need to perform 10 writes per second, your total WCU is 3 WCUs per item * 10 writes/second = **30 WCUs**.
> - **Read Capacity Units (RCU):**
>     - **Calculation:** One RCU provides enough capacity for **one 4 KB strongly consistent read per second**.
>     - **Example (Strongly Consistent):** To perform a strongly consistent read on a 2.5 KB item, you need to divide the item size by the unit size (2.5 KB / 4 KB) and round up. This results in **1 RCU per read**. If you need to perform 10 reads per second, your total RCU is 1 RCU per item * 10 reads/second = **10 RCUs**.
> - **Cost Difference:**
>     - An eventually consistent read is half the cost of a strongly consistent read.
>     - In the example above, 10 reads per second for a 2.5 KB item would only consume 1 RCU per item * 10 reads/second / 2 = **5 RCUs**.
> - **Storage Node:** A DynamoDB storage node is a physical component in the underlying distributed infrastructure that holds and manages a portion of a table's data. Data is automatically replicated across multiple storage nodes to ensure high availability and durability.

Consistency Models
- Bob updates a DynamoDB item, removing an attribute -> Dynamodb directs the write at the leader storage node which is elected from the three storage nodes -> leader node replicates data to other nodes, typically finishing within a few MS
- Eventually consistent reads check 1/3 nodes, could be unlucky with stale data if anode is checked before replication completes. 50% of the cost vs strongly consistent.
- Strongly consistent reads connect to the leader node to get the most updated copy of data
- Not every application or access type tolerates eventual consistency, select the model as appropriate
WCU Calculation
- If you need to store 10 ITEMS per second, 2.5K average size per ITEM
	- Calculate WCU per item, round up (ITEM SIZE/1KB) = 3
	- Multiply by average number per second = 10
	- 3 * 10 = 30 WCU
RCU Calculation
- Calculate RCU per item, round up (item size/4KB)
- Multiply by average read ops per second = Strongly consistent RCU required, eventually consistent RCU is 50%