**S3 Standard**
- Objects are stored and replicated across at least three availability zones
- Provides 11 9's of durability - if you store 10M objects, 1 object less per 10,000 years
- Replication over 3 AZ's & Content-MD5 checksums and Cyclic Redundancy Checks (CRCs) are used to detect and fix any data corruption.
- *When objects are stored properly a HTTP/1.1 200 OK response is provided by S3 API Endpoint*
- Charged GB/m fee for data stored, and transfer out, and price per 1K requests.
- Milliseconds first byte latency (availability) and objects can be made publicly available through S3 permissions or static website hosting
- ***Use S3 Standard for Frequently Accessed Data which is important and Non Replacable***
**S3 Standard-IA**
- Same availability, durability, checks as S3 Standard
- Minimum duration charge of 30 days (objects will be charged at minimum as they were stored for 30 days)
- Cheaper per GB stored
- New cost: per GB data retrieval fee
- Minimum capacity cost of 128KB per object
- **S3 Standard-IA should be used for long-lived data which is important but where access is infrequent***
**S3 One Zone-IA**
- Same concept as Standard-IA
- Difference is that this one only stores the data in one AZ
	- Does not provide the multi-AZ resilience model of Standard and Standard-IA
	- Same 11 9's of durability unless the AZ fails
- **S3 One Zone-IA should be used for long-lived data which is NON-CRITICAL and REPLACEABLE and where access is infrequent***