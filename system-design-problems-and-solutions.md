# System Design Problems and Solutions

1. Ready-heavy system
	- Use caching for faster reads
	
2. High-write traffic
	- Use async writes
		- message queues and worker processes
	- Use LSM-Trees Database
		- Cassandra: collect writes in memory and periodically flush to the disk as sorted files. To maintain performance, they perform compaction: merging files to reduce  the number of lookups  required  during reads. This makes writes very fast but reads become slower as they may need to check multiple files.
	
3. Single point of failure
	- Implement redundancy and failover:
	  - Implement database replication with primary and replica instances. This increases availability but introduces complexity in consistency management.
	  - We could choose synchronous replication to prevent data loss and accept higher latency or
	  - opt for asynchronous replication for better performance but risks slight data losses during failures.
	
4. High Availability
	- Use load balancing
	  - Distribute traffic and re-route around failures
	- Use replication
	  - Primary-replica setup is standard: Primary handles writes while multiple replicas handle reads.
	  - Failover ensures a replica can take over if the primary fails.
	
5. High Latency
	- Use CDN to reduce latency by caching content closer to users - reducing latency.
	- Works well for static content but for dynamic content, solution like  edge computing can complement CDN caching.
	
6. Handling large files
	- Use block storage for changing data (great for structured, fast-changing data)
	
	- and object storage for large data (Perfect for large, static, or append-only data)
	
	- | Feature      | Block Storage              | Object Storage                     |
	  | ------------ | -------------------------- | ---------------------------------- |
	  | Storage unit | Blocks                     | Objects (data + metadata + ID)     |
	  | Access       | Filesystem-level (via OS)  | HTTP API                           |
	  | Latency      | Very low                   | Higher (network + metadata lookup) |
	  | Scalability  | Limited to volume size     | Practically infinite               |
	  | Metadata     | Minimal                    | Rich and customizable              |
	  | Ideal for    | Databases, VMs, high IOPS  | Backups, logs, media, big data     |
	  | Mutability   | Mutable (overwrite blocks) | Immutable (write new objects)      |
	
7. Monitoring and Alerting
	- Use centralized logging solution:
	  - Prometheus: collects logs and metrics
	  - Grafana provides visualisation
	  - Distributed tracing tools like open telemetry help debug performance bottlenecks across components
	
8. Slow database queries
	- Use proper indexes
	- Use sharding to horizontally scale

# How to Improve API Performance

1. Pagination
2. Async Logging
3. Caching
4. Payload Compression
5. Connection Pool
