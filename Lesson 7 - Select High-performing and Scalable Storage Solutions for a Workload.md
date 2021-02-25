**Lesson 7 - Select High-performing and Scalable Storage Solutions for a Workload**

**7.1 Block-based Storage Performance**

* Instance Storage
	- Low latency
	- High IOPS
	- Depends on instance
	- Performance Independent of size

* EBS Standard HDD
	- Legacy storage
	- Throughput up to 90MB/s
	- Low IOPS
	- Independent of size
	- Maximum size 1 TB

* EBS Cold HDD
	- 250 MB/s
	- Dependent on size

* EBS  Throughput Optimised HDD
	- 500 MB/s
	- Dependent on size

* EBS general purpose SSD
	- Up to 16000 IOPS
	- 128-250 MB/s
	- Dependent of size

* EBS Provisioned IOPS SSD
	- Up to 64000 IOPS
	- Up to 1000 MB/s
	- Dependent on size

* Instance maximums
	- 160,000 IOPS across multiple volumes
	- 3500 Mbps across multiple volumes

**7.2 File-based Storage Performance**

* EFS File system resource

	- Up to 3 Gb/s throughput
	- Throughput depends on region
	- 250MB/s per client
	- Latency: unpublished but can be 1 ms
	- Two performance modes
		1. General purpose performance mode
			- Default
			- 7000 IOPS
			- Lowest metadata latency
		2. MaxIO performance mode
			- 500k+ IOPS
			- Highest metadata latency
			- Use for larger files that are used less frequently

	- Make sure you use the mount point in the same AZ as your client node
	- Watch your BurstIO credits in CloudWatch.
	- Recommended mount point:
		rsize=1M, wsize=1M
		smaller values limit throughput for large files
	- Use EFS mount helper
	- Parallelize file system access up to 40 concurrent transfers per client
	- 2-3 instances can exhaust the IOPS of a general purpose file system
	- Always test your throughput, don't assume you can achieve the maximum

**7.3 Object-based Storage Performance**

* S3 Parallelism

	- Don't aggregate S3 requests through a single node
	- Parallelize requests to improve S3 performance

	- Per-prefix performance
		- PUT/POST/COPY/DELETE 3500 requests/sec
		- GET/HEAD 5500/sec
		- Unlimited prefixes within a bucket
		- No random prefixes required

	- Latency performance
		- Based on object size
		- Small objects 100-200 ms
		- Large objects 100-200 ms but for first byte
		
	- S3 Caching
		- Cache via CloudFront on Edge location
		- Cache via Elasticache

	- Enable S3 transfer Acceleration
		- Not good for small geographical distance

**7.4 Caching Performance in CloudFront**

- Assets are cached in choice of continents
- Low latency
- Massively scalable

**7.5 Caching Performance in Elasticache**

- To use within the VPC
- Use case: A single RDS R/W endpoint can be overwhelmed with a large traffic spike. This problem can be solved the splitting the workloads but it is expensive.
- Use Elasticache
	- Memcached for horizontal scaling. Volatile.
	- Redis for durable storage
- Elasticache can help absorb traffic spike, reduce latency, especially for same-AZ traffic
- Using DynamoDB instead of Elasticache session state will optimize even higher durability. But it can introduce latency, variable cost and decreased performance when traffic spikes.

