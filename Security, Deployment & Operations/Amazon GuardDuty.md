> [!note]- AI
> #### AWS GuardDuty: Overview and Functionality
> - **Continuous Threat Detection:** AWS GuardDuty is a continuous security monitoring service that protects your AWS accounts and workloads. It is always running and immediately begins analyzing activity once enabled, without any performance impact on your resources.
> - **Intelligent Analysis:** GuardDuty uses a combination of machine learning, anomaly detection, and integrated threat intelligence feeds (from AWS and third-party sources like CrowdStrike) to identify unexpected or unauthorized behavior in your AWS environment. It automatically learns the normal behavior of your accounts.
> - **Key Data Sources:** GuardDuty analyzes metadata from multiple independent data sources, including:
>     - **VPC Flow Logs:** For network traffic analysis to detect suspicious connections to your EC2 instances.
>     - **AWS CloudTrail Logs:** For API activity monitoring to spot unusual API calls, unauthorized deployments, or privilege escalation attempts.
>     - **DNS Logs (via Route 53):** To identify compromised instances attempting to communicate with malicious domains.
>     - It also analyzes CloudTrail S3 data events, Kubernetes audit logs, and RDS login activity.
> #### Findings and Automated Response
> - **Findings:** When a threat is detected, GuardDuty generates a **finding**, which is a detailed report on the suspicious activity. Findings are categorized by severity (High, Medium, Low) and provide information on the potential threat type, the affected resource, and remediation suggestions.
> - **Automated Remediation:** GuardDuty findings can be used to trigger automated security responses. This is typically done by sending the finding as an event to **Amazon EventBridge**.
>     - **EventBridge:** You can create rules in EventBridge to match specific GuardDuty findings (e.g., a "high severity" finding for a compromised EC2 instance).
>     - **Targets:** These rules can then trigger a target to take action. Common targets include:
>         - **Amazon SNS:** To send a notification (e.g., an email or SMS) to the security team.
>         - **AWS Lambda:** To run a serverless function that automates remediation, such as isolating the compromised EC2 instance by modifying its security group or moving a malicious S3 object to a quarantine bucket.
> #### Multi-Account Architecture and Account Security
> - **Master and Member Accounts:** GuardDuty supports a multi-account architecture, which is the best practice for organizations with multiple AWS accounts. A single **master account** (often a dedicated security account) can be designated to centrally manage and view findings from multiple **member accounts**.
> - **Centralized Management:** This model, which integrates seamlessly with AWS Organizations, simplifies the management of GuardDuty and provides a consolidated view of security findings across the entire organization, eliminating the need to monitor each account individually.
> - **User Influence:** You can influence GuardDuty's behavior and reduce false positives by creating **Trusted IP Lists** (for IP addresses you know are safe) and **Suppression Rules** (to automatically archive findings that are determined to be harmless).
> - **Detective Control:** It's important to remember that GuardDuty is a **detective control**. It identifies and alerts on threats, but it does not prevent them. It's designed to be the first line of defense that helps you identify security issues so you can take action.

- Continuous security monitoring service
- Analyzes supported data sources plus AI/ML, plus threat intelligence feeds
- Identifies unexpected and unauthorized activity on its own (can influence this, but as a whole learns patterns as a whole)
- Notify or event-driven protection/remediation
- Supports multiple accounts (MASTER and MEMBER)
Architecture
- Receives logs from supported data sources (DNS Logs, VPC Flow Logs, CloudTrail Event Logs, CloudTrail Management Events, CloudTrail S3 Data Events) + Threat Intelligence Feeds
- Sends findings to EventBridge which will send notifications to SNS or invoke Lambda functions