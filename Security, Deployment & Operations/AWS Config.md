> [!note]- AI
> #### AWS Config: Core Functions and Architecture
> - **Primary Functions:** AWS Config has two main jobs:
>     1. **Change Tracking:** It records the configuration state of your AWS resources, including their relationships to other resources, at any given point in time. It tracks who made the change, the before-and-after states, and logs this information.
>     2. **Compliance Auditing:** It evaluates whether your resources are compliant with a set of standards that you define, which can be either a set of best practices or a regulatory standard.
> - **The Config Recorder:** This is the service component you enable to start monitoring. The recorder continuously tracks all supported resources in a given region and creates a new **configuration item** whenever a resource's configuration or relationship to another resource changes.
> - **Storage and History:** The full history of configuration items is stored in an Amazon S3 bucket that you designate. This history can be used for security analysis, change management, and operational troubleshooting.
> #### AWS Config Rules and Remediation
> - **Config Rules:** These are the heart of the compliance function. A rule evaluates the configuration items captured by the recorder and checks them against a specific standard.
>     - **Types of Rules:** You can use **AWS Managed Rules** (pre-built for common use cases like checking for unencrypted S3 buckets) or create **Custom Rules** using a Lambda function for more specific or unique compliance checks.
>     - **Compliance Status:** Rules mark a resource as either **Compliant** or **Non-Compliant**. AWS Config does not prevent a non-compliant change from happening. Its role is to identify and report the non-compliance.
> - **Automatic Remediation:** For certain non-compliant issues, you can configure automatic remediation. This workflow is typically handled by integrating with other AWS services:
>     1. When a resource becomes non-compliant, AWS Config sends an event to **Amazon EventBridge**.
>     2. An EventBridge rule triggers a target, such as a **Lambda function** or an **AWS Systems Manager Automation document**.
>     3. This Lambda function or SSM document then takes action to fix the non-compliant resource (e.g., enabling encryption on an S3 bucket or changing a security group rule).
> #### Cross-Region and Cross-Account Aggregation
> - **Regional Service:** By default, AWS Config operates within a single region. To get a holistic view of your entire organization, you must use data aggregation.
> - **Aggregators:** An aggregator is a feature that allows you to collect AWS Config data from multiple AWS accounts and multiple regions into a single central account. This is particularly useful for central IT administrators who need to monitor and enforce compliance for a large enterprise.
> - **Centralized Governance:** By using an aggregator, you can easily get an organization-wide view of compliance status and run queries across all your accounts from a single location, simplifying governance and auditing.
> #### Key Differentiators and Exam Focus
> - AWS Config is a powerful tool for **auditing, compliance, and change tracking**.
> - It is **not** a preventative tool or a permissions control service. It does not enforce a standard; it only reports on non-compliance.
> - Exam questions often focus on the distinction between Config's role (audit/report) and other services' roles (enforcement/prevention, like IAM). Another key area is how it integrates with other services to provide a fully automated, end-to-end compliance solution, especially for automatic remediation.

- Record configuration change over time on resources
- Auditing of changes, compliance with standards
- Doesn't do anything to prevent changes happening
- Regional service, supports cross-region and account aggregation
- Changes can generate SNS notifications and near-real-time events via EventBridge & Lambda
Architecture
- Resources are evaluated against Config Rules - either AWS Managed or custom (using Lambda)
- We can either store the Configuration Item (CI) that is created every time a change occurs to a resource in a bucket
- Or we can have it send to SNS for compliance notifications
- Send to EventBridge if Config Rule changes and we can remediate them automatically using Lambda
