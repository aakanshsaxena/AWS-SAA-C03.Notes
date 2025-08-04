
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**What are Private Hosted Zones?**
>
>* Private hosted zones in AWS Route 53 are similar to public hosted zones but are **only accessible within the VPCs they are associated with**. 
>* They are not accessible from the public internet.
>
>**How do they work?**
>
>* You can associate private hosted zones with VPCs using the console UI, CLI, or API.
>* VPCs associated with a private hosted zone can access its records via the Route 53 resolver.
>* Unassociated VPCs cannot access the private hosted zone, just like users on the public internet.
>
>**Use Cases:**
>
>* **Internal DNS for VPCs:** Provide DNS resolution for resources within your VPCs.
>* **Split View/Split Horizon DNS:**  
>
>    * Create a public hosted zone and a private hosted zone with the same name.
>    * The public hosted zone contains records accessible to the public internet.
>    * The private hosted zone contains additional records accessible only within your VPCs.
>    * This allows you to use the same domain name for both public and internal access with different sets of records.
>
>**Example:**
>
>* A company uses a private hosted zone to store internal resources like accounting records.
>* They also have a public hosted zone with a subset of records accessible from the internet.
>* Users on the internet can access the public website, while users within the company's VPC can access both the public website and the internal resources through the private hosted zone.
>
>**Important Considerations:**
>
>* Services need to be running within a VPC associated with the private hosted zone to access its records.
>* Understanding split view DNS is crucial for architects, developers, and engineers working with AWS DNS.
>
>
>
>Let me know if you need further clarification on any aspect of private hosted zones!
>

- A public hosted zone which isn't public
- Associated with VPCs and only accessible in those VPCs, using different accounts is supported though via CLI/API
- Split-view (overlapping public & private) can be used for public and internal use with the same zone
Architecture
- R53 zone is inaccessible from the public internet. Zone cannot be queried outside of associated VPCs.
- In order to have access to the R53 zone with the resource records you must be in a VPC that is associated with the private zone (will connect to DNS resolver and then connect to private zone).
- Use **public zones** to expose services to the **world**
- Use **private zones** to make services discoverable **only inside AWS VPCs**.
R53 Split View Hosted Zones
- From the public internet, some of the records are visible to them.
- Accessed same way as public zone
- Resource records in the private hosted zone are not accessible from the public internet
- From the private VPC, all resource records can be accessed.
- Inside VPCs associated with private hosted zone are commonly used, so that the private zone is a superset, containing the more sensitive records.