- Ask how many subnets will you need in each VPC?
- How many IPs will you need in total? How many will you need per subnet?
Subnet Essentials
- Services run within subnets, not directly from the VPC. Each subnet is located in a single AZ.
- Recommended to start with at least 4 AZ (A, B, C, and a spare for future growth)
- Recommended to normally have 4 tiers within each AZ (web, app, database, future growth)
- To maximize resilience, each tier should have its own subnet in each AZ. 4x4 = 16 subnets
- The VPC prefix size determines the number of subnets it can accommodate. A /16 VPC split into 16 subnets results in /20 subnets.
- Subnet size is determined by VPC prefix size, you can choose a larger VPC prefix to allow smaller subnet sizes, but make sure you have enough capacity for future growth.
Our Plan Part 2
- We reserved the range 10.16.0.0/16 for our AWS infrastructure - divided into 5 regions as listed above.
- Each region has 16 subnets allocated for its four AWS accounts (4 VPCs per account per region)
- Each account within each region receives four /16 network ranges (ex. 10.49, 10.50, 10.51, 10.52 because the first 16 bits - 8 bits per quartet are reserved - which is what /16 means, so then the 16 bits are given to us as our range)
 **VPC Structure:**  
>    - The plan assumes a VPC structure with three availability zones per region plus a spare, and three application tiers plus a spare.
>    - This results in a total of 16 subnets per VPC, each with a /20 subnet mask, providing 4,091 IP addresses per subnet.
**Top-Down vs. Bottom-Up Approach:** The speaker emphasizes the importance of carefully considering business needs and potential growth when designing the network topology. 
>    - This can be done either top-down (starting with the overall business requirements and working down) or bottom-up (starting with the minimum subnet size needed and working up).


