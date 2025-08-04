
>[!note]- Post-Processing
>## Key Insights and Information from the EC2 Bootstrapping Lesson:
>
>**What is EC2 Bootstrapping?**
>
>* EC2 bootstrapping is a powerful feature that allows you to automate the configuration of EC2 instances when they are launched.
>* It enables you to run scripts or configurations on an instance at launch time, bringing it into a pre-configured state.
>
>**How it Works:**
>
>* EC2 bootstrapping utilizes **user data**, a piece of information passed to the instance during launch.
>* This user data is executed by the instance's operating system as the root user only **once** at launch time.
>* EC2 doesn't interpret or validate user data, it simply passes it to the instance.
>
>**Important Considerations:**
>
>* **Security:** User data is not secure, so avoid storing sensitive information like long-term credentials within it.
>* **Size Limit:** User data is limited to 16 kilobytes. For larger configurations, use a script to download the necessary data.
>* **Execution:** User data is executed only once at launch. Changes made after launch won't be reflected unless the instance is restarted with updated user data.
>
>**Boot Time to Service Time:**
>
>* This metric measures the time it takes for an instance to be ready for service after launch.
>* AWS-provided AMIs generally have a boot time to service time of minutes.
>* **Post-launch time** refers to the time required for manual or automated configuration after launch.
>
>**Reducing Post-Launch Time:**
>
>* **Bootstrapping:** Automates installations and configurations, reducing post-launch time.
>* **AMI Baking:** Front-loads work by including configurations in the AMI, eliminating post-launch time but reducing flexibility.
>* **Optimal Approach:** Combine AMI baking for time-intensive tasks and bootstrapping for final configurations to maximize efficiency and flexibility.
>
>
>**Overall, EC2 bootstrapping is a powerful tool for automating instance configurations and reducing boot time to service time. However, it's crucial to understand its limitations and security implications.**
>

EC2 Bootstraping
- Allows EC2 Build Automation
- User data is accessed via the meta-data IP
	- http://169.254.169.254/latest/user-data
- Anything in user data is executed by the instance OS
- Only on LAUNCH (first time launch)
- EC2 doesn't interpret or check this data, the OS just needs to understand it and it will do it no matter what the instruction is
- AMI -> Instance <-> EC2 (sends user data)
	- Execute user data -> if good, running ready for service
	- If not, bad config
User Data Key Points
- Opaque to EC2, just a block of data
- Not secure - don't use for passwords or long term credentials
- User data is limited to 16KB
- Can be modified when instance is stopped, but only executed once at launch
Boot-Time-To-Service-Time
- How quickly you can bring an instance into service?
- AMI -> Instance -> Post Launch Time (download SW, etc.)
- AMI -> Instance -> Bootstrapping configurations
- AMI Bake -> AMI -> Instance
	- AMI Baking pre loads the AMI with the software needed, but can take away users ability to configure as needed
	- Combination of bootstrapping and AMI baking is best normally, for example if we need to install something that would take 90% time to download 10% to configure, we can pre bake the AMI to be installed with the software and then let the user bootstrap the 10%.
	