> [!note]- AI
> #### Amazon Athena: Serverless Query Service
> - **Purpose:** Athena is a serverless, interactive query service that makes it easy to analyze large amounts of data stored in Amazon S3 using standard SQL. It operates on a **schema-on-read** principle, where you define a table schema that maps to your raw data in S3, and Athena applies this schema only when a query is run.
> - **Architecture:**
>     - **Serverless:** There is no infrastructure to manage or set up. You simply connect to the service and run your queries.
>     - **Data Storage:** The data itself remains in Amazon S3. Athena tables do not store data; they are a metadata definition, or a "recipe," that tells Athena how to interpret the raw data files.
>     - **Data Formats:** Athena supports a wide variety of data formats, including plain text formats like CSV, TSV, and JSON, as well as columnar formats like Apache Parquet and ORC. Columnar formats are highly optimized for Athena's queries and can significantly reduce costs.
> #### Pricing and Optimization
> - **Cost Model:** Athena's pricing is based solely on the amount of data scanned by your queries. You are not charged for any infrastructure, and there are no upfront costs.
> - **Cost Optimization:** To reduce costs, you should optimize your original datasets in S3. This can be done by:
>     - **Using Columnar Formats:** Formats like Parquet and ORC allow Athena to read only the columns required by a query, not the entire dataset.
>     - **Partitioning:** Organizing your data in S3 by common query attributes (like date or region) allows Athena to skip entire partitions, drastically reducing the amount of data scanned.
> #### Advanced Features and Use Cases
> - **Ad-Hoc Queries:** Athena is ideal for ad-hoc or infrequent queries on large datasets, as it provides instant query capabilities without the need for data transformation or loading into a separate data warehouse.
> - **AWS Service Log Analysis:** Athena natively supports querying logs from various AWS services, including **VPC Flow Logs** and **AWS CloudTrail**.
> - **Federated Queries:** This feature allows Athena to run SQL queries across data from sources other than Amazon S3. It uses **data source connectors** to access and query data in-place from services like Amazon RDS, Amazon DynamoDB, and even on-premises databases.
> #### Definitions
> - **AWS Glue Data Catalog:** A centralized, serverless metadata repository that stores information about the data you have in S3 and other sources. Athena uses this catalog to find, access, and interpret the table definitions and schemas it needs to run a query.
> - **Athena Federated Query:** A feature that enables Athena to execute a single SQL query across multiple data sources, including non-S3 sources. This is achieved by invoking Lambda-based connectors that translate the query to the native format of the external data source.
> - **Data Source Connectors:** AWS Lambda functions that act as a translation layer for Athena's federated queries. These connectors are responsible for retrieving data from external sources (e.g., RDS, DynamoDB) and returning it to Athena in a format it can understand.
> - **CloudWatch Logs:** A monitoring service that collects, stores, and provides access to log files from a wide range of AWS services and on-premises servers. Athena can be used to query this data for in-depth analysis of application and system behavior.

- Serverless interactive querying service
- Ad-hoc queries on data, pay only data consumed
- Schema-on-read, table-like translation
- Original data never changed, remains on S3
- Schema translates data, relational-like when read
- Output can be sent to other AWS services
- Source Data: XML, JSON, CSV/TSV, AVRO, PARQUET, ORC, APACHE, CLODUTRIL, VPC FlOWLOGS
- Supports standard formats of structured, semi-structured and unstructured data. Source data stored on S3
- Tables are defined in advance in a data catalog and data is projected through when read, allows SQL-like queries on data without transforming source data.
- Billed based on data consumed during query, output can be sent to visualization tools
- No infrastructure
Considerations
- Queries where loading/transformation isn't desired
- Occasional/ad-hoc queries on data in S3
- Serverless querying scenarios, cost-conscious
- Querying AWS logs - VPC Flow Logs, CloudTrail, ELB Logs, Cost Reports
- AWS Glue Data Catalog and Web Server Logs
- w/ Athena Federated Query, other data sources