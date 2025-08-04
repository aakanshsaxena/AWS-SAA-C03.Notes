> [!note]- AI
> #### Introduction to Nested Stacks
> - **Purpose:** Nested stacks allow you to manage a complex application or a collection of resources by using a main "root" stack that orchestrates the deployment of other smaller, more focused "nested stacks." This creates a modular architecture that makes templates easier to read, reuse, and maintain.
> - **Template Reuse:** A key benefit of nested stacks is that you can reuse a template for common components (e.g., a VPC, an Active Directory setup) across different projects or within the same root stack. This reuses the template code, but each nested stack creates a new, separate set of physical resources.
> #### Nested Stack Architecture
> - **Parameter Flow:** The root stack passes parameters to a nested stack during its creation or update. The nested stack's template must define these parameters to accept the input. You can use default values in the nested stack's template to reduce the number of parameters you need to pass from the root stack.
> - **Outputs Flow:** A nested stack's outputs are the only way for the root stack to get information about the resources created within the nested stack. The root stack can then use the `Fn::GetAtt` intrinsic function with a special syntax (`!GetAtt NestedStackLogicalID.Outputs.OutputName`) to retrieve these output values and use them as parameters for other nested stacks.
> - **Coordinated Lifecycle:** All nested stacks are created, updated, and deleted as a single unit when you perform those actions on the root stack. A failure in a nested stack will cause the entire root stack to roll back, ensuring that the entire deployment remains consistent.
> #### Key Benefits and Use Cases
> - **Overcoming Resource Limits:** Nested stacks are the primary way to overcome the default **500-resource limit** of a single CloudFormation stack. By breaking a large template into smaller, nested templates, you can manage a deployment with thousands of resources within a single root stack.
> - **Shared Lifecycle:** Use nested stacks when the resources in the sub-stacks are tightly coupled and share the same lifecycle. For example, a single root stack can deploy a VPC, Active Directory, and a database, all of which are part of a single application and should be created and deleted together.
> - **Modularization:** They enable you to simplify a complex template by breaking it into reusable, logical components. This simplifies development, testing, and debugging, as you can work on smaller, more manageable template files.
> - **Simplified Management:** They simplify the installation of a complex solution for end-users, who only have to interact with a single root stack.
> #### Nested Stacks vs. Cross-Stack References
> - **Shared Lifecycle:** Use **nested stacks** when the resources in the sub-stacks have a **shared lifecycle**. The create and delete actions are coordinated by the root stack.
> - **Independent Lifecycles:** Use **cross-stack references** (which will be covered in the next lesson) when you need to share resources between stacks that have **independent lifecycles**. For example, a network stack that creates a VPC might have its own lifecycle, and multiple application stacks with separate lifecycles might need to reference the VPC's ID.
> - **Summary:** The key architectural decision is whether the resources should be created and deleted as a single unit (nested stacks) or if they need to be managed separately (cross-stack references).

- Normally CF stack is isolated
- Resources in a single stack share a lifecycle
- 500 Stack resource limit
- Can't easily reuse resources (like a VPC)
	- Can't easily reference other stacks
Nested Stacks
- Start with one stack (root stack)
- Parent stack = anything with its own nested stack
- Root stack is just a normal stack (can have parameters and outputs)
- Give nested stack a URL to CF stack
- Can reference outputs of a nested stack by using STACKNAME.Outputs.XXXXX
- Root stack can use outputs from one nested stack and use them as parameters for another nested stack
- Whole templates can be reused in other stacks
	- Reusing the stack template not the actual resources
- Use when the stacks form part of one solution - lifecycle linked
Uses
- Overcome the 500 resource limit of one stack
- Modular templates to be able to reuse the code
- Make the installation process easier, nested stacks created by the root stack
- ONLY use when everything is lifecycle linked