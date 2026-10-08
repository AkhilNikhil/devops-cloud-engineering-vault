# 📘 173 Q&A Complete Interview Guide

> *High-yield guide extracted from `Akhil_173QA_Complete_Guide.pdf` for mobile & web GitHub viewing.*

---

## Section / Page 1

AKHIL B M 
Complete Interview Q&A Guide 
AWS + Azure + Docker — Q1 to Q173 
Every question answered. Study this. Ace the interview. 
 
 
Cloud Basics EC2 & EBS S3 & VPC IAM & SNS Databases Azure+Docker

## Section / Page 2

☁️ CLOUD BASICS (Q1–Q5) 
 
Q1. What is cloud computing and what are its advantages over traditional servers? 
Cloud computing = accessing computing services (servers, storage, databases, networking) over the 
internet instead of owning physical hardware. 
  
Traditional Server Problems: 
❌ High upfront investment (buy hardware) 
❌ High maintenance (power, cooling, repairs) 
❌ Cannot scale quickly | ❌ Resources sit idle when not needed 
  
Cloud Advantages: 
✅ Pay as you go — only pay for what you use 
✅ No maintenance — provider handles hardware 
✅ High availability — runs across multiple data centers 
✅ On-demand scaling — add/remove resources instantly 
✅ Disaster recovery — built in | ✅ Global reach — deploy anywhere in minutes 
 
Q2. What are the types of cloud deployment models? 
Public Cloud: Infrastructure owned and managed by cloud provider. 
Shared across multiple customers (but isolated). 
Examples: AWS, Azure, Google Cloud. Use when: most workloads, cost effective. 
  
Private Cloud: Infrastructure dedicated to one organization. 
More control and security. Examples: On-premise VMware, OpenStack. 
Use when: sensitive data, compliance requirements. 
  
Hybrid Cloud: Combination of public and private cloud. 
Example: Database on-premise, web app on AWS. 
Use when: gradual migration, sensitive + non-sensitive workloads. 
 
Q3. What is the difference between IaaS, PaaS, and SaaS? 
IaaS — Infrastructure as a Service: 
Provider gives: hardware, networking, virtualization. 
You manage: OS, runtime, apps, data. 
Example: AWS EC2, Azure VM. 
  
PaaS — Platform as a Service: 
Provider gives: hardware + OS + runtime. 
You manage: apps and data only. 
Example: AWS Elastic Beanstalk, Heroku. 
  
SaaS — Software as a Service: 
Provider gives: everything including the application. 
You manage: nothing (just use it). 
Example: Gmail, Salesforce, Office 365. 
  
Simple analogy: 
IaaS = Renting a kitchen (you cook everything) 
PaaS = Ordering meal kit (ingredients given, you cook) 
SaaS = Ordering from restaurant (everything done for you)

## Section / Page 3

Q4. What is AWS and when was it officially released? 
AWS = Amazon Web Services. 
World's largest cloud computing platform with 200+ services. 
  
Officially released: 2006. Headquarters: Seattle, USA (Amazon subsidiary). 
Market leader: over 30% market share. 
  
Key facts: 
- Pay-as-you-go pricing model 
- Available in multiple regions worldwide 
- Used by Netflix, Airbnb, NASA, and millions of companies 
 
Q5. Name at least 8 AWS service categories. 
1. Compute         → EC2, Lambda, ECS, EKS 
2. Storage         → S3, EBS, EFS, Glacier 
3. Networking      → VPC, Route53, CloudFront, ELB 
4. Database        → RDS, DynamoDB, Aurora, ElastiCache 
5. Security        → IAM, KMS, WAF, Shield 
6. Monitoring      → CloudWatch, CloudTrail 
7. Machine Learning → SageMaker, Rekognition, Polly 
8. Big Data        → EMR, Athena, Kinesis, Redshift 
9. Messaging       → SNS, SQS, SES 
10. DevOps         → CodePipeline, CodeBuild, CodeDeploy

## Section / Page 4

☁️ EC2 — Elastic Compute Cloud (Q6–Q17) 
 
Q6. What is EC2 and what does it stand for? 
EC2 = Elastic Compute Cloud. 
A virtual server in the cloud — pay only for time you use. 
  
Key features: 
- Choose OS: Linux, Windows, macOS 
- Choose size: CPU, RAM, storage 
- Launch in minutes | Pay per hour or per second 
- Can stop, start, resize anytime 
  
In your project: Used EC2 as worker nodes in Kubernetes cluster via kOps on AWS. 
 
Q7. What are the different ways to connect to a Linux EC2 instance? 
1. SSH using Key Pair (most common): 
   ssh -i "mykey.pem" ec2-user@<public-ip> 
   Need: port 22 open in Security Group + .pem key file  
  
2. EC2 Instance Connect: 
   Browser-based SSH directly from AWS Console.  
   No key pair needed. Works for Amazon Linux and Ubuntu only. 
  
3. Session Manager (SSM): 
   No SSH, no open ports needed!  
   Connect through AWS Systems Manager. Most secure.  
  
4. EC2 Serial Console: 
   For troubleshooting when instance is unreachable.  
 
Q8. What are the different ways to connect to a Windows EC2 instance? 
1. RDP — Remote Desktop Protocol (most common): 
   Download .rdp file from AWS Console.  
   Need: port 3389 open in Security Group.  
   Need to decrypt password using key pair.  
  
2. Session Manager (SSM): 
   No RDP, no open ports needed.  
   Browser-based access from AWS Console. More secure option.  
  
3. EC2 Serial Console: 
   For troubleshooting unresponsive instances.  
 
Q9. What is an AMI and how is it different from a Launch Template? 
AMI — Amazon Machine Image: 
- Contains SOFTWARE configuration 
- OS + pre-installed applications + settings 
- Like a snapshot of a server's software state 
- Example: Amazon Linux 2 AMI, Ubuntu 22.04 AMI 
  
Launch Template: 
- Contains HARDWARE configuration

## Section / Page 5

- Instance type, VPC, subnet, security group, key pair 
- Does NOT include the OS/software — that comes from AMI 
  
Simple analogy: 
AMI            = What software is on the computer 
Launch Template = What specs (RAM, CPU) the computer has 
 
Q10. What are EC2 instance types and when do you use each family? 
t (General Purpose — Burstable): t2.micro, t3.medium 
→ web servers, dev/test, small apps 
  
m (General Purpose — Standard): m5.large 
→ application servers, mid-size databases 
  
c (Compute Optimized): c5.xlarge 
→ batch processing, gaming, ML inference 
  
r (Memory Optimized): r5.2xlarge 
→ in-memory databases, Redis, SAP HANA 
  
p/g (GPU Optimized): p3.2xlarge 
→ machine learning training, graphics rendering 
  
i (Storage Optimized): i3.xlarge 
→ NoSQL databases, high I/O workloads 
 
Q11. What is a Key Pair and why is it needed? 
Key Pair = set of public and private cryptographic keys. 
Used to securely connect to an EC2 instance. 
  
- Public key: stored on the EC2 instance by AWS 
- Private key (.pem file): downloaded by you — KEEP IT SAFE! 
  
ssh -i "mykey.pem" ec2-user@<public-ip> 
  
Important rules: 
❌ Never share your .pem file 
✅ Set correct permissions: chmod 400 mykey.pem 
❌ If lost, you cannot recover it — create a new one 
 
Q12. What is an Elastic IP and why do we use it? 
Elastic IP = static public IP address assigned to EC2 permanently. 
  
Problem: When you stop and start EC2, public IP CHANGES every time! 
DNS records, firewall rules break. 
  
Solution — Elastic IP: 
- Fixed IP that stays same even after restart 
- Can be moved from one instance to another instantly (failover) 
  
Important: 
✅ Free when ATTACHED to a running instance

## Section / Page 6

❌ Charged when NOT attached (AWS penalizes unused IPs) 
 
Q13. What is the difference between stopping and terminating an EC2 instance? 
Stopping: 
- Instance is shut down (like turning off a PC) 
- EBS root volume is PRESERVED — data is safe 
- You can start it again later 
- NOT charged for compute while stopped 
  
Terminating: 
- Instance is PERMANENTLY deleted 
- EBS root volume is DELETED by default 
- Cannot be recovered — all data is LOST! 
  
Simple analogy: 
Stop      = Putting laptop to sleep 
Terminate = Throwing laptop in trash 
 
Q14. What is EC2 User Data? 
EC2 User Data = script that runs automatically when EC2 launches for the FIRST time. 
  
Use to automate setup tasks on first boot: 
- Install software | Update packages | Start services 
  
Example User Data script: 
#!/bin/bash 
yum update -y 
yum install -y httpd 
systemctl start httpd 
systemctl enable httpd 
  
Key facts: 
- Runs ONLY ONCE at first launch | Runs as root user 
- Useful for automation — no manual setup needed! 
 
Q15. What is Auto Scaling and how does it work? 
Auto Scaling automatically adds or removes EC2 instances based on demand. 
  
How it works: 
1. Define: Min=2, Desired=4, Max=10 capacity 
2. CloudWatch monitors metrics (CPU, memory) 
3. When CPU > 70% for 5 min → Scale Out (add instances) 
4. When CPU < 30% for 10 min → Scale In (remove instances) 
  
Benefits: 
✅ Cost efficient — pay only for what you need 
✅ High availability — always enough capacity 
✅ No manual intervention needed 
  
Scaling Policies: 
- Target Tracking: maintain CPU at 50% 
- Step Scaling: add 2 instances if CPU > 70%

## Section / Page 7

- Scheduled: add instances every day at 9AM 
 
Q16. What is the difference between vertical and horizontal scaling? 
Vertical Scaling (Scale Up): 
- Increase size of existing instance 
- Example: t2.micro → t2.large (more CPU and RAM) 
- Has a LIMIT | Requires DOWNTIME to resize 
  
Horizontal Scaling (Scale Out): 
- Add MORE instances to distribute the load 
- Example: 2 servers → 10 servers 
- No limit | No downtime (traffic via load balancer) 
- More resilient — if one fails, others keep running 
  
AWS Auto Scaling = Horizontal scaling 
  
Simple analogy: 
Vertical   = Making one person work harder 
Horizontal = Hiring more people to share the work 
 
Q17. What is a Launch Template? 
Launch Template = saved configuration for launching EC2 instances. 
Stores all hardware and network settings so you don't configure every time. 
  
What it contains: 
- AMI ID | Instance type | Key pair 
- Security groups | Network settings (VPC, subnet) 
- User Data script | IAM role | Storage settings 
  
Benefits: 
✅ Consistency — every instance launched same way 
✅ Reusability — use same template across environments 
✅ Required for Auto Scaling Groups 
✅ Supports versioning — maintain v1, v2, v3 
  
AMI = Software blueprint | Launch Template = Config blueprint

## Section / Page 8

☁️ EBS — Elastic Block Store (Q18–Q25) 
 
Q18. What is EBS and what does it stand for? 
EBS = Elastic Block Store. 
Block storage attached to EC2 — like an external hard drive. 
  
Key facts: 
- Attached directly to ONE EC2 instance 
- Persists independently (data survives stop/start) 
- Exists within a SINGLE Availability Zone 
- Used for: OS storage, databases, application data 
  
In your project: EBS as persistent storage for PostgreSQL in Kubernetes. 
Each StatefulSet pod got its own EBS volume. 
 
Q19. What is the default storage size for Linux and Windows EC2 instances? 
Linux EC2 instance:   8 GB default root volume 
Windows EC2 instance: 30 GB default root volume 
  
These are EBS root volumes attached at launch. 
You can increase the size when launching. 
  
Note: 
- Root volume can be expanded after creation 
- Cannot DECREASE size (no shrinking) 
- Maximum EBS volume size: 16,384 GiB (16 TiB) 
 
Q20. Can one EBS volume be attached to multiple instances? 
Standard EBS volumes: NO — one volume to ONE instance at a time. 
  
Exception — EBS Multi-Attach: 
- Available for io1 and io2 volume types ONLY 
- Allows ONE volume to multiple instances in SAME AZ 
- Maximum 16 instances at a time 
  
So: 
✅ One instance → multiple volumes: ALWAYS possible 
✅ One volume → multiple instances: Only with Multi-Attach (io1/io2, same AZ) 
 
Q21. What is EBS Multi-Attach and when is it used? 
EBS Multi-Attach = single EBS volume (io1 or io2) attached to 
multiple EC2 instances simultaneously in the same AZ. 
  
When to use: 
- Clustered database applications (Oracle RAC) 
- Applications requiring concurrent write access 
  
Limitations: 
- Only io1 and io2 volume types 
- Maximum 16 instances at a time

## Section / Page 9

- All instances must be in the SAME AZ 
- Applications must handle concurrent write conflicts 
 
Q22. What is an EBS Snapshot and what are its types? 
EBS Snapshot = backup of an EBS volume stored in S3. 
Captures current state of the volume at a point in time. 
  
Types: 1. Owned by Me | 2. Public (shared by AWS) | 3. Private (specific accounts) 
  
Key facts: 
- Snapshots are INCREMENTAL (only changed blocks saved) 
- Stored in S3 automatically 
- Can create new EBS volume from a snapshot 
- Can copy snapshot to another region (for DR) 
  
Uses: Disaster recovery | Migrating volumes between AZs | Testing copies 
 
Q23. What is the maximum size of an EBS volume? 
Maximum size: 16,384 GiB (16 TiB) — approximately 16 terabytes. 
  
Notes: 
- You CAN increase size after creation 
- You CANNOT decrease size (no shrinking) 
- Expanding a 1 TiB volume can take around 6 hours 
 
Q24. Is EBS AZ specific? 
YES — EBS is Availability Zone SPECIFIC. 
  
An EBS volume in us-east-1a can ONLY be attached to EC2 in us-east-1a. 
CANNOT attach to instance in us-east-1b! 
  
To move EBS to another AZ: 
1. Create Snapshot | 2. Create new volume from snapshot in target AZ 
3. Attach new volume to instance in that AZ 
  
This is why EBS as K8s persistent storage is a LIMITATION! 
If AZ goes down → volume and all data become inaccessible. 
  
Production fix: Use EFS instead (Multi-AZ). 
 
Q25. What are the different EBS volume types and when do you use each? 
SSD-based (for random I/O): 
gp2/gp3 — General Purpose SSD: 
  Balanced performance and cost. Default for most workloads.  
  Use for: OS volumes, web servers, dev environments.  
  
io1/io2 — Provisioned IOPS SSD: 
  Highest performance, low latency.  
  Use for: production databases (MySQL, PostgreSQL, Oracle).  
  io2 supports Multi-Attach.

## Section / Page 10

HDD-based (for sequential I/O): 
st1 — Throughput Optimized HDD: Use for: big data, log processing. 
sc1 — Cold HDD: Lowest cost. Use for: infrequent access, archives. 
  
Summary: 
gp2/gp3  → default, most workloads 
io1/io2  → high performance databases 
st1      → big data, logs | sc1 → cheapest, cold storage

## Section / Page 11

☁️ S3 — Simple Storage Service (Q26–Q37) 
 
Q26. What is S3 and what does it stand for? 
S3 = Simple Storage Service. 
Object-based storage — store unlimited amounts of data in the cloud. 
  
Key facts: 
- Store any type of file (images, videos, code, backups) 
- Accessed over HTTP/HTTPS — NOT attached to an instance 
- Global service — not tied to a specific AZ 
- Highly durable — 99.999999999% (11 nines) 
- Serverless — works without EC2 
  
In your project: kOps used S3 to store cluster state file. 
s3://akhil-kops-state-store 
 
Q27. What is a Bucket and what is an Object in S3? 
Bucket: 
- Container for storing objects in S3 
- Bucket name must be GLOBALLY UNIQUE (across all AWS accounts) 
- Region-specific (you choose which region) 
  
Object: 
- The actual file stored inside a bucket 
- Has: Key (path/name), Value (data), Metadata 
- Maximum size: 5 TB 
  
Example: 
Bucket: akhil-devops-bucket 
Object: builds/2024/myapp.war 
URL: s3://akhil-devops-bucket/builds/2024/myapp.war 
 
Q28. What is the maximum size of a single object in S3? 
Maximum size of a single object: 5 TB (5 terabytes) 
  
For objects larger than 5 GB: 
- Must use Multipart Upload 
- AWS recommends multipart for anything over 100 MB 
- Splits file into parts, uploads in parallel, then assembles 
 
Q29. Is S3 AZ specific or global? 
S3 is a GLOBAL service — NOT AZ specific. 
  
However: 
- When you create a bucket, you choose a REGION (e.g., us-east-1) 
- Data is automatically replicated across multiple AZs WITHIN that region 
- For cross-region: use Cross Region Replication (CRR) 
  
Compare with EBS: 
EBS → AZ specific (only one AZ)

## Section / Page 12

S3  → Regional (replicated across AZs in region) 
 
Q30. What are the S3 storage classes and when do you use each? 
S3 Standard: Frequent access. Most expensive. 
  Use for: active application data, frequently accessed files.  
  
S3 Standard-IA (Infrequent Access): Less frequent (monthly). Cheaper but retrieval fee. 
  Use for: backups, disaster recovery files.  
  
S3 One Zone-IA: Infrequent, stored in ONE AZ only. Risk: if AZ down, data lost. 
  Use for: non-critical, reproducible data. 
  
S3 Intelligent-Tiering: AWS auto-moves objects between tiers based on usage. 
  Use for: unpredictable access patterns.  
  
S3 Glacier: Archive storage. Retrieval: minutes to hours. Very cheap. 
  Use for: data you rarely access but must keep.  
  
S3 Glacier Deep Archive: Cheapest of all. Retrieval: 12+ hours. 
  Use for: long-term compliance archives (7+ years).  
  
Memory trick: Standard → IA → One Zone → Glacier → Deep Archive 
(Most expensive → Cheapest) 
 
Q31. What is S3 Versioning? 
S3 Versioning keeps multiple versions of the same object. 
Every upload with same name → saves as new version (no overwriting). 
  
Benefits: 
- Recover from accidental deletion or overwrite 
- See full history of changes | Restore to any previous version 
  
Example: 
Upload myapp.war → Version 1 
Upload myapp.war again → Version 2 (V1 still exists) 
Delete myapp.war → Only adds delete marker (data still there!) 
Restore → Remove delete marker to bring it back 
  
Important: 
- Once enabled, versioning CANNOT be fully disabled (only suspended) 
- Increases storage cost (all versions stored) 
 
Q32. What is a Lifecycle Rule in S3? 
A Lifecycle Rule automatically transitions objects between storage classes 
or deletes them after a specified time period. 
  
Examples: 
- After 30 days → Move from Standard to Standard-IA 
- After 90 days → Move to Glacier 
- After 365 days → Delete permanently 
  
Use cases: 
- Reduce storage costs for aging data

## Section / Page 13

- Automatically clean up old logs 
- Comply with data retention policies 
  
Lifecycle Rule   → Moves or deletes files over time 
Replication Rule → Copies files to another bucket/region 
 
Q33. What is a Replication Rule in S3? 
A Replication Rule automatically copies objects from one S3 bucket to another. 
  
Types: 
- SRR (Same Region Replication) — replicate within same region 
- CRR (Cross Region Replication) — replicate to another region 
  
Requirements: 
- Versioning must be enabled on BOTH buckets 
- Replication is for NEW objects (existing NOT auto-replicated) 
  
Use cases: 
- Disaster recovery across regions 
- Compliance requirements | Low latency for users 
 
Q34. What is Cross Region Replication in S3? 
CRR = automatically copies objects from S3 bucket in one region 
to another S3 bucket in a DIFFERENT region. 
  
Example: 
Source: my-bucket in us-east-1 (N. Virginia) 
Destination: my-bucket-backup in ap-south-1 (Mumbai) 
Every new object uploaded → automatically copied to destination. 
  
Requirements: 
- Versioning must be enabled on BOTH buckets 
- Buckets must be in DIFFERENT regions 
- Must set up IAM role with replication permissions 
 
Q35. How do you host a static website on S3? 
Steps: 
1. Create S3 bucket (name = your domain, e.g., mywebsite.com) 
2. Upload all website files (index.html, style.css, images) 
3. Enable Static Website Hosting: 
   Bucket → Properties → Static website hosting → Enable  
   Set index document: index.html  
4. Make bucket publicly accessible: 
   Permissions → Block Public Access → Disable all blocks  
5. Add Bucket Policy to allow public read: 
   
{"Effect":"Allow","Principal":"*","Action":"s3:GetObject","Resource":"arn:aws:s3:::mybucket/*"}  
6. Access via S3 website URL: 
   http://mybucket.s3-website-us-east-1.amazonaws.com 
  
Optional: Point your domain (Route 53) to this URL.

## Section / Page 14

Q36. What is a Bucket Policy? 
A Bucket Policy = JSON-based access control attached to S3 bucket. 
Defines who can access the bucket and what actions they can perform. 
  
Example: 
{"Version":"2012-10-17","Statement":[{"Effect":"Allow","Principal":"*",  
"Action":"s3:GetObject","Resource":"arn:aws:s3:::my-bucket/*"}]} 
  
Key elements: 
- Effect: Allow or Deny 
- Principal: Who (* = everyone, or specific user/account) 
- Action: What they can do (s3:GetObject, s3:PutObject) 
- Resource: Which bucket or objects 
  
Uses: Static website | Cross-account access | Force HTTPS only 
 
Q37. How did you use S3 in your kOps project? 
Used S3 as the kOps STATE STORE. 
kOps stores cluster configuration and state in S3. 
Every create/update/validate reads from and writes to this S3 bucket. 
  
Steps: 
1. Created S3 bucket: s3://akhil-kops-state-store 
export KOPS_STATE_STORE=s3://akhil-kops-state-store 
  
2. Created cluster (config saved to S3): 
kops create cluster --name=myapp.k8s.local --zones=us-east-1a 
  
3. Applied cluster (reads config from S3): 
kops update cluster --name=myapp.k8s.local --yes 
  
4. Validated cluster: 
kops validate cluster 
  
Why S3: Persistent and durable | Accessible from anywhere | Version history

## Section / Page 15

☁️ VPC — Virtual Private Cloud (Q38–Q52) 
 
Q38. What is VPC and what does it stand for? 
VPC = Virtual Private Cloud. 
Your own isolated private network inside AWS. 
  
Before VPC: All AWS customers shared the same network. Security nightmare! 
  
With VPC: 
- Each customer gets their own isolated private network 
- You fully control: IP ranges, subnets, routing, firewalls 
- Resources inside cannot be reached unless you allow it 
  
In your project: kOps automatically created a VPC for your Kubernetes cluster. 
 
Q39. What are the 4 main components of a VPC? 
1. Subnet: 
   Division of VPC IP range into smaller segments.  
   Can be Public (internet access) or Private (no internet).  
   Each subnet exists in ONE Availability Zone.  
  
2. Route Table: 
   Controls where network traffic is directed.  
   Public subnet → route to IGW | Private subnet → route to NAT.  
  
3. Internet Gateway (IGW): 
   Connects VPC to public internet.  
   Allows BOTH inbound and outbound traffic.  
  
4. NAT Gateway: 
   Allows private subnet instances to access internet.  
   Blocks ALL inbound connections from internet.  
   Sits in public subnet, has Elastic IP.  
 
Q40. What is the difference between a Public Subnet and a Private Subnet? 
Public Subnet: 
- Has route to Internet Gateway → direct internet (in + out) 
- Instances can have public IP addresses 
- Used for: Load balancers, Bastion hosts 
  
Private Subnet: 
- Does NOT have route to Internet Gateway 
- Instances have only PRIVATE IP addresses 
- Internet access via NAT Gateway (OUTBOUND ONLY) 
- Used for: Databases, application servers, backend services 
  
Security principle: Put anything sensitive in Private subnet! 
  
In your project: K8s worker nodes → Private subnet (security) 
They access internet through NAT → to pull Docker images. 
 
Q41. What is an Internet Gateway and what does it do?

## Section / Page 16

Internet Gateway (IGW) = connects your VPC to the public internet. 
  
How it works: 
- Attached to a VPC (one IGW per VPC) 
- Allows BOTH inbound and outbound traffic 
- Performs NAT for instances with public IPs 
  
Without IGW: VPC is completely isolated from internet. 
With IGW: Public subnets can send and receive internet traffic. 
  
To make subnet public: 
1. Attach IGW to VPC 
2. Add route: Destination: 0.0.0.0/0 → Target: Internet Gateway 
  
IGW is FREE — no additional cost. 
 
Q42. What is a NAT Gateway and how is it different from Internet Gateway? 
NAT Gateway: Allows PRIVATE subnet instances to access internet. 
- Blocks ALL inbound connections (OUTBOUND ONLY) 
- Sits in PUBLIC subnet | Has Elastic IP | Costs money 
  
Internet Gateway: Connects PUBLIC subnet to internet. 
- Allows BOTH inbound and outbound traffic | FREE 
  
Comparison: 
Direction: IGW = Both ways | NAT = Outbound only 
Used by:   IGW = Public subnets | NAT = Private subnets 
Inbound from internet: IGW = Yes | NAT = No 
Cost: IGW = Free | NAT = Paid (hourly + data) 
  
Analogy: 
Internet Gateway = Main entrance door (can come in and go out) 
NAT Gateway      = Exit only door (you can leave, nobody can enter) 
 
Q43. What is a Bastion Host and why do we need it? 
Bastion Host (Jump Host) = EC2 instance in PUBLIC subnet 
used as secure gateway to SSH into PRIVATE subnet instances. 
  
Problem: Private subnet instances have NO public IP. 
Cannot SSH directly from your laptop! ❌ 
  
Solution: 
Step 1: SSH into Bastion Host (it has a public IP) 
Step 2: From Bastion, SSH into private instance 
  
Your Laptop → SSH → Bastion Host → SSH → Private Server 
  
Security benefits: 
- Only ONE server (Bastion) exposed to internet 
- All other servers completely hidden 
- Can restrict Bastion access to your IP only 
  
Bastion Host ≠ NAT Gateway

## Section / Page 17

Bastion = Admin SSH access | NAT = Private servers access internet 
 
Q44. What is VPC Peering? 
VPC Peering = networking connection between two VPCs that allows them 
to communicate as if they were in the same network. 
  
Example: 
VPC-A (10.0.0.0/16) ←→ VPC-B (172.31.0.0/16) 
Resources use PRIVATE IP addresses — no internet needed! 
  
Use cases: 
- Connect application VPC with database VPC 
- Share services between different AWS accounts 
  
Requirements: 
- VPCs must NOT have overlapping CIDR blocks 
- Peering is NON-TRANSITIVE: 
  If A peers with B, and B peers with C,  
  A CANNOT talk to C (must peer directly)  
 
Q45. What is the difference between Security Group and NACL? 
Security Group: 
- Works at INSTANCE level (attached to EC2) 
- STATEFUL — response is automatically allowed 
- ALLOW rules ONLY | All rules evaluated TOGETHER 
  
NACL (Network Access Control List): 
- Works at SUBNET level (attached to subnet) 
- STATELESS — must define BOTH inbound AND outbound 
- ALLOW and DENY rules both supported 
- Rules evaluated IN ORDER by rule number (lowest first) 
  
Analogy: 
Security Group = Guard at your house door 
NACL           = Guard at society/colony gate 
  
In your project: 
Port 80 → Allow (Apache) | Port 22 → Allow (SSH) 
Port 7789/8888 → Block (Tomcat internal only) 
 
Q46. Is Security Group stateful or stateless? 
Security Group is STATEFUL. 
  
What stateful means: 
If you allow inbound traffic on port 80, 
the response traffic is AUTOMATICALLY allowed outbound 
WITHOUT needing a separate outbound rule. 
  
Example: 
- User sends request to server on port 80 ✅ 
- Server sends response back 
- Response is AUTOMATICALLY allowed — no outbound rule needed ✅

## Section / Page 18

Security Group tracks connection state. 
 
Q47. Is NACL stateful or stateless? 
NACL is STATELESS. 
  
What stateless means: 
If you allow inbound traffic on port 80, 
you MUST ALSO add a separate outbound rule for the response. 
  
Example: 
- User sends request on port 80 → NACL checks inbound → Yes ✅ 
- Server sends response on ephemeral port (e.g., 32768) 
- NACL checks: Is outbound port 32768 allowed? → NO ❌ BLOCKED! 
  
So with NACL you must: 
- Allow inbound port 80 (for request) 
- Allow outbound ports 1024-65535 (for response — ephemeral ports) 
 
Q48. How are rules evaluated in Security Group vs NACL? 
Security Group — All rules evaluated TOGETHER: 
- If ANY rule allows the traffic → it is allowed 
- No concept of rule priority or order 
  
Example: 
Rule 1: Allow port 80 | Rule 2: Allow port 443 | Rule 3: Allow port 22 
Traffic on port 80 → all 3 rules checked → Rule 1 allows it ✅ 
  
NACL — Rules evaluated IN ORDER by rule number: 
- Rules numbered (100, 200, 300...) 
- Evaluated from LOWEST number to HIGHEST 
- First matching rule wins — stops evaluating 
  
Example: 
Rule 100: Allow port 80 | Rule 200: Deny port 80 
Traffic on port 80 → Check Rule 100: matches! → ALLOW ✅ 
(Rule 200 is NEVER reached) 
 
Q49. What ports did you allow in your project and why? 
In my Azure DevOps + Tomcat + Reverse Proxy project: 
  
Allowed (OPEN): 
- Port 80  → Apache Reverse Proxy (public HTTP traffic) 
- Port 22  → SSH access for admin/DevOps deployment 
  
Blocked/Internal only: 
- Port 7789 → Tomcat 1 (blocked by UFW — internal only) 
- Port 8888 → Tomcat 2 (blocked by UFW — internal only) 
- Port 5432 → PostgreSQL database (completely internal) 
  
Why this design: 
- Users access ONLY Port 80 (Apache)

## Section / Page 19

- Apache routes to Tomcat internally 
- Tomcat and DB NEVER exposed to internet 
- Single entry point = better security = Reverse Proxy pattern! 
 
Q50. What is a Route Table and what does it do? 
Route Table = set of rules that determines where network traffic is directed. 
  
Public subnet route table: 
Destination: 10.0.0.0/16 → Target: local (VPC-internal) 
Destination: 0.0.0.0/0   → Target: igw-xxxxxxxx (internet → IGW) 
  
Private subnet route table: 
Destination: 10.0.0.0/16 → Target: local (VPC-internal) 
Destination: 0.0.0.0/0   → Target: nat-xxxxxxxx (internet → NAT) 
  
Key facts: 
- Every subnet must be associated with ONE route table 
- Multiple subnets can share the same route table 
- The "local" route is always present — allows all VPC resources to talk 
 
Q51. What is a CIDR block? 
CIDR = Classless Inter-Domain Routing. 
A way to define a range of IP addresses. 
  
Format: IP_Address/Prefix_Length 
Example: 10.0.0.0/16 
/16 means first 16 bits are fixed → 65,536 possible IPs 
  
Common CIDR examples: 
10.0.0.0/8   → 16.7 million IPs (Class A) 
10.0.0.0/16  → 65,536 IPs      (common VPC size) 
10.0.0.0/24  → 256 IPs         (common subnet size) 
10.0.0.1/32  → exactly 1 IP    (specific host) 
0.0.0.0/0    → all IPs         (internet/everywhere) 
  
In your project: kOps created VPC with CIDR 172.20.0.0/16. 
 
Q52. What is the default VPC in AWS? 
AWS automatically creates a Default VPC in every region when you create an account. 
  
Properties: 
- CIDR: 172.31.0.0/16 
- Public subnet in EACH Availability Zone 
- Internet Gateway attached 
- Auto-assign public IP enabled 
  
Best practices: 
❌ NEVER use Default VPC for production! 
✅ Create custom VPC with proper public/private subnets 
✅ Default VPC is fine for learning and testing only

## Section / Page 20

☁️ IAM — Identity and Access Management (Q53–Q64) 
 
Q53. What is IAM and what does it stand for? 
IAM = Identity and Access Management. 
Controls WHO can access WHAT in your AWS environment and HOW. 
  
WHO → Users, Groups, Roles | WHAT → AWS services | HOW → Actions 
  
Key principle: LEAST PRIVILEGE — give minimum permissions needed. 
  
IAM is: 
- GLOBAL — not region-specific | FREE — no additional cost 
- The first line of security in AWS 
  
In your project: kOps created IAM roles for master and worker nodes. 
 
Q54. What are the 4 main components of IAM? 
1. Users: Individual identity for a person or application. 
   Has permanent credentials (username/password or access keys).  
  
2. Groups: Collection of IAM Users. 
   Assign permissions to the group — users inherit them. 
   Example: DevOps-Group, Dev-Group, ReadOnly-Group 
  
3. Roles: Temporary identity assumed by AWS services or users. 
   No permanent credentials — generates temporary tokens. 
   Used for: EC2 to access S3, Lambda to access DynamoDB.  
  
4. Policies: JSON documents that define permissions. 
   Specify: Effect (Allow/Deny), Action, Resource.  
   Attached to Users, Groups, or Roles.  
  
Analogy: 
Users = Employees | Groups = Departments | Roles = Visitor pass | Policies = Access rules 
 
Q55. What is the difference between an IAM User and an IAM Role? 
IAM User: 
- Permanent identity | For HUMANS (developers, admins) 
- Has username + password for console login 
- Has access keys for programmatic access (CLI/SDK) 
- Credentials are LONG-TERM 
  
IAM Role: 
- Temporary identity | For AWS SERVICES (EC2, Lambda, ECS) 
- NO username or password | NO permanent access keys 
- Generates temporary credentials automatically (1-12 hours) 
  
Why Role is better for services: 
❌ Bad: Store access keys in EC2 → if hacked, attacker has keys FOREVER! 
✅ Good: Attach IAM Role → tokens expire soon even if hacked! 
  
In your project: kOps attached IAM Roles to master and worker nodes.

## Section / Page 21

No hardcoded credentials anywhere! ✅ 
 
Q56. What is an IAM Group and why use it? 
IAM Group = collection of IAM Users. 
Attach policies to the group → all users inherit permissions. 
  
Without Groups: 
50 developers, each needs same permissions. 
Attach policy to each user individually (50 times!) ❌ 
  
With Groups: 
Create DevOps-Group, attach one policy. 
Add all 50 developers to the group ✅ 
Remove one user from group → instantly loses access ✅ 
  
Key facts: 
- Groups CANNOT contain other groups (no nesting) 
- A user can belong to MULTIPLE groups 
 
Q57. What is an IAM Policy and what does it look like? 
IAM Policy = JSON document defining permissions. 
  
Structure: 
{"Version":"2012-10-17","Statement":[{ 
  "Effect":"Allow", 
  "Action":["s3:GetObject","s3:PutObject"],  
  "Resource":"arn:aws:s3:::my-bucket/*" 
}]} 
  
Reading this policy: 
✅ Can read files from my-bucket 
✅ Can upload files to my-bucket 
❌ Cannot delete files | ❌ Cannot access other S3 buckets 
 
Q58. What are the 3 types of IAM Policies? 
1. AWS Managed Policies: 
   Pre-built by AWS. Auto-updated when new features launch.  
   Examples: AmazonS3FullAccess, AmazonEC2ReadOnlyAccess  
   Use when: standard permissions are enough.  
  
2. Customer Managed Policies: 
   You create and manage them. More specific and customizable.  
   Reusable — attach to multiple users/roles/groups.  
   Use when: need fine-grained custom control. 
  
3. Inline Policies: 
   Directly embedded into one User, Role, or Group.  
   1:1 relationship — NOT reusable. 
   Use when: permission is unique to one specific identity.  
  
Best practice: 
Prefer Customer Managed > AWS Managed > Inline 
Avoid inline policies (hard to manage at scale)

## Section / Page 22

Q59. What is the principle of Least Privilege? 
Least Privilege = give ONLY minimum permissions absolutely needed. 
  
Example: 
Developer who only reads from S3: 
❌ Wrong: Give AmazonS3FullAccess (can also delete, create buckets) 
✅ Right: Give only s3:GetObject on specific bucket 
  
Why it matters: 
- If credentials are compromised, damage is limited 
- Accidental operations are prevented 
- Reduces attack surface 
- Required for compliance (SOC2, ISO27001) 
  
In your project: 
Worker node role: can only READ EC2 info, pull from ECR 
Master node role: can manage EC2, ELB, Route53 (needs more) 
 
Q60. What is MFA and why is it important? 
MFA = Multi-Factor Authentication. 
Adds a SECOND layer of security beyond just a password. 
  
Without MFA: Username + Password → Access 
(If password stolen → attacker is in! 😱) 
  
With MFA: Username + Password + OTP code → Access 
(Even if password stolen → no OTP = no access 😱) 
  
MFA devices in AWS: 
- Virtual MFA: Google Authenticator, Authy (most common) 
- Hardware MFA: Physical security key (YubiKey) 
  
Best practices: 
✅ Always enable MFA on root account 
✅ Enable MFA for all admin/IAM users 
 
Q61. What is a Root account and what are best practices for it? 
Root account = first account created when you sign up for AWS. 
Uses your email and password. 
  
Root account has: 
- UNLIMITED access to everything in AWS 
- Cannot be restricted by any IAM policy 
- Can close the ENTIRE AWS account 
  
Why Root is DANGEROUS: 
If compromised → attacker can do ANYTHING! 
  
Best practices: 
✅ Enable MFA on root account IMMEDIATELY 
✅ NEVER use root for daily work 
✅ Create separate IAM admin user for daily use 
✅ Do NOT create access keys for root

## Section / Page 23

Simple rule: Root account = Emergency key. Use only when absolutely necessary. 
 
Q62. What is an Access Key and when do you use it? 
Access Key = credentials for programmatic access to AWS. 
(Through CLI, SDK, or APIs) 
  
An Access Key consists of: 
- Access Key ID (like username) — public 
- Secret Access Key (like password) — keep PRIVATE! 
  
When to use: 
- AWS CLI commands from your local machine 
- Applications using AWS SDK (Boto3, Java SDK) 
- CI/CD tools like Jenkins accessing AWS 
  
Security best practices: 
✅ NEVER hardcode access keys in code or Dockerfiles 
✅ NEVER commit access keys to Git 
✅ Use IAM Roles instead for EC2/Lambda 
✅ Rotate access keys regularly (every 90 days) 
 
Q63. How did kOps use IAM in your project? 
kOps automatically created TWO IAM Roles for cluster nodes: 
  
1. Master Node IAM Role: 
   - Can manage EC2 instances 
   - Can create and manage ELB (for Services)  
   - Can manage Route53 DNS records  
   - Can read/write to S3 (state store)  
  
2. Worker Node IAM Role: 
   - Can describe EC2 instances 
   - Can pull images from ECR 
   - Can read Auto Scaling info 
  
Why: Nodes need to call AWS APIs to function. 
IAM Roles → temporary credentials auto-rotate → more secure. 
Follows principle of least privilege ✅ 
 
Q64. What is the difference between authentication and authorization? 
Authentication (AuthN): 
- WHO are you? Proving your identity. 
- Examples: Username + Password, MFA, SSH key pair 
  
Authorization (AuthZ): 
- WHAT can you do? What are you allowed to do? 
- Examples: IAM Policies, File permissions, RBAC 
  
Order: Authentication happens FIRST → Then Authorization 
  
Real example: 
You log into AWS Console (Authentication)

## Section / Page 24

→ You try to delete an EC2 instance 
→ IAM checks your policies (Authorization) 
→ You have no ec2:TerminateInstances permission 
→ Access Denied ❌

## Section / Page 25

☁️ SNS & SQS (Q65–Q72) 
 
Q65. What is SNS and what does it stand for? 
SNS = Simple Notification Service. 
Fully managed publish-subscribe messaging service. 
Sends messages to MULTIPLE subscribers simultaneously. 
  
Flow: Publisher → SNS Topic → Subscribers 
  
Subscribers can be: Email | SMS | Lambda functions 
  SQS queues | HTTP/HTTPS endpoints | Mobile push notifications  
  
Real-world analogy: SNS like a WhatsApp Broadcast. 
You send one message → everyone receives it simultaneously! 
  
Common DevOps use case: 
CloudWatch Alarm (CPU > 80%) → SNS Topic → 
├── Email to DevOps team | ├── SMS to on-call engineer 
└── Trigger Lambda to add more EC2 (Auto Scaling) 
 
Q66. What is a Topic and what is a Subscription in SNS? 
Topic: 
- The CHANNEL or category in SNS 
- Publishers send messages TO the topic 
- Think of it like a WhatsApp group 
- Example: "CPU-Alert-Topic" or "Deployment-Notification" 
  
Subscription: 
- How someone signs up to RECEIVE messages from a topic 
- Supported types: Email | SMS | Lambda | SQS | HTTP/HTTPS 
  
Example: 
Topic: "Tomcat-Down-Alert" 
Subscriptions: 
- Email to team lead | SMS to on-call engineer 
- Lambda to automatically restart Tomcat 
 
Q67. What is SQS and what does it stand for? 
SQS = Simple Queue Service. 
Fully managed message queuing service. 
Decouples and scales microservices and distributed systems. 
  
Flow: Producer → SQS Queue → Consumer PULLS → Processes → Deletes 
  
Think of it like a TICKET QUEUE at a bank: 
- Customers take tokens (messages added to queue) 
- Queue holds all tokens 
- Bank staff processes ONE token at a time 
  
Key facts: 
- Messages stored up to 14 DAYS 
- Pull-based (consumer pulls, not pushed)

## Section / Page 26

- ONE message processed by ONE consumer 
- If consumer crashes → message goes BACK to queue (no loss!) 
 
Q68. What is the difference between SNS and SQS? 
SNS: 
- PUSH based (SNS pushes to subscribers) 
- Immediate delivery 
- Multiple subscribers get same message simultaneously 
- Messages NOT stored (fire and forget) 
- Use for: alerts, notifications, broadcasts 
  
SQS: 
- PULL based (consumers pull from queue) 
- Messages wait in queue until consumed 
- ONE consumer processes each message 
- Messages stored up to 14 days 
- Use for: task processing, job queues, decoupling 
  
Simple analogy: 
SNS = WhatsApp Broadcast (everyone gets it instantly) 
SQS = Shared task list (one person picks one task at a time) 
 
Q69. What is the Fan-out pattern in AWS? 
Fan-out = ONE SNS message triggers MULTIPLE SQS queues, 
each processed INDEPENDENTLY. 
  
Flow: One event → SNS Topic → 
├── SQS Queue 1 → Service A processes independently 
├── SQS Queue 2 → Service B processes independently 
└── SQS Queue 3 → Service C processes independently 
  
Real example — E-commerce order placed: 
Order Created → SNS Topic "new-order" → 
├── SQS → Payment Service (charge the card) 
├── SQS → Inventory Service (reduce stock) 
├── SQS → Email Service (send confirmation) 
└── SQS → Shipping Service (prepare shipment) 
  
Benefits: Decoupled | Scalable | Resilient | No message lost 
 
Q70. How long can SQS store messages? 
SQS can store messages for a maximum of 14 DAYS. 
  
Default retention period: 4 days 
Configurable range: 1 minute to 14 days 
  
Visibility Timeout: 
- When consumer picks a message → becomes INVISIBLE to others 
- Default: 30 seconds 
- If consumer crashes → message becomes visible again for retry 
- Prevents message LOSS on consumer failure!

## Section / Page 27

Q71. Give a real-world DevOps scenario where you would use SNS. 
Scenario: Automated alerting and response for production issues 
  
1. CloudWatch monitors CPU of EC2 instances every 5 minutes 
  
2. When CPU > 80% for 10 minutes: 
   CloudWatch Alarm → SNS Topic "High-CPU-Alert" 
  
3. SNS Topic delivers to: 
   ├── Email → DevOps team: "Server CPU is above 80%!"  
   ├── SMS  → On-call engineer's phone 
   └── Lambda → Automatically triggers Auto Scaling  
  
Result: 
✅ Team is immediately notified 
✅ Auto Scaling kicks in automatically 
✅ Application stays responsive — No manual intervention at 2AM! 
 
Q72. What is CloudWatch and how does it work with SNS? 
CloudWatch = AWS's native monitoring and observability service. 
  
CloudWatch Alarm States: 
- OK               → metric is within threshold ✅ 
- ALARM            → metric crossed threshold 😱 
- INSUFFICIENT_DATA → not enough data yet 😱 
  
How CloudWatch works WITH SNS: 
Step 1: Create CloudWatch Alarm 
"If EC2 CPU > 80% for 5 minutes → ALARM state"  
  
Step 2: Configure action → send to SNS Topic 
  
Step 3: SNS delivers to subscribers (Email, SMS, Lambda) 
  
Complete flow: 
EC2 CPU spikes to 90% → CloudWatch detects → 
ALARM state → SNS Topic → Email + Lambda to scale up

## Section / Page 28

☁️ STORAGE: S3 vs EBS vs EFS (Q73–Q78) 
 
Q73. What is the difference between S3, EBS and EFS? 
S3 — Object Storage: 
- Global (not AZ specific) | Unlimited storage | Cheapest 
- Accessed over HTTP/HTTPS — NOT mounted to server 
- Use for: backups, logs, images, videos, artifacts, websites 
  
EBS — Block Storage: 
- Attached to ONE EC2 instance | AZ specific ❌ 
- Fast random read/write | Fixed size | More expensive 
- Use for: OS volumes, databases 
  
EFS — File Storage: 
- MULTIPLE EC2s can mount simultaneously | Multi-AZ ✅ 
- Auto-scales | Most expensive 
- Use for: shared content, web server file sharing 
  
Summary: 
S3  → Files/backups | EBS → DB/OS volumes | EFS → Shared storage 
 
Q74. What is EFS and what does it stand for? 
EFS = Elastic File System. 
Fully managed, scalable SHARED file storage. 
Multiple EC2 instances can access simultaneously. 
  
Key characteristics: 
- File storage (like a shared network drive) 
- Multiple EC2 instances can mount and use at same time 
- Automatically scales up and down | No provisioning needed 
- Multi-AZ — data replicated across multiple AZs 
- Accessed using NFS protocol 
  
EC2 Instance 1 ─┐ 
EC2 Instance 2 ─┼──→ EFS File System (ALL see same files!) 
EC2 Instance 3 ─┘ 
  
Azure equivalent: Azure Files 
 
Q75. Is EFS AZ specific? 
NO — EFS is NOT AZ specific. It is MULTI-AZ. 
  
EBS: Created in ONE AZ → only accessible in that AZ. 
     If AZ us-east-1a goes down → EBS INACCESSIBLE! ❌ 
  
EFS: Data automatically replicated across MULTIPLE AZs. 
     If one AZ goes down → still accessible from other AZs ✅ 
  
This is EFS's BIGGEST advantage over EBS! 
  
In your project limitation: 
You used EBS for PostgreSQL in Kubernetes → AZ specific.

## Section / Page 29

If that AZ fails → database becomes inaccessible. 
  
Production improvement: Use EFS → data survives AZ failure ✅ 
 
Q76. How many EC2 instances can access EFS simultaneously? 
THOUSANDS of EC2 instances can access EFS simultaneously — no fixed limit! 
  
Compare: 
EBS: 1 EC2 at a time (standard volumes) 
     Max 16 instances (only io1/io2 Multi-Attach, same AZ) 
  
EFS: Thousands of EC2 instances simultaneously 
     Across multiple AZs in the same region  
  
Use case: 
Content management with 100 web servers: 
100 EC2 instances → all mount same EFS 
All servers see same files → consistent content ✅ 
 
Q77. What are Azure equivalents of S3, EBS and EFS? 
AWS S3  → Azure Blob Storage 
  Object storage. Store files, images, videos, backups.  
  Azure access tiers: Hot, Cool, Archive  
  
AWS EBS → Azure Managed Disks 
  Block storage attached to one VM.  
  Types: Premium SSD, Standard SSD, Standard HDD, Ultra Disk.  
  AZ specific (same limitation as EBS).  
  
AWS EFS → Azure Files 
  Shared file storage. Multiple VMs access simultaneously.  
  Uses SMB (Windows) or NFS (Linux) protocol. Multi-AZ. 
  
Mapping: 
S3  → Blob Storage (object/file storage) 
EBS → Managed Disks (block storage for VMs) 
EFS → Azure Files (shared file storage) 
 
Q78. When would you choose EFS over EBS? 
Choose EFS when: 
1. Multiple servers need to share the same files: 
   10 web servers all serving same content.  
   EBS: impossible (one attachment only) ❌ | EFS: perfect ✅ 
  
2. High availability is required: 
   EFS survives AZ failures ✅ 
  
3. Storage size is unpredictable: 
   EBS: must provision fixed size upfront  
   EFS: automatically grows and shrinks ✅ 
  
Choose EBS when: 
- Single server needs fast, dedicated storage 
- Database requiring very fast I/O

## Section / Page 30

- Cost is a concern (EBS cheaper than EFS) 
  
Summary: 
One server, fast, cheap → EBS 
Multiple servers, shared, HA → EFS

## Section / Page 31

☁️ DATABASES: RDS & DynamoDB (Q79–Q87) 
 
Q79. What is RDS and what does it stand for? 
RDS = Relational Database Service. 
Fully managed SQL database service by AWS. 
  
AWS handles: 
✅ Installation and setup | ✅ Patching and updates 
✅ Automated backups (daily) | ✅ High availability (Multi-AZ) 
✅ Monitoring and metrics 
  
Without RDS (DB on EC2): You manage EVERYTHING — time consuming and error-prone! 
With RDS: AWS manages everything. You just: create DB, connect, use it ✅ 
 
Q80. What databases does RDS support? 
RDS supports 6 database engines: 
  
1. MySQL          → most popular open source SQL DB 
2. PostgreSQL     → advanced open source SQL DB (YOUR project!) 
3. Aurora         → AWS proprietary (MySQL/PostgreSQL compatible) 
4. MariaDB        → MySQL fork, open source 
5. Oracle         → enterprise database (paid license) 
6. SQL Server     → Microsoft's database (paid license) 
  
Choosing: 
MySQL → common web apps | PostgreSQL → complex queries, enterprise 
Aurora → need MySQL/PG but want better performance 
  
Note: MongoDB is NOT an AWS RDS service! AWS NoSQL = DynamoDB 
 
Q81. What is Multi-AZ in RDS and why use it? 
Multi-AZ = creates a standby replica of your database in a DIFFERENT AZ. 
  
Flow: Primary DB (us-east-1a) → synchronous replication → Standby DB (us-east-1b) 
  
If Primary fails: 
- AWS auto-detects the failure 
- Auto-switches to Standby (failover) 
- Your connection string stays the SAME (DNS redirects) 
- Downtime: typically 1-2 minutes 
  
Why use Multi-AZ: 
✅ High Availability — survive AZ failures 
✅ Zero data loss — synchronous replication 
✅ Automatic failover — no manual intervention 
  
IMPORTANT: Standby is NOT readable — BACKUP ONLY! 
Cost: approximately 2x (two instances) 
 
Q82. What is a Read Replica in RDS and why use it?

## Section / Page 32

Read Replica = copy of database that handles READ traffic. 
Reduces load on the primary database. 
  
Flow: Primary DB (handles all writes) → async replication → 
Read Replica 1 → handles read queries 
Read Replica 2 → handles read queries 
  
Key characteristics: 
✅ You CAN read from replica 
❌ You CANNOT write to replica (read only) 
- Asynchronous — slight delay vs primary 
- Can have up to 5 read replicas per RDS instance 
- Can be in different regions (for global apps) 
  
Use for: High-traffic read-heavy apps | Analytics queries | Reporting dashboards 
 
Q83. What is the difference between Multi-AZ and Read Replica? 
Multi-AZ: 
- Purpose: HIGH AVAILABILITY (survive failures) 
- Standby: Cannot read or write 
- Replication: Synchronous (no data loss) 
- Failover: AUTOMATIC | Location: Same region only 
- Analogy: Spare tyre (only used when main punctures) 
  
Read Replica: 
- Purpose: PERFORMANCE (handle read traffic) 
- Replica: CAN read, cannot write 
- Replication: Asynchronous (slight lag possible) 
- Failover: MANUAL promotion needed | Location: Any region 
- Analogy: Photocopy of a book (many people can read) 
  
Can you use both together? YES! Best practice: 
Primary DB → Multi-AZ (for HA) + Read Replicas (for performance) 
 
Q84. What is DynamoDB? 
DynamoDB = AWS's fully managed NoSQL database service. 
  
Key characteristics: 
- NoSQL — stores data as key-value or document (JSON) 
- Serverless — no servers to manage 
- Auto-scales — scales up/down with traffic automatically 
- Single-digit millisecond latency — extremely fast 
  
Example document: 
{"userId":"u123","name":"Akhil","skills":["Docker","K8s"],"score":9999}  
Each record can have DIFFERENT fields — no rigid columns! 
  
Use cases: User sessions | Gaming leaderboards | Shopping cart | IoT sensor data 
 
Q85. When would you use DynamoDB instead of RDS? 
Use DynamoDB when: 
✅ Data is unstructured or flexible schema

## Section / Page 33

✅ Need massive scale (millions of requests/second) 
✅ Need single-digit millisecond speed 
✅ Simple access patterns (key-value lookups, no JOINs) 
✅ Serverless — no management overhead 
  
Use RDS when: 
✅ Structured data with relationships 
✅ Complex queries needed (GROUP BY, JOINs, aggregations) 
✅ ACID transactions required (financial data, banking) 
✅ Team knows SQL 
  
Simple rule: 
Structured + Relationships + Complex queries → RDS 
Unstructured + Massive scale + Simple lookups → DynamoDB 
 
Q86. What is Aurora and how is it different from MySQL? 
Aurora = AWS's proprietary cloud-native relational database. 
Compatible with MySQL and PostgreSQL. 
  
How Aurora differs: 
Performance: Aurora MySQL = 5x faster than standard MySQL! 
  
High Availability: 
- 6 copies of data across 3 AZs ALWAYS 
- Automatic healing of bad disk blocks 
- Read replicas promote to primary in 30 seconds 
  
Storage: Auto-scales from 10GB to 128TB automatically. 
  
Aurora Serverless: 
- Scales compute to ZERO when not in use 
- Pay only when database is active 
  
When to use: 
RDS MySQL/PostgreSQL → standard workloads, cost-sensitive 
Aurora               → high performance, critical production 
 
Q87. What is the difference between RDS and installing a DB on EC2? 
Installing DB on EC2 (DIY): 
You manage EVERYTHING: 
❌ Install manually | ❌ Apply patches | ❌ Set up backups 
❌ Set up High Availability | ❌ Monitor performance 
  
RDS (Managed Service): 
AWS manages: 
✅ Installation and configuration | ✅ Patching automatically 
✅ Automated daily backups | ✅ Multi-AZ HA option 
✅ CloudWatch monitoring | ✅ Storage auto-scaling 
  
When to use DB on EC2: 
- Need a database RDS doesn't support 
- Need specific OS-level configuration 
  
When to use RDS:

## Section / Page 34

- Most production scenarios (RECOMMENDED!) 
- Team should focus on app, not DB operations

## Section / Page 35

☁️ OTHER AWS SERVICES (Q88–Q106) 
 
Q88. What is CloudWatch and what does it monitor? 
CloudWatch = AWS's native monitoring and observability service. 
  
What it monitors: 
- EC2: CPUUtilization, NetworkIn/Out, DiskReadOps 
- RDS: DatabaseConnections, FreeStorageSpace 
- Lambda: Invocations, Errors, Duration, Throttles 
- Load Balancers: RequestCount, TargetResponseTime 
- Custom Metrics: push your own from applications 
  
Features: 
- Dashboards — visual graphs of metrics 
- Alarms     — notify when threshold crossed 
- Logs       — collect and store log files 
- Events     — trigger actions on schedule 
  
In your project: You used LGTM stack instead of CloudWatch. 
Open source, free, works across AWS AND Azure. 
 
Q89. What are the 3 states of a CloudWatch alarm? 
1. OK ✅ 
   Metric is within the defined threshold. Everything is normal.  
   Example: CPU is at 45% (threshold is 80%)  
  
2. ALARM 😱 
   Metric has CROSSED the threshold. Action is triggered!  
   Example: CPU is at 85% (above 80% threshold)  
  
3. INSUFFICIENT_DATA 😱 
   Not enough data to determine the state.  
   Happens when: alarm just created, instance just launched,  
   or metric stopped reporting. 
  
State transitions: 
New alarm → INSUFFICIENT_DATA → OK → ALARM → OK 
 
Q90. What is Lambda and when do you use it? 
AWS Lambda = serverless compute service. 
Run code WITHOUT provisioning or managing any servers. 
  
How it works: 
- Upload your code (Python, Node.js, Java, etc.) 
- Lambda runs it ONLY when triggered 
- Pay ONLY for execution time (no idle cost) 
- Scales automatically from 0 to thousands of instances 
  
Triggers: S3 event | API Gateway | CloudWatch Events | SNS | SQS 
  
When to use: 
- Image uploaded to S3 → Lambda resizes it

## Section / Page 36

- New order → Lambda sends confirmation email 
- EC2 stops at 6PM → Lambda triggers shutdown 
  
Limits: Max execution time = 15 minutes | Memory = up to 10 GB 
 
Q91. What is Auto Scaling Group and how do you configure it? 
Auto Scaling Group (ASG) = collection of EC2 instances that auto-scales. 
  
Configuration: 
1. Create Launch Template (defines WHAT to launch) 
2. Create ASG: Min=2, Desired=4, Max=10 
3. Attach Load Balancer (optional) 
4. Configure Scaling Policies: 
  
Option A — Target Tracking: "Keep average CPU at 50%" 
Option B — Step Scaling: "If CPU > 70% for 5 min → add 2 instances" 
Option C — Scheduled: "Every weekday at 9AM → set desired to 6" 
  
Flow: CloudWatch alarm → ASG launches new EC2 from template → 
Registers with Load Balancer → Traffic distributed ✅ 
 
Q92. What is ELB and what are the types of load balancers? 
ELB = Elastic Load Balancer. 
Automatically distributes incoming traffic across multiple EC2 instances. 
  
4 Types of ELB: 
  
1. ALB — Application Load Balancer: 
   Layer 7 (HTTP/HTTPS). Routes based on URL path or hostname.  
   Best for: web apps, microservices.  
  
2. NLB — Network Load Balancer: 
   Layer 4 (TCP/UDP). Ultra-high performance, low latency.  
   Best for: gaming, IoT, real-time apps. 
  
3. CLB — Classic Load Balancer (legacy): 
   Old generation. Use ALB or NLB instead.  
  
4. GLB — Gateway Load Balancer: 
   Third-party network appliances, firewalls.  
 
Q93. What is the difference between ALB and NLB? 
ALB — Application Load Balancer: 
- Layer 7 (HTTP/HTTPS) 
- Can inspect request content (URL, headers, cookies) 
- Routes: /api/* → API servers | /static/* → static servers 
- Best for: web apps, REST APIs, microservices 
- Slightly slower than NLB (more processing) 
  
NLB — Network Load Balancer: 
- Layer 4 (TCP/UDP) 
- Cannot inspect request content 
- Extremely fast: millions of requests per second

## Section / Page 37

- Ultra-low latency (microseconds) 
- Best for: gaming, video streaming, IoT, high performance 
  
Simple analogy: 
ALB = Smart traffic cop who reads road signs 
NLB = Very fast toll booth 
  
In Kubernetes: LoadBalancer Service on AWS → creates NLB by default. 
 
Q94. What is Route 53? 
Route 53 = AWS's scalable Domain Name System (DNS) web service. 
  
What it does: 
1. Domain Registration: Buy and register domain names (myapp.com) 
2. DNS Resolution: myapp.com → 52.23.45.67 
3. Health Checks: Monitor endpoints, auto-redirect if failed 
4. Traffic Routing Policies: 
   - Simple: domain → one IP 
   - Weighted: 70% → server A, 30% → server B  
   - Latency: route to lowest-latency region 
   - Failover: primary fails → switch to backup  
   - Geolocation: users in India → Indian servers  
  
Why "Route 53": DNS uses port 53. Hence Route 53. 
  
In your project: kOps uses Route 53 to register cluster DNS records. 
 
Q95. What is CloudFront? 
CloudFront = AWS's Content Delivery Network (CDN). 
Speeds up delivery by caching content at edge locations worldwide. 
  
Without CloudFront: India user → US East server → slow! 😱 
With CloudFront:    India user → Edge in Mumbai → fast! ✅ 
  
CloudFront has 400+ edge locations worldwide. 
  
Benefits: 
✅ Faster load times (reduced latency) 
✅ Reduced load on your origin server 
✅ DDoS protection (AWS Shield integration) 
✅ Free SSL/TLS certificate (AWS Certificate Manager) 
 
Q96. What is AWS CloudTrail? 
CloudTrail = AWS's audit and governance service. 
Records EVERY API call made in your AWS account. 
  
What it logs: 
- Every AWS Console login | Every CLI command | Every SDK API call 
- What was changed, by whom, and from which IP 
  
Example log entry: 
Who: Akhil (IAM user) 
What: Terminated EC2 instance i-12345

## Section / Page 38

When: 2026-04-20 14:30:00 UTC | Where: IP 192.168.1.100 
  
Why important: 
- Security: "Who deleted that S3 bucket?" 
- Compliance: SOC2, ISO27001, HIPAA require audit logs 
  
CloudTrail vs CloudWatch: 
CloudWatch → Monitors PERFORMANCE (CPU, memory) 
CloudTrail → Monitors ACTIVITY (who did what) 
 
Q97. Your EC2 instance is unreachable after launch — what do you check? 
Step 1: Check instance state — Is it running? Status Checks = "2/2 passed"? 
  
Step 2: Check Security Group rules 
  Is port 22 (SSH) or 3389 (RDP) open?  
  Is inbound rule allowing your IP or 0.0.0.0/0?  
  (MOST COMMON MISTAKE!) 
  
Step 3: Check if instance has a Public IP 
  If in private subnet → no public IP by default.  
  Fix: allocate and attach Elastic IP  
  
Step 4: Check Subnet and Route Table 
  Is instance in a PUBLIC subnet?  
  Does route table have route to Internet Gateway?  
  0.0.0.0/0 → igw-xxxxxxxxx 
  
Step 5: Check NACL rules (stateless — need both inbound AND outbound) 
  
Step 6: Check key pair (correct .pem file? chmod 400 key.pem?) 
  
Most common causes: 
1. Security Group missing inbound rule 
2. Wrong key pair | 3. Private subnet without Elastic IP 
 
Q98. Your S3 objects are not publicly accessible after enabling static hosting — what 
do you check? 
Step 1: Check Block Public Access settings (MOST COMMON MISTAKE!) 
  S3 → Bucket → Permissions → Block Public Access  
  ALL four settings must be DISABLED.  
  AWS enables these by default for security.  
  
Step 2: Check Bucket Policy 
  Must have policy allowing s3:GetObject for everyone (*)  
  Check for typos in bucket name in Resource ARN.  
  
Step 3: Check Static Website Hosting is enabled 
  S3 → Properties → Static website hosting → Must show Enabled  
  Index document must be set (e.g., index.html)  
  
Step 4: Check you are using the CORRECT URL 
✅ http://bucket.s3-website-region.amazonaws.com 
❌ https://s3.amazonaws.com/bucket/file.html 
  
Step 5: Clear browser cache — open in incognito/private mode.

## Section / Page 39

Q99. Your RDS database cannot connect from EC2 — what do you debug? 
Step 1: Check they are in the SAME VPC 
  
Step 2: Check RDS Security Group inbound rules 
  Must allow database port FROM the EC2 Security Group:  
  MySQL: port 3306 | PostgreSQL: port 5432  
  Best practice: allow from EC2's Security Group ID (not specific IP)  
  
Step 3: Check RDS is in "Available" state 
  
Step 4: Check DB credentials 
  Correct username and password? 
  postgresql://username:password@rds-endpoint:5432/dbname 
  
Step 5: Test connection from EC2 
  SSH into EC2 → psql -h <rds-endpoint> -U postgres -d mydb 
  Connection timeout → network issue  
  Authentication failed → credentials issue  
  
Most common cause: RDS Security Group missing inbound rule! 
 
Q100. Your private EC2 instance needs internet to download packages — how? 
Solution: NAT Gateway in Public Subnet. 
  
Step 1: Create NAT Gateway 
  VPC → NAT Gateways → Create NAT Gateway  
  Place it in PUBLIC subnet (important!)  
  Allocate Elastic IP to it 
  
Step 2: Update Private Subnet Route Table 
  Add route: Destination: 0.0.0.0/0 → Target: nat-gateway-id 
  
Step 3: Verify EC2 can access internet 
  SSH into private EC2 via Bastion Host  
  ping google.com 
  
Flow after setup: 
Private EC2 → NAT Gateway (public subnet) → IGW → Internet 
(outbound only — internet STILL cannot reach private EC2) 
  
Common mistakes: NAT Gateway in PRIVATE subnet (must be PUBLIC!) 
 
Q101. Your disk on EC2 is at 95% — walk me through how you fix it. 
Step 1: Confirm disk is full 
  df -h  (look for partition at 95%+ in "Use%" column)  
  
Step 2: Find which folders are biggest 
  du -sh /var/log/*   du -sh /opt/*   du -sh /home/* 
  
Step 3: Investigate the biggest folder 
  ls -lh /var/log/apache2/ 
  ls -lh /opt/tomcat1/logs/ 
  
Step 4: Clean up safely 
  rm -rf /opt/tomcat1/logs/catalina.out.*  
  rm -rf /var/log/apache2/*.gz

## Section / Page 40

OR truncate: > /var/log/large.log  
  
Step 5: Verify disk freed up: df -h 
  
Step 6: Prevent recurrence 
  Set up log rotation (logrotate)  
  Set CloudWatch alarm for disk > 80%  
  
😱 NEVER blindly run rm -rf — always check with ls -lh first! 
 
Q102. You need to reduce AWS costs for a dev environment that runs 8 hours a day — 
what do you do? 
Option 1 — Auto-Start/Stop with Lambda + CloudWatch Events: 
  Lambda starts EC2 at 9AM, stops at 6PM.  
  CloudWatch cron: cron(0 9 * * ? *) → trigger start Lambda  
  EC2 stopped = no compute charges!  
  
Option 2 — Use Spot Instances: 
  Up to 90% cheaper than On-Demand. 
  AWS can reclaim with 2 min warning.  
  Acceptable for dev/test (not production).  
  
Option 3 — Use smaller instance types for dev: 
  Production: m5.xlarge | Dev: t3.micro (much cheaper)  
  
Option 4 — Savings Plans or Reserved Instances: 
  Commit to 1 or 3 years → up to 72% discount.  
  
Real savings: 
t3.medium 24x7 = ~$30/month 
t3.medium 8 hrs/day = ~$10/month (66% reduction!) ✅ 
 
Q103. A developer accidentally deleted an S3 object — how do you recover it? 
Recovery depends on whether Versioning is enabled: 
  
If Versioning IS enabled ✅ (easy recovery): 
Step 1: Go to S3 → Bucket → Objects 
Step 2: Click "Show versions" toggle 
Step 3: Find the deleted file — it shows a "Delete marker" 
Step 4: Select the Delete marker → Delete it 
Step 5: Previous version is now RESTORED! 
  
If Versioning is NOT enabled ❌: 
- Object is PERMANENTLY deleted 
- No recovery possible from S3 alone 
- Check if backups exist elsewhere 
- If none → data is LOST 
  
LESSON: ALWAYS enable S3 Versioning on important buckets! 
  
Prevention: 
✅ Enable Versioning | ✅ Enable MFA Delete 
✅ Restrict s3:DeleteObject via IAM policies

## Section / Page 41

Q104. Your EC2 CPU is at 95% — how do you find which process and fix it? 
Step 1: Confirm CPU is high 
  top OR htop 
  
Step 2: Find highest CPU consumer 
  ps aux --sort=-%cpu | head -10 
  tomcat 1234  85.0  java -jar tomcat.jar  ← this one! 
  
Step 3: Investigate the process logs 
  tail -f /opt/tomcat/logs/catalina.out | grep -i "error" 
  
Step 4: Fix based on cause: 
  Memory leak/infinite loop → restart Tomcat:  
  /opt/tomcat/bin/shutdown.sh && /opt/tomcat/bin/startup.sh  
  Too much traffic → scale horizontally / add load balancer  
  Inefficient code → profile app, fix code, redeploy  
  
Step 5: Monitor after fix: top → watch CPU come down 
  
Step 6: Prevent: CloudWatch CPU alarm > 80% | Consider Auto Scaling 
 
Q105. You need to give an EC2 instance access to S3 without storing credentials — 
how? 
Use an IAM ROLE — the correct and secure way! 
  
Why NOT access keys: 
❌ If instance hacked → attacker has permanent S3 access! 
❌ Commit to Git → security nightmare! 
  
Correct solution — IAM Role: 
Step 1: Create IAM Role for EC2 
  IAM → Roles → Create Role → Trusted entity: EC2  
  Attach: AmazonS3ReadOnlyAccess | Name: EC2-S3-Access-Role 
  
Step 2: Attach Role to EC2 
  EC2 Console → instance → Actions → Security → Modify IAM Role  
  
Step 3: Test from EC2 
  aws s3 ls s3://my-bucket  (works WITHOUT aws configure!) ✅ 
  
How it works: 
- EC2 gets temporary credentials from Instance Metadata Service 
- Credentials expire and rotate automatically 
- Even if compromised → tokens expire in 1 hour! 
 
Q106. Your pipeline cannot push Docker images to ECR — what do you check? 
ECR = Elastic Container Registry (AWS's private Docker registry) 
  
Step 1: Check if ECR repository exists (exact name match) 
  
Step 2: Check authentication — must login to ECR first! 
aws ecr get-login-password --region us-east-1 | \ 
docker login --username AWS \ 
--password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com 
(Token is valid for 12 hours)

## Section / Page 42

Step 3: Check IAM permissions 
  ecr:GetAuthorizationToken | ecr:PutImage  
  ecr:InitiateLayerUpload | ecr:UploadLayerPart  
  
Step 4: Check image tag format 
  <account-id>.dkr.ecr.<region>.amazonaws.com/<repo>:<tag>  
  
Most common cause: Missing ECR login step OR wrong IAM permissions

## Section / Page 43

☁️ AZURE BASICS (Q107–Q117) 
 
Q107. What is the difference between AWS and Azure at a high level? 
AWS (Amazon Web Services): 
- Launched 2006 — oldest and largest cloud provider 
- Market leader (~33% market share) | 200+ services 
- Strongest in: compute, storage, ML, serverless 
- Better for startups and internet companies 
- Names: EC2, S3, RDS, Lambda, VPC 
  
Azure (Microsoft Azure): 
- Launched 2010 — second largest (~23% market share) 
- Strong integration with Microsoft products (Windows, AD, Office 365) 
- Better for enterprises using Microsoft stack 
- Strong in: hybrid cloud, enterprise, government 
- Names: VM, Blob, Azure SQL, Functions, VNet 
  
Your experience: 
AWS → Project 2 (Kubernetes via kOps) 
Azure → Project 1 (VM, Azure DevOps, NSG) 
 
Q108. What is a Resource Group in Azure? 
Resource Group = logical container that holds related Azure resources. 
Think of it as a FOLDER for all your Azure resources. 
  
Example: Resource Group "MyApp-Production-RG" 
  ├── Virtual Machine | ├── Azure SQL Database  
  ├── Virtual Network | └── Network Security Group  
  
Why Resource Groups are important: 
✅ Organized Management: all resources for one app in one place 
✅ Bulk Operations: delete one RG → ALL resources inside deleted! 
✅ Access Control: assign permissions at RG level 
✅ Cost Tracking: view total cost for all resources in group 
  
No direct AWS equivalent. 
AWS manages resources by region and service. 
Azure groups them EXPLICITLY in Resource Groups. 
 
Q109. What is Azure VNet and how is it similar to AWS VPC? 
Azure VNet (Virtual Network) = Azure equivalent of AWS VPC. 
Your own isolated private network in Azure cloud. 
  
Both VNet and VPC: 
- Provide isolated private network 
- You define IP address range (CIDR block) 
- Can be divided into subnets (public and private) 
- Have route tables for traffic control 
- Have firewall rules (NSG in Azure, Security Groups in AWS) 
  
Key difference: 
AWS VPC: Need to explicitly create Internet Gateway and attach it.

## Section / Page 44

Azure VNet: Internet access available by default for resources with public IPs. 
 
Q110. What is NSG in Azure and how is it different from AWS Security Group? 
NSG = Network Security Group — Azure's firewall. 
  
Similarities with AWS Security Group: 
- Both are firewalls | Both use inbound and outbound rules 
- Both allow/deny based on port, protocol, source/destination 
  
Key Differences: 
AWS Security Group: 
- Instance level ONLY | Stateful | Allow rules only 
  
Azure NSG: 
- Can attach to SUBNET (like AWS NACL) 
- Can also attach to NETWORK INTERFACE (like AWS SG) 
- Has BOTH Allow AND Deny rules (more flexible) 
- Priority-based rules (lower number = higher priority) 
  
In your project: 
Port 80 inbound → Allow (Apache) 
Port 22 inbound → Allow (SSH) 
Everything else → denied by default 
 
Q111. What is Azure Managed Disks and how is it similar to EBS? 
Azure Managed Disks = Azure's block storage — equivalent to AWS EBS. 
  
Similarities: 
- Block storage attached to VMs | Persistent (survives stop/start) 
- AZ-specific (same limitation as EBS) 
- Can create snapshots for backup | One disk → one VM at a time 
  
Types: 
Ultra Disk    → Extreme performance (like EBS io2) 
Premium SSD   → High performance databases (like EBS io1) 
Standard SSD  → Most workloads (like EBS gp3) 
Standard HDD  → Low cost, infrequent (like EBS sc1) 
  
In your project: 
Azure VM had Standard SSD Managed Disk as OS disk 
where Apache, Tomcat, and PostgreSQL were installed. 
 
Q112. What is Azure Blob Storage and how is it similar to S3? 
Azure Blob Storage = Azure's object storage — equivalent to AWS S3. 
  
Similarities: 
- Object storage (store any type of file) 
- Globally accessible via HTTP/HTTPS 
- High durability | Used for backups, logs, media, websites 
  
Structure comparison: 
AWS S3      → Azure Blob Storage

## Section / Page 45

Bucket      → Container 
Object      → Blob 
  
Blob types in Azure: 
- Block Blob: for regular files (images, videos, logs) 
- Append Blob: for log files (can only append) 
- Page Blob: for VHD files (VM disks) 
  
Lifecycle management: 
S3: Standard → IA → Glacier 
Azure: Hot → Cool → Archive 
 
Q113. What are the access tiers in Azure Blob Storage? 
Azure Blob Storage has 3 access tiers (similar to S3 storage classes): 
  
Hot Tier: 
- FREQUENTLY accessed data 
- Highest storage cost, lowest access cost 
- AWS equivalent: S3 Standard 
- Use for: active application data, recent backups 
  
Cool Tier: 
- INFREQUENTLY accessed (once a month) 
- Data must stay minimum 30 days 
- AWS equivalent: S3 Standard-IA 
- Use for: short-term backups, older content 
  
Archive Tier: 
- RARELY accessed (once a year or less) 
- Retrieval takes hours | Data must stay 180 days 
- AWS equivalent: S3 Glacier 
- Use for: long-term compliance, old archives 
 
Q114. What is Azure Files and how is it similar to EFS? 
Azure Files = Azure's shared file storage — equivalent to AWS EFS. 
Multiple VMs can mount and access the same file share simultaneously. 
  
Similarities: 
- Shared file storage | Multiple VMs mount simultaneously 
- All machines see the SAME files | Auto-scales 
- Multi-AZ replication available 
  
Protocols supported: 
- SMB (Server Message Block) — Windows and Linux 
- NFS (Network File System) — Linux (like EFS) 
  
Key difference from Managed Disks (EBS): 
Managed Disks → ONE VM at a time 
Azure Files   → MULTIPLE VMs simultaneously 
 
Q115. What is Azure AD and how is it similar to AWS IAM? 
Azure AD (Azure Active Directory) = Azure's identity and access management.

## Section / Page 46

Equivalent to AWS IAM. Controls who can access what Azure resources. 
  
Similarities: 
- Manage user identities | Control access to cloud resources 
- Role-based access control | Multi-factor authentication (MFA) 
  
Key components: 
Users: Human identities (like IAM Users) 
Groups: Collections of users (like IAM Groups) 
Service Principal: Non-human identity for apps (like IAM Roles) 
RBAC: Assign built-in roles (Owner, Contributor, Reader) 
  
Differences: 
- Azure AD also handles Office 365, Teams, other MS services 
- More integrated with enterprise (Active Directory sync) 
- Service Principal = IAM Role (terminology difference) 
 
Q116. What is Azure Monitor and how is it similar to CloudWatch? 
Azure Monitor = Azure's monitoring service — equivalent to AWS CloudWatch. 
  
Comparison: 
AWS CloudWatch Metrics  → Azure Monitor Metrics 
AWS CloudWatch Alarms   → Azure Alerts 
AWS CloudWatch Logs     → Azure Log Analytics 
AWS CloudTrail          → Azure Activity Log 
AWS X-Ray               → Azure Application Insights 
  
In your project: 
You used LGTM stack (Loki + Grafana) instead of Azure Monitor. 
Open source, free, multi-platform — works across AWS AND Azure. 
 
Q117. What is AKS and how is it similar to EKS? 
AKS = Azure Kubernetes Service. 
Azure's managed Kubernetes — equivalent to AWS EKS. 
  
Both AKS and EKS: 
- Managed Kubernetes — cloud provider manages control plane 
- You only manage worker nodes and workloads 
- Control plane is FREE (pay for worker VMs only) 
- Auto-scaling of nodes | Load balancer integration 
  
Your project comparison: 
You used kOps (not EKS) to provision K8s cluster on AWS. 
kOps = manual cluster management (creates EC2 for master) 
EKS  = fully managed (no master node management) 
AKS  = fully managed (Azure equivalent of EKS) 
  
Production recommendation: Use EKS (AWS) or AKS (Azure) instead of kOps.

## Section / Page 47

☁️ AZURE DEVOPS CORE (Q118–Q129) 
 
Q118. What are the 5 services of Azure DevOps? 
1. Azure Boards: Project management. Epics, Features, User Stories, Tasks, Bugs. 
   Sprint planning, Kanban board. Similar to Jira. YOU USED THIS ✅ 
  
2. Azure Repos: Source code management (Git repositories). 
   Pull Requests, Branch Policies. Similar to GitHub. YOU USED THIS ✅ 
  
3. Azure Pipelines: CI/CD automation. Build, test, deploy with YAML. 
   Similar to Jenkins / GitHub Actions. YOU USED THIS ✅ 
  
4. Azure Test Plans: Manual and automated test management. 
   Similar to TestRail. YOU DID NOT USE (theory only)  
  
5. Azure Artifacts: Package management. Store Maven, npm, NuGet packages. 
   Similar to Nexus. YOU DID NOT USE (theory only)  
  
Memory trick: B-R-P-T-A (Boards, Repos, Pipelines, Test Plans, Artifacts) 
 
Q119. Which services did you use and which did you not? 
Services YOU USED: 
  
Azure Boards ✅: 
- Created Epics, Features, Tasks for project tracking 
- Used Query Management for custom views 
- Tracked bugs and progress | Managed user roles 
  
Azure Repos ✅: 
- Stored all project code 
- Created PR template (.azuredevops/pull_request_template.md) 
- Set up Branch Policies (1 reviewer, no self-approve) 
  
Azure Pipelines ✅: 
- Multi-stage YAML CI/CD pipeline 
- Stages: Build → Test → Deploy Tomcat 1 → Deploy Tomcat 2 
- Self-hosted agent on same Azure VM 
  
NOT USED (theory only): 
- Azure Test Plans ❌ (manual testing management) 
- Azure Artifacts ❌ (like Nexus — package storage) 
 
Q120. What is Azure Boards and what is the work item hierarchy? 
Azure Boards = Azure DevOps's project management tool. 
Plan, track, and discuss work throughout development process. 
  
Work Item Hierarchy (Agile Process): 
Epic (Large business objective — multiple sprints) 
  │ Example: "Build CI/CD Infrastructure"  
Feature (Functional chunk of an Epic) 
  │ Example: "Automated Tomcat Deployment"  
User Story ("As a developer, I want...") 
  │ Example: "I want auto-deploy on code push"

## Section / Page 48

Task / Bug (Technical steps) 
  Example: "Configure azure-pipelines.yml" 
  
In your project: 
Epic: Multi-Tomcat Infrastructure & Automated Delivery 
  Feature 1: Azure VM & Environment Configuration  
  Feature 2: Tomcat Isolation & Apache Reverse Proxy  
  Feature 3: Agent Pool & Infrastructure Connectivity  
  Feature 4: CI/CD Pipeline Automation (YAML) 
  Feature 5: Operational Readiness & Validation  
 
Q121. What are the different work item states in Agile process? 
Default states in Agile process: 
  
New: Just created, work not started. In backlog. 
Active: Currently being worked on. Developer started. 
Resolved: Developer says done. Waiting for verification. 
Closed: Verified and accepted by reviewer/QA. Complete! 
Removed: Will not be worked on. Descoped or duplicate. 
  
State flow: 
New → Active → Resolved → Closed 
                        ↘ Removed (if descoped) 
  
On Kanban Board: Each column represents a state. 
Team drags cards from left to right as work progresses. 
 
Q122. What is a Sprint and how did you use it? 
Sprint = fixed time period (usually 1-4 weeks) during which 
a team completes a set of planned work items. 
  
In your project: 
Sprint 1: Infrastructure Setup 
  - Set up Azure VM | Install Apache and Tomcat  
  - Configure UFW firewall 
  
Sprint 2: CI/CD Pipeline 
  - Install self-hosted agent 
  - Create YAML pipeline | Set up branch policies 
  
Sprint 3: Monitoring 
  - Install Promtail, Loki, Grafana  
  - Configure dashboards | Test end-to-end 
 
Q123. What is Query Management in Azure Boards? 
Query Management = create custom searches and filters for work items. 
  
Example queries: 
"Show me all Active Bugs assigned to me"  
"Show me all Tasks in current Sprint"  
"Show me all Resolved items pending review"  
  
Types of queries: 
- Flat List: simple list of matching items 
- Tree of Work Items: shows parent-child hierarchy

## Section / Page 49

- Direct Links: shows relationships between items 
  
In your project: 
- "My Current Sprint Tasks" → showed only your tasks 
- "Open Bugs" → all unresolved bugs 
- "Deployment Issues" → bugs tagged with deployment 
Real-time visibility without scrolling! ✅ 
 
Q124. What is Azure Repos and how is it similar to GitHub? 
Azure Repos = Azure DevOps's source code management service. 
Hosts Git repositories for your code. 
  
Similarities with GitHub: 
- Both host Git repositories 
- Both support Pull Requests with code review 
- Both have branch management 
- Both integrate with CI/CD pipelines 
  
Azure Repos specific features: 
- Branch Policies (enforce quality gates on merges) 
- PR Templates (standardize code review) 
- Work Item integration (link PRs to Boards tasks) 
- Native integration with Azure Pipelines 
 
Q125. What is a Pull Request and why is it important? 
Pull Request (PR) = request to review your code changes 
before they are merged into the main branch. 
  
PR workflow: 
1. Developer creates feature branch 
2. Writes code on feature branch 
3. Pushes branch → Opens PR: "merge feature → main" 
4. Reviewer assigned → reviews code, leaves comments 
5. Developer addresses comments → Reviewer approves 
6. PR merged to main | Feature branch deleted 
  
Why PRs are important: 
✅ Code Quality: another person reviews before merge 
✅ Knowledge Sharing: team sees what others build 
✅ Traceability: full audit trail of changes 
✅ Protection: prevents direct pushes to main 
 
Q126. What is a PR Template and where do you store it? 
PR Template = markdown file that automatically pre-fills 
the Pull Request description when someone creates a new PR. 
  
Where to store it (MUST be exact): 
.azuredevops/pull_request_template.md 
  
Must be: In root of repository | Committed to MAIN branch 
  
Example content:

## Section / Page 50

## Type of Change 
- [ ] New Feature | - [ ] Bug Fix | - [ ] Refactor 
  
## What does this PR do? 
  
## Related Work Item: Closes #(Task/Bug ID)  
  
## Checklist: - [ ] No hardcoded credentials 
  
In your project: Created to standardize reviews and ensure 
every PR links to a work item. 
 
Q127. What are Branch Policies and what policies did you configure? 
Branch Policies = rules that protect important branches and 
enforce quality standards before code can be merged. 
  
What I configured: 
✅ Minimum 1 reviewer (someone else must approve) 
✅ No self-approval (cannot approve your own PR) 
✅ Check for linked work items (must link to a Task) 
✅ Build validation (CI pipeline must pass) 
✅ All comments resolved before merge 
  
Result: 
- Direct pushes to main: BLOCKED ❌ 
- Code without review: BLOCKED ❌ 
- Failed builds: BLOCKED from merging ✅ 
  
Configure at: 
Project Settings → Repositories → Branches → main → Branch Policies 
 
Q128. What is Azure Artifacts and how is it similar to Nexus? 
Azure Artifacts = Azure DevOps's package management service. 
Stores, manages, and shares code packages. 
  
What it stores: 
- Maven packages (Java JAR/WAR files) 
- npm packages (Node.js) 
- NuGet packages (.NET) | PyPI packages (Python) 
  
Similar to Nexus (used with Jenkins): 
Jenkins → Nexus Repository (common combo) 
Azure DevOps → Azure Artifacts (native combo) 
  
Both: Store build artifacts | Version management | Team access 
  
I did NOT use Azure Artifacts in my project — 
WAR file was copied directly by the same pipeline. 
But I understand the concept. 
 
Q129. What is Azure Test Plans and how is it different from SonarQube? 
Azure Test Plans: 
- MANUAL testing management tool

## Section / Page 51

- HUMANS create and execute test cases manually 
- "Click login button → verify redirect" 
- Useful for: UAT, regression testing 
- Similar to: TestRail, Zephyr 
  
SonarQube: 
- AUTOMATED code quality analysis tool 
- Runs automatically in CI pipeline 
- Scans code for: Bugs, Vulnerabilities, Code smells 
- No human involvement — fully automated 
  
Key difference: 
Azure Test Plans = HUMAN testing (does the button work?) 
SonarQube = AUTOMATED code analysis (is there a null pointer exception?)

## Section / Page 52

☁️ AZURE PIPELINES (Q130–Q155) 
 
Q130. What is the structure of a YAML pipeline in Azure DevOps? 
YAML pipeline defines your entire CI/CD workflow as code. 
  
Complete structure: 
trigger:                    # when to run  
- main 
  
pool:                       # which agent  
  name: Default 
  
variables:                  # reusable values 
  buildConfig: Release 
  
stages:                     # top-level phases 
- stage: Build 
  jobs:                     # units of work  
  - job: BuildJob 
    steps:                  # individual actions  
    - script: mvn clean package 
  
- stage: Test 
  dependsOn: Build          # runs after Build  
  condition: succeeded()    # only if Build succeeded  
  
Hierarchy: Pipeline → Stages → Jobs → Steps 
 
Q131. What is the difference between trigger, pool, stages, jobs and steps? 
trigger: Defines WHEN the pipeline runs automatically.  
  trigger: [main] → runs when code pushed to main branch.  
  
pool: Defines WHERE the pipeline runs (which agent).  
  pool: name: Default → Self-hosted agent pool 
  
stages: Top-level phases. Run SEQUENTIALLY by default.  
  Examples: Build, Test, DeployDev, DeployProd  
  
jobs: Units of work INSIDE a stage. 
  Jobs within a stage can run in PARALLEL.  
  Each job runs on a separate agent. 
  
steps: Individual actions INSIDE a job. Run SEQUENTIALLY. 
  task:   pre-built action (Maven@3, Docker@2)  
  script: raw shell/bash command  
  
Summary: 
trigger → when | pool → where | stage → phase  
job → group of work | step → individual action 
 
Q132. What is dependsOn and condition in a pipeline? 
dependsOn: Defines which stage/job must complete BEFORE this one. 
  
Example: 
- stage: Test

## Section / Page 53

dependsOn: Build      ← Test only starts after Build completes  
  
- stage: Deploy 
  dependsOn: 
  - Build 
  - Test               ← Deploy waits for BOTH Build AND Test  
  
Without dependsOn: All stages run in parallel! 
  
condition: Defines WHEN a stage/job should run. 
  
Common conditions: 
condition: succeeded()      # run only if previous stage passed 
condition: failed()         # run only if previous stage FAILED 
condition: always()         # run regardless of previous result 
  
In your project: dependsOn + condition: succeeded() on each stage. 
Test only runs if Build passed. Deploy only if Tests passed. ✅ 
 
Q133. What is condition: succeeded() and when do you use it? 
condition: succeeded() means: 
"Run this stage ONLY if the previous stage SUCCEEDED"  
  
Pipeline flow: 
Stage 1: Build          → runs always (first stage) 
Stage 2: Test           → runs only if Build succeeded 
Stage 3: DeployStaging  → runs only if Test succeeded 
Stage 4: DeployProd     → runs only if DeployStaging succeeded 
  
WITHOUT condition (default): 
If Build fails → Test STILL runs (wasted time!) 
If Test fails  → Deploy STILL runs (deploys broken code! 😱) 
  
WITH condition: succeeded(): 
If Build fails → Test is SKIPPED ✅ (no wasted time) 
If Test fails  → Deploy is SKIPPED ✅ (no broken code!) 
  
Use condition: failed() for: send failure notification, cleanup steps 
 
Q134. What are Variables in Azure Pipelines — what types exist? 
1. Inline YAML Variables: 
   variables: 
     appName: myapp 
   Reference: $(appName) 
  
2. Pipeline UI Variables: 
   Defined in Azure DevOps web UI. Can change without editing YAML.  
  
3. Variable Groups (Library): 
   Shared across MULTIPLE pipelines. Create once, use everywhere.  
  
4. Secret Variables: 
   Encrypted, never shown in logs (shows as ***).  
   Use for: passwords, API keys, tokens.

## Section / Page 54

5. System/Built-in Variables: 
   $(Build.BuildNumber) | $(Build.SourceBranch) | $(Agent.OS)  
  
6. Runtime Parameters: 
   User inputs when manually triggering pipeline.  
  
Best practice: NEVER hardcode passwords in YAML! 
Use Secret Variables or Azure Key Vault ✅ 
 
Q135. What is a Variable Group and when do you use it? 
Variable Group = named set of variables defined ONCE 
and reusable across MULTIPLE pipelines. 
  
Without Variable Groups: 
Pipeline A, B, C all define: appName: myapp, dbHost: prod-db-01 
DB host changes → update in 3 pipelines ❌ 
  
With Variable Groups: 
Create group "Production-Settings": 
  appName: myapp | dbHost: prod-db-01 
  
All 3 pipelines reference: 
variables: 
  - group: Production-Settings 
  
DB host changes → update in ONE place ✅ 
  
Create at: Pipelines → Library → + Variable Group 
  
Important: Can mark variables as SECRET (locked and encrypted). 
 
Q136. What is Azure Key Vault integration with pipelines? 
Azure Key Vault = securely stores secrets, keys, and certificates. 
Integrating with Azure Pipelines → pipelines use secrets without hardcoding. 
  
Why Azure Key Vault: 
✅ Secrets stored SEPARATELY from code and pipelines 
✅ Central secret management | ✅ Access controlled by Azure AD 
✅ Automatic rotation support | ✅ Audit trail 
  
How integration works: 
1. Create secrets in Azure Key Vault: 
   DatabasePassword → mySecretPass123  
  
2. Create Variable Group linked to Key Vault: 
   Pipelines → Library → + Variable Group 
   Toggle: "Link secrets from Azure Key Vault"  
  
3. Reference in YAML: 
variables: 
  - group: KeyVaultSecrets 
  
Shows as *** in logs — NEVER in YAML or source code ✅

## Section / Page 55

Q137. What is a Service Connection and what types did you use? 
Service Connection = secure, stored connection to external service 
used by Azure DevOps pipelines. 
  
Instead of hardcoding credentials in YAML: 
- Store credentials ONCE in Service Connections 
- Reference by name in pipeline 
  
Types: 
Azure Resource Manager: Connect to Azure subscription 
Docker Registry: Connect to Docker Hub, ACR, or private registry 
GitHub: Connect to GitHub repository 
SSH: Connect to Linux server via SSH 
Kubernetes: Connect to Kubernetes cluster 
SonarQube: Connect to SonarQube server 
  
Create at: Project Settings → Service Connections → + New 
  
In your project: 
Used SSH Service Connection to connect pipeline to Azure VM 
for deploying WAR files to Tomcat. 
 
Q138. What is an Environment in Azure DevOps? 
Environment = logical target for deployment. 
Represents real-world infrastructure: Development, Staging, Production. 
  
What Environments give you: 
1. Deployment History: Every deployment recorded (who, when, version) 
2. Approval Gates: Require human approval before deploying 
3. Checks: Branch control | Business hours | Custom validation 
4. Resource Tracking: See which version deployed where RIGHT NOW 
  
Create at: Pipelines → Environments → + New Environment 
  
Using in YAML: 
jobs: 
- deployment: DeployToProd 
  environment: Production   ← must match environment name  
  strategy: 
    runOnce: 
      deploy: 
        steps: 
        - script: echo "Deploying to production"  
 
Q139. What is an Approval Gate and when would you use it? 
Approval Gate = human checkpoint where someone must APPROVE or REJECT 
before the pipeline continues. 
  
Why use Approvals: 
- Production is risky — human should verify staging first 
- Compliance — someone must sign off on production deploys 
- Reduces accidental production deployments 
  
How to set up:

## Section / Page 56

Pipelines → Environments → Production → "..." → Approvals and Checks 
→ Add Approval → assign approver(s) 
  
What happens: 
1. Pipeline PAUSES 😱 
2. Email sent to approver: "Deployment waiting for approval" 
3. Approver reviews → clicks APPROVE ✅ → pipeline continues 
   OR REJECT ❌ → pipeline stops 
  
Pipeline flow: 
Build ✅ → Test ✅ → Deploy Staging ✅ 
   ↓ [PAUSE] Email to manager → Manager approves  
Deploy Production ✅ 
 
Q140. What is a self-hosted agent? 
Self-hosted agent = YOUR OWN VM registered with Azure DevOps to run pipeline jobs. 
  
Microsoft-Hosted Agent (default): 
- Microsoft provides and manages the VM 
- Fresh VM for every pipeline run 
- Free minutes (1800/month) 
- Cannot control the environment 
  
Self-Hosted Agent (what you used): 
- YOUR OWN VM or server running agent software 
- Same machine every time (persistent state) 
- UNLIMITED free pipeline minutes 
- Full control over installed tools 
  
Why you used self-hosted: 
Your pipeline needed to: 
- Copy WAR file to /opt/tomcat1/webapps/ 
- Restart Tomcat service 
Both require DIRECT access to your Azure VM. 
Only possible with self-hosted agent ON THAT SAME VM! 
 
Q141. What are the steps to set up a self-hosted agent? 
Step 1: Create PAT (Personal Access Token) 
  Azure DevOps → User Settings → Personal Access Tokens → New Token  
  Scope: Agent Pools: Read & Manage | Copy token (shown only ONCE!)  
  
Step 2: Create agent folder and download 
mkdir ~/myagent && cd ~/myagent  
tar zxvf vsts-agent-linux-x64-*.tar.gz 
  
Step 3: Configure the agent 
./config.sh 
  Server URL: https://dev.azure.com/YourOrgName  
  Auth: PAT | Pool: Default | Agent name: myagent  
  
Step 4: Start the agent 
./run.sh 
  Should see: "Listening for Jobs" ✅ 
  
Step 5: Verify in Azure DevOps 
  Organization Settings → Agent Pools → Default

## Section / Page 57

Agent shows as ONLINE (green dot)  
  
Step 6: Reference in pipeline YAML 
pool: 
  name: Default     ← Use POOL name, NOT agent name!  
 
Q142. Why did you choose self-hosted agent over Microsoft-hosted agent? 
I chose self-hosted for one main reason — DIRECT FILE SYSTEM ACCESS. 
  
My pipeline needed to: 
- Copy WAR file to /opt/tomcat1/webapps/ 
- Restart: /opt/tomcat1/bin/shutdown.sh && startup.sh 
  
Microsoft-hosted agent: 
- Runs on a DIFFERENT VM (Microsoft's machine) 
- Cannot access /opt/tomcat1/ on MY Azure VM 
- Would need SSH setup → complex, security risk ❌ 
  
Self-hosted agent (running on MY Azure VM): 
- Agent IS on the same VM as Tomcat 
- cp target/*.war /opt/tomcat1/webapps/ → works directly! 
- No network hop ✅ | More secure ✅ | Faster ✅ 
  
Additional benefits: 
✅ Free unlimited pipeline minutes 
✅ Pre-installed tools (Java, Maven already there) 
✅ Persistent workspace 
 
Q143. What is a PAT token and what did you use it for? 
PAT = Personal Access Token. 
Password substitute for authenticating tools to Azure DevOps. 
  
Creating a PAT: 
Azure DevOps → User Settings → Personal Access Tokens → New Token 
Set name, expiry date, scope (minimum permissions) 
Create → COPY IMMEDIATELY (shown only ONCE!) 
  
Common scopes: 
Agent Pools: Read & Manage → for registering agents 
Code: Read & Write         → for git operations 
  
What I used my PAT for: 
1. Registering self-hosted agent: ./config.sh → enter PAT when prompted 
2. Git clone authentication: 
   git clone https://user:PAT@dev.azure.com/org/repo  
  
Security: 
✅ Set expiry date (never "no expiry") 
✅ NEVER commit PAT to Git 
✅ Revoke immediately if compromised 
 
Q144. What is the difference between pool name and agent name? 
This is a VERY COMMON mistake when setting up pipelines!

## Section / Page 58

Agent Name: The name of a SPECIFIC agent machine. 
  Set during ./config.sh ("Agent name: myagent")  
  Example: "myagent", "build-server-1" 
  
Pool Name: A COLLECTION of agents. 
  Multiple agents belong to one pool.  
  Pipelines target POOLS, not individual agents.  
  Default pool is called "Default".  
  
WRONG ❌: 
pool: 
  name: myagent     ← This is AGENT name, not pool! 
  (Error: "No agent found matching the criteria")  
  
CORRECT ✅: 
pool: 
  name: Default              # Pool name  
  demands: 
  - Agent.Name -equals myagent  # Optional: target specific agent  
  
In your project: Common error I faced! 
Fix: Change pool: name: myagent → pool: name: Default 
 
Q145. What are the common errors when setting up a self-hosted agent? 
Error 1: VS30063 — Unauthorized 
  Cause: Wrong PAT token or PAT expired  
  Fix: Create new PAT with scope "Agent Pools: Read & Manage"  
  
Error 2: Pool not found / Agent not matching 
  Cause: Used agent name instead of pool name in YAML  
  Fix: pool: name: Default  ← NOT: name: myagent  
  
Error 3: Agent offline in Azure DevOps 
  Cause: run.sh is not running on the VM  
  Fix: ssh into VM → cd ~/myagent → ./run.sh  
  To keep running: nohup ./run.sh &  
  
Error 4: Permission denied errors during pipeline 
  Cause: Agent user lacks permission to access folders  
  Fix: sudo chown -R $USER:$USER /opt/tomcat1 
  
Error 5: Git authentication failure 
  Cause: PAT doesn't have Code: Read permission  
  Fix: Create new PAT with Code: Read & Write scope  
 
Q146. What is CI vs CD vs Continuous Deployment? 
CI — Continuous Integration: 
"Every code change automatically builds and tests"  
  
Developer pushes code → Pipeline AUTOMATICALLY triggers → 
Build → Run automated tests → Report results (pass/fail) 
  
Goal: Catch bugs EARLY. Frequency: Multiple times per day. 
  
CD — Continuous Delivery: 
"Tested code auto-deployed to staging, HUMAN approves production"

## Section / Page 59

CI passes → Auto-deploy to Staging → [HUMAN approves] → Deploy to Production 
  
Goal: Always have production-ready artifact. 
  
Continuous Deployment: 
"Everything is fully automated, NO human approval"  
  
CI passes → Auto-deploy to Staging → Auto-deploy to Production 
  
In your project: CI + Continuous Delivery: 
Code push → Build → Test (CI) 
Test pass → Auto-deploy to Tomcat 1 and 2 (CD) 
 
Q147. What are the stages in YOUR Azure DevOps pipeline? 
My pipeline had 4 stages: 
  
Stage 1: BUILD 
  Trigger: push to main branch 
  What happens: mvn clean package  
  Output: target/myapp.war file created  
  Runs on: self-hosted agent (my Azure VM) 
  
Stage 2: TEST 
  Depends on: Build | Condition: succeeded()  
  What happens: mvn test 
  If tests fail → pipeline STOPS, no deployment!  
  
Stage 3: DEPLOY TO TOMCAT 1 
  Depends on: Test | Condition: succeeded()  
  What happens: 
  cp target/myapp.war /opt/tomcat1/webapps/ 
  /opt/tomcat1/bin/shutdown.sh → sleep 5 → startup.sh  
  Tomcat 1 now running new version on port 7789  
  
Stage 4: DEPLOY TO TOMCAT 2 
  Same as Stage 3 but for Tomcat 2 (port 8888)  
  
Full flow: git push → Build WAR → Tests → Deploy T1 → Deploy T2 
 
Q148. What happens if one stage fails in your pipeline? 
With condition: succeeded() on each stage: 
  
If BUILD fails: 
- Test SKIPPED | Deploy T1 SKIPPED | Deploy T2 SKIPPED 
- Pipeline marked FAILED | Developer gets notification 
- No broken code deployed ✅ 
  
If TEST fails: 
- Deploy Tomcat 1 SKIPPED | Deploy Tomcat 2 SKIPPED 
- Bug needs to be fixed and code pushed again 
  
If DEPLOY TOMCAT 1 fails: 
- Tomcat 2 deployment SKIPPED 
- Investigate why deployment failed (disk? permissions?)

## Section / Page 60

Exception — using condition: always(): 
- stage: Notify 
  condition: failed()   ← runs ONLY when something failed  
  steps: 
  - script: send_slack_alert.sh 
  
In your project: Either everything deploys or nothing deploys ✅

## Section / Page 61

☁️ AZURE DEVOPS SCENARIO QUESTIONS (Q149–Q155) 
 
Q149. Your pipeline is triggered but the agent is offline — what do you check? 
Step 1: Verify agent status in Azure DevOps 
  Organization Settings → Agent Pools → Default  
  Is your agent Offline (red) or Online (green)?  
  
Step 2: SSH into your Azure VM (where agent is installed) 
  ssh -i key.pem azureuser@<vm-ip> 
  
Step 3: Check if agent process is running 
  ps aux | grep agent 
  
Step 4: Start the agent 
  cd ~/myagent 
  ./run.sh  (should show: "Listening for Jobs")  
  
Step 5: Keep agent running after logout 
  nohup ./run.sh > agent.log 2>&1 &  
  OR set up as system service: 
  ./svc.sh install && ./svc.sh start  
  
Most common cause: Agent stopped because VM restarted or SSH session ended. 
Solution: Configure agent as a system service (auto-starts on boot). 
 
Q150. Your pipeline deploys successfully but the application is not updated — what 
do you check? 
Step 1: Verify WAR file was actually copied 
  ls -lh /opt/tomcat1/webapps/ 
  Check TIMESTAMP — is it recent? 
  
Step 2: Check if Tomcat restarted 
  ps aux | grep tomcat 
  tail -f /opt/tomcat1/logs/catalina.out  
  
Step 3: Check shutdown/startup timing 
  If startup runs before shutdown completes → issue!  
  Fix: add sleep between shutdown and startup:  
  /opt/tomcat1/bin/shutdown.sh 
  sleep 5 
  /opt/tomcat1/bin/startup.sh 
  
Step 4: Clear browser cache 
  Open in incognito/private mode.  
  Hard refresh: Ctrl + Shift + R 
  
Most common causes: 
1. Browser caching old version 
2. Tomcat not restarted properly 
3. WAR copied to wrong path 
 
Q151. A developer merged code without review — how do you prevent this from 
happening again? 
Immediate action: 
  Revert the merge if it introduced issues:

## Section / Page 62

git revert <merge-commit-id> 
  
Prevention — configure Branch Policies on main branch: 
  
Step 1: Go to Branch Policies 
  Project Settings → Repositories → Branches → main → Branch Policies  
  
Step 2: Enable "Require minimum number of reviewers" 
  Minimum: 1 or 2 
  DISABLE: "Allow requestors to approve their own changes"  
  
Step 3: Enable "Build validation" 
  CI pipeline must pass before merge is allowed.  
  
Step 4: Check user permissions 
  Ensure no one has "Force push" or "Bypass policies" permission.  
  
After policies are set: 
- Direct push to main → BLOCKED ❌ 
- PR without approval → BLOCKED ❌ 
- PR without passing build → BLOCKED ❌ 
 
Q152. Your pipeline is slow and taking 45 minutes — how do you optimize it? 
Step 1: Identify which stage is slowest 
  Look at pipeline run logs — each stage shows duration. 
  
Step 2: Optimize Maven/npm dependencies 
  Maven: cache ~/.m2/repository between runs  
  npm: cache node_modules folder  
  
Step 3: Run tests in parallel 
  Split into groups → run multiple jobs simultaneously.  
  
Step 4: Use Docker layer caching 
  COPY package.json first → npm install → COPY code  
  (npm install cached if package.json unchanged)  
  
Step 5: Skip unnecessary steps on feature branches 
  condition: eq(variables['Build.SourceBranch'], 'refs/heads/main')  
  
Step 6: Use artifacts instead of rebuilding 
  Build WAR once → store as artifact → reuse in deploy stage.  
  
Step 7: Use self-hosted agent 
  No VM startup time | Pre-installed tools | Persistent cache 
 
Q153. The self-hosted agent keeps going offline — what could be the reason? 
Reason 1: Agent started with SSH session and session ended 
  Fix: nohup ./run.sh > ~/myagent/agent.log 2>&1 &  
  Better: sudo ./svc.sh install && sudo ./svc.sh start  
  
Reason 2: VM was restarted 
  Fix: Configure as system service (auto-starts on boot) 
  
Reason 3: PAT token expired 
  Fix: Create new PAT → ./config.sh --unattended --replace

## Section / Page 63

Reason 4: Memory or CPU pressure on VM 
  Fix: Upgrade VM size or check what else is running 
  
Reason 5: Azure VM auto-shutdown configured 
  Fix: Disable auto-shutdown for agent VM 
  
Reason 6: Network connectivity issues 
  Fix: Check outbound internet | Azure DevOps requires port 443 outbound  
  
Best practice: ALWAYS run agent as a system service! 
 
Q154. Your pipeline cannot connect to the Azure VM to deploy — what do you check? 
Since you use self-hosted agent ON the same VM, 
this means the deploy script is failing to access Tomcat folders. 
  
Step 1: Check agent is online and picked up the job 
  Azure DevOps → Agent Pools → Default → agent online?  
  
Step 2: Check file permissions 
  ls -la /opt/tomcat1/webapps/ 
  Can the agent user write to this directory?  
  Fix: sudo chown -R $USER:$USER /opt/tomcat1/ 
  
Step 3: Check if path is correct in YAML 
  ls /opt/  ← verify exact path on the VM  
  
Step 4: Check if Tomcat user conflicts 
  Tomcat may be owned by "tomcat" user  
  Agent runs as "azureuser" → permission conflict!  
  Fix: Add agent user to tomcat group or use sudo in script 
  
Step 5: Verify pipeline commands: 
- script: | 
    cp $(Build.ArtifactStagingDirectory)/myapp.war /opt/tomcat1/webapps/  
    sudo systemctl restart tomcat1  
 
Q155. Two developers pushed code at the same time — what happens to the pipeline? 
Developer A pushes commit X at 10:00:00 
Developer B pushes commit Y at 10:00:05 
  
Option A — Both trigger separate pipelines: 
- Pipeline run 1 starts for commit X 
- Pipeline run 2 starts for commit Y 
- Both run simultaneously (if agents available) 
- Both may try to deploy → potential CONFLICT! 
  
Option B — Pipeline batching (recommended): 
- Enable "Batch changes while a build is in progress" 
- Batches X and Y together → ONE new run with latest code (Y) 
  
How to configure batching: 
trigger: 
  batch: true   ← enable batching  
  branches: 
    include:

## Section / Page 64

- main 
  
Best practice: 
Enable batch: true for production pipelines. 
Deploy only from main branch (after PR review). 
Prevents race conditions in deployments.

## Section / Page 65

☁️ DOCKER — Basics & Dockerfile (Q156–Q173) 
 
Q156. What is Docker and what problem does it solve? 
Docker = platform for building, shipping, and running apps in containers. 
  
The problem Docker solves: 
"It works on my machine!" problem:  
Developer: "My code works perfectly on my laptop" 
Server:    "App crashes with missing dependency!" 
  
Docker solution: Package EVERYTHING together: 
App code + Dependencies + Libraries + Config + OS libraries 
into ONE container image. 
  
Run the same image EVERYWHERE: 
✅ Developer laptop | ✅ Test server | ✅ Production server 
Same behavior everywhere! 
  
In your project: You containerized Node.js backend and Apache frontend 
using Docker for the Kubernetes deployment on AWS. 
 
Q157. What is the difference between a VM and a Container? 
Virtual Machine (VM): 
- Full operating system per VM (GBs in size) 
- Hypervisor (VMware, VirtualBox) manages VMs 
- Startup: minutes | Strong isolation (separate OS) 
  
Container: 
- Shares HOST OS kernel (MBs in size) 
- Docker Engine manages containers 
- Startup: seconds | Process-level isolation 
  
VM use cases: 
- Need different OS | Strong isolation | Legacy applications 
  
Container use cases: 
- Microservices | Modern cloud-native apps | CI/CD | Fast scaling 
  
Simple analogy: 
VM        = Separate house (own everything) 
Container = Separate room in same house (share foundation) 
 
Q158. What is a Dockerfile, Image and Container — explain all three? 
Dockerfile: 
- Plain text file with instructions to BUILD an image 
- Written by developers, stored in Git 
- Contains: base image, install commands, copy files, start command 
  
Docker Image: 
- Built FROM Dockerfile using: docker build 
- Read-only blueprint/template 
- Stored in registry (Docker Hub, ECR, ACR)

## Section / Page 66

- Immutable (cannot be changed once built) 
  
Docker Container: 
- RUNNING instance created FROM an image 
- Has own filesystem, network, process space 
- Can be started, stopped, restarted, deleted 
- Multiple containers can run from same image 
  
Flow: Dockerfile → docker build → Image → docker run → Container 
  
Analogy: 
Dockerfile = Recipe | Image = Cake mould | Container = Actual Cake 
 
Q159. What is a Docker Registry and give examples? 
Docker Registry = storage and distribution system for Docker images. 
  
Public Registries (anyone can access): 
- Docker Hub (hub.docker.com) — most popular, DEFAULT 
  All official images: nginx, ubuntu, node, postgres  
  
Private Registries (access controlled): 
- AWS ECR (Elastic Container Registry) — AWS native 
- Azure ACR (Azure Container Registry) — Azure native 
- GitHub Container Registry (ghcr.io) 
- JFrog Artifactory | Self-hosted registry 
  
Workflow: 
Developer builds → docker push → Registry stores → 
Server: docker pull ← Registry → Container runs 
  
In your project: 
Used ECR for Docker images for Kubernetes deployment. 
kOps K8s nodes pulled images from ECR to run pods. 
 
Q160. What is Docker Hub? 
Docker Hub = world's largest public container registry. 
Docker's official cloud-based registry service. 
  
What Docker Hub provides: 
- Official Images: pre-built base images by Docker/companies 
  ubuntu, nginx, node, python, postgres, redis, maven  
- Community Images: millions of images by community 
- Private Repositories: store your own private images 
  
Docker Hub is the DEFAULT registry: 
docker pull nginx 
→ Actually pulls from: docker.io/library/nginx:latest 
  
Commands: 
docker pull nginx:latest       # pull official image  
docker login                   # authenticate  
docker push username/myapp:1.0 # push to Docker Hub  
docker search nginx            # search images

## Section / Page 67

Q161. What is the flow from Dockerfile to running container? 
Step 1: Write Dockerfile 
FROM node:18-alpine 
WORKDIR /app 
COPY . . 
RUN npm install 
EXPOSE 3000 
CMD ["node", "app.js"] 
  
Step 2: Build Image 
docker build -t myapp:1.0 . 
  
Step 3: Verify image was created 
docker images 
# Shows: myapp   1.0   abc123   2 minutes ago   150MB  
  
Step 4: Run container from image 
docker run -d -p 3000:3000 --name mycontainer myapp:1.0 
  
Step 5: Verify container is running 
docker ps 
  
Step 6: Check logs 
docker logs -f mycontainer 
  
Step 7: Stop and remove 
docker stop mycontainer && docker rm mycontainer  
 
Q162. What does FROM do in a Dockerfile? 
FROM specifies the BASE IMAGE to build upon.  
Always the FIRST instruction in a Dockerfile. 
  
Examples: 
FROM ubuntu:22.04          # Ubuntu OS as base  
FROM node:18-alpine        # Node.js (alpine = small!)  
FROM maven:3.9             # Maven for building Java  
FROM nginx:alpine          # Nginx web server  
  
Why base images matter: 
FROM ubuntu:22.04          # 70MB  
FROM node:18               # 900MB (Ubuntu + Node.js)  
FROM node:18-alpine        # 150MB (Alpine + Node.js) ← preferred! 
  
In multi-stage builds: 
FROM maven:3.9 AS builder  # Stage 1 (build)  
FROM tomcat:11-alpine      # Stage 2 (runtime)  
  
Best practices: 
✅ Use specific versions (node:18, not node:latest) 
✅ Use alpine variants when possible 
 
Q163. What does RUN do and when does it execute? 
RUN executes a command during IMAGE BUILD process.  
Creates a new LAYER in the image. 
Executes at BUILD TIME — NOT when container starts!

## Section / Page 68

Common uses: 
RUN apt-get update && apt-get install -y nginx 
RUN npm install 
RUN mkdir -p /app/logs 
RUN chmod +x /app/start.sh 
  
Best practices — Combine multiple RUN into ONE: 
  
BAD (3 layers, larger image): 
RUN apt-get update 
RUN apt-get install -y nginx 
RUN apt-get install -y curl 
  
GOOD (1 layer, smaller image): 
RUN apt-get update && \ 
    apt-get install -y nginx curl && \ 
    rm -rf /var/lib/apt/lists/* 
 
Q164. What does CMD do and when does it execute? 
CMD specifies the DEFAULT command when container STARTS.  
Executes at RUNTIME (not build time). 
  
Default = can be OVERRIDDEN: 
docker run myimage                   # uses CMD  
docker run myimage python other.py   # overrides CMD  
  
Formats: 
CMD ["node", "app.js"]               # Exec format (preferred)  
CMD node app.js                      # Shell format  
  
Examples: 
CMD ["nginx", "-g", "daemon off;"]   # start nginx  
CMD ["java", "-jar", "app.jar"]      # start Java  
CMD ["npm", "start"]                 # start Node.js  
  
Only ONE CMD is used — if multiple, only LAST one is used. 
 
Q165. What does ENTRYPOINT do and how is it different from CMD? 
ENTRYPOINT defines the FIXED main command — NOT easily overridden. 
  
CMD: Default command. COMPLETELY overridden by docker run command.  
ENTRYPOINT: Fixed command. Arguments from docker run are APPENDED. 
  
Using both together (most flexible): 
ENTRYPOINT ["java", "-jar"] 
CMD ["app.jar"] 
  
docker run myapp              # runs: java -jar app.jar 
docker run myapp newapp.jar   # runs: java -jar newapp.jar 
(CMD overridden, ENTRYPOINT stays) 
  
Real analogy: 
ENTRYPOINT = The verb (always do THIS) 
CMD        = The default noun (do this BY DEFAULT)  
  
Use ENTRYPOINT when: 
- Container should always run a specific program

## Section / Page 69

- Use container like a command (CLI tool) 
 
Q166. What does COPY do? 
COPY copies files from BUILD CONTEXT (your local machine) INTO the Docker image.  
  
Syntax: COPY <source> <destination> 
  
Examples: 
COPY app.js /app/               # copy single file  
COPY src/ /app/src/             # copy entire directory  
COPY package*.json /app/        # copy with wildcard  
COPY . /app/                    # copy everything  
  
Best practice — copy in order of change frequency: 
  
# SLOW CHANGE (copy first for better caching) 
COPY package.json ./ 
RUN npm install          # ← cached unless package.json changes  
  
# FAST CHANGE (copy last) 
COPY . .                 # ← fresh copy every time  
  
COPY = simple copy (use this 99% of the time) ✅ 
ADD = copy + auto-extract tar + download URL (avoid unless needed) 
 
Q167. What does ADD do and how is it different from COPY? 
ADD is similar to COPY but has two EXTRA features: 
  
Feature 1: Auto-extract archives 
ADD app.tar.gz /app/ 
→ Automatically extracts .tar.gz into /app/ 
(COPY would just copy the .tar.gz as-is) 
  
Feature 2: Download from URL 
ADD https://example.com/file.txt /app/ 
→ Downloads file from internet and adds to image 
(COPY cannot do this) 
  
Best practice: 
✅ Use COPY for everything by default 
✅ Use ADD ONLY when need to auto-extract a tar archive 
✅ Use ADD ONLY when need to download a file from URL 
  
Why avoid ADD unnecessarily: 
- ADD from URL can have security risks 
- ADD behavior is less predictable 
- COPY is explicit and clear 
 
Q168. What does WORKDIR do? 
WORKDIR sets the working directory for all subsequent instructions.  
Think of it as: cd /path in your Dockerfile. 
  
Without WORKDIR (verbose and error-prone): 
COPY . /app/src/myproject/

## Section / Page 70

RUN cd /app/src/myproject && npm install  
CMD ["node", "/app/src/myproject/app.js"]  
  
With WORKDIR (clean and simple): 
WORKDIR /app               # all following commands run from /app  
COPY . .                   # copies to /app/  
RUN npm install            # runs in /app/  
CMD ["node", "app.js"]     # runs from /app/  
  
Benefits: 
✅ Cleaner, shorter instructions 
✅ Creates directory if it doesn't exist 
  
Best practice: Always set WORKDIR before COPY and RUN. 
Prefer /app as standard directory name. 
 
Q169. What does EXPOSE do — does it actually publish the port? 
EXPOSE documents which port the container listens on.  
But NO — it does NOT actually publish or open the port! 
  
EXPOSE is just DOCUMENTATION (metadata).  
  
EXPOSE 3000 
# Tells Docker: "this container uses port 3000"  
# But port is NOT accessible from outside!  
  
To actually publish → use -p in docker run: 
docker run -p 8080:3000 myapp 
# -p host_port:container_port 
# Now http://localhost:8080 → container port 3000  
  
What EXPOSE actually does: 
1. Documentation: tells developers which port to expect 
2. Inter-container communication on same Docker network 
3. Used by docker run -P: publishes ALL exposed ports to random host ports 
  
Summary: 
EXPOSE 3000   → "Container uses port 3000" (info only) 
docker run -p → Actually maps host port to container port  
 
Q170. What does ENV do? 
ENV sets environment variables inside the container.  
Available at BOTH build time AND runtime. 
  
Syntax: 
ENV NODE_ENV=production 
ENV PORT=3000 
  
Multiple variables: 
ENV NODE_ENV=production \ 
    PORT=3000 \ 
    APP_VERSION=1.0 
  
Accessing in application: 
Node.js: process.env.NODE_ENV 
Python:  os.environ["NODE_ENV"] 
Shell:   $NODE_ENV

## Section / Page 71

Override at runtime: 
docker run -e NODE_ENV=development myapp 
  
ENV vs ARG: 
ENV: Available during BUILD and at RUNTIME ✅ 
ARG: Available ONLY during BUILD (not at runtime) 
  
Best practice: Do NOT use ENV for secrets/passwords! 
Use Docker secrets for sensitive data. 
 
Q171. What does ARG do and how is it different from ENV? 
ARG defines a BUILD-TIME argument — variable passed to docker build.  
  
Syntax in Dockerfile: 
ARG VERSION=1.0 
ARG BASE_IMAGE=node:18-alpine 
  
Passing ARG value during build: 
docker build --build-arg VERSION=2.0 . 
docker build --build-arg BASE_IMAGE=node:20-alpine . 
  
ARG vs ENV comparison: 
Feature               ARG               ENV 
When available        Build time ONLY   Build + Runtime 
Visible in container  No                Yes (docker inspect) 
Override at runtime   No                Yes (-e flag) 
Use for               Build config      Runtime config 
  
Combined pattern: 
ARG APP_VERSION=1.0 
ENV APP_VERSION=$APP_VERSION 
# ARG receives build-time value → ENV makes it available at runtime  
 
Q172. What does USER do and why is it important for security? 
USER sets the user that will run subsequent instructions and container process.  
  
Example: 
FROM node:18-alpine 
WORKDIR /app 
COPY . . 
RUN npm install 
RUN addgroup -S appgroup && adduser -S appuser -G appgroup 
USER appuser              # Switch to non-root user 
CMD ["node", "app.js"]    # runs as appuser, NOT root  
  
Why USER is important for SECURITY: 
By default, Docker containers run as ROOT user! 
  
Root inside container = very privileged: 
- If hacked → attacker has root 
- Root can write to any file 
- Container escape → attacker has root on HOST OS! 
  
Using non-root user: 
- If hacked → attacker only has limited user ✅ 
- Reduced blast radius of compromise ✅

## Section / Page 72

Security best practice: ALWAYS run containers as non-root in production! 
USER nobody    ← built-in restricted user 
 
Q173. What is the best practice order of instructions in a Dockerfile? 
Order matters for BUILD CACHING and EFFICIENCY! 
If a layer changes → ALL subsequent layers REBUILT. 
  
Optimal order (least-changing to most-changing): 
  
1. FROM — base image (rarely changes) 
FROM node:18-alpine 
  
2. ENV, ARG — environment variables 
ENV NODE_ENV=production 
  
3. WORKDIR — set working directory 
WORKDIR /app 
  
4. System dependencies (rarely changes) 
RUN apk add --no-cache curl 
  
5. Dependency files BEFORE source code 
COPY package*.json ./       ← ONLY dependency file  
  
6. Install dependencies (cached unless package.json changes) 
RUN npm install 
  
7. Copy source code LAST (changes most often) 
COPY . . 
  
8. USER — switch to non-root | 9. EXPOSE — document port 
USER node 
EXPOSE 3000 
  
10. CMD — start command 
CMD ["node", "app.js"] 
  
Key benefit: Source code changes → npm install is CACHED (fast!)

## Section / Page 73

☁️ ALL 173 QUESTIONS DONE! ☁️ 
You now have answers to every question in this bank. 
Combine this with the 55 Q&A guide and you are UNSTOPPABLE! 🔥

