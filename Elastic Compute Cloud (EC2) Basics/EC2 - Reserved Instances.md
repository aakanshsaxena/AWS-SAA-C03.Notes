
>[!note]- Post-Processing
>## Key Insights and Information from the AWS EC2 Reserved Instances and Savings Plans Transcript:
>
>**1. Different EC2 Purchase Options:**
>
>* **Standard Reserved Instances:** Best for consistent, long-term (1 or 3 years) usage running 24/7/365. Cheapest option for this type of workload.
>* **Scheduled Reserved Instances:** Ideal for predictable, long-term usage that isn't continuous. You specify the frequency, duration, and time window for the reserved capacity. 
>    * Minimum commitment: 1200 hours per year.
>    * Minimum purchase period: 1 year.
>* **Capacity Reservations:** Guarantee access to specific EC2 capacity in a chosen availability zone, even during peak demand.
>    * No billing discounts, only capacity guarantee.
>    * Can be regional or zonal.
>    * Can be on-demand (pay for capacity regardless of usage).
>* **Savings Plans:** Commit to a minimum hourly spend with AWS for 1 or 3 years and receive discounts on various compute services (EC2, Fargate, Lambda).
>    * General compute savings plans offer discounts across multiple services.
>    * EC2 savings plans offer the highest discounts (up to 72% off on-demand prices).
>
>**2. Choosing the Right Option:**
>
>* **Usage Pattern:** Analyze your workload's frequency, duration, and consistency.
>* **Commitment:** Consider your willingness to commit to a specific term and spend.
>* **Cost Optimization:** Compare the potential savings of each option against your usage needs.
>
>**3. Additional Notes:**
>
>* Capacity reservations don't offer billing discounts, only capacity guarantee.
>* Savings plans are a powerful tool for cost optimization, especially for organizations migrating to emerging architectures like Fargate and Lambda.
>* Regularly review and adjust your savings plan usage to ensure optimal cost efficiency.
>
>**4. Exam Focus:**
>
>* Understand the different types of EC2 purchase options and their key features.
>* Know how savings plans work and their potential benefits.
>
>
>
>

Scheduled Reserved Instances
- Ideal for long term usage which doesn't run constantly
- For example, if you know you need batch processing daily for 5 hours starting at 23:00, or weekly analysis on Friday for 24 hours, or 100 hours of EC2 per month
- You book a time, type of instance, and duration for a discounted price
- Doesn't support all instance types or regions, and you must book 1200 hours per year for at least one year
Capacity Reservation
- AWS gives instances to
	- Reserved -> On-Demand -> Spot
- Regional reservations provide a discount for valid instances launched in that region, zonal reservations give you a billing **and** capacity discount in just one AZ
- Regional reservation are flexible but don't reserve capacity within an AZ which can be risky during major faults when capacity could be limited
- On-demand capacity reservations can make sure you always have access to capacity in an AZ when you need it, but you pay full on-demand price, and you pay no matter if you use it or not.
EC2 Savings Plan
- Hourly commitment for a 1 or 3 year plan
- Reservation of general compute $ amounts ($20 per hour for 3 years)
- Or a specific EC2 savings plan - flexibility on size & OS
	- 66% savings for general compute, 72% for EC2 savings plan
- Compute products = EC2, Fargate, Lambda
- Products have an on-demand rate and a savings plan rate
	- You pay the savings plan rate up until your usage cap rate (for our example $20/hour)
	- After we hit $20/hour (our commitment $), we are billed the on-demand price
