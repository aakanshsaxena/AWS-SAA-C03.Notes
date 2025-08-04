> [!note]- AI
> #### AWS DataSync Core Architecture
> - **DataSync Agent:** A virtual appliance (VM) that you deploy on-premises to act as the bridge between your local storage and AWS. It can run on common hypervisors like VMware ESXi, Linux KVM, or Microsoft Hyper-V. The agent connects to your on-premises storage using standard protocols.
> - **Locations:** These define the source and destination for a data transfer. Locations can be on-premises (NFS or SMB file shares) or within AWS (S3 buckets, EFS file systems, or FSx for Windows File Server).
> - **Task:** A DataSync task is the core job that defines what data to transfer, where to transfer it, and how to transfer it. A task requires both a source and a destination location and includes settings for scheduling, bandwidth limits, and transfer options.
> #### Key Features and Transfer Management
> - **Transfer Optimization:** DataSync uses a purpose-built network protocol to accelerate data movement. It supports compression, incremental transfers (only moving changed files), and automatic recovery from network errors for high reliability.
> - **Bandwidth Control:** You can set bandwidth limiters on a task to prevent network link saturation, allowing you to manage the impact of data transfers on your network. This is useful for scheduling transfers during off-peak hours.
> - **Transfer Flexibility:** DataSync supports both one-time data migrations and recurring, scheduled transfers. It can also perform bidirectional syncs between on-premises and AWS storage.
> - **Security:** All data transferred between the agent and AWS is encrypted in transit using TLS. Data is also validated to ensure integrity throughout the transfer process.
> #### Integration with AWS and On-Premises
> - **On-Premises Connectivity:** The DataSync agent connects to your on-premises NAS or SAN storage devices using standard **NFS** or **SMB** protocols.
> - **AWS Service Integration:** DataSync integrates directly with several AWS storage services as transfer targets. This includes Amazon S3 (with support for various storage classes), Amazon EFS, and Amazon FSx for Windows File Server.
> - **Cloud-to-Cloud Transfer:** DataSync is not limited to on-premises to cloud transfers; it can also be used to transfer data between different AWS storage services, even across different AWS Regions or accounts.
> #### Exam Focus and Use Cases
> - The key to exam success is to understand the **architecture** and when to use DataSync compared to other data transfer services.
> - **DataSync** is the recommended tool for automated, online, and recurring electronic data transfers of large datasets.
> - It is often compared with **AWS Snow Family** (which is for offline, massive-scale data transfers) and **AWS Storage Gateway** (which provides hybrid cloud storage access rather than a one-time or recurring transfer service).

- Data transfer service to and from AWS
- Migrations, data processing transfers, archival/cost effective storage or DR/BC
- Designed to work at huge scale
- Two big plus: keeps metadata (permissions/timestamps), and built in validation
Key Features
- Scalable up to 10Gbps per agent (about 100TB per day)
- Bandwidth limiters (to avoid saturated the network link)
- Incremental and scheduled transfer options
- Supports compression and encryption
- Automatic recovery from transit errors
- AWS Service Integration with S3, EFS, FSx
- Pay as you use, per GB cost for data moved
Architecture
- We connect our on-prem SAN/NAS storage via NFS or SMB to the DataSync Agent which runs on a virtualization platform like VMWare and communicated with the AWS DataSync Endpoint
- Schedules can be set to ensure the transfer of data occurs during or avoiding specific time periods
- Customer impact can be minimized by setting a bandwidth limit in MiB/s
- Encryption in transit through TLS
- We send the data to the DataSync endpoint in our designated region which defines the SRC or DST for the sync of data TO or FROM AWS S3, EFS, FSx, NSF, SMB (can work both ways)
DataSync Components
- Task - A job within DataSync that defines what is being synced, how quickly, FROM where and TO where
- Agent - software used to read or write to on-premises data stores using NFS or SMB
- Location - every task has two locations FROM and TO. NFS, SMB, EFS, FSx, S3