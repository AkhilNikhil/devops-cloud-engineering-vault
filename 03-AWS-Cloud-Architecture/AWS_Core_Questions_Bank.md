# 📝 AWS Core Questions Bank

```text
aws questions


############################################################
COMPLETE DEVOPS INTERVIEW PREPARATION (JUNIOR → MID)
DETAILED QUESTION → ANSWER FORMAT (NO REDUCTION)
############################################################

============================================================
******AWS NETWORKING & VPC******
============================================================

Q) Difference between Public EC2 and Private EC2
A)
Public EC2 Instance:
- An EC2 instance that resides in a public subnet
- Has a public IPv4 address or Elastic IP (EIP – Elastic IP)
- The subnet route table contains a route (0.0.0.0/0) pointing to an Internet Gateway (IGW – Internet Gateway)
- Can directly communicate with the internet
- Common use cases: Web servers, Load Balancers, Bastion Hosts

Private EC2 Instance:
- An EC2 instance that resides in a private subnet
- Does NOT have a public IP address
- Cannot receive inbound internet traffic directly
- Uses a NAT Gateway (Network Address Translation Gateway) for outbound internet access
- Common use cases: Databases, application servers, backend services

------------------------------------------------------------

Q) What is a NAT Gateway (Network Address Translation Gateway), where does it reside, and how is it used?
A)
- NAT Gateway is a fully managed AWS service that allows instances in private subnets to access the internet
- It performs Network Address Translation (NAT)
- It always resides in a public subnet
- Requires an Elastic IP to communicate with the internet
- It allows outbound internet traffic but blocks inbound internet-initiated connections
- Commonly used for OS updates, package downloads, and external API calls from private EC2

------------------------------------------------------------

Q) Difference between NAT Gateway and Bastion Host
A)
NAT Gateway:
- Used only for outbound internet access
- Managed service provided by AWS
- Highly available and scalable by default
- Cannot be used for SSH or RDP access

Bastion Host:
- A hardened EC2 instance used for administrative access
- Allows SSH (Linux) or RDP (Windows) access to private EC2 instances
- Requires manual patching and security hardening
- Used only for management access, not internet access

------------------------------------------------------------

Q) How does routing work for NAT Gateway?
A)
- The NAT Gateway is deployed in a public subnet
- The public subnet route table has a route:
  0.0.0.0/0 → Internet Gateway (IGW)
- The private subnet route table has a route:
  0.0.0.0/0 → NAT Gateway
- Traffic flow:
  Private EC2 → NAT Gateway → IGW → Internet → Response → NAT Gateway → Private EC2

------------------------------------------------------------

Q) What is an Internet Gateway (IGW – Internet Gateway)?
A)
- Internet Gateway is a horizontally scaled, redundant AWS-managed component
- It allows communication between resources in a VPC and the public internet
- Required for public subnets
- Supports IPv4 and IPv6 traffic
- Enables inbound and outbound internet connectivity

------------------------------------------------------------

Q) How to access S3 from a private subnet without using public internet?
A)
- Use a VPC Endpoint (Gateway Endpoint) for Amazon S3
- The endpoint allows private connectivity between VPC and S3
- Traffic does not leave the AWS network
- Improves security and reduces data transfer cost
- Requires updating route tables and bucket policies

------------------------------------------------------------

Q) Types of Load Balancers in AWS
A)
Application Load Balancer (ALB – Application Load Balancer):
- Operates at Layer 7 (HTTP/HTTPS)
- Supports path-based and host-based routing
- Commonly used with microservices and Kubernetes

Network Load Balancer (NLB – Network Load Balancer):
- Operates at Layer 4 (TCP/UDP)
- Extremely low latency
- Used for high-performance workloads

Classic Load Balancer (CLB – Classic Load Balancer):
- Legacy load balancer
- Supports Layer 4 and basic Layer 7

------------------------------------------------------------

Q) What is a VPC (Virtual Private Cloud)?
A)
- A logically isolated virtual network in AWS
- You define the IP address range using CIDR (Classless Inter-Domain Routing)
- Supports subnets, route tables, gateways, and security controls
- Forms the foundation of AWS networking

------------------------------------------------------------

Q) How to connect multiple VPCs together?
A)
- VPC Peering: One-to-one private connection
- Transit Gateway (TGW – Transit Gateway): Hub-and-spoke connectivity
- VPN (Virtual Private Network): Encrypted tunnel over internet

------------------------------------------------------------

Q) Alternatives to VPC Peering
A)
- Transit Gateway for scalable multi-VPC connectivity
- AWS PrivateLink for service-level access without full VPC connectivity

------------------------------------------------------------

Q) What is CIDR (Classless Inter-Domain Routing) in AWS?
A)
- CIDR defines the IP address range for a VPC or subnet
- Example: 10.0.0.0/16
- Smaller CIDR means fewer IP addresses

------------------------------------------------------------

Q) How to calculate IP addresses from CIDR?
A)
- Formula: Total IPs = 2^(32 – subnet mask)
- Example:
  /24 → 2^(32-24) = 256 IPs
  /16 → 65,536 IPs

------------------------------------------------------------

Q) How many IPs are reserved/blocked by AWS?
A)
- AWS reserves 5 IP addresses per subnet

------------------------------------------------------------

Q) Which IP addresses are blocked by AWS?
A)
- First IP: Network address
- Second IP: VPC router
- Third IP: DNS resolver
- Fourth IP: Reserved by AWS
- Last IP: Broadcast address

============================================================
******EC2 (Elastic Compute Cloud)******
============================================================

Q) What is EC2 in AWS?
A)
- EC2 provides resizable compute capacity in the cloud
- Allows users to launch virtual servers called instances
- Supports multiple operating systems and instance sizes

------------------------------------------------------------

Q) What are the different types of EC2 instances?
A)
- General Purpose: Balanced workloads
- Compute Optimized: CPU-intensive applications
- Memory Optimized: In-memory databases
- Storage Optimized: High I/O workloads
- GPU Instances: Machine learning and graphics

------------------------------------------------------------

Q) What is an AMI (Amazon Machine Image)?
A)
- A pre-configured template containing OS, software, and configuration
- Used to launch EC2 instances consistently
- Can be AWS-managed or custom-built

------------------------------------------------------------

Q) What are EC2 key pairs?
A)
- Used for secure authentication
- Consists of a public key (stored in AWS) and private key (stored by user)
- Required for SSH access

------------------------------------------------------------

Q) What are EC2 pricing models?
A)
- On-Demand: Pay-as-you-go
- Reserved Instances: Discounted pricing with commitment
- Spot Instances: Cheapest option but interruptible

------------------------------------------------------------

Q) What is an Elastic IP (EIP – Elastic IP)?
A)
- Static public IPv4 address
- Used to remap IPs during failures

------------------------------------------------------------

Q) What is User Data in EC2?
A)
- A script executed at first boot
- Used to install packages and configure applications automatically

------------------------------------------------------------

Q) What is an Auto Scaling Group (ASG – Auto Scaling Group)?
A)
- Automatically increases or decreases EC2 instances
- Ensures high availability and fault tolerance

============================================================
******S3 (Simple Storage Service)******
============================================================

Q) What is Amazon S3?
A)
- Highly scalable object storage service
- Designed for 99.999999999% durability

------------------------------------------------------------

Q) What are the storage classes in S3?
A)
- Standard
- Intelligent-Tiering
- Standard-IA (Infrequent Access)
- One Zone-IA
- Glacier
- Glacier Deep Archive

------------------------------------------------------------

Q) How does versioning work in S3?
A)
- Maintains multiple object versions
- Helps recover from accidental deletions

------------------------------------------------------------

Q) What is an S3 bucket?
A)
- Logical container for objects
- Bucket names are globally unique

------------------------------------------------------------

Q) What are S3 access control policies?
A)
- Bucket Policies (JSON-based)
- ACLs (Access Control Lists)

------------------------------------------------------------

Q) What encryption types are supported in S3?
A)
- SSE-S3 (S3-managed keys)
- SSE-KMS (Key Management Service)
- Client-side encryption

------------------------------------------------------------

Q) What are S3 Lifecycle Policies?
A)
- Automates object transition and deletion
- Reduces storage cost

============================================================
******IAM (Identity and Access Management)******
============================================================

Q) What is AWS IAM?
A)
- Central service to manage authentication and authorization
- Controls access to AWS resources securely

------------------------------------------------------------

Q) IAM User vs IAM Role
A)
IAM User:
- Used by humans
- Long-term credentials

IAM Role:
- Used by AWS services
- Temporary credentials via STS

------------------------------------------------------------

Q) What are IAM Policy types?
A)
- Managed Policies (AWS-managed or customer-managed)
- Inline Policies

------------------------------------------------------------

Q) What is a Trust Policy?
A)
- Defines which entity can assume a role

------------------------------------------------------------

Q) What is STS (Security Token Service)?
A)
- Issues temporary credentials
- Used for role assumption and federation

------------------------------------------------------------

Q) How do you implement MFA (Multi-Factor Authentication) in AWS?
A)
- Adds an additional authentication factor
- Improves account security

============================================================
******DOCKER & CONTAINERS******
============================================================

Q) Explain Docker Architecture
A)
- Docker Client sends commands
- Docker Daemon builds and runs containers
- Docker Images are templates
- Docker Registry stores images

------------------------------------------------------------

Q) Difference between Containers and Virtual Machines
A)
Containers:
- Share host OS kernel
- Lightweight and fast

Virtual Machines:
- Have separate OS
- Higher resource usage

------------------------------------------------------------

Q) How containers use OS resources
A)
- Namespaces provide isolation
- cgroups (Control Groups) manage resources

------------------------------------------------------------

Q) How resource allocation works for containers
A)
- CPU and memory limits defined during runtime

------------------------------------------------------------

Q) Explain Dockerfile
A)
- Declarative file used to build Docker images
- Common instructions:
  FROM, RUN, COPY, CMD, ENTRYPOINT

------------------------------------------------------------

Q) What is a Multi-stage Dockerfile?
A)
- Uses multiple build stages
- Produces smaller and secure images

============================================================
******KUBERNETES******
============================================================

Q) What are Services in Kubernetes?
A)
- Provide stable networking for Pods
- Abstract Pod IP changes

------------------------------------------------------------

Q) Types of Kubernetes Services
A)
- ClusterIP: Internal access
- NodePort: Exposes service on node
- LoadBalancer: Cloud-managed LB

------------------------------------------------------------

Q) What is Ingress and Ingress Controller?
A)
Ingress:
- Defines routing rules for HTTP/HTTPS

Ingress Controller:
- Implements those rules using a load balancer

------------------------------------------------------------

Q) How do you set up an Ingress Controller?
A)
- Deploy NGINX Ingress Controller
- Create Ingress resource YAML

------------------------------------------------------------

Q) How does traffic flow from domain → Ingress → Service → Pod?
A)
- DNS resolves domain
- Traffic hits Load Balancer
- Ingress routes to Service
- Service forwards to Pod

------------------------------------------------------------

Q) Difference between LoadBalancer Service and Ingress
A)
LoadBalancer:
- One external load balancer per service

Ingress:
- Single load balancer for multiple services

------------------------------------------------------------

Q) What is a Pod?
A)
- Smallest Kubernetes object
- Encapsulates containers

------------------------------------------------------------

Q) What is a Deployment?
A)
- Manages ReplicaSets
- Supports rolling updates and rollback

------------------------------------------------------------

Q) What are ConfigMaps and Secrets?
A)
- ConfigMap: Non-sensitive configuration
- Secret: Sensitive information

============================================================
******MONITORING & OBSERVABILITY******
============================================================

Q) What monitoring tools have you used?
A)
- Amazon CloudWatch
- Prometheus
- Grafana

------------------------------------------------------------

Q) What is Grafana and how do you configure it?
A)
- Visualization and dashboarding tool
- Integrated with Prometheus datasource

------------------------------------------------------------

Q) What is Prometheus?
A)
- Open-source monitoring and alerting system
- Uses pull-based metrics collection

------------------------------------------------------------

Q) What are the components of Prometheus?
A)
- Prometheus Server
- Exporters
- Alertmanager

------------------------------------------------------------

Q) How did you configure Prometheus?
A)
- Installed using Helm
- Configured scrape targets
- Integrated Alertmanager

############################################################
END – DETAILED, NO CONTENT REDUCED
############################################################


```
