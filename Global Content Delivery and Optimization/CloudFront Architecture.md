
>[!note]- Post-Processing
>## CloudFront Architecture: Key Insights and Information
>
>This transcript provides a high-level overview of Amazon CloudFront's architecture, functionality, and key concepts. Here's a breakdown of the key insights:
>
>**What is CloudFront?**
>
>* CloudFront is a Content Delivery Network (CDN) that improves content delivery by caching and utilizing a global network.
>
>**How CloudFront Works:**
>
>* **Origin:** The original location of your content (e.g., an S3 bucket or a web server).
>* **Distribution:** The configuration unit within CloudFront. It defines how content is delivered, including origin settings, caching behavior, and domain name.
>* **Edge Locations:** Global points of presence (PoPs) where content is cached. There are over 200 edge locations worldwide, strategically placed close to users.
>* **Regional Edge Cache:** Larger caches located in specific geographic regions, serving multiple edge locations. They store less frequently accessed content for faster retrieval.
>
>**Benefits of Using CloudFront:**
>
>* **Improved Performance:** Delivers content from edge locations closer to users, reducing latency and improving load times.
>* **Reduced Origin Load:** Caching content at edge locations reduces the number of requests hitting the origin server, improving its performance and scalability.
>* **Global Reach:** Content is distributed globally, ensuring fast access for users worldwide.
>
>**Important Architectural Points:**
>
>* **Domain Name:** Each CloudFront distribution has a unique domain name ending in ".cloudfront.net". You can also use your own custom domain name.
>* **SSL Integration:** CloudFront integrates with AWS Certificate Manager (ACM) for secure HTTPS connections.
>* **Read-Only Caching:** CloudFront performs read-only caching. It does not cache write operations.
>
>**Further Learning:**
>
>The transcript emphasizes that the distribution is the core configuration entity, but detailed configurations are not directly stored within it. This suggests that further lessons will delve into the specifics of configuring distributions and leveraging CloudFront's advanced features.
>
>
>

>[!note]- Post-Processing
>## Key Insights from CloudFront Configuration Transcript:
>
>**1. Centralized Configuration:**
>
>* While CloudFront distributions provide a high-level configuration, the detailed settings reside within **behaviors**.
>* Behaviors act as **sub-configurations** within distributions, allowing for granular control over specific aspects of content delivery.
>
>**2. Pattern Matching:**
>
>* Behaviors operate on a **pattern matching** principle. Each behavior defines a specific path pattern that triggers its configuration.
>* This enables different configurations for different parts of your website or application.
>
>**3. Hierarchy:**
>
>* **Distributions** receive high-level configuration and manage multiple **behaviors**.
>* **Behaviors** are linked to **origins**, determining how content is fetched and delivered.
>
>**4. Default Behavior:**
>
>* Every distribution has a **default behavior** with a wildcard pattern (`*`), capturing everything not matched by other behaviors.
>* This ensures that all requests are handled, even if no specific behavior matches.
>
>**5. Specificity:**
>
>* More specific behaviors take precedence over less specific ones.
>* This allows you to prioritize certain configurations for specific paths or content types.
>
>**6. Configuration Options:**
>
>* Behaviors control various aspects of content delivery, including:
>    * **TTL (Time To Live)**
>    * **Policies**
>    * **Origins**
>    * **Public/Private access**
>
>**7. Focus Areas:**
>
>* The remaining lessons will delve deeper into specific functionalities provided by CloudFront.
>
>
>**In essence, CloudFront's configuration relies on a hierarchical structure of distributions and behaviors, leveraging pattern matching to apply granular configurations for different parts of your content delivery pipeline.**
>

CloudFront Terms
- Origin - The source location of your content
- S3 origin or custom origin
- Distribution - the 'configuration' unit of CloudFront
- Edge Location - local cache of your data
- Regional Edge Cache - larger version of an edge location. Provides another layer of caching
CloudFront Architecture
- We have an S3 bucket that is our origin and then a distribution that we configured. When a user goes to try and retrieve data, CloudFront first checks if it is in the edge location cache, if not it will check regional edge cache, and finally will check origin and perform an origin fetch.
- When origin fetch, or regional edge cache hit happens then everything down the chain adds that item to its cache.
-  Distribution contains the configuration deployed to the edge locations. We connect to the edge locations that has distributions which can have many behaviors which are configured with a path pattern. If requests match that pattern - that behavior is used otherwise the default. Origins are used by behaviors as content sources.

