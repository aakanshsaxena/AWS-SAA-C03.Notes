> [!note]- AI
> #### CloudFormation Helper Script: cfn-hup
> - **Purpose:** The `cfn-hup` helper script is a daemon that runs on an EC2 instance. Its sole purpose is to monitor the instance's metadata for changes, and when a change is detected, it executes a custom action.
> - **Solving the `cfn-init` Limitation:** The `cfn-init` helper script is executed only once, during the initial bootstrapping of an instance. If you update the `CloudFormation::Init` metadata in your template and perform a stack update, `cfn-init` will not run again automatically. The `cfn-hup` daemon solves this by continuously checking for metadata changes and triggering `cfn-init` to reapply the configuration.
> #### Architecture and Configuration
> - **Installation and Monitoring:** The `cfn-hup` daemon must be installed and started during the initial bootstrapping of the EC2 instance, typically via the `UserData` script. It runs in the background and periodically polls the instance's metadata.
> - **Configuration Files:** `cfn-hup` is configured using two files on the EC2 instance:
>     1. `/etc/cfn/cfn-hup.conf`: This file specifies the `stack` ID and `region` to monitor, along with the `interval` (in minutes) for polling.
>     2. `/etc/cfn/hooks.d/cfn-auto-reloader.conf`: This file defines the "hook." It specifies the `path` to the specific metadata to monitor (e.g., the `AWS::CloudFormation::Init` section of a resource) and the `action` to execute when a change is detected (e.g., running `cfn-init` with the updated configuration).
> - **Process Flow:**
>     1. You launch a stack, and the `UserData` script on the EC2 instance starts `cfn-hup`.
>     2. You update the stack, making a change to the `CloudFormation::Init` metadata of the EC2 resource.
>     3. `cfn-hup` detects the metadata change.
>     4. It executes the action defined in its hook, which is to re-run `cfn-init` to apply the new configuration.
> #### Benefits and Usage
> - **In-Place Updates:** The primary benefit of `cfn-hup` is that it allows you to perform "in-place updates" on an EC2 instance's configuration without needing to replace the instance itself. This is a powerful feature for continuous configuration management.
> - **Continuous Monitoring:** By using `cfn-hup`, you ensure that the configuration of your EC2 instance remains in sync with the desired state defined in your CloudFormation template, even as the template evolves over time.
> - **Exam Relevance:** Understanding the relationship between `cfn-init` (for initial bootstrapping) and `cfn-hup` (for in-place updates) is a key concept for both real-world architecture and exam scenarios. It is the go-to solution for managing dynamic application configurations with CloudFormation.

- cfn-init is run once as part of bootstrapping (user data)
- if CloudFormation::Init is updated, it isn't rerun
- cfn-hup helper is a daemon which can be installed
	- it detects changes in resource metadata running configurable actions when a change is detected
- UpdateStack => updated config on EC2 instances
Architecture 
- CFN template is changed, so UpdateStack
- cfn-hup checks metadata periodically
- When updated, calls cfn-init
- cfn-init applies new configuration