
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript on AWS Instance Store Volumes:
>
>**What are Instance Store Volumes?**
>
>* Block storage devices attached directly to an EC2 instance, offering the highest storage performance within AWS.
>* Act as the basis for a file system used by applications.
>* Physically connected to a single EC2 host, isolated to that host.
>
>**Pros:**
>
>* **Highest Performance:** Significantly faster throughput and IOPS compared to EBS.
>* **Included in Instance Price:** No additional cost for using them, making them cost-effective for performance-critical workloads.
>
>**Cons:**
>
>* **Ephemeral:** Data is lost if the instance moves hosts, is resized, restarted, or if the physical volume fails.
>* **Cannot be Added Later:** Must be attached at instance launch time.
>
>**Performance Comparison:**
>
>* **D3 Instances (Storage Optimized):** Up to 4.6 GB/s throughput.
>* **I3 Instances (Storage Optimized):** Up to 16 GB/s throughput and 2 million read IOPS / 1 million write IOPS.
>
>**Key Takeaways:**
>
>* **Trade-off:** Instance store volumes offer exceptional performance but come with the risk of data loss.
>* **Use Cases:** Ideal for temporary data, caching, and high-performance workloads where data persistence is not critical.
>* **Not Suitable:** Avoid using for mission-critical data, databases, or any data requiring long-term storage.
>* **Exam Tip:** Remember that instance store volumes are ephemeral and data is lost upon instance migration or failure.
>
>
>**Remember:** Always consider the trade-offs and potential risks before choosing instance store volumes for your workloads.
>

- Block storage devices that are physically connected to one EC2 host
- Instances on that host can access them with the highest storage performance in AWS
- Included in the instance price
- Attached at launch, cannot add them post launch
- Instances like D3 and i3 can make drastic improvements over even the best EBS with 4.6GB/s throughput and 16GB/second of sequential throughput respectively
**Exam Powerups**
- Local on EC2 host
- Add at launch only
- Lost on instance move, resize, or hardware failure (so if you move hosts like when stopping or restarting an instance = move, basically anytime you have a different host you lose the original instance store)
- High performance
- Pay for it anyway - included in the instance price
- TEMPORARY, should not be used for any sensitive data or anything you need to hold long term. Holds data in ephemeral storage (temp).
