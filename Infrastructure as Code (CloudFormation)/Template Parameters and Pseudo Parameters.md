> [!note]- AI
> #### Introduction to Parameters
> - **Purpose:** CloudFormation parameters provide a mechanism to pass external values into a template, making it reusable and adaptable. Instead of hardcoding values like instance sizes or security group IDs, you can define parameters that allow users or processes to provide input during stack creation or updates.
> - **Two Types:** CloudFormation uses two types of parameters: **Template Parameters**, which are user-defined, and **Pseudo Parameters**, which are automatically provided by AWS.
> #### Template Parameters
> - **User-Defined Input:** These parameters are explicitly defined in the `Parameters` section of your template. They expose a customizable interface for a template, allowing users to specify values for resources via the console, CLI, or API.
> - **Key Properties:**
>     - **Type:** Defines the data type of the input, such as `String`, `Number`, `List<String>`, or an AWS-specific type like `AWS::EC2::Instance::Id`, which can be automatically populated with valid values in the console.
>     - **Default:** An optional value that is used if the user does not provide an explicit input. Using defaults is a best practice to reduce the amount of required input.
>     - **AllowedValues:** A list of valid values that the user can choose from, which helps with input validation and reduces errors.
>     - **NoEcho:** A boolean property that, when set to `true`, hides the value of a parameter (e.g., a password) from being displayed in the CloudFormation console and logs.
> #### Pseudo Parameters
> - **AWS-Provided Values:** These are built-in, immutable parameters that are automatically provided by AWS CloudFormation. You do not define them in your template; you only reference them. Their values are derived from the environment in which the stack is being deployed.
> - **Key Pseudo Parameters:**
>     - `AWS::AccountId`: The 12-digit AWS account ID where the stack is being created.
>     - `AWS::Region`: The AWS region where the stack is being deployed (e.g., `us-east-1`).
>     - `AWS::StackId`: The unique Amazon Resource Name (ARN) for the stack.
>     - `AWS::StackName`: The name of the CloudFormation stack.
>     - `AWS::NotificationARNs`: The list of SNS topics that receive stack event notifications.
>     - `AWS::Partition`: The partition in which the resource is located (e.g., `aws`, `aws-cn`).
> - **Usage:** Pseudo parameters are essential for creating portable templates that can be used across different accounts and regions without modification.
> #### Best Practices and Comparison
> - **Flexibility and Portability:** Both template and pseudo parameters are crucial for creating flexible and portable templates. They eliminate the need for static, hard-coded values, which makes templates much more reusable.
> - **Best Practices:**
>     - **Minimize Explicit Input:** Aim to design templates with as few required parameters as possible. Use `Default` values where appropriate.
>     - **Leverage AWS Values:** Wherever possible, use a pseudo parameter (e.g., `AWS::Region` or `AWS::AccountId`) instead of a template parameter to get an AWS-provided value. This reduces user input and makes your template more robust.
> - **Differentiators:** The key difference is the source of the value. **Template parameters** get their values from the user or process creating the stack, while **pseudo parameters** get their values automatically from the AWS environment.

- Allow input 
- Template parameters accept input when a stack is created or updated via console/CLI/API
- Can be referenced from within logical resource and influence physical resources and/or config
- Can be configured with defaults, allowedvalues, min and max length, allowed patterns, no echo and type
Architecture
- Defined within CF template
- We can have a default value if the user doesn't choose a parameter value
Pseudo Parameters
- Template parameters are populated by AWS based on the environment when creating the stack
- Like AWS::Region, AWS::StackName, AWS::AccountID