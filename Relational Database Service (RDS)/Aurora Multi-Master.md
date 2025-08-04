
>[!note]- Post-Processing
>## Key Insights and Information from the Amazon Aurora Multi-Master Writes Transcript:
>
>**What is Multi-Master Writes?**
>
>* An advanced Aurora feature allowing multiple instances within a cluster to perform both reads and writes.
>* This contrasts with the default "single master" mode, where only one instance handles writes and others only reads.
>
>**Architecture Differences:**
>
>* **Single Master:**
>    * One read-write instance (primary) and zero or more read-only replicas.
>    * A cluster endpoint handles both read and write operations.
>    * A separate read endpoint balances read traffic across replicas.
>    * Failover requires promoting a replica to read-write, which takes time.
>* **Multi-Master:**
>    * All instances are read-write capable.
>    * No cluster endpoint; applications connect directly to instances.
>    * No load balancing; applications manage connections.
>    * Failover is near-instantaneous as any instance can take over.
>
>**How Multi-Master Works:**
>
>* When a write request is received, the instance proposes the change to all storage nodes.
>* Each node confirms or rejects the proposal based on potential conflicts.
>* A quorum of nodes agreeing allows the change to be committed to shared storage.
>* Replicated across all nodes, ensuring consistency for reads.
>
>**Benefits:**
>
>* **Faster Availability:** Near-instantaneous failover minimizes disruption.
>* **Fault Tolerance:** Applications can connect to multiple writers, allowing them to continue operating even if one instance fails.
>* **Improved Scalability:** Multiple writers can handle more write traffic.
>
>**Considerations:**
>
>* Application logic needs to handle load balancing and connection management.
>* Multi-master is not a guaranteed 100% fault-tolerant solution, but it provides a strong foundation.
>
>**Overall:**
>
>Multi-Master writes in Amazon Aurora offer significant advantages for building highly available and fault-tolerant applications. However, careful planning and application design are crucial to fully leverage its benefits.
>

- Default Aurora mode is single-master
- One R/W and 0+ Read Only Replicas
- Cluster Endpoint is used to write, read endpoint is used for load balanced reads
- Failover takes time while replica is promoted to R/W
- In Multi-Master mode all instances are R/W
- Application can connect to one or both of these R/W instances, and they will try to make a change to all the shared cluster storage. Assuming there is no conflicting in flight data, it will commit this change and also replicate this change into the other R/W instances so that they respond correctly to any read requests (saved in their cache)
- Because no-endpoints, in multi-master if one of our writers fail, it's okay because the application will be sending to the other writer instantly as well as there's no need for promotion to R/W
	- Almost fault tolerant -> first step in developing fault tolerant app
