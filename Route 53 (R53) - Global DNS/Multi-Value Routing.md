
>[!note]- Post-Processing
>## Key Insights from Multi-Value Routing in Route 53 Video:
>
>**What is Multi-Value Routing?**
>
>* A Route 53 routing policy that combines the benefits of simple and failover routing.
>* Allows you to create multiple records with the same name (e.g., multiple A records for "www").
>* Each record can be associated with a health check.
>
>**How it Works:**
>
>* When a query is received, Route 53 returns up to eight healthy records randomly selected from the pool.
>* Clients choose one of the returned records to connect to.
>* Unhealthy records are excluded from the response.
>
>**Use Cases:**
>
>* Improve application availability by using an active-active DNS approach.
>* Distribute traffic across multiple healthy resources that can handle requests.
>
>**Benefits:**
>
>* Enhanced availability through health checks and random record selection.
>* Flexibility in managing multiple resources serving the same purpose.
>
>**Comparison to Other Routing Policies:**
>
>* **Simple Routing:** No health checks, suitable for single resource deployments.
>* **Failover Routing:** Active backup architecture, typically used with S3 as a backup.
>* **Multi-Value Routing:** Ideal for scenarios with multiple healthy resources that can handle requests, requiring health checks and random selection.
>
>**Limitations:**
>
>* Not a replacement for load balancers, which handle network-level connection management.
>
>
>**Overall, multi-value routing in Route 53 provides a powerful tool for enhancing application availability and distributing traffic across multiple healthy resources.**
>

- Best of both worlds between simple and failover routing
- Supports multiple record with the same name
- Each record is independent and can have an associated health check
- Any records which fail health checks won't be returned when queried
- Up to 8 healthy records are returned, if more exist then 8 are randomly selected
- Client chooses and uses 1 value
- Multi value improves availability, not a replacement for load balancer
- Simple Routing best for when you only have one server available that you want to use
- Failover Routing best for when you are running in an active/passive configuration
- Multivalue Routing best when you have multiple servers available and functional (active/active)
