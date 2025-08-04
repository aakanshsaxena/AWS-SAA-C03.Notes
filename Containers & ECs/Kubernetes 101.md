
>[!note]- Post-Processing
>## Kubernetes Fundamentals: Key Insights and Information
>
>This video provides a high-level overview of Kubernetes, an open-source container orchestration system. Here are the key takeaways:
>
>**What is Kubernetes?**
>
>* Automates the deployment, scaling, and management of containerized applications.
>* Makes running containers reliable, scalable, and efficient.
>* Exposes containerized applications to the outside world.
>* Cloud-agnostic, meaning it can be used on various platforms (including public clouds like AWS, Azure, and GCP).
>
>**Architecture:**
>
>* **Cluster:** A highly available cluster of compute resources organized as one unit.
>* **Control Plane:** Manages the cluster, handles scheduling, application management, scaling, and deployment.
>* **Nodes:** Virtual or physical servers that act as workers within the cluster and run containerized applications.
>* **Containerd (or another container runtime):** Software on each node that handles container operations.
>* **Kubelet:** Agent on each node that interacts with the control plane using the Kubernetes API.
>
>**Key Concepts:**
>
>* **Pods:** The smallest unit of computing in Kubernetes.
>    * Can contain one or more containers.
>    * Provide shared storage and networking for containers within a pod.
>    * Temporary and ephemeral; created, used, and disposed of as needed.
>* **Services:** Abstractions from pods that provide a consistent way to access applications.
>* **Jobs:** Ad hoc tasks within the cluster that create pods, run them until completion, and then finish.
>* **Ingress:** Allows external access to services within the cluster.
>* **Ingress Controller:** Software that configures the underlying hardware to allow ingress.
>* **Persistent Volumes (PVs):** Provide long-lasting storage that survives pod lifecycle changes.
>
>**Statelessness:**
>
>* Kubernetes generally assumes pods are stateless.
>* If your application requires persistent storage, use Persistent Volumes.
>
>**Further Learning:**
>
>* The video mentions follow-up videos on AWS EKS (Elastic Kubernetes Service) and deeper dives into specific Kubernetes topics.
>
>
>This overview provides a foundation for understanding Kubernetes. For more in-depth knowledge, explore the mentioned resources and continue learning about this powerful container orchestration system.
>

- An Open-Source container orchestration system that is used to automate the deployment, scaling, and management of containerization images -> lets you run containers in a reliable and scalable way
Cluster Structure 
- Cluster Nodes - VM or physical server which functions as a worker in the cluster
- Cluster Control Plane - manages the cluster, scheduling, applications, scaling and deploying
- containerd or Docker software for handling container operations
- kubelet - agent to interact with the cluster control plane
- Kubernetes API used for communication between control pane and kubelet agent
- Highly available cluster of compute resource which are organized to work as one unit
Cluster Detail
- Pods - the smallest units of computing in Kubernetes - shared storage and networking. One-container to one-pod is very common. Pods are not permanent
- Kube-proxy = network proxy. Runs on each node and coordinates networking with the control plane. Helps implement services and configures rules allowing comms. with pods from inside or outside the cluster
- Kube-apiserver - the front end for the Kubernetes control plane. What nodes and other cluster elements interact with. Can be horizontally scaled for HA and performance
- etcd - provides a highly-available key value store used within the cluster. Used as the main backing store for the cluster
- Kube-scheduler - identifies any pods within the cluster with no assigned node and assigns a node based on resource requirements, deadlines, affinity/anti-affinity, data locality, and any constraints
- kube-controller-manager 
	- Node controller - monitoring and responding to node outages
	- Job controller - one-off tasks (jobs) -> pods
	- Endpoint controller - populates endpoints (services <-> pods)
	- Service account & token controllers - accounts/API tokens
- Cloud-Controller-Manager - provides cloud-specific control logic. Allows you to link Kubernetes with a cloud providers APIs
Kubernetes Summary
- Cluster - a deployment of Kubernetes, management, orchestration
- Node - resources, pods are placed on nodes to run
- Pod - 1+ containers, smallest unit in kubernetes, often 1 container to 1 pods
- Service - abstraction, service running on 1+ pods
- Job - ad-hoc, creates one or more pods until completion
- Ingress - exposes a way into a service (ingress -> routing -> service -> 1+ pods)
- Ingress controller - used to provide ingress 
- Persistent Storage (PV) - typically pods have ephemeral storage like an instance, PV allocates volume whose lifecycle lives beyond any 1 pod using it