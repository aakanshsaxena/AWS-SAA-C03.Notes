> [!note]- AI
> #### Amazon Inspector: Core Functionality and Architecture
> - **Purpose:** Amazon Inspector is an automated security assessment service that continuously scans your AWS resources for software vulnerabilities and unintended network exposure.
> - **Continuous Scanning:** The modern version of Inspector operates on a continuous, event-driven basis rather than fixed schedules. It automatically discovers and scans resources like EC2 instances, container images in ECR, and Lambda functions. It also detects and scans newly deployed resources.
> - **Findings:** Inspector produces a detailed list of security findings, prioritized by severity (Critical, High, Medium, Low), that can be reviewed in the console. Findings include details about the vulnerability, the affected resource, and remediation guidance.
> - **Agent Requirement:** Inspector uses the **AWS Systems Manager (SSM) Agent** that is pre-installed on most modern AMIs for host-level assessments. Some assessments can be performed agentlessly, while others require the agent for a more detailed analysis.
> #### Network Assessments
> - **Network Reachability Package:** This rules package analyzes your network configurations (VPC, security groups, ACLs, etc.) to identify any unintended network paths to your EC2 instances. It can run **without an agent**, which is a key exam point.
> - **Agent vs. Agentless:** When an agent is **not** present, Inspector can still identify if a port is publicly exposed based on your network configuration. However, with the agent installed, it can provide more granular detail, such as whether a process is actually listening on that exposed port, which is crucial for confirming a true vulnerability.
> #### Host-Level Rules Packages
> - **These rules packages require the SSM Agent** to be installed on the EC2 instance, as they inspect the operating system, installed software, and configurations.
> - **Common Vulnerabilities and Exposures (CVEs):** This package checks your instances and containers for known software vulnerabilities by comparing the software installed against the CVE database. Findings are reported with a CVE ID, severity, and remediation steps.
> - **Center for Internet Security (CIS) Benchmarks:** This package evaluates your EC2 instances' operating system configurations against the industry-standard CIS Security Benchmarks. This helps you ensure that your systems are configured according to consensus-based best practices.
> - **Security Best Practices:** This rules package checks for a collection of security best practices, such as disabling root SSH logins, ensuring password policies are met, and other common misconfigurations.
> #### Exam Preparation
> - **Keyword Association:** For the exam, associate **Inspector** with keywords like **CVE**, **CIS Benchmarks**, **network reachability**, and **vulnerability assessment**.
> - **Agent's Role:** Understand when the agent is required. Host-level assessments (CVE, CIS) depend on the agent to gather data from inside the OS, while the network reachability assessment can be performed agentlessly.
> - **High-Level Function:** Remember that Inspector is a **detective control** that identifies vulnerabilities and misconfigurations. It does not prevent them or automatically remediate them without integration with other services.

- Scans EC2 instances and the instance OS along with containers
- Checks for vulnerabilities and deviations against best practice
- Length: 15mins, 1 hour, 8/12 hours, or 1 day
- Provides a report of findings ordered by priority
- Network Assessment (Agentless)
- Network & Host Assessment (Agent)
- Rules package determine what is checked
- Network Reachability (no agent required)
- Agent can provide additional OS visibility
- Check reachability end to end. EC2, ALB, DX, ELB, ENI, IGW, ACLs, RT's, SG's, Subnets, VPCs, VGW & VPC Peering
- RecognizedPortWithListener, RecognizedPortNoListener, RecognizedPortNoAgent
- UnrecognizedPortWithListener
- Packages (.. Host Assessments, Agent required)
- CVE
- Center for Internet Security (CIS) Benchmarks
- Security best practices for Amazon Inspector