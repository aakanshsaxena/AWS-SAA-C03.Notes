
>[!note]- Post-Processing
>## Key Insights and Information from the EC2 Auto-Scaling Groups Transcript:
>
>**What are Auto-Scaling Groups?**
>
>*  Auto-scaling groups (ASGs) are the core component for automatically scaling EC2 instances based on demand.
>*  They work in conjunction with load balancers and launch templates to create elastic architectures.
>
>**How ASGs Work:**
>
>*  ASGs are defined by three key parameters: minimum size, desired capacity, and maximum size.
>*  They maintain the number of running EC2 instances at the desired capacity by provisioning or terminating instances as needed.
>*  ASGs can be managed manually or through scaling policies.
>
>**Scaling Policies:**
>
>*  **Manual Scaling:** Directly adjust the desired capacity.
>*  **Scheduled Scaling:**  Automatically scale up or down based on pre-defined schedules.
>*  **Dynamic Scaling:**  Automatically adjust the desired capacity based on predefined metrics:
>    *  **Simple Scaling:** Add/remove instances based on a single metric (e.g., CPU utilization).
>    *  **Step Scaling:** Define more granular rules for scaling based on metric thresholds.
>    *  **Target Tracking:** Maintain a desired target value for a metric (e.g., average CPU utilization).
>
>**Health Monitoring and Self-Healing:**
>
>*  ASGs monitor the health of instances using EC2 status checks or load balancer health checks.
>*  If an instance fails, the ASG terminates it and provisions a new one, ensuring continuous availability.
>
>**Integration with Load Balancers:**
>
>*  ASGs can be integrated with load balancers to automatically add and remove instances from the target group based on load.
>*  Load balancer health checks can be more application-aware than EC2 status checks, providing richer insights into application health.
>*  Careful selection of load balancer health checks is crucial to avoid false positives or negatives.
>
>**Key Takeaways:**
>
>*  ASGs are a powerful tool for automating and managing the scaling of EC2 instances.
>*  Different scaling policies cater to various needs and use cases.
>*  Integration with load balancers enables elastic architectures and seamless user experience.
>*  Careful consideration of health checks is essential for reliable and efficient scaling.
>
>
>
>Let me know if you need further clarification on any specific aspect of the transcript.
>

>[!note]- Post-Processing
>## Key Insights and Information from the Autoscaling Group Transcript:
>
>**Functionality:**
>
>* **Process Control:** Auto Scaling Groups (ASGs) allow you to control various processes like launching/terminating instances, adding them to load balancers, reacting to alarms, rebalancing across availability zones, and managing instance health.
>* **Instance Status:** You can set individual instances within an ASG to "standby" to temporarily suspend activities related to that instance. This is useful for maintenance.
>
>**Configuration Options:**
>
>* **Launch/Terminate:**  Control whether the ASG scales out (launches instances) or terminates instances based on alarms or scheduled actions.
>* **Add to Load Balancer:**  Decide if newly provisioned instances are added to the load balancer.
>* **Alarm Notification:** Enable or disable the ASG's response to CloudWatch alarms.
>* **AZ Rebalance:** Control whether the ASG redistributes instances across availability zones.
>* **Health Check:**  Turn on or off instance health checks for the entire ASG.
>* **Replace Unhealthy:**  Determine if the ASG replaces unhealthy instances.
>* **Scheduled Actions:** Enable or disable scheduled actions performed by the ASG.
>
>**Cost Optimization:**
>
>* **Free to Use:** ASGs themselves are free. Costs are incurred only for the resources they create (instances, load balancers, etc.).
>* **Cooldowns:** Use cooldowns to prevent rapid scaling and avoid excessive costs.
>* **Smaller Instances:** Consider using more smaller instances for finer control over compute resources and costs.
>
>**Integration and Best Practices:**
>
>* **Application Load Balancers:** ASGs work with Application Load Balancers to provide elasticity and abstract away instance details.
>* **Launch Templates/Configurations:** Define the "what" (instance type, configuration) while ASGs control the "when" and "where" (launch time and subnet).
>
>
>This summary provides a concise overview of the key points discussed in the transcript about Auto Scaling Groups in AWS.
>

Auto Scaling Groups
- Automatic scaling and self-healing for EC2
- Uses launch templates or configurations
- Has a minimum, desired, and a maximum size (e.g. 1:2:4)
- Keep running instances at the desired capacity by provisioning or terminating instances
- Scaling policies automate based on metrics
Scaling Policies
- Manual scaling - we can manually adjust the desired capacity
- Scheduled scaling - time based adjustment (ex. clothing drops)
- Dynamic Scaling
	- Simple - "CPU above 50% +1", "CPU below 50% - 1"
	- Stepped scaling - Bigger +/- based on difference
	- Target tracking - desired aggregate CPU = 40%, ASG handles the rest
- Cooldown periods = the time between scaling operations (helpful for keeping costs down)
ASG + Load Balancers
- ASG can use the load balancer health checks rather than EC2 status checks application awareness
- ASG instances are automatically added to or removed from the target group
Scaling Processes
- Launch and terminate - suspend and resume
- AddToLoadBalancer - add to LB on launch
- AlarmNotification - accept notification from CW
- AZRebalance - balances instances evenly across all of the AZ's
- HealthCheck - turns health checks on/off
- ReplaceUnhealthy - terminate unhealthy and replace
- ScheduledActions - scheduled on/off
- Standby - use this for instances 'InService vs Standby'
Final Points
- ASG are free, only resources created are billed
- Use cooldowns to avoid rapid scaling
- Think about more smaller instances rather to have granularity in your scaling
- Use with ALB's for elasticity - abstraction
- ASG defines when and where to add/remove instances, LT defines what instances to add 
