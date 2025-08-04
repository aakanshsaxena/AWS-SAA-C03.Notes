
>[!note]- Post-Processing
>## AWS Site-to-Site VPN: Key Insights & Information
>
>This transcript provides a comprehensive overview of AWS Site-to-Site VPN architecture, highlighting key points for exam preparation and real-world implementation. 
>
>**Here are the main takeaways:**
>
>* **Purpose:** Site-to-Site VPNs establish encrypted connections between an AWS VPC and an on-premises network, enabling secure data transfer over the public internet (or Direct Connect).
>* **Architecture:**
>
>    * **VPC:**  The AWS virtual private cloud that will be connected.
>    * **Virtual Private Gateway (VGW):**  A logical gateway object in AWS, representing a highly available endpoint for the VPN connection.
>    * **Customer Gateway (CGW):** Represents the physical router on the customer's premises.
>    * **VPN Connection:**  The link between the VGW and CGW, establishing encrypted tunnels for data flow.
>
>* **High Availability:**
>
>    * **VGW:**  By design, highly available due to physical endpoints in different availability zones.
>    * **Partial Availability:**  Standard implementation relies on a single customer router, creating a single point of failure.
>    * **Full Availability:** Achieved by using two customer routers with separate internet connections, ideally in different locations, and configuring two VPN connections to the VGW.
>
>* **VPN Types:**
>
>    * **Static:** Requires manual configuration of IP addressing information on both sides.
>    * **Dynamic:**  Automatically adjusts IP addressing information.
>
>* **Provisioning:**  Site-to-Site VPNs can be provisioned quickly (less than an hour) compared to physical connections like Direct Connect.
>
>
>**Remember:**
>
>*  VPN connections are encrypted using IPsec.
>*  The on-premises network and VPC IP address ranges must be configured correctly.
>*  For full high availability, use two customer routers and two VPN connections.
>
>
>
>This summary provides a clear understanding of AWS Site-to-Site VPN architecture and its key considerations for both exam preparation and real-world deployments.
>

>[!note]- Post-Processing
>## Key Insights and Information from the VPN Transcript:
>
>**Types of VPNs:**
>
>* **Static VPN:**
>    * Uses IPsec protocol.
>    * Simple to set up.
>    * Limited in features like load balancing and multi-connection failover.
>    * Works with any router combination.
>* **Dynamic VPN:**
>    * Uses BGP (Border Gateway Protocol) for route communication.
>    * Enables advanced availability features like load balancing and multi-connection failover.
>    * Requires BGP support on customer routers.
>    * Allows for automatic route learning through route propagation.
>
>**VPN Considerations:**
>
>* **Speed:**
>    * Maximum throughput of 1.25 GB per second per connection (two tunnels).
>    * Encryption introduces processing overhead, impacting performance at high speeds.
>    * Consider data transfer charges.
>* **Latency:**
>    * Transits over the public internet, potentially introducing latency and variability.
>    * May not be suitable for latency-sensitive applications.
>* **Cost:**
>    * Hourly operational cost.
>    * Data transfer charges.
>    * Potential impact on on-premises internet connection usage (data caps).
>* **Setup Time:**
>    * Very quick to set up (hours or less).
>    * Requires BGP support for dynamic VPNs.
>
>**VPN Benefits:**
>
>* **Speed of Deployment:**
>    * Significantly faster to set up compared to other private connection technologies.
>* **Backup Solution:**
>    * Can be used as a backup for physical connections like Direct Connect.
>* **Transitional Solution:**
>    * Can be used as a temporary solution while provisioning Direct Connect.
>
>
>**Important Exam Points:**
>
>* **Speed Limit:** 1.25 GB per second per connection.
>* **Latency:** VPNs may introduce latency due to public internet transit.
>* **BGP Support:** Required for dynamic VPNs.
>* **Setup Speed:** VPNs are significantly faster to set up than other private connection technologies.
>
>
>
>This summary provides a concise overview of the key insights and information regarding static and dynamic VPNs.
>

- A logical connection between a VPC and on-premises network encrypted using IPSec, running over the public internet
- Can be fully HA if you design and implement it correctly
- Quick to provision, under an hour
- Uses virtual private gateway (VGW), Customer Gateway (CGW), VPN connection between VGW and CGW
![[Pasted image 20250726221456.png]]
- We can see an example of a HA Site-to-Site VPN. We create this by using multiple AZ's in AWS, and using multiple VPN's in our public zone that connect to the CGW.
- Each VPN in AWS creates two ENI's for us to use.
- We have primary and backup infrastructure in every step now.
Static v Dynamic VPN
- Static 
	- Routes for remote side added to route tables as static routes
	- Networks for remote side statically configured on the VPN connection
	- No load balancing and multi connection failover
- Dynamic
	- Routes for remote side added to route tables as static routes
	- Border Gateway Protocol is configured on both the customer and AWS side using BGP and ASN. Networks are exchanged via BGP
	- Multiple VPN connections provide HA and traffic distribution
- If we enable route propagation, it means that routes are added to RT's automatically.
VPN Considerations
- Speed limitations = 1.25Gbps
- Latency Considerations - inconsistent, public internet
- Cost - AWS hourly cost, GB out cost, data cap (on premises)
- Speed of setup - very quick, software config, takes hours max
- Can be used as a backup for direct connect (DX)
- Can be used on top of DX to encrypt data