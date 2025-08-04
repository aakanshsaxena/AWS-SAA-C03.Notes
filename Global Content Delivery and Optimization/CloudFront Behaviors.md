
>[!note]- Post-Processing
>## CloudFront Behaviors: Key Insights and Information
>
>This transcript provides a concise overview of CloudFront Behaviors and their configuration within a distribution. Here are the key takeaways:
>
>**Distribution Level Configuration:**
>
>* **Price Class:** Determines edge location deployment (US, Canada, Europe, all). Affects cost and performance.
>* **Web Application Firewall (WAF):** Integrates with AWS WAF for layer 7 security.
>* **Alternate Domain Names:** Allows using custom domain names with HTTPS.
>* **SSL Certificate:** Use default or custom SSL certificate based on domain name.
>* **Security Policy:** Choose a security policy balancing security and browser compatibility.
>* **Supported HTTP Versions:** Configure supported HTTP versions.
>* **Logging:** Enable or disable logging.
>
>**Behavior Level Configuration:**
>
>* **Path Pattern:** Matches incoming requests to specific behaviors. Default behavior uses a wildcard.
>* **Origin/Origin Group:** Specifies the origin server for the request.
>* **Viewer Protocol Policy:** Controls the protocol used between the viewer and edge location (insecure, secure, redirect).
>* **HTTP Methods:** Define allowed HTTP methods for the behavior.
>* **Field Level Encryption:** Encrypt data from the edge location through the CloudFront network.
>* **Cache Directives:** Control caching behavior using legacy settings or newer cache policy and origin request policy.
>* **Restricted Viewer Access:** Restrict access to the behavior using trusted key groups or trusted signers. Requires signed cookies or URLs for access.
>* **Object Compression:** Automatically compress objects for the behavior.
>* **Lambda@Edge Functions:** Associate Lambda functions for custom logic at the edge.
>
>**Important Notes:**
>
>* **Caching and Restricted Access are Behavior-Specific:** This means different behaviors within the same distribution can have different settings.
>* **Exam Focus:** Memorize that caching controls and restricted access are configured at the behavior level.
>
>
>Understanding these distinctions between distribution and behavior configurations is crucial for effectively utilizing CloudFront and answering exam questions.
>

*Demo-Type Content - No Notes*
