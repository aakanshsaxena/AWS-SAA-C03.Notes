
>[!note]- Post-Processing
>## Key Insights and Information from the AWS AMI Transcript:
>
>**What are AMIs?**
>
>* AMIs (Amazon Machine Images) are templates for launching EC2 instances.
>* They contain the configuration of an instance, including the operating system, applications, and attached EBS volumes.
>* AMIs can be used to quickly and easily create multiple identical instances.
>
>**Types of AMIs:**
>
>* **AWS-provided AMIs:** Pre-built images for common operating systems and software distributions like Amazon Linux 2.
>* **Community-provided AMIs:** Images from third-party vendors like Red Hat, CentOS, and Ubuntu.
>* **Marketplace-provided AMIs:** Images that include commercial software, with additional licensing costs.
>
>**AMI Lifecycle:**
>
>1. **Launch:** Use an AMI to create an EC2 instance.
>2. **Configure:** Customize the instance with desired software, applications, and settings.
>3. **Create Image:** Capture the customized configuration as a new AMI.
>4. **Launch Again:** Use the new AMI to create additional instances with the same configuration.
>
>**AMI Architecture:**
>
>* AMIs are regional constructs, meaning an AMI created in one region can only be used in that region.
>* AMIs reference EBS snapshots of the original instance's volumes, allowing for consistent volume configurations across instances.
>* Block device mapping links snapshot IDs to device IDs, ensuring correct volume attachment to new instances.
>
>**Important Considerations:**
>
>* **AMI Baking:** The process of creating an AMI from a customized instance for efficient deployment of identical configurations.
>* **AMI Immutability:** AMIs cannot be directly edited; changes require creating a new AMI from an updated instance.
>* **AMI Copying:** AMIs can be copied between AWS regions.
>* **AMI Cost:** AMIs incur storage costs based on the size of the referenced EBS snapshots.
>
>**Exam Power-Ups:**
>
>* Understand the regional nature of AMIs and their usage within a region.
>* Recognize the concept of AMI baking and its benefits.
>* Remember that AMIs are immutable and require a new AMI for configuration changes.
>* Be aware of the cost implications associated with AMI storage.
>
>
>
>This summary provides a concise overview of the key concepts and information presented in the transcript.
>

- Can be used to launch EC2 instance
- AWS or Community Provided
- Marketplace (can include commercial software - often an additional cost)
- Unique AMI ID (Format ami-letters/numbers), unique to that region
- Permissions (Public, your account, explicitly stated accounts)
- Can create an AMI from an EC2 instance you want to template
Architecture
- Launch 
	- Launch an instance with its own EBS volumes (BOOT /dev/xvda DATA /dev/xvdf)
- Configure
	- Configure the instance and apply any customizations -> 
- Create Image
	- An AMI is created of that instance and any volumes attached to it
	- When you create an AMI, the snapshots from the original EBS volumes -> referenced inside the AMI via block device mapping
- Launch
	- Launch an instance using AMI with the same EBS configurations as the original
**Exam Powerups**
- AMI = One region, only works in that region
- AMI Baking = creating an AMI from a configured instance + application
- An AMI cannot be edited. If you need to edit, launch the instance from the AMI -> update the configuration and make a new AMI
- Can be copied between regions (includes its snapshots)
- Remember permissions (three options):
	- Your account
	- Accounts you explicitly say are allowed access to the AMI
	- Publicly available
