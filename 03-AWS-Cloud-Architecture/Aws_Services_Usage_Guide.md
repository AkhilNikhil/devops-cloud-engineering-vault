# 📖 Aws Services Usage Guide
> *Converted from `Aws Services Usage Guide.pdf` for high-readability on GitHub.*

---
## Page 1

AWS Services Practical Guide
1. AWS EC2 (Elastic Compute Cloud)
Steps: 1. Login to AWS Console. 2. Services → Compute → EC2 → Launch Instance. 3. Choose AMI (Amazon
Linux  2,  Ubuntu,  etc).  4.  Select  Instance  Type  (t2.micro  for  free  tier).  5.  Configure  Instance  → default
settings. 6. Add Storage (default EBS). 7. Add Tags (optional). 8. Configure Security Group (SSH port 22 for
your IP). 9. Launch → Create or select key pair → Download .pem file. 10. Access Instance: 
ssh -i "your-key.pem" ec2-user@public-ip
2. AWS S3 (Simple Storage Service)
Steps: 1. Navigate: Services → Storage → S3 → Create Bucket. 2. Bucket Name → Unique. 3. Region →
Nearest. 4. Settings → Default (public access blocked). 5. Create Bucket. 6. Upload File → Open Bucket →
Upload → Add Files → Upload. 7. Access File → Generate pre-signed URL if needed.
3. AWS IAM (Identity and Access Management)
Steps: 1. Services → IAM → Users → Add User . 2. Enter Username → Access Type (Programmatic / Console).
3. Permissions → Attach Policies (AdministratorAccess). 4. Tags → Optional. 5. Review & Create User . 6.
Download credentials (Access Key, Secret Key).
4. AWS VPC (Virtual Private Cloud)
Steps:  1.  Services  → Networking  → VPC  → Your  VPCs  → Create  VPC.  2.  Name,  IPv4  CIDR  block  (e.g.,
10.0.0.0/16). 3. Create Subnet → Associate with VPC. 4. Configure Route Tables. 5. Attach Internet Gateway
for public access.
5. AWS Lambda
Steps: 1. Services → Compute → Lambda → Create Function. 2. Author from scratch → Name → Runtime
(Python, Node.js, Java). 3. Permissions → Default role. 4. Code → Inline or Upload zip. 5. Test → Add test
event → Invoke. 6. Add Trigger → S3, API Gateway, CloudWatch.
6. AWS RDS (Relational Database Service)
Steps: 1. Services → Database → RDS → Create Database. 2. Choose Engine (MySQL, PostgreSQL, etc). 3.
Template → Free tier . 4. DB Instance Settings → Name, Username, Password. 5. Connectivity → VPC, public
access, security groups. 6. Create DB → Wait for status Available. 7. Connect → Client software using
endpoint, username, password.
1

## Page 2

7. AWS CloudFront
Steps: 1. Services → Networking → CloudFront → Create Distribution. 2. Origin Settings → Choose S3
bucket or Web server . 3. Default Settings → Keep caching and security default. 4. Create Distribution → Wait
for Deployed. 5. Access URL → CloudFront domain.
8. AWS Route 53
Steps: 1. Services → Networking → Route 53 → Hosted Zones → Create Hosted Zone. 2. Enter Domain
Name (mywebsite.com). 3. Add Record Set → Type A → Value = EC2 public IP . 4. Update domain registrar →
Point name servers to Route 53 NS records.
9. AWS CloudWatch
Steps: 1. Services → Management & Governance → CloudWatch. 2. View Metrics → EC2, Lambda, S3. 3.
Create Alarm → Select metric → Threshold → Action (SNS notification).
10. AWS Elastic Beanstalk
Steps: 1. Services → Compute → Elastic Beanstalk → Create Application. 2. Name Application → Select
Platform (Java, Node.js). 3. Upload Code → Zip or WAR file. 4. Environment Settings → Default. 5. Launch →
Wait for environment ready. 6. Access URL → Provided by Beanstalk.
This guide provides practical steps for 10 core AWS services for hands-on usage.
2

