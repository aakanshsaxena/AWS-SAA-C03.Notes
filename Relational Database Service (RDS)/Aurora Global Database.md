
>[!note]- Post-Processing
>## Key Insights from Aurora Global Database Explanation:
>
>**What is it?**
>
>* Aurora Global Database allows you to replicate your Aurora database across up to five AWS regions.
>* It enables global level replication with a master region and up to five secondary regions.
>
>**Architecture:**
>
>* **Primary Region:** Functions like a normal Aurora cluster with one read/write instance and up to 15 read-only replicas.
>* **Secondary Regions:** Contain read-only replicas (up to 16 per region) and serve as backups.
>* Replication occurs at the storage layer, typically within one second.
>
>**Use Cases:**
>
>* **Cross-Disaster Recovery & Business Continuity:** Secondary regions can act as primary clusters in case of a disaster in the primary region, ensuring low RPO and RTO values.
>* **Global Read Scaling:**  Reduces latency for international customers by placing read replicas in closer geographical locations.
>
>**Important Points:**
>
>* **One-Way Replication:** Data flows from the primary region to secondary regions, not vice versa.
>* **Storage-Layer Replication:** Doesn't impact database performance as it doesn't require additional CPU resources.
>* **Secondary Region Role:** All replicas in a secondary region are read-only, but can be promoted to read-write in case of a disaster.
>* **Maximum Secondary Regions:** Currently limited to five, but this is subject to change.
>
>**Exam Relevance:**
>
>* While not expected to be a major focus, understanding the basic functionality and use cases of Aurora Global Database is important for the exam.
>
>
>
>
>Let me know if you have any other questions!
>

- Useful for cross-region disaster recovery and business continuity
- Global Read Scaling - low latency performance improvements
- Around 1S or less replication between regions
- No impact on DB performance
- Secondary regions can have up to 16 replicas (can think about it because primary region has one R/W and up to 15 replicas = 16)
- Any of the replicas can be promoted to R/W
- Currently MAX of 5 secondary regions
