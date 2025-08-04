>[!note]- Post-Processing
>### Key Insights and Information
>
>The transcript discusses the importance of subnets in Amazon Web Services (AWS) Virtual Private Clouds (VPCs) and their configuration. The key insights and information extracted from the transcript are:
>
>#### Subnets and their Characteristics
>
>1. **Definition**: A subnet is an AZ (Availability Zone) resilient feature of a VPC, a subnetwork of the VPC, created within one availability zone.
>2. **Relationship with Availability Zones**: One subnet is created in a specific availability zone and can never be changed. A subnet can never be in multiple availability zones, but one availability zone can have zero or many subnets.
>3. **IP Addressing**: Subnets use IP version 4 networking by default and are allocated an IP version 4 CIDR block, which is a subset of the VPC CIDR block. The CIDR blocks of subnets within a VPC cannot overlap.
>4. **Optional IPv6 Allocation**: A subnet can be allocated an IP version 6 CIDR block if the VPC is enabled for IP version 6. The allocated range is a /64 range, which is a subset of the VPC's /56 range.
>
>#### Communication between Subnets and Reserved IP Addresses
>
>1. **Default Communication**: Subnets within a VPC can communicate with each other by default. The isolation of the VPC is at its perimeter.
>2. **Reserved IP Addresses**: Five IP addresses within every VPC subnet are reserved and cannot be used:
>	* Network address (first address)
>	* Network + 1 address (used by the VPC router)
>	* Network + 2 address (used for DNS)
>	* Network + 3 address (reserved for future use)
>	* Network broadcast address (last address)
>
>#### DHCP Option Sets and IP Allocation Options
>
>1. **DHCP Option Sets**: A VPC has a DHCP option set applied to it, which controls settings like DNS servers, NTP servers, and NetBIOS servers. The DHCP option set can be changed, but not edited.
>2. **IP Allocation Options**: Two important IP allocation options can be defined at the subnet level:
>	* Auto-assign public IPv4 addresses
>	* Assign IPv6 addresses to resources deployed into the subnet
>
>#### Key Takeaways
>
>1. Understand the relationship between subnets and availability zones.
>2. Be aware of the reserved IP addresses within every VPC subnet.
>3. Know how to configure DHCP option sets and IP allocation options for subnets.
>4. Understand the

VPC Subnets
- AZ Resilient
- A subnetwork (subnet) of a VPC that is located within a particular VPC
- 1 Subnet can be in 1 AZ ONLY, but 1 AZ can have multiple subnets
- IPv4 CIDR is a subset of the VPC CIDR
- Cannot overlap with other subnets
- You can optionally allocate an IPv6 CIDR (/64 subset of the /56 VPC - space for 256)
- Subnets can communicate with other subnets that are within the VPC (free communication within that VPC)
Subnet IP Addressing
- There are 5 reserved IP addresses in total in any VPC Subnet (Let's say 10.16.16.0/20)
	- Network address - first address in the range - 10.16.16.0
	- VPC Router - address+1 - 10.16.16.1
	- Reserved DNS Resolution - address+2 - 10.16.16.2
	- Reserved for future use - address+3 - 10.16.16.3
	- Broadcast Address - last address in the range - 10.16.31.255
Dynamic Host Configuration Protocol (DHCP)
- How computers receive IP addresses automatically
- There is one DHCP options set applied to a VPC that flows down to the subnets
- Controls DNS Servers, NTP Servers, Net BIOS Server
- Can create option sets but cannot edit them (so to make changes you must make a new one and allocate the DHCP option set to the new one)
- Can also define two important IP allocation options per set
	- Control if resources are assigned a public IPv4 address along with the private address automatically
	- Auto assign IPv6, but the subnet and VPC need to have an IPv6 allocation in order to use this
