
>[!note]- Post-Processing
>## Key Insights and Information from RDS Proxy Video Transcript:
>
>**What is RDS Proxy?**
>
>* A fully managed database proxy service for RDS and Aurora.
>* Acts as an intermediary between applications and databases.
>* Auto-scales and highly available by default, reducing admin overhead.
>
>**Why Use RDS Proxy?**
>
>* **Reduced Connection Overhead:** 
>    * Maintains a pool of long-term connections to the database, eliminating the cost and time of constantly opening and closing connections.
>    * Multiplexing allows fewer database connections to handle more client requests, especially beneficial for smaller database instances.
>* **Improved Database Performance:**
>    * Lessens the load on the database server by reducing connection churn and utilizing multiplexing.
>* **Enhanced Resilience:**
>    * Abstracts database failures from applications, ensuring continuous service.
>    * Handles failover events transparently, allowing applications to remain connected without interruption.
>* **Simplified Security:**
>    * Enforces SSL/TLS connections for secure communication.
>
>**Use Cases:**
>
>* **Applications with High Connection Volumes:**
>    * Serverless applications like Lambda functions.
>    * SaaS applications requiring low latency and high availability.
>* **Applications Using Small Database Instances:**
>    * T2 or T3 instances where resources are limited.
>
>**Key Features:**
>
>* **Connection Pooling:** Efficiently manages database connections.
>* **Multiplexing:** Uses fewer database connections for a larger number of client connections.
>* **Auto-Scaling and High Availability:** Ensures continuous service and performance.
>* **Secure Communication:** Enforces SSL/TLS connections.
>* **Failover Management:** Minimizes downtime during database failures.
>* **VPC-Only Access:** Provides secure access within a VPC or private VPC-connected networks.
>
>**Exam Tips:**
>
>* Understand the benefits of RDS Proxy for performance, resilience, and security.
>* Recognize the use cases where RDS Proxy is most beneficial.
>* Be familiar with the key features and functionalities of RDS Proxy.
>
>
>
>This summary provides a concise overview of the key insights and information presented in the video transcript.
>

Why?
- Opening and closing connections consumes resources, takes time and creates latency
- With serverless, every lambda invocation opens and closes
- Handling failure of DB instances is hard and doing it within your app can add risks
- DB proxies helps but managing them is not easy which is why we use something like RDS Proxy
- Applications connect to our proxy which connect in the backend in longterm connection pools to our DB
Architecture
- RDS Proxy -> DB instance connections can be reused which avoids lag of establishment, usage & termination for each invocation
- Each Lambda function connects to the proxy which is much quicker than direct to DB
- Abstracts clients away from DB failure or failover events
- Client -> Proxy connection is established and waits even if the target DB is unresponsive
- ***Multiplexing in AWS RDS Proxy** refers to the ability of the proxy to **manage and reuse a smaller pool of database connections**, while handling many concurrent application connections. This improves scalability and efficiency—especially for serverless or bursty workloads.*
When to use?
- Too many connections errors
- DB instances using T2/T3 (burst or smaller instances)
- AWS Lambda - time saved/connection reuse + IAM Auth
- Long running connections that require low latency (like SAAS apps)
- Where resilience to DB failure is a priority, RDS proxy can reduce the time for failover and make it transparent to the application
Key Facts
- Fully managed DB Proxy for RDS/Aurora with auto scaling, HA by default
- Provides connection pooling which reduces DB load
- Only accessible from a VPC
- Accessed via proxy endpoint 
- Can enforce SSL/TLS and reduce failover time by over 60% while also abstracting failure away from your applications