### IAM Users
- IAM Users are an identity used for anything requiring long-term AWS access e.g.. Humans, apps, or service accounts
	- If you can picture one thing, a named thing then you need an IAM User typically
- IAM starts with a principal = an entity trying to access an AWS account. Can be individual people, computers, services, or a group of any of those things
	- Makes requests with IAM to be able to access resources, to authenticate against an identity within IAM 
	- Authentication is done by either using username + password, or access keys
	- After it's authenticated then it is considered an authenticated identity
### Amazon Resource Name (ARN)
- ARN = uniquely identify resources within any AWS accounts
- Formats:
	- arn:partition:service:region:account-id:resource-id
	- arn:partition:service:region:account-id:resource-type/resource-id
	- arn:partition:service:region:account-id:resource-type:resource-id
		- arn:aws:s3:::catgifs = bucket
		- arn:aws:s3:::catgifs/* = objects in the bucket
		- These two don't overlap
		- Use double colon when something doesn't need to be specified, * when we want to refer to all possible
### Exam Powerup
- 5,000 IAM Users per account 
- IAM User can be a member of max 10 groups
- This has systems design impacts
	- Might be a limit for internet-scale apps
	- Large orgs & org merges
- Can use IAM Roles & Identity Federation to solve this problem