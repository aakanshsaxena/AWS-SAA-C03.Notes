> [!note]- AI
> #### Amazon FSx for Windows File Server Architecture
> - **Hybrid Connectivity:** FSx for Windows File Server is designed to be a native file system for Windows environments, whether in the cloud or on-premises. It is accessible via VPC peering, VPN, or AWS Direct Connect, allowing access from your corporate network.
> - **VPC and AD Integration:** A typical implementation involves deploying FSx within a VPC that is connected to your corporate network. It requires a directory service for user authentication and permissions. This can be either **AWS Managed Microsoft AD** or your existing **on-premises Active Directory**.
> - **Deployment Modes:** FSx can be deployed in a single or multi-Availability Zone (AZ) configuration, providing options for durability and high availability. Multi-AZ deployments automatically replicate data and provide failover.
> - **Access Protocol:** FSx for Windows File Server uses the industry-standard **SMB (Server Message Block) protocol** for file share access. This allows it to be used seamlessly by Windows, macOS, and Linux clients, as well as AWS services like Amazon WorkSpaces. File shares are accessed using standard Windows UNC paths.
> #### Native Windows Features
> - **Windows Permission Model:** FSx provides native support for the Windows permission model, using **NTFS Access Control Lists (ACLs)**. This allows you to manage file and folder permissions for users and groups from your Active Directory, just as you would with a traditional on-premises file server.
> - **Volume Shadow Copies (VSS):** This feature allows end-users to restore previous versions of files and folders directly from their client machines without needing an administrator's help. It's a key capability for self-service file recovery.
> - **Distributed File System (DFS):** FSx supports DFS, which is a Windows Server feature that lets you logically group file shares on different servers and present them to users as a single, unified namespace. This simplifies data access and can be used for scaling and replication.
> - **Additional Features:** FSx also supports other Windows-native features like **data deduplication** to optimize storage usage and reduce costs.
> #### Performance and Exam Focus
> - **High Performance:** FSx is a high-performance file system designed for demanding workloads. It provides high throughput (from 8MB/s to 2GB/s), hundreds of thousands of IOPS, and consistent sub-millisecond latency.
> - **Exam Keywords:** For the exam, it's important to recognize the key features and use cases. FSx is the answer when a question mentions:
>     - High-performance, low-latency file storage for **Windows applications**.
>     - A requirement for **native Windows features** like VSS for user-driven restores or SMB access.
>     - The need to integrate with an **existing Active Directory**.
>     - A comparison with EFS, where FSx is the choice for Windows environments and EFS is the choice for Linux environments (using the NFS protocol).
> #### Definitions
> - **Windows Permission Model:** A security framework on NTFS file systems that uses **Access Control Lists (ACLs)** to define which users and groups can perform specific actions (e.g., Read, Write, Modify, Full Control) on a file or folder.
> - **Distributed File System (DFS):** A Windows Server feature that allows you to create a logical, unified namespace for multiple file shares that are physically located on different servers. This simplifies access for users and can improve availability.
> - **Directory Service:** A network service that stores information about network resources, such as users, groups, and computers. It provides a central, authoritative source for authentication and authorization. AWS offers managed versions of this service, such as **AWS Managed Microsoft AD**.

FSx for Windows File Server
- Fully managed native windows file servers/shares
- Designed for integration with Windows environments
- Integrates with Directory Service or Self-Managed AD
- Single or Multi-AZ within a VPC
- On-demand and scheduled backups
- Accessible using VPC, Peering, Direct Connect![[Pasted image 20250727204820.png]]
- We can use our own AD, or an AWS AD
- Supports lots of native Windows features
- High performance 
Key Features and Benefits
- VSS - User-Driven Restores
- Native file system accessible over SMB
- Windows permission model
- Supports DFS, scale-out file share structure
- Managed - no file server admin
- Integrates with DS AND your own directory