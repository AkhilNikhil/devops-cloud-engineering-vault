# ☁️ AWS Cloud Architecture: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers VPC Networking, IAM Least Privilege, Multi-Tier High Availability, Compute (EC2, Auto Scaling), Load Balancing (ALB vs NLB), Storage (S3, EBS gp3, EFS), Databases (RDS Multi-AZ vs DynamoDB), CloudWatch Observability, and Modern Cloud Security Standards (IMDSv2, VPC Endpoints).

---

## 📑 Table of Contents
- [1. Identity & Access Management (IAM) Deep Dive](#1-identity--access-management-iam-deep-dive)
- [2. Global Infrastructure: Regions vs Availability Zones](#2-global-infrastructure-regions-vs-availability-zones)
- [3. VPC Networking Architecture](#3-vpc-networking-architecture)
- [4. Security Groups vs Network ACLs (NACLs)](#4-security-groups-vs-network-acls-nacls)
- [5. Compute & Auto Scaling Groups (ASG)](#5-compute--auto-scaling-groups-asg)
- [6. Elastic Load Balancing: ALB vs NLB](#6-elastic-load-balancing-alb-vs-nlb)
- [7. Cloud Storage Systems: S3 vs EBS vs EFS](#7-cloud-storage-systems-s3-vs-ebs-vs-efs)
- [8. Managed Databases: RDS vs DynamoDB](#8-managed-databases-rds-vs-dynamodb)
- [9. Observability: CloudWatch & Alarms](#9-observability-cloudwatch--alarms)
- [10. Modern AWS Architecture Standards](#10-modern-aws-architecture-standards)
- [11. Senior DevOps Interview Q&A](#11-senior-devops-interview-qa)

---

## 1. Identity & Access Management (IAM) Deep Dive

### Core Principles
* **Principle of Least Privilege (PoLP)**: Grant only the minimum permissions necessary for an identity to perform its designated duties.
* **Never Use Root Account**: Lock root credentials behind hardware MFA; manage daily infrastructure using IAM Identity Center (SSO) or temporary federated roles.
* **Explicit Deny Precedence**: In AWS policy evaluation: `Explicit Deny > Explicit Allow > Default Deny (Implicit)`.

### IAM Entities Comparison

| Entity | Long-Term Credentials? | Primary Use Case | Security Best Practice |
| :--- | :--- | :--- | :--- |
| **IAM User** | Yes (Access Key + Secret Key) | Human developers (Legacy) | Deprecated in modern AWS; replace with IAM Identity Center SSO |
| **IAM Group** | N/A (Collection of Users) | Batch permission attachment | Attach policies to groups, not individual users |
| **IAM Role** | **No** (Temporary STS tokens) | EC2 instances, Lambda, GitHub Actions, EKS Pods | **Golden Standard**: Eliminates hardcoded long-lived credentials |

### Production IAM Role Policy Example (EC2 S3 Access)
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowAppBucketReadWrite",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::enterprise-app-storage-vault",
        "arn:aws:s3:::enterprise-app-storage-vault/*"
      ]
    }
  ]
}
```

---

## 2. Global Infrastructure: Regions vs Availability Zones

### Infrastructure Hierarchy
* **AWS Region**:
  * Physical geographic location across the globe (e.g., `us-east-1` N. Virginia, `ap-south-1` Mumbai).
  * Consists of multiple, isolated, and physically separated Availability Zones.
  * Designed for compliance, data sovereignty, and global user latency reduction.
* **Availability Zone (AZ)**:
  * One or more discrete data centers with redundant power, networking, and connectivity.
  * Separated by meaningful physical distance (miles) to safeguard against localized natural disasters.
  * Interconnected via ultra-low latency, high-throughput private fiber networks.
* **Edge Locations**:
  * Hundreds of global points of presence (PoPs) running AWS CloudFront CDN and Route53 DNS for caching content closest to end users.

### High Availability (HA) Rule
* Always architect production workloads across **at least two Availability Zones** (Multi-AZ) behind a Load Balancer to guarantee 99.99% uptime.

---

## 3. VPC Networking Architecture

### VPC Component Breakdown
```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       Virtual Private Cloud (10.0.0.0/16)                   │
│                                                                             │
│   ┌──────────────────────────────┐     ┌────────────────────────────────┐   │
│   │ Public Subnet (10.0.1.0/24)  │     │ Private Subnet (10.0.2.0/24)   │   │
│   │                              │     │                                │   │
│   │  ┌────────────────────────┐  │     │  ┌──────────────────────────┐  │   │
│   │  │ Application Load Balancer│ │     │  │ Backend App / RDS Cluster│  │   │
│   │  │ NAT Gateway (Elastic IP)│ │     │  │ No Direct Public IP     │  │   │
│   │  └────────────────────────┘  │     │  └─────────────┬────────────┘  │   │
│   └──────────────┬───────────────┘     └────────────────┼───────────────┘   │
│                  │                                      │                   │
│                  ▼                                      ▼                   │
│   ┌──────────────────────────────┐     ┌────────────────────────────────┐   │
│   │ Internet Gateway (IGW)       │     │ Outbound via NAT Gateway       │   │
│   │ (Direct Route: 0.0.0.0/0)    │     │ (Private Route: 0.0.0.0/0->NAT)│   │
│   └──────────────┬───────────────┘     └────────────────────────────────┘   │
└──────────────────┼──────────────────────────────────────────────────────────┘
                   ▼
              Internet
```

### Core Subnet & Gateway Rules
* **Public Subnet**:
  * Route table has a direct route (`0.0.0.0/0`) pointing to an **Internet Gateway (IGW)**.
  * Instances inside receive Public IPv4 addresses.
  * Houses ALBs, Bastion jump hosts, and NAT Gateways.
* **Private Subnet**:
  * Route table routes outbound internet traffic (`0.0.0.0/0`) through a **NAT Gateway** residing in the public subnet.
  * Instances have **zero public IP addresses**; completely shielded from inbound internet traffic.
  * Houses backend APIs, microservices, databases, and message brokers.

---

## 4. Security Groups vs Network ACLs (NACLs)

### Comparison Matrix

| Feature | Security Group (SG) | Network ACL (NACL) |
| :--- | :--- | :--- |
| **Layer of Operation** | Instance level (Virtual NIC / ENI) | Subnet level (Subnet boundary) |
| **State Tracking** | **Stateful** (Return traffic automatically allowed) | **Stateless** (Return traffic must be explicitly allowed) |
| **Rule Types** | **ALLOW rules only** (Implicit deny all) | **ALLOW and DENY rules** |
| **Rule Evaluation** | All rules evaluated simultaneously | Evaluated in sequential numerical rule order |
| **Ephemerality** | Return traffic on ephemeral ports is automatic | Requires opening ephemeral ports (`1024-65535`) |

---

## 5. Compute & Auto Scaling Groups (ASG)

### Auto Scaling Group Components
* **1. Launch Template**:
  * Defines AMI ID, instance type, key pair, Security Groups, IAM role profile, and User Data bootstrap scripts.
* **2. Auto Scaling Group (ASG)**:
  * Manages fleet sizing: `Min Capacity`, `Desired Capacity`, `Max Capacity`.
  * Automatically distributes EC2 instances across multiple configured Availability Zones.
  * Integrates with ALB Target Groups to add healthy instances and drain terminating instances.
* **3. Scaling Policies**:
  * **Target Tracking Scaling**: Maintains average metric (e.g., *"Keep ASG average CPU at 60%"*).
  * **Step Scaling**: Increases instance count in steps based on CloudWatch Alarm breach thresholds.
  * **Scheduled Scaling**: Anticipates traffic surges (e.g., Black Friday sales).

---

## 6. Elastic Load Balancing: ALB vs NLB

### Comparison Matrix

| Capability | Application Load Balancer (ALB) | Network Load Balancer (NLB) |
| :--- | :--- | :--- |
| **OSI Layer** | **Layer 7** (Application: HTTP / HTTPS / gRPC) | **Layer 4** (Transport: TCP / UDP / TLS) |
| **Performance** | Millions of requests/sec with SSL termination | Ultra-high performance, tens of millions req/sec |
| **Latency** | Single-digit to low double-digit ms | Ultra-low sub-millisecond latency |
| **Static IP Support**| Dynamic DNS endpoint (IPs change dynamically) | **Static Anycast IP** per AZ (Elastic IP assigned) |
| **Routing Features** | Path-based (`/api`), host-based, query params | Pure IP and Port forwarding |
| **WebSocket** | Native support | Native support |

---

## 7. Cloud Storage Systems: S3 vs EBS vs EFS

### Comparison Matrix

| Attribute | Amazon S3 | Amazon EBS (gp3) | Amazon EFS |
| :--- | :--- | :--- | :--- |
| **Storage Paradigm** | **Object Storage** (Key-Value) | **Block Storage** (Virtual Disk) | **File Storage** (NFS v4) |
| **Access Protocol** | HTTP / HTTPS REST API | Block-level SCSI attachment | POSIX Network File System |
| **Max Scale** | Virtually unlimited | Up to 64TB per volume | Petabytes, grows dynamically |
| **Multi-Attach** | Web-accessible by millions | Attached to **one EC2** in single AZ | Concurrent mount by **thousands of EC2s** |
| **Use Cases** | Backups, static assets, media | Root OS drives, low-latency DBs | Shared web assets, CMS, Kubernetes RWX |

---

## 8. Managed Databases: RDS vs DynamoDB

### Comparison Matrix

| Feature | Amazon RDS (PostgreSQL/MySQL) | Amazon DynamoDB |
| :--- | :--- | :--- |
| **Model** | Relational Database (RDBMS - SQL) | NoSQL Key-Value & Document |
| **Schema** | Rigid, predefined table schema | Flexible, schemaless items |
| **High Availability** | Multi-AZ synchronous replication (Active-Standby)| Built-in multi-AZ replication across 3 AZs |
| **Scaling** | Vertical (scale instance compute); Read Replicas | Horizontal auto-scaling (on-demand or provisioned) |
| **Performance** | Milliseconds | Consistent single-digit milliseconds at any scale |
| **Joins & Transactions**| Full ACID joins, foreign keys, complex queries | No joins; atomic single-table transactions |

---

## 9. Observability: CloudWatch & Alarms

### CloudWatch Core Pillars
* **1. CloudWatch Metrics**:
  * Ingests numerical performance telemetry from AWS services (CPU, Network In/Out, Disk Read/Write).
  * Standard interval: 5 minutes; Detailed monitoring: 1 minute.
* **2. CloudWatch Alarms**:
  * Monitors metric thresholds over time (e.g., `CPUUtilization > 80% for 2 consecutive periods of 5m`).
  * Triggers notifications (SNS -> Email / Slack / PagerDuty) or auto-remediation (ASG Scaling Policy).
* **3. CloudWatch Logs**:
  * Collects and centralizes system logs, container stdout, and application exceptions via CloudWatch Logs Agent.
  * Features Log Insights for querying logs using SQL-like filtering syntax.

---

## 10. Modern AWS Architecture Standards

### 1. Mandatory IMDSv2 Token Security
* Always enforce **Instance Metadata Service Version 2 (IMDSv2)** to mitigate SSRF (Server-Side Request Forgery) attacks:
```bash
aws ec2 modify-instance-metadata-options   --instance-id i-0123456789abcdef0   --http-tokens required   --http-endpoint enabled
```

### 2. EBS gp3 Volume Standard
* Always provision `gp3` volumes instead of legacy `gp2`. Delivers baseline 3,000 IOPS and 125 MB/s throughput independently of volume size at **20% lower cost**.

### 3. Free S3 Gateway VPC Endpoint
* Always attach an S3 Gateway Endpoint to your VPC route tables. Enables private, high-speed traffic directly from private subnets to AWS S3 without passing through expensive NAT Gateways!

---

## 11. Senior DevOps Interview Q&A

### Q1: How do you design a secure, highly-available 3-tier web architecture on AWS?
* **Web Tier**: Public Subnets across 2 AZs housing an Application Load Balancer (ALB) with AWS WAF attached.
* **Application Tier**: Private Subnets across 2 AZs housing an Auto Scaling Group of stateless backend compute instances.
* **Database Tier**: Isolated Database Subnets across 2 AZs housing an Amazon RDS Multi-AZ cluster (Primary in AZ-a, Standby in AZ-b).
* **Security Controls**:
  * Web ALB SG accepts 80/443 from `0.0.0.0/0`.
  * App SG accepts traffic on port 8080 **only from Web ALB SG**.
  * DB SG accepts traffic on port 5432 **only from App SG**.

### Q2: Why is a NAT Gateway placed in a public subnet instead of a private subnet?
* A NAT Gateway needs a Public IP (Elastic IP) and a direct route to an Internet Gateway (`0.0.0.0/0 -> igw`) so it can translate private IP packets to its own public IP and route them to the external internet.
* If placed in a private subnet, the NAT Gateway itself would have no path to reach the internet!

### Q3: What is the difference between AWS Security Group statefulness and NACL statelessness?
* **Security Group (Stateful)**: When inbound traffic is permitted on port 443, return outbound traffic is automatically permitted on the ephemeral port, regardless of outbound rules.
* **NACL (Stateless)**: If inbound traffic is allowed on port 443, return outbound traffic must be explicitly permitted in the outbound rules table on ephemeral ports (`1024-65535`).
