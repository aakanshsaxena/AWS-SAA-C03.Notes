
>[!note]- Post-Processing
>## RDS Architecture Insights:
>
>This video provides a foundational overview of Amazon Relational Database Service (RDS). Here are the key takeaways:
>
>**What is RDS?**
>
>* **Database Server as a Service:** RDS manages the underlying database server hardware, operating system, and much of the maintenance, allowing you to focus on your applications.
>* **Not a Database as a Service:** You get a database server instance, not just a database. You can host multiple databases on a single instance.
>
>**RDS Engines:**
>
>* Supports open-source engines like MySQL, MariaDB, PostgreSQL, and commercial engines like Oracle and Microsoft SQL Server.
>* Licensing implications apply for commercial engines.
>
>**Differentiating RDS from Aurora:**
>
>* Amazon Aurora is a separate, custom-built database engine by AWS with improved features and compatibility with some RDS engines.
>
>**RDS Architecture:**
>
>* **Runs within a VPC:** Not publicly accessible, requires subnets within a specific AWS region.
>* **DB Subnet Groups:** Define the subnets RDS instances can use.
>* **Availability Zones:** RDS instances can be deployed across multiple availability zones for high availability.
>* **Public vs. Private Subnets:** Public subnets allow internet access to instances, while private subnets restrict access to within the VPC.
>
>**Instance Features:**
>
>* **Multiple Databases:** Each instance can host multiple databases.
>* **Dedicated EBS Storage:** Each instance has its own dedicated storage provided by Elastic Block Storage (EBS).
>* **Multi-AZ:** Enables synchronous replication between primary and standby instances in different availability zones.
>* **Read Replicas:** Asynchronous replicas for scaling read load or adding resilience across regions.
>* **Backups:** Automated backups to managed S3 buckets, ensuring data safety and recovery.
>
>**Cost Considerations:**
>
>* **Instance Size and Type:** Larger, more feature-rich instances cost more.
>* **Multi-AZ:** Additional cost due to the use of multiple instances.
>* **Storage:** Per-gig monthly fee for storage usage.
>* **Data Transfer:** Cost per gig of data transferred in and out of the instance.
>* **Backups and Snapshots:** Free snapshots up to the instance storage size, then a per-gig monthly fee for additional storage.
>* **Commercial Engines:** Additional costs based on licensing agreements.
>
>
>This video provides a good starting point for understanding RDS. Further videos will delve deeper into specific features

- Database Server as a Service 
	- Can run multiple databases on one DB Server (Instance)
- Choice of DB Engines (MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL Server) -> some with licensing costs some are open source
- Managed service with no access to OS or SSH access
Architecture 2
- RDS works within a VPC
- If you configure multi AZ then RDS automatically creates a standby RDS server in a seperate AZ that using synchronous replication to always have most recent data
- DB Subnet Groups tell RDS where it's allowed to launch database
- RDS Instance can have 1+ database
- Each RDS instance has its own dedicated EBS storage and we can make backups and snapshots to S3
- RDS can be accessed from VPC or any connected private networks, or configured with public addressing from public internet (BAD)
Costs
- Loosely based on EC2
- Cost 1 - Instance Type + Size
- Cost 2 - Multi AZ or not
- Cost 3 - Storage type & amount
- Cost 4 - Data transferred
- Cost 4 - Backups + Snapshots (You get backup storage equal to size of provisioned DB instance for free)
- Licensing