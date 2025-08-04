
>[!note]- Post-Processing
>## Key Insights and Information from the DNS and Route 53 Transcript:
>
>**1. CNAME vs. Alias Records:**
>
>* **CNAME:** Maps a name to another name (e.g., www.example.com to example.com).
>    * **Limitation:** Cannot be used for the apex of a domain (e.g., example.com).
>* **Alias Record:** Maps a name to an AWS resource (like an Elastic Load Balancer).
>    * **Advantage:** Can be used for both apex domains and subdomains.
>    * **AWS Benefit:** Free requests when pointing to AWS resources.
>
>**2. When to Use Which:**
>
>* **CNAME:** Suitable for subdomains (e.g., www.example.com).
>* **Alias Record:** Essential for apex domains (e.g., example.com) when pointing to AWS resources.
>
>**3. AWS Resource Compatibility:**
>
>* Alias records are designed to work with AWS services like:
>    * Elastic Load Balancers
>    * API Gateway
>    * CloudFront
>    * Elastic Beanstalk
>    * Global Accelerator
>    * S3 buckets
>
>**4. Alias Record Types:**
>
>* **A Record Alias:** Used for pointing to AWS resources with an A record (e.g., ELB).
>* **CNAME Record Alias:** Used for pointing to AWS resources with a CNAME (less common).
>
>**5. Route 53 Specificity:**
>
>* Alias records are an AWS implementation and are only available within Route 53.
>
>
>**Overall:**
>
>The video emphasizes the importance of understanding the difference between CNAME and alias records, particularly when working with AWS services. Alias records offer a more flexible and cost-effective solution for managing DNS records pointing to AWS resources, especially for apex domains.
>

- "A" records map a name to an IP address
- catagram.io -> 1.3.3.7
- CNAME maps a name to another name
- www.catagram.io -> catagram.io
- CNAME is invalid for naked domain/apex domain
	- The domain without anything before it like catagram.io
- Many AWS services use a DNS name (ELBs)
- With just CNAME catagram.io -> ELB would be invalid
Alias
- Alias records map a name to an AWS resource and can be used for both naked/apex and normal records
- For non apex/naked - functions the same way as CNAME
- There is no charge for Alias requests pointing at AWS resoures
- For AWS services - default should be picking Alias
- Should be the same "type" (CName or A Alias) as what the record is pointing at
- Used by API Gateway, CloudFront, Elastic Beanstalk, ELB, Global Accelerator, S3