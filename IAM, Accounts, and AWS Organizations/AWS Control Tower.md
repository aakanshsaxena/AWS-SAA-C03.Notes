- Quick and easy setup of multi-account environment
- Orchestrates other AWS services to provide this functionality
	- Organizations, IAM Identity Center, CloudFormation, Config,...
- **Landing Zone** - multi-account environment (what control tower builds on)
	- Contains SSO/ID Federation, Centralized logging + auditing
- **Guard Rails** - Detect/mandate rules and standards across all accounts
- **Account Factory** - Automates and standardizes new account creation
- **Dashboard** - single page oversight of the entire environment
**Landing Zone**
- Allows anyone to create well architected multi-account environment in the home region
- Built with various AWS services
- Two OU's - security OU (Log Archive & Audit Accounts using CloudTrail and Config Logs)
	- Sandbox OU - test/less rigid security
- Can create other OU's and accounts
- Using IAM Identity Center for SSO, ID Federation
- Monitoring and Notifications through CloudWatch and SNS
- End user provisioning via service catalog
**Guard Rails**
- Rules - multi-account governance
- Three standards - mandatory, strongly recommended, elective
- Can be preventative - via AWS ORG SCP - enforced or not enabled
- Detective - compliance checks - via AWS CONFIG Rules - clear, in violation, not enabled
**Account Factory
- Automated account provisioning
- Cloud Admins or End Users have access to this (appropriate permissions required)
- Guardrails are automatically added
- Account admin given to a named user via IAM Identity Center
- Account + network standard config
- Accounts can be closed or repurposed - can be fully integrated with a businesses SDLC (Software Dev Life Cycle)

