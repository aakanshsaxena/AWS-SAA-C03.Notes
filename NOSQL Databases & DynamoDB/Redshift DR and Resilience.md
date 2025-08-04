> [!note]- AI
> #### Redshift Backups and Resilience
> - **Single Availability Zone Risk:** A Redshift cluster is deployed within a single Availability Zone (AZ). While this provides high availability within that AZ, it makes the cluster vulnerable to a failure of the entire AZ. A robust backup and recovery strategy is essential to mitigate this risk.
> - **Snapshot Storage:** Redshift snapshots are point-in-time backups of your cluster that are stored in Amazon S3. S3's multi-AZ durability provides a high level of data protection against localized failures within a single region.
> #### Snapshot Types
> - **Automatic Snapshots:**
>     - **Trigger:** By default, Amazon Redshift automatically takes snapshots of your cluster about every 8 hours or following every 5 GB of data changes per node, whichever comes first.
>     - **Retention:** The default retention period is **1 day**, but this can be configured for up to **35 days**. When a cluster is deleted, all automatic snapshots are also deleted.
>     - **Incremental:** These snapshots are **incremental**. They only store the data that has changed since the last snapshot, which makes them very space-efficient and reduces the time it takes to create them.
> - **Manual Snapshots:**
>     - **On-Demand:** You can create a manual snapshot at any time.
>     - **Retention:** Manual snapshots have a retention period of **"until deleted"**. They are retained indefinitely, even if the cluster is deleted. This is a critical feature for long-term data retention and compliance requirements.
> #### Disaster Recovery and Resilience
> - **Cross-Region Snapshot Copy:** This is the key feature for a disaster recovery (DR) strategy. You can configure Redshift to automatically copy both manual and automatic snapshots to a different AWS region.
> - **Recovery:** In the event of a full region failure, you can use the latest cross-region snapshot to restore your data to a new Redshift cluster in a different region, which significantly reduces your recovery time.
> - **Cost and Management:** Snapshots incur storage charges in your account, but Redshift provides a free storage capacity equal to your provisioned cluster size. Any snapshots beyond that capacity are billed at standard S3 rates.
> #### Definitions
> - **Incremental Process:** In the context of database backups, this refers to a strategy where only the data that has changed since the last backup (either full or incremental) is copied. This reduces backup time, bandwidth usage, and storage space.
> - **Availability Zone:** One or more isolated data centers within an AWS Region. Each AZ has independent power, cooling, and networking and is connected to other AZs via low-latency links.
> - **Redshift:** A fully managed, petabyte-scale data warehouse service in the AWS cloud. It is designed for large-scale analytical processing and business intelligence.
> - **Retention Period:** The length of time that a backup or snapshot is stored for recovery purposes. After this period, the backup is automatically deleted.
> 

- Use S3 snapshots for backups - automatic every 8 hours/5GB of data change, 1-35 day retention. Manual Snapshots
- Can configure snapshots to be copied to another region (in case of region failure)
	- Separate configurable retention period