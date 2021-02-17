**Lesson 6 - Elasticity and Scalability**

* Scalability
	- Ability of system to increase resources to accommodate increased demand
	- Can be done Horizontal or vertical
	- Doesn't imply automation

* Elasticity
	- Ability of system to increase and decrease the resources with demand
	- Done Horizontally
	- Imply automation
	- Elastic is also scalable but not vice-versa

**6.1 Elasticity with unified auto scaling**

* EC2 Spot Fleet
	- Cost Effective
	- Multi AZ
	- Multi instance type
	- Volatile
	- Less resilient

* EC2
	- Durable (but not that durable)
	- Multi AZ
	- Multi instance type
	- Not volatile
	- More resilient

* Auto scale launch templates (New Configuration)
	- Version control: Re-use or even setup default templates
	- Utilize T2 unlimited instances
	- Multiple instance types
	- On-demand and spot at the same time
	- Use regular EC2 launch tasks

* Auto Scaling Reactive Scaling
	- This is default scaling
	- As load increases, new resources are added to the fleet with a minimum reaction time of at least a few minutes
	- We can scale proactively
	- Predictive scaling mode
		- Forecast mode: ML model that observe pattern of traffic
		- Forecast and Scale
		- Max capacity behavior: Set min and max capacity

* ECS on Fargate
	- Serverless
	- VPC Integration

* Aurora
	- With read replicas that automatically scale
	- Scaling isn't instant

* DynamoDB
	- Table or GSI
	- Scale read/write
	- Capacity

**6.2 Elasticity with Managed services**

* Used for serverless

* API Gateway
	- REST API
	- SSL Termination
	- Instant Scaling

* S3
	- Static assets
	- Instant Scaling

* ALB
	- Web Proxy
	- SSL Termination
	- Path-based routing
	- Not instant

* Lambda
	- Compute back end
	- Instant scaling
	- Provisioned limits

* ECS
	- Compute back end
	- Auto Scaling
	- Not instant

* DynamoDB
	- Instant scaling
	- Provisioned limits

