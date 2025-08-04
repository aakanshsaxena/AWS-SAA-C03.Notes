
>[!note]- Post-Processing
>## AWS Backup: Key Insights and Information
>
>This transcript provides a solid overview of AWS Backup, focusing on essential knowledge for AWS certifications and practical use. 
>
>**Here are the key takeaways:**
>
>**What is AWS Backup?**
>
>* A fully managed data protection service acting as a centralized backup and restore solution.
>* Offers more than just backup and restore, including auditing and management oversight.
>* Consolidates backup management and storage across multiple AWS accounts and regions.
>
>**Benefits:**
>
>* Simplifies backup management by handling backups for various AWS services in one place.
>* Enables cross-account and cross-region data protection.
>
>**Supported Services:**
>
>* **Compute:** EC2, VMware running on AWS
>* **Block Storage:** EBS
>* **File Storage:** EFS, FSx
>* **Databases:** Aurora, RDS, Neptune, DynamoDB, DocumentDB
>* **Object Storage:** S3
>
>**Key Concepts and Components:**
>
>* **Backup Plans:** Define backup frequency (hourly, daily, weekly, monthly, cron expression), backup window, lifecycle policies, vault, and region copy.
>* **Backup Resources:**  Specify the individual AWS resources to be backed up (e.g., S3 bucket, RDS database).
>* **Vaults:** Store backup data. Can be configured with AWS Backup Vault Lock for write-once read-many (WORM) protection.
>* **On-Demand Backups:** Allow for manual backups beyond scheduled plans.
>* **Point-in-Time Recovery:** Supported by some services (e.g., S3, RDS) enabling restoration to a specific point in time within the retention window.
>
>**Additional Resources:**
>
>* The transcript encourages viewers to refer to official AWS documentation for the most up-to-date information on AWS Backup features.
>
>
>**Overall, this transcript provides a concise and informative introduction to AWS Backup, highlighting its key features and benefits. It emphasizes the importance of understanding the core concepts for AWS certifications and encourages further exploration through official resources.**

- Fully managed data-protection (backup/restore) service
- Consolidate management into one place across accounts and across regions
- Supports a wide range of AWS products
- Supports backup plans which list frequency, window, lifecycle, vault, region copy settings
- Resources - what resources are backed up 
- Vaults - backup destination (container), assign a KMS key for encryption
- Vault Lock - write-once, read-many (WORM), 72 hour cool off and even AWS can't delete (helpful for compliance, means that no one can edit or delete until end of retention period)
- Can still create on demand backups as needed
- Supports PITR (point in time recovery) 
