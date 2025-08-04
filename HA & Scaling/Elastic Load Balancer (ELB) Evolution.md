
>[!note]- Post-Processing
>## Key Insights and Information from the AWS Elastic Load Balancers Transcript:
>
>**1. Three Types of Elastic Load Balancers (ELB):**
>
>* AWS offers three types of ELBs: Classic Load Balancer (CLB), Application Load Balancer (ALB), and Network Load Balancer (NLB).
>* **Avoid using CLB:**  It's an older version 1 product with limited functionality and higher costs.
>
>**2. Version 1 vs. Version 2:**
>
>* **Version 2 (ALB and NLB) are preferred:**  They offer advanced features, better performance, and cost-efficiency.
>* **No scenarios favor version 1:** Migrate existing CLBs to version 2 products.
>
>**3. Classic Load Balancer (CLB):**
>
>* Introduced in 2009, it's one of the oldest AWS products.
>* Supports HTTP, HTTPS, and lower-level protocols.
>* Lacks HTTP understanding and advanced features.
>* Can be significantly more expensive due to limitations like supporting only one SSL certificate per load balancer.
>
>**4. Application Load Balancer (ALB):**
>
>* A version 2 load balancer designed for application layer (layer 7) traffic.
>* Supports HTTP, HTTPS, and WebSocket protocols.
>* Ideal for applications using these protocols.
>
>**5. Network Load Balancer (NLB):**
>
>* A version 2 load balancer designed for network layer (layer 4) traffic.
>* Supports TCP, TLS, and UDP protocols.
>* Suitable for applications not using HTTP or HTTPS, such as email servers, SSH servers, or custom protocol-based games.
>
>**6. Version 2 Advantages:**
>
>* Faster performance.
>* Support for target groups and rules for flexible load balancing based on various criteria.
>
>
>**7. Exam Focus:**
>
>* Understand the differences between ALB and NLB to choose the appropriate load balancer for specific scenarios.
>
>
>**Overall:** The transcript emphasizes the importance of migrating from the outdated Classic Load Balancer to the more advanced and efficient version 2 load balancers (ALB and NLB) for modern AWS deployments.
>

- 3 types of ELB available within AWS
- Split between v1 (AVOID) and v2
- Classic Load Balancer - v1
	- Not really layer 7, lacking features, 1 SSL certificate per CLB so it could take hundreds/thousands of ELB to properly use this whereas v2 ones could do it with a single ELB
- Application Load Balancer (ALB) - v2
	- Good for HTTP/HTTPS/WebSocket
- Network Load Balancer (NLB) - v2
	- Good for TCP, TLS, UDP
- V2 = faster, cheaper, support target groups and rules
