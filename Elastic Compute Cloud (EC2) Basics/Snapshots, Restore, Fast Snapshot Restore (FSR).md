
>[!note]- Post-Processing
>## Key Insights from EBS Snapshots Lesson:
>
>**What are EBS Snapshots?**
>
>* Backups of EBS volumes stored on S3.
>* Provide region-level resilience against availability zone issues.
>* Can be used to migrate data between availability zones and regions.
>* Offer a way to clone volumes.
>
>**How do they work?**
>
>* **Incremental:**
>    * First snapshot is a full copy of used data.
>    * Subsequent snapshots only store changes since the previous snapshot.
>    * Reduces storage space and improves performance.
>* **Self-contained:**
>    * Each snapshot, even incremental ones, is self-sufficient and can be used to restore the volume.
>
>**Snapshot Performance:**
>
>* **New Volumes:** Performance is available immediately.
>* **Restored Volumes:**
>    * **Lazy Restore:** Data is transferred from S3 to the new volume in the background.
>    * **Performance Impact:** Reading data not yet restored results in lower performance.
>    * **Fast Snapshot Restore (FSR):**
>        * Option to enable instant restore for specific snapshots and availability zones.
>        * Costs extra and has a limit per region.
>
>**Snapshot Cost:**
>
>* Billed based on "gigabyte-month" usage.
>* Only charges for used data, not allocated volume size.
>* Incremental nature allows for frequent snapshots without significant cost increase.
>
>**Key Takeaways:**
>
>* EBS snapshots are a powerful tool for data protection, migration, and cloning.
>* Understand the difference between full and incremental snapshots.
>* Be aware of performance implications when restoring volumes from snapshots.
>* Consider the cost implications of using FSR.
>
>
>

EBS Snapshots
- Snapshots are incremental volume copies to S3
	- First is a full copy of the in-use data on that volume
	- Every following snapshot is the changes between the first snapshot and now
- Volumes can be created and restored from snapshots
- Snapshots can be copied to another region (S3)
EBS Snapshots/Volume Performance
- New EBS volume gives you the full performance immediately
- Snapshots restore lazily/gradually
- Requested blocks are fetched immediately from S3, but this could cause reduced performance
- You can force a read of all data immediately
	- using DD on Linux or a similar tool
	- using Fast Snapshot Restore (FSR) - immediate restore but at a cost
- Up to 50 snapshots per region. Each set of the snapshot and AZ you choose to be able to do instant restores to counts as one snapshot/50 total.
Snapshot Consumption and Billing
- Gigabyte-month
	- 10GB stored for one month = 10GBmonth
	- 20GB stored for 1/2 month = 10GB month
- Charged for USED data, not all allocated data
	- If you have 40GB allocated, and only use 10GB (because your snapshot is only 10GB, it also saves the used data), then charged for the 10GB used
