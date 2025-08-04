> [!note]- AI
> #### AWS CloudFormation: Infrastructure as Code
> - **Purpose:** AWS CloudFormation is a service that helps you model and set up your Amazon Web Services resources so that you can spend less time managing those resources and more time focusing on your applications. It provides a common language to describe your entire infrastructure in text files (templates).
> - **Infrastructure as Code (IaC):** It allows you to provision your AWS infrastructure in an automated, secure, and repeatable manner, treating your infrastructure definition like application code.
> - **Templates:** These are declarative text files (written in YAML or JSON) that serve as blueprints for your infrastructure. They define all the AWS resources you want to create and how they should be configured.
> #### Logical and Physical Resources
> - **Logical Resources:** These are the declarations of AWS resources within your CloudFormation template. Each logical resource has a unique **Logical ID** (a name you choose) and a `Type` attribute that follows a namespace format (e.g., `AWS::EC2::Instance`, `AWS::S3::Bucket`). Logical resources also have `Properties` that configure the specific characteristics of the physical resource that will be created.
> - **Physical Resources:** These are the actual AWS resources (e.g., a running EC2 instance, an S3 bucket with a specific name) that CloudFormation provisions in your AWS account based on the logical resource definitions in your template. Each physical resource gets a unique **Physical ID** (like an EC2 instance ID or an S3 bucket name) assigned by AWS after creation.
> - **Synchronization:** CloudFormation is responsible for keeping the desired state defined by your logical resources in sync with the actual state of your physical resources.
> #### CloudFormation Stacks
> - **Stacks as Units:** A CloudFormation **stack** is a collection of AWS resources that you can manage as a single unit. When you deploy a CloudFormation template, you create a stack.
> - **Dependencies:** CloudFormation automatically understands and manages the dependencies between resources defined in your template, ensuring they are created, updated, or deleted in the correct order.
> #### Stack Lifecycle: Create, Update, Delete
> - **Stack Creation:** When you create a stack from a template, CloudFormation provisions all the physical resources defined by your logical resources. It tracks the status of each resource as it moves through its creation process.
> - **Stack Updates:** When you modify a template and update an existing stack, CloudFormation compares the new template with the current stack state. It then intelligently determines the necessary changes to the physical resources (additions, modifications, or deletions).
>     - **Change Sets:** Before applying an update, you can generate a **Change Set** to preview the exact changes CloudFormation will make to your stack, including which resources might be replaced or interrupted, allowing for review and approval.
> - **Stack Deletion:** When you delete a stack, CloudFormation systematically deletes all the physical resources that were created as part of that stack. This ensures a clean teardown of your infrastructure.
> #### Benefits and Usage
> - **Automation at Scale:** CloudFormation automates the deployment of complex infrastructure, reducing manual effort and human error. A single template can deploy anything from a single WordPress blog to an entire multi-tier application.
> - **Consistency and Repeatability:** Templates ensure that your infrastructure is deployed consistently and reliably every time, across different environments (development, test, production) or AWS regions.
> - **Change Management:** By storing templates in source code repositories, you can version control your infrastructure, track changes, and implement approval workflows before any modifications are deployed.
> - **Quick Deployment:** It enables rapid, one-off deployments for testing or specific projects, and then easy deletion when no longer needed.
> - **Extensive Use:** CloudFormation is a fundamental tool for AWS architects and engineers and is used extensively in AWS training courses to provide practical, hands-on experience with infrastructure deployment.

- Begins with a template - YAML or JSON
	- contains logical resources - the "WHAT"
- Templates used to create stacks
- Stacks create physical resources from the logical
- If a stacks template is changed, physical resources are changed
- If a stack is deleted, normally, the physical resources are deleted
Architecture
- Resource properties are used by CF when creating the matching physical resources
- CreateStack uses template, params, options to create a stakc
- Stack creates updates, deletes, physical resources based on logicla resources in template
- Once logical resource moves to create_complete = physical resource is active = can be queried for attributes of the physical resource within the template
