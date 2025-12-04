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
	- Use CDN to reduce latency
6. Handling large files
	- Use block storage and object storage
7. Monitoring and Alerting
	- Use centralized logging solution
8. Slow database queries
	- Use proper indexes
	- Use sharding to horizontally scale
