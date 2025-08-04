
>[!note]- Post-Processing
>## Key Insights and Information from AWS GP2 and GP3 Storage Lesson:
>
>**GP2 (General Purpose SSD):**
>
>* **Default storage type:** Currently the default for EBS volumes.
>* **Performance:**
>    * Baseline performance: 3 IOPS per GB of volume size (minimum 100 IOPS for volumes up to 33.33 GB).
>    * Burst performance: Up to 3,000 IOPS.
>* **IO Credit Architecture:**
>    * Volumes have a bucket of IO credits (5.4 million max).
>    * Each IOPS consumes 16 KB of data.
>    * Baseline performance refills the bucket at a rate of 3 IOPS per GB per second.
>    * Bursting uses credits from the bucket.
>    * **Important:** Requires managing IO credit buckets for all volumes to ensure they don't deplete.
>* **Maximum IOPS:** 16,000 for volumes larger than 5.33 TB.
>* **Maximum Throughput:** 250 MB/s.
>* **Usage Scenarios:**
>    * Boot volumes
>    * Low latency applications
>    * Dev and test environments
>    * Medium-sized databases
>
>**GP3 (General Purpose SSD):**
>
>* **Simpler Architecture:**
>    * No IO credit bucket system.
>    * Standard performance of 3,000 IOPS and 125 MB/s throughput for all volumes.
>* **Pricing:** 20% cheaper than GP2 at the time of recording.
>* **Scalability:**
>    * Can be scaled up to 16,000 IOPS and 1000 MB/s throughput, but requires additional cost.
>* **Usage Scenarios:**
>    * Same as GP2.
>
>**Key Takeaways:**
>
>* GP3 is generally more economical than GP2, especially for workloads under 3,000 IOPS.
>* GP3 is simpler to understand and manage due to its lack of IO credit architecture.
>* GP2 is still the default but GP3 is expected to replace it in the future.
>* Both GP2 and GP3 are suitable for various workloads, including boot volumes, databases, and applications.
>
>
>

EBS - GP2
- The default type of EBS volume for now
- Volumes can range from 1GB-16TB
- An IO Credit is 16KB, IOPS assume 16KB, 1 IOPS is 1 IO in 1 second
- We have a bucket that starts with a capacity of 5.4 million IO credits, and fills at different rates
	- Baseline = 100 IO Credits per second
	- If over 33.33GB volume, then fills at 3 IO credits per second per GB of volume size
- Can burst up to 3,000 IOPS which can last 30 minutes @ full capacity bucket. Great for boots and initial workloads
- Maximum for GP2 of 16,000 IO Credits per second, volumes larger than 1TB, baseline is above burst. Thus credit system isn't used & you always achieve baseline performance of 16,000 IO credits per second.

EBS - GP3
- Standard "Tier" - 3,000 IOPS & 125 MiB/s 
- Extra Cost for up to 16,000 IOPS or 1,000 MiB/s
- GP3 is about 20% cheaper than GP2, 4x Faster max throughput vs GP2 - 1,000 MiB/s vs 250 MiB/s

Both are good for virtual desktops, medium sized single instances databases (MSSQL Server and Oracle DB), low-latency interactive apps, dev & test, boot volumes
