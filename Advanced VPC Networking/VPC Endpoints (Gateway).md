
>[!note]- Post-Processing
>##  Gateway Endpoints: Key Insights and Information
>
>This transcript explains **AWS Gateway Endpoints**, a way to provide private access to supported AWS services (currently S3 and DynamoDB) from within a VPC.
>
>**Here are the key takeaways:**
>
>* **Purpose:** Gateway endpoints allow private resources within a VPC to access public AWS services (like S3 and DynamoDB) **without** needing public IP addresses or NAT gateways.
>
>* **How it works:**
>    * You create a gateway endpoint per service per region.
>    * You associate it with one or more subnets in your VPC.
>    * AWS automatically configures a route in the subnet's route table, directing traffic destined for the service to the gateway endpoint.
>    * The gateway endpoint acts as a secure tunnel to the public service.
>
>* **Benefits:**
>    * **Enhanced Security:** Resources inside the VPC can access public services without exposure to the public internet.
>    * **Simplified Architecture:** Eliminates the need for internet gateways, NAT gateways, and public IP addresses for accessing supported services.
>    * **Private-Only Buckets:**  Can be used to create S3 buckets accessible only through the gateway endpoint, enforcing strict access control.
>
>* **Limitations:**
>    * **Region-Specific:** Gateway endpoints can only access services within the same region.
>    * **VPC-Bound:**  Only accessible from within the VPC they are associated with.
>
>* **Endpoint Policies:** Allow you to control which resources within the service can be accessed through the gateway endpoint.
>
>* **Architecture:** Gateway endpoints are highly available and managed by AWS. They don't require placement in a specific availability zone.
>
>**Comparison to Interface Endpoints:**
>
>The transcript mentions that interface endpoints offer similar functionality but are implemented differently. 
>
>
>Let me know if you'd like me to elaborate on any specific point or compare gateway endpoints to interface endpoints in more detail!
>

- Provide private access to S3 and DynamoDB
- Prefix List is added to the route table by the Gateway Endpoint
- HA across all AZs in a region by default
- Endpoint policy can be used to control what the Gateway Endpoint can access
- Regional, so it can't be used cross-region to access services
- Prevents leaky buckets since we can create a bucket policy on S3 buckets that only allows access from a specific gateway endpoint
Architecture
- We can have two AZ's with private instances, that route to a VPC router and then to a gateway endpoint which creates a kind of private tunnel between itself and the S3 bucket
- Because of this, we don't need public addressing for S3 or DynamoDB access (from our instances)
- We associate our gateway endpoint with a subnet (subnet association), and use endpoint policies to control what the Gateway Endpoint can be used for
- Gateway Endpoints are not accessible outside the VPC
- Region resilient by default

