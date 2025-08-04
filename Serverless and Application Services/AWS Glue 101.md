
>[!note]- Post-Processing
>## AWS Glue: Key Insights and Information
>
>This lesson provides a high-level overview of AWS Glue, focusing on its key features and how it compares to other AWS ETL solutions like Data Pipeline.
>
>**What is AWS Glue?**
>
>* **Serverless ETL service:** Glue automates the process of extracting, transforming, and loading data between various sources and destinations.
>* **Managed service:** AWS handles all infrastructure management, scaling, and maintenance, eliminating the need for manual configuration and administration.
>* **Cost-effective:** You only pay for the resources consumed during ETL jobs.
>
>**Key Features:**
>
>* **Data Catalog:** Glue automatically crawls data sources (S3, RDS, JDBC-compatible databases, DynamoDB, Kinesis, Kafka) and generates a central metadata repository. This improves data discoverability and promotes data sharing across the organization.
>* **Glue Jobs:** Serverless ETL jobs that can be triggered manually, event-driven, or scheduled. They allow you to define complex data transformations using scripts and leverage Glue's managed compute resources.
>* **Wide range of data sources and destinations:** Glue supports various data stores and streaming platforms, enabling seamless data integration across your data ecosystem.
>
>**Glue vs. Data Pipeline:**
>
>* **Glue is serverless:** You don't manage infrastructure, leading to easier deployment and cost optimization.
>* **Data Pipeline uses EMR clusters:** It requires more manual configuration and management.
>* **Glue is generally recommended for new projects:** It's more cost-effective and easier to use.
>
>**Exam Tips:**
>
>* **Focus on Glue's serverless nature and cost-effectiveness.**
>* **Look for keywords like "serverless," "ad hoc," or "cost-effective" when comparing Glue and Data Pipeline.**
>* **Understand the role of the Glue Data Catalog in improving data discoverability and sharing.**
>
>
>**Overall, AWS Glue is a powerful and versatile ETL service that simplifies data integration and transformation in the cloud.**
>

- Serverless ETL (Extract, Transform & Load) vs datapipeline which can do ETL and uses servers (EMR clusters)
- Moves and transforms data between source and destination
- Crawls data sources and generates AWS Glue Data Catalog
- Data Source: Stores
	- S3, RDS, JDBC Compatible DB & DynamoDB
- Data Source: Streams
	- Kinesis Data Stream & Apache Kafka
- Data Targets
	- S3, RDS, JDBC Databases
Data Catalog
- Persistent metadata about data sources in region
- One catalog per region per account
- Avoids data silos
	- A data silo is when data is stored in one department, system, or tool but isn’t easily accessible to other parts of an organization
- Amazon Athena, Redshift Spectrum, EMR & AWS Lake Formation all use Data Catalog by configuring crawlers for data sources
AWS Glue Architecture
- We have data sources from supported platforms that crawlers connect to, determine schema and create metadata in the data catalog which we can access via the management console 
- Or we extract data and create a Glue Job with a script that extracts the data into a supported data target, or if resources are required, glue allocates from a AWS Warm Pool to perform the ETL processes