
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**Problem:**
>
>* Traditional security appliances (firewalls, IDS/IPS, data analysis tools) can be difficult to scale and manage in dynamic environments like AWS.
>* Tight coupling between applications and security appliances creates single points of failure and limits flexibility.
>
>**Solution: Gateway Load Balancers (GWLB)**
>
>* GWLBs are AWS products designed to run and scale third-party security appliances at scale.
>* They enable horizontal scaling of security appliances, ensuring high availability and performance.
>
>**Architecture:**
>
>* **Gateway Load Balancer Endpoints:** Similar to interface endpoints in VPCs but can be added to route tables, allowing them to participate in traffic flows.
>* **Gateway Load Balancer (GWLB):**
>
>    * Forwards packets to backend security appliances running on EC2 instances.
>    * Uses Geneve tunneling to encapsulate packets and maintain original source and destination IP addresses.
>    * Provides flow stickiness, ensuring consistent traffic flow to a single security appliance for stateful analysis.
>    * Abstracts away the complexity of managing multiple security appliances, allowing for resilience and flexibility.
>
>**Benefits:**
>
>* **Scalability:** Horizontally scale security appliances based on load.
>* **Resilience:** Multiple security appliances provide redundancy and failover protection.
>* **Flexibility:** Use a variety of third-party security appliances without vendor lock-in.
>* **Abstraction:** Simplifies management of security infrastructure.
>
>**Use Cases:**
>
>* Deploying and scaling third-party security appliances in AWS.
>* Leveraging existing security skills and investments.
>* Meeting specific security requirements or feature needs not met by native AWS services.
>
>**Example:**
>
>* The transcript describes a typical architecture where a web application running in a private subnet is protected by security appliances in a separate VPC.
>* GWLB manages traffic flow between the application and security appliances, ensuring transparent inspection and protection.
>
>
>**Overall:**
>
>Gateway Load Balancers offer a powerful solution for deploying and managing third-party security appliances at scale in AWS, providing flexibility, resilience, and ease of management.
>

- Helps you run and scale 3rd party applications, things like firewalls, intrusion detection and preventions systems
- For inbound and outbound traffic (transparent inspection and protection)
- uses GWLB endpoint, traffic enters/leaves via these endpoints, and the GWLB balances across multiple backend appliances
- Traffic and metadata is tunneled using GENEVE protocol
How it works
- Client connects to GWLBE which connects to GWLB sends to horizontally scaling appliances via GENEVE encapsulation. 
	- Original packets remain unaltered encapsulated through to appliances and back
![[Pasted image 20250723183646.png]]

1. Client accesses the catagram.io webapp, which connects to IGW which redirects to GWLBE, which sends the data to GWLB, packets are encapsulated and sent to security appliances and sent back to GWLB, which sends to GWLBE, which sends to ALB which redirects traffic based on load and instances. 
2. On the way back we send the data from the instance to the ALB, then to the GWLBE, which sends the packet to the GWLB, which then again sends it to the security appliance and receives the data back, sends it back to the GWLBE which looks at the route table and defaults to sending to IGW who sends it back to the client