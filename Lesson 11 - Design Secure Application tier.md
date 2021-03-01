**Lesson 11 - Design Secure Application tier**

**11.1 Design Secure VPC Internal Network**

* Isolate public-facing resources like ALB and NAT GW
* Isolate application workloads
* Isolate database resources
* Use NACL (Network access control list) to blacklist between subnets. Don't use them for whitelisting. Block all outbound traffic from public subnet to database.
* Use security groups to whitelist application traffic. Stateful firewall entity.
* Enable VPC flow log for auditing network traffic header. Apply at individual ENI, subnet boundary or at entire VPC.
* Audit network traffic headers and payload. Can only apply at individual ENI.

**11.2 Designing secure VPC egress**

* Internet Gateway
    * No security features
* Route tables for direct outbound to the internet
* NAT GW for outbound-only access. Apply route table for indirect outbound through NAT GW.
* No need to apply at database level.
* Gateway endpoint provide network access to S3 and DynamoDB
* Interface endpoint provide private networks access to other services and private links
* Virtual private gateway VPN to outside network
* VPC peering: Private network access to another VPC

**11.3 Securing Application Access**

* ALB (Automatic Load balancer) + WAF (Web Application Firewall) to proxy and reject unauthorized access
* IAM role to access other AWS services
* Inspector agent for OS security audit
* Secrets manager for RDS DB credentials
* SSM Parameter store for keys and user/pass pairs

**11.4 Monitoring Application Activity**

* Set 1
    * Cloudtrail as audit trail for action taken in AWS account
    * CloudWatch logs to monitor log entries and set alarms based on filters
    * CloudWatch agent can installed on EC2 instance
    * Config rules to monitor resource changes

* Set 2
    * GuardDuty to monitor API key usage. It will generate ML models for access patterns.
    * Macie to monitor sensitive S3 objects
    * CloudWatch Event rules to monitor account event bus
    * SNS topic for notification and integration
    * Lambda function for complex logic and mitigation

