
>[!note]- Post-Processing
>## Key Insights and Information from the ECS Lesson:
>
>**What is ECS?**
>
>* Elastic Container Service (ECS) is a managed service that allows you to run Docker containers on AWS infrastructure.
>* It simplifies container orchestration by taking care of the administrative overhead of managing container hosts.
>* Think of it as the "EC2 for containers."
>
>**ECS Modes:**
>
>* **EC2 Mode:** You manage the underlying EC2 instances that run your containers. 
>* **Fargate Mode:** AWS manages the container hosts for you, providing a serverless approach.
>
>**ECS Architecture:**
>
>1. **Container Registry:** Store your container images (e.g., Amazon ECR or Docker Hub).
>2. **Container Definition:** Specifies the container image and exposed ports.
>3. **Task Definition:** Defines the entire application, including:
>    * One or more container definitions.
>    * Resources (CPU, memory) required by the task.
>    * Networking configuration.
>    * **Task Role:** An IAM role that grants temporary credentials to containers within the task, allowing them to access AWS resources securely.
>4. **ECS Cluster:** Where your tasks and services run.
>5. **ECS Service:** Defines how many copies of a task to run, scales the application, and provides high availability.
>
>**Key Concepts:**
>
>* **Task:** A self-contained application, which can consist of one or more containers.
>* **Service:**  Manages the scaling and availability of tasks.
>
>**When to Use Services:**
>
>* For business-critical applications.
>* When you need to handle significant incoming load.
>
>
>**Next Steps:**
>
>* Learn more about the technical differences between EC2 and Fargate modes.
>* Explore the detailed configuration options available in container and task definitions.
>* Practice deploying and managing tasks and services in an ECS cluster.
>

- ECS is a service that lets you run containers on AWS infrastructure
- Two modes: EC2 mode - you manage the EC2 instances that run your infrastructure, Fargate Mode - serverless approach
- You store your container in a container host, and give ECS the container definition (which specifies the docker image and open ports)
- Task definition specifies what needs to be done, consists of 1+ container definitions
	- Task roles can be given which allow temporary credentials to be granted to containers to let them use AWS services
- ECS Cluster = where your services and tasks run, ECS Service = how many copies to run, scaling your application, and provides HA
- ECS only supports Docker container standard
