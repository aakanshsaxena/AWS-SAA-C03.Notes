
>[!note]- Post-Processing
>## Key Insights and Information from the Video Transcript:
>
>**CloudFront Security Modes:**
>
>* **Public:** Any viewer can access content. This is the default mode.
>* **Private:** Requests require signed URLs or signed cookies for access.
>
>**Private Behaviors:**
>
>* **Configuration:** CloudFront distributions can have public or private behaviors.
>* **Signers:** Both methods require a signer to create signed URLs or cookies.
>* **Old Method:** CloudFront keys tied to AWS accounts are used as trusted signers.
>* **New Method (Preferred):** Trusted key groups are used, allowing for more flexible key management and association with multiple public keys.
>
>**Signed URLs vs. Signed Cookies:**
>
>* **Signed URLs:**
>    * Access granted to a single object.
>    * Used when clients don't support cookies.
>    * Generate custom URLs.
>* **Signed Cookies:**
>    * Access granted to groups of objects (e.g., all files of a specific type).
>    * Maintain application-specific URL formats.
>
>**Catagram Application Example:**
>
>* Uses CloudFront for content delivery.
>* Public behavior handles non-sensitive content.
>* Private behavior handles sensitive content (e.g., cat images).
>* Serverless architecture with API Gateway, Lambda, and S3.
>* ID Federation for user logins.
>* Lambda signer function generates signed cookies for authorized access to private content.
>* Origin access identity secures S3 origin, preventing bypass.
>
>**Key Takeaways:**
>
>* Private behaviors in CloudFront are essential for securing sensitive content.
>* Use trusted key groups for more flexible and secure key management.
>* Choose between signed URLs and signed cookies based on access requirements and client capabilities.
>* Ensure the origin (e.g., S3) is also secure to prevent content bypass.
>
>
>
>

Private Distributions (*behaviors)
- Public - open access to objects
- Private - requests require signed cookie/URL
- 1 behavior - whole distribution is either public or private
- Multiple behaviors - each is public or private
- Old Method
	- CloudFront Key is created by Account Root User
	- The account is added as a trusted signer
- New
	- Trusted key groups are added
Signed URLs vs Cookies
- SignedURLs provides access to one object
- Use URL's if your client doesn't support cookies
- Cookies provide access to groups of objects
- Use for groups of files/all files of a type (example all cat gifs)
- Or if maintaining application URL's is important 
Private Distribution Architecture
- We have users on our Catagram app that are requesting some private pictures.
- We have a default path for public images and then a private behavior for the private images S3 bucket
- We request a private picture so we go to through CloudFront to the API Gateway and then the Lambda signer confirms our access after we log in and if we have access to the images it will grant us a signed cookie (because our AWS infrastructure here is on the AWS account which is a trusted key group)
- Then, we will use this signed cookie and give it to CloudFront which will validate it and give us access to the private images S3 bucket
![[Pasted image 20250725234557.png]]