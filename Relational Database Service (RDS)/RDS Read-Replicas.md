
>[!note]- Post-Processing
>## Key Insights and Information from RDS Read Replicas Video:
>
>**What are Read Replicas?**
>
>* Read-only replicas of an RDS instance.
>* Separate from the primary instance with its own endpoint address.
>* Applications need to be configured to use them.
>* Used for read operations only, not writes.
>
>**Types of Replication:**
>
>* **Synchronous:** Used in Multi-AZ deployments. Data is written to both primary and replica simultaneously, ensuring minimal lag.
>* **Asynchronous:** Used for read replicas. Data is written to the primary first, then replicated to the replica, resulting in potential lag (seconds).
>
>**Benefits:**
>
>* **Read Performance and Scaling:**  Increase read capacity by creating multiple read replicas. Each replica adds additional read performance.
>* **Global Performance Improvements:**  Read workloads in other regions can connect to cross-region read replicas, improving performance and reducing load on the primary instance.
>* **Low Recovery Time Objectives (RTO):**  Quickly promote a read replica to become the new primary in case of failure, minimizing downtime.
>* **Near Zero Recovery Point Objectives (RPO):** Data on read replicas is synchronized with the primary, minimizing potential data loss in case of failure.
>
>**Limitations:**
>
>* **Lag:** Asynchronous replication can introduce lag between the primary and read replicas, which can become problematic with multiple levels of read replicas.
>* **Data Corruption:** Read replicas will reflect any data corruption present on the primary instance.
>
>**Important Notes:**
>
>* Read replicas are not suitable for recovering from data corruption.
>* Cross-region read replicas are managed by AWS, including encryption and networking.
>* Promoting a read replica to a primary instance is a quick process.
>
>
>**Exam Tips:**
>
>* Remember that synchronous replication is used in Multi-AZ deployments, while asynchronous replication is used for read replicas.
>* Understand the benefits and limitations of read replicas.
>* Be aware of the potential for lag with multiple levels of read replicas.
>

- Read only replicas of RDS instance
- Can use read replicas for read operations
- Have their own DB address, so think of them as their own thing
- Kept in sync via async replication - small lag maybe seconds
Performance Improvements
- 5x direct read-replicas per DB instance
- Each providing an additional instance of read performance
- Read-replicas can have read-replicas but lag can stack
- Global performance improvements 
RPO/RTO Improvements
- Snapshots & Backups improve RTO
- RTO's are a problem
- RR's offer nr. 0 RPO
- RR's can be promoted quickly - low RTO
- Failure only - watch for data corruption
- Read only until promoted
- Global availability improvements, global resilience
