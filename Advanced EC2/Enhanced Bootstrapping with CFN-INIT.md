
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>This transcript discusses **CloudFormation** and its powerful feature **cfn-init**, a configuration management system for EC2 instances. 
>
>**Here are the key takeaways:**
>
>* **cfn-init vs. User Data:**
>    * User data is procedural, running commands line by line.
>    * cfn-init is a desired state configuration system, ensuring the instance reaches a specific state.
>    * cfn-init can install packages, manage users and groups, download and extract sources, create files, run commands, and control services.
>* **How cfn-init Works:**
>    * cfn-init is triggered by user data passed to the EC2 instance during creation.
>    * It retrieves configuration from the CloudFormation stack metadata.
>    * It implements the desired state defined in the CloudFormation template.
>* **CloudFormation Creation Policies and Signals:**
>    * Creation policies allow CloudFormation to wait for a signal from the resource (e.g., cfn-init) to confirm successful configuration.
>    * cfn-signal command reports the success or failure of the bootstrapping process to CloudFormation.
>    * This ensures that the stack creation is only marked as complete when the resource is fully configured.
>    * Creation policies are crucial for complex bootstrapping processes involving multiple steps and configurations.
>
>**Additional Points:**
>
>* cfn-init can handle stack updates, automatically updating the instance configuration when changes are made to the CloudFormation template.
>* While not essential for the Solutions Architect Associate exam, understanding cfn-init and CloudFormation creation policies will be beneficial for automation-related questions.
>
>
>This transcript provides a comprehensive overview of cfn-init and its role in automating EC2 instance configuration using CloudFormation.
>

AWS::CloudFormation::Init
- cfn-init helper script - installed on EC2 OS
- Simple configuration management system
- Procedural (user data) vs desired state (cfn-init)
- Packages, groups, users, sources, files, commands, and services
- Provided with directives via metadata and AWS::CloudFormation::Init on a CFN Resource
cfn-init
- Stored in CloudFormation template and accessed by the stack through the userdata inside the template
- Uses this to create EC2 instance and instance executes cfn-init
CreationPolicy and Signals
- Normally, our stack is considered complete once all the resources needed are created (don't have to be functional)
- However, we can create a CreationPolicy in our CF template that will create the stack and then ask for a signal from our resource (ex. EC2 instance) to make sure its operational before saying our resource creation is complete.
	- cfn-signal sends a signal to CF to report status of our instance 
