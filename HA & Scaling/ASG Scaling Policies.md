
>[!note]- Post-Processing
>## Key Insights and Information from the Auto-Scaling Group Scaling Policies Lesson:
>
>**1. Auto-Scaling Group Scaling Policies:**
>
>* **Not Required:** Auto-scaling groups can function without scaling policies, relying on static `min size`, `max size`, and `desired capacity`. This is called **manual scaling**.
>* **Manual Scaling Use Cases:** Useful for testing, urgent situations, or cost control by keeping capacity fixed.
>* **Dynamic Scaling:**  Allows auto-scaling groups to adjust capacity based on changing demand.
>
>**2. Types of Dynamic Scaling:**
>
>* **Simple Scaling:**  Adds or removes a fixed number of instances based on alarm thresholds.
>    * **Pros:** Simple to implement.
>    * **Cons:** Inflexible, scales by a static amount regardless of the severity of the change.
>
>* **Step Scaling:** Adjusts capacity in steps based on the severity of the alarm breach.
>    * **Pros:** More flexible, scales proportionally to the change in the monitored metric.
>    * **Cons:** Requires more configuration.
>
>* **Target Tracking:** Maintains a target value for a predefined metric (CPU utilization, network in/out, ALB request count).
>    * **Pros:** Automatically adjusts capacity to keep the metric at the desired level.
>    * **Cons:** Limited to predefined metrics.
>
>* **SQS Queue Scaling:** Scales based on the approximate number of messages visible in an SQS queue.
>    * **Pros:** Useful for worker pools.
>    * **Cons:** Relies on SQS queue health and accuracy.
>
>**3. AWS Recommendation:**
>
>* AWS recommends **step scaling** over simple scaling due to its flexibility and ability to handle variable load patterns.
>
>**4. Visual Comparison:**
>
>* The lesson provides a visual comparison of simple and step scaling, demonstrating how step scaling adjusts capacity more proportionally to the change in the monitored metric.
>
>**5. Key Takeaways:**
>
>* Choose the appropriate scaling policy based on your application's needs and load patterns.
>* Step scaling generally offers better performance and flexibility compared to simple scaling.
>* Consider target tracking or SQS queue scaling for specific use cases.
>
>
>
>

- ASGs don't need scaling policies, they can have none
- Manual - min, max & desired - testing and urgent
- Simple scaling, but we should normally use step scaling
- Target tracking
- Scaling based on SQS - ApproximateNumberOfMessagesVisible -> as number of messages increase we want to scale up, and scale down when opposite
- Main difference between simple and step is the ability to scale in different ways (keep in mind though we will always stay between the minimum and maximum)

