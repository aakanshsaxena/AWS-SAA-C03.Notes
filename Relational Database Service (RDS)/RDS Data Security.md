
>[!note]- Post-Processing
>## Key Insights and Information from the RDS Security Transcript:
>
>**1. Data Security Features in RDS:**
>
>* **Encryption in Transit:**
>    * Supported for all RDS engines.
>    * Uses SSL/TLS to encrypt data between client and RDS instance.
>    * Can be mandatory on a per-user basis.
>* **Encryption at Rest:**
>    * Supported using KMS and EBS encryption (default).
>    * Microsoft SQL and Oracle also support TDE (Transparent Data Encryption).
>    * RDS Oracle supports TDE using Cloud HSM for enhanced security and key control.
>
>**2. Encryption at Rest Mechanisms:**
>
>* **KMS-based Encryption:**
>    * RDS host uses customer master keys (CMKs) to generate data encryption keys (DEKs).
>    * Encryption handled by the host, not the database engine.
>    * Storage, logs, snapshots, and replicas encrypted using the same CMK.
>    * Encryption cannot be removed once added.
>* **TDE (Transparent Data Encryption):**
>    * Encryption handled within the database engine itself.
>    * Data encrypted and decrypted by the database engine, not the host.
>    * Reduces trust reliance on the host.
>    * RDS Oracle with Cloud HSM provides even stronger key controls with no AWS key exposure.
>
>**3. IAM Authentication for RDS:**
>
>* Allows IAM users and roles to authenticate to RDS using an authentication token instead of passwords.
>* Requires enabling IAM authentication on the RDS instance.
>* Policies map IAM identities to local RDS database users.
>* Authentication tokens have a 15-minute validity.
>* **Important Note:** IAM authentication is only for authentication, not authorization. Local database user permissions still control access to the RDS database.
>
>**4. Key Takeaways:**
>
>* RDS provides robust security features for both data in transit and at rest.
>* Choose the appropriate encryption method based on your security requirements and database engine.
>* Leverage IAM authentication for passwordless access to RDS, but remember it only handles authentication, not authorization.
>
>
>
>

- SSL/TLS (in transit) is available for RDS, can be mandatory
- RDS support EBS volume encryption using KMS
- Handled by Host/EBS
- AWS or Customer Managed CMK generates data keys
- Data keys used for encryption operations (storage, logs, snapshots, replicas) and encryption can't be removed
- RDS MSSQL and RDS Oracle Support TDE (Transparent Data Encryption) -> encryption handled within the DB engine
- RDS Oracle supports integration with CloudHSM
- Much stronger key controls (even from AWS)
Encryption & TDE
- With RDS Oracle - keys can be provided via CloudHSM - removing AWS from the chain of trust
- TDE is native DB Engine encryption. Data is encrypted before leaving the instance
- DEKs loaded onto hosts as required
- KMS provides AWS or Costumer Managed CMKs which are used to generate DEKs for RDS
- Snapshots of encrypted RDS instances are also encrypted with the same key
IAM Authentication
- We have a DB user (created on DB creation) and we configure to use AWS Auth Token
- Policy attached to users or role maps that IAM Identity onto the local RDS user, and we use generate-db-auth-token to create a token so a user can be authenticated to RDS