# ☁️ AWS Cloud Architecture: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Multi-Tier VPC Networking, EC2 Compute, IMDSv2 Hardening, EBS gp3, S3 Lifecycles, IAM Security Governance, High-Availability Databases (RDS/Aurora), and Cost FinOps.

---

## 📑 Table of Contents
- [AWS Core Concepts & Global Infrastructure](#section-1-aws-core-concepts)
- [IAM Security Governance (Users, Roles, Policies)](#q1-what-is-iam-and-why-does-it-matter-in-devops)
- [VPC Networking: Subnets, Route Tables, IGW, NAT](#q10-what-is-a-vpc-and-why-is-it-important-for-devops)
- [Security Groups vs Network ACLs](#q4-what-is-the-difference-between-a-security-group-and-a-network-acl)
- [EC2 Virtual Servers & Auto Scaling](#q5-what-is-an-auto-scaling-group-and-why-does-a-devops-engineer-care)
- [Storage Architecture: S3 vs EBS](#q9-what-is-s3-and-how-does-it-differ-from-ebs)
- [Databases: RDS Multi-AZ vs DynamoDB vs Aurora](#q8-what-is-the-difference-between-rds-and-dynamodb)
- [CloudWatch Monitoring & Observability](#q7-what-is-cloudwatch-and-how-do-you-use-it-in-devops)
- [Modern AWS Production Standards (gp3, IMDSv2, S3 Endpoints)](#modern-aws-standards)
- [Production Troubleshooting Playbook](#troubleshooting-playbook)

---

SECTION 1: AWS CORE CONCEPTS
Q1. What is IAM and why does it matter in DevOps?
Answer:
IAM (Identity and Access Management) is AWS's service for managing who can access what in your AWS
environment. You create users or groups and assign them specific permissions to particular services like EC2 or
S3.




The key principle is least privilege — you only give users the minimum access they actually need. This is crucial
for security in DevOps environments where multiple team members need different levels of access.
Key points to mention:
Create users, groups, and roles
Attach policies to control access
Principle of least privilege
IAM roles can be assigned to EC2 instances (so apps can access AWS services without hardcoded
credentials)
Q2. What is the difference between IAM User and IAM Role?
Answer:
IAM User — a permanent identity for a person. Has long-term credentials (username/password or access
keys). Used for people who need permanent access.
IAM Role — a temporary identity without credentials. A service or user assumes a role and gets temporary
access keys for a specific task.
DevOps use case: Assign roles to EC2 instances so they can access S3 or DynamoDB without storing credentials
inside the instance. Lambda functions also use roles to access other AWS services.
Q3. What is the difference between Availability Zones and Regions?
Answer:
Region — a completely separate geographic area with its own infrastructure (e.g., US East, Europe West,
Asia Pacific)
Availability Zone (AZ) — isolated data centers within a region. If one AZ goes down, your app in another
AZ stays up.
Why it matters for DevOps:
Deploy across multiple AZs for high availability
Use multiple regions for disaster recovery
Auto Scaling groups and Load Balancers automatically distribute across AZs




Q4. What is the difference between a Security Group and a Network ACL?
Answer:
Feature Security Group Network ACL
Level Instance level Subnet level
State Stateful Stateless
Rules Allow only Allow and Deny
Use case Most common, day-to-day Broad subnet-wide rules
Stateful — allow inbound, response goes out automatically
Stateless — must define both inbound and outbound rules separately
In practice: Security Groups are used most of the time in DevOps.
Q5. What is an Auto Scaling Group and why does a DevOps engineer care?
Answer:
An Auto Scaling Group automatically adds or removes EC2 instances based on demand. You define:
Minimum instances — always running
Maximum instances — cap on scaling
Desired capacity — normal state
Scaling policies — based on CloudWatch metrics like CPU usage
Why DevOps cares:
Maintains performance during high traffic without manual intervention
Reduces costs during low traffic by terminating unused instances
Ensures high availability by replacing unhealthy instances automatically
Q6. What is the difference between ALB and NLB?
Answer:




Feature ALB (Layer 7) NLB (Layer 4)
OSI Layer Layer 7 (Application) Layer 4 (Transport)
Routing Path-based, host-based IP and port-based
Use case Microservices, web apps High performance, low latency
Protocol HTTP/HTTPS TCP/UDP
ALB — looks inside your request, routes based on path or hostname. Use for microservices.
NLB — moves data super fast without inspecting it. Use for extreme speed needs.
In practice: Most DevOps teams use ALB for web applications.
Q7. What is CloudWatch and how do you use it in DevOps?
Answer:
CloudWatch is AWS's native monitoring and observability service. It does three main things:
1. Metrics — tracks CPU, memory, network, disk usage of EC2, RDS, and other AWS services
2. Alarms — set thresholds so if CPU goes above 80%, it triggers an alert or Auto Scaling event
3. Logs — stream and search application and system logs for debugging
In DevOps context:
Set alarms to trigger Auto Scaling
Monitor pipeline health
Debug application errors via log groups
Create dashboards for visibility
Note for DevOpsEngineer: In your Azure DevOps project, you used the LGTM stack (Loki, Grafana, Tempo, Mimir)
— this is essentially an open-source alternative to CloudWatch. Mention this in interviews to show broader
monitoring experience.
Q8. What is the difference between RDS and DynamoDB?
Answer:




Feature RDS DynamoDB
Type Relational (SQL) NoSQL (key-value)
Schema Fixed schema Flexible schema
Scaling Vertical (mostly) Horizontal (automatic)
Use case Structured data, complex queries High-speed, large-scale, simple queries
Examples MySQL, PostgreSQL, Aurora Session data, IoT, gaming leaderboards
Note for DevOpsEngineer: You worked with PostgreSQL (RDS equivalent) in your project. Mention that directly.
Q9. What is S3 and how does it differ from EBS?
Answer:
S3 (Simple Storage Service) — stores data as objects (files) in buckets. Cheap, infinitely scalable, accessed
over HTTP. Used for backups, logs, artifacts, static assets.
EBS (Elastic Block Store) — block storage directly attached to EC2 instances. Faster because it's directly
connected. Used for databases and applications needing fast disk access.
Use S3 for: Storing Docker images, artifacts, logs, backups
Use EBS for: Database storage, OS volumes on EC2
Q10. What is a VPC and why is it important for DevOps?
Answer:
A VPC (Virtual Private Cloud) is your own isolated network in AWS. You control:
Subnets (public and private)
Routing tables
Internet Gateways
Security Groups and ACLs
Traffic flow between resources
DevOps use: Create a VPC with public subnets for load balancers and private subnets for databases. Control
who can access what.




Q11. What is the difference between a Public Subnet and a Private Subnet?
Answer:
Public Subnet — has a route to an Internet Gateway. Instances here can be reached from the internet.
Used for load balancers, bastion hosts.
Private Subnet — no direct route to the internet. Instances here can't be reached externally. Used for
databases, application servers.
Bastion Host — a public EC2 instance you SSH into first, then jump to private instances. Acts as a secure entry
point.
Q12. What is an Elastic IP?
Answer:
An Elastic IP is a static public IP address that stays attached to your instance even if you stop and restart it.
Regular public IPs change when you stop an instance. Elastic IPs are assigned by AWS — you can't choose the
specific number, but once assigned, it stays the same as long as you keep it.
Use for: Web servers, databases, or anything that needs a consistent IP address.
AWS — Deep Dive & Additional Topics
Additional AWS concepts from your notes not covered in Section 1.
A. Cloud Computing — Foundations
Traditional Servers — Drawbacks:
High investment (buy expensive hardware upfront)
High maintenance (dedicated team to manage)
No disaster management
No high availability




No on-demand scaling
Poor resource management
Cloud Computing Definition:
Accessing all computing services (servers, storage, databases, networking) over the internet virtually, on-
demand, and paying only for what you use.
Advantages of Cloud:
Pay as you go — no upfront cost
No maintenance — cloud provider handles hardware
Disaster management — built-in redundancy
High availability — across multiple zones
On-demand services — provision in minutes
Infinite scalability
Types of Cloud:
Deployment Models:
Type Description Example
Public Cloud Resources shared, managed by provider AWS, Azure, GCP
Private Cloud Dedicated resources for one organization On-premise VMware
Hybrid Cloud Mix of public and private AWS + on-premise datacenter
Service Models:
Model Full Form You manage Provider manages Example
IaaS Infrastructure as a
Service
OS, apps, data Hardware, network AWS EC2
PaaS Platform as a Service Apps, data OS, hardware,
runtime
AWS Elastic
Beanstalk
SaaS Software as a Service Nothing (just use
it)
Everything Gmail, Office 365
B. AWS — Overview




Amazon Web Services launched officially in 2006. World's largest cloud platform.
Why AWS?
Cost effective — pay only for what you use
User friendly — console + CLI + SDK
200+ services available
On-demand — provision in minutes
High availability — multiple regions globally
AWS Service Categories:
Category Services
Compute EC2, Lambda, ECS, EKS
Storage S3, EBS, EFS, Glacier
Network VPC, Route 53, CloudFront, Direct Connect
Database RDS, DynamoDB, Aurora, ElastiCache
Security IAM, KMS, WAF, Shield
Monitoring CloudWatch, CloudTrail
Machine Learning SageMaker, Rekognition
DevOps CodePipeline, CodeBuild, CodeDeploy
C. EC2 — Deep Dive
What is EC2?
Elastic Compute Cloud — virtual servers in the cloud. You choose OS, CPU, RAM, storage. Pay per hour or
second.
Connect to EC2:
Method Use for
SSH with key pair Linux instances
Session Manager Linux/Windows without opening port 22




 
RDP Client Windows instances
EC2 Serial Console Emergency access
AMI vs Launch Template:
AMI Launch Template
Contains Software configuration (OS, apps) Hardware configuration (instance type, VPC, SG)
Use Create consistent OS environments Define how instances are launched
D. EBS — Elastic Block Store (Deep Dive)
What is EBS?
Extra storage volumes attached to EC2 instances. Like a hard drive you plug in.
Key Facts:
Default: 8 GB for Linux, 30 GB for Windows
Availability Zone specific — volume and instance must be in same AZ
One volume can attach to ONE instance at a time (standard)
Exception: io1/io2 volumes support Multi-Attach (multiple instances simultaneously)
Max volume size: 16,384 GiB
Root volume can be expanded (can take ~6 hours)
Attach Volume to Windows:
EC2 Console → Attach Volume → Server Manager → File and Storage Services → Disks → Ini
EBS Snapshots:
Backup of a volume at a point in time
Stored in S3 (managed by AWS)
Types: Owned by me / Public / Private
One snapshot per volume
Snapshot of an instance with N volumes creates N snapshots
Can create new volume from snapshot in any AZ




E. S3 — Simple Storage Service (Deep Dive)
Key Facts:
Unlimited storage
Object-based storage (files stored as objects)
Each object max size: 5 TB
Storage space = Bucket (must have unique name globally)
S3 is global (region-specific bucket but globally accessible)
Can be used with or without EC2 (serverless)
S3 Storage Classes:
Class Use Cost
S3 Standard Frequently accessed data Higher
S3 Intelligent-Tiering Unknown access patterns Auto optimizes
S3 Standard-IA Infrequently accessed Lower storage, retrieval fee
S3 One Zone-IA Single AZ, infrequent Cheapest IA, no redundancy
S3 Glacier Archives, rare access Very cheap
S3 Glacier Deep Archive Long-term archives Cheapest
S3 Snowball On-premise data transfer Physical device
Static Website Hosting on S3:
Upload files to bucket (all files same bucket)
→ Properties → Static Web Hosting → Enable
→ Permissions → Unblock public access
→ Bucket Policy → Add GetObject for * (all)
Important S3 Rules:
Replication Rule — copies files to another storage class, original deleted from Standard
Lifecycle Rule — doesn't copy but deletes files after scheduled time period
Cross Region Replication — copy objects from bucket in one region to bucket in another region




F. Auto Scaling
Scaling Types:
Type How
Vertical Scaling Increase capacity of existing server (bigger instance)
Horizontal Scaling Add more servers to distribute load
Auto Scaling Group:
1. Create Launch Template (defines instance config)
2. Create Auto Scaling Group
3. Define: min, max, desired capacity
4. Set scaling policies (based on CloudWatch metrics)
G. CloudWatch — Deep Dive
What is CloudWatch?
AWS's native monitoring service. Collects metrics, logs, and events from AWS resources.
CloudWatch States:
Icon State Meaning
✅ OK Metric is within threshold
🚥 INSUFFICIENT_DATA Not enough data yet
⚠ ALARM Metric crossed threshold
How to Set a CloudWatch Alarm:
CloudWatch → Alarms → Create Alarm
→ Select Metric (EC2 CPU, S3 requests, etc.)
→ Define threshold (e.g., CPU > 80%)
→ Define action (send SNS notification, trigger Auto Scaling)
→ Set alarm name
CloudWatch + SNS + Lambda:




S3 Bucket → Lambda trigger → Lambda runs → SNS notification
CloudWatch alarm → SNS topic → Email/SMS notification
H. Lambda Function — Serverless Computing
What is Lambda?
Run code without managing servers. You just upload code, AWS runs it when triggered.
Your Lambda Example (Start/Stop EC2):
import boto3
ec2 = boto3.client('ec2')
def lambda_handler(event, context):
    instance_id = 'i-xxxxxxxxxxxxxxxx'
    
    try:
        # Check current state
        response = ec2.describe_instances(InstanceIds=[instance_id])
        state = response['Reservations'][0]['Instances'][0]['State']['Name']
        
        if state == 'stopped':
            ec2.start_instances(InstanceIds=[instance_id])
            print(f"Started EC2 instance {instance_id}")
        elif state == 'running':
            ec2.stop_instances(InstanceIds=[instance_id])
            print(f"Stopped EC2 instance {instance_id}")
        else:
            print(f"Instance in {state} state, no action taken")
            
    except Exception as e:
        print(f"Error: {str(e)}")
Lambda — Stop All Running Instances in a Region:
import boto3
def lambda_handler(event, context):
    region = 'us-east-1'
    ec2 = boto3.client('ec2', region_name=region)
    




    # Get all running instances
    instances = ec2.describe_instances(
        Filters=[{'Name': 'instance-state-name', 'Values': ['running']}]
    )
    
    # Stop each running instance
    for reservation in instances['Reservations']:
        for instance in reservation['Instances']:
            instance_id = instance['InstanceId']
            ec2.stop_instances(InstanceIds=[instance_id])
            print(f"Stopped instance: {instance_id}")
    
    print("All EC2 instances stopped.")
I. VPC Peering
What is VPC Peering?
A networking connection between two VPCs that allows routing traffic using private IP addresses. Instances in
peered VPCs can communicate as if they're in the same network.
Key facts:
No single point of failure
Traffic doesn't traverse the internet
Can peer VPCs in same account, different accounts, different regions
Not transitive — if A peers B and B peers C, A cannot reach C through B
VPC A (172.31.0.0/16) ←──── Peering ──── ▶  VPC B (190.0.0.0/23)
After peering:
- Add route in VPC A's route table: 190.0.0.0/23 → Peering connection
- Add route in VPC B's route table: 172.31.0.0/16 → Peering connection
J. Bastion Host (Jump Host)
What is a Bastion Host?
A special purpose server in a public subnet used as a secure entry point to access instances in private subnets.
Architecture:




Internet
    ↓
Bastion Host (Public Subnet — has public IP)
    ↓ SSH with private key
Private Instance (Private Subnet — no public IP)
How to access private instance:
# Step 1: Copy private key to bastion host
scp -i key.pem key.pem ec2-user@bastion-public-ip:~
# Step 2: SSH to bastion
ssh -i key.pem ec2-user@bastion-public-ip
# Step 3: From bastion, SSH to private instance
ssh -i key.pem ec2-user@private-instance-private-ip
Public Subnet: Has Internet Gateway, public IP, public route table (0.0.0.0/0 → IGW)
Private Subnet: No public IP, private route table (0.0.0.0/0 → NAT Gateway)
NAT Gateway: Allows outbound traffic from private subnet, blocks inbound
K. Cloud Shell
AWS CloudShell is a browser-based CLI in the AWS Console. Use it to manage AWS services through commands
without installing AWS CLI locally. Pre-authenticated with your console credentials.


---

## 🚀 Modern AWS Architecture Standards

### 1. Mandatory IMDSv2 Token Security
```bash
# Fetch temporary IMDSv2 token
TOKEN=$(curl -s -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 60")
# Retrieve metadata securely
curl -s -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/instance-id
```

### 2. EBS gp3 Volume Standard
* Always provision `gp3` instead of legacy `gp2`. gp3 provides baseline 3,000 IOPS and 125 MB/s throughput independently of disk size, at 20% lower cost.

### 3. Free S3 Gateway VPC Endpoint
* Avoid paying $0.045/GB NAT Gateway data transfer fees for S3 traffic. Add a free **S3 Gateway Endpoint** to your private route tables.
