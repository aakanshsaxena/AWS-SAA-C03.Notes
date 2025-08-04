
>[!note]- Post-Processing
>## AWS Certificate Manager (ACM) Key Insights:
>
>**What is ACM?**
>
>* AWS Certificate Manager (ACM) is a service for managing SSL/TLS certificates used to secure websites and applications.
>* It can act as a public certificate authority (CA) trusted by browsers or a private CA for internal use within an organization.
>
>**Why is ACM important?**
>
>* Essential for AWS certifications (associate and professional levels).
>* Crucial for real-world projects involving secure communication.
>
>**How does ACM work?**
>
>* **Public Mode:** Browsers trust certificates signed by ACM because it's a recognized CA.
>* **Private Mode:** Organizations configure their clients to trust their private ACM instance.
>* **Certificate Generation:** ACM can generate certificates for domains through DNS or email verification. It also automatically renews them.
>* **Certificate Import:** Users can import certificates from other sources but are responsible for renewing them.
>
>**Important Points:**
>
>* **Regionality:** ACM is a regional service. Certificates generated or imported in a region are locked to that region.
>* **Service Support:** ACM can only deploy certificates to supported services, primarily CloudFront and Application Load Balancers. EC2 is not supported due to security concerns.
>* **CloudFront:** Although global, CloudFront is treated as residing in US East 1 from an ACM perspective. All CloudFront certificates must be in US East 1.
>
>**Exam Focus:**
>
>* ACM frequently appears in exams, focusing on:
>    * Certificate regionality and deployment limitations.
>    * Supported services (CloudFront and Application Load Balancers).
>    * EC2's lack of support for ACM.
>    * CloudFront's US East 1 association with ACM.
>
>
>This summary provides a concise understanding of ACM's functionalities, key concepts, and exam relevance.
>

ACM
- HTTP - Simple and insecure
- HTTPS - SSL/TLS Layer of encryption added to HTTP
- Data is encrypted in-transit
- Certificates provide identity
- Can also use chain of trust - which means certificate is signed by a trusted authority
- ACM lets you run a public or private certificate authority (CA)
- Private CA - Applications need to trust your private CA
- Public CA - Browsers trust a list of providers, which can trust other providers
- ACM can generate or import certificates
- If generated, it can automatically renew
- If imported, you are responsible for renewal
- Certificates can be deployed out to supported services
- Support AWS services only (CloudFront, ALBs NOT EC2)
- ACM is a regional service, and certs cannot leave the region they are generated or imported in
- To use a cert with an ALB is ap-southeast-2 you need a cert in ACM in ap-southeast-2
- Global services like CloudFront operate as though within us-east-1
Architecture
- We have a certificate in each region that we have a supported service and a need for it. 
- Keep in mind we can't move certificates and we can't use them cross-region
- For CloudFront, the cert is deployed by ACM to the distribution, then the distribution sends to the edge locations which use certs to prove identity, establish trust and secure connections (because ACM is trusted by web browsers)