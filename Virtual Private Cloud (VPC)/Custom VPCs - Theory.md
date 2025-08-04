
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**Topic:** Building a Multi-Tier Custom VPC in AWS
>
>**Overall:** This section of a course explains how to create a complex multi-tier VPC in AWS, starting with the basics and gradually adding complexity.
>
>**Key Points:**
>
>* **VPC Fundamentals:**
>    * VPCs are isolated networks within a specific AWS region.
>    * They provide isolation and security, limiting the impact of potential issues.
>    * VPCs can be customized with various configurations.
>    * Two tenancy options exist: default (shared hardware) and dedicated (dedicated hardware).
>    * Dedicated tenancy comes at a cost premium and should be carefully considered.
>* **This Specific VPC:**
>    * Uses the first IP address range of the US region one (10.16.0.0/16).
>    * Is designed for four tiers: reserve, database, app, and web.
>    * Will be deployed across three availability zones (A, B, and C) out of four.
>    * Future availability zone is reserved for future expansion.
>* **Components to be Added:**
>    * **Internet Gateway:** Provides public access to resources within the VPC.
>    * **NAT Gateways:** Allow private instances to send traffic outbound.
>    * **Bastian Host:** A less secure method for accessing the VPC (explained for educational purposes).
>    * **Network Access Control Lists (NICLS):** Used for securing the VPC and controlling traffic flow.
>* **Course Progression:**
>    * This lesson focuses on creating the basic VPC structure.
>    * Subsequent lessons will cover the other components mentioned above.
>    * Later sections will delve into more secure alternatives to Bastion hosts and network security best practices.
>
>
>**Overall, the transcript provides a roadmap for building a multi-tier custom VPC in AWS, highlighting key concepts, architectural choices, and the learning progression of the course.**
>
Custom VPCs 
- Regional service = All AZs in the region
- Isolated network - nothing is allowed in or out without explicit configuration
- Can be simple or multi-tier configuration
- Allows for hybrid networking with other cloud + on-premises hardware
- Default or Dedicated Tenancy
	- Only choose dedicated if you are sure because you can't switch back from dedicated to default
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**VPC IP Addresses:**
>
>* **Private IPs:** Used for internal communication within the VPC.  Each VPC has a mandatory private IP block (minimum /28 prefix, 16 IPs, maximum /16 prefix, 65,536 IPs).
>* **Public IPs:** Used for communication with the public internet. Resources need a public IP to be accessible from outside the VPC.
>* **Secondary Private Blocks:** Can be added after VPC creation (maximum 5 by default, can be increased with support).
>* **IPv6:** Optional configuration for the VPC. AWS assigns a slash 56 IPv6 CIDR by default.  You can use your own IPv6 addresses.  IPv6 addresses are publicly routable by default, but explicit allowlist rules are still needed for security.
>
>**VPC DNS:**
>
>* **DNS is provided by Route 53 within the VPC.**
>* **Base DNS IP address:** VPC's base IP address + 2 (e.g., if VPC is 10.0.0.0, DNS IP is 10.0.0.2).
>* **Critical DNS settings:**
>    * **Enable DNS host names:** Determines if instances with public IPs get public DNS host names.
>    * **Enable DNS support:** Enables or disables DNS resolution within the VPC. 
>
>
>**Additional Points:**
>
>* The transcript emphasizes the importance of understanding the difference between private and public IPs, especially when designing network architectures within AWS.
>* It highlights the growing importance of IPv6 and encourages users to consider it for future deployments.
>* It provides practical tips for troubleshooting DNS issues in a VPC by checking the two critical DNS settings mentioned.
>
>**Overall, the transcript provides a concise overview of key concepts related to IP addressing and DNS in AWS VPCs.**
>
- IPv4 Private CIDR Blocks & Public IPs
- 1 Primary Private IPv4 CIDR Block - min /28 (16 IP) max /16 (65536 IP)
- Optional secondary IPv4 Blocks
- Optionally you can assign an IPv6 /56 CIDR Block although this isn't standard yet
DNS in a VPC
- Provided by Route 53
- By default it is set to the VPC's base IP address + 2 -> 10.0.0.0, DNS is 10.0.0.2
- enableDnsHostnames - gives instances DNS Names
- enableDnsSupport - enables DNS Resolution in VPC

