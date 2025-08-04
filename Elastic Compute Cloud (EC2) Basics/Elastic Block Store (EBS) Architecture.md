
>[!note]- Post-Processing
>## Key Insights and Information from the EBS Lesson:
>
>**What is EBS?**
>
>* **Block storage service:** Provides storage addressed using block IDs, like physical hard drives.
>* **Volumes:** Allocations of physical disks presented to EC2 instances. Can be encrypted using KMS.
>
>**How EBS Works:**
>
>* **Availability Zone Based:** EBS operates within a single availability zone. Volumes in one AZ cannot be accessed from another.
>* **Resilient within AZ:** Built-in redundancy within an AZ protects against single-device failures.
>* **EC2 Instance Attachment:** Appears as a raw storage device to EC2 instances, allowing file system creation (EXT3, EXT4, NTFS, etc.).
>* **Persistent:** Data remains even if the instance is stopped, restarted, or moved between hosts.
>
>**Volume Management:**
>
>* **Single Instance Attachment (Default):** Volumes are typically attached to one instance at a time.
>* **Multi-Attach (Specific Use Cases):** Allows attaching to multiple instances simultaneously, requiring cluster application management to avoid data corruption.
>* **Detach and Reattach:** Volumes can be detached from one instance and attached to another within the same AZ.
>
>**Snapshots and Replication:**
>
>* **Snapshots:** Backups of volumes stored in S3, providing regional resilience.
>* **Cross-AZ and Region Snapshots:** Snapshots can be copied to other regions, enabling volume creation in different AZs or regions.
>
>**Billing:**
>
>* **GB per month:** Charged based on volume size and usage.
>
>**Important Considerations:**
>
>* **AZ Dependency:** EBS is strictly availability zone-based.
>* **Snapshot Importance:** Use snapshots for cross-AZ and regional data replication and recovery.
>
>
>This summary provides a concise overview of the key concepts and functionalities of EBS as explained in the lesson.
>

- Block Storage - raw disk allocations (volume) - can be encrypted using KMS
- Instances see block device and create file system on that device using ext3/4, xfs, or NTFS
- Storage is in ONE AZ and resilient in that AZ 
- Attached to one EC2 instance over a storage network
- Can be detached and reattached to instances, not lifecycle linked to one instance = persistent
- Snapshot (backup) into S3. Create volume from snapshot to migrate between AZs
- Different physical storage types, different sizes, different performance profiles
- Billed based on GB-month (and in some cases performance)
![[EBS Diagram.png]]

- We can link different volumes of EBS to different EC2 instances within the same az, and can have multiple EBS attached to one EC2 instance.
- We cannot go cross AZ or cross region.
	- In order to do this, we create a snapshot to S3, and then use the S3 snapshot to create an EBS volume that we then link with the EC2 instance in the "new" region.