
>[!note]- Post-Processing
>## Key Insights and Information from EC2 Launch Configurations and Templates Lesson:
>
>**What they do:**
>
>* Both launch configurations and launch templates define the configuration of EC2 instances in advance.
>* This includes:
>    * AMI to use
>    * Instance type and size
>    * Storage configuration
>    * Key pair
>    * Networking configuration
>    * Security groups
>    * User data
>    * IAM role
>
>**Key Differences:**
>
>* **Launch Templates:**
>    * Newer feature, superset of launch configurations.
>    * Include versioning.
>    * Support additional features:
>        * T2/T3 unlimited CPU options
>        * Placement groups
>        * Capacity reservations
>        * Elastic graphics
>* **Launch Configurations:**
>    * Older feature, limited to use with auto-scaling groups.
>    * No versioning.
>
>**AWS Recommendation:**
>
>* Use launch templates as they offer more features and flexibility.
>
>**Use Cases:**
>
>* **Launch Configurations:**
>    * Defining the configuration for EC2 instances within auto-scaling groups.
>* **Launch Templates:**
>    * Defining the configuration for EC2 instances within auto-scaling groups.
>    * Launching EC2 instances directly from the console or CLI.
>
>**Important Notes:**
>
>* Both launch configurations and launch templates are **not editable** after creation.
>* Any changes require creating a new configuration.
>
>
>This lesson provides a foundational understanding of launch configurations and launch templates, highlighting their similarities and differences. It emphasizes the advantages of using launch templates and their broader applicability.
>

LC and LT Key Concepts
- Allow you to define the configuration of an EC2 instance in advance
- Let you decide networking and security groups an instance uses + AMI, Instance Type, Storage & Key Pair
- Let you configure Userdata which is given to the IAM Role to provide the instance permissions
- Both are not editable - LT has version though
- LT is the newer version and has newer features like T2/T3 unlimited CPU, placement groups, capacity reservations, and elastic graphs
- LC are only used within autoscaling groups, LT can be used within autoscaling groups + for launching EC2 instances
