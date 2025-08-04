
>[!note]- Post-Processing
>## EC2 Dedicated Hosts: Key Insights and Information
>
>This transcript provides an overview of EC2 Dedicated Hosts, a feature allowing users to rent entire EC2 hosts for exclusive use.
>
>**Here are the key takeaways:**
>
>* **Dedicated hosts are for you:** You get exclusive access to the entire host, paying for its capacity in full.
>* **No instance charges:**  Once you pay for the host, you don't incur additional charges for running instances on it.
>* **Flexible payment options:** You can choose on-demand pricing for short-term needs or reservations for long-term commitments with upfront, partial upfront, or no upfront payment options.
>* **Hardware visibility:** Dedicated hosts come with a specific number of physical sockets and cores, which is important for:
>    * **Instance capacity:**  It dictates how many instances can run on the host.
>    * **Software licensing:**  Enterprise software licensed based on physical sockets or cores can utilize this visibility.
>* **Mix-and-match flexibility:** Newer Nitro-based dedicated hosts offer more flexibility, allowing you to run different instance sizes simultaneously within the host's core limit.
>* **Dedicated host types:** Different dedicated hosts are available for different instance families (e.g., A1, R5, C5) with varying configurations and pricing. 
>* **Limitations:**
>    * **AMI restrictions:**  Only REL SUSE Linux and Windows AMIs are supported.
>    * **RDS incompatibility:** You cannot use Amazon RDS instances on dedicated hosts.
>    * **Placement group exclusion:** Placement groups are not supported with dedicated hosts.
>* **Sharing with other accounts:** Dedicated hosts can be shared within your organization using AWS RAM (Resource Access Manager).
>
>**Overall:**
>
>EC2 Dedicated Hosts provide a dedicated and isolated environment for running your instances, with the benefit of potentially lower costs and better control over hardware resources. However, they come with specific limitations and are best suited for specific use cases.
>
>
>

- Generally used for licensing restrictions
