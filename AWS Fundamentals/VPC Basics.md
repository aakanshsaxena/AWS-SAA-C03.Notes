- VPC = Virtual Network in AWS
    
- VPC is within 1 account & 1 region
    
- Private and isolated unless you decide otherwise
    
- Two types of VPC available inside a region - default VPC and custom VPCs (can only have **one** default VPC per region, many custom VPCs)
    
- Use custom VPCs in almost all AWS deployments
    
- Unless configured, there's no way for two VPCs to communicate beyond their boundaries
    
- VPC are regionally resilient
    
- VPC CIDR - the range of IP addresses that the VPC can use
    
- Custom VPCs can have custom IP CIDR, default only have one (172.31.0.0/16)
    
- 172.31.0.0/16 means first 16 bits are network bits (unchangeable), rest are. So 172.31.0.0/8 would mean that 8 bits are network bits and rest are changeable: 172.0.0.0 to 172.255.255.255
    
- To create resilience in a region, VPC spread out through subnets across the different availability zones with each subnet having a specific part of the VPC CIDR dedicated to it (for example SN-A: 172.31.0.0/20, SN-B: 172.31.16.0/20)
### Default VPC Facts

- One per region - can be created & removed
    
- Default VPC CIDR is always 172.31.0.0/16
    
- /20 subnet in each AZ in the region
    
- Internet Gateway (IGW), Security Group (SG), NAGL
    
- Subnets assign public IPv4 addresses
    
- Best practice to not use default VPCs and instead create custom VPCs