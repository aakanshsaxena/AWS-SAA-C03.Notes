
>[!note]- Post-Processing
>## BGP: A High-Level Overview for Solutions Architects
>
>This transcript provides a high-level explanation of Border Gateway Protocol (BGP), a routing protocol crucial for understanding how data flows across the internet. 
>
>**Key Insights:**
>
>* **BGP Basics:** BGP is a complex protocol used to exchange routing information between different networks, known as Autonomous Systems (AS). Each AS is a self-managing network controlled by a single entity and assigned a unique 16-bit number (ASN).
>* **Peering Relationships:** BGP relies on peering relationships between ASs to exchange routing information. These relationships are manually configured and allow ASs to learn about networks within each other's reach.
>* **Path Vector Protocol:** BGP is a path vector protocol, meaning it exchanges the best path to a destination network, not all possible paths. This "best path" is known as the AS path and includes the sequence of ASNs traversed to reach the destination.
>* **Reliability and Distribution:** BGP operates over TCP port 179, ensuring reliable communication through error correction and flow control. Its distributed nature allows for redundancy and fault tolerance.
>* **IBGP vs EBGP:**  
>    * **IBGP:** Focuses on routing within an AS.
>    * **EBGP:** Focuses on routing between ASs. AWS primarily uses EBGP.
>* **AWS Integration:** AWS products like Direct Connect and Dynamic VPNs utilize BGP for connectivity and routing between AWS services and on-premises networks.
>
>**Practical Implications for Solutions Architects:**
>
>* Understanding BGP fundamentals is essential for designing and managing hybrid architectures that integrate AWS with on-premises networks.
>*  Knowledge of peering relationships and AS paths is crucial for troubleshooting connectivity issues and optimizing network performance.
>*  Familiarity with IBGP and EBGP concepts helps in configuring and managing BGP connections within and between AWS environments.
>
>
>This high-level overview provides a foundation for further exploration of BGP and its intricacies.
>

>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**BGP (Border Gateway Protocol) Fundamentals:**
>
>* **Advertises Shortest Paths:** Autonomous systems (AS) advertise the shortest known path to a destination to their peering partners.
>* **Path Length is Key:** BGP prioritizes paths based on their length (number of hops). Shorter paths are preferred.
>* **Dynamic Routing:** BGP creates a dynamic and constantly evolving network topology as routes are learned and shared.
>
>**AS Path Prepending:**
>
>* **Influencing Path Selection:** Allows administrators to manipulate path length to influence route selection.
>* **Making a Path Appear Longer:**  Additional AS numbers are added to a path, artificially increasing its length.
>* **Example Use Case:**  Ensuring a slower, less preferred connection (e.g., satellite) is only used as a backup by making it appear longer than a faster connection (e.g., fiber).
>
>**Scenario:**
>
>* **Three Sites:** Brisbane, Alice Springs, Adelaide.
>* **Network Connectivity:** Direct satellite link between Brisbane and Alice Springs, fiber link between Alice Springs and Adelaide, and fiber link between Adelaide and Brisbane.
>* **Goal:** Prioritize the fiber link for traffic between Brisbane and Alice Springs.
>
>**Solution:**
>
>* **AS Path Prepending:** Alice Springs configures BGP to add extra AS numbers to the path towards Brisbane, making it appear longer.
>* **Result:** Brisbane learns a new, shorter path via Adelaide, ensuring traffic flows primarily over the fiber link.
>
>**Importance of BGP:**
>
>* **Large Enterprise Networks:** BGP is essential for routing traffic within and between large organizations.
>* **The Internet:**  BGP is the foundation of the internet's routing system.
>* **AWS Services:** BGP is used in Direct Connect and dynamic VPNs within AWS.
>
>
>
>Let me know if you have any other questions or need further clarification on any of these points.
>

- Autonomous System (AS) - Routers controlled by one entity, a network in BGP
- ASN are unique and allocated by IANA (0-65535), 64512-65534 are private
- BGP operates over tcp/179
- Not automatic, peering is manually configured
- BGP is a path vector protocol, it exchanges the best path to a destination between peers, the path is called the aspath
- iBGP = Internal BGP - routing within an AS
- eBGP = External BGP - routing between an AS

*What is BGP?*
- **BGP (Border Gateway Protocol)** is a dynamic routing protocol used to exchange routing information between different networks (autonomous systems).
- Instead of manually configuring static routes, BGP allows networks to automatically learn the best path to reach a destination.*
*Where BGP is used in AWS?*
1. **AWS Direct Connect (DX):**
    - When you establish a **Direct Connect private virtual interface (VIF)**, AWS uses BGP to advertise AWS VPC routes to your on-premises routers.        
    - Your on-premises router uses BGP to advertise your internal routes to AWS.       
2. **Site-to-Site VPN:**   
    - In **dynamic routing VPNs**, AWS uses BGP to automatically exchange routes between the Virtual Private Gateway (VGW) or Transit Gateway and your on-premises router/firewall.     
3. **Transit Gateway:** 
    - When connecting on-premises networks to a Transit Gateway over Direct Connect or VPN, BGP advertises routes dynamically.
*Why Use BGP in AWS?*
- **Automatic route updates:** When new subnets are added in AWS, they are automatically advertised.   
- **Redundancy and failover:** BGP can quickly reroute traffic if one connection (e.g., a VPN tunnel) fails.  
- **Scalability:** Avoids manual route configuration for large networks.
*Key Concepts in AWS BGP*
- **Autonomous System Number (ASN):**   
    - AWS uses an ASN (default 64512 for VGWs) to identify its network in BGP sessions.  
    - You can configure your on-premises ASN for your router.      
- **Prefixes (Routes):**
    - AWS advertises the CIDR blocks of your VPC via BGP.
    - Your router advertises your on-premises network CIDRs back to AWS.
- **MD5 Authentication:**
    - BGP sessions in AWS require an MD5 key (password) for security.
- **Keepalive & Hold Timers:**
    - AWS uses BGP timers to monitor session health.
![[Pasted image 20250726143454.png]]  


