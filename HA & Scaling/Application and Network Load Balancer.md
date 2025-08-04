
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**Application Load Balancers (ALB)**
>
>* **Layer 7:** Understands HTTP, HTTPS, and other layer 7 protocols (SMTP, SSH, etc.). Can inspect headers, cookies, and application behavior.
>* **Consolidation:** Can handle multiple applications with different SSL certificates on a single load balancer, reducing the number of load balancers needed.
>* **Rules-based:**  Use rules to direct traffic based on host headers, HTTP headers, request methods, paths, query strings, and source IP. Can perform actions like forwarding, redirecting, providing responses, and authentication.
>* **Slower:**  More processing due to layer 7 analysis.
>* **No End-to-End SSL:** Terminates SSL connections on itself, establishing a new connection to the application instances.
>
>**Network Load Balancers (NLB)**
>
>* **Layer 4:** Handles TCP, TLS, and UDP protocols. No understanding of HTTP or HTTPS.
>* **Faster:**  Handles millions of requests per second with low latency due to simpler processing.
>* **Ideal for Non-Web Protocols:**  Suitable for applications using protocols like SMTP, SSH, game servers, and financial applications not using HTTP or HTTPS.
>
>**Choosing Between ALB and NLB:**
>
>* **ALB:** Use when you need to route traffic based on application-level information (headers, cookies, etc.) and can tolerate slightly slower performance.
>* **NLB:** Use when you need maximum performance and are handling non-web protocols or applications that don't require layer 7 analysis.
>
>**Exam Tips:**
>
>* Understand the differences between layer 4 and layer 7 load balancing.
>* Be aware of the limitations of ALB regarding end-to-end SSL encryption.
>* Consider performance requirements when choosing between ALB and NLB.
>* Recognize the specific use cases for each type of load balancer.
>
>
>
>This summary provides a concise overview of the key concepts discussed in the transcript.
>

>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**Network Load Balancers (NLB)**
>
>* **Pros:**
>    * **Unbroken End-to-End Encryption:** Forward TCP traffic directly to instances, preserving encryption layers.
>    * **Static IP Addresses:** Useful for whitelisting in strict security environments.
>    * **High Performance:** Ideal for handling millions of requests per second with low latency.
>    * **Protocol Flexibility:** Can handle protocols beyond HTTP and HTTPS.
>    * **Private Link:**  Enable services to be accessed by other VPCs.
>* **Cons:**
>    * **Limited Health Checks:** Only perform basic ICMP and TCP handshaking checks, not application-aware.
>
>**Application Load Balancers (ALB)**
>
>* **Pros:**
>    * **Detailed Health Checks:** Can perform application-aware health checks.
>    * **Additional Functionality:** Offer features like path-based routing and content caching.
>* **Cons:**
>    * **Less performant than NLB:** May not be suitable for extremely high-traffic scenarios.
>
>**Decision-Making:**
>
>* Use NLB for:
>    * Unbroken encryption
>    * Static IPs
>    * High performance
>    * Non-HTTP/HTTPS protocols
>    * Private Link requirements
>* Default to ALB for other scenarios.
>
>
>**Exam Tips:**
>
>* Remember the specific use cases for NLB and ALB.
>* Understand how NLBs enable unbroken end-to-end encryption.
>* Recognize the role of NLBs in private link functionality.
>

- v2 load balancers support rules and target groups. Host based rules using SNI and an ALB allows consolidation.
	- For example, we can have one load balancer that listens for two domains (catagram.io and doggogram.io) and directs traffic to the two separate target groups.
- Layer 7 load balancer - listens on HTTP and/or HTTPS
- No other layer 7 protocols (SMTP, SSH, Gaming)
- and no TCP/UDP/TLS listeners
- L7 content type -> cookies, custom headers, user location, and app behavior
- HTTP HTTPS (SSL/TLS) always terminated on the ALB - no unbroken SSL (good for security teams.)
	- A new connection is made to the application
- ALBs must have SSL certs if HTTPS is used
- ALBs are slower than NLB because there are more levels of the network stack to process
ALB Rules 
- Rules direct connections which arrive at listener
- Processed in priority order
- Default rule = catchall
- Rule conditions: host-header, http-header, http-request-method, path-pattern, query-string & source-ip
- If you have to forward encrypted connections without terminating them on the load balancer -> must use NLB
Network Load Balancer (NLB)
- Layer 4 load balancer -> TCP, TLS, UDP, TCP_UDP
- No visibility or understanding of HTTP or HTTPS
- No headers, no cookies, no session stickiness
- Really really fast (millions of RPS (requests per second), 25% of ALB latency)
- SMTP, SSH, Game Servers, financial apps (not http/s)
- Health checks just check ICMP/TCP Handshake -> not app aware
- NLB's can have static IP's which is useful for whitelisting
- Forward TCP to instances -> unbroken encryption
- Used with private link to provide services to other VPCs
When to use
- Unbroken encryption -> NLB
- Static IP for whitelisting -> NLB
- Fastest performance -> NLB
- Protocols not HTTP or HTTPs -> NLB
- Privatelink -> NLB
- Otherwise -> ALB (more features in general)