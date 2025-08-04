
>[!note]- Post-Processing
>## RDS Backup and Restore: Key Insights
>
>This video explains how to back up and restore data in Amazon Relational Database Service (RDS). Here are the key takeaways:
>
>**Backup Types:**
>
>* **Automated Backups:**
>    * Occur daily, with a full backup followed by incremental backups of changed data.
>    * Provide a recovery point objective (RPO) of 5 minutes due to transaction log backups every 5 minutes.
>    * Retention period configurable from 0 to 35 days.
>    * Default setting does not enable cross-region replication.
>* **Snapshots:**
>    * Manual, scheduled backups (hourly, daily, weekly, monthly).
>    * Provide a point-in-time recovery but require manual scheduling for optimal RPO.
>    * Stored in S3, managed by AWS, and do not expire.
>
>**Backup Process:**
>
>* Backups are taken from the standby instance in multi-AZ deployments, minimizing performance impact.
>* Single-AZ deployments may experience IO pauses during backups.
>* Initial snapshots are full copies; subsequent snapshots store only changed data.
>
>**Restore Process:**
>
>* Restores create a new RDS instance with the restored data.
>* Requires updating application connections to the new endpoint.
>* Automated backups allow restoration to a specific point in time within the retention period.
>* Snapshots restore to a single point in time, potentially leading to data loss if not taken immediately before a failure.
>* Restores can be time-consuming, especially for large databases.
>
>**Important Considerations:**
>
>* Cross-region replication for backups requires explicit configuration.
>* Automated backups expire after the configured retention period.
>* Final snapshots must be manually created and deleted to preserve data beyond the retention period.
>* Read replicas offer improved RPO for disaster recovery.
>
>
>**Overall:**
>
>RDS provides robust backup and restore capabilities, but understanding the different options and their implications is crucial for effective data protection and disaster recovery planning.
>

RDS Backups - General
- Automated backups, or manual snapshots
- Regardless they are taken as snapshots
- First snap is full, onward is incremental and these are taken from standby instance/SingleAZ
- Put into AWS managed S3 buckets, and have a 5 minute RPO (every 5 minutes transaction logs)
- Retention is anywhere between 0 (disabled) and 35 days
- After deleting an RDS database, snapshots will delete according to retention period unless you manually take final snapshot.
RDS Restores
- Creates a new RDS Instance - New Address
- Snapshots = single point in time, creation time
- Automated = any 5 minute point in time
- Backup is restored and transaction logs are replayed to bring DB to desired point in time (GOOD RPO)
- Restores aren't fast - think about RTO (*RR's)
