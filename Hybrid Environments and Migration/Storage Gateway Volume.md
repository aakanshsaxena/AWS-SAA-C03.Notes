> [!note]- AI
> #### Volume Gateway: Overview and Core Concepts
> 
> AWS Storage Gateway is a hybrid cloud storage service that provides on-premises applications with seamless access to virtually unlimited cloud storage. It runs as a virtual appliance or a physical hardware device in your local data center. The service communicates with AWS over the public internet, a VPN, or a dedicated AWS Direct Connect link.
> 
> All modes of the Volume Gateway present storage to on-premises servers as a **block-based iSCSI volume**. This means the gateway emulates a local SAN (Storage Area Network) or a disk array. The on-premises server sees and mounts this storage as if it were a local drive, using the iSCSI protocol. The data on these volumes is backed up to AWS as **EBS Snapshots**. These snapshots are point-in-time copies of your entire volume data, which are then stored in Amazon S3 for long-term durability and can be used to create new volumes in the cloud or on a different gateway.
> 
> #### Volume Stored Mode
> 
> In **Stored Mode**, the primary copy of your application's data is kept locally on your gateway's on-premises storage. This local storage can be a set of hard disks or SSDs that you allocate to the virtual appliance.
> 
> - **Primary Data Location:** All primary data is stored locally. The on-premises storage acts as the single source of truth for the data.
>     
> - **Performance:** Because the primary data is local, applications can access it at LAN speeds, providing very low latency for all read and write operations.
>     
> - **AWS Role:** AWS's role is primarily for **backup and disaster recovery**. The gateway asynchronously uploads a copy of all data to Amazon S3 as EBS Snapshots. This ensures that you have a durable, off-site backup in the event of a local hardware failure or site disaster.
>     
> - **Use Case Example:** A small business with a critical on-premises database wants a reliable off-site backup. They can use Stored Mode to store their primary data locally for fast access, and the gateway will automatically create snapshots in AWS S3. If their local server fails, they can restore the volume from an S3 snapshot.
>     
> 
> #### Volume Cached Mode
> 
> In **Cached Mode**, the primary copy of your application's data is stored in Amazon S3. The local gateway's storage is used as a **cache** for frequently accessed data.
> 
> - **Primary Data Location:** The single source of truth for your data is in Amazon S3. The local gateway only stores a subset of this data.
>     
> - **Performance:** Performance is excellent for data that is in the local cache (known as "hot" data) as it's accessed at LAN speeds. However, there will be a slight performance hit (latency) when an application needs to access "cold" data that has not been cached and must be retrieved from S3.
>     
> - **AWS Role:** AWS is the primary, unlimited storage repository. The gateway acts as a high-speed access point and buffer between your applications and the cloud. This architecture allows you to manage hundreds of terabytes or even petabytes of data without having to buy and maintain the corresponding local storage.
>     
> - **Capacity:** A single gateway in Cached Mode can support up to 32 volumes, with each volume up to 32 TB, for a total of **1 PB of storage**. This massive scale is a key advantage over Stored Mode.
>     
> - **Use Case Example:** A media company with terabytes of archival footage needs to free up space on their expensive on-premises SAN. They can use Cached Mode to seamlessly offload their old, infrequently accessed video files to Amazon S3. Their video editors still see a single, large volume, but the local gateway only caches the current projects and recently accessed files, while the rest of the data resides in the cloud, transparently accessible when needed.
>     
> 
> #### Comparing Stored and Cached Modes
>
> | Feature                   | Volume Stored Mode                                 | Volume Cached Mode                                               |
> | ------------------------- | -------------------------------------------------- | ---------------------------------------------------------------- |
> | **Primary Data Location** | On-premises (Local)                                | AWS S3 (Cloud)                                                   |
> | **Data on Gateway**       | All data                                           | Frequently accessed data (Cache)                                 |
> | **Use Case**              | Backup, disaster recovery, migration of local data | Data center extension, large-scale storage, offloading cold data |
> | **Performance**           | LAN speed for all data                             | LAN speed for cached data, latency for cold data (from S3)       |
> | **Total Capacity**        | Limited by local storage size                      | Up to 1 PB per gateway                                           |
> | **AWS Function**          | Off-site backup target                             | Primary storage repository                                       |
> 
> #### Data Center Extension Architecture
> 
> The **Cached Mode** architecture is perfectly suited for extending your on-premises data center into AWS. This is particularly useful when:
> 
> 1. **You're running out of local storage capacity.** Instead of buying new hardware, you can use the gateway to extend your storage to S3, which has virtually unlimited capacity.
>     
> 2. **You want to consolidate storage.** You can centralize vast amounts of data in S3 while still providing local applications with low-latency access to the active datasets they need.
>     
> 3. **You're planning a long-term migration to AWS.** This architecture allows you to incrementally move your data to the cloud while maintaining business continuity. Your on-premises servers see the storage as local, but the data is already being stored and managed in AWS, simplifying the eventual full migration.

- Storage Gateway is often a virtual machine but sometimes can be a hardware appliance
- It presents storage using iSCSI, NFS, or SMB and integrates with EBS, S3, and Glacier within AWS
- Migrations, extensions, storage tiering, DR, and replacement of backups systems are all functions of Storage Gateway, but you need to know what mode to use for scenarios.
- We connect to the storage gateway VM via iSCSI, and it allows the on-prem servers to interact with the storage like it's a local block device
Storage Gateway - Volume Stored
![[Pasted image 20250727154111.png]]
- We have our on-prem servers, and storage gateway VM. All have a storage gateway endpoint. 
- We can have 32 volumes per Gateway, 16B per volume, 512TB per gateway.
- We connect our storage gateway VM to the storage gateway endpoint in AWS, which creates full disk EBS snapshots that we can use.
- Great for full disk backups of servers, when we want our data stored locally, or if we are planning to use AWS to help with disaster recovery (we can use EBS volumes in AWS for usage)
- Don't use for more datacenter capacity because our main copy of data is stored on the gateway and on-prem
Storage Gateway - Volume Cached
![[Pasted image 20250727154345.png]]
- Using it in volume cached mode, we have a similar structure on-prem, but we have cache storage instead of local storage. 
- Now, our storage is AWS managed in S3 in AWS. It appears on-prem but is actually within AWS. Any frequently used data is loaded onto our cache storage on-prem.
- We can't access the S3 as buckets, but we can still make EBS snapshots
- 32TB per volume, 32 volumes per gateway, 1PB per gateway -> data stored in AWS, cached on-premises
- We can use this mode for capacity extension