> [!note]- AI
> #### What is a Custom Resource?
> - **Purpose:** A CloudFormation custom resource is a mechanism that allows you to write custom provisioning logic that is executed by CloudFormation. It extends CloudFormation's native capabilities to manage resources that are not natively supported or to perform custom actions during a stack's lifecycle.
> - **Architecture:** A custom resource is backed by an AWS Lambda function. CloudFormation sends events to this Lambda function, which contains the custom logic to create, update, or delete the resource. The Lambda function is responsible for signaling success or failure back to CloudFormation.
> - **Key Use Case:** A common use case is to solve the problem of a stack failing to delete an S3 bucket because it contains objects. A custom resource can be created to ensure the bucket is emptied during stack deletion, allowing the process to complete successfully.
> #### Core Architecture and Event Flow
> - **Resource Declaration:** A custom resource is declared in a CloudFormation template with a logical type such as `AWS::CloudFormation::CustomResource` or a custom type like `Custom::MyCustomResource`.
> - **The `ServiceToken`:** The custom resource's declaration must include a `ServiceToken` property, which specifies the Amazon Resource Name (ARN) of the Lambda function that will handle the resource's events.
> - **CloudFormation Events:** CloudFormation sends a JSON-formatted event to the Lambda function. This event includes important information for the Lambda function, such as:
>     - `RequestType`: Indicates whether the event is for a `Create`, `Update`, or `Delete` action.
>     - `ResourceProperties`: The properties you pass to the custom resource in your template.
>     - `ResponseURL`: A pre-signed S3 URL that the Lambda function must use to send its response back to CloudFormation.
> #### The Deletion Lifecycle and Cleanup
> - **The Problem:** CloudFormation cannot delete a non-empty S3 bucket. If a stack creates a bucket and objects are later added, the stack deletion will fail.
> - **The Custom Resource Solution:** The custom resource is added to the template along with the S3 bucket. A dependency is created by having the custom resource reference the bucket's name. This ensures that CloudFormation attempts to delete the custom resource _first_.
> - **Deletion Event:** When a stack deletion is initiated, CloudFormation sends a `Delete` event to the Lambda function.
> - **Cleanup Logic:** The Lambda function's code is specifically designed to handle this `Delete` request. It will retrieve the S3 bucket name from the event data and programmatically **delete all objects** within the bucket.
> - **Success Signal:** After the bucket is empty, the Lambda function sends a success signal to the `ResponseURL`, and CloudFormation can then successfully proceed to delete the now-empty S3 bucket resource.
> #### Key Components and Best Practices
> - **Implicit Dependency:** The custom resource's dependency on the S3 bucket is crucial. By referencing the bucket's name in the custom resource's properties, you guarantee that the cleanup logic runs in the correct order before CloudFormation attempts to delete the bucket itself.
> - **Lambda Function Logic:** Your Lambda function must handle all three request types (`Create`, `Update`, `Delete`) and send a response back to CloudFormation for each one.
> - **Error Handling:** If your Lambda function fails to send a response to the `ResponseURL` or sends a failure status, CloudFormation will eventually time out and fail the stack operation, so robust error handling is essential.

- Logical resources in a template - what you want
- CFN uses them to create, update, and delete physical resources
- However, CFN doesn't support everything.
- Custom Resources let CFN integrate with anything it doesn't yet, or doesn't natively support
- Architecture = passes data to something, gets data back from something
w/o custom resource
- template -> stack -> physical resources -> add items to bucket -> deletion error because bucket not empty
w/ custom resource
- custom resource -> stack (backed by lambda) -> physical resource 
- deleting works backwards, so we called Lambda when we created stack, backwards means that Lambda function will be invoked again
- Lets us invoke our Lambda function to remove objects from bucket, send ResponseURL to StackDelete to allow us to delete the bucket