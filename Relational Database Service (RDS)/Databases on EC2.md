
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>This lesson discusses the pros and cons of running databases directly on EC2 instances within the AWS cloud.
>
>**Reasons to Consider Running Databases on EC2:**
>
>* **OS Level Access:**  Some applications or situations might require direct access to the database operating system, which managed services might not provide. 
>* **Specific Database Versions:** AWS might not offer support for niche or very specific database versions, requiring installation on EC2.
>* **Unique Architectural Requirements:**  Projects might demand very specific OS and database version combinations not readily available in managed services.
>* **Business Demand:** Sometimes, despite the drawbacks, clients or organizations might insist on running databases on EC2.
>
>**Reasons to Avoid Running Databases on EC2:**
>
>* **Increased Admin Overhead:** Managing both the EC2 instance and the database server adds significant administrative burden, including patching, upgrades, backups, and disaster recovery.
>* **Single Availability Zone Limitation:** EC2 instances reside within a single availability zone, making the database vulnerable to zone failures.
>* **Missed Features:** AWS managed database products often offer advanced features, performance optimizations, and built-in replication that are not available when running databases on EC2.
>* **Limited Scalability:** EC2 is a traditional server model with limited auto-scaling capabilities compared to managed database services.
>* **Higher Costs:** Running databases on EC2 incurs ongoing costs for the EC2 instance, storage, and potential additional resources.
>
>**Overall:**
>
>While there are valid reasons for running databases on EC2 in specific situations, the transcript strongly emphasizes the disadvantages and encourages exploring AWS managed database services whenever possible.
>
>
>**Key Takeaways:**
>
>* Carefully evaluate the need for running databases on EC2.
>* Understand the implications of single availability zone deployment.
>* Consider the administrative overhead and potential performance limitations.
>* Explore AWS managed database services for their advanced features and cost-effectiveness.
>

Why you might
- Access to DB Instance OS (Normally not really required)
- Advanced DB Option Tuning (DBROOT)
- Vendor demands
- DB or DB Version AWS don't provide
- Specific OS/DB Combination AWS don't provide
- Architecture AWS don't provide 
- Architecture AWS don't provide (replication/resilience)
- Decision makers just want it
- Keep in mind though there are valid reasons to want EC2 DB
Why you shouldn't
- Admin overhead to manage EC2 and DBHost
- Backup and disaster recovery management becomes complex
- EC2 is a single AZ
- AWS DB products have been built out with features and performance
- EC2 is on or off - no serverless or easy scaling
- Replication takes skills, setup time, monitoring & effectiveness control
