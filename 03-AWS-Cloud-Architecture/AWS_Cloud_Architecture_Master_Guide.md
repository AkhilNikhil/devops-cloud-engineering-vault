# ☁️ AWS Cloud Architecture: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers VPC Networking & CIDR Binary Math, IAM Least Privilege, Multi-Tier High Availability, Compute (EC2, Launch Templates vs AMIs), Storage (S3 Classes & Lifecycle, EBS gp3 vs Snapshots), Load Balancing (ALB vs NLB), Databases (RDS Multi-AZ vs DynamoDB), CloudWatch Observability, and Modern Cloud Security Standards (IMDSv2, VPC Endpoints).

---

## 📑 Table of Contents
- [1. Cloud Service & Deployment Models](#1-cloud-service--deployment-models)
- [2. Global Infrastructure: Regions, AZs, & Edge Locations](#2-global-infrastructure-regions-azs--edge-locations)
- [3. Complete VPC Networking & CIDR Subnetting Math](#3-complete-vpc-networking--cidr-subnetting-math)
- [4. VPC Core Components: Gateways & Routing](#4-vpc-core-components-gateways--routing)
- [5. Security Controls: Security Groups vs Network ACLs (NACLs)](#5-security-controls-security-groups-vs-network-acls-nacls)
- [6. EC2 Compute Architecture: AMIs vs Launch Templates](#6-ec2-compute-architecture-amis-vs-launch-templates)
- [7. The 4 EC2 Connection Methods](#7-the-4-ec2-connection-methods)
- [8. Elastic Block Store (EBS) Volumes vs Snapshots](#8-elastic-block-store-ebs-volumes-vs-snapshots)
- [9. S3 Object Storage: Classes, Lifecycle Rules, & Replication](#9-s3-object-storage-classes-lifecycle-rules--replication)
- [10. Identity & Access Management (IAM) Deep Dive](#10-identity--access-management-iam-deep-dive)
- [11. Elastic Load Balancing & Auto Scaling Groups (ASG)](#11-elastic-load-balancing--auto-scaling-groups-asg)
- [12. Managed Databases: RDS Multi-AZ vs Aurora vs DynamoDB](#12-managed-databases-rds-multi-az-vs-aurora-vs-dynamodb)
- [13. Modern Security & Observability (IMDSv2, CloudWatch)](#13-modern-security--observability-imdsv2-cloudwatch)
- [14. Senior DevOps Interview Q&A](#14-senior-devops-interview-qa)

---

## 1. Cloud Service & Deployment Models

### Cloud Deployment Models
* **Public Cloud**:
  * Multi-tenant computing infrastructure owned and operated by a third-party cloud provider (e.g., AWS, Azure, GCP).
  * Pay-as-you-go pricing, near-infinite scalability, provider manages physical hardware.
* **Private Cloud**:
  * Dedicated cloud infrastructure provisioned strictly for a single organization.
  * Provides maximum compliance and security isolation; higher capital expenditure and operational maintenance.
* **Hybrid Cloud**:
  * Integrates on-premises private infrastructure with public cloud environments via AWS Direct Connect or Site-to-Site VPN.
  * Enables **Cloud Bursting**: baseline workloads run on-premise, while temporary seasonal traffic spikes overflow dynamically into AWS.

### Cloud Service Models Comparison

```text
┌─────────────────────────────────┬───────────────────┬───────────────────┬───────────────────┐
│ Layer                           │ IaaS (e.g., EC2)  │ PaaS (Elastic BS) │ SaaS (Gmail/M365) │
├─────────────────────────────────┼───────────────────┼───────────────────┼───────────────────┤
│ Applications & Data             │ YOU Manage        │ YOU Manage        │ Provider Manages  │
│ Runtime & Middleware            │ YOU Manage        │ Provider Manages  │ Provider Manages  │
│ Operating System (OS)           │ YOU Manage        │ Provider Manages  │ Provider Manages  │
│ Virtualization & Hypervisor     │ Provider Manages  │ Provider Manages  │ Provider Manages  │
│ Servers, Storage, & Physical Net│ Provider Manages  │ Provider Manages  │ Provider Manages  │
└─────────────────────────────────┴───────────────────┴───────────────────┴───────────────────┘
```

---

## 2. Global Infrastructure: Regions, AZs, & Edge Locations

Understanding the physical topology of AWS is essential for high-availability architectural design.

### 1. AWS Region
* A separate geographic area (e.g., `us-east-1` in N. Virginia, `ap-south-1` in Mumbai).
* Each region is completely autonomous and isolated from other regions to prevent blast-radius cascading failures.
* Composed of a minimum of **3 Availability Zones** (up to 6 AZs in large regions).

### 2. Availability Zone (AZ)
* One or more distinct physical data centers housed in separate buildings located several miles apart.
* Engineered with redundant power grids, cooling infrastructure, and ultra-low-latency private fiber networking (< 2ms).
* Designed so that localized floods, power outages, or fires in one AZ do not impact neighboring AZs.

### 3. Edge Locations & CloudFront
* Physical points of presence (PoP) strategically placed in hundreds of major cities globally.
* Used by **Amazon CloudFront** (CDN) to cache static and streaming content close to end users, minimizing latency.
* Also houses **AWS WAF** (Web Application Firewall) and **AWS Shield** for edge DDoS mitigation.

---

## 3. Complete VPC Networking & CIDR Subnetting Math

A **VPC (Virtual Private Cloud)** is a logically isolated virtual network dedicated to your AWS account.

### IPv4 Fundamentals & Binary Structure
* An IPv4 address is a **32-bit binary number** divided into **4 octets** (8 bits each), separated by dots.
* Each octet ranges from 0 to 255: `[0-255].[0-255].[0-255].[0-255]`.
* Total IPv4 address space: $2^{32} = 4,294,967,296$ (approx. 4.3 billion addresses).

### The Historical IPv4 Classes
Before CIDR, IP routing followed rigid, wasteful classes:

| Class | IP Range | Default Mask | CIDR | Purpose | Networks | Hosts per Network |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Class A** | `0.0.0.0` - `126.255.255.255` | `255.0.0.0` | `/8` | Massive Enterprises | 126 | 16,777,214 |
| **Loopback**| `127.0.0.0` - `127.255.255.255`| `255.0.0.0` | `/8` | Localhost diagnostic | Reserved | N/A |
| **Class B** | `128.0.0.0` - `191.255.255.255`| `255.255.0.0` | `/16`| Medium/Large Orgs | 16,384 | 65,534 |
| **Class C** | `192.0.0.0` - `223.255.255.255`| `255.255.255.0` | `/24`| Small Local Networks | 2,097,152 | 254 |
| **Class D** | `224.0.0.0` - `239.255.255.255`| N/A | N/A | Multicast | Reserved | Reserved |
| **Class E** | `240.0.0.0` - `255.255.255.255`| N/A | N/A | Experimental | Reserved | Reserved |

### Classless Inter-Domain Routing (CIDR)
* Introduced to eliminate classful address waste by allowing variable-length subnet masks.
* Syntax: `IP_Address / Prefix_Length` (e.g., `10.0.0.0/16`).
* The **Prefix Length** indicates how many bits are fixed for the **Network ID**. The remaining bits ($32 - 	ext{Prefix}$) are available for **Host IDs**.

### The Subnetting Math Formula
* **Number of Subnets**: $2^n$ (where $n$ is the number of bits borrowed from the host portion).
* **Total IP Addresses**: $2^h$ (where $h = 32 - 	ext{prefix}$).
* **Standard Usable Hosts**: $2^h - 2$ (subtracting network ID and broadcast address).

### ⚠️ The AWS VPC 5 Reserved IPs Rule
Unlike traditional on-premise networking which reserves only 2 IPs per subnet, **AWS always reserves 5 IP addresses in every subnet**:
1. **`10.0.0.0`**: Network Address (identifies the subnet).
2. **`10.0.0.1`**: Reserved by AWS for the **VPC Local Router**.
3. **`10.0.0.2`**: Reserved by AWS for the **Amazon DNS Server (Route 53 Resolver)**.
4. **`10.0.0.3`**: Reserved by AWS for future use.
5. **`10.0.0.255`**: Network Broadcast Address (AWS VPC does not support broadcast, but reserves this address).
* **Formula for AWS Subnets**: $	ext{Usable Hosts} = 2^{(32 - 	ext{prefix})} - 5$.

### Master CIDR Subnetting Reference Table

| CIDR Prefix | Subnet Mask | Total IP Count | Usable Hosts in AWS | Common Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **`/16`** | `255.255.0.0` | 65,536 | **65,531** | Standard Production VPC Base Block |
| **`/20`** | `255.255.240.0` | 4,096 | **4,091** | Large Shared Cloud Environments |
| **`/21`** | `255.255.248.0` | 2,048 | **2,043** | Large Kubernetes Node Pools |
| **`/22`** | `255.255.252.0` | 1,024 | **1,019** | Standard Application Subnets |
| **`/23`** | `255.255.254.0` | 512 | **507** | Medium Compute Subnets |
| **`/24`** | `255.255.255.0` | 256 | **251** | Standard Public/Private Web Subnet |
| **`/25`** | `255.255.255.128` | 128 | **123** | Database Cluster Subnet |
| **`/26`** | `255.255.255.192` | 64 | **59** | Bastion / Jump Host Management Subnet |
| **`/27`** | `255.255.255.224` | 32 | **27** | Firewall / Gateway Endpoint Subnet |
| **`/28`** | `255.255.255.240` | 16 | **11** | Smallest allowable subnet in AWS VPC |

---

## 4. VPC Core Components: Gateways & Routing

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                          AWS VPC (10.0.0.0/16)                              │
│                                                                             │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                     Internet Gateway (IGW)                          │   │
│   └──────────────────────────────────┬──────────────────────────────────┘   │
│                                      │                                      │
│                                      ▼                                      │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │             PUBLIC SUBNET (10.0.1.0/24) - Route: 0.0.0.0/0 -> IGW  │   │
│   │                                                                     │   │
│   │  ┌───────────────────────┐             ┌─────────────────────────┐  │   │
│   │  │   Public ALB          │             │   NAT Gateway           │  │   │
│   │  │ (Elastic Load Balancer│             │   (with Elastic IP)     │  │   │
│   │  └───────────┬───────────┘             └────────────┬────────────┘  │   │
│   └──────────────┼──────────────────────────────────────┼───────────────┘   │
│                  │                                      │                   │
│                  ▼                                      ▼                   │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │           PRIVATE SUBNET (10.0.2.0/24) - Route: 0.0.0.0/0 -> NAT GW │   │
│   │                                                                     │   │
│   │  ┌───────────────────────────────────────────────────────────────┐  │   │
│   │  │   Backend Compute Instances (EC2 / EKS Pods)                  │  │   │
│   │  │   • Accepts traffic ONLY from Public ALB                      │  │   │
│   │  │   • Reaches internet outbound for updates strictly via NAT GW │  │   │
│   │  └───────────────────────────────┬───────────────────────────────┘  │   │
│   └──────────────────────────────────┼──────────────────────────────────┘   │
│                                      │                                      │
│                                      ▼                                      │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │       ISOLATED DATABASE SUBNET (10.0.3.0/24) - Route: Local Only    │   │
│   │                                                                     │   │
│   │  ┌───────────────────────────────────────────────────────────────┐  │   │
│   │  │   Amazon RDS PostgreSQL / Aurora Multi-AZ Cluster             │  │   │
│   │  │   • Zero internet routes (No IGW, No NAT Gateway)             │  │   │
│   │  └───────────────────────────────────────────────────────────────┘  │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 1. Internet Gateway (IGW)
* Horizontally scaled, highly available VPC component that enables two-way communication between instances in your VPC and the internet.
* Performs 1-to-1 NAT translation between instance private IPs and public IPv4 addresses.
* Exactly **one IGW** can be attached to a VPC.

### 2. NAT Gateway vs NAT Instance
* **NAT Gateway (Managed Production Standard)**:
  * Deployed inside a **Public Subnet** and assigned a dedicated Elastic IP (EIP).
  * Automatically scales bandwidth from 5 Gbps up to 100 Gbps.
  * Allows private instances to access the internet outbound (for OS updates, yum/apt packages, API calls) while **strictly blocking unsolicited inbound internet connections**.
  * Highly available within its AZ; for multi-AZ fault tolerance, deploy **one NAT Gateway per AZ**.
* **NAT Instance (Legacy / Cost-Saving)**:
  * Single EC2 instance running Linux `iptables` IP masquerading.
  * Must disable Source/Destination Check on the EC2 instance.
  * Represents a single point of failure; requires manual maintenance and patching.

### 3. Route Tables
* Determines where network traffic from your subnet is directed.
* **Public Subnet Route Table**: Contains route `0.0.0.0/0 -> igw-xxxx`.
* **Private Subnet Route Table**: Contains route `0.0.0.0/0 -> nat-xxxx`.
* **Database Subnet Route Table**: Contains only local route `10.0.0.0/16 -> local` (fully air-gapped).

---

## 5. Security Controls: Security Groups vs Network ACLs (NACLs)

Understanding the statefulness and operational layers of AWS firewalls is tested in every senior interview.

```text
Incoming Packet ──► [ NACL (Subnet Boundary) ] ──► [ Security Group (Instance Boundary) ] ──► EC2 ENI
```

### Point-by-Point Comparison

| Feature | Security Group (SG) | Network ACL (NACL) |
| :--- | :--- | :--- |
| **Operates At** | Virtual Network Interface (ENI / Instance Level) | Subnet Boundary Level |
| **Statefulness** | **Stateful**: Return traffic is automatically permitted regardless of outbound rules | **Stateless**: Return traffic must be explicitly allowed in outbound table |
| **Rules Evaluation** | Evaluates **ALL** rules before deciding; no rule priority numbers | Evaluates rules in strict numerical order (lowest number first: 100, 200, *) |
| **Default Inbound** | Denies all inbound traffic by default | Default NACL allows all inbound; custom NACL denies all |
| **Explicit Deny Rules**| ❌ **Cannot create Deny rules** (Allow rules only) | ✅ **Supports both Allow and Deny rules** (e.g., block malicious IP 1.2.3.4) |
| **Ephemeral Ports** | Handled automatically due to stateful connection tracking | Requires opening outbound ephemeral ports (`1024-65535`) |

---

## 6. EC2 Compute Architecture: AMIs vs Launch Templates

### AMI (Amazon Machine Image) vs Launch Template Comparison

| Attribute | Amazon Machine Image (AMI) | Launch Template (LT) |
| :--- | :--- | :--- |
| **What It Defines** | **Software Configuration**: Operating system, kernel, installed middleware, application code, data snapshot | **Hardware & Provisioning Spec**: Instance type, AMI ID, key pair, Security Groups, Subnets, EBS mappings, User Data |
| **Versioning** | Immutable snapshot; cannot be versioned (you create a new AMI ID) | **Full Native Versioning**: Supports `$Latest`, `$Default`, and specific numbered versions (v1, v2) |
| **Scope** | Regional; must be copied across regions | Regional; references regional AMIs and subnets |
| **Use in Auto Scaling**| Referenced inside a Launch Template | **Directly drives Auto Scaling Groups** (replaces deprecated Launch Configurations) |
| **Bootstrap Automation**| Static pre-installed packages | Dynamic runtime scripts executed at boot via **User Data** |

---

## 7. The 4 EC2 Connection Methods

| Method | Requirements | Security Profile | Primary Use Case |
| :--- | :--- | :--- | :--- |
| **1. AWS SSM Session Manager** | SSM Agent installed, IAM instance profile attached, outbound 443 | 🌟 **Highest Security**: Zero open ports (No port 22), no public IP, no SSH keys | **Production Enterprise Standard**; audit logs piped to CloudWatch/S3 |
| **2. SSH Client (`.pem`)** | Port 22 open to client IP, Public IP or Bastion, private `.pem` key | Medium: Dependent on private key protection and IP restriction | Developers and automation scripts |
| **3. EC2 Instance Connect** | Port 22 open, EC2 Instance Connect software, AWS IAM permissions | High: Pushes temporary one-time public key via AWS API for 60 seconds | Browser-based administrative terminal access |
| **4. EC2 Serial Console** | Nitro-based instance, root password or SSH key | Highest Privileged Access: Out-of-band console access | **Emergency Recovery**: Fix kernel panics, bad `/etc/fstab`, or misconfigured firewall |

---

## 8. Elastic Block Store (EBS) Volumes vs Snapshots

### Point-by-Point Comparison

| Feature | EBS Volume | EBS Snapshot |
| :--- | :--- | :--- |
| **Physical Nature** | Virtual block storage disk attached to an active EC2 instance | Point-in-time backup snapshot stored durably on Amazon S3 |
| **Availability Zone** | **Bound to a single AZ** (cannot attach directly across AZs) | **Regional**: Can restore an EBS volume into **any AZ** in that region |
| **Persistence** | Persists independently of instance lifecycle if DeleteOnTermination is false | Persists indefinitely until explicitly deleted |
| **Performance** | High IOPS and throughput (`gp3`, `io2 Block Express`) | Read-only cold backup; not directly mountable without restoration |
| **Multi-Attach** | Supported on `io1` / `io2` provisioned IOPS volumes (up to 16 instances) | N/A |

### EBS Volume Types Breakdown
* **`gp3` (General Purpose SSD - Default)**:
  * Baseline 3,000 IOPS and 125 MB/s throughput included free regardless of volume size.
  * 20% cheaper than legacy `gp2`; can scale IOPS and throughput independently of storage capacity.
* **`io2` / `io2 Block Express` (Provisioned IOPS SSD)**:
  * Mission-critical databases requiring sub-millisecond latency and up to 256,000 IOPS.
* **`st1` (Throughput Optimized HDD)**:
  * Big data, data warehousing, and log processing requiring continuous sequential throughput.
* **`sc1` (Cold HDD)**:
  * Infrequently accessed large sequential storage; lowest cost block storage.

---

## 9. S3 Object Storage: Classes, Lifecycle Rules, & Replication

Amazon S3 is a serverless, highly durable (99.999999999% - 11 9's durability) object storage service.

### S3 Storage Classes

| Storage Class | Durability | Availability | Retrieval Fee? | Ideal Workload |
| :--- | :--- | :--- | :--- | :--- |
| **S3 Standard** | 11 9's | 99.99% | None | Frequently accessed data, active web assets |
| **S3 Intelligent-Tiering** | 11 9's | 99.9% | None (Small monitoring fee) | Unknown or changing access patterns (auto-moves tiers) |
| **S3 Standard-IA** | 11 9's | 99.9% | Yes (per GB) | Backups, disaster recovery, long-term storage |
| **S3 One Zone-IA** | 11 9's (Single AZ) | 99.5% | Yes (per GB) | Secondary backups that can be recreated if AZ is destroyed |
| **S3 Glacier Flexible** | 11 9's | 99.99% | Yes | Archive data retrievable in 1-5 minutes to 3-5 hours |
| **S3 Glacier Deep Archive** | 11 9's | 99.99% | Yes (Lowest cost) | Regulatory compliance data retrievable in 12 hours |

### Lifecycle Rules vs Cross-Region Replication (CRR)
* **S3 Lifecycle Rules**:
  * Automates cost reduction: Transition objects from Standard $	o$ Standard-IA after 30 days $	o$ Glacier after 90 days $	o$ Permanent expiration/deletion after 365 days.
* **Cross-Region Replication (CRR)**:
  * Automatically replicates newly uploaded objects across buckets in different AWS regions for compliance and low-latency global reads. Requires S3 Versioning enabled on both source and destination buckets.

---

## 10. Identity & Access Management (IAM) Deep Dive

### Core Security Rules
* **Principle of Least Privilege (PoLP)**: Grant only the bare minimum actions, resources, and condition keys required.
* **Explicit Deny Overrides All**: `Explicit Deny > Explicit Allow > Default (Implicit) Deny`.
* **IAM Roles Over Long-Lived Access Keys**: EC2 instances and CI/CD runners must use temporary STS credentials via IAM Roles.

### Production IAM Role Policy Blueprint
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowS3ReadWriteOnAppBucket",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::enterprise-taskflow-vault",
        "arn:aws:s3:::enterprise-taskflow-vault/*"
      ],
      "Condition": {
        "Bool": {
          "aws:SecureTransport": "true"
        }
      }
    }
  ]
}
```

---

## 11. Elastic Load Balancing & Auto Scaling Groups (ASG)

### ALB vs NLB Comparison

| Feature | Application Load Balancer (ALB) | Network Load Balancer (NLB) |
| :--- | :--- | :--- |
| **OSI Layer** | **Layer 7 (Application)**: HTTP, HTTPS, gRPC, WebSockets | **Layer 4 (Transport)**: TCP, UDP, TLS |
| **Routing Decisions**| Content-based: Host header, URL path (`/api`), query params, HTTP headers | Port and IP protocol level routing |
| **Static IP Support**| ❌ No static IP (uses dynamic DNS names) | ✅ **Allocates static Elastic IPs per AZ** |
| **Latency & Scale** | Milliseconds; handles complex URL rewriting | **Ultra-low sub-millisecond latency**; millions of requests/sec |
| **Target Types** | EC2 instances, Lambda functions, IP addresses, EKS Pods | EC2 instances, IP addresses, Application Load Balancers |

### Auto Scaling Group Scaling Policies
* **Target Tracking Scaling**: Maintains a specific metric target (e.g., keep average ASG CPU at 65%).
* **Step Scaling**: Increases instance count in steps based on CloudWatch alarm breach magnitude.
* **Scheduled Scaling**: Scales based on predictable calendar events (e.g., scale up at 9 AM on Monday).

---

## 12. Managed Databases: RDS Multi-AZ vs Aurora vs DynamoDB

| Capability | Amazon RDS Multi-AZ | Amazon Aurora | Amazon DynamoDB |
| :--- | :--- | :--- | :--- |
| **Database Type** | Relational (PostgreSQL, MySQL) | Cloud-Native Relational | NoSQL (Key-Value & Document) |
| **High Availability**| Synchronous replication to Standby instance in 2nd AZ (Active-Passive) | 6 copies of data replicated across 3 AZs; storage auto-scales up to 128 TiB | Multi-AZ distributed hash partition; global active-active tables |
| **Failover Time** | 60 - 120 seconds | **< 30 seconds** (Promotes read replica) | Instantaneous partition routing |
| **Scaling** | Vertical compute scaling; read replicas for read offloading | Auto-scales compute up to 15 read replicas; Aurora Serverless v2 | Near-infinite horizontal partition scaling with On-Demand capacity |

---

## 13. Modern Security & Observability (IMDSv2, CloudWatch)

### 1. Instance Metadata Service v2 (IMDSv2)
* Protects EC2 instances against SSRF (Server-Side Request Forgery) vulnerabilities.
* Requires a session token via an initial `PUT` request with a hop-limit header before reading IAM credentials:
  ```bash
  # Step 1: Fetch session token
  TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")

  # Step 2: Use token to retrieve metadata
  curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/iam/security-credentials/
  ```

### 2. CloudWatch Alarms & Observability
* Monitors metrics (CPUUtilization, DiskReadOps, NetworkIn).
* Triggers automated SNS email alerts, Auto Scaling events, or EC2 instance auto-recovery actions.

---

## 14. Senior DevOps Interview Q&A

### Q1: How do you design a secure, highly-available 3-tier web architecture on AWS?
* **Web Tier**: Public Subnets across 2 AZs housing an Application Load Balancer (ALB) with AWS WAF attached.
* **Application Tier**: Private Subnets across 2 AZs housing an Auto Scaling Group of stateless backend compute instances.
* **Database Tier**: Isolated Database Subnets across 2 AZs housing an Amazon RDS Multi-AZ cluster (Primary in AZ-a, Standby in AZ-b).
* **Security Controls**:
  * Web ALB SG accepts 80/443 from `0.0.0.0/0`.
  * App SG accepts traffic on port 8080 **only from Web ALB SG ID**.
  * DB SG accepts traffic on port 5432 **only from App SG ID**.

### Q2: Why is a NAT Gateway placed in a public subnet instead of a private subnet?
* A NAT Gateway requires a Public IP (Elastic IP) and a direct route to an Internet Gateway (`0.0.0.0/0 -> igw`) to translate private IP packets to its public IP and route them to the external internet.
* If placed in a private subnet, the NAT Gateway itself would have no outbound route to reach the Internet Gateway!

### Q3: What is the difference between AWS Security Group statefulness and NACL statelessness?
* **Security Group (Stateful)**: When inbound traffic is permitted on port 443, return outbound traffic is automatically permitted on the ephemeral port, regardless of outbound rules.
* **NACL (Stateless)**: If inbound traffic is allowed on port 443, return outbound traffic must be explicitly permitted in the outbound rules table on ephemeral ports (`1024-65535`).
