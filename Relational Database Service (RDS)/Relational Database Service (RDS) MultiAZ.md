
>[!note]- Post-Processing
>## RDS High Availability: Multi-AZ Instance vs. Multi-AZ Cluster
>
>This transcript explains two ways Amazon RDS provides high availability: multi-AZ instance deployment and multi-AZ cluster deployment. 
>
>**Key Insights:**
>
>* **Multi-AZ Instance Deployment (Older Method):**
>    * Uses synchronous replication at the storage level.
>    * Only one standby replica exists, which cannot be used for reads or writes.
>    * Failover can take 60-120 seconds.
>    * Only available within the same AWS region.
>    * Backups can be taken from the standby replica.
>* **Multi-AZ Cluster Deployment (Newer Method):**
>    * Uses one writer instance and two reader instances in different availability zones.
>    * Readers can be used for read operations, allowing for read scaling.
>    * Faster failover (35 seconds + transaction log application time).
>    * Runs on faster hardware with Graviton architecture and local NVMe SSD storage.
>    * Replication is done using transaction logs, which is more efficient.
>    * Requires application support for separate read/write endpoints.
>
>**Differences between Multi-AZ Instance and Multi-AZ Cluster:**
>
>* **Number of replicas:** Instance mode has one standby, while cluster mode has two readers.
>* **Reader usage:** Readers in cluster mode can be used for read operations, while the standby in instance mode cannot.
>* **Failover time:** Cluster mode has faster failover.
>* **Hardware and storage:** Cluster mode uses faster hardware and local NVMe SSD storage.
>* **Replication method:** Cluster mode uses transaction logs for replication, which is more efficient.
>
>**Important Notes:**
>
>* Aurora is a different database platform with its own scaling and availability features.
>* Multi-AZ cluster mode requires application support for separate read/write endpoints.
>* Both modes offer high availability within the same AWS region.
>
>
>
>This summary provides a clear understanding of the key differences between the two multi-AZ architectures offered by RDS, helping you choose the best option for your needs.
>

Multi AZ - Instance
- You have a primary and standby RDS instance, synchronous replication, and standby is not used until primary fails
- When primary fails, database CNAME adjusts from primary to standby
- Backups to S3 and other background work may be performed by standby RDS database
- Located in at least two diff AZ's
- Data -> primary and replicated to standby committed (synchronous)
- Not free tier, extra cost for replica
- Only one standby replica which we cant use for reads or writers
- 60-120 second failover
- Same region only, diff AZ's in same region
- Backups taken from standby to improve performance
- Used for AZ outage, primary failure, manual failover, instance type change and software patching
Multi AZ - Cluster
- 1 Writer and 2 Reader DB Instances in different AZ's
- Much faster hardware, Graviton + local NVME SSD Storage
- Fast writes to local storage -> flushed to EBS
- Readers can be used for reads allowing some read scaling
- Replication is via transaction logs which is more efficient
- Failover is faster at around 35s + transaction log apply
- Writes are committed when 1 reader has confirmed
