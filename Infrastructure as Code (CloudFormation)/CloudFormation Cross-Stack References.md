> [!note]- AI
> #### Introduction to Cross-Stack References
> - **Purpose:** Cross-stack references allow different CloudFormation stacks to share information and resources. This is a crucial feature for creating modular, service-oriented architectures where different teams or applications have their own stacks but need to share common infrastructure resources.
> - **Independent Lifecycles:** The key use case for cross-stack references is when resources have different lifecycles. For example, a networking stack that creates a VPC and its associated resources may have a long, stable lifecycle, while a separate application stack that uses that VPC may have a much shorter, more dynamic lifecycle.
> #### The Export and Import Process
> - **Exporting a Value:** To share a resource, the stack that creates it must declare an output in its `Outputs` section and add an **`Export`** field with a unique name.
>     - The export name must be unique within a given AWS account and region.
>     - Example: A VPC stack can output the VPC ID and export it with a name like `MySharedVPC-VpcId`.
> - **Importing a Value:** Another stack that needs to use the shared resource can import the value using the **`Fn::ImportValue`** intrinsic function.
>     - The function takes the unique export name as its argument (e.g., `!ImportValue "MySharedVPC-VpcId"`) and retrieves the corresponding value.
>     - This effectively replaces the need for a parameter that a user would have to manually input.
> - **Limitations:**
>     - Cross-stack references only work within the **same AWS Region**.
>     - A stack that is exporting a value **cannot be deleted or have its exported value modified** as long as another stack is importing it. All importing stacks must be deleted or updated to stop the import before the exporting stack can be changed.
> #### Use Cases and Architecture
> - **Shared Services Architecture:** Cross-stack references are the ideal solution for creating shared services. A central team can manage a single stack for core networking components (VPC, subnets, security groups), and then other teams can simply import the necessary values into their own application stacks.
> - **Resource Reuse:** Unlike nested stacks, which reuse templates, cross-stack references allow you to reuse the **actual physical resources** that have already been created by another stack. This is fundamental for building a decoupled, service-oriented architecture.
> - **Short-Lived Applications:** A short-lived application that is created and deleted frequently can be deployed in its own stack. By importing the shared network resources, the application stack can be managed independently without affecting the core infrastructure.
> #### Cross-Stack vs. Nested Stacks
> - **Cross-Stack References:**
>     - **Lifecycle:** Stacks have **independent lifecycles**. The exporting stack can be managed separately from the importing stack.
>     - **Reuse:** Reuses **actual resources**.
>     - **Complexity:** Best for decoupling infrastructure components managed by different teams.
> - **Nested Stacks:**
>     - **Lifecycle:** Stacks have a **shared lifecycle**. The nested stack is created and deleted by its root stack.
>     - **Reuse:** Reuses **templates** to create new resources each time.
>     - **Complexity:** Best for modularizing a single, complex application that shares a single lifecycle.
> - **Summary:** The choice between these two methods depends on whether the resources you are sharing have a shared lifecycle or need to be managed independently.


- By default things in one stack can't be used by others (because CF)
- Outputs are normally not visible from other stacks
- Nested stacks can reference them (but this would mean they are linked in life cycle)
- Outputs can be exported making them visible from other stacks
- Exports must have a unique name in the region
- Fn::ImportValue can be used instead of Ref
Architecture
- We use Export: with a Name: to export the output of a stack to a unqiue name in that region of that account to the Exports List
- After this we can use ImportValue instead of Ref to reference region exported values (!ImportValue NAME)
When to use
- Service-orientated, different lifecycles, stack reuse
- Used when you want to re-use the resources from a stack versus the template from the stack