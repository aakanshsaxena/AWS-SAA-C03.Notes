
>[!note]- Post-Processing
>## Key Insights and Information from the AWS Parameter Store Lesson:
>
>**What is it?**
>
>* AWS Parameter Store is a service for securely storing system configuration data like strings, documents, and secrets.
>* It offers resilience, scalability, and security for managing your configuration information.
>
>**Why use it?**
>
>* **Improved Security:**  Avoids storing secrets directly in EC2 instances, mitigating the risk of exposure.
>* **Centralized Management:**  Provides a single location to store and manage configuration data across your AWS environment.
>* **Integration with AWS Services:**  Seamlessly integrates with services like CloudFormation and Lambda.
>
>**Key Features:**
>
>* **Parameter Types:**
>    * Strings
>    * String Lists
>    * Secure Strings (encrypted using KMS)
>* **Hierarchical Structure:** Organize parameters into logical groups for better management.
>* **Versioning:** Track changes and revert to previous versions if needed.
>* **Public Parameters:** AWS provides pre-defined public parameters for common use cases.
>* **Permissions:** Fine-grained control over access to parameters using IAM.
>* **Event Notifications:** Trigger actions in other AWS services based on parameter changes.
>
>**How to use it:**
>
>* **AWS Console:**  Manage parameters through a user-friendly interface.
>* **AWS CLI:**  Interact with Parameter Store programmatically.
>* **CloudFormation:**  Define and manage parameters as part of your infrastructure deployments.
>
>**Benefits:**
>
>* Enhanced security and compliance.
>* Simplified configuration management.
>* Improved collaboration and automation.
>
>
>**Next Steps:**
>
>* The lesson concludes with a demo showcasing how to interact with Parameter Store using the console and AWS CLI. 
>

- Storage for configuration & secrets
- String, StringList & SecureString
- Good for license codes, DB strings, full configs and passwords
- Hierarchies & Versioning
- Plaintext and Ciphertext
- Public Parameters - latest AMIs per region
- App, Lambda, EC2 can all utilize systems manager parameter store, and IAM authorizes access
- Allows you to make flat and hierarchical structures inside the store
