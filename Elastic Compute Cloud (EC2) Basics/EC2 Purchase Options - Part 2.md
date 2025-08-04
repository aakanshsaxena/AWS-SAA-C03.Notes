
>[!note]- Post-Processing
>## Key Insights and Information from the AWS EC2 Purchase Options Transcript:
>
>**1. EC2 Purchase Options:**
>
>* **On-Demand:** For short-term, unpredictable usage, billed per second.
>* **Reserved Instances:** For long-term, consistent usage, discounted pricing based on commitment (1 or 3 years) and upfront payment (No Upfront, Partial Upfront, All Upfront).
>* **Spot Instances:** For flexible, fault-tolerant workloads, lowest price but instances can be interrupted.
>* **Dedicated Hosts:** Entire physical EC2 host dedicated to your use, no per-second charge for instances, manage capacity yourself.
>* **Dedicated Instances:** Instances run on dedicated hardware with no other AWS customers, higher cost but guaranteed isolation.
>
>**2. Reserved Instances Explained:**
>
>* **Commitment:** You commit to using specific EC2 instance types in a chosen availability zone or region for a defined period (1 or 3 years).
>* **Benefits:** Significantly reduced per-second cost or even complete removal of the cost.
>* **Risks:** Unused reservations still incur cost. Choose wisely based on long-term usage needs.
>* **Payment Structures:**
>    * **No Upfront:** Reduced per-second cost, no upfront payment.
>    * **Partial Upfront:** Lower upfront cost and per-second cost than No Upfront.
>    * **All Upfront:** Greatest discount, full upfront payment.
>
>**3. Use Cases:**
>
>* **On-Demand:** Short-term, unpredictable workloads.
>* **Reserved Instances:** Long-term, consistent workloads with known usage.
>* **Spot Instances:** Flexible, fault-tolerant workloads where cost savings are prioritized.
>* **Dedicated Hosts:** Workloads with strict licensing requirements based on physical sockets or cores.
>* **Dedicated Instances:** Workloads requiring guaranteed hardware isolation.
>
>**4. Exam Focus:**
>
>* Prioritize understanding On-Demand, Reserved, and Spot instances for the exam.
>
>**5. Key Takeaways:**
>
>* Choose the purchase option that best aligns with your workload's characteristics and usage patterns.
>* Carefully consider the trade-offs between cost savings and commitment levels.
>* Understand the implications of licensing requirements when selecting a purchase option.
>
>
>
>

EC2 - Reserved
- Reserve for 1-3 years (greater discount for 3 years)
- You reserve an instance and pay 1/3 ways
	- No up-front (some savings) - pay a per second fee
	- Partial upfront (more savings) - pay a reduced per second fee
	- All upfront (most savings) - no per second fee
- Unused reservation are still billed
- Partial coverage of larger instances
	- If you reserve t3.micro and you use t3.small, you will be able to use the t3.micro "allowance" towards t3.small and pay the difference
EC2 - Dedicated Hosts
- You dedicate the whole host to yourself and pay for the host, no instance charges
- You need to manage capacity on the hosts 
- Make sure to not underutilize or overutilize (because overutilize means you can't run any more instances)
- Good for software that is licensed based on sockets/cores
- Also good because starting and stopping an instance won't mean you move across hosts
EC2 - Dedicated Instances
- You don't own or share the host
- You pay extra charges for the instances but you get dedicated hardware
- Good for compliance heavy regulations where you can't be sharing the hardware
