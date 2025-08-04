> [!note]- AI
> #### AWS Shield Standard
> - **Automatic and Free:** This is the baseline level of DDoS protection that is automatically enabled and available to all AWS customers at no additional cost.
> - **Network-Level Protection:** It provides always-on detection and in-line mitigation of the most common and frequent network and transport layer (Layer 3 and Layer 4) DDoS attacks, such as SYN floods and UDP reflection attacks.
> - **Perimeter Defense:** This protection occurs at the AWS network perimeter or near the edge network, meaning it protects your resources before the traffic even reaches your VPC.
> - **Limited Scope:** Shield Standard is not configurable and does not provide proactive engagement or advanced metrics.
> #### AWS Shield Advanced
> - **Paid Service:** Shield Advanced is a paid service with a commitment of **$3,000 per month** and a one-year minimum subscription. The subscription is billed to the organization's payer account and covers all accounts under that organization.
> - **Explicit Activation:** Unlike Shield Standard, Shield Advanced is not automatic. You must explicitly enable protection for specific resources through the AWS Management Console or AWS Firewall Manager.
> - **Protected Resources:** It extends protection to a wider range of resources, including:
>     - Application Load Balancers (ALB) and Classic Load Balancers
>     - Amazon CloudFront distributions
>     - Amazon Route 53 hosted zones
>     - AWS Global Accelerator accelerators
>     - Elastic IP addresses
> - **Cost Protection:** A key benefit is **DDoS cost protection**. Shield Advanced provides service credits for charges related to a DDoS attack on a protected resource, such as increased Data Transfer Out or scaling-related costs, that are not mitigated by AWS. This protection does not apply to normal scaling events from excessive legitimate traffic.
> - **Proactive Management and Support:**
>     - **DDoS Response Team (SRT):** You get 24/7 access to the AWS DDoS Response Team (SRT) for help during an active DDoS attack. The SRT can apply custom mitigations and help you design a more resilient architecture.
>     - **Proactive Engagement:** With the help of the SRT, you can configure proactive health checks (using Amazon Route 53) to detect attacks on your application faster, reducing the impact on performance.
> #### Advanced Features and Integration
> - **Health-Based Detection:** This feature uses Amazon Route 53 health checks to detect application unresponsiveness. By using this health data, Shield Advanced can more quickly and accurately detect an attack that is impacting application health, even at lower traffic thresholds.
> - **Protection Groups:** This feature allows you to group resources together for easier management. This reduces administrative overhead by allowing you to manage protection, metrics, and alerts for a logical group of resources rather than individually.
> - **Advanced Metrics:** Shield Advanced provides detailed, real-time metrics and reports that give you deep visibility into ongoing DDoS attacks. These metrics are available in the AWS Shield Advanced console and can also be sent to Amazon CloudWatch for monitoring and alerting.
> - **WAF Integration:** Shield Advanced integrates with AWS WAF to provide Layer 7 (application layer) protection. It includes a managed rule group for Layer 7 attacks, and the SRT can help you create custom WAF rules to mitigate sophisticated application-layer attacks.

- AWS Shield protects DDOS protection, standard = free, advanced = cost
- Protects against Network Volumetric Attacks (L3) - saturate capacity
	- Network Protocol Attacks (L4)  - TCP SYN Flood
		- which leaves connections open to prevent new ones
		- L4 can also have a volumetric component
	- Application Layer Attacks (L7) - web request floods
		- query.php?search=all_the_cat_images_ever
AWS Shield - Standard
- Free, protects perimeter (region/VPC or AWS edge)
- Common network or Transport layer attacks (L3, L4)
- Best protection using R53, CloudFront, AWS Global Accelerator
AWS Shield - Advanced
- 3K/month (per ORG), 1 year lock-in + outbound data/M
- Protects CF, R53, Global Accelerator, Anything associated with EIPs (like EC2), ALBs, CLBs, NLBs
- Not automatic, must explicitly enable
- Cost protection (like EC2 scaling) for unmitigated attacks
- Proactive engagement & access to AWS Shield response Team (SRT)
- WAF integration - includes basic AWS WAF fees for web ACLs, rules, and web requests
- Application Layer (L7) DDOS protection (uses WAF)
- Real time visibility of DDOS events and attacks
- Health-based detection - application specific health checks, used by proactive engagement team
- Protection groups