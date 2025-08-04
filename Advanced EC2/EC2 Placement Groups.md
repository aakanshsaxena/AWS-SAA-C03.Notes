Cluster Placement Groups
- All members have direct connection to each other
- All members must be located on the same AZ
- Located on same rack, sometimes same host
- Lowest latency and max PPS possible in AWS
- 10GBps p/ stream vs 5GBps normal
- Can't span AZs - 1 AZ only - locked when launching first instance
- Can span VPC peers but impacts performance
- Requires a supported instance type
- Use the same type of instance, and launch at same time (not mandatory but recommended)
- 10GBps single stream performance
- Use for performance, fast speeds, low latency
Spread Placement Groups
- Instances placed on distinct racks
- 7 instances per AZ - isolated infrastructure limit
- Provides infrastructure isolation
- Each instance runs from a different rack
- Each rack has its own network and power source
- 7 instances per AZ (Hard Limit)
- Not supported for dedicated instances or hosts
- Use: small number of critical instances that need to be kept separated from each other
Partition Placement Groups
- Divided into partitions max 7 per AZ
- Each partition has its own racks - no sharing between partitions
- 7 partitions per AZ
- Instances can be placed in a specific partition or auto placed by EC2
- Great for topology aware apps like HDFS, HBase, and Cassandra
- Contain the impact of failure to part of an application

When to use spread vs partition
### 🔹 Spread Placement Group — **Use Case**

**Purpose:** Maximize **availability** and **fault tolerance** by placing instances on distinct hardware (different racks, power, network).

#### ✅ Best For:

- **Critical applications** that must avoid simultaneous failure of multiple instances.
    
- **Small number** of instances (max 7 per Availability Zone).
    
- **Low-latency** requirements are **not critical**.
    
- **Domain controllers, quorum nodes, or master databases**.
    

#### 📌 Example:

> You are running 3 critical web servers behind a load balancer, and you want to ensure they don’t all fail at once due to rack failure.

---

### 🔸 Partition Placement Group — **Use Case**

**Purpose:** Split instances across logical partitions, with each partition on **distinct racks**, allowing large-scale **fault isolation**.

#### ✅ Best For:

- **Large distributed systems** like **Hadoop**, **Kafka**, **Cassandra**.
    
- Applications requiring **high availability** **and** the ability to scale to **dozens/hundreds** of instances.
    
- **Fault-tolerant architecture** where a failure in one partition shouldn't impact the others.
    

#### 📌 Example:

> You’re deploying a Cassandra database with 9 nodes across 3 partitions so that each partition (rack) has 3 nodes. If one rack fails, the other partitions still operate.