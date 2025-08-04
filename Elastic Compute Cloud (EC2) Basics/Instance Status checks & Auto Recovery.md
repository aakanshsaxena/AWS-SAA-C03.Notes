
>[!note]- Post-Processing
>## Key Insights and Information from the EC2 Instance Status Checks and Auto-Recovery Transcript:
>
>**Instance Status Checks:**
>
>* Every EC2 instance has two status checks: **system status** and **instance status**.
>* Both checks must pass for the instance to be considered healthy.
>* **System status:** Checks the health of the EC2 service or host, e.g., power, network connectivity, hardware/software issues.
>* **Instance status:** Checks the health of the instance itself, e.g., file system corruption, networking issues, kernel problems.
>
>**Handling Failed Status Checks:**
>
>* Manually: Stop/restart/terminate and recreate the instance.
>* **EC2 Auto-Recovery:** Automatically recovers from failed status checks by:
>    * **Rebooting** the instance.
>    * **Migrating** the instance to a new EC2 host within the same availability zone.
>
>**Auto-Recovery Requirements:**
>
>* **Spare EC2 host capacity** in the availability zone.
>* **Modern instance types:** A1, C4, C5, M4, M5, R3, R4, R5 (link provided in transcript).
>* **EBS volumes:** Auto-recovery does not work with instance store volumes.
>
>**Limitations:**
>
>* Auto-recovery only addresses isolated failures, not entire AZ failures.
>* Not a solution for complex system issues.
>
>**Key Takeaways:**
>
>* Instance status checks are crucial for monitoring EC2 instance health.
>* EC2 auto-recovery provides a simple way to automatically recover from certain failures.
>* Understand the requirements and limitations of auto-recovery before relying on it.
>
>
>

Instance Status Checks
- System Status Check
	- Loss of system power
	- Loss of network connectivity
	- Host software/hardware issues
- Instance status check
	- Corrupted file system
	- Incorrect instance networking
	- OS Kernel Issues
- We can set up an alert for our EC2 Instance so that if any of the status check fails, EC2 can try to recover the instance -> it will take a series of step ranging up to restarting itself on a new host within that AZ to see if it can self-diagnose the issue. Used for simple issues, not large scale failures.
