**Lesson 9 - Choose High-performing Database Solutions for a Workload**

**9.1 RDS Performance**

* **EC2 unmanaged DB with Instance Storage**

	- Not Resilient
	- Lowest latency
	- High/Very High throughput
	- Fixed performance
	- This is risky solution

* **EC2 unmanaged DB with 1 EBS Volume**

	- Low latency
	- Medium/High throughput
	- Some scalability
	- Limited by single EBS volume throughput/IOPS

* **EC2 unmanaged DB with 2+ EBS Volume**

	- Low latency
	- Very high throughput
	- Signigicant scalability
	- This solution may add complexity due to OS volume manager RAID
	- Risk of if single volume is lost, we might lose all the data on volume manager
	- Low resilience than single volume

* **RDS single instance**

	- Upsize instance type
	- Upsize storage
	- Limited by single RDS instance size capacity
	- Deploying read replicas allows you to scale your reads horizontal. This focuses on read workflow performance

* **Aurora DB**

	- Deploy multi-master + read replicas
	- MySQL or Postgres only
	- When client connect directly to db, horizontal scaling is difficult
	- Enable Aurora serverless 
		- Specify capacity up to 488Gb aggregate memory
		- It breaks compute units into discrete chunks
		- This changes endpoint to a proxy for database capacity pool
		- Capacity pool scales according to load by adding discrete units
		- Scale targets have an already warmed buffer pool

**9.2 DynamoDB Performance**

* DynamoDB is a key-value and document database
* Static provisioning
	- Fixed Read Ops, Write Ops
* Auto Scaling
	- Minimums 
	- Scaling thresholds
	- Maximums
* On demand
	- No capacity planning
	- This can increase cost in case of DDOS
* Account service limits
* Region service limits
* Partition key is the single most important decision for performances
* Table IOPS are divided by partition, so even distribution is important
* Global tables
    - In accordance with multiple best practices
    - This will allow the tables to be replicated in multiple regions
    - Done with DynamoDB events
