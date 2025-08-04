
>[!note]- Post-Processing
>## RDS Custom: Key Insights and Information
>
>This transcript discusses RDS Custom, a lesser-known feature of AWS Relational Database Service (RDS). Here are the key takeaways:
>
>**What is RDS Custom?**
>
>* Bridges the gap between fully managed RDS and self-managed databases on EC2.
>* Offers customization options similar to EC2 while leveraging some RDS benefits.
>* Currently supports MS SQL and Oracle.
>
>**Key Differences from RDS:**
>
>* **Management:** RDS is fully managed by AWS, while RDS Custom runs within your AWS account, giving you more control.
>* **Visibility:** RDS resources are hidden within AWS's managed environment, while RDS Custom instances, EBS volumes, and backups are visible in your account.
>* **Access:** RDS Custom allows SSH, RDP, and Session Manager access to the operating system and database engine.
>
>**Service Model:**
>
>* **RDS:** AWS manages everything except application optimization.
>* **RDS Custom:** Shared responsibility model where AWS manages hardware and RDS Custom handles application optimization.
>
>**Real-World Use:**
>
>* Niche feature with limited real-world applications.
>* Primarily useful for specific customization needs not met by standard RDS.
>
>**Exam Relevance:**
>
>* Understanding the existence and basic functionality of RDS Custom is sufficient for exams.
>
>
>**In summary, RDS Custom offers a middle ground between fully managed RDS and self-managed databases on EC2, providing increased customization but requiring more customer involvement in management tasks.**
>

- Fills the gap between RDS and EC2 running as a DB Engine
- RDS is fully managed but OS/Engine access is limited
- DB on EC2 is self managed but has high overhead
- RDS Custom only works right now for MS SQL and Oracle
- Can connect using RDP, SSH, Session Manager
- RDS Custom Database Automation should be paused when customizing and resuming for normal production usage
![[Pasted image 20250721211159.png]]