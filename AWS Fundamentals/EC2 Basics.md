EC2 Basics

- Provides access to virtual machines called instances
  
- IAAS - provides virtual machines => instances (an OS configured in a certain ways with a certain set of allocated resources)
  
- Private service by-default - uses VPC networking
  
- EC2 is AZ resilient because of the VPC netowrking - instance fails if AZ fails
  
- Local on-host storage or Elastic Block Storage (EBS)
### Instance Lifecycle

- EC2 instance has an attribute called a state, provides an indication into its condition.
  
- Running, Stopped, Terminated (there are states between those but these are big three)
  
- In stopped state, you are not being charged for CPU, Memory, or Networking, but you are still be charged for storage (because you are still allocated to the storage.
### Amazon Machine Instance (AMI)

- An image of an EC2 instance, can be used to create an EC2 instance or can be created from an EC2 instance.
  
- Similar to a server image to create VM or USB device to load Linux, Windows, etc.
  
- AMI contains attached permissions, public - everyone allowed to launch instances from AMI, owner - implicitly allowed to create EC2 instances from AMI, explicit - owner explicitly gives access to AMI to AWS accounts
  
- AMI also handles the boot volume of the instance and block device mapping, links the volumes the AMI has and how they are given to the OS.