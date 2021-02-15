**Lesson 5 - Choosing Appropriate Resilient Storage**

**5.1 Instance Store**

* Server scope
* Availability and durability not published
* Anti pattern
* Avoid this if you want resilient

**5.2 EBS Resilience**

* HDD and SSD storage available
* AZ scope
* Availability: 5 9s
* Durability: AFR of 0.1 to 0.2%
* Data replicated within AZ
* For region scope, you have to create a snapshot. This will increase durability but decrease availability.
* Custom solution for cross-region snapshot copy
* Not resilient if all the backups are stored in the same AWS account.

**5.3 EFS Resilience**

* Resilient shared storage
* Multiple EC2 can access EFS at same time.
* Availability: 3 9s
* Durability: 11 9s
* Lower availability but higher durability than EBS
* EFS Mount point
	- AZ scope
	- Associated with subnet in VPC
	- No published resilience data
* "AWS backup" can restore points for EFS filesystem
* "AWS Data Sync" can be used for cross-region copy

**5.4 S3 Resilience**

* S3 Standard
	- Region scope
	- Availability: 4 9s
	- Durability: 11 9s
	- Replicated across at least 3 AZs
	- Copies validated via checksum

* S3 IA
	- Region scope
	- Availability: 3 9s
	- Durability: 11 9s

* S3 Intelligent Tiering
	- Migrate your objects intelligently
	- Region scope
	- Availability: 3 9s
	- Durability: 11 9s

* S3 Z-IA
	- AZ scope
	- Availability: 2.5 9s
	- Durability: 11 9s
	- Data replicated 3 times within same AZ

To further increase the durability, we can create buckets in the second region, and enable bucket versioning. Then enable bucket versioning in the source bucket, then configure cross-region replication.
Not a complete solution, will not work for existing objects. All data still sits on the same account.

* S3 Glacier
	- Region scope
	- Availability: 4 9s
	- Durability: 11 9s
	- Much higher latency, few minutes to few hours
	- Data replicated across at least 3 AZs.

* S3 Glacier Deep archive
	- Region scope
	- Availability: 4 9s
	- Durability: 11 9s
	- Very high latency (within 12 hours)
