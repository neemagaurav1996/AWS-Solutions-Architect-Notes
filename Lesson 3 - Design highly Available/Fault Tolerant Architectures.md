**Lesson 3 - Design highly Available/Fault Tolerant Architectures**

**3.1 Definitions**

- High Availability: System will work despite complete failure of any component in architecture
- Fault tolerant: System will work without degradation in performance
- Availability: % of uptime, in 9s
- Redundant: Multiple resources to perform same task
- Availability documentation
	- aws.amazon.com/<service>/sla
	- Well-architected Reliability pillar whitepaper, pages 54-58
	- Many services have 4 9s but don't assume it
	- Route 53 health checks can help with arbitrary endpoints
- Examples of high availability:
	- Virtual private gateway
	- NAT gateway
	- Elasticache: In memory cache service
	- Redshift: Not high available
	- RDS Multi-AZ
- Examples of fault tolerance:
	- S3
	- DynamoDB
	- API Gateway
	- CloudFront - Deployed globally
	- Route 53 - Deployed globally

**3.2 AWS Global Infrastructure**

- AWS Data center
	- 10s of thousands of servers
	- Infrastructure atomic unit
	- No services are deployed here
	- No direct resources

- Availability Zone (AZ)
	- 3+ data centers
 	- Failure zone
 	- High Availability(HA) building blocks
 	- Low latency
 	- Resources deployed on AZ scope:
 		- EBS volumes
 		- NAT Gateway
 		- EC2 instance
 		- RedShift Node
 		- RDS Instance

- Region
	- Fully independent
 	- 3+ AZ
 	- HA (Highly available) and FT (Fault tolerant)
 	- Service API endpoints are deployed here
 	- Resources deployed on region scope:
 		- S3
 		- DynamoDB table
 		- SNS topic
 		- VPC
 		- CloudWatch Alarm

- Multi Region
	- Higher availability
	- Higher cost
	- Higher overhead
	- Resources deployed on multi-region scope
		- S3 cross region replication
		- RDS
		- DynamoDB Global Table

- AWS Edge Location
	- Colocation facility
	- No sensitive data is deployed here
	- Better geographic distribution
	- To optimize end User Experience
	- Few Services: DNS, CDN
	- Glocal Resources Deployed on edge location
		- Route 53 hosted zone
		- Cloudfront distribution
		- WAF filtering rule
		- Lambda edge


