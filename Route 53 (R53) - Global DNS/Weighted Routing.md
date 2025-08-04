
>[!note]- Post-Processing
>## Key Insights and Information from Weighted Routing in Route 53 Video:
>
>**What is Weighted Routing?**
>
>* A routing policy in Amazon Route 53 that allows you to distribute traffic across multiple records (e.g., IP addresses) based on specified weights.
>* Useful for simple load balancing and A/B testing of software versions.
>
>**How it Works:**
>
>1. **Hosted Zone:** Starts with a hosted zone containing records (e.g., A records pointing to IP addresses).
>2. **Record Weights:** Each record is assigned a weight.
>3. **Traffic Distribution:** Traffic is distributed proportionally to the assigned weights.
>    *  The total weight of all records determines the percentage of traffic each record receives.
>    *  A weight of 0 means the record is never returned.
>4. **Health Checks:** Can be combined with health checks. If a selected record is unhealthy, it is skipped and the process repeats until a healthy record is selected.
>
>**Use Cases:**
>
>* **Simple Load Balancing:** Distribute traffic evenly across multiple servers.
>* **A/B Testing:** Send a percentage of traffic to a specific server running a new software version for testing.
>
>**Advantages:**
>
>* Easy to set up and configure.
>* Flexible traffic distribution based on weights.
>* Can be used with health checks for reliable traffic routing.
>
>**Limitations:**
>
>* Only provides basic load balancing capabilities.
>* Not suitable for complex routing scenarios.
>
>
>
>**Overall:**
>
>Weighted routing is a straightforward and effective tool for simple load balancing and A/B testing in Route 53. It offers flexibility in traffic distribution and can be easily integrated with health checks for enhanced reliability.
>

- Weighted Routing has records and each record is assigned a weight
- This weight divided by the sum of all the weights is the % of times that that record will be used
	- For example if we have 3 records with weight 40, 40, 20. Then Record 1 = 40%, Record 2 = 40%, Record 3 = 20%
- A 0 weight means a record will never be returned unless all are 0 then all are considered
- If incorporating health checks,
	- Do process normally, if a chosen record is unhealthy the process of selection is repeated until a healthy record is chosen
- Best used for simple load balancing or testing new versions (etc. if we want 5% of users to visit our record that links to a newer version of our software)
