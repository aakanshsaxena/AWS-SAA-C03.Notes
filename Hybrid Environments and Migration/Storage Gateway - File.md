> [!note]- AI
> #### Hybrid Architecture and Multi-Site Capabilities
> - **File Gateway** extends local storage to AWS S3, creating a hybrid architecture that includes both on-premises and AWS environments.
> - This architecture enables a **true multi-site setup**, where multiple on-premises environments can access the same S3 bucket.
> - There is a **one-to-one mapping** between files on the local file share and objects in the S3 bucket.
> - When a file is updated on an on-premises gateway, the changes are automatically copied to the S3 object.
> #### File Share Synchronization and Features
> - By default, updates from S3 are **not automatically pushed back** to the local gateways. A file share listing shows the most recent state known to the gateway.
> - New S3 objects, or changes made by other gateways, will only appear on a gateway's file share after a new listing is performed.
> - The gateway includes a **"notify when uploaded"** feature that uses **CloudWatch Events** to inform other gateways about updates, prompting them to refresh their listings.
> - The gateway uses standard file protocols like **NFS and SMB** to present file shares to on-premises applications.
> #### Limitations and Replication
> - File Gateway **does not support file locking**; concurrent edits from multiple users or applications can lead to data loss.
> - It also **does not support S3 Object Locking**.
> - The gateway integrates with **S3 Cross-Region Replication**, which allows you to automatically replicate your S3 objects to a different AWS region for multi-region disaster recovery (DR) at minimal cost.
> #### S3 Lifecycle Management Integration
> - File Gateway seamlessly integrates with **S3 Lifecycle Management**. You can define policies to automatically transition S3 objects to more cost-effective storage classes over time.
> - The default storage class for new objects is set when you create the file share.
> - Lifecycle policies automatically move objects (and thus your files) to cheaper storage classes like S3 Standard-IA or Glacier as they age.
> - This process happens automatically, helping you to optimize storage costs without any manual intervention.

- Bridges on-premises file storage and S3
- Mount points (shares) available via NFS or SMB
- Map directly onto a S3 bucket
- Files stored into a mount point, are visible as objects in an S3 bucket
- Read and write caching to ensure LAN-like performance
Basic Architecture
- We have on-premises servers and possibly even an Active Directory server
- We have files that we upload via SMB/NFS to different file shares and each file share is linked to a S3 Bucket with a file gateway in the same name, directory, etc.
- This is called a bucket share, an AWS S3 bucket and an on-premises file share, and we can have 10 bucket shares per file gateway
- The primary data is held in S3, but S3 objects are visible as on-premises files and maintain their structure
Multiple Contributors and Replication
- We can have multiple contributors to a single file share (more than one premises), but keep in mind that updates would not transfer through automatically.
- We would use NotifyWhenUploaded API to notify other gateways when objects are changed or added.
- File Gateway also doesn't support object locking, which means if someone on premises 1 edits at the same time as someone on premises 2, they could overwrite each other and cause data loss
	- To fix this, we can use read only mode on other shares or tightly control file access
- Like normal S3, we can have lifecycle policies that adjust which storage class a file belongs to automatically (S3 Standard -> S3 Standard IA -> S3 Glacier)