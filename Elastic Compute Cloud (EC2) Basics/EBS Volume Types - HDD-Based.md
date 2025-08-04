>[!info]- Transcription
>![[Recordings/recording-2025-07-17T02-44-34-548Z.webm]]
> I want to talk about the hard disk drive or HDD based volume types provided by EDS. HDD based means they have moving bits, platters which spin, little robot arms known as heads which move across those spinning platters. Moving parts means slower, which is why you only want to use these volume types in very specific situations. Now let's jump straight in and look at the types of situations where you would want to use HDD based storage. Now there are two types of HDD based storage within EPS. Well, that's not true. There are actually three, but one of them is legacy. So I'll be covering the two ones which are in general usage. And those are SD1, which is throughput optimized HDD, and SC1, which is co-op HDD. So think about SD1 as the fast hard drive, not very agile, but pretty fast. And think about SC1 as co-op. SD1 is cheap, it's less expensive than the SSD volumes, which makes it ideal for any larger volumes of data. SD1 is even cheaper, but it cuts with some significant trade-offs. Now, SD1 is designed for data which is sequentially accessed. Because it's HDD-based, it's not great at random access. It's more designed for data which needs to be written or read in a fairly sequential way. Applications where throughput and economy is more important than IOPS or extreme levels of performance. SD1 volumes range from 125 GB to 16 TB in size, and you have a maximum of 500 IOPS. But, and this is important, IO on HDD-based volumes is measured as 1 MB blocks. So 500 IOPS means 500 MB per second. Now their maximum HDD-based storage works in a similar way to how GP2 volumes work with a credit bucket. Only with HDD volumes it good around MP per second rather than IOS So with SG you have a baseline performance of 40 MP per second for every 1 TB of volume size and you can burst to a maximum of 250 MB per second for every TB of volume size obviously up to the maximum of 500 IOTs and 500 MB per second SG is designed for when cost is a concern, but you need frequent access storage for throughput-intensive sequential workloads, so things like big data, data warehouses, and log processing. Now, SC-1, on the other hand, is designed for infrequent workloads. It's geared towards maximum economy when you just want to store lots of data and don't care about performance, so it offers a maximum of 250 IOTs. Again, this is with a 1 MB I.O. size. So this means a maximum of 250 MB per second throughput. And just like with ST1, this is based on the same credit pool architecture. So it has a baseline of 12 MB per TB volume size and a burst of 80 MB per second per TB volume size. So you can see that this offers significantly less performance than ST1, but it's also significantly cheaper. And just like with ST1, volumes can range from 125 GB to 16 TB in size. This storage type is the lowest cost EDS storage available. It's designed for less frequently accessed workloads. So if you have colder data, archives, or anything which requires less than a few loads or scans per game, this is the type of storage volume to pick. And that's it for HDD based storage. Both of these are lower cost and lower performance versus SSD. It's time for what you need, economy and data storage. Thinking between them is simple. If you can tolerate the trade-offs of SC1, then use that. It's SuperG, and for anything which isn't day-to-day access, it's perfect. Otherwise, choose ST1. And if you have a requirement for anything IOP space, then avoid both of these and look at SSD based storage. With that being said though, that's everything that I wanted to cover in this lecture.
---
>[!note]- Post-Processing
>## Key Insights from HDD-Based Storage Lecture:
>
>**Understanding HDD Storage:**
>
>* **HDDs (Hard Disk Drives) are slower than SSDs:** They use moving parts (platters and heads) which limit their speed.
>* **Ideal for specific situations:** Use HDDs when cost is a major concern and performance isn't critical.
>
>**Two Main HDD Types in EDS:**
>
>* **SD1 (Throughput Optimized HDD):**
>    * **Faster HDD:**  Good for sequential data access (writing/reading in order).
>    * **Lower IOPS:** Not ideal for random access.
>    * **Cost-effective:** Cheaper than SSDs, especially for large volumes.
>    * **Size:** 125 GB to 16 TB.
>    * **IOPS:** 500 (measured in 1 MB blocks, meaning 500 MB/second throughput).
>    * **Use Cases:** Big data, data warehouses, log processing.
>* **SC1 (Co-op HDD):**
>    * **Lowest Cost:** Most economical HDD option.
>    * **Infrequent Workloads:** Designed for data accessed less frequently.
>    * **Very Low IOPS:** 250 (measured in 1 MB blocks, meaning 250 MB/second throughput).
>    * **Size:** 125 GB to 16 TB.
>    * **Use Cases:** Cold data, archives.
>
>**Key Points to Remember:**
>
>* **HDDs are slower than SSDs:**  Understand the performance trade-offs.
>* **IOPS are measured in 1 MB blocks:**  Don't confuse the numbers.
>* **Choose based on your needs:** SD1 for throughput-intensive sequential workloads, SC1 for infrequent, low-performance access.
>* **Consider SSDs for high performance requirements:** If IOPS are crucial, avoid HDDs.
>
>
>
>Let me know if you have any other questions or need further clarification!
>

Two main types of HDD-based EBS
- st1
	- Throughput optimized, but still slower than SSD-based EBS
	- Cheaper than SSD-based EBS
	- 125GB-16TB
	- Best for frequent access, throughput-intensive, sequential data (not random)
	- Max 500 IOPS (1MB block size) = 500MB/s
	- 40MB/s/TB Base
	- 250MB/s/TB Burst
	- Big data, data warehouses, log processing
- sc1
	- Cold HDD
	- Cheapest form of EBS
	- 125GB-16TB
	- Lowest cost HDD volume designed for less frequently accessed workloads
	- Colder data requiring fewer scans per day
	- Max 250IOPS (1MB Block Size) = 250MB/s
	- 12MB/s/TB Base
	- 80MB/s/TB Burst
