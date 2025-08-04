> [!note]- AI
> #### Amazon Kendra: An Intelligent Search Service
> - **Purpose:** Kendra is an intelligent search service powered by machine learning. It is designed to act like a human expert, providing accurate and relevant answers to a wide range of user questions from across your organization's data sources.
> - **Architecture:**
>     - **Index:** The core component of Kendra is the **index**, which is a searchable data repository that contains all the documents and information you want to be able to search.
>     - **Data Sources:** A data source is the original location of your data (e.g., S3, Confluence, RDS, etc.). You configure Kendra to connect to these sources, and it ingests and indexes the data into a searchable format.
>     - **Synchronization:** Kendra can be scheduled to automatically synchronize with your data sources, ensuring that the information in your index remains current with the original source.
> #### Natural Language and Question Types
> - **Intent-Based Search:** Kendra uses natural language processing (NLP) to understand the intent behind a user's question. This allows it to provide a direct answer rather than just a list of links.
> - **Supported Question Types:**
>     - **Factoid Questions:** Simple questions that have a single, definitive answer (e.g., "Who is the CEO?").
>     - **Descriptive Questions:** More complex questions that require a longer, more detailed answer (e.g., "How do I fill out my expense report?").
>     - **Keyword Questions:** Handles ambiguous keyword searches (e.g., "IT address") by disambiguating the terms and providing a relevant answer.
> - **Data Indexing:** Kendra is capable of indexing both **structured data** (like FAQs or database tables) and unstructured data (like PDF documents, text files, and HTML pages).
> #### Integration and Use Cases
> - **Backend Service:** Kendra is not a user-facing application but a backend service. It is designed to be integrated into your own applications, websites, or chat bots via **APIs**. This allows you to build a custom search experience for your users while offloading the complexity of the search engine to AWS.
> - **Access Control:** Kendra integrates with **IAM Identity Center** to provide single sign-on (SSO) and manage user permissions. This ensures that users can only search for and access documents they are authorized to see in the original data source.
> - **Common Use Cases:** Kendra is ideal for building knowledge base search, IT help desk solutions, and internal search portals that allow employees to find information quickly without asking a human expert.
> #### Definitions
> - **Data Source:** A data repository or location that Amazon Kendra connects to and indexes documents or content from. Examples include S3 buckets, Microsoft SharePoint, relational databases, and Confluence.
> - **Structured Data:** Data that has a standardized, predefined format, such as rows and columns in a relational database or fields in a JSON document. It is easy for machines to process and analyze.
> - **IAM Identity Center:** A cloud-based service that centrally manages workforce user access to multiple AWS accounts and applications. It provides single sign-on (SSO) and is often connected to an external identity provider like Microsoft Entra ID.
> - **APIs (Application Programming Interfaces):** A set of rules and protocols that enable different software applications to communicate and interact with each other. Kendra provides a set of APIs that developers use to submit queries and retrieve search results from a Kendra index.

- Intelligent search service, designed to mimic interacting with a human expert
- Supports wide range of question types
	- Factoid - who, what, where
	- Descriptive - How do I get my cat to stop being a jerk?
	- Keyword - What time is the keynote address (address can have multiple meanings) - Kendra helps determine intent
- Index = searchable data organized in an efficient way
- Data Source = where your data lives, Kendra connects and indexes from this location
	- S3, Confluence, Google Workspace, RDS, OneDrive, Salesforce, Kendra Web Crawler, Workdocs, FSX
- Synchronize with index based on a schedule
- Documents - structured (FAQs), unstructured (HTML, PDFs, text)
- Integrates with AWS services (IAM, Identity Center (SSO))