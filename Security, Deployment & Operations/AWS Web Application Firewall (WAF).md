> [!note]- AI
> #### Rule Logic and Actions
> - **Matching Criteria:** AWS WAF rules are based on a set of criteria using logical operators (AND/OR). These criteria can be as simple as an IP address set or as complex as a regular expression pattern matching on a specific part of an HTTP request body or header.
> - **Rule Actions:** When a request matches a rule's criteria, WAF performs one of five possible actions:
>     - **Allow:** The request is allowed to proceed to the protected resource. This action stops the evaluation of any further rules in the Web ACL.
>     - **Block:** The request is denied and a 403 Forbidden response is returned. This action also stops further processing of the Web ACL.
>     - **Count:** The request is logged as a match in CloudWatch and continues to be evaluated by subsequent rules in the Web ACL. This is useful for testing rules before putting them into production.
>     - **Challenge:** The request is sent a non-interactive challenge to verify that it's from a legitimate browser, but without a visible CAPTCHA puzzle.
>     - **CAPTCHA:** A CAPTCHA puzzle is presented to the user to confirm they are human. If the user solves the puzzle, a token is issued and subsequent requests are not challenged again until the token expires. This is a very effective way to block bot traffic without blocking legitimate users.
> - **Rate-Based Rules:** These special rules count requests from an IP address over a five-minute period. They are designed to mitigate DDoS attacks and brute-force attempts. Rate-based rules **do not support the `allow` action**. They can only be configured to `block`, `count`, `challenge`, or `captcha`.
> #### Custom Responses and Labels
> - **Custom Responses:** For a `block` action, you can configure a custom HTTP response code (e.g., 403, 404) and a custom body, which is a powerful feature for returning a user-friendly error message or a specific redirect.
> - **Custom Headers:** For `allow`, `count`, and `captcha` actions, you can add custom headers to the request. These headers are prefixed with `x-amzn-waf-on-`, and your application can inspect them to react to the WAF's evaluation (e.g., to log a counted request or to trigger a different user experience).
> - **Labels:** WAF can add labels to requests that match a rule. Labels are useful for creating complex, multi-stage rule flows within a single Web ACL. An action like `count` or `captcha` can add a label to a request, which can then be used by a later rule in the Web ACL as a matching condition. This allows for a more granular and sophisticated security policy.
> #### AWS WAF Pricing
> - **Web ACL and Rule Fees:**
>     - **Web ACLs:** A flat monthly fee of **$5.00 per Web ACL** (prorated hourly). This fee is charged for each Web ACL you create, regardless of the number of resources it protects.
>     - **Rules:** A monthly fee of **$1.00 per rule** (prorated hourly). This applies to custom rules you create, as well as each rule within an AWS Managed Rule Group or Marketplace Rule Group.
> - **Request Fees:**
>     - A charge of **$0.60 per 1 million requests** processed by a Web ACL. The number of protected resources (e.g., a CloudFront distribution and an Application Load Balancer) using the same Web ACL will increase the total requests and thus the cost.
> - **Intelligent Threat Mitigation:** Additional fees apply for advanced managed rule groups:
>     - **Bot Control:** A monthly subscription fee plus a per-request fee for requests processed by the rule group.
>     - **Fraud Control:** A monthly subscription fee for services like Account Takeover Prevention (ATP) and Account Creation Fraud Prevention (ACFP), plus a fee per thousand login attempts analyzed.
>     - **CAPTCHA/Challenge Actions:** These have a separate usage-based fee. For example, CAPTCHA is priced per thousand attempts.
> - **Cost Management:** It is highly recommended to use the **AWS Pricing Calculator** for a detailed cost breakdown and to track costs using AWS Cost Explorer, especially when using multiple Web ACLs or advanced features. Pricing may vary across regions and is subject to change.

- A WAF is a Layer 7 Firewall that operates using a Web ACL, which can contain many things like:
	- AWS Managed Rules, Allow List, Deny List, Protection against SQL Injection, XSS, HTTP Flood, IP Reputation, BOTS
- Rules are put within rule groups -> within WebACL
- We can put the logs from the WAF into S3 (every 5 mins), CW Logs, or Firehose (much quicker), and then have Lambda Event Driven processing of logs or event subscriptions
Web Access Control Lists (WEBACL
- WEBACL Default Action - Allow/Block
- Resource Type - CloudFront or Regional Service
- For ALB, API GW, AppSync -> pick region
- Add Rule Groups or Rules, processed in order
- Web ACL Capacity Units (WCU) - default 1500
	- but can be increased via a support ticket
- WEBACL's are associated with resources which can take time, so adjusting a WEBACL takes less time than associating one
Rule Groups
- Contain rules
- Don't have default actions, that's defined when groups or rules are added to WEBACL's
- Managed (AWS or marketplace), yours, service owned
- Rule groups can be referenced by multiple WEBACL
- Have a WCU capacity (defined upfront, max 1500
WAF Rules
- Type, statement, action
- Type: regular, rate-based
- Statement: what to match, count all, what&count
	- origin country, IP, label, header, cookies, query parameter, URI path, query string, body (first 8192 bytes), HTTP method
- Single, AND, or, not
- Action: Allow, Block, Count, Captcha, Custom Response, Label
	- labels can be referenced later in the same WEBACL, multi-stage flows
- Allow and block stop processing, count/captcha actions continue
Pricing
- WEBACL - $5/Month (WACLs can be reused)
- RULE on WEBACL - $1/Month
- Requests per WEBACL - $0.6/1M
- Bot Control - $10/Month + $1/1M
- Captcha - $0.40/1K
- Fraud Control/Account Takeover - $10/Month + $1/1K Login Attempts