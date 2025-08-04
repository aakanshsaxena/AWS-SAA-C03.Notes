
>[!note]- Post-Processing
>## VPC Flow Logs: Key Insights and Information
>
>This transcript provides a comprehensive overview of AWS VPC Flow Logs, a valuable networking feature for understanding traffic flow within private networks. 
>
>Here are the key takeaways:
>
>**What are VPC Flow Logs?**
>
>* Capture **packet metadata**, not content.
>* Useful for observing network traffic patterns.
>* **Do not provide real-time telemetry**. There is a delay between traffic flow and log updates.
>
>**How do they work?**
>
>* **Virtual monitors** are attached to VPCs, subnets, or individual network interfaces.
>* Flow logs capture traffic **from the monitored point downwards**.
>* Can be configured to capture metadata for **accepted, rejected, or all connections**.
>
>**Where is the data stored?**
>
>* **S3** allows direct access and integration with third-party tools.
>* **CloudWatch Logs** offers integration with other AWS services and programmatic access.
>* **Athena** enables ad-hoc querying of flow logs stored in S3 using SQL.
>
>**What information do they contain?**
>
>* **Flow Log Records** consist of fields like:
>    * Source and destination IP addresses
>    * Source and destination ports
>    * Protocol (e.g., ICMP, TCP, UDP)
>    * Action (accepted or rejected)
>
>**Important Considerations:**
>
>* **Security Groups:** Evaluate conversations (request and response) as a single unit.
>* **Network ACLs:** Evaluate requests and responses separately, potentially resulting in two log entries.
>* **Excluded Traffic:** Metadata service, time server requests, and communications with license servers are not logged.
>
>**Practical Applications:**
>
>* Troubleshooting network connectivity issues.
>* Identifying security threats and anomalies.
>* Monitoring application performance and traffic patterns.
>* Auditing network activity for compliance purposes.
>
>
>
>This transcript provides a solid foundation for understanding VPC Flow Logs and their practical applications in managing and securing AWS networks.
>

- Capture metadata (not contents)
	- version, account-id, interface-id, **srcaddr**, **dstaddr**, **srcport**, **dstport**, **protocol**, packets, bytes, start, end, **action**, log-status
- Attached to a VPC
	- Can attach it to all ENIs in that VPC, all ENIs in a subnet, or specific ENIs directly
- Flow Logs are not realtime
- We can send flow logs to S3 or CloudWatch Logs or Athena for querying
- Flow logs capture metadata from the capture point down (VPC, subnet, interface)
- Flow Logs can capture accepted, rejected, or all metadata
- It will not record some data, like from 169.254.169.254 (userdata/metadata), 169.254.169.123, DHCP, Amazon DNS Server & Amazon Windows License
