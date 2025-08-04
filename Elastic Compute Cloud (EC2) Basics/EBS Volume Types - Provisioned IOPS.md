
>[!note]- Post-Processing
>## Key Insights and Information from EBS Provisioned IOPS SSD Transcript:
>
>**Types of Provisioned IOPS SSDs:**
>
>* **IO1:** General release, max 64,000 IOPS, 1,000 MB/s throughput, 4GB-16TB volumes.
>* **IO2:** General release, successor to IO1, max 64,000 IOPS, 1,000 MB/s throughput, 4GB-16TB volumes.
>* **IO2 Block Express:** Preview, max 256,000 IOPS, 4,000 MB/s throughput, 4GB-64TB volumes.
>
>**Key Features:**
>
>* **Configurable IOPS:** Performance independent of volume size.
>* **High Performance:** Designed for low latency and consistent performance.
>* **Pricing:** Pay for both volume size and provisioned IOPS.
>
>**Performance Ratios:**
>
>* **IO1:** 50 IOPS per GB of volume size.
>* **IO2:** 500 IOPS per GB of volume size.
>* **Block Express:** 1000 IOPS per GB of volume size.
>
>**Per-Instance Performance Limits:**
>
>* **IO1:** 260,000 IOPS, 7,500 MB/s throughput per instance.
>* **IO2:** 160,000 IOPS, 4,750 MB/s throughput per instance.
>* **Block Express:** 260,000 IOPS, 7,500 MB/s throughput per instance.
>
>**Use Cases:**
>
>* **Low Latency Applications:** Applications requiring consistent millisecond latency.
>* **Small Volumes with High Performance Needs:** Ideal for smaller volumes needing extreme performance.
>
>**Comparison to Other Volume Types:**
>
>* **GP2 and GP3:** Lower performance, 260,000 IOPS and 7,000 MB/s per instance maximum.
>* **Instant Store:** Even higher performance but non-persistent.
>
>**Remember:**
>
>*  These are maximums, actual performance depends on various factors.
>*  Multiple volumes may be required to saturate per-instance performance limits.
>*  Consider instance type and size limitations when planning

IO1/IO2/Block Express
- Up to:
	- 64,000 IOPS per volume (4xGP2/3)
	- 256,000 IOPS per volume (Block Express)
	- Up to 1,000 MB/s throughput
	- Up to 4,000 MB/s throughput (Block Express)
- With io1/io2/BlockExpress, IOPS can be adjusted independently of size
	- io1 50IOPS/GB (max)
	- io2 500IOPS/GB (max)
	- Block Express 1000IOPS/GB (max)
- 4GB-16TB io1/2
- 4GB-64TB BlockExpress
- Per Instance Performance
	- io1 - 260,000 IOPS & 7500 MB/s
	- io2 - 160,000 IOPS & 4750 MB/s
	- io2 Block Express - 260,000 IOPS & 7500 MB/s
- Only the most modern and largest instances support high levels of performance, and to maximize performance you're going to need multiple volumes to saturate per instance performance level.