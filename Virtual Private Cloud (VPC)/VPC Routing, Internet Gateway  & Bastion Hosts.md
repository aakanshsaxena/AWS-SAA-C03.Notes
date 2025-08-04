VPC Router
- Every VPC has a VPC Router - the VPC Router is HA
- In every subnet it is allocated as the 'network+1' address
- It routes traffic between subnets
- Controlled by 'route tables' - each subnet has one
- A VPC has a Main route table which is the subnet default
Route Tables
- Look at the source, and the destination and decides where to send (target) based on what traffic the data matches and what route to take (propogated)
- Destination can be 1 IP address, or a range (like the whole CIDR range), or the default fall back of 0.0.0.0/0
- Higher prefix = more specific = higher priority
Internet Gateway (IGW)
- Regionally resilient gateway that's attached to a single VPC
- 1 VPC = 0 or 1 IGW, 1 IGW = 0 or 1 VPC
- Runs from within the AWS Public Zone
- Gateways traffic between the VPC and the Internet/AWS Public Zone (in case of services like S3, SQS, SNS)
- Managed by AWS
Using an IGW
- Create IGW
- Attach IGW to VPC
- Create Custom RT
- Associate RT
- Set Default Routes to IGW
- Subnet allocate IPv4
IPv4 Addresses with an IGW
- We have an IPv4 Instance (Private IPv4 - 10.16.16.20), an IGW (that has a copy of the instance private address and also stores the public IPv4 address of the instance), and a Linux Update Server (1.3.3.7)
- When the instance sends a packet, the source is considered as its private IP address and sent to the IGW, the IGW recognizes the instance has a public IP address and sends it to the update server using this public IP
- Flipside, the update server sends the file to the instance public IP address which is really just the IGW, IGW changes the address from this public address to the original IP address of the instance by translating the public to private IP.
- The IPv4 instance never knows its own public IP, there is no space in the OS to configure this **MIGHT BE a trick question on the exam**
- For IPv6, all IP addresses used are natively, publicly routable. In this case the IGW does not do any sort of translation.
Bastion Hosts
- Bastion Host is the same thing as a Jumpbox
- An instance in a public subnet
- Incoming management connections arrive there, and is often the only way IN to a VPC to access internal VPC Resources
- Inbound management points that you can configure for security purposes (eg. only accept connections from certain IP addresses, auth with SSH, or integrate w/ on-premises identity server)
