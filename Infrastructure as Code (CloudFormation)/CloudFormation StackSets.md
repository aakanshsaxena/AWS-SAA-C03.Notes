> [!note]- AI
> #### CloudFormation StackSets Overview
> - **Purpose:** A stack set is an extension of CloudFormation that allows you to create, update, or delete stacks across multiple AWS accounts and regions with a single operation. It is the primary tool for managing common infrastructure consistently across a multi-account organization.
> - **Architecture:** The architecture involves an **admin account** where the stack set is created and managed. This admin account then deploys **stack instances** to specified **target accounts** in specified regions.
> - **Stack Instances:** A stack instance is a container that represents a single CloudFormation stack deployed in a specific target account and region. Each stack instance is a unique deployment of the stack set's template and its resources.
> #### Permissions and Deployment Models
> - **Self-Managed Permissions:** In this model, you are responsible for creating the necessary IAM roles in the admin account and in each target account. You must ensure that the roles have the correct permissions for the stack set to deploy resources. This is a good option for a small number of accounts or for accounts that are not part of an AWS Organization.
> - **Service-Managed Permissions:** This is the recommended model for multi-account deployments, as it integrates with AWS Organizations. By enabling trusted access, CloudFormation automatically creates the required IAM roles in your target accounts on your behalf. This simplifies large-scale deployments and ensures permissions are always correct.
> #### Deployment Controls and Management
> - **Concurrent Accounts:** This setting defines the number of target accounts in which stacks can be deployed simultaneously. It helps control the speed of the deployment.
> - **Failure Tolerance:** This setting defines the maximum number of stack instance deployments that can fail before the entire stack set operation is stopped. This provides a crucial safety mechanism, preventing widespread deployment failures.
> - **Retain Stacks:** This option allows you to remove a stack instance from a stack set but prevent the corresponding CloudFormation stack from being deleted. The stack will continue to run independently and can be managed like a regular CloudFormation stack.
> #### Use Cases and Benefits
> - **Centralized Security and Governance:** Stack sets are ideal for deploying and managing common security resources across an entire organization. This includes deploying IAM roles, security groups, or a consistent set of AWS Config rules.
> - **Reduced Manual Effort:** They significantly reduce the manual effort of deploying foundational infrastructure. Instead of deploying the same stack to dozens of accounts and regions individually, you can do it with a single operation.
> - **Standardized Deployments:** They enforce consistency across your organization by ensuring that all accounts and regions have the same version of a resource, as defined by a single CloudFormation template.
> #### Definitions
> - **Stack Set:** A single CloudFormation template that can be used to create, update, or delete stacks across multiple AWS accounts and AWS regions with a single operation.
> - **Failure Tolerance:** A deployment control that defines the number of stack instance deployments that are allowed to fail in a stack set operation before the operation is stopped.
> - **Retain Stack:** A deployment option that, when enabled, prevents the deletion of a CloudFormation stack when its corresponding stack instance is removed from a stack set.
> - **AWS Config Rules:** A feature of AWS Config that defines desired configuration settings for your AWS resources and continuously evaluates whether your resources are compliant with those settings.
