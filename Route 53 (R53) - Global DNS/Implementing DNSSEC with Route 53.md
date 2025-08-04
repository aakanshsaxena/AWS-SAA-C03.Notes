
>[!note]- Post-Processing
>## Key Insights and Information from the DNSSEC with Route 53 Transcript:
>
>**Understanding DNSSEC:**
>
>* DNSSEC (Domain Name System Security Extensions) is a protocol that adds security to the DNS system, ensuring the authenticity and integrity of DNS data.
>
>**Route 53 Implementation:**
>
>* Enabling DNSSEC on a Route 53 hosted zone is done through the Route 53 console UI or CLI.
>* The process involves using AWS Key Management Service (KMS) to create an asymmetric key pair (public and private).
>* Route 53 internally creates zone signing keys and adds the public parts of these keys to DNSKEY records within the hosted zone.
>* The private key signing key is used to sign the DNSKEY records, creating RRSIG records for verification.
>
>**Chain of Trust:**
>
>* Route 53 establishes a chain of trust with the parent zone (e.g., .org) by adding a DS record (Delegated Signer record) to the parent zone.
>* This DS record contains a hash of the public key signing key for the child zone.
>
>**Key Points:**
>
>* KMS keys used for DNSSEC must be in the US East 1 region.
>* Route 53 manages the creation and management of zone signing keys internally.
>* Configure CloudWatch alarms for DNSSEC internal failures and key-signing key hatching to monitor for issues.
>* Consider enabling DNSSEC validation for VPCs to ensure only trusted DNS records are returned.
>
>**Next Steps:**
>
>* The transcript proceeds to a live demonstration of implementing DNSSEC for a hosted zone in the AWS console.
>
>
>
>Let me know if you have any other questions.
>

- DNSSEC adds **digital signatures** to DNS records, so resolvers (like your browser or ISP) can **verify that the DNS response is legit** and came from the actual domain owner.
- The only change for the user is that they first go to a DNSSEC Resolver before going to the root servers in their request 
- For us:
	- Create the public key and private key which are asymmetric with KMS (can think of as KSK but in reality the KSK is created from these)
	- Zone signing key is created and rotated internally by R53
	- R53 adds KSK and ZSK public parts into a DNSKEY record into public zone, tells DNSKEY Resolvers which keys to use to verify signatures on any other records in this zone
	- Private KSK is used to sign those records -> creates the RRSIG DNSKEY
	- Next R53 has to establish a chain of trust with parent zone -> parent zone needs to add a Delegated Signer record which is a hash of the public part of the KSK for this zone
- Make sure to configure CloudWatch alarms for DNSSECInternalFailure and DNSSECKeySigningKeysNeedingAction
