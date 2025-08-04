> [!note]- AI
> #### DynamoDB Global Tables: Multi-Region Replication
> - **Purpose:** DynamoDB Global Tables provide a fully managed, multi-region, and multi-master replication solution for DynamoDB. This allows you to deploy a single application that is highly available and provides low-latency reads and writes for a globally distributed user base.
> - **Architecture:** Global tables are a collection of multiple DynamoDB tables, each created in a different AWS region. All these tables have the same name and primary key. DynamoDB automatically manages the replication links between all the replica tables, forming a multi-master replication model.
> #### Conflict Resolution and Consistency
> - **Multi-Master Replication:** This is a database replication model where multiple database nodes (or, in this case, regional tables) can accept both read and write operations concurrently. Changes made on one replica table are propagated to all other replica tables to maintain data consistency across the global system. This design enhances both availability and performance.
> - **Last Write Wins Conflict Resolution:** Conflicts can arise when the same item is updated in two different regions at about the same time. To resolve these conflicts, DynamoDB Global Tables use a "last write wins" strategy. This simple, effective mechanism uses a system-defined timestamp to determine which write is the most recent. The write with the highest timestamp is replicated to all other replicas, overwriting any previous updates and ensuring that all replicas eventually converge to the same state.
> - **Consistency Model:**
>     - **Asynchronous Replication:** The replication between regional tables is asynchronous, with typical latency under one second.
>     - **Regional Consistency:** Within the region where a write operation occurs, you can perform a **strongly consistent read** on that data.
>     - **Global Consistency:** However, all reads from other regions (i.e., not the region where the write was performed) will be **eventually consistent**. This means that applications must be designed to tolerate a slight delay in seeing the latest data.
> #### Benefits and Use Cases
> - **Global Disaster Recovery:** If a single AWS region becomes isolated or degraded, your application can fail over to another region and continue to perform reads and writes against a different replica table, ensuring business continuity.
> - **Low Latency:** By placing data closer to your global user base, you can achieve single-digit millisecond latency for reads and writes, as users can interact with the regional table that is closest to them.
> - **Simplified Management:** Global tables abstract away the operational complexity of managing a multi-region database. You simply enable the feature on a table, and DynamoDB handles all the replication, conflict resolution, and synchronization.
> #### Definitions
> - **Multi-Master Replication:** A database replication method where multiple nodes (or masters) in a cluster can accept read and write operations simultaneously. Changes from each master are asynchronously propagated to all other masters to maintain a consistent state.
> - **Last Write Wins Conflict Resolution:** A conflict resolution strategy where, in the case of concurrent updates to the same item, the write with the most recent timestamp is the one that is accepted and replicated, overwriting all other conflicting writes.

- Provide multi-master cross-region replication
- Allows for read adn write replication
- Tables are created in multiple regions and added to the same global table (becoming replica tables)
- Last writer wins is used for conflict resolution
- Reads and Writes can occur to any region
- Generally sub-second replication between regions
- Strongly consistent reads ONLY in the same region as writes
- Sub-second replication between table replicas
- Global eventual consistency same-region eventual or strongly consistent
- Multi-master replication, all tables can be used for Read and Write operations
- Provides Global HA and Global DR/BC
- Last writer wins conflict resolution