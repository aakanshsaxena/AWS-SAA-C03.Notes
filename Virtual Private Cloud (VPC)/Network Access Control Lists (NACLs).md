>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**Network Access Control Lists (NACLs):**
>
>* **Function:** Act as traditional firewalls within AWS VPCs, filtering traffic at the subnet level.
>* **Association:** Each subnet has a dedicated NACL that controls traffic entering and leaving the subnet.
>* **Scope:** NACLs do **not** affect traffic between instances within the same subnet.
>* **Stateless:** NACLs do not track the state of connections (e.g., request/response). They only consider the direction of traffic.
>* **Rules:**
>    * **Inbound:** Control traffic entering the subnet.
>    * **Outbound:** Control traffic leaving the subnet.
>    * **Matching:** Rules are evaluated based on destination IP/range, destination port/range, and protocol.
>    * **Ordering:** Rules are processed sequentially. A deny rule before an allow rule will always block traffic.
>    * **Implicit Deny:** A catch-all rule (denoted by *) denies any traffic not explicitly allowed by other rules.
>    * **Explicit Allows and Denies:** NACLs use both explicit allows and denies for traffic control.
>
>**Stateless Firewall Implications:**
>
>* **Both Request and Response:**  Since NACLs are stateless, you need separate rules for both the request and the response of a communication.
>* **Example:**  For a web server receiving an HTTPS request, you need an inbound rule allowing traffic on TCP port 443 and an outbound rule allowing traffic on the ephemeral port range used by the client.
>
>**Security Considerations:**
>
>* **Rule Ordering:** Carefully consider the order of rules to ensure desired traffic is allowed while unwanted traffic is blocked.
>* **Implicit Deny:**  Be aware of the implicit deny rule and ensure all necessary traffic is explicitly allowed.
>
>
>
>This transcript provides a comprehensive overview of NACLs in AWS VPCs, covering their functionality, rules, and implications for security.
>
- NACLs contain rule grouped into inbound and outbound (inbound = entering the subnet, outbound = leaving the subnet)
- Every subnet has a NACL, connections within a subnet aren't impacted by NACLs
- NACLs filter traffic crossing the subnet boundary inbound or outbound
- Rules are processed in order, lowest rule number first. Once a match occurs, processing STOPS.
- \* is an implicit deny if nothing else matches
- Rules match the DST IP/Range, DST Port and Protocol and ALLOW or DENY based on that match

- Let's say we have a user Bob making a request to a web app using tcp/443. He gets the response through one of his machines ephemeral ports
- Keep in mind that NACLs are stateless, both the request and response parts of every comm. need individual rules
	- In terms of the web app, inbound rule would be rule #, Type (HTTPS (443)), Protocol (TCP (6)), Port Range (443), Source (0.0.0.0/0) -> Allow
	- Outbound would be rule #, Type (HTTPS (443)), Protocl (TCP (6)), Port Range (1024-65535), Source (0.0.0.0/0) -> Allow

>[!note]- AI Summary
>## Key Insights and Information from Network ACLs Transcript:
>
>**What are Network ACLs?**
>
>* Network Access Control Lists (NACLs) are stateless firewall rules that control traffic flow in and out of subnets within a VPC.
>
>**How do they work?**
>
>* **Stateless:** Treat each request and response as separate events, requiring both inbound and outbound rules for complete communication.
>* **Subnet-based:** Only affect traffic crossing subnet boundaries. Communication within the same subnet is unaffected.
>* **Explicit Allow/Deny:**  Can explicitly allow or deny traffic based on IP addresses, IP ranges, ports, and protocols.
>
>**Key Points:**
>
>* **Multi-Tiered Architectures:**  Increase complexity due to multiple subnet crossings. Each communication path (request and response) may require multiple rules across different NACLs.
>* **Software Updates:**  Require additional rules as they involve communication between servers across subnets.
>* **NAT:**  May necessitate additional rules due to the nature of NAT operations.
>
>**Default vs. Custom NACLs:**
>
>* **Default NACL:**  Created with each VPC, has a "catch-all allow" rule, effectively allowing all traffic by default.
>* **Custom NACL:**  Created separately, initially has only a "default deny" rule.  Associating it with a subnet will block all traffic unless explicitly allowed.
>
>**Best Practices:**
>
>* **Security Groups:**  AWS prefers using security groups for allowing traffic, while NACLs are used for explicitly denying traffic.
>* **Combined Approach:**  Use both security groups and NACLs for comprehensive security.
>
>**Limitations:**
>
>* **Stateless:**  Cannot track session states.
>* **No Logical Resource References:**  Only work with IP addresses, ranges, ports, and protocols. Cannot reference AWS resources directly.
>
>
>**Overall:**
>
>Network ACLs are a powerful tool for controlling traffic flow within a VPC. Understanding their limitations and best practices is crucial for effective network security.
>

Summary 
- NACLs are stateless - request and response are seen as different
- Only impacts data crossing subnet boundary
- NACLs can explicitly allow and deny
- Only have access to IPs/CIDR, Ports & Protocols - no logical resources
- Cannot be assigned to AWS resources - only subnets
- Use together with security groups to add explicit DENY (Bad IPs/Nets)
- Each subnet can have one NACL, but one NACL can be associated with many subnets




