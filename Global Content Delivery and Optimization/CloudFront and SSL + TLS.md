
>[!note]- Post-Processing
>## Key Insights and Information from the CloudFront and SSL Transcript:
>
>**CloudFront Basics:**
>
>* **Default Domain:** Each CloudFront distribution gets a default domain name (e.g., random-part.cloudfront.net) with a default SSL certificate (star.cloudfront.net).
>* **Custom Domains:** You can use alternate domain names (e.g., cdn.catagram.whatever) via DNS configuration.
>
>**SSL Certificates:**
>
>* **Requirement:** You need an SSL certificate for each alternate domain name you use, even if you don't use HTTPS.
>* **Certificate Manager (ACM):** Use AWS Certificate Manager (ACM) to generate or import SSL certificates.
>* **Regional vs. Global:**
>    * Usually, certificates need to be in the same region as the service.
>    * **Exception:** CloudFront is a global service, so certificates **must** be created in US East 1 (Northern Virginia).
>
>**HTTPS Configuration:**
>
>* **Options:**
>    * Allow both HTTP and HTTPS.
>    * Redirect HTTP to HTTPS.
>    * Only allow HTTPS.
>
>**Important Concepts:**
>
>* **Viewer and Origin Protocols:** Both the connection between the viewer and CloudFront edge location AND the connection between CloudFront and the origin server require valid public SSL certificates.
>* **Self-Signed Certificates:** Not allowed with CloudFront. Only publicly trusted certificates work.
>* **SNI (Server Name Indication):**  Allows one IP address to host multiple HTTPS websites with different certificates. Supported by modern browsers.
>* **Dedicated IP Addresses:** Required for CloudFront if you need to support browsers that don't support SNI. Costs $600 per month per distribution.
>
>
>Let me know if you have any other questions or need further clarification on any of these points.
>

>[!note]- Post-Processing
>## Key Insights and Information from the CloudFront SSL Architecture Transcript:
>
>**1. Certificate Requirements:**
>
>* **Viewer Side (Client to CloudFront):**
>    * **Must use a publicly trusted certificate:** Issued by major CAs like Codo, DigiCert, Spantag, or AWS Certificate Manager (ACM).
>    * **Certificate must match the CloudFront distribution's DNS name:**  Ensure consistency between the certificate and the domain name used by customers.
>    * **Self-signed certificates are not allowed.**
>* **Origin Side (CloudFront to Origin):**
>    * **Must use a publicly trusted certificate:** Same as viewer side, no self-signed certificates.
>    * **Certificate must match the DNS name of the Origin:**  Match the certificate to the domain name CloudFront uses to communicate with the origin.
>
>**2. Dedicated IP Address:**
>
>* **Required for mixed browser support (older and modern):**  Older browsers (pre-2003) may not support Etta and I, necessitating a dedicated IP address for compatibility.
>* **Costs $600 per month:**  This is an additional expense compared to using the shared IP address.
>
>**3. S3 Origins:**
>
>* **No need to apply certificates:** S3 handles SSL certificates natively.
>
>**4. Application Load Balancer Origins:**
>
>* **Require a publicly trusted certificate:** Can be generated externally or managed using ACM.
>
>**5. Custom Origins (EC2 instances or on-premise servers):**
>
>* **Require a publicly trusted certificate:** ACM cannot manage certificates for these origins, so manual application is necessary.
>
>**6. US East 1 Region:**
>
>* **Crucial for ACM certificates used with CloudFront:**  All CloudFront integrations with regional services, including certificates, must interact with US East 1.
>
>**7. Viewer Protocol:**
>
>* **Connection between viewers (customers) and CloudFront edge locations:**  Uses the publicly trusted certificate applied to the CloudFront distribution.
>
>**8. Origin Protocol:**
>
>* **Connection between CloudFront edge locations and origins:**  Uses the publicly trusted certificate applied to the origin.
>
>
>
>This summary provides a concise overview of the key points regarding SSL architecture in CloudFront, focusing on certificate requirements, IP address considerations, and origin-specific details.
>

CloudFront and SSL 
- CloudFront Default Domain Name (CNAME)
- https://d1111abcdef8.cloudfront.net
- SSL supported by default \*.cloudfront.net cert
- Alternate domain names (CNAMES) e.g. cdn.catagram...
- Verify ownership using a matching certificate
- Generate or import in ACM in US-EAST-1
- Three options for CloudFront: HTTP or HTTPS, HTTP redirects to HTTPS, HTTPS only
- Two SSL connections: Viwer -> Cloudfront and CloudFront -> Origin, both need valid public certificates and intermediate certs
CloudFront and SNI
- Historically, every SSL enabled site needed its own IP
- Because encryption starts at the TCP connection and host headers happen after that
- But we can use SNI which allows a host to be included so we can have many SSL certs/hosts using one shared IP
- If we want support for older browsers that don't support SNI, we can enable for 600 a month in CloudFront for a dedicated IP
Architecture
- We have two people connecting, one with new browser, one with old browser. We connect to CloudFront at CF Edge Location which supports non SNI capable browsers.
- Certificate is issued by a trusted CA such as Comodo, DigiCert, Symantec, or ACM and matches the DNS name
- S3 origins handles certificates natively, ALB has certificate from ACM, EC2 needs an external generated cert
- Origins need to have certificates issued by a trusted CA, ALB can use ACM, others need to use an external generated cert. No self-signed certs.