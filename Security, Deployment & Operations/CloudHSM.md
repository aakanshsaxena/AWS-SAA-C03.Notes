> [!note]- AI
> #### CloudHSM Architecture and Deployment
> - **Managed VPC:** AWS CloudHSM is deployed in a dedicated, AWS-managed VPC that is separate from your own. This VPC is configured across two or more Availability Zones (AZs) to ensure high availability and redundancy.
> - **Clustering:** HSMs are deployed as a cluster, automatically replicating keys and policies across devices. This cluster-based architecture ensures that if one HSM fails, another can take over, providing seamless operation.
> - **Network Integration:** The HSM cluster is made accessible to your applications via **Elastic Network Interfaces (ENIs)** that are injected directly into your VPC. This allows resources like EC2 instances to communicate with the HSMs over your private network.
> - **Client-Side Access:** To interact with the HSMs, you must install the **CloudHSM client software** on your EC2 instances. This client uses industry-standard cryptographic APIs like **PKCS#11**, Java Cryptography Extensions (JCE), and Microsoft CryptoNG (CNG).
> #### Key Control and Security
> - **Exclusive Key Ownership:** A key differentiator of CloudHSM is that you, the customer, have exclusive, single-tenant control over your encryption keys. AWS has no access to your keys and no visibility into the cryptographic operations you perform.
> - **Tamper-Resistant Hardware:** CloudHSM devices are dedicated, tamper-resistant hardware appliances that are **FIPS 140-2 Level 3** compliant. This is the highest level of FIPS compliance in the AWS cloud and is often a requirement for specific regulatory frameworks like PCI DSS.
> - **Separation of Duties:** AWS manages the underlying hardware, firmware updates, and infrastructure maintenance. However, you are responsible for managing the keys and user accounts within the secure cryptographic boundary of the HSMs themselves.
> #### Use Cases and Differentiators vs. KMS
> - **When to use CloudHSM:**
>     - **Strict Compliance:** When your compliance requirements (e.g., PCI DSS, FIPS 140-2 Level 3) mandate that you have exclusive control over your keys and a dedicated hardware device.
>     - **Third-Party Applications:** When you need to integrate with applications that require direct access to a hardware security module via industry-standard APIs like PKCS#11 (e.g., for Transparent Data Encryption (TDE) with Oracle DB or for signing certificates with a custom CA).
>     - **Cryptographic Offloading:** For high-performance workloads that benefit from offloading cryptographic operations like SSL/TLS processing to dedicated hardware.
> - **When to use KMS:**
>     - AWS Key Management Service (KMS) is the default choice for most use cases in AWS. It provides a more user-friendly, deeply integrated service for managing keys for AWS services like S3, EBS, and RDS.
>     - With KMS, AWS manages the underlying HSMs on your behalf. KMS is typically FIPS 140-2 Level 2 compliant, which is sufficient for most applications. You control key access via IAM, but you don't have the same level of direct control over the hardware as with CloudHSM.
> - **Summary:** CloudHSM is for specific, high-compliance and custom integration scenarios, while KMS is for general-purpose key management that is seamlessly integrated with the AWS ecosystem.

- True "Single Tenant" Hardware Security Module (HSM)
- AWS provisioned, fully customer managed
- Fully FIPS 140-2 Level 3 (KMS is L2)
- Uses Industry Standard APIs - PKCS#11, Java Cryptography Extensions (JCE), Microsoft CryptoNG (CNG) Libraries
- KMS can use CloudHSM as a custom key store, CloudHSM integration with KMS
Architecture
- An ENI is created for each HSM in the AZ
- HSM are created in a separate VPC that we cannot access that is AWS managed HSM VPC
- Interfaces are added to our VPC, and the HSM that is provisioned by AWS are not accessible by AWS
- HSMs keep keys and policies in sync when nodes are added or removed
CloudHSM Use Cases
- No Native AWS integration, no S3 SSE
- Offload the SSL/TLS Processing for Web Servers
- Enable Transparent Data Encryption (TDE) for Oracle DB
- Protect the Private Keys for an Issuing Certificate Authority (CA)