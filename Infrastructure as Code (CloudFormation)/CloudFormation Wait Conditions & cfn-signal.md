> [!note]- AI
> #### CreationPolicy
> - **Purpose:** A `CreationPolicy` is a resource attribute used to pause the creation of a resource until it receives a specified number of success signals. This is typically used for bootstrapping resources where you need to wait for a user data script to finish installing and configuring an application.
> - **Usage:** You apply a `CreationPolicy` to a resource, most commonly an `AWS::AutoScaling::AutoScalingGroup` or an `AWS::EC2::Instance`. The policy specifies a `Count` (the number of signals to wait for) and a `Timeout` duration.
> - **Signaling:** A helper script, `cfn-signal`, is run from within the EC2 instance's user data script. It sends a success or failure signal to CloudFormation.
> - **Process Flow:** CloudFormation will not mark the resource as `CREATE_COMPLETE` until it receives the required number of success signals or the timeout is exceeded, at which point the stack creation will fail and initiate a rollback.
> - **Recommendation:** AWS recommends using `CreationPolicy` for simple bootstrapping scenarios because it is a more straightforward and integrated way to signal completion directly on a resource.
> #### WaitConditions
> - **Purpose:** A `WaitCondition` is a dedicated resource that allows you to pause a stack's creation or update process until an external process sends a signal. It is more flexible and advanced than a `CreationPolicy`.
> - **Two Components:** A `WaitCondition` is composed of two resources:
>     1. `AWS::CloudFormation::WaitConditionHandle`: A logical resource that has no properties. When you reference it with `Fn::Ref`, it returns a pre-signed S3 URL that acts as the signal endpoint.
>     2. `AWS::CloudFormation::WaitCondition`: This is the resource that waits for the signals. It references the `WaitConditionHandle` and defines the `Count` of signals to expect and a `Timeout` for how long to wait.
> - **Usage:** An external process (e.g., a bootstrapping script on an EC2 instance, a Lambda function, or an on-premises script) sends an HTTP PUT request to the pre-signed URL from the `WaitConditionHandle`. The body of the request contains the signal data.
> - **Advanced Functionality:** A key feature of `WaitCondition` is that it allows for a small amount of data to be passed back to the CloudFormation stack in the signal. This data can be retrieved using the `Fn::GetAtt` intrinsic function, which is useful for passing back things like licensing information, status messages, or dynamic configuration values.
> #### Comparison and Exam Focus
> - **Granularity:** `CreationPolicy` is an attribute of a specific resource, making it tied to that resource's lifecycle. `WaitCondition` is a separate resource that can be used to coordinate actions across different parts of a template or even with external systems.
> - **Data Flow:** `WaitCondition` supports a two-way data exchange (signal with a data payload), while `CreationPolicy` only supports a simple success/failure signal.
> - **Simplicity:** For simple bootstrapping tasks on an Auto Scaling Group or a single EC2 instance, `CreationPolicy` is the recommended and simpler choice. For complex, multi-resource, or external-system coordination, `WaitCondition` is the more powerful tool.
> - **Exam Relevance:** Both `CreationPolicy` and `WaitCondition` are important for exams. The key is to understand their differences and which one to choose for a given use case. Look for keywords like "bootstrapping a single resource" (CreationPolicy) versus "coordinating multiple resources" or "passing back data" (WaitCondition).

CF Signal
- Configure CF to hold for a certain amount of success signals
- Wait for timeout H:M:S for those signals (12 hours max)
- If success signals received then CREATE_COMPLETE
- If failure signal received, creation fails
- If timeout is reached, creation fails
- CreationPolicy or WaitCondition
- Generally used for EC2 or autoscaling groups
WaitCondition
- Can depend on other resources, other resources can depend on the WaitCondition
- Relies on WaitHandle -> generates a presigned URL for resource signals