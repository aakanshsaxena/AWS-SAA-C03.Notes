
>[!note]- Post-Processing
>## Key Insights and Information about Route 53 Public Hosted Zones:
>
>**What are they?**
>
>* Public hosted zones are DNS databases hosted by Route 53 on public nameservers, accessible from the public internet and within AWS VPCs using the Route 53 resolver.
>* They are essentially zone files containing DNS records like A records, MX records, NS records, and text records.
>
>**How do they work?**
>
>1. **Creation:** When you create a public hosted zone, Route 53 allocates four public nameservers.
>2. **Integration:** You update the nameserver records for your domain to point to these four Route 53 nameservers, integrating it with the public DNS system.
>3. **Access:** 
>    * **Public Internet:** Users access the hosted zone through the public nameservers.
>    * **VPCs:** Instances within a VPC can access the hosted zone directly using the VPC resolver.
>4. **DNS Resolution:** DNS resolution follows a "walking the tree" process, starting from root servers, traversing through top-level domain servers, and finally reaching the Route 53 nameservers hosting the specific domain's zone file.
>
>**Key Features:**
>
>* **Globally Resilient:** Route 53's distributed nameservers ensure global availability even in case of regional outages.
>* **Flexible Hosting:** You can host zone files for domains registered elsewhere (e.g., GoDaddy, Hover) by utilizing Route 53's public nameservers.
>
>**Costs:**
>
>* Monthly fee for hosting the zone.
>* Small charge per query made against the zone.
>
>
>**In Summary:**
>
>Route 53 public hosted zones provide a reliable and flexible way to manage DNS for your domains, ensuring global accessibility and seamless integration with AWS VPCs.
>

- A R53 Hosted Zone is a DNS DB for a domain e.g. animals4life.org
- Globally resilient 
- Created with domain registration via R53, but can be created separately
- Hosts DNS Records (A, AAAA, MX, NS, TXT)
- Hosted zones are what the DNS system references 
- Authoritative for a domain
- DNS Database (zone file) hosted by R53 (public name servers)
- Accessible from the public internet and VPCs
- Hosted on 4 R53 name servers (NS) specific for the zone 
- Uses NS records to point at these NS (connect to Global DNS)
- Resource Records (RR) created within the host zone
- Externally registered domains can point at R53 Public Zone
Architecture
- Public Internet
	- Let's say someone queries for our site -> some ISP resolver will resolve to root servers which will go to the .org TLD servers which will recover the NS records for our domain (animals4life.org)
- VPC
	- VPC instances are already configured, if enabled, with the VPC+2 address as their DNS resolver which allows for querying of R53 public and internet hosted dns zones
- Public R53 hosted zone
	- www A 1.2.3.4
	- MX 10 someserver
	- MX 20 someserver
	- TXT "say something"
	- Contains resource records like this