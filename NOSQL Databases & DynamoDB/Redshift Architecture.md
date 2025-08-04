> [!note]- AI
> #### Redshift Cluster Architecture
> - **Provisioned Service:** Amazon Redshift is a powerful, fully managed, and provisioned data warehouse service. It is designed for large-scale analytical processing and requires you to manage the underlying server cluster, unlike a serverless service like Athena.
> - **Cluster Components:** A Redshift cluster consists of two main types of nodes:
>     - **Leader Node:** This is the central point of contact for all client applications. The leader node receives queries, parses the SQL, develops an optimal execution plan, and then distributes the compiled code and data to the compute nodes for parallel processing. It also aggregates the final results from the compute nodes before returning them to the client.
>     - **Compute Nodes:** These are the "workhorses" of the cluster. They are responsible for storing the data and executing the query plan that is sent by the leader node. Each compute node is partitioned into units called "slices," and each slice has its own dedicated CPU, memory, and disk space for parallel processing.
> - **Massively Parallel Processing (MPP):** Redshift uses an MPP architecture to distribute data and query workloads across multiple compute nodes and their slices, allowing for high-performance and scalable analytics.
> #### Networking and Security
> - **Single Availability Zone:** A Redshift cluster is deployed within a single Availability Zone (AZ) in a private network, and it is not highly available by design.
> - **Enhanced VPC Routing:** By default, a Redshift cluster uses public routes to access other services on the internet. However, you can enable **Enhanced VPC Routing**, which forces all network traffic to and from your cluster to be routed through your VPC. This allows you to apply your own VPC-level security groups, network ACLs, and routing rules to all traffic for enhanced network security and control.
> - **Security Features:** Redshift integrates with IAM for granular access control and uses AWS KMS for at-rest and in-transit data encryption to secure your data.
> #### Data Loading and Use Cases
> - **Data Loading:** Data can be loaded into Redshift from a wide variety of sources, including Amazon S3, Amazon DynamoDB, streaming data via Kinesis Firehose, and other on-premises or cloud databases using the Database Migration Service (DMS).
> - **Use Cases:** Redshift is ideal for large-scale, complex analytical workloads, business intelligence, and reporting. It is not designed for frequent, ad-hoc queries on raw data; for those use cases, a serverless service like Athena would be a better choice.
> #### Definitions
> - **Leader Node:** The central coordinating node in a Redshift cluster that handles all client communications, parses SQL queries, develops execution plans, and distributes tasks to the compute nodes. It does not store user data but manages all client-facing and internal communications.
> - **ODBC (Open Database Connectivity):** An industry-standard Application Programming Interface (API) that provides a standard way for client applications (e.g., BI tools) to connect to and access data in a wide range of databases, including Amazon Redshift. It acts as a universal translator, enabling applications to be database-agnostic.
> - **Compute Nodes:** The workhorse nodes of a Redshift cluster. They are responsible for storing the data and executing the portions of a query plan assigned to them by the leader node. They operate in parallel to achieve high performance.
> - **Database Migration Service (DMS):** An AWS managed service that makes it easy to migrate relational databases, data warehouses, and other data stores to AWS quickly and securely. It supports both one-time migrations and continuous data replication, making it a viable option for loading data into a Redshift cluster.
> 

- Petabyte-scale Data warehouse
- OLAP (Column based) not OLTP (row/transaction)
- Pay as you use, similar to RDS
- Direct Query S3 using Redshift Spectrum
- Direct Query using other DBs using federated query 
- Integrates with other AWS tooling such as Quicksight and has SQL-like interface
Architecture
- Server-based 
- For ad-hoc queries look to Athena
- Redshift cluster is a private network, one AZ in a VPC
- Leader Node - query input, planning and aggregation
- Compute Node - performing queries of data
- VPC Security, IAM Permissions, KMS at rest encryption, CW Monitoring
- Redshift Enhanced VPC Routing - VPC networking, can be controlled by SG, NACL, VPC Gateway - for advanced networking controls
- Redshift cluster located in one AZ
- Applications communicate via the leader node, which splits the work to the compute nodes
- Automatic snapshots to S3 with retention, manual snapshots to S3 - Snapshots configured to copy to another AWS region 
- Connect w/ standard JDBC, ODBC compatible applications and visualization suites
- Firehose can stream data into redshift, DMS can migrate data into Redshift