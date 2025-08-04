
>[!note]- Post-Processing
>## Key Insights and Information from the EC2 Virtualization Lesson:
>
>**1. Virtualization Basics:**
>
>* Virtualization allows running multiple operating systems (guest OS) on a single physical server (host).
>* Each guest OS has its own virtual resources (CPU, memory, storage, network) and operates independently.
>
>**2. Types of Virtualization:**
>
>* **Emulated Virtualization (Software Virtualization):**
>    * Guest OSes believe they are running on real hardware.
>    * Hypervisor emulates hardware and intercepts privileged instructions, translating them to software.
>    * **Performance Penalty:** Slow due to software translation.
>* **Para-Virtualization:**
>    * Guest OSes are modified to call the hypervisor instead of hardware for privileged operations.
>    * Requires specific OS modifications for the hypervisor.
>    * **Performance Improvement:** Faster than emulated virtualization due to direct hypervisor interaction.
>* **Hardware-Assisted Virtualization:**
>    * CPU has built-in instructions and capabilities for virtualization.
>    * Hypervisor directly controls CPU resources and handles privileged instructions.
>    * **Performance Benefit:** Minimal performance degradation compared to running directly on hardware.
>
>**3. Network Performance Bottleneck:**
>
>* Even with hardware-assisted virtualization, network and disk I/O can be slow due to software translation layers.
>
>**4. SRIOV (Single Root I-O Virtualization):**
>
>* Allows network cards to present themselves as multiple virtual cards to guest OSes.
>* Provides direct physical access to network resources for each guest OS.
>* **Performance Improvement:** Significantly faster network speeds, lower latency, and reduced CPU usage.
>
>
>**5. EC2's Enhanced Networking:**
>
>* Leverages SRIOV and other advanced virtualization techniques.
>* Delivers high-performance networking for EC2 instances.
>
>**6. AWS Nitro:**
>
>* AWS's own hypervisor stack enabling advanced EC2 features.
>* Will be discussed in more detail in future lessons.
>
>
>
>**Overall, the lesson provides a strong foundation for understanding virtualization concepts and how they apply to EC2.** It highlights the evolution of virtualization techniques and their impact on performance.
>

- Typically in the past, in order to allow virtualization to occur, you have the an application on top of the OS on top of the hardware
	- Only the OS is allowed to make kernel calls/system calls -> so when applications would try to make these calls, they would need to go through the OS and if they didn't it could cause system crashes
- Initially, very inefficient to do virtualization because the hardware wasn't aware of it
	- Emulated Virtualization: includes a hypervisor, with VMs. Guest OS (VM OS that had privileged calls) thought that they were all real, but this was inefficient.
	- Hypervisor catches privileged calls and performs binary translation to stop crashes -> extremely slow and inefficient
	- Paravirtualization: only works with small number of OS
		- Areas of OS would be changed in Source Code to make hypercalls (hypervisor calls) instead of making system calls. Means that system became almost virtualization aware -> more efficient
- Hardware Assisted Virtualization: hardware is aware that it is performing virtualization. Privileged calls made straight to CPU and then CPU sends to hypervisor to execute. Issue was that applications and OS thought they had all physical hardware (like network cards), but they didn't.
	- SR-IOV = single route IO virtualization. Allows a network card or any other card to appear as several unique mini cards -> no translation needed -> basically one network card per VM. = EC2 Enhanced Networking.
	- Many advanced virtualization techniques on EC2 use SR-IOV

