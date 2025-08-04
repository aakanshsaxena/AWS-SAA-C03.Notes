- By default, Lambda functions are given public networking -> they can access public AWS services and the public internet
- Public networking offers the best performance because no customer specific VPC networking is required
- Lambda functions have no access to VPC based services unless public IPs are provided and security controls allow external access
- We can also run Lambda within a private VPC in the same way we run any other AWS services within a VPC
	- By default it wouldn't have access to the public internet but we can configure VPC Endpoints to provide access to public AWS services
	- We can use NatGW and Internet Gateway to allow VPC Lambdas to access internet resources
- In the past, each Lambda invocation required creating an ENI for every invocation of a function -> slow.
- Now the Lambda Service VPC can connect to our VPC through a NATGW, each unique combination of security group and subnets, each time a ENI is loaded there is a 90second delay but it's only for the first invocation.
	- For example, if we have 3 subnets and 1 security group across the subnets, we would have 3 ENI's. If we had 1 subnet and 4 security groups, we would have 4 ENI's
Security
- Lambda resource policy controls what services and accounts can invoke lambda functions
- Lambda execution policies are IAM roles attached to Lambda functions which control permissions the Lambda function receives. 
Logging
- Lambda uses CloudWatch for metrics - invocation success/failure, retries, latency
- CloudWatchLogs - logs from Lambda executions
- Can be integrated with X-Ray for distributed tracing
- CloudWatch Logs require permissions via Execution role