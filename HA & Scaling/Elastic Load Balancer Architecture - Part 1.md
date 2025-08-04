 
>[!note]- Post-Processing
>## Key Insights and Information from the Elastic Load Balancer Architecture Lesson:
>
>**1. Load Balancer Function:**
>
>* Accepts connections from users and distributes them across registered backend compute resources (e.g., EC2 instances).
>* Abstracts the physical infrastructure from users, allowing for scaling and failover without user impact.
>
>**2. Load Balancer Architecture:**
>
>* **Multiple Nodes:** A single load balancer object consists of multiple nodes deployed across availability zones.
>* **DNS Resolution:** Load balancers are assigned a single DNS record (A record) that resolves to all nodes, ensuring equal distribution of requests.
>* **Availability Zones:** Load balancers are deployed in multiple availability zones for high availability and redundancy.
>* **Subnet Configuration:**  When provisioning a load balancer, you select one subnet in each availability zone. Load balancer nodes are deployed within these subnets.
>
>**3. Load Balancer Types:**
>
>* **Internet-Facing:** Nodes have public IP addresses, accessible from the public internet. Can connect to both public and private backend instances.
>* **Internal:** Nodes have only private IP addresses, used for communication within a VPC.
>
>**4. Listener Configuration:**
>
>* Controls which protocols and ports the load balancer listens on.
>* Determines how incoming connections are handled.
>
>**5. IP Address Requirements:**
>
>* **Minimum:** 8 free IP addresses per subnet (AWS recommends a /27 subnet or larger).
>
>**6. Scaling:**
>
>* Load balancers can automatically scale up or down based on traffic load.
>* Additional nodes are provisioned within the configured subnets as needed.
>
>**7. Use Cases:**
>
>* Distributing traffic across multiple backend instances.
>* Providing high availability and redundancy.
>* Separating application tiers for independent scaling.
>
>
>
>This summary provides a concise overview of the key points covered in the lesson on elastic load balancer architecture.
>

- Configured to run in 2+ AZ's. 1+ ELB Nodes are placed into a subnet in each AZ and scale with load
- Each ELB is configured with an A record DNS name that resolves to the ELB Nodes
- Internet facing ELB/ELB Nodes have public IPs but can connect to public and private EC2 instances, while Internal only have private IPs and can only connect to private EC2 instances
- Load balancer nodes are configured with listeners which accept traffic on a port and protocol and communicate with targets on a port and protocol
- We need 8+ free IPs per subnet and a /27 or larger subnet to allow for scale (technically can be /28 but we would only have 11 free IPs then)
- Internal load balancers can be used to allow scaling between application tiers
