
>[!note]- Post-Processing
>## EKS Key Insights and Information:
>
>**What is EKS?**
>
>* EKS (Elastic Kubernetes Service) is AWS's managed implementation of Kubernetes.
>* It allows you to run Kubernetes clusters on AWS without managing the underlying infrastructure.
>* Kubernetes is cloud-agnostic, so EKS offers flexibility if you want to avoid vendor lock-in.
>
>**EKS Deployment Options:**
>
>* **AWS:** Standard deployment within AWS infrastructure.
>* **AWS Outposts:** Running EKS on a mini-AWS environment on-premises.
>* **EKS Anywhere:** Deploying EKS clusters on-premises or in other cloud providers.
>* **EKS Distro:** Open-source EKS distribution for more control.
>
>**EKS Architecture:**
>
>* **Control Plane:** Managed by AWS, scales automatically, runs across multiple availability zones, and integrates with AWS services like ECR, Elastic Load Balancers, IAM, and VPCs.
>* **Nodes:** Can be self-managed EC2 instances or managed node groups (provisioned and managed by AWS).
>* **Fargate:** Option to run pods without managing EC2 instances, similar to ECS Fargate.
>
>**Key Considerations:**
>
>* **Node Type:** Choose based on your requirements (Windows, GPUs, Inferentia, etc.). Check the capabilities list for each node type.
>* **Persistent Storage:** EKS supports EBS, EFS, and FSx for persistent storage needs.
>
>**EKS and VPCs:**
>
>* Two VPCs are typically used:
>    * AWS-managed VPC for the control plane.
>    * Custom VPC for worker nodes.
>* Worker nodes connect to the control plane via ENIs injected into the custom VPC or a public control plane endpoint.
>
>**Further Learning:**
>
>* This video provides a high-level overview.
>* Deep dive videos and demos are available for specific topics.
>
>
>This summary highlights the essential aspects of EKS, its deployment options, architecture, and key considerations for choosing the right configuration.
>

- AWS managed Kubernetes - open source & cloud agnostic
- Can use through AWS, Outposts, EKS Anywhere, EKS Distro
- Control plane scales and runs on multiple AZs
- Integrates with AWS services (ECR, ELB, IAM, VPC)
- EKS Cluster = EKS Control Plane & EKS Nodes
- etcd distributed across multiple AZs
- Nodes - self managed, managed node groups, or fargate pods
- Check node type (windows, GPU, Inferentia, Bottlerocket, Outposts, Local zones)
- Storage providers include EBS, EFS, FSx

- AWS Managed VPC contains the EKS Control plane which injects ENIs into the customer VPC to allow kube-api traffic between the worker nodes (EC2) and the control plane.
	- Can also use a public control plane endpoint that also allows admin
	- Any consumption of EKS service is done through ingress configurations which start from customer VPC