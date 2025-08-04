
>[!note]- Post-Processing
>## Key Insights and Information from the Serverless Architecture Lesson:
>
>**What is Serverless Architecture?**
>
>* It's a software architecture where developers manage little to no servers.
>* It aims to minimize server-related overhead (cost, administration, risk).
>* It combines elements of microservices and event-driven architectures.
>
>**Key Concepts:**
>
>* **Functions as a Service (FaaS):** Applications are broken down into small, specialized functions that execute on demand.
>* **Stateless and Ephemeral Environments:** Functions run in temporary, clean environments, allowing them to run anywhere.
>* **Event-Driven:** Functions are triggered by events (user interactions, system events, etc.), ensuring they only run when needed.
>* **Managed Services:** Leveraging third-party services like S3, DynamoDB, and Cognito reduces the need for self-managed infrastructure.
>* **Pay-as-you-go:** Costs are incurred only when resources are used, leading to potentially lower overall expenses.
>
>**Benefits:**
>
>* Reduced operational overhead
>* Scalability and elasticity
>* Cost efficiency
>* Faster development cycles
>
>**Example: PetTube Application**
>
>The lesson uses the example of a video-sharing platform called PetTube to illustrate serverless architecture in action.
>
>* **Client-side:** Users interact with the application through a static website hosted on S3, with JavaScript running in their browsers.
>* **Authentication:** Third-party identity providers (e.g., Google) handle user authentication, reducing administrative burden and complexity.
>* **Function Triggers:**
>
>    * Uploading a video triggers a Lambda function that processes and transcodes the video using Elastic Transcoder.
>    * Retrieving video information triggers another Lambda function that fetches data from DynamoDB.
>
>**Next Steps:**
>
>* The lesson encourages learners to explore the "Pent Cuddle-a-Tron" demo to gain practical experience implementing a serverless application.
>* It highlights the importance of understanding the core concepts and principles of serverless architecture.
>
>
>
>Let me know if you have any other questions or would like me to elaborate on any specific aspect.
>

What is serverless
- Serverless isn't one single thing
- You manage few, if any servers - low overhead
- Applications are a collection of small and specialized functions which are stateless and ephemeral environments -> thus we are billed only during usage
- Event-driven, we only consume the product when it's being used
- FaaS is used where possible for compute functionality
- Managed services are used when possible
![[Pasted image 20250724234938.png]]- In this example, we use S3 to host website, Google IDP (Third party) to authenticate a user, which we swap for AWS temp credentials using Cognito, upload the video using temp credentials to our S3 bucket, which generates an event for Lambda to use Elastic Transcoder, which transcodes the media and sends to either S3 or DynamoDB which resends it to Lambda and then the user.