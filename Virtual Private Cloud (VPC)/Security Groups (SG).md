>[!note]- Post-Processing
>## Key Insights and Information from the AWS Security Groups Transcript:
>
>**1. Security Groups vs. Network Access Control Lists (NACLs):**
>
>* Both are used for security filtering in AWS, but operate differently.
>* Security groups are **stateful**, automatically allowing responses to allowed requests (e.g., if you allow inbound traffic on port 443, the response traffic is automatically allowed).
>* NACLs are **stateless** and require explicit rules for both inbound and outbound traffic.
>* Security groups are **more feature-rich** and operate higher on the OSI model, allowing for IP & CIDR-based rules and referencing AWS resources.
>* **NACLs are used for explicit denies**, while security groups rely on implicit denies (traffic not explicitly allowed is denied).
>
>**2. Security Group Limitations:**
>
>* **No explicit deny**: You can only allow or not allow traffic. You cannot block specific bad actors using security groups alone.
>
>**3. Security Group Attachment:**
>
>* Security groups are attached to **Elastic Network Interfaces (ENIs)**, not instances or subnets.
>* When you attach a security group to an instance, it's actually attached to the instance's primary ENI.
>
>**4. Security Group Features:**
>
>* **Advanced Functionality**: Security groups allow referencing other security groups and AWS resources within rules, enabling complex configurations.
>
>**5. Exam Tip:**
>
>* Remember that security groups are attached to ENIs, not instances or subnets.
>
>
>This information summarizes the key takeaways from the transcript and highlights important points for both exam preparation and real-world AWS usage.
>

- Stateful - so if we allow the request, then the response is automatically allowed
- No way to explicitly deny a specific bad actor > often why it's used in conjunction with NACLs
- Supports IP/CIDR and logical resources -> including other security groups and itself
- Attaches to ENI's (Elastic Network Interfaces), not instances 

>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**Security Groups vs. Network ACLs:**
>
>* **Security Groups:**
>    * Surround network interfaces (like the primary interface of an EC2 instance).
>    * Stateful: Automatically allow responses to requests they allow.
>    * **Cannot explicitly block traffic:**  You can only allow traffic from specific sources or ranges.
>    * Use **logical references** to simplify management and scaling.
>    * Best for allowing traffic to your VPC-based resources.
>* **Network ACLs:**
>    * Apply to subnets.
>    * Stateless: Each rule is evaluated individually.
>    * **Can explicitly block traffic:** Useful for blocking bad actors.
>    * Best for explicitly denying traffic at the subnet level.
>
>**Security Group Functionality:**
>
>* **Inbound and Outbound Rules:** Control traffic entering and leaving the network interface.
>* **Logical References:**
>    * Reference other security groups, simplifying management and scaling.
>    * Allows communication between instances with the referenced security group attached.
>    * Example: Web security group referencing the application security group allows web instances to communicate with any application instance.
>* **Self-Referencing:**
>    * Allows instances with the security group attached to communicate with each other.
>    * Useful for intra-app communication, auto-scaling groups, and high availability.
>
>**Best Practices:**
>
>* Use Network ACLs to explicitly block bad actors.
>* Use Security Groups to allow traffic to your VPC-based resources.
>* Leverage logical references in security groups for simplified management and scaling.
>
>
>
>**General Takeaways:**
>
>* Security groups and network ACLs work together to provide a layered security approach.
>* Understanding the differences and functionalities of each is crucial for effective security management in AWS.
>* Logical references in security groups offer powerful capabilities for simplifying and scaling your security configurations.
>

- SG is associated with the primary ENI of the instance 
- Applies to all traffic entering or leaving the ENI

SG Logical References
- Let's say we have a web instance that also needs to connect to our application instance
- We could use the IP of the instance, or range of the subnet to allow connection between the two in our SG
- But instead we reference the Web SG, and allow our app instance to accept inbound traffic from our anything associated with our web SG
- This is helpful because it scales well (we can add as many instances and as long as they are associated with our web SG, then they are able to connect to our app no problem)
SG Self References 
- Within an SG, an SG source is the same as anything with the SG attached
- Using a self reference means anything with this SG attached
- This scales with adds and removes from the SG
- For example, intra app communication (MS Domain Controllers)
	- IP Changes are automatically handled using this
- Basically just a rule within our SG saying that allow any traffic between any instances, etc. that are associated with this SG (the same one)