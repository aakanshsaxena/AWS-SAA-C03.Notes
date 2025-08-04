
>[!note]- Post-Processing
>## Key Insights and Information from the AWS EC2 Instance Types Transcript:
>
>**1. Instance Type Categories:**
>
>The transcript focuses on different categories of AWS EC2 instances, each tailored for specific use cases:
>
>* **General Purpose:**  A1/M6G (ARM-based, efficient), T3/T3A (burstable, low CPU load with occasional bursts), M5/M5A/M5N (steady state CPU, consistent load).
>* **Compute Optimized:** C5/C5N (high CPU for media encoding, scientific modeling, game servers, machine learning).
>* **Memory Optimized:** R5/R5A (large in-memory applications), X1/X1E (highest memory), A3S (high memory).
>* **Accelerated Computing:** P3 (parallel processing, machine learning), G4 (graphics intensive), F1 (field programmable gate arrays for genomics, financial analysis, big data), Inf1 (custom designed for machine learning).
>* **Storage Optimized:** High local storage with different throughput/IO options.
>
>**2. Instance Type Selection:**
>
>Choosing the right instance type depends on your application's needs:
>
>* **CPU-intensive:**  Compute optimized (C5/C5N)
>* **Memory-intensive:** Memory optimized (R5/R5A, X1/X1E, A3S)
>* **Specific acceleration:** Accelerated computing (P3, G4, F1, Inf1)
>* **High storage requirements:** Storage optimized
>
>**3. Useful Resources:**
>
>The transcript recommends two websites for further exploration:
>
>* **Amazon EC2 Instance Types Documentation:** Provides detailed information on each instance type, use cases, features, and resources.
>* **ec2instances.info:** Offers a sortable and filterable list of instance types with details on size, capabilities, costings (on-demand and reserved), operating system compatibility, and more.
>
>**4. Key Takeaways:**
>
>* Understand the different categories of EC2 instances and their strengths.
>*  Choose instance types based on your application's specific requirements.
>*  Utilize the provided resources to explore and compare different instance options.
>*  Focus on understanding the core concepts rather than memorizing all instance details.
>
>
>
>

![[EC2 Instance Types.png]]
Resources:
[https://aws.amazon.com/ec2/instance-types/](https://aws.amazon.com/ec2/instance-types/)
[https://ec2instances.info/](https://ec2instances.info/)

How to remember a bit easier?
- T = Tiny/Burstable
- M = Medium/Balanced
- C = Compute Optimized
- R = RAM Optimized
- X = Extra RAM (High Memory)
- A = AMD Based
- I = I/O Optimized
- G = GPU (Nvidia)
- P = Powered GPU (More ML Focus)
- H = Hard Disk Optimized
- D = Dense Storage
- Z = High Compute & Memory
- F = FPGA
- Inf = Inference ML
- Trn = Train ML Models