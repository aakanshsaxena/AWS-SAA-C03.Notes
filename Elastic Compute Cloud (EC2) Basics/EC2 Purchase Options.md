
>[!note]- Post-Processing
>## Key Insights from EC2 Purchase Options Lesson:
>
>**On-Demand:**
>
>* **Default option:**  Start here for all projects.
>* **Predictable pricing:** Consistent cost per second while running.
>* **No discounts:**  No upfront savings.
>* **No capacity reservation:** Lower priority in case of capacity shortages.
>* **Suitable for:** Short-term, unpredictable workloads, testing, and situations where interruptions are not critical.
>
>**Spot Pricing:**
>
>* **Cheapest option:** Up to 90% discount compared to on-demand.
>* **Dynamic pricing:** Spot prices fluctuate based on available capacity.
>* **High risk of interruption:** Instances can be terminated if the spot price exceeds your maximum bid.
>* **Not reliable:** Not suitable for mission-critical applications or workloads requiring consistent uptime.
>* **Suitable for:**
>
>    * Non-time-sensitive workloads (e.g., batch processing, scientific analysis)
>    * Highly parallel workloads that can be easily restarted
>    * Cost-sensitive tasks that can tolerate interruptions (e.g., media processing, image processing)
>    * Stateless applications where data is not stored on the instance
>
>**General Recommendations:**
>
>* **Understand your workload:**  Identify its sensitivity to interruptions, duration, and resource requirements.
>* **Start with on-demand:** Evaluate its suitability and consider alternatives only if justified.
>* **Avoid spot for critical workloads:**  Spot pricing introduces significant risk and should not be used for business-critical applications.
>
>
>
>This summary provides a concise overview of the key insights and information presented in the transcript.
>

EC2 On-Demand
- The default way to purchase EC2 instances
- Features:
	- No interruption
	- No capacity reservation
	- Predictable pricing
	- No upfront cost
	- No discount
	- Short term/unknown workloads
	- Apps which can't be interrupted
- On-Demand instances are isolated but multiple customer instances run on shared hardware
- Per-second billing while an instance is running, other resources like storage consume capacity, so bill, regardless of if instance is stopped or running.
- Instances of different sizes run on the same EC2 hosts, consume a defined allocation of resources
EC2 Spot
- Spot pricing is AWS selling unused EC2 host capacity for up to 90% discount, spot price is based on spare capacity at a given time
- Set your max spot price you are willing to pay, you stay on your instance until spot price goes above that price and then it terminates your instance
- Never use spot for workloads that can't tolerate interruption.
- Good for:
	- Non-time critical
	- Anything which can be rerun
	- Burst capacity needs
	- Cost sensitive workloads
	- Anything which is stateless