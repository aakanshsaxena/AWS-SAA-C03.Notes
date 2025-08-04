>[!note]- AI
> #### AWS Snowball Edge Device Types
> - **Snowball Edge Storage Optimized:** The primary focus is on high-capacity data transfer.
>     - Offers a balance of storage and compute.
>     - Typically provides a large amount of HDD storage (up to 80 TB) and some EC2-compatible compute.
>     - Includes a small amount of local SSD storage for running instances.
>     - Suitable for large data migrations and basic data processing at the edge.
> - **Snowball Edge Compute Optimized:** This variant is for demanding compute needs at the edge.
>     - Prioritizes VCPUs and RAM over total storage capacity.
>     - Comes with dedicated, high-performance NVMe SSD storage for compute instances, offering significantly faster I/O.
>     - A **Compute Optimized with GPU** variant is also available, which is ideal for machine learning inference, real-time video processing, and other highly parallel workloads in disconnected environments.
> - **Original Snowball:** This is the older generation device, designed solely for secure data transfer without any on-board compute capability.
> #### Snowball Edge Use Cases and Features
> - **Remote Data Processing:** Snowball Edge's key differentiator is its ability to run EC2 instances and Lambda functions directly on the device. This allows for data processing and analysis to happen "at the edge" in locations with limited or no internet connectivity.
> - **Networking:** Snowball Edge offers faster, high-speed network interfaces (e.g., 100 Gbps) compared to standard network connections, which significantly accelerates the data transfer process. This makes it a very efficient solution for both importing data to and exporting data from AWS.
> - **Multi-Site Migrations:** Due to its manageable size, you can order multiple Snowball Edge devices to handle data transfers from several different physical locations simultaneously.
> #### AWS Snowmobile
> - **Massive-Scale Data Transfer:** Snowmobile is a highly specialized service for migrating massive datasets, specifically those over **10 petabytes (PB)**.
> - **Physical Architecture:** It is a 45-foot, ruggedized shipping container that is delivered to your data center by a semi-trailer truck.
> - **Capacity:** A single Snowmobile can transfer up to **100 PB** of data in one trip.
> - **Usage:** After arrival, it connects to your data center's power and network. Your team then transfers data to the Snowmobile, after which it is driven back to an AWS data center for ingestion.
> - **Single-Site Limitation:** A single Snowmobile unit cannot be split to service multiple sites at once, making it unsuitable for multi-site migrations unless the scale is enormous. It is an uneconomical choice for data migrations under 10 PB.
> #### Exam and Architectural Focus
> - The primary exam focus for the AWS Snow Family is to **understand the use cases** for each device type. You should know which device is appropriate based on the amount of data to be migrated and whether on-site compute is required.
> - The key architectural decision points are:
>     - **Data size:** Is it terabytes (Snowball Edge) or tens/hundreds of petabytes (Snowmobile)?
>     - **Compute needs:** Is on-board processing needed at the edge? If so, Snowball Edge is the only choice.
>     - **Number of locations:** Is the data in a single massive location (Snowmobile) or spread across multiple sites (Snowball Edge)

Snowball
- Ordered from AWS, Log a Job, Device Delivered (Not instant)
- Encrypted at rest with KMS
- 50TB or 80TB capacity
- 1Gbps, 10GBps network
- Economical between 10TB to 10PB
- Multiple devices to multiple premises
- Only storage
Snowball Edge
- Storage + Compute
- Larger capacity vs Snowball
- 10Gbps, 10/25, 45/50/100 Gbps
- Storage Optimized (w/ EC2) - 80TB, 24 vCPU, 32 GiB RAM, 1TB SSD
- Compute Optimized - 100TB + 7.68 NVME, 52 VPCU, 208 GiB RAM
- Compute w/ GPU - same as above + GPU
- Ideal for remote sites or where data processing on ingestion is needed
Snowmobile
- Portable datacenter within a shipping container on a truck
- Special order
- Ideal for single location when 10PB+ is required
- Up to 100PB per snowmobile
- Not economical for multi-site, unless huge or sub 10PB