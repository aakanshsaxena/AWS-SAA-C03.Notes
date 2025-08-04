> [!note]- AI
> #### Lower-Layer Firewall Limitations
> - **Stateful Inspection:** Traditional firewalls typically operate at Layers 3 and 4 of the OSI model. This means they can inspect network traffic based on IP addresses, port numbers, and TCP/UDP protocol flags.
> - **Session-Aware:** These firewalls are often "stateful," meaning they can track the state of a session. They know the difference between traffic initiating a connection and return traffic. This allows for a simplified security policy with a single rule that permits an outbound connection, and the firewall will automatically allow the corresponding inbound response traffic.
> - **Lack of Context:** A key limitation is that they do not understand the content or context of the data within the packets. They cannot inspect encrypted traffic and cannot distinguish between normal and malicious traffic at the application layer. For example, they can allow all traffic on port 80 (HTTP) but can't block a SQL injection attack sent over that port.
> #### Layer 7 (Application-Layer) Firewalls
> - **Deep Packet Inspection:** Layer 7 firewalls (also known as Application Firewalls or Next-Generation Firewalls) overcome the limitations of lower-layer firewalls by inspecting traffic at the application layer. This allows them to understand specific application protocols like HTTP, FTP, DNS, and SMTP.
> - **HTTPS Handling:** To inspect encrypted traffic, a Layer 7 firewall acts as a man-in-the-middle proxy. It terminates the HTTPS connection from the client, decrypts the traffic, inspects the plain-text HTTP content, and then creates a new, re-encrypted HTTPS connection to the backend server.
> - **Granular Control:** By understanding the application protocols, Layer 7 firewalls can apply granular rules based on the content of the data. This enables them to:
>     - Block specific applications (e.g., Facebook, Dropbox).
>     - Filter specific content, such as blocking malware, spam, or sensitive data from being uploaded.
>     - Enforce protocol compliance and block malicious activity like SQL injection or cross-site scripting (XSS) attempts.
> #### Features and AWS Services
> - **Comprehensive Security:** A Layer 7 firewall retains all the capabilities of a Layer 3/4 firewall, including session tracking and IP/port filtering. It adds a new layer of security by providing context-aware and content-based controls.
> - **AWS Implementation:** AWS offers services that function as Layer 7 firewalls to protect your applications and services. The primary example is **AWS WAF (Web Application Firewall)**, which can be deployed in front of resources like Application Load Balancers, Amazon API Gateway, and Amazon CloudFront to protect against common web exploits and bots.

- Layer 7 firewalls are aware of the Layer 7 protocol (like HTTP)
- L7 FW can identify normal or abnormal requests protocol specific attacks
- The encryption of HTTPS is decrypted on the L7 firewall allowing us to inspect and block, replace, or tag the data 
- We can also identify, block and adjust specific applications like FB
- A new encrypted L7 connection is created by the firewall between it and the backend
- L7 FW keeps all L3, L4, L5 features but can react to L7 elements (DNS, RATE, Content, Headers)