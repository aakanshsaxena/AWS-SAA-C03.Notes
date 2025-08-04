
>[!note]- Post-Processing
>## Key Insights and Information from the AWS Global Accelerator Transcript:
>
>**What is AWS Global Accelerator?**
>
>* A product designed to optimize data flow from users to AWS infrastructure.
>* Improves performance by routing traffic through AWS's global network.
>* Uses Anycast IP addresses to direct traffic to the closest edge location.
>
>**Why is Global Accelerator Needed?**
>
>* Addresses the issue of latency and performance degradation for users located far from AWS infrastructure.
>* Internet traffic often takes indirect routes, adding hops and increasing delay.
>* Global Accelerator minimizes hops by routing traffic through AWS's dedicated network.
>
>**How Global Accelerator Works:**
>
>1. **Anycast IP Addresses:** Users connect to Global Accelerator via Anycast IP addresses.
>2. **Edge Locations:** Traffic is routed to the closest Global Accelerator edge location based on user location.
>3. **AWS Global Network:** Data traverses AWS's private network to the destination infrastructure.
>
>**Global Accelerator vs. CloudFront:**
>
>* **CloudFront:** Caches content at edge locations, improving content delivery performance.
>* **Global Accelerator:** Optimizes network performance for TCP/UDP applications by routing traffic through AWS's global network.
>* **Key Difference:** CloudFront caches content, while Global Accelerator does not.
>
>**When to Use Which Product:**
>
>* **CloudFront:** For content delivery, caching, and HTTP/HTTPS traffic optimization.
>* **Global Accelerator:** For global network performance optimization of TCP/UDP applications.
>
>**Exam Focus:**
>
>* Understand the architecture of Global Accelerator.
>* Differentiate between Global Accelerator and CloudFront based on their functionalities.
>* Identify scenarios where Global Accelerator is the appropriate solution.
>
>
>
>Let me know if you have any other questions.
>

- Global accelerator lets our clients connect to the global accelerator designated Anycast IP's (each standard accelerator is allocated two of these) over the public internet.
	- These IP's allow a single IP to be in multiple locations and routing moves traffic to the closest location
- After we reach this Anycast IP we are in a Global Accelerator edge location and from there the data transits globally across the AWS global network NOT public internet.
- -> Less hops, directly under AWS control, used and managed by AWS = significantly better performance
Key Concepts
- Moves the AWS network closer to customers
- Connections enter at edge using anycast IPs
- Trasnit over AWS backbone to 1+ locations
- Can be used for NON HTTP/S (TCP/UDP) - difference from CloudFront
- Global Accelerator also doesn't cache ANYTHING or do anything with HTTP/S, headers, cookies, signed links. It uses TCP/UDP protocol to get us from one place to another quicker.
