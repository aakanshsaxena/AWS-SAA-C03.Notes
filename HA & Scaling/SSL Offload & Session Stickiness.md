
>[!note]- Post-Processing
>## Key Insights and Information from the Elastic Load Balancer Transcript:
>
>**1. SSL Handling Methods:**
>
>* **Bridging (Default):**
>    * Load balancer decrypts SSL connections, sees unencrypted HTTP traffic.
>    *  Load balancer and EC2 instances need SSL certificates.
>    *  Pros: Load balancer can take actions based on HTTP content.
>    *  Cons: Certificate storage risk, EC2 instances need cryptographic capabilities.
>* **Pass-Through:**
>    * Load balancer forwards encrypted connections to EC2 instances without decryption.
>    *  Load balancer doesn't need an SSL certificate.
>    *  Pros: Enhanced security, AWS doesn't see the certificate.
>    *  Cons: Load balancing based on HTTP content is impossible, EC2 instances still need certificates and cryptographic capabilities.
>* **Offload:**
>    * Load balancer decrypts SSL connections but backend instances use HTTP.
>    * Load balancer needs an SSL certificate, EC2 instances don't.
>    * Pros: Reduced EC2 instance overhead, potential for smaller instances.
>    * Cons: Data is in plain text across AWS network.
>
>**2. Session Stickiness:**
>
>* **Purpose:** Maintain user sessions on the same backend instance for consistency.
>* **How it works:**
>    * Load balancer generates a cookie (AWS ALB) upon initial user request.
>    * Cookie is sent with subsequent requests, directing traffic to the same instance.
>* **Duration:** Customizable between 1 second and 7 days.
>* **Expiration/Failure:**
>    * Cookie expiration or backend instance failure triggers a new session assignment.
>* **Pros:** Enables stateful applications with load balancing.
>* **Cons:** Can cause uneven load distribution on backend servers.
>
>**3. Best Practices:**
>
>* Design applications to be stateless whenever possible.
>* Store user session data externally (e.g., DynamoDB) to avoid reliance on individual server state.
>* Choose the SSL handling method that best balances security, performance, and application requirements.
>
>
>
>This summary provides a clear understanding of the key concepts and considerations related to Elastic Load Balancers, SSL handling, and session stickiness.
>

SSL Offload
- Three types:
- Bridging
	- Listener is configured for HTTPS. Connection is terminated on the ELB & needs a certificate for the domain name
	- ELB initiates a new SSL connection to backend instances. Instances need SSL certificates and the compute required for cryptographic operations
- Pass-Through
	- Listener is configured for TCP. No encryption or decryption happens on the NLB. Connection is passed to backend instance
	- Each instnace needs to have the appropriate SSL certificate installed. With this architecture there is no certificate exposure to AWS -> all self-managed and secured.
- Offload
	- Listener is configured for HTTPS. Connections are terminated and then backend connections use HTTPS.
	- ELB to instance connections use HTTP - no cryptographic or certificate requirements
- Basically, bridging = AWS holds certificate in ELB and Instances -> also requires the instances to perform cryptographic operations so heavy on them, but secure
- Passthrough = Secure like bridging but we hold the certificates and self-manage and secure certificates, each instance still needs SSL certificate installed. Encrypted tunnel from client to instance.
- Offload = The encrypted tunnel exists on the public internet, backend AWS doesn't use encryption so less heavy on our instances, but less secure
Cookie Stickiness
- Stickiness generates a cookie which locks the device to a single backend instance for a duration
	- Can be anywhere between 1s to 7 days
- This can cause interruptions because it would mean every time a user connects to a new instance (they don't know this but ELB would do this for them), then they would need to restart basically (re log-in, add to cart, etc.)
- Solution to this is a longer connection stickiness or handling session details like cookies and user state off-instance like in DynamoDB.