
>[!note]- Post-Processing
>## Amazon AppFlow: Key Insights and Information
>
>This video provides a high-level overview of Amazon AppFlow, a fully managed integration service. 
>
>**Here are the key takeaways:**
>
>* **What it is:** AppFlow acts as middleware, enabling data exchange between applications using "flows."
>* **How it works:**
>    * Flows consist of a source connector and a destination connector, along with optional components.
>    * Connectors store configuration and credentials for accessing applications.
>    * Flows define field mappings, data transformations, filtering, and validation rules.
>* **Use cases:**
>    * Syncing data between applications (e.g., Salesforce to Redshift).
>    * Aggregating data from different sources.
>    * Copying data for storage or analysis (e.g., Zendesk tickets to S3).
>* **Benefits:**
>    * **Managed service:** Amazon handles infrastructure and maintenance.
>    * **Connectors:** Pre-built connectors for popular applications, with the option to build custom connectors.
>    * **Flexibility:**  Supports various data integration scenarios.
>* **Architecture:**
>    * Flows connect source and destination applications via configured connectors.
>    * Connections store application-specific credentials and configuration.
>    * Flows define data mapping and transformation rules.
>
>**Important points:**
>
>* AppFlow uses public endpoints by default, but can access private sources via private link.
>* Understanding the basic architecture is sufficient for most AWS exams.
>
>
>This video provides a good starting point for understanding AppFlow. For more in-depth knowledge, additional resources and videos are recommended.
>

- Fully managed integration service
- Exchange data between application (connectors) using flows
- Sync data across applications
- Aggregate data from different sources
- Public endpoints, but works with PrivateLink for privacy
- Supports some popular applications by default, but if not you need to create your own AppFlow Custom Connector SDK
- Usage:
	- Contact records from Salesforce to Redshift, or support tickets from Zendesk to S3
Architecture
- We create a flow with a source and destination connection
- We configure source to destination field mapping and optionally configure filters, validation, or data transformation
- We create connections that store configurations & credentials to access applications, and can be reused across many flows because they are defined seperately