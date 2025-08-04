
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**EC2 Instance Roles: Best Practice for Service Permissions**
>
>* **IAM Roles:**  The best way to grant permissions to AbleUS services from one service to another.
>* **EC2 Instance Roles:** Roles specifically for EC2 instances.  
>    *  Allow instances to assume a role and gain its permissions.
>    *  Enable applications running on the instance to access AWS resources.
>
>**Instance Role Architecture:**
>
>1. **IAM Role:**  Contains a permissions policy defining what actions the role can perform.
>2. **Instance Profile:**  A wrapper around an IAM role. 
>    *  Attached to an EC2 instance.
>    *  Delivers the role's permissions to the instance.
>3. **Instance Metadata:**  
>    *  Stores temporary security credentials generated when the instance assumes the role.
>    *  Applications inside the instance access these credentials via the metadata.
>
>**Benefits of Instance Roles:**
>
>* **Always Valid Credentials:** EC2 and STS (Security Token Service) ensure credentials are renewed before expiration.
>* **Security:** Avoids storing long-term credentials (access keys) in instances, reducing security risks.
>* **Automation:** AWS CLI tools automatically use instance role credentials.
>
>**Important Points:**
>
>* **Attach Instance Profile, Not Role:** When using the AWS console, you attach an instance profile, not the role directly.
>* **Periodic Refresh:** Applications should periodically check the metadata for updated credentials.
>* **Avoid Caching:**  Do not cache credentials for extended periods.
>
>
>**Overall Message:**
>
>EC2 instance roles are a secure and efficient way to manage permissions for applications running on EC2 instances. Always prioritize using roles over storing long-term credentials.
>

- Permissions policy with some permissions -> used to create an IAM Role
- In order for IAM Role to be applied to an EC2 instance we apply it to the corresponding InstanceProfile, that profile is attached to the instance which delivers temp credentials to the instance via meta-data.
- Credentials are inside meta-data
- IAM/Security-Credentials/Role-Name
- Automatically rotated -> always valid
- Should always be used rather than adding access keys (permanent) into instance
- CLI tools will use ROLE credentials automatically