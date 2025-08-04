
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**ECS Cluster Modes:**
>
>* **EC2 Mode:**
>    * You manage EC2 instances that act as container hosts.
>    * You are responsible for capacity planning, scaling, and availability.
>    * Benefits: Cost-effective for large, consistent workloads, utilizes existing reserved instances or spot pricing.
>    * Best for: Price-conscious organizations with large, consistent workloads.
>* **Fargate Mode:**
>    * AWS manages the underlying infrastructure (container hosts).
>    * No need to manage EC2 instances.
>    * Pay-as-you-go pricing based on container resource consumption.
>    * Benefits: Reduced management overhead, ideal for small, burst, or sporadic workloads.
>    * Best for: Organizations prioritizing ease of use and minimizing management overhead, regardless of workload size.
>
>**ECS Concepts:**
>
>* **Cluster:** A logical grouping of EC2 instances or Fargate tasks.
>* **Task:** A single instance of a container running within a cluster.
>* **Service:** A group of tasks that maintain a desired number of running containers.
>* **Container Registry:** A repository for storing container images.
>
>**General ECS Considerations:**
>
>* **Containerization Benefits:** Isolation, portability, consistent environment, efficient resource utilization.
>* **Choosing ECS:** If you are already using containers or want to adopt them, ECS is a strong option.
>* **Choosing EC2 vs. ECS:**
>    * EC2: For applications requiring full control over the underlying infrastructure.
>    * ECS: For containerized applications, prioritizing ease of use and managed infrastructure.
>
>**Fargate Specifics:**
>
>* Tasks run on a shared infrastructure platform managed by AWS.
>* Tasks are injected into your VPC with their own network interfaces and IP addresses.
>* You only pay for the resources consumed by your containers.
>
>
>This transcript provides a solid foundation for understanding the key concepts and considerations surrounding ECS cluster modes.
>

ECS/Fargate Service handles
- SchedulingandOrchestration
- ClusterManager
- PlacementEngine
ECS - EC2 Mode
- You are responsible for managing the underlying EC2 Hosts that run the container images
- You use the container registry + container definition + task definition -> give to ECS
- You can use an auto scaling group (AWS service that horizontally scales for you) 
- Requires to manage capacity and availability for your cluster
- ECS handles the number of tasks that are deployed
- Pay for the hosts 
ECS - Fargate Mode
- No servers to manage
- AWS maintain a shared Fargate platform
- Use same container and task definitions -> allocated to the Fargate platform
- Still use VPC but in a different way than EC2 Mode, tasks are injected into our VPC and given an ENI
	- Running from shared Fargate infrastructure and then injected into our VPC
- Only pay for containers that you are using
EC2 vs ECS (EC2) vs Fargate
- If you use containers: ECS>EC2
- Large workload - price conscious - EC2 Mode
	- Can make use of reservation and spot pricing
- Large workload - overhead conscious - Fargate
- Small/Burst workloads - Fargate
- Batch/Periodic workloads - Fargate