
>[!note]- Post-Processing
>##  EBS Encryption: Key Insights from the Transcript
>
>This transcript provides a comprehensive overview of EBS encryption, a crucial concept for AWS users and exam preparation. Here are the key takeaways:
>
>**What is EBS Encryption?**
>
>* EBS encryption provides **at-rest encryption** for both EBS volumes and snapshots.
>* It protects your data by encrypting it on the physical storage devices where the volumes reside.
>
>**How Does it Work?**
>
>* **KMS (Key Management Service):** EBS encryption relies on KMS to generate and manage encryption keys.
>* **Data Encryption Key (DEK):** For each encrypted volume, a unique DEK is generated using a KMS key. This DEK is stored with the volume on the raw storage.
>* **Decryption in Memory:** When an instance uses an encrypted volume, the DEK is decrypted by KMS and loaded into the instance's memory. The instance uses this decrypted key to encrypt and decrypt data between itself and the volume.
>
>**Important Points to Remember:**
>
>* **Default Encryption:** AWS accounts can be configured to encrypt EBS volumes by default.
>* **Unique DEKs:** Each new volume created from scratch uses a unique DEK. Snapshots and volumes created from snapshots use the same DEK as the original volume.
>* **Irreversible Encryption:** Once a volume or snapshot is encrypted, it cannot be decrypted.
>* **OS Unaware:** The operating system is unaware of the encryption. It sees plain text data because the encryption happens between the EC2 host and the EBS system.
>* **Software Disk Encryption:** For operating system-level encryption, you need to configure software disk encryption within the OS itself.
>* **Benefits:** EBS encryption is efficient, cost-effective, and doesn't impact performance.
>
>**Exam Tips:**
>
>* Be prepared for curveball questions about encryption.
>* Understand the role of KMS and DEKs in EBS encryption.
>* Know the implications of creating snapshots and new volumes from encrypted sources.
>* Remember that encryption is irreversible.
>
>
>
>By understanding these key insights, you can confidently navigate EBS encryption and ace your AWS exams.
>

- We use KMS to encrypt any data on an EBS volume
- KMS using the GenerateDataKeyWithoutPlaintext API to create a DEK, that it uses to encrypt the EBS volume
	- Any snapshots, or volumes made down the line using snapshots are all encrypted with the same DEK
- At rest (in EBS), data is stored in ciphertext, the EC2 host decrypts and then gives the plaintext data to the EC2 instance, and vice versa.
**Exam Powerups**
- Accounts can be set to encrypt by default with the default KMS key
- Otherwise choose a KMS key to use everytime
- Each volume uses 1 unique DEK, snapshots + future volumes use the same DEK though
- Can't change a volume to NOT be encrypted
- OS isn't aware of the encryption (it receives everything as plaintext from the EC2 Host)
- No performance loss and cost -> basically no reason to not have EBS encryption enabled