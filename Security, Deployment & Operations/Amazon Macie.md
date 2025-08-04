> [!note]- AI
> #### AWS Macie: Multi-Account Architecture
> - **Purpose:** AWS Macie is a data security and privacy service that uses machine learning to automatically discover, classify, and protect sensitive data in Amazon S3. It provides visibility into where sensitive data resides and monitors for potential security risks.
> - **Multi-Account Management:** Macie is designed for multi-account environments. A single administrator account can be designated to manage and monitor Macie across all member accounts in an AWS Organization, providing a centralized view of your S3 data security posture.
> - **Findings and Remediation:** Macie produces **findings** when it discovers sensitive data or security risks. These findings can be sent to Amazon EventBridge, which allows you to set up automated remediation workflows using services like AWS Lambda.
> #### Discovery Jobs and Data Identifiers
> - **Discovery Jobs:** These jobs are configured to analyze objects in specific S3 buckets on a one-time or scheduled basis. Macie samples and analyzes objects for sensitive data, which is then reported in its findings.
> - **Managed Data Identifiers:** These are pre-built, pattern-matching and machine learning models that are provided and maintained by AWS. They automatically detect a growing list of sensitive data types, such as **personally identifiable information (PII)**, financial information (e.g., credit card numbers), and healthcare data.
> - **Custom Data Identifiers:** You can create your own custom identifiers using regular expressions (regex) to detect organization-specific sensitive data patterns. Custom identifiers can be further refined with additional criteria.
> #### Custom Data Identifier Refinements
> - **Keywords:** You can specify keywords that must be in close proximity to the text that matches your regex pattern.
> - **Maximum Match Distance:** This defines the maximum number of characters that can exist between a keyword and the regex match.
> - **Ignore Words:** This is a crucial feature that allows you to specify words or phrases to exclude from a match. If the text matches the regex pattern but also contains an "ignore word," Macie will disregard it, which is useful for reducing false positives.
> #### Types of Findings
> - **Policy Findings:** These are generated when Macie detects a potential policy violation or security risk with the configuration of an S3 bucket itself. Examples include a bucket becoming publicly accessible, encryption being disabled, or external sharing permissions being misconfigured.
> - **Sensitive Data Findings:** These are generated when a discovery job finds actual sensitive data within an S3 object. The findings provide details about the location and type of sensitive data found, such as PII, credentials, or financial data.
> #### Definitions
> - **Ignore Words:** In the context of a custom data identifier, these are specific words or phrases that, if present, cause Macie to ignore a potential match to the defined regular expression, helping to eliminate false positives.
> - **Policy Findings:** A report from AWS Macie that identifies potential security risks or policy violations with an Amazon S3 bucket's configuration (e.g., access control, encryption status), rather than detecting sensitive data within the bucket's objects.
> - **Personally Identifiable Information (PII):** Any information that can be used to distinguish or trace an individual's identity, either alone (e.g., Social Security Number) or when combined with other data (e.g., a combination of name, date of birth, and location).

- Data Security and Data Privacy Service
- Discover, Monitor and Protect Data stored in S3 Buckets
- Automated discovery of data (PII, PHI, Finance)
- Managed Data Identifiers - Built-in, ML, Patterns
- Custom Data Identifiers - Proprietary - Regex Based
- Integrates - w/ security hub & finding events to EventBridge
- Centrally manage either via AWS ORG or one Macie Account inviting
Architecture
- We have S3 buckets that we feed into Macie, and run discovery jobs on discovery schedules that look for managed data identifiers/custom data identifiers
- If it finds an event, we can either deliver it as an event to EventBridge and then to other AWS services or just as findings
Identifiers
- Managed data identifiers - maintained by AWS
	- growing list of common sensitive data types: creds, finance, health, PII
- Custom data identifiers - created by you
- Regex - defines a pattern to match in data
- Keywords - optional sequences that need to be in proximity to regex match
- Maximum Match Distance - how close keywords are to regex pattern
- Ignore Words - if regex match contains ignore words, it's ignored
Findings
- Policy Findings or Sensitive data findings
- Policy:IAMUser/S3BlockPublicAccessDisabled, Policy:IAMUser/S3BucketEncryptionDisabled, Policy:IAMUser/S3BucketPublic, Policy:IAMUser/S3BucketSharedExternally
- SensitiveData:S3Object/Credentials, SensitiveData:S3Object/CustomIdentifier, SensitiveData:S3Object/Financial, SensitiveData:S3Object/Multiple, SensitiveData:S3Object/Personal