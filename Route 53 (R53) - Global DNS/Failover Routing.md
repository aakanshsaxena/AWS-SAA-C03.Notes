
>[!note]- Post-Processing
>## Failover Routing: Key Insights and Information
>
>This transcript explains the concept of **failover routing** in a hosted zone. Here are the key takeaways:
>
>**What is it?**
>
>* Failover routing allows you to define **multiple records with the same name** (e.g., "WWW") in a hosted zone.
>* These records point to different resources, acting as **primary and secondary endpoints**.
>* A **health check** is crucial, typically performed on the primary record.
>
>**How it works:**
>
>* If the **primary record is healthy**, traffic is routed to its associated resource (e.g., an EC2 instance).
>* If the **primary record fails the health check**, traffic is automatically rerouted to the **secondary record's** resource (e.g., an S3 bucket).
>
>**Use case:**
>
>* **Active-passive failover**: Route traffic to the healthy resource and automatically switch to the backup in case of failure.
>
>**Example:**
>
>* Primary: EC2 instance running "catagram" application.
>* Secondary: S3 bucket for serving static content.
>
>**Next steps:**
>
>* A demo video will illustrate the concept of failover routing in action.
>
>
>**In essence, failover routing ensures high availability by automatically switching to a backup resource when the primary resource becomes unavailable.**
>

- We have a primary and secondary record within our hosted zone
- Failover routing includes a health check, if health check is healthy then the primary record is used
- If unhealthy, then queries return the secondary record of the same name
- Common architecture is to use failover for a "out of band" failure (like S3 as a backup, versus EC2 would be our main)
- Use when you want to configure active passive failover

