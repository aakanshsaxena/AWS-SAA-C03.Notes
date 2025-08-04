>[!note]- AI
> #### Resilience Architecture Details
> - Use two geographically spread buildings for resilience
> - Two different Direct Connect locations added for redundancy
> - Provision one DX4 per DX location cross connected to customer routers
> - Each DX4 extends to different customer routers in separate premises
> - Two DX locations improve resilience over previous architecture
> #### Resilience Architecture Details Continued
> - Architecture tolerates failure of one location and continues operating
> - Architecture tolerates customer hardware and location failures too
> - Outage risk only if entire location and remaining hardware fail
> - Solution continues running despite hardware or entire DX location failure
> - Solution maintains connectivity despite failure of DX location and customer premises
> - Connectivity only interrupted if both DX locations and hardware fail simultaneously
> #### Extreme Resilience Architecture
> - Question raised about connectivity interruption under multiple failures
> - Architecture can be enhanced for extreme resilience levels
> - Next design offers maximum resilience with AWS region included
> - Two DX locations are positioned centrally in the architecture
> - AWS west region, two DX locations, and two customer premises included
> #### Extreme Resilience Architecture Details
> - Each DX location has two DX ports on separate equipment
> - Each DX location has two customer DT routers for added resilience
> - Two customer DX routers per location enhance hardware and location failure resilience
> - Architecture includes dual cross connects between AWS and customer routers
> - High availability ensured from direct connect location perspective
> #### Resilience and Connectivity Details
> - Connectivity remains active despite failure due to dual infrastructure
> - High availability maintained even if one DX location fails
> - Connectivity remains fine even if one DX location fails
> - Extensions follow two separate physical routes for added resilience
> - Separate routing applies to both DX locations and customer premises
> #### Network Architecture and Resilience
> - Extensions follow two separate physical routes for added resilience
> - Extensions connect different physical buildings for high availability
> - Multiple customer routers used for high availability inside premises
> - Network architecture is complex but important for exams
> - Key takeaway for exams and real-world Direct Connect use
> #### Direct Connect Resilience Strategies
> - Direct Connect is physical and not inherently resilient
> - Single Direct Connect is a single point of failure at each step
> - Highly available Direct Connect requires resilient multi-route solutions
> - Site-to-site VPN can back up Direct Connect
> - Lesson theory and architecture discussion concluded
> - Site-to-site VPN can back up Direct Connect for resilience
> - Highly available Direct Connect requires multi-route architectures

- DX by default has no resilience
- AWS regions typically have multiple DX locations which are normally major metro DC's
- DX locations are connected to the AWS region via redundant high speed connection
- We connect using a single cross-connect from a DX port with a customer/provider router
- Then the DX is physically extended from the DX location to our customer premises.
- Single Points of Failure (DX Location, DX Router, Cross Connect, Customer DX Router, Extension, Customer Premises, Customer Router)
- We can make this OK by having multiple DX cross-connects and multiple customer premises router
	- We still have a SPOF at DX Location as a whole, customer premises as a whole, and potentially extension link path (telco might use the same cable path between the DX location and our premises)
- We can make this BETTER by using two DX locations and two customer premises, but if an entire location fails, a router in the other location fails, or corresponding customer premises fails then we will operate at a reduced resiliency level
- We can make it GREAT by combining OK and BETTER, by having two DX cross-connects per location, having 2 different DX locations, two different customer premises, and two different customer routers. We are now HA at every stage -> HA in general.