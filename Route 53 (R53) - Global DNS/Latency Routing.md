
>[!note]- Post-Processing
>## Key Insights from Latency-Based Routing Video:
>
>**What is Latency-Based Routing?**
>
>* A routing policy in Route 53 designed to optimize performance and user experience.
>* Directs traffic to the AWS region with the lowest latency for the user.
>
>**How it Works:**
>
>1. **Hosted Zone & Records:** You need a hosted zone in Route 53 with multiple A records pointing to different IP addresses.
>2. **Record Regions:** Each record must have a specified region associated with it, indicating the location of its corresponding infrastructure.
>3. **AWS Latency Database:** AWS maintains a database of latencies between regions based on IP lookups.
>4. **User Location:** When a user makes a resolution request, Route 53 uses IP lookup to determine their location.
>5. **Latency-Based Selection:** Route 53 selects the record with the lowest latency to the user's location and returns it.
>
>**Benefits:**
>
>* **Improved Performance:** Traffic is routed to the closest infrastructure, reducing latency and improving user experience.
>* **Global Application Optimization:** Suitable for applications with infrastructure spread across multiple regions.
>
>**Additional Features:**
>
>* **Health Checks:**  Can be combined with health checks. If a record is unhealthy, Route 53 will choose the next lowest latency record.
>
>**Limitations:**
>
>* **Database Update Frequency:** AWS latency database is not real-time and may not account for local networking issues.
>
>**Overall:**
>
>Latency-based routing is a valuable tool for optimizing the performance of global applications by intelligently directing traffic based on user location and infrastructure proximity. While it has limitations, it significantly improves user experience compared to static routing.
>
>
>

- Supports one record with the same name in each AWS region
- AWS maintains a database of latency between the users general location and the regions tagged in the records
- The record returned is the one that offers the lowest estimated latency
	- Combined with health checks, it will return the lowest latency + healthy record
- Use latency-based routing when optimizing for performance and user experience
