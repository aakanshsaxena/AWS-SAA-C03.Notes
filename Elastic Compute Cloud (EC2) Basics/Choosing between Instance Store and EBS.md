
>[!note]- Post-Processing
>## Key Insights and Information from the AWS EBS vs. Instance Store Transcript:
>
>This transcript focuses on helping viewers understand the differences between Amazon Elastic Block Storage (EBS) and Instance Store volumes, and when to use each.
>
>**Here are the key takeaways:**
>
>**Default to EBS:**
>
>* **Persistent Storage:** Always use EBS for persistent storage. Instance store volumes are not persistent and data can be lost due to hardware failure, instance reboots, maintenance, or instance movements.
>* **Isolated Storage:** Use EBS if you need to detach a volume from an instance and reattach it to another.
>
>**When Instance Store Volumes Might Be Suitable:**
>
>* **Built-in Replication:** If your application replicates data internally, you can use instance store volumes for performance benefits without the data loss risk.
>* **High Performance Needs:** For extremely high performance requirements exceeding the limits of EBS, instance store volumes can be used, but remember they are not persistent.
>* **Cost-Sensitive Scenarios:** Instance store volumes are often included in the price of EC2 instances, making them a cost-effective option when cost is a primary concern.
>
>**Performance Levels:**
>
>* **EBS:**
>    * **GD2 and GD3:** Up to 16,000 IOPS per volume.
>    * **IO1 and IO2:** Up to 64,000 IOPS per volume.
>    * **IO2 Block Express:** Up to 256,000 IOPS per volume (requires larger instance types).
>* **RAID 0:** Combining multiple EBS volumes can increase performance, but the maximum is limited by the instance type (currently 260,000 IOPS).
>* **Instance Store:** Can achieve millions of IOPS, but remember the data is not persistent.
>
>**Important Notes:**
>
>* **Exam Focus:** The transcript emphasizes memorizing performance figures and understanding when to use each storage type for specific scenarios.
>* **Instance Type Matters:**  The maximum performance achievable with both EBS and instance store volumes is dependent on the size of the EC2 instance used.
>
>
>**Overall, the transcript provides a concise overview of the key differences between EBS and Instance Store volumes, highlighting the factors to consider when making a decision.**

Use EBS
- Persistence
- Resilience
- Storage isolated from instance lifecycles
Depends
- Resilience w/ app that has in-built replication (Instance store could work)
- High performance needs (depends on how high performance needs to be -> covered next)
Instance Store
- Super high performance needs
- Cost (often included in EC2 instance cost)

Other Tips
For EBS
- Cheap = ST1 or SC1
- Throughput or streaming = ST1
- Boot = CANT be ST1 or SC1
- GP2/3 - up to 16,000 IOPS (GP2 you pay for extra over 3K)
- IO1/2 - up to 64,000 IOPS
- IO2 Block Express - up to 256,000 IOPS 
- RAID0 + EBS - up to 260,000 IOPS
	- Combine multiple EBS volumes using RAID0 to combine the performance from all, capped by EC2 instance max of 260,000 IOPS
- More than 260,000 IOPS - INSTANCE STORE