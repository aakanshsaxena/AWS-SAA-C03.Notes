Invocation
- We can have **synchronous** invocations which means the someone invokes the lambda function and waits for a response -> Lambda either responds or fails
- Results (Success or Failure) returned during the request
- Errors or Retries have to be handled within the client
- Best used for a human manually making invocations
- We can also have **asynchronous** invocations which is typically used when AWS services invoke Lambda functions
- If processing fails, Lambda will retry between 0 and 2 times (configurable), and Lambda handles the retry logic
- We want to make sure that the functions is idempotent - meaning that continuous re runs won't give us the wrong effect (e.g. if we want a function that adds $10 from $10 to $20, idempotent = setting bank balance to $20 versus adding $10 over and over again)
- Events can be sent to dead letter queues after repeated failed processing
- Lambda supports destinations (SQS, SNS, Lambda & EventBridge) where succesful or failed events can be sent
- We can also use **Event Source Mapping** which is typically used on streams or queues which don't support event generation to invoke Lambda (Kinesis, DynamoDB Streams, SQS)
- Permissions from the Lambda execution role are used by the event source mapping to interact with the event source
- SQS Queues or SNS Topics can be used for any discarded failed event batches
Versions
- Lambda functions have versions
- These are the code + configuration of the Lambda function
- They are immutable and never change once published and have their own ARN
- $Latest points at the latest version
- Aliases (DEV, STAGE, PROD) point at a version and can be changed
Execution
- An execution context is the environment a Lambda function runs in. A cold start is a full creation and configuration including function code download (100ms)
- A Lambda invocation can reuse an execution context but has to assume it can't. If used infrequently contexts will be removed. Concurrent executions will use multiple contexts.
- Provisioned currency can be used. AWS will create and keep __ contexts warm and ready to use -> improving start speeds
- With a warm start, the same execution context is reused. A new event is passed in but the execution context creation can be skipped (1-2 ms).