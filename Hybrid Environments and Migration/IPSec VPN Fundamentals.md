
>[!note]- Post-Processing
>## IPsec Fundamentals: Key Insights and Information
>
>This transcript provides a comprehensive overview of IPsec, covering its purpose, architecture, and key phases. Here's a breakdown of the key insights and information:
>
>**What is IPsec?**
>
>* IPsec is a suite of protocols designed to establish secure networking tunnels across insecure networks (like the public internet).
>* It enables secure communication between networks or devices, ensuring data confidentiality and integrity.
>
>**Why is IPsec important?**
>
>* **Authentication:** Verifies the identity of communicating peers, preventing unauthorized access.
>* **Encryption:** Protects data transmitted over the tunnel, making it unreadable to unauthorized parties.
>* **Data Integrity:** Ensures data remains unaltered during transit, preventing tampering.
>
>**How does IPsec work?**
>
>* **IPsec VPNs:** Utilize the concept of "interesting traffic" - data matching specific rules (e.g., network prefixes) that gets routed through a secure tunnel.
>* **Tunnel Establishment:** Tunnels are dynamically created when "interesting traffic" is detected and torn down when no longer needed, optimizing resource utilization.
>* **Two-Phase Process:**
>
>    * **IKE Phase 1 (Authentication and Key Exchange):**
>        * Establishes a secure connection between peers using certificates or pre-shared keys.
>        * Employs Diffie-Hellman key exchange to securely generate a shared symmetric key.
>        * Results in a Phase 1 tunnel (IKE Security Association) for subsequent communication.
>    * **IKE Phase 2 (Tunnel Configuration and Data Encryption):**
>        * Uses the shared symmetric key from Phase 1 to negotiate encryption methods and establish a data transfer tunnel (IPsec Security Association).
>        * Both peers agree on a specific cipher suite for efficient and secure data transfer.
>
>**Types of VPNs:**
>
>* **Policy-Based VPNs:** Route traffic based on predefined policies (e.g., network addresses, applications).
>* **Route-Based VPNs:** Utilize static routes to determine traffic flow.
>
>**Overall, the transcript emphasizes the importance of IPsec in securing network communications, explaining its two-phase process, and highlighting the key concepts of authentication, encryption, and tunnel establishment.**
>

>[!note]- Post-Processing
>## Key Insights and Information from VPN Transcript:
>
>**1. Types of VPNs:**
>
>* **Policy-based VPNs:**
>    * Use rules to match traffic and determine which security association (SA) pair to use.
>    * Allow for different security settings for different types of traffic, suitable for rigorous security environments.
>    * More complex to configure.
>* **Route-based VPNs:**
>    * Match traffic based on network prefixes (e.g., 192.168.0.0/24).
>    * Use a single SA pair for each network prefix, simplifying setup but limiting flexibility.
>
>**2. VPN Architecture:**
>
>* **Phase 1:** Establishes the initial tunnel using a phase one tunnel key.
>* **Phase 2:**  
>    * **Route-based VPN:** Uses a single SA pair per network prefix within a single tunnel.
>    * **Policy-based VPN:** Uses unique SA pairs with different IPsec keys for each policy match, allowing for granular security control.
>
>**3. Key Differences:**
>
>* **Traffic Matching:** Policy-based VPNs use rules, while route-based VPNs use network prefixes.
>* **Security Flexibility:** Policy-based VPNs offer more granular control over security settings for different traffic types.
>* **Complexity:** Route-based VPNs are simpler to configure than policy-based VPNs.
>
>**4. Practical Applications:**
>
>* The transcript emphasizes the importance of understanding VPN types for implementing secure network architectures.
>* It suggests learning how to utilize VPNs within specific product sets for practical application.
>
>
>
>**Overall, the transcript provides a concise overview of VPN types, their architectures, and key differences. It highlights the trade-offs between security flexibility and complexity, emphasizing the need for choosing the appropriate VPN type based on specific security requirements.**
>

- IPSEC is a group of protocols that sets up secure tunnels across insecure networks
- Between two peers (local and a remote peer)
- Provides authentication and encryption
Architecture
- On a global scale, we have one business site that wants to create IPSec Tunnels between two other business sites. The data inside these tunnels is encrypted (secure connection over an insecure network)
- Reminder: symmetric encryption is fast but its challenging to exchange keys securely, while asymmetric encryption is slow but you can easily exchange public keys
IPSec Phases
- We have two main phases
- IKE Phase 1 (Slow and Heavy)
	- Authenticate - PSK/Certificate
	- Using asymmetric encryption to agree on and create a shared symmetric key
	- IKE SA created (phase 1 tunnel)
- IKE Phase 2 (Fast and Agile)
	- Uses the keys agreed in phase 1
	- Agree encryption method and keys used for bulk data transfer
	- Create IPSEC SA -> phase 2 tunnel which is architecturally running over phase 1
IKE Phase 1 Detailed
![[Pasted image 20250726144959.png]]
- Important things to remember here: we use Diffie Hellman private keys, then generate the same shared DH key from our private key and the other sides public key
- Using this new DH Key, which is shared but has not been sent over network (therefore shared securely), we exchange key material and agreements and generate a symmetrical key from our DH key + exchanged material
IKE Phase 2 Detailed
![[Pasted image 20250726145152.png]]
- We use the symmetrical key to encrypt and decrypt agreements and pass in more material
- The DH Key and Exchanged Key Material is used to make a symmetrical IPSEC Key that is used for bulk encryption and decryption of interesting traffic (*"interesting traffic" refers to the specific data packets that are designated to be encrypted and routed through the VPN tunnel*)
Fundamentals Cont.
- Two types of VPN
	- Policy-based VPN
		- Rule sets match traffic a pair of SAs
		- Different rule and security settings
	- Route based VPN
		- Target matching (prefix)
- Route-based is more rigid because it only uses a single SA pair and a single IPSEC Key, which means we can only really have one security group
- Policy-based is much more flexible and we can have multiple "areas", because each policy has its own SA pair and unique IPSEC Key
![[Pasted image 20250726145521.png]]
- As you can see here, using policy-based VPN we have it separated for servers, CCTV, and financial, while route-based only has one.