
>[!note]- Post-Processing
>## Key Insights and Information from AWS Storage Lesson:
>
>**Storage Basics:**
>
>* **Direct Attached Storage (DAS):** Physical disks directly connected to a device (e.g., laptop, server). 
>    * **Pros:** Very fast.
>    * **Cons:** Data loss if disk, hardware, or host fails.
>* **Network Attached Storage (NAS):** Volumes accessed over a network.
>    * **Pros:** Highly resilient, data survives host issues.
>    * **Cons:** Can be slower than DAS.
>* **Ephemeral Storage:** Temporary storage that doesn't persist (e.g., instance store).
>* **Persistent Storage:** Storage that exists independently of the device (e.g., EBS).
>
>**AWS Storage Categories:**
>
>* **Block Storage (EBS):** 
>    * Raw, addressable blocks.
>    * Requires an OS to create a file system.
>    * Can be used for booting instances.
>* **File Storage:** 
>    * Ready-made file systems accessed over a network.
>    * Not bootable.
>* **Object Storage (S3):** 
>    * Flat, key-value storage.
>    * Highly scalable and accessible.
>    * Not bootable or mountable.
>
>**Storage Performance:**
>
>* **IO (Block Size):** Size of data blocks written to disk.
>* **IOPS (Input/Output Operations Per Second):** Number of reads/writes per second.
>* **Throughput:** Rate of data transfer (MB/s).
>* **Relationship:** Throughput = IO Block Size * IOPS.
>
>**Exam Tips:**
>
>* Understand the differences between storage types.
>* Know the maximum IOPS and throughput for each AWS storage type.
>* Consider block size and IOPS when optimizing performance.
>
>
>The lesson emphasizes the importance of understanding the different types of storage, their strengths and weaknesses, and how they relate to performance metrics. It also highlights the need to consider these factors when choosing the right storage solution for specific use cases.
>

Key Terms
- Direct attached storage - local hardware attached to the host (for example instance store on EC2)
- Network attached storage - volumes delivered over the network (EBS)
- Ephemeral storage - temporary storage (instance store)
- Persistent storage - permanent storage - lives on past the lifetime of the instance
Key Terms - Part 2
- Block Storage - Volume presented to the OS as a collection of blocks with no structure. Mountable & Bootable
- File Storage - Presented as a file share with structure. Mountable NOT bootable
- Object Storage - collection of objects, flat. Not mountable or bootable
Storage Performance
IO (Block Size) x IOPS = Throughput
If either of these three are limited, it can impact the other two. Throughput can have its own cap beyond what IO x IOPS does.