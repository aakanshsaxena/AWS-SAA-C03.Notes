## IAM Basics

- Globally resilient service, data stays available and secure across all AWS regions
  
- IAM of account is primarily trusted with all abilities (like Root User minus some billing permissions and account closure permissions)
  
- Lets you create three different types of accounts, IAM users, groups, roles
  
  - Users - identities which represent humans or applications that need access to your account
    
  - Group - collection of related users (dev team, HR)
    
  - Role - can be used by AWS services, or for granting external access to your AWS account (used when number of things is uncertain or if you want AWS services themselves to interact with other AWS services)
    
- Policy/policy document - can be used to allow or deny access to AWS services when and only when they are attached to user, group, role
  
- IAM has three main principles/jobs:
  
  - **ID Provider/IDP** - Manages identities
    
  - **Authenticate** - prove you are who you claim to be
    
  - **Authorize** - allow or deny access to resources
### Summary

- No cost
    
- Global Service/Global Resilience
    
- Allow or deny its identities on its AWS account
    
- No direct control on external accounts or users
    
- Lets you make use of identity federation and MFA