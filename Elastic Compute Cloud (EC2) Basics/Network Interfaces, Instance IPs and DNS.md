
>[!note]- Post-Processing
>## Key Insights and Information from the EC2 Networking Theory Transcript:
>
>**Core Concepts:**
>
>* **EC2 Instances:**  Each instance starts with one primary **Elastic Network Interface (ENI)** and can have additional secondary ENIs.
>* **Subnet Importance:**  ENIs are tied to subnets within the same availability zone.
>* **Network Interface Attributes:** ENIs have:
>    * **MAC Address:**  Hardware address visible within the OS.
>    * **Primary Private IP:** Static, assigned from the subnet.
>    * **Secondary Private IPs:**  Optional, can be added.
>    * **Public IP:** Optional, dynamic unless replaced by an Elastic IP.
>    * **Elastic IP:**  Public, static IP allocated to your AWS account. Can be associated with a private IP on an ENI.
>    * **IPv6 Addresses:**  Optional, publicly routable.
>    * **Security Groups:**  Applied to ENIs, controlling traffic to/from all IPs on that interface.
>    * **Source/Destination Check:**  Can be enabled/disabled on ENIs, discarding traffic not matching the interface's IPs.
>
>**Important Points:**
>
>* **Security Groups Impact:** Security groups are attached to ENIs, affecting all IPs on that interface.
>* **Public IP Dynamics:** Dynamic public IPs change on instance stop/start and when the instance moves between EC2 hosts.
>* **Elastic IP vs. Public IP:** Assigning an Elastic IP replaces the instance's dynamic public IP. Removing an Elastic IP results in a new dynamic public IP.
>* **DNS Names:** Instances have both internal (private) and external (public) DNS names.
>* **Hybrid Network Design:**  The public DNS name resolves to the private IP within the VPC and the public IP outside the VPC.
>
>**Exam Tips:**
>
>* Understand the relationship between ENIs, subnets, and IPs.
>* Know the difference between dynamic and elastic IPs.
>* Be aware of how security groups are applied to ENIs.
>
>
>This transcript provides a comprehensive overview of EC2 networking concepts. By understanding these key insights, you can effectively manage and secure your EC2 instances.
>

- Each instance has at least one primary ENI and can have secondary ENI's.
- The ENI's have a MAC address, primary IPv4 private IP, 0+ secondary IPs, 0 or 1 public IPv4 address, 1 elastic IP per private IPv4 address, 0+ IPv6 addresses, security groups, source/destination checks
- Security groups are applied to the ENI not the instance itself.
- IP addresses can and will change if you stop and start an instance.
- Instances have both a public and private DNS name, contact within VPC will occur through private DNS/IP, contact outside of VPC will occur through public DNS/IP.
- Private IP Format EXAMPLE - 10.16.0.10 -> ip-10-16-0-10.ec2.internal
- Public IPv4 Format EXAMPLE - 3.89.7.136 -> ec2-3-89-7-136.compute-1.amazonaws.com

>[!note]- Post-Processing
>## Key Insights and Information from the AWS EC2 Transcript:
>
>**Elastic Network Interfaces (ENIs):**
>
>* **Secondary ENIs:**  Allow licensing based on MAC addresses, which can be moved between EC2 instances.
>* **Multiple ENIs:** Enable multi-homed systems (instance in two different subnets) and different security groups for different IPs or types of access.
>* **Primary ENI:**  Generally interacts with security groups at the instance level.
>
>**EC2 IP Addressing:**
>
>* **Public IP:** Dynamically assigned, changes upon instance stop/start or migration.
>* **Private IP:**  Used by the operating system, configured within the instance.
>* **Elastic IP:**  Static public IP, allocated and assigned to avoid changes.
>* **Public DNS:** Resolves to the primary private IP within the VPC for instance-to-instance communication, never leaving the VPC. Outside the VPC, it resolves to the public IP.
>
>**Important Exam Points:**
>
>* Operating systems never directly configure with public IPv4 addresses.
>* Public IP addresses are dynamic and change upon instance stop/start or migration.
>* Elastic IPs are used for static public IP addresses.
>* Public DNS resolves to private IP within the VPC and public IP outside the VPC.
>
>**General Notes:**
>
>* Theory will become clearer with practical application.
>* Understanding these concepts is crucial for later topics like VPC peering.
>
>
>

**Exam Powerups**
- Since you can detach and reattach a secondary ENI to an instance (uses same MAC address), we can use this for software licensing that attaches to a MAC address and transfer it through instances
- Multiple interfaces can be used for multi-homed (subnets) - for example one for data, one for management.
	- Useful when we have different security groups for different interfaces
- OS never sees the public IPv4 - NAT does this. Always configure private IPv4 address inside OS
- IPv4 public IPs are dynamic - stop and start = change
	- To avoid allocate and assign an elastic IP
- Public DNS = private IP in VPC, public IP everywhere else

