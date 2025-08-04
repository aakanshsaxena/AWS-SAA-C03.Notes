> [!note]- AI
> #### CloudFormation Stack Roles and Role Separation
> - **Purpose:** A CloudFormation stack role is an IAM role that a CloudFormation stack assumes to create, update, or delete resources in your AWS account. This role-based approach is a fundamental security best practice that enables **role separation** and the principle of least privilege.
> - **Role Separation in Practice:** A common scenario involves two types of identities:
>     - **Administrator (Gabby):** An identity with broad permissions who is trusted to create secure, pre-approved IAM roles that define what resources can be created.
>     - **Limited User (Phil):** An identity with very limited permissions (e.g., a help desk engineer) who is only allowed to deploy CloudFormation stacks and pass the pre-approved IAM role to the stack.
> - **How it Works:** The administrator creates an IAM role (the stack role) with permissions to create specific resources (e.g., EC2 instances, S3 buckets). The limited user, who does not have direct permissions to create these resources, starts a CloudFormation stack and specifies the ARN of the stack role. CloudFormation then assumes this role and uses its permissions to perform all resource actions, not the limited user's.
> #### Benefits and Permission Management
> - **Enforcing Least Privilege:** The user (Phil) does not need direct permissions to create or manage resources. Their permissions are limited to managing the stack itself and passing the stack role. This is a highly secure model as it minimizes the risk associated with broad user permissions.
> - **Centralized Control:** The administrator (Gabby) retains central control over what can be deployed by controlling the permissions of the IAM role. By creating different roles for different types of deployments, the administrator can enforce what resources and configurations are allowed.
> - **Avoiding Direct Permissions:** This model avoids the security risk of giving a user direct permissions to a wide range of AWS services. The permissions are consolidated into a role that is only assumed by CloudFormation to perform a specific, templated task.
> #### Definitions
> - **Administrator:** An individual or identity with the necessary permissions to manage an AWS account and its resources. In the context of CloudFormation stack roles, an administrator is typically responsible for creating and maintaining the secure IAM roles that define deployment permissions.
> - **CloudFormation:** An AWS service for provisioning infrastructure as code. It allows you to define your AWS resources in a template and deploy them as a single unit (a stack).
> - **CloudFormation Stack Role (Stack Role):** An IAM role that a CloudFormation stack assumes to perform actions on your behalf. This role is passed to the stack by the user and is the identity that CloudFormation uses to create, update, and delete resources.

- When you create a stack, CFN creates physical resources
- CFN uses the permissions of the logged in identity
- Which means you need permissions for AWS
- Allows CFN to assume a role to gain the permissions to access AWS services
- This lets you implement role seperation
- The identity creating the stack doesn't need resource permissions, only PassRole
Architecture
- Issue because normally, CFN requires the account user to have access to create whatever resources the AWS stack is creating, but we don't always want accounts in our organization for example to have this access
- We let an account admin create the IMA Role that can be passed into CFN, IAM Role w permissions to create, update, and delete AWS resources
- Role is attached to the stack and used for any operations
- Phil only need permissions to create, update, delete stacks, and to pass in the role, not permissions to manipulate the resources