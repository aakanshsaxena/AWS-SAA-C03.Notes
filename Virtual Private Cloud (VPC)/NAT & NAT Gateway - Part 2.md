>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**NAT Gateways vs. NAT Instances:**
>
>* **NAT Gateways:**
>    * Recommended by AWS for most scenarios.
>    * Highly available within an AZ, automatically scales and recovers.
>    * Offers high-end performance, custom-designed for NAT.
>    * Charges based on usage and gateway size.
>    * **NOT** suitable for bastion hosts or port forwarding.
>* **NAT Instances:**
>    * Run as EC2 instances, can be cheaper for low-volume scenarios.
>    * Can be used for bastion hosts and port forwarding.
>    * Limited performance compared to NAT gateways.
>    * Can be configured with security groups and network ACLs.
>
>**Availability and Resilience:**
>
>* For region-wide resilience, deploy a NAT gateway in each availability zone (AZ) used by the VPC.
>* A single NAT gateway in an AZ provides high availability within that AZ but fails if the AZ fails.
>
>**IPv6 and NAT:**
>
>* NAT is not required for IPv6.
>* Internet Gateway works directly with IPv6 addresses.
>* NAT gateways do **NOT** support IPv6.
>
>**Other Important Points:**
>
>* NAT gateways are managed services, no direct OS access.
>* NAT instances can be used for multi-purpose tasks.
>* Be aware of costs associated with NAT gateways.
>
>
>**Exam Focus:**
>
>* Understand the differences between NAT gateways and NAT instances.
>* Know when to use each type.
>* Remember that NAT gateways are not region-resilient by default and require deployment in each AZ.
>* NAT gateways do not support IPv6.
>
>
>This summary should help you grasp the key takeaways from the transcript.
>

![[Pasted image 20250715224040.png]]

NAT Instance vs NAT Gateway
- NAT Instance is just an EC2 instance that drops any data that is on its network card where it's not the source or destination
- NAT Instance = need to disable a feature called source and destination checks
- High level architecturally both are the same, both need a public IPv4 address, run in public subnet, and an internet gateway
- Not preferred to use EC2 NAT instance
- Priority on availability, performance, low maintenance, high bandwidth = NAT Gateway
- NAT Instance is limited by the instance it's running on
- NAT Gateway is highly available within an AZ better than NAT Instance
- NAT Instance can be cheaper and significantly cheaper at high volumes of data, fixed costs
- NAT Gateway scales -> can raise costs and no free tier
- Can use Instance for other things, port forwarding, bastion hosts. CANNOT use NAT Gateway for this
- NAT Gateways can only use NACLs, NAT Instances can use Security Groups or NACLs
IPv6
- NAT is not required for IPv6
- All IPv6 addresses in AWS are publicly routable
- IGW works with ALL IPv6 IPs directly
- NAT Gateways don't work with IPv6
	- Any test question with this you can ignore
- If you add default IPv6 route ::/0 + IGW = bi-directional connectivity
- ::/0 Route + Egress-Only IGW = Outbound only