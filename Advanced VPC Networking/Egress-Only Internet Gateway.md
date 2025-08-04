
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**Egress-Only Internet Gateway:**
>
>* **Purpose:** Allows connections from within a VPC to the internet but prevents connections from the internet to instances within the VPC.
>* **Necessity:**  Addresses the inherent difference between IPv4 and IPv6 in AWS.
>    * IPv4: Private instances require NAT gateways for internet access, blocking inbound connections.
>    * IPv6: All addresses are public, requiring a mechanism to control inbound traffic.
>* **Functionality:**
>    * Allows outbound connections from IPv6 instances to the internet and public AWS services.
>    * Allows inbound traffic (responses) from the internet to the VPC.
>    * Blocks any unsolicited inbound connections from the internet.
>
>**Architecture:**
>
>* Identical to a regular internet gateway in terms of setup and availability.
>* Requires a default IPv6 route in the subnet's route table pointing to the egress-only internet gateway.
>
>**Use Cases:**
>
>* Environments where only outbound connectivity is required for IPv6 instances.
>* Scenarios mimicking the security features of NAT gateways for IPv6.
>
>**Comparison with Normal Internet Gateway:**
>
>* Normal Internet Gateway allows both outbound and inbound traffic for both IPv4 and IPv6 instances.
>* Egress-only Internet Gateway specifically controls inbound traffic for IPv6 instances, blocking unsolicited connections.
>
>**Demo Lesson:**
>
>* The transcript encourages viewers to implement an egress-only internet gateway in a demo lesson for practical understanding.
>
>
>
>Let me know if you have any other questions.
>

- IPv4 addresses can be private or public
- NAT allows private IPs to access public networks without allowing externally initiated connections in
- With IPv6 all IPs are public, and the IGW allows all IPv6 IN and OUT
- Egress-only is outbound-only for IPv6
Architecture
- We have EC2 instances in two AZ's and by default the egress-only gateway is HA across all AZs in the region
- We add a default IPv6 route ::/0 to the RT with the eigw-id as target, it send the data from here to the IGW.
- Inbound is denied but we can make outbound requests
