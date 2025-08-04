### Nameserver (NS)
- Nameservers are _part_ of the DNS that stores your domain information and makes it accessible on the internet.
### A and AAAA Records
- Host to IP
- A - maps the host to an IPv4
- AAAA - maps the host to an IPv6
- You create two records with the same name, one A record one AAAA record
### CNAME Records
- Lets you create the equivalent of DNS shortcuts = host to host records
- Reduce admin overhead
- Example: given server performs multiple tasks. Create three cnmaes (CNAME ftp CNAME mail CNAME www and pointing them all at the A server record which links to IPv4 address. This way if IPv4 changes, we also need to change A Server record)
- Cannot point directly at IP addresses only at other names
### MX Records
- How the server can find the mail server (SMTP) for a domain
- Example: want to send an email to hi@google.com
- Start with google.com zone, you have an A record called (anything but lets say) mail pointing to an IP Address
- Zone also contains various MX records, in this case MX 10 mail, MX 20 mail.other.domain.
- MX Records have two parts: value, and a priority.
- Value = just a host which we can tell because there's no dot to the right = part of the same zone it's located in. So MX 10 mail is mail.google.com
- If we include a dot then it's a fully qualified domain name which means it can either point to the host inside the same zone or outside the zone.
- How does this work?
- If we're sending an email to hi@google.com, we focus on the domain name (google.com) and then the email server does an MX query using DNS for google.com
- Priority field -> lower values = higher priority when performing an MX query
- So in our example, MX query would first look at mail (because priority is 10<20), and only if this wasn't functional would it look at mail.other.domain.
### TXT Records
- Allow you to add arbitrary text to a domain
- One common use is to prove domain ownership
- For example, let's say we want to add an email system to our domain.
	- That system might tell us to add a random piece of text data to our domain to prove ownership (TXT Records)
	- Then the email system queries TXT to validate ownership
- Other uses: fight spam (add certain info to domain indicating which entities are authorized to communicate with server)
### Time To Live (TTL)
- Example: Client wants to connect to amazon.com
	- Queries DNS using a resolver server hosted at its ISP
	- Resolver talks to DNS root which points at the .com registry authoritative servers
	- These servers provide the nameservers at the amazon.com zone, which is authoritative for amazon.com zone, which has a record for www.
	- Uses this record to get IP address. Getting the result from authoritative source = authoritative answer 
	- TTL values indicate how long records can be cached for
	- Thus results of this query will be cached at resolver server for TTL time, which would give you a non-authoritative and immediate answer
	- 