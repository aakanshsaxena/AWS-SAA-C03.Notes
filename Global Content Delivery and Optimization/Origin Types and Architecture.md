
>[!note]- Post-Processing
>## Key Insights and Information from the CloudFront Origin Types Transcript:
>
>**1. Origins: Where CloudFront Gets Content**
>
>- Origins are the servers where CloudFront fetches content when a request isn't cached at an edge location.
>-  Origin groups allow for resilience by distributing requests across multiple origins.
>
>**2. Types of Origins:**
>
>- **S3 Buckets:**
>    - Simplest to integrate with CloudFront.
>    - Features:
>        - Origin access (identity and control)
>        - Viewer and origin protocol matching (HTTP/HTTPS)
>        - Passing through custom headers
>- **Media Package/Media Store:**
>    - Not covered in this lesson, but will be discussed elsewhere.
>- **Custom Origins (Web Servers):**
>    - More granular configuration options:
>        - Origin path
>        - Minimum SSL protocol version
>        - Origin protocol policy (HTTP only, HTTPS only, or match viewer)
>        - HTTP and HTTPS port selection
>    - Require additional security measures like custom headers for access control.
>
>**3. Origin Access:**
>
>- S3 origins: Use origin access identity (legacy) or origin access control (recommended).
>- Custom origins: Require custom headers for secure access.
>
>**4. Origin Protocol Policy:**
>
>- S3 origins: Viewer and origin protocols match (HTTP/HTTPS).
>- Custom origins: Can be configured independently (HTTP only, HTTPS only, or match viewer).
>
>**5. Exam Considerations:**
>
>- Understand the differences between S3 and custom origins.
>- Be familiar with origin access methods for both types.
>- Know how to configure origin protocol policy and minimum SSL protocol versions for custom origins.
>
>
>**6. Security:**
>
>- S3 origins: Offer built-in security through origin access.
>- Custom origins: Require custom headers for secure access control.
>


