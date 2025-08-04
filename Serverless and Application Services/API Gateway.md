
>[!note]- Post-Processing
>##  API Gateway: Key Insights and Information 
>
>This transcript provides a comprehensive overview of AWS API Gateway, highlighting its functionalities, architectural components, and deployment strategies. 
>
>**Here are the key takeaways:**
>
>**What is API Gateway?**
>
>* API Gateway is a fully managed service that enables developers to create, publish, maintain, monitor, and secure APIs at any scale. 
>* It acts as a front-end for backend services, handling routing, authentication, authorization, throttling, caching, and more.
>
>**Architectural Components:**
>
>* **API Gateway:** The central component that receives requests from clients and routes them to appropriate backend integrations.
>* **Integrations:** Backend services that provide the actual functionality of the API. These can be Lambda functions, HTTP endpoints, or other AWS services.
>* **Clients:** Applications or users that consume the API.
>
>**Key Features:**
>
>* **High Availability and Scalability:** API Gateway automatically scales to handle traffic fluctuations, ensuring consistent performance.
>* **Authentication and Authorization:** Supports various authentication methods, including Cognito, IAM, and custom authorizers.
>* **Throttling:** Limits the rate of API calls to prevent abuse and ensure fair resource allocation.
>* **Caching:** Reduces the load on backend services by caching frequently accessed responses.
>* **CORS Support:** Enables cross-origin requests, allowing APIs to be consumed by applications from different domains.
>* **Direct Integration with AWS Services:** Seamlessly integrates with services like Lambda, DynamoDB, SNS, and SQS.
>* **Open API Support:** Allows for easy definition and management of APIs using OpenAPI specifications.
>* **Endpoint Types:** Offers Edge Optimized, Regional, and Private endpoints to suit different deployment scenarios.
>
>**Deployment Strategies:**
>
>* **Stages:** Allows for separate environments for development, testing, and production.
>* **Canary Deployments:** Enables gradual rollout of new API versions to a subset of users before full deployment.
>
>**Benefits:**
>
>* **Simplified API Management:** Provides a centralized platform for managing all aspects of the API lifecycle.
>* **Improved Security:** Enforces authentication and authorization policies to protect APIs from unauthorized access.
>* **Enhanced Performance:** Caching and throttling mechanisms optimize API performance and scalability.
>* **Reduced Costs:** Efficient resource utilization and serverless integration can lead to cost savings.
>
>
>**Remember:** 
>
>* API Gateway is a powerful tool for building and managing APIs

>[!note]- Post-Processing
>## Key Insights and Information from API Gateway Lesson:
>
>**Error Codes:**
>
>* **400 Series (Client Errors):** Indicate issues on the client-side, such as incorrect request parameters, headers, or authentication.
>    * **400:** Generic client-side error (hard to diagnose)
>    * **403:** Access denied (authorizer or web application firewall)
>    * **429:** Throttling exceeded (API Gateway rate limits)
>* **500 Series (Server Errors):** Indicate issues on the server-side, despite a valid request.
>    * **502:** Bad Gateway (backend service returned invalid output)
>    * **503:** Service Unavailable (backend service is down or experiencing issues)
>    * **504:** Integration Failure (backend service took longer than 29 seconds to respond)
>
>**Caching:**
>
>* **Per Stage Configuration:** Caching settings are specific to each API Gateway stage (development, testing, production).
>* **Cache Size:** Default size is between 500 MB and 237 GB.
>* **Default Cache Duration:** 300 seconds (5 minutes).
>* **Benefits:**
>    * Reduced load on backend services
>    * Lower costs
>    * Improved performance due to lower latency
>
>**Important Notes:**
>
>* API Gateway can be configured to throttle requests.
>* Lambda functions backing API Gateway have a maximum response time of 29 seconds.
>* The cache can be cleared.
>
>**Resources:**
>
>* A link to detailed information about all API Gateway error codes is provided in the lesson.
>
>
>
>This summary provides a concise overview of the key points covered in the API Gateway lesson.
>

API Gateway 101
- Create and manage APIs
- Endpoint/entry-point for applications
- Sits between applications and integrations (services)
- HA, scalable, handles authorization, throttling, caching, CORS, transformations, OpenAPI spec, direct integration, + more
- Can connect to services/endpoints in AWS or on-premises
- HTTP APIs, REST APIs, and WebSocket APIs
![[Pasted image 20250725003737.png]]
Endpoint Types 
- Edge-Optimized
- Routed to the nearest CloudFront POP
- Regional - clients in the same region
- Private - endpoint accessible only within a VPC via interface endpoint
API Gateway - Stages
- APIs are deployed to stages, each stage has one deployment
- Stages can be enabled for canary deployments. If done, deployments are made to the canary not the stage. Stages enabled for canary deployments can be configured so a certain percentage of traffic is sent to the canary. This can be adjusted over time, or the canary can be promoted to make it the new base 'stage'
API Gateway - Errors
4XX - Client Error - Invalid request on client side
5XX - Server Error - Valid request, backend issue
400 - Bad Request - Generic
403 - Access Denied - Authorizer denies..WAF Filtered
429 - API Gateway can throttle - this means you exceeded that amount
502 - Bad Gateway Exception - bad output returned by Lambda
503 - service Unavailable - backing endpoint offline? Major service issues
504 - Integration Failure/Timeout - 29s Limit
API Gateway - Caching
- Cache TTL default is 300s, min 0s max 3600s. Can be encrypted. Cache size 500MB to 237GB.
- Calls are only made to backend integrations if request is a cache miss
- Cache is defined per stage within API Gateway
- Reduced load and cost. Improved performance