
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>This transcript explains the fundamentals of Elastic Load Balancers (ELBs) in AWS, focusing on their architecture and benefits.
>
>**Core Concepts:**
>
>* **Multi-Tiered Architecture:** ELBs are crucial for separating application components into tiers (web, application, database) for better scalability and resilience.
>* **Abstraction:** ELBs abstract the underlying infrastructure, hiding complexities from users and applications. This allows for independent scaling and updates without disrupting service.
>* **Load Balancing:** ELBs distribute incoming traffic evenly across multiple instances within a tier, ensuring no single instance is overloaded and improving overall performance and availability.
>* **Cross-Zone Load Balancing:**  A key feature that allows load balancing across availability zones, ensuring even distribution of traffic and high availability. This was historically a limitation, but is now enabled by default for Application Load Balancers.
>
>**Types of ELBs:**
>
>* **Internet-facing:**  Nodes have public IP addresses, accessible from the internet. Can handle traffic from both public and private instances.
>* **Internal:** Nodes have private IP addresses, accessible only within the VPC.
>
>**Important Points:**
>
>* **DNS Record:** ELBs have a DNS name that directs traffic to all active nodes.
>* **Node Scaling:** ELBs automatically scale the number of nodes based on traffic load.
>* **Listener Configuration:** Controls which protocols and ports the ELB listens to and how traffic is routed.
>* **IP Address Requirements:** ELBs require a minimum of 8 free IP addresses per subnet they are deployed in.
>
>**Exam Focus:**
>
>The transcript emphasizes the importance of understanding cross-zone load balancing for the exam.
>
>
>**Overall, the transcript provides a clear and concise introduction to Elastic Load Balancers, covering their key features, benefits, and important considerations for deployment and configuration.**
>

![[Pasted image 20250722235037.png]]

- When creating well structured applications, we want to have ELBs at each tier and ASGs at each tier
- This allows abstraction and connection for the customers without interruption
	- For example, if we just have ELB then any scaling could potentially disrupt customers as instances are stopped and started
	- By using this architecture we have the ELB nodes connect with the ASG which creates abstraction and let's them figure out what to connect to without interruptions
- It also lets each tier scale as it needs without having to scale the whole website/application, for example if we need extra instances for the application tier ASG will automatically add these for the application tier without touching the other tiers
Cross-Zone LB
- Allows us to split the work evenly between all the instances in all the AZ's
- For example if we have an ELB in two AZ's, AZ-A and AZ-B, and AZ-A has four instances and AZ-B has one instance, then historically each AZ ELB Node would receive 50% of the connections, but this would mean each instance in AZ-A only handles 12.5% and AZ-B instance handles 50%
- Cross-Zone LB lets the nodes in either AZ split the traffic between all five of the instances so the AZ-B node can send traffic to an instance in AZ-A to even it properly
**Exam Powerups**
- ELB is a DNS A Record pointing at 1+ nodes per AZ
- Nodes (in one subnet per AZ) can scale
- Internet-facing means nodes have public IPv4 IPs
- Internal is private only IPs
- EC2 doesn't need to be public to work with a LB
- Listener configuration control what the LB does
- 8+ free IPs per subnet, and /27 subnet to allow scaling
