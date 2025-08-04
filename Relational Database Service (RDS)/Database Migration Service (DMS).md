
>[!note]- Post-Processing
>## AWS Database Migration Service (DMS) - Key Insights
>
>This lesson focuses on AWS Database Migration Service (DMS), a crucial tool for database migrations in the AWS ecosystem. 
>
>**Here are the key takeaways:**
>
>**What is DMS?**
>
>* A managed service for migrating databases to and within AWS.
>* Simplifies complex database migrations, handling tasks like replication and data transfer.
>* Supports a wide range of database engines (MySQL, Aurora, SQL Server, MariaDB, MongoDB, PostgreSQL, Oracle, Azure SQL, and more).
>
>**How DMS Works:**
>
>* Uses a replication instance (an EC2 instance) to run replication tasks.
>* Requires defining source and destination endpoints pointing to the source and target databases.
>* One endpoint must be within AWS.
>
>**Types of DMS Migrations:**
>
>* **Full Load:** Migrates existing data from source to target, creating tables as needed.
>* **Full Load + CDC (Change Data Capture):** Migrates existing data and replicates ongoing changes. 
>* **CDC Only:** Replicates only data changes, useful for initial bulk data transfer using other tools.
>
>**Schema Conversion Tool (SCT):**
>
>* A standalone tool used for schema conversions between different database engines.
>* **Not** used for migrations between compatible engines.
>* Used for large migrations or when network transfer is impractical.
>* Works with both OLTP and OLAP databases.
>
>**DMS and Snowball:**
>
>* For large migrations, DMS can leverage Snowball devices for bulk data transfer.
>* SCT extracts data into a generic format for transfer via Snowball.
>* Data is loaded into S3, and DMS migrates it to the target database.
>
>**Exam Tips:**
>
>* DMS is a safe default for database migration questions involving AWS.
>* SCT is only used for migrations involving a change in database engine.
>
>
>**Overall, DMS is a powerful tool for database migrations in AWS, offering flexibility and efficiency for various scenarios.**
>

- A managed database migration service
- Runs on a replication EC2 instance
- Source and destination endpoints = source and target DB
- One endpoint MUST be AWS
- Replication instance performs the migration between source and destination endpoints which store connection information for source and target DB
- Wide range of common DB support
- Jobs can be:
	- Full Load (one off migration of all data), need to shut down DB for this
	- Full Load + CDC - full load + captures any changes to the data made in that time
	- CDC only - if you want to use an alternative method to transfer the bulk DB data like native tooling
- Schema Conversion Tool (SCT) can help with Schema conversion
Schema Conversion Tool (SCT)
- Used when converting from one DB engine to another
- Including DB -> S3 (migrations using DMS)
- SCT is not used when migrating between DB's of the same type (on-premises MySQL -> RDS MySQL)
- Works with OLTP and OLAP database types 
	- OLTP (Online Transaction Processing) = Databases optimized for **real-time, high-volume transactional workloads**, like inserting and updating records
	- OLAP (Online Analytical Processing) = Databases optimized for complex queries, aggregations, and data analysis, often over large datasets (e.g., dashboards, BI tools).
DMS & Snowball
- Larger migrations may be TB's in size, moving data over networks take time and consume capacity
- DMS can use snowball products
	- Step 1: Use SCT to extract data locally (converts to generic type) and moved onto a snowball device
	- Ship the device back to AWS who loads it onto a S3 bucket
	- DMS migrates from S3 into the target store
	- Change Data Capture (CDC) can capture changes and via S3 intermediary they are also written to the target DB