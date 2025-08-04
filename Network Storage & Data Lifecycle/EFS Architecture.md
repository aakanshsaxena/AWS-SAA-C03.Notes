
>[!note]- Post-Processing
>## Key Insights and Information from the AWS EFS Lesson:
>
>**What is EFS?**
>
>* Elastic File System (EFS) is a network-based file system service offered by AWS.
>* It provides shared storage accessible to multiple Linux EC2 instances simultaneously.
>* EFS is based on the NFS (Network File System) protocol, specifically version 4.
>
>**Benefits of EFS:**
>
>* **Scalability:** Allows for easy scaling of applications by adding or removing EC2 instances without losing data.
>* **Self-healing architecture:** Data is stored centrally, so it's not lost if an instance fails.
>* **Statelessness:** Promotes stateless EC2 instances, making them more portable and easier to manage.
>* **Centralized media storage:**  Ideal for storing media files like images, videos, and audio, eliminating redundancy and improving efficiency.
>
>**EFS Architecture:**
>
>* Runs within a VPC.
>* File systems are created within EFS and use POSIX permissions for access control.
>* Mount targets are deployed within subnets of the VPC and provide access points for EC2 instances.
>* Multiple mount targets in different availability zones ensure high availability.
>
>**EFS Access:**
>
>* **Private:** By default, accessible only within the VPC where it's provisioned.
>* **Hybrid networking:** Can be accessed from on-premises networks using VPC peering, VPN, or Direct Connect.
>
>**EFS Features:**
>
>* **Linux-only:** Officially supported only on Linux EC2 instances.
>* **Performance modes:**
>    * **General Purpose:** Suitable for most use cases, offering low latency.
>    * **Max.io:** Designed for high-throughput, parallel applications.
>* **Throughput modes:**
>    * **Bursting:** Scales throughput based on file system size, similar to GP2 volumes.
>    * **Provisioned:** Allows specifying dedicated throughput requirements.
>* **Storage classes:**
>    * **Standard:** For frequently accessed files.
>    * **Infrequent Access (IA):** For less frequently accessed files, offering lower cost.
>* **Lifecycle policies:** Enable moving data between storage classes based on access patterns.
>
>
>
>**Exam Preparation:**
>
>* Understand the EFS architecture and key components.
>* Know the different performance modes, throughput modes, and storage classes.
>* Be aware of EFS's limitations (Linux-only support).

- An implementation of NFSv4
- EFS filesystems can be mounted in Linux and shared between many EC2 instance
- Private service, via mount targets inside a vpc
- Can be accessed from on-premises using VPN or AWS direct connect
- Linux only
- General purpose and MAX I/O performance modes
- General purpose is the default for majority of use cases
- Max I/O can increase latency
- Bursting and provisioned throughput modes
- Standard and Infrequent Access (IA) classes
- Lifecycle policies can be used with classes
