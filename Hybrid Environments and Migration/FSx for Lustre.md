> [!note]- AI
> #### FSx for Lustre Deployment Types
> * **Scratch Deployment:** This type is designed for temporary storage and short-term, performance-focused workloads where data is not needed after the job is complete.
>     * It does not provide replication or high availability. If a hardware component fails, data stored on the affected component can be lost.
>     * It offers high performance for a low cost, making it ideal for processing data from S3 or another durable source during a single, short-lived compute job.
> * **Persistent Deployment:** This type is for long-term storage of data. It is a highly available and durable file system.
>     * Data is replicated within a single Availability Zone (AZ) to protect against hardware component failure. The service auto-heals after a failure, preventing data loss.
>     * It supports both automatic daily backups and user-initiated backups to Amazon S3.
> #### Performance and Scaling
> * **Proportional Throughput:** An FSx for Lustre file system's performance is directly proportional to its storage capacity. For persistent deployments, there are different throughput levels per TiB (e.g., 50, 100, 200 MB/s per TiB) that you can provision.
> * **Credit System:** Performance is based on a credit system, similar to Amazon EBS burstable volumes. The file system earns credits when operating at or below its baseline throughput and consumes credits when bursting above the baseline to achieve higher speeds. This allows for peak performance up to **1,300 MB/s per TiB** for short periods.
> * **Architecture:** The file system is a parallel file system that scales across multiple servers. More storage capacity results in more storage servers, which provides higher aggregate throughput and IOPS.
> * **Network Access:** Clients (e.g., Linux EC2 instances) access the file system via a single Elastic Network Interface (ENI) in the VPC. The Lustre client on the instance handles parallel I/O, allowing reads and writes to be distributed across the storage servers for maximum performance.
> #### Data Protection and Backups
> * **Intra-AZ Replication:** Persistent file systems are replicated within an Availability Zone to protect against component failure. However, they are not resilient to an entire AZ failure.
> * **Backups to S3:** Backups provide the primary method for disaster recovery. You can create manual or automatic backups of persistent file systems, which are stored durably in Amazon S3. The retention period for automatic backups can be set from 0 to 35 days.
> * **Backup Limitations:** Backups are **not supported** on scratch file systems because they are designed for temporary data. They are also not supported on file systems that are linked to an S3 data repository, as the S3 bucket is considered the primary, durable data source.
> #### Use Cases and Integration
> * **High-Performance Workloads:** FSx for Lustre is the ideal choice for workloads that require a high-performance, parallel file system, such as High-Performance Computing (HPC), machine learning, and big data analytics.
> * **POSIX-Compliant:** It provides a POSIX-compliant file system that is easily accessible from Linux EC2 instances, making it a great solution for cloud-native or migrated Linux workloads.
> * **S3 Data Repository:** The file system can be linked to an Amazon S3 bucket, which allows you to process data in the high-performance Lustre file system and then write the results back to the durable S3 data repository.

- Managed Lustre - designed for high-performance computing (HPC) - LINUX Clients (POSIX)
- ML, Big Data, Financial Modelling
- 100 GB/s throughput & sub ms latency
- Deployment types - Persistent or Scratch
- Scratch - Highly optimized for short term, no replication and fast
- Persistent - longer term, HA (in one AZ), self-healing
- Accessible over VPN or DX
- Data is lazy loaded from S3 into the file system as its needed, and then we can export it back to S3 at any point using hsm_archive
- Metadata stored on Metadata Targets (MST)
- Objects are stored on called object storage targets (OSTs) (1.17TiB)
- Baseline performance is based on size which starts at 1.2TiB then increments of 2.4TiB
- For scratch - base 200 mb/s per TiB of storage
- Persistent offers 50, 100, 200Mb/s per TiB of storage
- Can burst up to 1,300Mb/s per TiB, operates on a credit system similar to EFS
- Connections between VPC and S3/FSX happen through a single VPC-injected ENI 
Overview
- Scratch is designed for pure performance
- Short term or temp workloads
- No HA, No Replication
- Larger file systems means more servers, more disks and more chance of failure
- Persistent has replication within one AZ only
- Auto-heals when hardware failure occurs
- You can backup to S3 with both (manual or automatic 0-35 day retention)