
>[!note]- Post-Processing
>## Key Insights and Information from the VPC Peering Transcript:
>
>**What is VPC Peering?**
>
>* VPC peering is a service that creates a private and encrypted network link between two VPCs.
>* It allows secure communication between VPCs, whether they are in the same or different regions, and even across different AWS accounts.
>
>**Important Facts:**
>
>* **One-to-one connections:** A single VPC peering connection links only *two* VPCs.
>* **Non-transitive routing:**  If VPC A is peered to VPC B, and VPC B is peered to VPC C, there is no automatic connection between VPC A and VPC C. A separate peering connection is required between VPC A and VPC C for them to communicate.
>
>**Benefits:**
>
>* **Private and encrypted communication:** All data transferred between peered VPCs is encrypted.
>* **Secure global transit:** Cross-region peering utilizes AWS's secure global network for fast and secure data transfer.
>* **DNS resolution:** You can configure VPC peering to resolve public hostnames to private IP addresses within the peered VPCs.
>* **Security group integration:** In the same region, VPC peering allows for efficient security group referencing and nesting, improving security.
>
>**Technical Considerations:**
>
>* **Routing configuration:**  You need to configure routing tables in each VPC to direct traffic to the remote VPC using the VPC peering connection gateway object.
>* **Security group and network ACL configuration:** Ensure that security groups and network ACLs allow traffic flow between the peered VPCs.
>* **Non-overlapping CIDR ranges:** VPCs cannot have overlapping IP address ranges for peering connections.
>
>**Alternatives:**
>
>* **Transit Gateway:** A more feature-rich service that allows for multi-VPC connectivity and routing without requiring individual peering connections between each VPC.
>
>
>This transcript provides a comprehensive overview of VPC peering, covering its key features, benefits, technical considerations, and limitations. It also highlights the importance of understanding routing concepts and security configurations for successful VPC peering implementation.
>

- Allows for direct encrypted network link between two VPCs 
- Works same/cross-region and same/cross-account
- Can optionally have public hostnames resolve to private IPs
- Same region SG's can reference peer SG's
- VPC peering does not support transitive peering
- Routing configuration is needed, SGs and NACLs can filter
![[Pasted image 20250726134830.png]]
- We can see here the architecture of VPC peering
- We create route tables at both sides of the peering connection that direct the traffic flow for the remote CIDR at the peer gateway object
- MAKE SURE that the VPC IP do not overlap, if they do then we cannot use VP Peering connections
- Peering is not transitive, just because A connects B, and B connects C -> A does not connect C
- Communication is encrypted and transits over the AWS global network