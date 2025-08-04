> [!note]- AI
> #### Amazon SageMaker: A High-Level Overview
> - **Purpose:** Amazon SageMaker is a fully managed service that provides a complete platform for machine learning. It covers the entire machine learning (ML) lifecycle, from data preparation to building, training, deploying, and monitoring models.
> - **ML Lifecycle:** SageMaker simplifies and accelerates the ML lifecycle with a comprehensive set of tools. It enables data scientists and developers to:
>     - **Prepare Data:** Connect to various data sources and prepare data for training.
>     - **Build and Train:** Use a wide range of built-in algorithms or custom code to build and train ML models.
>     - **Deploy and Host:** Deploy trained models as highly available, production-ready endpoints for real-time or batch inference.
>     - **Monitor:** Continuously monitor model performance in production to detect anomalies.
> #### Core Architecture and Concepts
> - **SageMaker Studio:** This is the web-based, integrated development environment (IDE) for the entire ML lifecycle. From SageMaker Studio, users can access notebooks, run training jobs, and manage their projects and resources from a single pane of glass.
> - **SageMaker Domain:** A SageMaker domain is the central administrative and security-related component. It acts as a logical container for all a team's ML assets, users, and projects. Domains are used to centrally manage security policies, VPC configurations, and access controls for all users and resources.
> - **Containers and Compute:** The heavy lifting of ML—training and inference—is performed on powerful EC2 instances that are optimized for ML workloads. SageMaker abstracts away this infrastructure management. It uses **Docker containers**, which include the operating system, frameworks, libraries, and tools needed for a specific ML task. SageMaker provides many pre-built containers, but you can also use your own.
> - **Model Hosting:** Once a model is trained, SageMaker can host it as an endpoint. You can choose a persistent endpoint for real-time inference or a serverless endpoint that automatically scales to zero for cost-efficiency.
> #### Pricing and Cost Management
> - **Pay-as-you-go:** There is **no cost for the SageMaker service itself**. You only pay for the underlying AWS resources that you use.
> - **Primary Cost Components:** The primary costs associated with SageMaker come from:
>     - **Compute Instance Usage:** This is the largest cost component. You are charged for the instance type and duration of use for training, processing, and hosting models. ML compute resources can be very large and expensive, so choosing the right instance type is critical.
>     - **Storage:** You are charged for the storage used for notebooks, data (e.g., in Amazon S3), and model artifacts.
>     - **Data Transfer:** Data transfer fees apply, particularly for data moving out of the AWS network.
> - **Exam Relevance:** For most AWS exams, a high-level architectural understanding of SageMaker is sufficient. You should know its purpose, the components that make up the ML lifecycle, and how it simplifies the process by being a fully managed service.
> 

- Collection of packages and features - fully managed Machine Learning (ML) Service
- Fetch, clean, prepare, train, evaluate, deploy, monitor/collect
- Sage Maker Studio - build, train, debug and monitor ML models 
- Sagemaker Domain - EFS volume, users, apps, policies, VPCs -> isolation
- Containers - docker containers deployed to ML EC2 instance - ML environments (OS, Libs, Tooling)
- Hosting - deploy endpoints for your ML models
- Sagemaker has no cost - the resources it creates do - complex pricing