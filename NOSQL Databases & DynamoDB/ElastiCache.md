> [!note]- AI
> #### ElastiCache for Session State Caching
> - **Purpose:** Amazon ElastiCache is a fully managed, in-memory caching service that is commonly used to store session state data for web applications. By externalizing session data from individual application instances to a central cache, you can make your applications stateless and highly fault-tolerant.
> - **Fault Tolerance:** With external session storage, if an application instance fails, a user's session data is not lost. The load balancer can simply route the user's next request to a healthy instance, which can retrieve the session data from the cache and continue the user's session without interruption.
> #### Redis vs. Memcached: A Comparison
> - **Redis:**
>     - **Advanced Data Types:** Supports complex data types beyond simple strings, including lists, hashes, sets, and sorted sets. This is ideal for use cases like leaderboards or managing user sessions with multiple attributes.
>     - **High Availability:** Provides built-in **replication** for multi-Availability Zone (AZ) deployments, which enables automatic failover and read scaling across replica nodes.
>     - **Data Persistence:** Supports **backup and restore** functionality, allowing you to take snapshots of your cache data for recovery or archival.
>     - **Transactions:** Supports atomic operations and transactions, ensuring that a group of commands is executed as a single, isolated operation.
> - **Memcached:**
>     - **Simplicity:** It is a simpler, multi-threaded caching engine that is highly effective for basic key-value caching.
>     - **No Replication:** It does not have built-in replication or automatic failover. High availability requires manual sharding and external management.
>     - **No Backups:** It is a non-persistent, purely in-memory cache and does not support backup and restore.
> #### Addressing the Code Change Objection
> - **Objection: Cannot make code changes to application.**
>     - **Response:** This is a key real-world consideration. Implementing a caching layer like ElastiCache fundamentally requires you to modify your application code. The application must be updated to follow a specific caching strategy, such as a **cache-aside** or **write-through** pattern.
>     - The code must be changed to first check the cache for data before querying the database. If the data is found (a cache hit), it is returned directly from the cache. If not (a cache miss), the application queries the database, retrieves the data, and writes it to the cache before returning it to the user. While this requires development effort, the resulting improvements in performance, scalability, and cost reduction are significant.
> #### Definitions
> - **Replication:** In the context of ElastiCache for Redis, replication is the process of creating one or more read-only replicas of a primary cache node. This ensures high availability (by providing a replica for automatic failover) and increases read performance by distributing read traffic across multiple nodes.
> - **Backup and Restores:** A feature of ElastiCache for Redis that allows you to create point-in-time snapshots of your cluster's data. These snapshots can then be used to restore the data to a new cluster, providing a mechanism for disaster recovery and long-term data archival.
> - **Transactions:** A feature of Redis that allows a sequence of commands to be executed as a single, atomic operation. This ensures that either all commands in the transaction are completed successfully, or none of them are, which is important for maintaining data integrity.
> 

- In-memory database for high performance
- Not persistent, but much faster for throughput and storage
- Managed Redis or Memcached as a service
- Can be used to cache data for READ heavy workloads with low latency requirements
- Reduces database workloads (expensive)
- Can be used to store session data for stateless servers
- Requires application code changes
Architecture
- Let's say you have an application that is backed by Aurora and works with Elasticache
- DB Query (Cache Hit) means data will be loaded to Elasticache, and later queries for same data will result in cache hit
- Won't have a proportional increase in DB accesses
- An in-memory cache allows cost effective scaling of read-heavy workloads and performance improvement at scale
Session State Data
- Session data is written to Elasticache when Bob first connects to the application, if application needs to deal with failure of instance
- Bob's experience moved to different instance and session state loaded from cache, session continues with no interruption
Redis vs MemcacheD
- MemCahced = simple data structures, Redis = advanced structures
- Redis supports Multi-AZ replication of data, MemCached does not support replication
- Memcached (Sharding = multiple nodes), Redits = replication (scale reads)
- MemCacheD = no backups, Redis = backup & restore
- Memcached = Multi-threaded, Redis = transaction