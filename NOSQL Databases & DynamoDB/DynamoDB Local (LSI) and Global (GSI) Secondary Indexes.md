> [!note]- AI
> #### What are Global Secondary Indexes?
> - **Purpose:** A Global Secondary Index (GSI) is a powerful DynamoDB feature that provides an alternative view of your table data. It is a secondary index with a primary key schema that can be completely different from the base table's primary key. This allows you to query the same data using different access patterns without performing a costly `Scan` operation.
> - **Core Features:**
>     - **Separate Capacity:** Every GSI has its own dedicated read and write capacity units (RCUs/WCUs), which are separate from the base table.
>     - **Flexibility:** You can create a GSI on an existing table at any time. DynamoDB will backfill the index with the existing data.
>     - **Eventual Consistency:** Data replication from the base table to a GSI is an asynchronous process. This means that a query on a GSI is **always eventually consistent** and may not reflect the results of a very recent write operation to the base table.
>     - **Sparsity:** A GSI is "sparse" by nature. An item from the base table is only added to the GSI if it contains the attributes defined as the GSI's primary key.
> #### Addressing the Objection: Queries on Non-Projected Attributes
> - **Projections:** When you create a GSI, you must define which attributes from the base table you want to **project** into the index. You have three options: `KEYS_ONLY` (just the primary keys), `INCLUDE` (specific attributes), or `ALL` (all attributes).
> - **The Problem:** A query on a GSI can **only return attributes that are projected into that index**.
> - **The Cost:** If your application needs an attribute that was not projected, it cannot be retrieved with a single query. The application would first have to query the GSI to find the primary key of the item it needs, and then perform a separate `GetItem` call on the base table to retrieve the missing attribute. This is an inefficient, two-step process that consumes additional RCUs.
> - **Best Practice:** To avoid this, you must carefully plan your GSIs to project all the attributes that your query patterns will need. While projecting all attributes is an option, it increases the GSI's storage cost and write capacity consumption.
> #### GSIs vs. LSIs (Local Secondary Indexes)
> - **Key Schema:** A GSI can have a completely different partition key from the base table. A Local Secondary Index (LSI) must have the same partition key as the base table but a different sort key.
> - **Consistency:** GSI queries are always eventually consistent. LSI queries can be either eventually or **strongly consistent**, making them the choice for applications that require immediate data accuracy.
> - **Flexibility:** You can create and delete GSIs at any time after table creation. An LSI must be created at the same time as the base table and cannot be removed afterward.
> #### Definitions
> - **Global Secondary Indexes (GSIs):** A secondary index that provides an alternative primary key for querying a DynamoDB table. GSIs are globally scoped, can have different key attributes from the base table, and have their own provisioned capacity.
> - **Eventual Consistency:** A consistency model in which, if no new updates are made to an item, all copies of the item across a distributed system will eventually converge to the same value. This provides higher availability and scalability.

- Indexes a way to improve efficiency
- Query is the most efficient operation in DDB
- Query can only work on 1 PK value at a time
	- and optionally a single, or range of SK values
- Indexes are alternative views on table data
- Different SK (LSI) or Different PK and SK (GSI)
- Some or all attributes (projection)
Local Secondary Indexes - LSI
- An alternative view for a table
- Must be created with a table
- 5 LSI's per base table
- Alternative SK on the table
- Shares the RCU and WCU with the table
- Attributes - ALL, KEYS_ONLY & INCLUDE
- Indexes are sparse, only items which have a value in the index alternative sort key are added to the index. Non sunny days are omitted
Global Secondary Indexes - GSI
- Can be created at any time
- Default 20 limit per base table
- Alternative PK and SK
- GSI's have their own RCU and WCU allocations
- Attributes - ALL, KEYS_ONLY & INCLUDE
- An alternative view on the base table with alternative PK and SK, they have their own RCU and WCU and can be created at any time
- GSI's are sparse, only ITEMS which have values in the new PK and optional SK are added
LSI and GSI considerations
- Careful w/ projection
- Queries on attributes NOT projected are expensive
- Use GSIs as default, LSI only when strong consistency is required
- Use indexes for alternative access patterns