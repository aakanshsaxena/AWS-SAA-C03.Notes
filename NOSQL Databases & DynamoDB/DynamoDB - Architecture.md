> [!note]- AI
> #### Amazon DynamoDB: Core Concepts
> - **NoSQL Database:** DynamoDB is a fully managed, serverless NoSQL database service that supports key-value and document data models. It is designed for single-digit millisecond performance at any scale.
> - **Flexible Schema:** Unlike a relational database, DynamoDB tables do not have a fixed schema. Items can have a mixture of different attributes, and you only pay for the storage of the attributes you use.
> - **Item Size Limit:** Each item in a DynamoDB table has a maximum size of **400 KB**. This size limit includes the total of all attribute names and attribute values within the item.
> #### Capacity Modes and Units
> - **On-Demand Capacity:** This mode is best for unpredictable or spiky workloads where you don't know your traffic patterns in advance. With on-demand, you pay per request, and DynamoDB automatically scales your table's throughput to meet your workload needs without requiring you to provision capacity upfront.
> - **Provisioned Capacity:** This mode is for predictable, consistent workloads. You must explicitly set your table's capacity by specifying the number of Read Capacity Units (RCUs) and Write Capacity Units (WCUs) you require. It can be more cost-effective than on-demand if you can maintain high utilization of your provisioned capacity.
> - **Read Capacity Units (RCUs):**
>     - One RCU provides enough capacity for **one strongly consistent read per second** for an item up to 4 KB in size.
>     - For an **eventually consistent read**, one RCU provides two reads per second (up to 4 KB).
>     - If an item is larger than 4 KB, you will consume additional RCUs.
> - **Write Capacity Units (WCUs):**
>     - One WCU provides enough capacity for **one 1 KB write per second**.
>     - If an item is larger than 1 KB, you will consume additional WCUs.
> #### Backup and Recovery
> - **Point-in-Time Recovery (PITR):**
>     - This feature provides continuous, automatic backups of your table data with per-second granularity for the past **35 days**.
>     - It is disabled by default and must be explicitly enabled for each table.
>     - PITR allows you to restore your table to any single second within the 35-day window.
> - **On-Demand Backups:**
>     - These are manual, full backups of a table that are retained until you manually delete them.
>     - On-demand backups are typically used for long-term archival or for meeting specific regulatory requirements.
>     - They can be used to restore the table to a new table name, even in a different region.
> #### Billing and Exam Tips
> - **Billing:** DynamoDB is a pay-per-use service with no base costs for the service itself. You are billed based on your capacity units (or requests), storage consumed, and optional features like backups.
> - **Reserved Capacity:** For long-term, predictable workloads using provisioned capacity, you can purchase reserved capacity for one or three years in exchange for a significant discount.
> - **Exam Focus:** For exam questions that mention NoSQL or a key-value store, **DynamoDB** is almost always the correct answer. The exam often tests your understanding of the different capacity modes, the details of RCU/WCU, and the various backup options.

- NoSQL Public DB-as-a-Service (DBaaS) - Key/Value & Document
- No self-managed servers or infrastructure
	- reduced complexity and admin overhead
- Manual/automatic provisioned performance IN/OUT or On-Demand
- Highly resilient across AZs and optionally global
- Really really fast, single-digit MS (SSD Based)
- Backups, point-in-time recovery
- Event-driven integration, do things when data changes
DynamoDB Tables 
- Table is a grouping of items with the same primary key
	- Primary key = simple (partition) key or composite (partition & sort) 
- Each item must have a unqiue value for PK and SK, can have none, all, mixture, or different attributes
- Item MAX 400KB
- Write capacity unit (1 WCU) = 1 KB/s
- Read capacity unit (1 RCU) = 4KB/s
DynamoDB Backups
- On-demand backup = full copy of table, retained until removed
- Restore = same/cross region, with/without indexes, adjust encryption settings
Point-In-time-Recovery
- Must be enabled, continous record of cahnges allows replay to any point in the window (35 day recovery window)
- 1 second granulairty
Considerations
- NoSQL = prefer DynamoDB
- Relational Data = NOT DynamoDB
- Key/Value = prefer DynamoDB
- Access via console, CLI, API. Cannot use SQL 
- Billed based RCU, WCU, Storage, and features