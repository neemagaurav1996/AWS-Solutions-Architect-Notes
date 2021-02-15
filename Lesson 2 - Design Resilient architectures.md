**Lesson 2 - Design Resilient architectures**

**2.1 Resilient VPC**
* Multi tier resilient VPC design

**2.2 Resilient Application architecture**

* ELB
	- Elastic load balancer
	- Availability: 4 9s
	- Multiple AZ

* Auto scaling
	- Redundant EC2
	- Multi AZ
	- Availability: 1 9

* RDS
	- Multi AZ
	- Active/Passive writes
	- Availability: 3.5 9s

* RDS Aurora
	- Multi master
	- Active/Active
	- Availability: 4 9s
	- Can only use MySQL and Postgres and specific versions

**2.3 Resilient Multi-tier Serverless Architecture**

* Route 53
	- Global DNS
	- 100% uptime SLA (Service level agreement)

* Cloudfront
	- Global CDN service
	- Availability 4 9s

* S3 Region
	- Availability: 4 9s
	- Cached through cloud fronts
	- Region scope

* API gateway
	- Availability: 4 9s
	- Region scope

* Cognito
	- Used for authentication
	- Region scope
	- Availability: 3 9s
	- If only portion of requests go here then this is not a weak link

* Lamda
	- Region scope
	- Availability: 3.5 9s
	- Entirely serverless

* DynamoDB
	- Region scope
	- Availability: 4 9s
	- For dynamic data
