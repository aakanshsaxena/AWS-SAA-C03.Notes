
>[!note]- Post-Processing
>## Key Insights and Information from the CloudFront, Lambda, and Edge Transcript:
>
>**What is Lambda at the Edge?**
>
>* A feature of CloudFront that allows you to run lightweight Lambda functions at CloudFront Edge locations.
>* Enables you to adjust traffic between the viewer and the origin in various ways.
>
>**Limitations:**
>
>* Runs on Node.js and Python only.
>* Cannot access VPC-based resources.
>* Lambda layers are not supported.
>* Different size and execution time limits compared to regular Lambda functions.
>
>**Architecture:**
>
>* Traditional CloudFront architecture with customers, edge locations, and origins.
>* Lambda functions can be integrated at each stage of the communication flow:
>    * **Viewer Request:** Runs after CloudFront receives a request from the viewer.
>    * **Origin Request:** Runs before CloudFront forwards the request to the origin.
>    * **Origin Response:** Runs after CloudFront receives a response from the origin.
>    * **Viewer Response:** Runs before the response is sent back to the viewer.
>
>**Memory and Timeout Limits:**
>
>* **Viewer Side:** 128MB memory, 5-second timeout.
>* **Origin Side:** Same memory limits as regular Lambda, 30-second timeout.
>
>**Example Use Cases:**
>
>* **A-B Testing:** Present different versions of content (e.g., images) without redirects.
>* **Gradual S3 Origin Migration:** Gradually shift traffic from an old to a new S3 origin.
>* **Device-Specific Content:** Display different content based on the viewer's device type and capabilities (e.g., DPI).
>* **Geo-Targeted Content:** Customize content based on the viewer's country.
>
>**Further Exploration:**
>
>* The transcript provides a link to additional resources with more examples and Lambda function code.
>
>
>**Important Note:**
>
>* For the AWS certification, understanding the Lambda at the Edge architecture is key.
>* You don't need to memorize specific function limits or code examples.

- You can run lightweight Lambda at edge locations
- Adjust data between the viewer and the origin
- Currently supports Node.js and Python
- Only run in the AWS Public Space
- Lambda Layers are not supported
- Different limits vs Normal Lambda functions
![[Pasted image 20250725235634.png]]Use Cases
- A/B Testing - Viewer Request (change what viewer sees)
- Migration between S3 origins - Origin Request
- Different objects based on device - Origin Request (maybe change resolution of image based on the monitor resolution of the monitor they are viewing on, etc.)
- Content by Country - Origin Request