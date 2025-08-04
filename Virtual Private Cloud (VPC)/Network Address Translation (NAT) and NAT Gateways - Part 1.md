>[!note]- Post-Processing
>## Key Insights and Information from the NAT Gateway Explanation:
>
>**What is NAT?**
>
>* **Network Address Translation (NAT)** is a process that changes the IP addresses of network packets.
>* It can modify source or destination IP addresses.
>* **Static NAT:** One-to-one mapping between a private IP and a public IP. Used by the Internet Gateway to allocate public IP addresses to resources.
>* **IP Masquerading (NAT):** Many private IPs share a single public IP. Popular due to the limited availability of public IP addresses.
>
>**How NAT Works:**
>
>1. **Private instances send data:** Packets originate from private IPs within a VPC.
>2. **Traffic routed to NAT Gateway:**  A default route in the private subnet's route table directs traffic to the NAT Gateway in a public subnet.
>3. **NAT Gateway records information:** It stores details about the communication (source IP, destination IP, port numbers) in a translation table.
>4. **Source IP address changed:** The NAT Gateway modifies the packet's source IP to its own public IP address.
>5. **Traffic sent to Internet Gateway:**  The NAT Gateway forwards the packet to the Internet Gateway.
>6. **Internet Gateway translates to public IP:** The Internet Gateway uses the NAT Gateway's public IP to send the packet to the intended destination on the public internet.
>7. **Response traffic returns:**  The response packet is received by the NAT Gateway, which uses its translation table to identify the original private instance and forwards the data accordingly.
>
>**Key Points:**
>
>* NAT allows private instances to access the public internet and AWS services.
>* Incoming connections to private IPs are not possible with NAT.
>* **Internet Gateway:** Allocates public IP addresses and translates NAT Gateway's IP to a real public IP.
>* **NAT Gateway:** Provides many-to-one IP translation, allowing multiple private IPs to share a public IP.
>
>**Next Steps:**
>
>* The lesson will demonstrate how to implement a NAT Gateway in a VPC.
>
>
>
>This summary provides a concise overview of the key concepts and functionalities of NAT Gateway as explained in the transcript.
>

What is NAT?
- Network Address Translation
- A set of processes to remap SRC or DST IPs
- Internet Gateway is a form of NAT (Static)
- NAT Gateway provides **IP Masquerading** - hiding CIDR blocks behind one public facing IPv4 address
- Gives private CIDR ranges outgoing ONLY internet access

NAT Architecture 
- Let's say we have four private instances (in the APP tier) and our web tier and then our VPC router and an internet gateway. If we want to send traffic publicly from the private instances, first we would sent the data to the NAT (keep in mind the NAT can IP masquerade multiple sources into one public IP)
- Then the default route table since we want the data going out would redirect the data to the VPC Router which would send it to the internet gateway.
- If you need to give an instance its on IPv4 public address only internet gateway is required
- If you want to give private instances access to the internet and the AWS public zone services like S3, then you need a NAT gateway + internet gateway

Important Notes
- Runs from a public subnet 
- Uses Elastic IPs (Static Public IPv4)
- AZ Resilient Service NOT Regionally Resilient like IGW
- For regional resilience - NATGW in each AZ
- Route Table in for each AZ with that NATGW as a target
- Managed, scales to 45 Gbps, charged for hourly duration of use & data volume

