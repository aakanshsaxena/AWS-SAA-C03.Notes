
>[!note]- Post-Processing
>This transcript discusses different types of NoSQL databases, focusing on their structure, strengths, and use cases. Here's a breakdown of the key insights:
>
>**1. Key-Value Stores:**
>
>* **Structure:** Simple key-value pairs, no schema or tables.
>* **Strengths:** Extremely fast and scalable due to their simplicity.
>* **Use Cases:** In-memory caching, storing simple data like user sessions or product information.
>
>**2. Wide Column Stores:**
>
>* **Structure:** Each item has one or more keys (partition key and optional sort key), and attributes.  
>* **Strengths:** High performance and scalability, good for large datasets with flexible schema.
>* **Use Cases:** DynamoDB (AWS), storing user profiles, product catalogs, and content management systems.
>
>**3. Document Databases:**
>
>* **Structure:** Store data as documents (JSON, XML, etc.) with unique IDs.
>* **Strengths:** Flexible schema, good for nested data and hierarchical relationships.
>* **Use Cases:** Content management systems, e-commerce product catalogs, user profiles.
>
>**4. Column-Based Databases:**
>
>* **Structure:** Data stored by columns, not rows.
>* **Strengths:** Optimized for analytical queries and reporting on specific columns.
>* **Use Cases:** Data warehousing, reporting, and analytics.
>
>**General Takeaways:**
>
>* NoSQL databases offer different approaches to data storage and querying, each with its strengths and weaknesses.
>* Choosing the right NoSQL database depends on the specific use case, data structure, and performance requirements.
>* Understanding the key characteristics of each type of NoSQL database is crucial for making informed decisions.
>
>
>
>Let me know if you have any other questions about this transcript!
>

Key-Value
- Straight forward, key and a value
- No schema, structure, very scalable and fast
Wide Column Store
- Certain amount of keys but at least one key (partition key) and then a table containing the attributes which have no schema
Document
- Interacting with whole documents or deep attribute interactions
Column store 
- Columns are stored together (instead of typical rows). Ideal for reporting or when all values for a specific attribute are required

>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**1. Graph Databases vs. Relational Databases:**
>
>* **Relational databases:** Store data in tables with relationships defined through keys. Relationships are calculated on the fly when querying.
>* **Graph databases:** Store data as "nodes" (objects) and relationships as "edges" with names and directions. Relationships are explicitly stored, making queries faster for relationship-driven data.
>
>**2. Advantages of Graph Databases:**
>
>* **Efficiency:** Queries involving complex relationships are faster because the relationships are already stored.
>* **Scalability:** Can handle massive amounts of complex relationships.
>* **Flexibility:** Relationships are dynamic and can be easily modified.
>
>**3. Use Cases for Graph Databases:**
>
>* Social media platforms
>* HR systems
>* Any application with complex interconnected data
>
>**4. Identifying Graph Database Scenarios:**
>
>* Look for keywords like "social media," "complex relationships," or scenarios involving many interconnected entities.
>
>**5. Exam Tips:**
>
>* Be aware of the differences between graph and relational databases.
>* Consider graph databases when analyzing exam questions involving relationship-heavy data.
>
>
>**In essence, the transcript highlights the strengths of graph databases in handling complex relationships efficiently, making them suitable for specific data types and applications.**
>

Graph DB
- Store the data and the relationships between data as well
- Can store attributes about the relationships, make it much quicker to query about these relationships
![[Pasted image 20250720232559.png]]