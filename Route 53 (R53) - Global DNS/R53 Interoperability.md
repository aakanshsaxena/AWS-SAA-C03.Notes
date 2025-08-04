
>[!note]- Post-Processing
>## Route 53 Interoperability: Key Insights
>
>This video explains how Route 53 can be used for both domain registration (registrar) and domain hosting, but also how it can be used in conjunction with other providers for these functions. 
>
>**Here are the key takeaways:**
>
>* **Route 53 offers two distinct services:**
>    * **Registrar:** Registers your domain name with the appropriate top-level domain (TLD) registry.
>    * **Domain Hosting:** Manages the DNS records and name servers for your domain.
>* **Traditional Architecture:** Route 53 handles both registrar and hosting functions. This is the default configuration when registering a domain with Route 53.
>* **Registrar Only:** Route 53 registers the domain but a different provider (e.g., Hover) handles hosting. This is less common as it loses the benefits of Route 53's hosting features.
>* **Hosting Only:** Route 53 hosts the domain while a different provider (e.g., Hover) handles registration. This is useful for existing domains or when leveraging specific registrar deals.
>* **Understanding the difference between registrar and hosting is crucial** for configuring and troubleshooting DNS setups.
>
>**Additional points:**
>
>*  Route 53 is generally considered a good DNS provider.
>*  The video encourages viewers to explore different architectures and understand how they work.
>
>
>This information should help you understand how Route 53 can be used in various scenarios and make informed decisions about your domain management.
>

- R53 normally has two jobs, domain registrar and domain hosting and it can perform both of these jobs or only perform one of them
- R53 accepts your money (domain registration fee), and then allocates 4 name servers and creates a zone file on the name servers (domain hosting) for a monthly fee, it then communicates with the registry of the top level directory to set the NS records for the domain to point at the 4 NS above (domain registrar)
Both Roles
- You register a domain and pay the yearly fee, R53 domain registrar liaises with R53 domain hosting create public hosted zone -> creates the zone file and four NS for monthly fee and returns this to the registrar
- Registrar gives this information, registration fee, and domain name to the TLD and entry is added in TLD, using NS delegation pointing at our four name servers
Registrar Only
- We pay the domain yearly fee and then provide this domain to an external platform that creates the name servers, zone file for us in hosted zone.
- We give the TLD the registration fee, domain name, and 4 external NS and this entry is added to TLD using NS delegation records pointing at 4 NS
- Normally not common, domain hosting is the most valuable part of R53
Hosting Only
- We give R53 the domain and it creates the public hosted zone for the domain -> name servers, zone file. 
- We give this info back to our 3rd party domain registrar, and it gives it to the TLD and entry is added into the TLD using NS delegation records to point at our four name servers
- More common: might be used if we owned the domain from before, or if we have an agreement to buy domains from a 3rd party
- Makes use of R53 important part which is the domain hosting
