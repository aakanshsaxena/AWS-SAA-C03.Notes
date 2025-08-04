
>[!note]- Post-Processing
>## EC2 Architecture Insights:
>
>This transcript provides a detailed explanation of the EC2 service architecture in AWS, focusing on key points relevant for exam preparation. Here's a breakdown of the key insights:
>
>**1. EC2 Instances:**
>
>* Virtual machines running on EC2 hosts, offering OS, CPU, memory, local storage, network access, and potentially GPUs.
>* Instances can be on shared or dedicated hosts.
>* Shared hosts are default, cost-effective, and isolated from other customers.
>* Dedicated hosts offer exclusive use of the hardware, higher cost, but no shared resources.
>
>**2. Availability Zone (AZ) Resilience:**
>
>* EC2 is an AZ-resilient service, meaning all components (hosts, network, storage) are within a single AZ.
>* If an AZ fails, instances on that host will also fail or be heavily impacted.
>* AZ awareness is crucial when designing EC2 solutions.
>
>**3. EC2 Host Components:**
>
>* Hosts have local CPU, memory, and instance store (temporary storage).
>* Instances can connect to Elastic Block Store (EBS) for persistent storage within the same AZ.
>
>**4. Networking and Storage:**
>
>* Instances are provisioned into a subnet within a VPC, with a primary elastic network interface mapped to the physical host.
>* Multiple network interfaces are allowed within the same AZ.
>* Instances cannot cross AZs with network interfaces or EBS volumes.
>
>**5. Instance Types and Generations:**
>
>* Instances come in different types and generations, which may reside on different host types based on their configuration (CPU, memory, storage).
>
>**6. Use Cases for EC2:**
>
>* Traditional OS and application compute needs.
>* Long-running compute requirements.
>* Server-style applications.
>* Applications with burst or steady-state load requirements.
>* Monolithic applications.
>* Migrating application workloads and disaster recovery.
>
>**7. EC2 as a Default:**
>
>* EC2 is generally the default compute service for traditional workloads.
>* Consider other services like Elastic Container Service or Lambda for specific niche requirements.
>
>
>
>**Key takeaway:** Understanding EC2 architecture, particularly its reliance on AZs, is crucial for designing and deploying solutions on AWS. While EC2 is a versatile service suitable for various workloads, it's essential to consider specific requirements and explore alternative services when needed.
>

EC2 Architecture 
- EC2 Instances are VMs (OS + Resources)
- EC2 Instances run on EC2 Hosts
- Shared Hosts = default, multiple AWS accounts sharing one host, all private
- Dedicated Hosts = One host for one AWS account
- Hosts run on a single AZ - AZ Fails, Host Fails, Instances Fail
- ALL components of an EC2 instance are locked to a single AZ (instance store, storage, data network) and CANNOT cross AZ's
	- EBS can be used to increase storage (Elastic Block Storage) but is also only available on the same AZ as the instance
EC2 Good For?
- Traditional OS+Application Compute
- Long-running compute
- Server style apps
- Burst or steady state load
- Monolithic application stacks
- Migrated application workloads/disaster recovery
Basically in any default use case -> use EC2 -> unless you have some specific reason to use a different compute service like ECS or Lambda
