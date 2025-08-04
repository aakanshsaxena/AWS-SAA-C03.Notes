> [!note]- AI
> #### AWS Secrets Manager
> - **Purpose:** A dedicated, fully managed service for securely storing and managing secrets such as database credentials, API keys, and other sensitive data. It is specifically designed for confidential information.
> - **Key Features:**
>     - **Automatic Rotation:** The primary differentiator is its built-in capability for automatic secret rotation. It uses a **Lambda function** to periodically change the secret in the database (e.g., Amazon RDS) and then updates the corresponding secret in Secrets Manager.
>     - **Application Integration:** Integrates tightly with services like Amazon RDS, Amazon Redshift, and Amazon DocumentDB for seamless password rotation and updates.
>     - **Security:** All secrets are **always encrypted at rest** using AWS Key Management Service (KMS). Access is controlled through IAM policies and resource-based policies.
> - **Access Model:** Applications typically retrieve secrets at runtime using the AWS SDK, which fetches the most recent version of the secret. This avoids hardcoding credentials in the application's source code.
> - **Cost Model:** A paid service with a per-secret and per-API call pricing model.
> #### AWS Systems Manager Parameter Store
> - **Purpose:** A service for storing configuration data and secrets as key-value pairs in a hierarchical structure. It is a more general-purpose tool.
> - **Key Features:**
>     - **Hierarchical Structure:** Parameters can be organized in a folder-like hierarchy (e.g., `/app/prod/db-credentials`).
>     - **Secure Strings:** It can store sensitive data as **"SecureString"** parameters, which are encrypted using KMS. However, it can also store plain text parameters.
>     - **No Automatic Rotation:** Unlike Secrets Manager, Parameter Store does not have a built-in feature for automatic secret rotation. You would need to build a custom solution using other AWS services to achieve this.
> - **Access Model:** Applications can retrieve parameters via the AWS SDK, CLI, or API. It's often used for non-secret configuration data like hostnames, port numbers, or feature flags.
> - **Cost Model:** Standard parameters are available at **no additional charge**. Advanced parameters and API calls above a certain free tier have a cost.
> #### Key Differentiators and Exam Focus
> - The main difference is the **automatic rotation feature**. Secrets Manager is the correct choice whenever a question mentions the need to automatically rotate credentials.
> - **Use Case:** Choose **Secrets Manager** for highly sensitive secrets that require rotation and lifecycle management. Choose **Parameter Store** for application configuration data and secrets that do not require automatic rotation.
> - **Cost:** Parameter Store's standard tier is a more cost-effective solution for non-secret or non-rotating data.
> - **Exam Questions:** Exam questions will often include keywords like "automatic rotation," "database credentials," or "API keys" to point you toward Secrets Manager. If the question is about a simple, hierarchical key-value store for configuration, Parameter Store is the likely answer.

- It does share functionality with Parameter Store
- But it is designed for secrets like passwords, API keys
- Usable via Console, CLI, API or SDK's (integration)
- Supports automatic rotation using Lambda
- Directly integrates with some AWS products like RDS 
Architecture
- We access Catagram, and it uses the Secrets Manager SDK to retrieve database credentials, SDK uses IAM credentials authorization, application uses secrets obtained from Secrets Manager to securely access the database, Lambda is invoked periodically to rotate secrets to keep products like RDS in sync
- Lambda permissions via IAM Roles, and secrets are encrypted using KMS