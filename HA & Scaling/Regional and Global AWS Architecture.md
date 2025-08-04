
>[!note]- Post-Processing
>## Key Insights and Information from the AWS Architecture Lesson:
>
>**Global vs. Regional Architectures:**
>
>* **Small-scale:** Exists in one region, no DR requirements.
>* **Regional with DR:** Exists in one region but with failover to a secondary region.
>* **Global:** Operates across multiple regions, resilient to failures in one or more regions.
>
>**Global Architectural Components (Netflix Example):**
>
>1. **Service Location and Discovery (DNS):**  
>    * Uses DNS to direct users to appropriate service endpoints.
>    * Route 53 is the AWS implementation, offering flexibility for various configurations.
>    * Health checks ensure routing to healthy regions.
>2. **Content Delivery Network (CDN):**
>    * Caches content globally for faster delivery to users.
>    * CloudFront is the AWS CDN, pulling content from an origin location (e.g., S3).
>3. **Global Health Checks and Failover:**
>    * Monitors infrastructure health in each region.
>    * Routes users to healthy regions automatically in case of failures.
>
>**Regional Architectural Components:**
>
>1. **Regional Entry Point:**
>    * Acts as the initial point of contact for regional traffic.
>    * Examples: Application Load Balancer, API Gateway.
>2. **Regional Scaling and Resilience:**
>    * Ensures application can handle traffic fluctuations and regional failures.
>3. **Application Services and Components:**
>    * Includes compute services (EC2, Lambda, ECS), storage (EBS, EFS, S3), databases (RDS, Aurora, DynamoDB), caching (ElastiCache, DAX), and application services (Kinesis, Step Functions, SQS, SNS).
>
>**Architectural Tiers:**
>
>1. **Web Tier:**
>    * Entry point for regional traffic.
>    * Abstracts customers from underlying infrastructure.
>2. **Compute Tier:**
>    * Provides application logic and functionality.
>    * Utilizes services like EC2, Lambda, or containers.
>3. **Caching Tier:**
>    * Improves performance by caching frequently accessed data.
>    * Uses services like ElastiCache or DynamoDB Accelerator (DAX).
>4. **Storage Tier:**
>    * Stores application data and media content.
>    * Utilizes services like EBS, EFS, S3.
>5. **Database Tier:**
>    * Stores structured data for the

Global
- Global service location & discovery (how do we access our application and discover it globally)
- Content delivery (CDN) and optimization
- Global health checks and failovers
Regional
- Regional entry point
- Scaling and resilience
- Application services and components
Architecture
- We can think of it as first using global services to "zoom in" onto a region where we host our infrastructure (in the case where we have many region infrastructure)
- Then, we have layers once we're zoomed into a specific region
- A user connects via Route 53 to our web tier, that has a compute tier that uses a storage tier and a caching system to access our DB tier. We can also have a separate app services tier (with things like SNS), as well as utilize CloudFront which lets the user access data (Netflix shows for example) directly through the S3 cache resulting in quicker times and less compute time
