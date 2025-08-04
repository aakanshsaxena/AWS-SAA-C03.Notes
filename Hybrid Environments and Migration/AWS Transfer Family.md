> [!note]- AI
> #### AWS Transfer Family Architecture
> - **Managed File Transfer:** AWS Transfer Family is a fully managed service that provides highly available and scalable endpoints for secure file transfers. It eliminates the need to run and manage your own SFTP, FTPS, FTP, or AS2 servers.
> - **Storage Integration:** Transfer Family acts as a front-end for data stored in either Amazon S3 or Amazon EFS. This means that files are transferred directly to and from these storage services.
> - **IAM for Permissions:** User permissions are managed using **IAM roles and policies**. Each Transfer Family user is associated with an IAM role that defines their specific access to the underlying S3 bucket or EFS file system.
> - **Multi-AZ Availability:** The service is multi-AZ, providing built-in high availability and durability.
> #### Server Endpoint Types and Protocols
> AWS Transfer Family offers three main endpoint types, each with different access and security characteristics.
> - **Public VPC Endpoint:**
>     - Access is public via the internet.
>     - Uses a **dynamic IP address** that is not a static Elastic IP, so it's not suitable for clients that require IP whitelisting.
>     - Only supports the **SFTP protocol**.
>     - It lacks network access control via security groups or Network ACLs.
> - **VPC Internet Endpoint:**
>     - Access is public via the internet.
>     - Uses a **static Elastic IP address**, making it suitable for clients that need to whitelist a specific IP address.
>     - Supports **SFTP, FTPS, and AS2** protocols.
>     - Supports **network access control** through security groups and Network ACLs attached to the VPC.
> - **VPC Internal Endpoint:**
>     - Access is restricted to within your VPC and connected private networks (via VPN or Direct Connect).
>     - Uses a **private, static IP address**.
>     - Supports all protocols: **SFTP, FTPS, FTP, and AS2**. FTP is only available on this endpoint type for security reasons as it is not an encrypted protocol.
> #### Authentication and Security
> - **Multiple Authentication Methods:** Transfer Family supports several ways to authenticate users:
>     - **Service Managed:** User credentials (SSH public keys or passwords) are managed directly within the Transfer Family service.
>     - **AWS Managed Microsoft AD:** Integrates with an AWS Directory Service for Microsoft Active Directory to authenticate users against your existing directory.
>     - **Custom Identity Provider:** Allows you to use an external identity store for authentication by using a Lambda function to verify user credentials.
> - **Protocol-Specifics:** FTPS and FTP protocols only support authentication via a directory service or custom identity provider, while SFTP also supports service-managed users.
> - **Security:** All data is encrypted in transit using the specified protocol and can be encrypted at rest in S3 or EFS.
> #### Exam Focus and Use Cases
> - For the exam, it is crucial to understand the **differences between the three endpoint types** and their supported protocols and security features.
> - A key question is to identify the best endpoint type for a given scenario based on its access requirements (public vs. private), need for a static IP, and required protocol.
> - Use cases include B2B data exchange with partners, modernizing legacy file transfer workflows, and providing a secure file transfer endpoint for internal users.

- Managed file transfer service - Supports transferring TO or FROM S3 and EFS
- Provides managed "servers" which support protocols
- FTP - Unencrypted file transfer
- FTPS - File transfer with TLS encryption
- SSH File Transfer Protocol (SFTP) - File transfer over SSH
- Applicability Statement 2 (AS2) - not commonly used, structured B2B data
- Identities - service managed, directory service, custom (Lambda/APIGW)
- Managed file transfer workflows (MFTW) - serverless file workflow engine
Architecture
- We have an S3 bucket/EFS that we configure with IAM Roles for AWS Transfer Family, that we enable for 1+ protocols
- We have a user who can connect through a custom domain/domain and provide authentication with ID provider service, directory service, custom
Endpoint Type
Public
- Uses SFTP, dynamic IP, managed by AWS, can't control via IP lists
VPC - Internet
- Static public IP, can use SG and NACL to control access, uses SFTP or FTPS, can connect via DX/VPN, but not necessary
VPC - Internal
- Similar to VPC - Internet, but can't connect to internet
AWS Transfer Family
- Multi-AZ - Resilient and Scalable
- Provisioned server per hour $ + data transferred $
- FTP and FTPS - directory service or custom IDP only
- FTP - VPC only (cannot be public)
- AS2 VPC Internet/Internal only
- If you need to access S3/EFS, but with existing protocols
	- Integrating with existing workflows, or using MFTW to create new ones.