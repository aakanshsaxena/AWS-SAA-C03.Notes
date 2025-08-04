> [!note]- AI
> #### DAX Caching Architecture
> - **Purpose:** DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for DynamoDB. Its primary goal is to drastically reduce read latency from milliseconds to **microseconds** and offload read traffic from the underlying DynamoDB table, which reduces costs.
> - **Dual Caches:** A DAX cluster maintains two types of caches:
>     - **Item Cache:** This cache stores individual items that are retrieved from `GetItem` or `BatchGetItem` operations. Items are stored based on their primary key.
>     - **Query Cache:** This cache stores the results of `Query` and `Scan` operations, along with their parameters.
> - **Write-Through Caching:** DAX uses a write-through caching strategy. When an application performs a write operation, DAX writes the data to both the DAX cache and the underlying DynamoDB table simultaneously. This ensures that the cache is always kept up to date with the latest writes.
> - **High Availability:** A DAX cluster is deployed with a primary node for write operations and one or more replica nodes for read operations. In the event of a primary node failure, a replica is automatically elected as the new primary to ensure high availability.
> #### Addressing Common Objections
> - **Objection: High cost of large RCU values on DynamoDB tables.**
>     - **Response:** DAX is a direct solution to this problem. For read-heavy or bursty workloads, the cost of provisioning a large number of RCUs can be very high. By caching read results, DAX handles a majority of the read traffic, which significantly reduces the required RCU values on the underlying DynamoDB table. This lowers your operational costs, making DAX an excellent choice for read-intensive applications.
> - **Objection: DAX not suitable for applications needing strong consistency or low latency.**
>     - **Response:** DAX is an **eventually consistent** cache. While a read from the cache is extremely fast, it may not reflect the latest write. If an application requires a strongly consistent read, DAX is configured to pass that request directly to the DynamoDB table. Therefore, DAX is not suitable for applications that cannot tolerate a slight data lag. It is also not ideal for applications with infrequent read operations, as the cost of running a DAX cluster may outweigh the cost savings from the cache.
> #### DAX Use Cases and Benefits
> - **Reduced Latency:** DAX can reduce read latency by an order of magnitude, from milliseconds to microseconds, which is critical for real-time applications like gaming, finance, and online advertising.
> - **Read-Intensive Workloads:** It is an ideal fit for applications that have a high volume of repetitive reads, such as leaderboards, time-series data, or product catalog lookups.
> - **Simplified Integration:** DAX is seamlessly integrated with the DynamoDB SDK, which means you can add DAX to an existing application with only a few simple configuration changes.
> #### Definitions
> - **VPC:** An Amazon Virtual Private Cloud (VPC) is a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have full control over your virtual networking environment, including your own IP address ranges, subnets, and security groups.
> - **Strongly Consistent Reads:** A consistency model in DynamoDB that guarantees that a read operation returns the most up-to-date data, reflecting all completed write operations. While this is critical for sensitive applications, it consumes twice the read capacity of an eventually consistent read.
> 

Traditional Cache vs DAX
- Normal: application checks cache for data, either cache miss (and load data into cache), or cache hit
- DAX: DAX SDK installed on application, DAX and DynamoDB considered same by application. Application uses DAX SDK and makes a single call for the data which is returned by dax, DAX returns data from its cache or retrieves from the DB and then caches it
	- Less complexity for app developer and tighter integration
Architecture
- Operates from within a VPC
- Primary node (read and write node), read replicas created in other AZ
- Item cache holds results of (Batch)GetItem. The query cache holds data based on query/scan parameters
- DAX is accessed via an endpoint. Cache hits are returned in microseconds, misses in milliseconds
- DAX can use write-through caching. Data is written to DDB then DAX
- If a cache miss occurs, data is also written to the primary node of the cluster
Consideration
- Primary node (writes) and replicas (read)
- Nodes are HA, primary failure = election
- In-memory cache - scaling, much faster reads and reduced costs
- Scale up or Scale Out (Bigger or more DAX instances)
- Write-through support
- DAX is not a public service, deployed within a VPC. Applications using DAX must also be deployed or have access to this VPC.