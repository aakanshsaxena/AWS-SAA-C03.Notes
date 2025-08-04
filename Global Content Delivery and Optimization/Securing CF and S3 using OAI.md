
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>This transcript focuses on securing the content delivery path when using Amazon CloudFront, specifically addressing the "origin fetch side" - the transfer of data from origins to CloudFront and edge locations.
>
>**Here are the key takeaways:**
>
>* **Secure Content Delivery Path:** Securing the content delivery path is crucial to prevent unauthorized access to your content.
>* **Three Zones:**  Understanding the three zones involved is important: origins (where content is hosted), CloudFront network (consisting of the network itself and edge locations), and the public internet (where consumers access content).
>* **Origin Access Identities (OAIs):** OAIs are a key security mechanism for S3 origins. They act as a virtual identity for CloudFront distributions, allowing explicit control over access to S3 buckets.
>    * **Implicit Deny:** OAIs work with an implicit deny policy, meaning all access is denied by default except for the explicitly allowed OAI.
>    * **Best Practice:** It's recommended to create a dedicated OAI for each CloudFront distribution and S3 bucket for easier management.
>* **Securing Non-S3 Origins (Custom Origins):**  
>    * **Custom Headers:** CloudFront can add custom headers to requests sent to custom origins. These headers can be used by the origin to verify the request's source and ensure it's coming from a CloudFront edge location.
>    * **Traditional Firewall:** Using AWS-published IP ranges for CloudFront edge locations, a firewall can be configured to allow connections only from these IP ranges, effectively blocking direct access to the origin.
>* **Combined Approaches:** Both custom headers and traditional firewalls can be used together to enhance security for custom origins.
>
>**Overall, the transcript emphasizes the importance of securing the origin fetch side of the content delivery path using appropriate methods like OAIs, custom headers, and firewalls. This ensures that content is only accessible through authorized channels and prevents unauthorized access to your origins.**
>
>
>

Origin Access Identity (OAI)
- An OAI is a type of identity
- It can be associated with CloudFront Distributions
- CloudFront 'becomes' that OAI
- That OAI can be used in S3 bucket policies
- Deny all but one or more OAI's
Architecture when using S3 origin
- We can associate an OAI with our distribution which effectively lets our edge locations act as that OAI
- We create a bucket policy that allows access from that OAI but implicitly denies access from anywhere else
- Once OAI is associated with the distribution accesses are from the OAI
Securing Custom Origins
- We use an HTTPS connection between client and CloudFront and match this from CloudFront to our custom origin.
- We can then require a custom header that is injected securely at the edge location so that when our custom origin receives the request it checks for the custom header and refuses if it's not there (can't be falsified)
- Or, since CloudFront IP Ranges are publicly available we can set up a firewall around our custom origin that only allows traffic from the CF IP Ranges and no where else.
- Or we can use a combination of both these strategies.