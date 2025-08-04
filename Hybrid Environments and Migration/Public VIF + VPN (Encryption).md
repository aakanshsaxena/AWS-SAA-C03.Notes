>[!note]- AI
> #### Public vs Private VIFs
> - Private VIFs access private IPs; public VIFs access public IPs
> - Public VIFs access AWS-owned public IP addresses
> - Public VIFs are needed to access public IPs of virtual private or transit gateways
> - Choose VIF type based on the IPs you need to access
> - VPN over Direct Connect offers both security and low latency
> #### VPN and Encryption Details
> - VPN connects to virtual private or transit gateway transit-agnostic
> - VPN configuration is the same for public or private VIFs
> - VPN provides end-to-end encryption from customer to gateway
> - MacSec is single-hop encryption between DX router and cross connect
> - MacSec connects two parts in the same LAN layer
> - VPNs have wider vendor support than MacSec
> - VPNs have more cryptographic overhead than MacSec
> #### VPN and Direct Connect Integration
> - MacSec is faster and designed for terabit+ network speeds
> - VPN speeds limited by hardware due to cryptographic overhead
> - VPN can be used immediately; Direct Connect takes time
> - VPN can encrypt primary or backup traffic over Direct Connect
> - Clients use VPN and Direct Connect together for traffic encryption resilience
> - Direct Connect is primary; VPN acts as backup for resilience
> - Clients run multiple IPsec VPNs for continuous encryption
> #### VPN and Direct Connect Architecture
> - Direct Connect is primary with VPN as separate backup connection
> - VPN and Direct Connect architecture visually explained
> - Typical architecture includes two AWS regions: US East 1 and AP Southeast 2
> - Direct Connect locations include AP Southeast 2 region
> - Business premises shown on the right in architecture diagram
> - Using VPN with AWS Virtual Private Gateway
> #### VPN Endpoint Details
> - Two VPN endpoints created in AWS public zone per region
> - Two VPN endpoints created in different availability zones with public IPs
> - VPN endpoints can connect via public Internet with variable latency
> - IPSEC VPN over public VIF offers low, consistent latency
> #### VPN Performance and Connectivity
> - IPSEC VPN over public VIF uses encrypted tunnel with consistent latency
> - Direct Connect uses public VIF as transit for VPN
> - Direct Connect improves VPN performance across AWS global network
> - IPSEC VPN over Direct Connect enables global encrypted transit
> - IPSEC VPN over Direct Connect complements, not competes with maxac VPN
> - Connect to VPCs in remote regions with same equipment
> - Public VIF connects customer gateway to public IPs of AWS gateways
> - Public VIF is used to connect customer gateway to public IPs of AWS gateways

Public VIF + VPN
- Encrypted and authenticated tunnel over DX so we get low and consistent latency
- Uses a public VIF + VGW/TGW public endpoints
- Transit agnostic (DX/Public internet)
- End-2-End vs MACSec which is single hop based
- Wider vendor support for VPN
- More cryptographic overhead vs MACSec which limits speed but still can be used while DX is being provisioned or as a DX backup
Architecture
- We have two AWS regions (East 1 and SE 2), each has its own VPC
- We create a VGW in SE 2 which creates two VGW endpoints in the AWS public zone with public addressing.
- We can then connected from our business premises through the DX location, all while creating an encrypted tunnel, all the way to our AWS region
- Public VIF transit means its direct and low latency, and the VPN tunnel creates a private VPC connection between the customer gateway at our business premises and an AWS VGW or TGW. It uses a public VIF but creates a private connection into a VPC.
- Using a VPN also allows connections to VPCs in remote regions over the global AWS netowrk.