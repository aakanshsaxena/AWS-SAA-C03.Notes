Considerations 
- What size should the VPC be (VPC CIDR)
- Are there any networks that we can't use
- Consider other VPC's, Cloud, On-premises, partners & vendors
- Try to predict the future (will this continue working in the future, VPC are hard to change)
- VPC Structure - Tiers & Resiliency Zones (AZs)
Our Scenario and Our VPC
- We have three major offices, one in London, one in New York, and one in Seattle. The on-premises IP address is 192.168.10.0/24. Our AWS Pilot IP address is 10.0.0.0/16, and our Azure Pilot is 172.31.0.0/16, So we need to avoid all three of these ranges.
IP Ranges to Avoid
-  We want to avoid the IP range **192.168.10.0/24**, **10.0.0.0/16**, which is AWS's VPC range, **172.31.0.0/16**, which is Azure's VPC range, **192.168.15.0/24**, which is our London office's IP range, **192.168.20.0/24**, which is our New York office's range, **192.168.25.0/24**, which is our Seattle office's IP address range. Our engineers do not know our specific GCP IP Address so we cannot use anything within **10.128.0.0/9**.
- As architects where possible we avoid using the default VPC, keep in mind that Azure is using our AWS default VPC CIDR Range
Our Plan
- VPC Minimum /28 (16 IP), maximum /16 (65536 IP)
- Personal Preference for 10.x.y.z range, we're going to use 10.16.y.z
- Avoid common ranges - logically 10.0 and 10.1, and up to and including 10.10
- Reserve 2+ networks per region being used per account
- Let's say for our purpose that 3 US, 1 Europe, 1 Australia (AZ-wise) x2 (2 networks per region) x4 (We have 4 AWS accounts) = (Ideally) 40 Ranges
- So in summary, we are going to start 10.16 range, and we can't use 10.128-10.255, so our possible range is 10.16-10.127