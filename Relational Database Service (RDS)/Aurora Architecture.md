
>[!note]- Post-Processing
>## Key Insights and Information from the Amazon Aurora Managed Database Lesson:
>
>**Architecture:**
>
>* **Cluster-based:** Aurora is built on a cluster architecture, consisting of a primary instance and zero or more replicas.
>* **Shared Storage:** All instances in a cluster share a single, high-performance SSD-based storage volume called the cluster volume. This volume is replicated across multiple availability zones for high availability and durability.
>* **Read Replicas:** Aurora replicas can be used for read operations during normal operations, providing both read scaling and high availability.
>* **Failover:** Aurora supports failover to any of its 15 replicas, ensuring quick recovery in case of primary instance failure.
>
>**Benefits:**
>
>* **High Availability and Durability:**  The shared storage volume and multi-AZ deployment minimize the risk of data loss due to disk failures.
>* **Read Scaling:** Read replicas enable efficient read scaling, improving application performance.
>* **Fast Failover:** Failover to a replica is quick due to the shared storage architecture.
>* **Performance:** SSD-based storage provides high IOPS and low latency.
>
>**Storage:**
>
>* **High Watermark Billing:** Storage is billed based on the maximum amount consumed (high watermark) during the cluster's lifetime.
>* **Free Backup Allocation:** 100GB of storage is provided for free backups, typically sufficient for most use cases.
>
>**Advanced Features:**
>
>* **Backtrack:** Allows rolling back the database to a previous point in time, avoiding data loss from corruption.
>* **Fast Clone:** Creates a new database from an existing one, referencing the original storage and only storing changes, resulting in faster cloning and reduced storage consumption.
>
>**Costs:**
>
>* **No Free Tier:** Aurora doesn't have a free tier due to its use of larger instances.
>* **Hourly Compute Charges:** Billed per second with a 10-minute minimum.
>* **Storage Charges:** Based on gigabyte-month consumed (high watermark).
>* **IO Charges:** Per request made to the cluster shared storage.
>
>
>**Overall:**
>
>Aurora is a powerful and scalable managed database service offering significant advantages over traditional RDS engines, particularly in terms of availability, performance, and advanced features like Backtrack and Fast Clone.
>

- Very different architecture vs RDS
- Uses clusters -> a single primary instance + 0 or more replicas
- No local storage - uses combined cluster volume
- All SSD Based - high IOPS, low latency
- Storage is billed on whats used from a high watermark point (billed for most used storage in that clusters lifetime)
- Storage which is freed up can be re-used
- Replicas can be added and removed without requiring storage provisioning
Cost
- No free-tier
- Doesn't support micro instances
- Beyond RDS singleAZ (micro) Aurora has a better value
	- Compute - hourly charge per second, min 10 mins
	- Storage - GB-Month consumed, IO cost per request
	- 100% DB Size in backups included free
Aurora Restore, Clone & Backtrack
- Backups in Aurora work in the same way as RDS
- Restores create a new cluster
- Backtrack can be used which allow in-place rewinds to a previous point in time
- Fast clones make a new database MUCH faster than copying all the data - copy-on-write