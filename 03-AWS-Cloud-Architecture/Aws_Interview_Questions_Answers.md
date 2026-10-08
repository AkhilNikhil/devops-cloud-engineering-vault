# 📖 Aws Interview Questions Answers
> *Converted from `Aws Interview Questions Answers.pdf` for high-readability on GitHub.*

---
## Page 1

AWS Interview Questions and Answers
Basic AWS Questions
What  is  AWS?  AWS  (Amazon  Web  Services)  is  a  cloud  computing  platform  by  Amazon  offering
scalable,  on-demand  computing  resources  like  servers,  storage,  databases,  networking,  and
analytics.
Types of cloud computing?
IaaS (Infrastructure as a Service): EC2, S3
PaaS (Platform as a Service): Elastic Beanstalk
SaaS (Software as a Service): AWS WorkMail
What is EC2? EC2 (Elastic Compute Cloud) is a virtual server in AWS that allows launching instances
with different OS, CPU, memory, and storage.
What is S3? S3 (Simple Storage Service) is an object storage service to store files, backups, static web
content. Features include durability, scalability, versioning, and lifecycle policies.
What is a VPC? VPC (Virtual Private Cloud) lets you create a private network in AWS. You can define
subnets, route tables, and security groups for secure network isolation.
What is IAM? IAM (Identity and Access Management) manages users, groups, roles, and permissions
to control who can access AWS resources.
Difference  between  Instance  Store  and  EBS  |  Feature  |  Instance  Store  |  EBS  |
|---------|---------------|-----| | Persistence | Temporary | Persistent | | Data survives | Reboot No,
Termination No | Reboot Yes, Termination Optional | | Use Case | Temporary storage, cache |
Database, logs, critical data |
What is CloudFront? CloudFront is AWS’s CDN that delivers static and dynamic content with low
latency using edge locations globally.
What is Auto Scaling? Automatically adjusts the number of EC2 instances based on demand for
performance and cost efficiency.
What is Elastic Load Balancer (ELB)? Distributes incoming traffic across multiple EC2 instances. Types:
Classic, Application (ALB), Network (NLB).
1. 
2. 
3. 
4. 
5. 
6. 
7. 
8. 
9. 
10. 
11. 
12. 
13. 
1

## Page 2

Intermediate AWS Questions
What is RDS? RDS (Relational Database Service) is a managed relational database supporting MySQL,
PostgreSQL, Oracle, SQL Server , and Aurora, handling backups, patching, and scaling.
Difference between S3 and EBS | Feature | S3 | EBS | |---------|----|-----| | Type | Object Storage |
Block Storage | | Use Case | Files, backup, media | OS, databases, EC2 volume | | Access | Over
HTTP(S) | Attached to EC2 instance |
What is Lambda? AWS Lambda is serverless computing allowing code execution without provisioning
servers, triggered by events like S3 upload or API Gateway.
What is Route 53? Scalable DNS service that can route traffic to EC2, S3, ELB, or external resources.
What is CloudWatch? Monitoring and logging service tracking metrics like CPU, memory, disk usage,
logs, and alarms.
What is CloudTrail? Tracks user and API activity in AWS, useful for auditing and compliance.
Difference  between  CloudFront  and  S3  S3:  Storage  service.  CloudFront:  CDN  for  faster  content
delivery using edge locations.
What is an AMI? AMI (Amazon Machine Image) is a template for launching EC2 instances containing
OS, software, and configuration.
What  is  a  Security  Group?  Acts  as  a  virtual  firewall  for  EC2  instances  controlling  inbound  and
outbound traffic.
What  is  a  NAT  Gateway?  Allows  instances  in  a  private  subnet  to  access  the  internet  securely;
outbound allowed, inbound restricted.
Advanced AWS Questions
AWS Elastic Beanstalk? PaaS to deploy web applications quickly, handling scaling, load balancing,
and monitoring.
Difference between Horizontal and Vertical Scaling
Horizontal Scaling: Add more EC2 instances
Vertical Scaling: Increase CPU/RAM of a single instance
What  is  AWS  Aurora?  Managed,  MySQL/PostgreSQL-compatible  relational  database  with  high
performance and scalability.
AWS ECS and EKS?
1. 
2. 
3. 
4. 
5. 
6. 
7. 
8. 
9. 
10. 
1. 
2. 
3. 
4. 
5. 
6. 
2

## Page 3

ECS: Container orchestration service using Docker
EKS: Kubernetes-managed service for container orchestration
What is AWS SQS? Simple Queue Service for decoupling distributed applications, providing reliable
message queuing.
Difference between SQS and SNS | Feature | SQS | SNS | |---------|-----|-----| | Pattern | Pull | Push |
| Use | Decouple apps | Broadcast messages |
What is Elasticache? In-memory caching service for Redis or Memcached, improving performance by
reducing database load.
What  is  AWS  KMS?  Key  Management  Service  for  encryption/decryption  of  data  and  managing
encryption keys securely.
What  is  AWS  CloudFormation?  Infrastructure  as  Code  (IaC)  service  to  automate  creation  and
management of AWS resources using templates.
Difference  between  S3  Standard,  IA,  and  Glacier  |  Storage  Class  |  Use  Case  |  Cost  |
|---------------|----------|------| | Standard | Frequently accessed | High | | IA (Infrequent Access) |
Rarely accessed | Lower | | Glacier | Archival & backup | Very Low |
7. 
8. 
9. 
10. 
11. 
12. 
13. 
14. 
3

