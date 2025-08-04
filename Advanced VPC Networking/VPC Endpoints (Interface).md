
>[!note]- Post-Processing
>## Key Insights and Information from the AWS Interface Endpoints Tutorial:
>
>**What are Interface Endpoints?**
>
>* Provide private access to AWS public services (like S3 and SNS) for instances within a VPC, even fully private ones.
>* Historically used for all services except S3 and DynamoDB, but now support S3. DynamoDB still requires gateway endpoints.
>
>**How do they differ from Gateway Endpoints?**
>
>* **Availability:** Gateway endpoints are highly available by design, while interface endpoints are not. You need to create multiple interface endpoints in each availability zone for high availability.
>* **Mechanism:** Interface endpoints use DNS and private IP addresses, while gateway endpoints use prefix lists and route tables.
>* **Security:** You can control access to interface endpoints using security groups, which isn't possible with gateway endpoints.
>
>**Key Features:**
>
>* **Private DNS:**  Overwrites the default service DNS with the interface endpoint's private IP address, allowing unmodified applications to use interface endpoints.
>* **Endpoint-Specific DNS Names:**  Applications can be updated to use these names directly for accessing the service via the interface endpoint.
>* **PrivateLink:**  The underlying technology that allows interface endpoints to function, also enabling the injection of third-party services into your VPC.
>
>**Important Considerations:**
>
>* **Protocol:** Currently only supports TCP and IPv4.
>* **Availability Zones:**  For high availability, create an interface endpoint in each availability zone used by your VPC.
>
>**In Summary:**
>
>Interface endpoints offer a flexible and secure way to access AWS services privately within your VPC. While they require more configuration than gateway endpoints, they provide granular control over security and DNS resolution, making them suitable for specific use cases.
>
>
>

- Provides private access to AWS public services, currently all minus DynamoDB (S3 is a new addition)
- Added to specific subnets, an ENI, and thus not HA
- For HA, add one endpoint, to one subnet, per AZ used in the VPC
- Network access controlled via security groups
- Endpoint policies can restrict what can be done with the endpoint
- TCP and IPv4 only
- Uses PrivateLink
- Endpoint provides a new service endpoint for DNS like vpce-123-xyz.sns.us-east-1.vpce.amazonaws.com
- Two DNS, endpoint regional/zonal DNS
- Applications can optionally use these or privateDNS overrides the default DNS for services
Architecture
- Typically, if we had a private instance we wouldn't be able to access public services without either a) being a public instance or b) a NGW
- But, by setting up an interface endpoint, our private instances would go the VPC router and then to the interface endpoint and route to the public service securely (almost as if the public service is within our VPC)
- Public instances would still function the same way
- However, if we use the endpoint-specific DNS/private DNS then, private DNS associates a private R53 hosted zone to the VPC changing the default service DNS to resolve to the interface endpoint IP
- So our public and private instances would follow the same path, VPC Router, to interface endpoint which connects directly to the public service