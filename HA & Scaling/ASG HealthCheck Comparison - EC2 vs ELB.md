
>[!note]- Post-Processing
>## Key Insights and Information about Auto-Scaling Groups and Health Checks:
>
>**1. Auto-Scaling Groups and Health Checks:**
>
>* Auto-scaling groups use health checks to monitor the health of instances within the group.
>* If an instance fails a health check, it's replaced, automatically healing the group.
>
>**2. Types of Health Checks:**
>
>* **EC2 Checks (Default):**  Any status except "running" is considered unhealthy (stopping, stopped, terminated, impaired).
>* **ELB Checks:** 
>    * Instance must be running AND pass the load balancer health check.
>    * **Application Load Balancers:**  Allow application-aware checks (specific page, text pattern matching).
>* **Custom Health Checks:** External systems can mark instances as healthy or unhealthy.
>
>**3. Health Check Grace Period:**
>
>* Default: 300 seconds (5 minutes).
>* Configurable value allowing instances to launch, bootstrap, and configure before failing a health check.
>* **Importance:**  
>    * Prevents continuous provisioning and termination cycles if applications need time to start up.
>    * Must be set long enough to accommodate application launch and configuration processes.
>
>**4. Exam Relevance:**
>
>* Auto-scaling groups and health checks are important concepts for exams.
>* Understanding grace periods is crucial for troubleshooting autoscaling issues.
>
>
>**5. Key Takeaways:**
>
>* Auto-scaling groups use health checks to maintain a healthy pool of instances.
>* Choose the appropriate health check type based on your application needs.
>* Configure a sufficient health check grace period to avoid continuous provisioning cycles.

ASG Health Checks
- EC2 (Default), ELB (Can be enabled) & Custom
- EC2 - any state besides running is considered unhealthy
	- Stopping, Stopped, Terminated, Shutting Down or Impaired (not 2/2 status)
- ELB - to be healthy an instance must be running and passing ELB health check
	- These can also be more application aware since they run on layer 7, and can be configured to check for certain pages or text matching
- Custom - instances marked healthy & unhealthy by an external system
- Health check grace period (Default 300s) - delay before starting checks
	- Allows for systems to launch, bootstrapping, and application to start
	- Can cause instances to be continuously terminated and provisioned, so make sure that it is adequately long to allow instances to be started properly without being put into this loop
