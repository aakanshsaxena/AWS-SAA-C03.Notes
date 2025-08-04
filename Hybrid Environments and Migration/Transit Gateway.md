> [!note]- AI
> #### Connectivity and Availability Details
> - Corporate office connectivity also required
> - Corporate office requires full mesh VPN connections to all VPCs
> - Current setup has a single point of failure
> - Add second customer gateway for full high availability
> - Full mesh network is complex and scales poorly
> #### Architecture Challenges and Solutions
> - Corporate office requires two customer gateways for HA
> - Full mesh complexity and scaling issues worsen with more networks
> - Transit gateway simplifies connectivity beyond full mesh complexity
> - Transit Gateway starts with the same basic architecture
> #### Transit Gateway Architecture
> - Transit Gateway introduced with four VPCs and two customer gateways
> - Transit Gateway supports site-to-site VPN attachments
> - Transit Gateway acts as AWS VPN termination point
> - Transit Gateway terminates VPNs, reducing direct VPC connections
> #### Transit Gateway Routing and Attachments
> - Transit Gateway reduces VPN tunnels while maintaining high availability
> - Four tunnels connect AWS availability zones to on-premises gateways
> - Transit Gateway creates attachments to VPCs via subnets in each AZ
> - Transit Gateway acts as a highly available InterVPC router
> - Transit Gateway enables full connectivity between all VPCs via VPN attachment
> - Transit Gateway enables on-premises to VPCs communication via VPN
> #### Transit Gateway Peering and Global Networking
> - Transit gateways can be peered across accounts and regions
> - Transit gateways can be peered across accounts and regions
> - Cross-region data uses AWS global network for predictable latency
> - Transit Gateway can attach to Direct Connect gateways for private networking
> #### Transit Gateway Routing Details
> - Dedicated lesson will cover specific Transit Gateway feature
> - Transit Gateway uses a default route table for traffic routing between attachments
> - Transit Gateway supports multiple route tables for complex routing
> - Transit Gateway supports transitive routing, avoiding full mesh topology
> #### Transit Gateway Sharing and Peering
> - Transit Gateway supports transitive routing for simplified network design
> - Transit Gateway can create global networks
> - Transit gateways can be peered across accounts and regions
> - Transit gateways can be shared across accounts using AWS RAM
> - Transit gateways can be peered across regions and accounts
> - AWS RAM enables sharing Transit Gateways across accounts
> - Transit Gateway reduces network complexity compared to VPC peering
> #### Transit Gateway Implementation
> - Transit Gateway is a resilient, scalable, highly available device
> - It massively reduces network complexity by enabling transitive routing

- Network Transit Hub to connect VPCs to on premises network
- Significantly reduces network complexity
- Single network object - HA and scalable
- Attachments to other network types
- VPC, Site-to-Site VPN, Direct Connect Gateway
w/o TGW Architecture
- Typically if we had four VPCs we wanted to connect to each other + our on-prem environment, we would need a VPC peering connection between each (6 VPC peering connections), plus two VPN tunnels per customer gateway we have. This doesn't scale well, becomes complex, and has lots of admin overhead
w/ TGW
- Instead we can have all the VPCs connect to the TGW (and they can communicate to any of the other VPCs connected/transitive), integrate a direct connect gateway using a transit VIF to our CGW, so we only have to create one connection between each VPC and TGW, and then two tunnels between our on-prem location and the TGW. This scales very well and is much easier to manage.
- We can also cross-peer TGW to use TGW in different accounts or regions.
TGW Considerations
- Supports transitive routing
- Can be used to create global networks
- Share between accounts using AWS RAM
- Peer with different regions, same or cross accounts
- Less complexity vs w/o TGW
