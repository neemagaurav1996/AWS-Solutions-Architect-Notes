**Lesson 8: Select High-performing Networking Solutions for a Workload**

**8.1 VPC Performance**

* Consolidate resources within a single AZ to minimize latency (< 1ms), but this compromises resilience
* Traffic Egress Fragmentation - Jumbo frames are fragmented to 1500 MTU if they use an IGW for egress from the VPC. This is anti-pattern
* Avoid Public AWS Network. Using an IGW to reach AWS services requires traffic crossing public AWS networks. Instead adding a gw or interface endpoint allows traffic to be proxied directly to aws serves.
* Avoid Inline Gateways. An EC2 based inline gateway can be a router, proxy or NAT. This is an anti-pattern because it will be a bottleneck and single point of failure.

**8.2 Single-node Performance**

* **EC2 instance type with ENI (Elastic Network Interface)**

	* Directly attached to EC2
	* Maximum 25Gbps but this depends on the instance type, can be much lower

* **EC2 instance type with ENA (Elastic Network Adapter)**

	* Instance types that end with "n" support ENA
	* Some are bare metal
	* Some use Nitro virtualization
	* No published maximum but significantly higher than ENI
	* ENA require Enhanced Networking to be enabled on instance

* **EC2 instance type with EFA (Elastic Fabric Adapter)**

	* 2 largest instance types of each family that end with "n" support EFA
	* MPI (Message Passing Interface) one-way latency as low as 15.5 microseconds
	* Maximum 100Gbps but depends on instance
	* It is ENA with added capabilities, and benefits from cluster placement groups

* **EC2 Enhanced Networking**

	* Using Software or the guest OS to improve the network performance
	* Uses single root I/O virtualization
	* For ENI, just switch the kernel driver to enable this mode
	* For ENA/EFA, switch the kernel driver then attach the resource
	* Higher bandwidth, higher PPS, lower latency, less jitter

* **EC2 Placement Groups**

	* Designed to influence EC2 instance placement within the region for performance
	* Placement groups can be used within single AZ or across multiple AZ
	* Three types:
		1. **EC2 Cluster Placement Group**
			- Deploy all the instances within a single rack. 
			- No blocking, no oversubscription 
			- High throughput, low latency
			- Use case: Clusters have majority of traffic between group nodes
			- Not designed for resilience
		2. **Partition Placement Group**
			- You can deploy your resources into  multiple places in the same AZ across partition where partition = set of racks
			- Use case: Distributed + Replicated workloads
			- Can span multiple AZ
			- Designed for performance and resilience
		3. **EC2 Spread Placement Group**
			- Each instance = separate rack
			- Use case: Critical instances that must be kept separate
			- Designed for guaranteed resilience
			- Not for performance
			- Can span multiple AZ

**8.3 Hybrid Network Performance**

* Connecting two networks together where one of them is not on AWS

* **VPG (Virtual Private Gateway)**
	* Connecting corporate network through VPN to a VPC
	* Connection will be encrypted with IPSEC and key exchange
	* Traffic traverses the internet
	* There is not way to guarantee specific throughput or latency

* **VPC Peering**
	* Guaranteed private connection 
	* Within the same region the traffic is not encrypted
	* Encrypted if cross region
	* Better performance than DIY or other custom solution
	* No published latency or throughput metrics

* **Direct Connect Gateway**
	* This is where you run a fibre WAN into an AWS partner data center and they cross connect you into AWS
	* Guaranteed bw upto 10GBps per connection
	* You can connect into your VPC or into the AWS service API gateways
	* Lower latency than VPG
	* Latency numbers are only published to the closest region

* **DIY**
	* Do it yourself
	* Full flexibility
	* No guaranteed performance
