> [!note]- AI
> #### AWS Managed Microsoft AD
> - **Full-featured Active Directory:** This is a fully managed, real Microsoft Active Directory (AD) powered by Windows Server. It provides a native AD experience and supports features like schemas, trust relationships, and Group Policy.
> - **Application Support:** It is the ideal choice for migrating and running a wide range of AD-aware applications to the cloud, including SharePoint, Microsoft SQL Server, and custom .NET applications.
> - **Trust Relationships:** It can establish **trust relationships** (one-way or two-way) with your on-premises AD. This allows users to access resources in the AWS cloud using their existing on-premises credentials, simplifying identity management and security.
> - **Standalone Cloud Directory:** It is a standalone directory in the AWS cloud, managed by AWS for high availability and automated patching. It is the best option when you need a full Microsoft AD implementation in AWS.
> #### AD Connector
> - **Proxy Service:** AD Connector is not a directory itself; it is a **proxy** that connects AWS services to your existing on-premises Active Directory. It doesn't store any user credentials or directory data in the cloud.
> - **Hybrid Connectivity:** It requires **private network connectivity** (such as a VPN or AWS Direct Connect) between your VPC and your on-premises data center to function. All requests are proxied over this connection.
> - **Use Case:** This mode is perfect for organizations that want to leverage their existing on-premises AD for authentication and authorization without syncing any directory data to the cloud. AWS services can seamlessly access your on-premises directory through this proxy.
> - **Limitations:** If the private network connection fails, AD Connector will be unable to proxy requests, and services that depend on it will lose connectivity to your directory.
> #### Simple AD
> - **Cost-Effective Option:** Simple AD is a managed directory based on Samba 4, which is a Linux-based, Active Directory-compatible server. It is a cost-effective solution for basic directory needs.
> - **Feature Limitations:** It provides a subset of Microsoft AD features, such as user and group management, Kerberos-based single sign-on (SSO), and LDAP support. However, it does not support more advanced features like trust relationships, schema extensions, or Group Policy.
> - **Ideal Use Case:** Simple AD is best for small to medium-sized businesses or for basic AWS services that require a directory but do not need advanced Microsoft AD functionality or connectivity to an on-premises AD.
> #### Choosing the Right Directory Service
> - **Managed Microsoft AD:** Choose this for AWS applications that need a full-featured, managed Microsoft AD and for creating trust relationships with on-premises directories.
> - **AD Connector:** Use this when you have an existing on-premises AD and want to use it with AWS services without moving any directory data to the cloud. It's a proxy for your on-premises environment.
> - **Simple AD:** Use this for a simple, low-cost directory in the AWS cloud when no on-premises connectivity is required and only basic directory features are needed.

Directory
- Stores objects (users, groups, computers, servers, file shares) with a structure
- Multiple trees can be grouped into a forest
- Commonly used in Windows Environments
- Sign-in to multiple devices with the same username/password provides centralized management for assets
- Microsoft Active Directory Domain Services (AD DS) and SAMBA (Open-Source DS) are the most popular
Directory Service
- AWS Managed implementation that runs within a VPC, to implement HA -> deploy into multiple AZ's
- Some AWS services need a directory (Amazon Workspaces)
- Can be isolated or integrated with existing on-premises system, or act as a proxy back to on-premises
Simple AD Mode
- Standalone directory that uses Samba 4 for up to 500 users for small, and 5,000 users for large
- Integrates with AWS services, EC2 instances can join SimpleAD and Workspaces can use it for logins and maangement
- Not designed to integrate with any existing on-premises directory system such as Microsoft AD
AWS Managed Microsoft AD
- Full Microsoft AD DS Running in 2012 RS Mode (not emulated)
- Supports applications which require MS AD specific schema or schema updates
- Primary running location is in AWS, trust relationships can be created between AWS and on-prem directory services (through VPN or DirectConnect)
- Resilient if the VPN fails, services in AWS will still be able to access the local directory running in Directory Service
AD Connector
- Allows AWS services which need a directory to use an existing on-premises directory
- Only a proxy, no local functionality
- Primary directory is located on-premises requests from AWS are proxied back to the existing directory, if private connectivity fails, the AD proxy won't function, interrupting service at the AWS side
Picking between modes
- Simple AD - the default, simple requirements, just need a directory in AWS
- Microsoft AD - applications in AWS which need MS AD DS, or you need to trust AD DS
- AD Connector - use AWS services which need a directory without storing any directory info in the cloud, proxy to your on-premises directory