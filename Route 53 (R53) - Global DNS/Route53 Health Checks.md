
>[!note]- Post-Processing
>## Key Insights and Information from the Route 53 Health Checks Transcript:
>
>**What are Health Checks?**
>
>* Health checks are a core feature of Route 53, used to determine the health status of your applications and services.
>* They are separate from DNS records and are configured independently.
>* Health checks are performed by a globally distributed fleet of health checkers, ensuring comprehensive monitoring.
>
>**Types of Health Checks:**
>
>* **Endpoint Checks:** Assess the health of a specific endpoint (IP address or domain name) using TCP, HTTP, or HTTPS protocols.
>* **CloudWatch Alarm Checks:** React to CloudWatch alarms, which can be configured to trigger based on various application metrics and events.
>* **Calculated Checks:** Monitor the overall health of an application by combining the status of multiple individual health checks.
>
>**Health Check Features:**
>
>* **Frequency:** Checks occur every 30 seconds by default, but can be increased to every 10 seconds (at an additional cost).
>* **Protocols:** Supports TCP, HTTP, and HTTPS checks.
>* **String Matching:** HTTP and HTTPS checks can include string matching to verify the content of the response body.
>* **Failure Threshold:** Defines the number of consecutive failed checks before an endpoint is marked as unhealthy.
>* **Latency Graph:** Provides a visualization of the latency of health checks over time.
>
>**Health Check Architecture:**
>
>* Health checkers globally monitor applications associated with Route 53 records.
>* If more than 18% of health checkers report an endpoint as healthy, the overall health check is considered healthy.
>* Unhealthy records are typically not returned in response to DNS queries.
>
>**Benefits of Health Checks:**
>
>* **Improved Application Availability:** Route 53 can automatically redirect traffic away from unhealthy endpoints, ensuring high availability.
>* **Proactive Monitoring:** Health checks provide early warning of potential issues, allowing for timely intervention.
>* **Enhanced Application Performance:** By identifying and removing unhealthy endpoints, health checks can improve overall application performance.
>
>**Next Steps:**
>
>* The transcript encourages further exploration of health checks through a hands-on demo lesson.
>* The importance of understanding health checks for Route 53 design, implementation, and management is emphasized.
>
>
>
>

- Health checks are separate from, but are used by records
- Health checkers are located globally
- Health checkers check by default every 30s, but you can pay extra for this to be every 10s
- TCP, http/https, http/https with string matching
- Healthy or unhealthy
- Endpoint, CloudWatch Alarm, Checks of Checks (Calculated)
Architecture
- Let's say we have a record catagram.io
- We can associate a health check with our record which means that our application will be health checked by a globally distributed set of health checkers
- If 18%+ of health checkers report as healthy, the health check is healthy
- In most cases, an unhealthy record is NOT returned in queries
