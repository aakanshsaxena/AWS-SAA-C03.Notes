
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**Problem:**
>
>* CloudWatch and CloudWatch Logs can't natively access data inside an EC2 instance.
>
>**Solution:**
>
>* Use the **CloudWatch Agent**, a software installed on the EC2 instance, to capture OS-level data and logs and send them to CloudWatch and CloudWatch Logs.
>
>**Architecture:**
>
>* **CloudWatch Agent:** Runs on the EC2 instance and captures data.
>* **IAM Role:** Grants the agent permissions to interact with CloudWatch and CloudWatch Logs.
>* **Log Groups:**  Used to organize logs, with one group per log file.
>* **Log Streams:** Within each log group, a stream is created for each instance logging data.
>
>**Configuration:**
>
>* The agent needs configuration to specify which data to capture.
>* This configuration can be stored in the **AWS Parameter Store**.
>
>**Implementation:**
>
>* **Manual:** Install agent, configure it, attach role, and start capturing data (for single instances).
>* **Automated:** Use tools like **CloudFormation** to automate agent configuration for multiple instances.
>
>**Demo Lesson:**
>
>* The next lesson will demonstrate how to install and configure the CloudWatch agent using the Parameter Store to capture logs from three files:
>    * `/var/log/secure` (Apache access log)
>    * `/var/log/secure` (Apache error log)
>
>
>**Key Takeaways:**
>
>* The CloudWatch Agent is essential for accessing internal EC2 instance data and logs.
>* IAM roles provide secure access for the agent to CloudWatch and CloudWatch Logs.
>* Parameter Store is a convenient way to store and manage agent configurations.
>* Automation tools like CloudFormation can streamline agent deployment and configuration at scale.

- CloudWatch can only really be used to measure metrics that we can see from "outside" the instance
- Sometimes we might want access to OS level metrics (like apps running, how much memory they are taking)
- We need CloudWatch Agent and configurations and permissions for this
- We create and configure a CloudWatch Agent on our EC2 instance and give it appropriate permissions (through IAM Roles on our EC2 instance profile).
- Log injected into CloudWatch using log groups, we can configure one log group for every log file, and for each log file there will be one log stream 
- We can use parameter store and store the agent configuration as a parameter