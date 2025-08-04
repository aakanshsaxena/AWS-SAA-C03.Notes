 - AWS managed DNS product
 - Two main services: register domains, host zone files for you on managed nameservers
 - Global Service - single database
 - Globally Resilient
 - DNS Zones - Database which store your DNS records
### Register Domains
 - Has relationships with all major domain registries
 - IANA manages the root zone for DNS, each registry manages a zone (.com zone, .io zone, .net zone, etc)
 - Route53 checks with registry to see if domain is available -> R53 creates a zone file for the domain being registered (contains all DNS info for particular domain), also allocates name service for this zone -> generally four per zone -> takes zone file (hosted zone) and puts it onto four managed name servers -> adds name server records into the zone file for top level domain 
 - Name server records - how PIR (.org registry) delegates admin of the domain tools
 - creating a zone file -> creating number of managed name servers -> putting zone file on those servers -> liaising with the registry for top level domain -> getting name server records added to the top level domain zone
### Hosted Zones
- Zone files in AWS
- Hosted on four managed (AWS) name servers
- When a hosted zone created, number of servers created and allocated to the domain
- Hosted zone can be public
- Hosted zone could also be private (linked to VPCs)
- Hosted zone hosts DNS records (recordsets)