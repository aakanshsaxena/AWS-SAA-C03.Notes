- S3 is private by default - only identity with access is the account which created it.
Bucket Policies
- A form of resource policy (like an identity policy, but attached to a bucket)
	- Who can access a resource?
- Allow/deny within the same account or different AWS accounts
- Allow/deny anonymous principals
- Can set anonymous principals by setting to "Principal": "*"
- Can block specific IP addresses
- Can only have one bucket policy per bucket
**Exam Powerup**
- When to use identity policies
	- Controlling different resources (not just S3)
	- Preference for IAM (can only use identity policies within IAM)
	- Adjusting access within the same AWS account
- When to use bucket policies/resource policies
	- Just controlling access to S3
	- Allowing anonymous/cross-account access
- ACLs
	- Never - unless you absolutely have to