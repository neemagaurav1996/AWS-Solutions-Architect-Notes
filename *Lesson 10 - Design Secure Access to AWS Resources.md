**Lesson 10 - Design Secure Access to AWS Resources**

**10.1 Account-based access control**

* **AWS Organizations**
	- Manage multiple AWS accounts

* **AWS SSO (Single Sign-On)**
	- Used within AWS Organizations
	- Account access federation

* **SCPs (Service Control Policies)**
	- JSON document like IAM policies
	- Act as permission boundaries
	- Can't be used to grant access
	- Can be used to deny access
	- But allow statement can be set
	- Good for both allow and deny statements

**10.2 User-based access control**

* **IAM Policies**
	- JSON documents that can be used to grant or deny access to resources that are within the same AWS account
	- Supports permission (grant access) and permission boundaries (max. level of permissions)
	- Understand the relationship between permission and boundaries
	- IAM roles
		- For temporary privileges
		- Can be used for cross-account access
		- Used for cross-service access

**10.3 Resource-bases access control**

* **S3 Bucket Policy**
	- Only applies to the associated bucket
	- Required for some functions (Example: Access logging from ALB)
	- Watch for S3 Block public access override

* **Glacier Vault Access Policy**
	- Only applies to the associated vault
	- Similar to S3 policy
	- Vault lock policy is separate

* **KMS CMK Key Policy**
	- KMS - Key Management service
	- CMK - Customer Master Key
	- Applies to specific CMK
	- Required for all CMKs
	- Contains two different sections - One for Key Admin and another for Key user

* **Lambda Function Access Policy**
	- Only applies to the associated function
	- Can be used to share lambda layers
	- Be careful of IAM and Function policy interaction

* **API Gateway Resource Policy**
	- Only applies to associated API
	- Usable for all endpoint types
	- Can affect authorization workflows

* **SNS Access Policy**
	- Only applies to the associated topic
	- Required for some use cases (AWS Budgets)
	- Overrides IAM in some cases
