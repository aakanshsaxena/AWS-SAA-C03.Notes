
>[!note]- Post-Processing
>## Key Insights and Information from Aurora Serverless Transcript:
>
>**What is Aurora Serverless?**
>
>* Aurora Serverless is a database-as-a-service offering from AWS, similar to Fargate for ECS.
>* It removes the need to statically provision database instances, simplifying management and scaling.
>* You pay only for the resources used on a per-second basis.
>
>**Benefits of Aurora Serverless:**
>
>* **Simplicity:** Reduces complexity of managing database instances and capacity.
>* **Ease of Scaling:** Seamlessly scales compute and memory (ACUs) up or down based on demand.
>* **Cost-Effectiveness:** Only pay for resources consumed.
>* **Resilience:** Offers the same levels of cluster storage replication and availability as Aurora Provision.
>
>**Architecture:**
>
>* **Aurora Serverless Cluster:** Replaces provisioned clusters.
>* **ACUs (Aurora Capacity Units):** Represent compute and memory, allocated from a shared pool managed by AWS.
>* **Shared Proxy Fleet:** Manages connections between applications and ACUs, enabling transparent scaling.
>
>**Use Cases:**
>
>* **Infrequently Used Applications:** Ideal for low-volume sites with sporadic traffic.
>* **New Applications:** Scales dynamically based on unpredictable workloads.
>* **Variable Workloads:** Handles peaks and troughs in demand efficiently.
>* **Unpredictable Workloads:** Adapts to fluctuating loads with minimal manual intervention.
>* **Development and Test Databases:** Scales down to zero during inactivity, reducing costs.
>* **Multi-Tenant Applications:** Scales based on revenue, aligning infrastructure with income.
>
>**Exam Relevance:**
>
>* While not a major focus yet, Aurora Serverless will become increasingly important for exams in the future.
>
>
>This analysis provides a concise overview of Aurora Serverless, highlighting its key features, benefits, and use cases.
>

Concepts
- Scalable - ACU - Aurora Capacity Units
- We give a min and a max number of ACU's
- Cluster adjusts based on load
- Can go to 0 and be paused
- Consumption is billed per-second 
- Same resilience as Aurora (6 copies across AZs)
- User interacts with the cluster via an application is really via an AWS managed proxy fleet
Use Cases
- Infrequently used applications
- New applications
- Variable or unpredictable workloads
- Development and test DBs
- Multi-tenant applications where revenue scales with load
	- We're okay with paying more for usage if we're earning more from the usage
