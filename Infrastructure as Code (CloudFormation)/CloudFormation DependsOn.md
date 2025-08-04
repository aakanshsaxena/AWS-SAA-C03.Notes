> [!note]- AI
> #### CloudFormation Dependency Management Overview
> - **Purpose:** CloudFormation must manage the order in which it creates, updates, and deletes resources. This is because many resources have dependencies on others (e.g., you must create a VPC before you can create a subnet within it).
> - **Parallelism:** By default, CloudFormation attempts to provision resources in parallel to reduce deployment time. It relies on a dependency management system to ensure that dependent resources are not provisioned until their dependencies are ready.
> - **Two Types of Dependencies:** CloudFormation uses two methods to determine this order: **Implicit Dependencies** and **Explicit Dependencies**.
> #### Implicit Dependencies
> - **Automatic Inference:** CloudFormation automatically infers a dependency when a resource's property uses an intrinsic function (`!Ref`, `!GetAtt`, `!Sub`, etc.) to reference another resource in the same template.
> - **Creation Order:** When a resource (Resource A) references another resource (Resource B), CloudFormation understands that Resource B must be created and fully provisioned before it can begin creating Resource A.
> - **Example:** In a template, an EC2 instance's `SubnetId` property references a subnet's logical ID. CloudFormation automatically creates the VPC, then the subnet, and only then creates the EC2 instance, since it needs the subnet's physical ID.
> #### Explicit Dependencies with `DependsOn`
> - **When to Use:** There are cases where an implicit dependency is not sufficient. This often happens when a resource needs to be ready before another can begin, but there is no direct reference between them in the template. In these scenarios, you must use the `DependsOn` attribute.
> - **The `DependsOn` Attribute:** This attribute allows you to explicitly specify that a resource depends on another. You add the `DependsOn` attribute to the dependent resource, and its value is the logical ID of the resource it depends on.
> - **Example: Elastic IP and Internet Gateway:** A classic example is creating an Elastic IP (EIP) that will be used in a VPC. An EIP can fail to create or delete correctly if the Internet Gateway has not been attached to the VPC. Since the EIP and Internet Gateway Attachment resources may not have a direct reference to each other, you would use `DependsOn` on the EIP resource to force CloudFormation to wait for the Internet Gateway Attachment to be complete.
> - **Impact on Deletion:** The `DependsOn` attribute also dictates the deletion order. The resource with the `DependsOn` attribute will be deleted _before_ the resource it depends on, which is critical for preventing deletion errors.
> - **Syntax:** `DependsOn` can take a single string (for one dependency) or a list of strings (for multiple dependencies).
> #### Best Practices and Exam Focus
> - **Trust Implicit First:** As a best practice, rely on CloudFormation's implicit dependency mapping whenever possible. Only use the `DependsOn` attribute when you encounter a deployment error due to an unexpressed dependency.
> - **Debugging:** `DependsOn` is a powerful debugging tool for deployment errors. If a stack fails during creation, an analysis of the event logs may reveal a dependency issue that can be resolved with `DependsOn`.
> - **Exam Relevance:** For the exam, be aware of the "edge cases" where `DependsOn` is required. The EIP/Internet Gateway scenario is a common example. You should also understand that `DependsOn` is the correct solution when a question describes a dependency that is not logically expressed in the template's resource references.

- CF tries to be efficient
	- does things in parallel (create, update, delete)
	- tries to determine a dependency order (VPC->SUBNET-> EC2)
	- Uses references or functions to create this (EC2 needs a VPC, create a VPC first)
- DependsOn lets you explicitly define this
	- If resources B and C depend on A, both wait for A to complete before starting
- Can have a single dependency in DependsOn or a list of dependencies