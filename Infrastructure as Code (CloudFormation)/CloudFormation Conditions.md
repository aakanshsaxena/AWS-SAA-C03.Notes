> [!note]- AI
> #### Introduction to Conditions
> - **Purpose:** CloudFormation conditions allow you to control whether resources are created or if resource properties are configured based on a logical evaluation. They are an essential tool for creating flexible and reusable templates that can adapt to different environments.
> - **Evaluation:** Conditions are evaluated at the beginning of the stack processing and resolve to a simple boolean value: `true` or `false`.
> #### Defining and Applying Conditions
> - **Defining the Condition:** Conditions are defined in a dedicated `Conditions` block within your template. This is where you write the logical statement using a set of intrinsic functions. The most common function is `Fn::Equals`, which checks if two values are the same.
> - **Applying to Resources:** To make a resource creation conditional, you add a `Condition` attribute to its definition in the `Resources` section. The value of this attribute is the logical ID of the condition you defined.
>     - If the condition evaluates to `true`, the resource is created as normal.
>     - If the condition evaluates to `false`, the resource is simply **skipped and not created**. It will not appear in the final stack.
> - **Implicitly Created Resources:** Any resource that does not have a `Condition` attribute is always created when the stack is deployed.
> #### Condition Logic and Functions
> - **Intrinsic Functions:** Conditions primarily use a special set of intrinsic functions for logical evaluations:
>     - `Fn::Equals`: Checks if two values are equal.
>     - `Fn::Not`: Inverts the result of another condition (e.g., `Fn::Not [!Condition "IsProdEnv"]`).
>     - `Fn::And`: Returns `true` if all conditions in a list are `true`.
>     - `Fn::Or`: Returns `true` if at least one condition in a list is `true`.
> - **Complex Logic:** By nesting these functions, you can build complex conditional logic. For example, you can create a condition that is `true` only if the environment is "production" AND the region is "us-east-1".
> #### Conditional Properties with Fn::If
> - **Conditional Resource Properties:** In addition to conditionally creating entire resources, you can also conditionally set a property of a resource. This is done using the `Fn::If` intrinsic function, which is used inside a resource's property definition, not in the `Conditions` block.
> - **Fn::If Syntax:** `!If [Condition, Value_if_True, Value_if_False]`.
> - **Use Case:** A common use case is to specify a smaller EC2 instance size (e.g., `t3.micro`) if a condition is `false` (i.e., a development environment) and a larger instance size (e.g., `m5.large`) if the condition is `true` (i.e., a production environment).
> #### Use Cases and Best Practices
> - **Environment Control:** The most common use case is to create environment-specific stacks. For example, a single template can deploy a small, cost-effective set of resources for a `dev` environment and a larger, more highly available set for a `prod` environment.
> - **Conditional Security:** Conditions can be used to apply a strict security policy (e.g., an S3 bucket policy) only when the stack is for a production environment.
> - **Best Practices:** While powerful, avoid creating overly complex or deeply nested conditions. This can make templates difficult to read and debug. It is often better to use simpler conditions and combine them in a logical and easy-to-understand way.
> - **Upcoming Demos:** The concepts discussed will be demonstrated in upcoming practical videos, so it is a good idea to review the template code to see these conditions in action.

- Allows a stack to react to certain conditions to change infrastructure or configuration of infrastructure
- Created in the optional conditions section of a template
	- Set to either T or F and processed before resources are created
- Uses the other intrinsic function AND, EQUALS, IF, NOT, OR
	- associated with logical resources to control if they are created or not
Architecture
- Example:
	- We decide on an environment type via a template parameter (pick either dev or prod)
	- We have a condition block that CF looks at first and evaluates based on the state of the condition (isProd)
	- When processing resources if a condition key/value is present, the resource is only created if the condition is true (There would need to be a Condition: IsProd listed under the resource we want to create if we only want it to be created if isProd is true)