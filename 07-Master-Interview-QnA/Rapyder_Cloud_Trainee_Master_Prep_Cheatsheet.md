# ⚡ Rapyder Cloud Trainee: The Definitive Master Interview & Systems Cheatsheet

> **Candidate:** Akhil B M | Cloud & DevOps Engineer | Bengaluru, Karnataka  
> **Target Role:** Cloud Trainee (L1 Cloud Support / Managed Services)  
> **Company:** Rapyder Cloud Solutions (AWS Premier Tier Services Partner)  
> **Master Guide Scope:**  
> 1. All Interview Questions & Speakable Scenarios (Rapyder Technical, 17 Printed Questions, Handwritten Notes, and Part 7 Questions)  
> 2. Ultra-Simple "Whiteboard & Typing" Manifests (Jenkins, Docker, Compose, Pods, Services, ReplicaSets, RC, Deployments, DaemonSets, Secrets, PV/PVC, Terraform)  
> 3. Technology Cheat Sheets (AWS, Azure, Linux, Git, Jenkins, Docker, Kubernetes, Terraform)  
> 4. Real-Time Projects Deep Dive (TaskFlow V4.9.2 & Azure DevOps CI/CD Suite from Resume)

---

## 📑 Master Table of Contents
- [PART 1: Complete Rapyder Technical Interview Q&A](#part-1-complete-rapyder-technical-interview-qa)
  - [1.1 Rapyder Specific Cloud Questions](#11-rapyder-specific-cloud-questions)
  - [1.2 The 17 Printed Technical Questions](#12-the-17-printed-technical-questions)
  - [1.3 The Handwritten Round 2 & Round 3 Questions](#13-the-handwritten-round-2--round-3-questions)
  - [1.4 Part 7 AWS Core & FinOps](#14-part-7-aws-core--finops)
  - [1.5 Part 7 Real-World Incident Troubleshooting Scenarios](#15-part-7-real-world-incident-troubleshooting-scenarios)
  - [1.6 Part 7 Linux & Networking Fundamentals](#16-part-7-linux--networking-fundamentals)
  - [1.7 Part 7 Azure & GCP Multi-Cloud](#17-part-7-azure--gcp-multi-cloud)
  - [1.8 Part 7 Containers, Kubernetes & DevOps Tools](#18-part-7-containers-kubernetes--devops-tools)
  - [1.9 Part 7 ITSM, SLA Governance & Behavioral Excellence](#19-part-7-itsm-sla-governance--behavioral-excellence)
- [PART 2: Ultra-Simple "Whiteboard" Manifests & Scripts](#part-2-ultra-simple-whiteboard-manifests--scripts)
  - [2.1 Minimal Single-Stage Dockerfile (Nginx)](#21-minimal-single-stage-dockerfile-nginx)
  - [2.2 Minimal Multi-Stage Dockerfile (Node.js)](#22-minimal-multi-stage-dockerfile-nodejs)
  - [2.3 Minimal Docker Compose (`compose.yaml`)](#23-minimal-docker-compose-composeyaml)
  - [2.4 Minimal Jenkins Declarative Pipeline (`Jenkinsfile`)](#24-minimal-jenkins-declarative-pipeline-jenkinsfile)
  - [2.5 Minimal GitHub Actions Pipeline (`ci.yml`)](#25-minimal-github-actions-pipeline-ciyml)
  - [2.6 Minimal Kubernetes Pod (`pod.yaml`)](#26-minimal-kubernetes-pod-podyaml)
  - [2.7 Minimal Kubernetes Service (`service.yaml`)](#27-minimal-kubernetes-service-serviceyaml)
  - [2.8 Minimal Kubernetes ReplicaSet (`replicaset.yaml`)](#28-minimal-kubernetes-replicaset-replicasetyaml)
  - [2.9 Minimal Kubernetes ReplicationController (`rc.yaml`)](#29-minimal-kubernetes-replicationcontroller-rcyaml)
  - [2.10 Minimal Kubernetes Deployment (`deployment.yaml`)](#210-minimal-kubernetes-deployment-deploymentyaml)
  - [2.11 Minimal Kubernetes DaemonSet (`daemonset.yaml`)](#211-minimal-kubernetes-daemonset-daemonsetyaml)
  - [2.12 Minimal Kubernetes Secret (`secret.yaml`)](#212-minimal-kubernetes-secret-secretyaml)
  - [2.13 Minimal Kubernetes PV & PVC](#213-minimal-kubernetes-pv--pvc)
  - [2.14 Minimal Terraform Script (AWS EC2)](#214-minimal-terraform-script-aws-ec2)
- [PART 3: Quick-Revision Technology Cheatsheets](#part-3-quick-revision-technology-cheatsheets)
  - [3.1 AWS Cloud Core Cheat Sheet](#31-aws-cloud-core-cheat-sheet)
  - [3.2 Microsoft Azure & Multi-Cloud Cheat Sheet](#32-microsoft-azure--multi-cloud-cheat-sheet)
  - [3.3 Linux Systems Administration Cheat Sheet](#33-linux-systems-administration-cheat-sheet)
  - [3.4 Git Version Control & Reflog Cheat Sheet](#34-git-version-control--reflog-cheat-sheet)
  - [3.5 Jenkins & CI/CD Automation Cheat Sheet](#35-jenkins--cicd-automation-cheat-sheet)
  - [3.6 Docker Container Engineering Cheat Sheet](#36-docker-container-engineering-cheat-sheet)
  - [3.7 Kubernetes Orchestration Cheat Sheet](#37-kubernetes-orchestration-cheat-sheet)
  - [3.8 Terraform Infrastructure as Code Cheat Sheet](#38-terraform-infrastructure-as-code-cheat-sheet)
- [PART 4: Real-Time Projects Deep Dive (From Your Resume)](#part-4-real-time-projects-deep-dive-from-your-resume)
  - [4.1 TaskFlow V4.9.2 Cloud Platform (AWS / Docker / Supabase)](#41-taskflow-v492-cloud-platform-aws--docker--supabase)
  - [4.2 Azure DevOps CI/CD Automation Suite](#42-azure-devops-cicd-automation-suite)

---

# PART 1: Complete Rapyder Technical Interview Q&A

## 1.1 Rapyder Specific Cloud Questions

### Q1: What is the Import/Export method in Azure?
* **Speakable Answer**: Azure Import/Export service allows you to securely transfer petabytes of data into Azure Blob Storage or Azure Files by shipping physical SATA hard disk drives directly to a Microsoft datacenter. It is used when internet bandwidth is limited and network uploads would take weeks. For automated modern appliances, Azure Data Box is used, while `AzCopy` handles high-speed network-based transfers.
* **Project Example**: In our database archiving drill, we evaluated Azure Data Box and AzCopy scripts with SAS tokens to migrate 2TB of cold logs into an Azure Cool Blob container.

### Q2: How do you access files in Azure from AWS?
* **Speakable Answer**: The standard method is generating a time-limited Shared Access Signature (SAS) token on the Azure Blob container and pulling files from an AWS EC2 instance or Lambda function using `AzCopy`, `rclone`, or the Azure Storage SDK over HTTPS. For managed continuous synchronization without custom scripts, AWS DataSync can directly ingest data from Azure Blob Storage into Amazon S3. For private connections, a Site-to-Site VPN is configured between AWS and Azure.
* **Project Example**: In our project, an analytics worker running on an AWS EC2 instance ingested nightly invoice PDFs from an Azure Blob container via an automated cron script with `rclone` and a SAS URI.

### Q3: How do you connect local files to AWS Cloud without an internet connection?
* **Speakable Answer**: When zero internet connection is available, we use the **AWS Snow Family** (AWS Snowcone up to 8TB or AWS Snowball Edge up to 80TB). AWS ships an encrypted hardware appliance; you connect it to your local network, copy data using AWS OpsHub, and ship it back to AWS, where engineers import it directly into your S3 bucket. For dedicated private live connectivity without using public internet, **AWS Direct Connect** provides a dedicated physical fiber link.
* **Project Example**: For offline compliance archiving, we designed a Snowball migration procedure with AES-256 encryption and checksum validation for offline ingest into Amazon S3.

### Q4: What is AWS Lambda?
* **Speakable Answer**: AWS Lambda is a serverless, event-driven compute service that executes code without provisioning or managing servers. It automatically scales from zero to thousands of concurrent executions in response to events like S3 uploads, DynamoDB streams, API Gateway requests, or CloudWatch cron schedules. You pay strictly for execution time measured in milliseconds.
* **Project Example**: In our application, whenever a user uploaded a profile image to an S3 bucket, a Python Lambda function automatically resized the image and generated a thumbnail.

### Q5: What is GCP (Google Cloud Platform)?
* **Speakable Answer**: Google Cloud Platform is Google's public cloud computing suite built on the same global infrastructure that powers Google Search and YouTube. It provides compute via Compute Engine and GKE, storage via Cloud Storage, and leading data/AI services like BigQuery and Vertex AI. GCP is known for its native Kubernetes integration and global VPC networking.
* **Project Example**: In our multi-cloud labs, we compared AWS S3 and GCP Cloud Storage lifecycle rules, managing both using unified Terraform modules.

### Q6: How do you design a web page that is NOT publicly accessible?
* **Speakable Answer**: Deploy the web application on an EC2 instance in a **Private Subnet** with no public IP, placed behind an **Internal Application Load Balancer**. Users access it securely through an AWS Client VPN, Site-to-Site VPN, or AWS Systems Manager (SSM) Session Manager. For a static site, host it in a private S3 bucket with 'Block Public Access' enabled, accessible only via a VPC Gateway Endpoint with a restrictive bucket policy.
* **Project Example**: For our internal admin dashboard, we hosted the frontend in an S3 bucket restricted exclusively to our VPC ID via an S3 VPC Endpoint policy.

### Q7: Explain Amazon S3.
* **Speakable Answer**: Amazon S3 is an object storage service offering 99.999999999% (11 9's) durability. Data is stored in buckets with support for versioning, lifecycle rules, KMS encryption, and static website hosting. Storage classes include S3 Standard, Intelligent-Tiering, Standard-IA, and Glacier. Access is controlled by IAM policies, bucket policies, and Block Public Access.
* **Project Example**: In TaskFlow, we stored user uploads and database backups in S3, using lifecycle rules to transition `.sql.gz` backups older than 30 days to Glacier.

### Q8: What is Azure Blob Storage?
* **Speakable Answer**: Azure Blob Storage is Microsoft's object storage service for massive amounts of unstructured data like files, backups, and logs. It organizes data into Storage Accounts, Containers, and Blobs. It offers Hot, Cool, Cold, and Archive tiers, secured by Entra ID, Access Keys, and SAS tokens.
* **Project Example**: In our Azure lab, we stored application debug logs in a Cool tier blob container with automatic deletion after 90 days.

---

## 1.2 The 17 Printed Technical Questions

### Q1: What is DevOps? What is the use of DevOps in the application lifecycle?
* **Speakable Answer**: DevOps is a cultural philosophy and set of automated practices combining software development (Dev) and IT operations (Ops). It eliminates operational silos and replaces manual server handoffs with automated CI/CD pipelines across the 8 lifecycle stages: Plan, Code, Build, Test, Release, Deploy, Operate, and Monitor.
* **Project Example**: Implementing automated Jenkins CI/CD in our project reduced release deployment times from 45 minutes of manual SSH commands down to 3 minutes.

### Q2: What is Git and what problem does it solve?
* **Speakable Answer**: Git is an open-source distributed version control system that tracks file changes and enables multi-developer collaboration through branching and merging. It prevents code overwrites and lost work by recording an immutable cryptographic commit ledger, allowing instant rollbacks to any stable release.
* **Project Example**: When two teammates modified our database configuration simultaneously, Git detected the merge conflict, allowing us to safely resolve conflicting lines.

### Q3: Difference between physical and virtual systems?
* **Speakable Answer**: A physical system is bare-metal hardware dedicated to one OS with no virtualization layer. A virtual system is a virtual machine (VM) created by a hypervisor running on shared hardware. VMs provide rapid provisioning, snapshot backups, and high density, while physical systems provide raw maximum hardware performance.
* **Project Example**: Migrating our workload to AWS EC2 virtual instances allowed us to dynamically resize instance types from t3.micro to t3.medium in 2 minutes without purchasing physical hardware.

### Q4: Difference between Linux and Windows OS?
* **Speakable Answer**: Linux is open-source, lightweight, CLI-driven, and powers over 90% of cloud servers and containers with a unified root filesystem (`/`). Windows is a commercial, GUI-focused OS common in desktops and Active Directory environments using drive letters (`C:\`, `D:\`).
* **Project Example**: We chose Ubuntu 22.04 LTS for our cloud servers because its headless baseline consumes less than 400MB RAM, leaving maximum capacity for application workloads.

### Q5: Ten mostly used Linux commands.
1. `ls -la`: Lists all files with permissions, sizes, and hidden items.
2. `cd` / `pwd`: Change and print working directory.
3. `systemctl status <service>`: Inspects and manages system services (Nginx, Docker).
4. `df -h`: Shows disk space utilization per filesystem in human-readable format.
5. `top` / `htop`: Real-time interactive CPU and memory process table.
6. `tail -f <file>`: Live-streams appended log entries.
7. `grep -rnI "ERROR" /var/log`: Searches recursively for text patterns with line numbers.
8. `chmod 755` / `chown user:group`: Modifies file permissions and ownership.
9. `ps aux | grep <process>`: Finds active processes and their PIDs.
10. `ss -tulpn`: Displays listening TCP/UDP ports and associated programs.

### Q6: Sample Dockerfile for deploying Nginx.
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### Q7: Docker network types. Which is default?
* **Speakable Answer**: Docker provides Bridge, Host, None, Overlay, and Macvlan. The **default is Bridge (`docker0`)**. Custom user-defined bridges are preferred in production because they provide automatic internal DNS service discovery by container name.
* **Project Example**: In TaskFlow, we created a user-defined bridge network so our Flask API container communicated with the database container using the hostname `database` instead of IP addresses.

### Q8: What is CI/CD and why is it used?
* **Speakable Answer**: Continuous Integration (CI) automatically builds and tests code on every commit. Continuous Delivery/Deployment (CD) automatically stages and releases validated builds to production. It is used to eliminate manual human errors, reduce release cycles, and maintain high code quality.
* **Project Example**: In our CI/CD pipeline, every pull request automatically ran Pytest and ESLint suites before code could merge to `main`.

### Q9: List CI/CD tools and which is best to use?
* **Speakable Answer**: Jenkins, GitHub Actions, GitLab CI, AWS CodePipeline, and Azure Pipelines. GitHub Actions is best for GitHub-hosted repositories; Jenkins is best for complex on-premise workflows requiring custom plugins; AWS CodePipeline is best for purely AWS-native setups.
* **Project Example**: We leveraged Azure DevOps pipelines with self-hosted Linux agents during my JSpiders internship to cut deployment cycles by 35%.

### Q10: Sample CI/CD pipeline and steps.
Steps: Checkout $	o$ Setup Environment $	o$ Install Dependencies $	o$ Run Unit Tests $	o$ Build Docker Image $	o$ Security Scan $	o$ Deploy to Cloud.

### Q11: Short explanations of EC2, VPC, S3, and EBS.
* **EC2**: Virtual compute servers in AWS with scalable CPU and RAM.
* **VPC**: Isolated private virtual network inside AWS where you define subnets, route tables, and gateways.
* **S3**: Highly durable, scalable object storage for files, backups, and media assets.
* **EBS**: Persistent virtual block storage volume attached to an EC2 instance like a hard drive.

### Q12: What is Terraform? Sample EC2 script.
* **Speakable Answer**: Terraform is an open-source Infrastructure as Code tool that provisions cloud infrastructure declaratively using HCL. It tracks actual cloud state in `.tfstate` and provides dry-run previews (`terraform plan`).
```hcl
provider "aws" { region = "ap-south-1" }
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.micro"
  tags          = { Name = "Rapyder-Demo" }
}
```

### Q13: What is Kubernetes? Sample deployment file.
* **Speakable Answer**: Kubernetes is a container orchestration platform that automates deployment, dynamic scaling, healing, and load balancing of containerized workloads across multi-node clusters.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 3
  selector:
    matchLabels: { app: web }
  template:
    metadata:
      labels: { app: web }
    spec:
      containers:
      - name: nginx
        image: nginx:alpine
        ports:
        - containerPort: 80
```

### Q14: Difference between Docker and Kubernetes?
* **Speakable Answer**: Docker builds and runs containers on a **single host machine**. Kubernetes coordinates, scales, and manages fleets of containers across a **cluster of multiple machines**. Docker packages the application; Kubernetes orchestrates it.

### Q15: Difference between AWS CloudFormation (CFT) and Terraform?
* **Speakable Answer**: CloudFormation is AWS-proprietary, written in verbose JSON/YAML, with state managed automatically by AWS. Terraform is multi-cloud, written in clean HCL, and keeps its own state file in remote backends like S3 with DynamoDB locking.

### Q16: Types of Kubernetes Services?
* **ClusterIP (Default)**: Exposes service internally within the cluster.
* **NodePort**: Exposes service on a static high port (30000–32767) on each worker node.
* **LoadBalancer**: Provisions a cloud provider load balancer (AWS NLB/ALB).
* **ExternalName**: Maps the service to an external DNS CNAME.

### Q17: Difference between Deployment, StatefulSet, DaemonSet, and ReplicaSet?
* **ReplicaSet**: Ensures a specified count of identical pods are running.
* **Deployment**: Manages ReplicaSets with zero-downtime rolling updates and rollbacks for stateless apps.
* **StatefulSet**: Provides stable network identities (`db-0`) and dedicated persistent storage for databases.
* **DaemonSet**: Runs exactly one copy of a pod on every worker node (logging, monitoring agents).

---

## 1.3 The Handwritten Round 2 & Round 3 Questions

* **In `df -h`, what is `-h`?**: Human-readable (displays sizes in K, M, G instead of raw blocks).
* **List running vs exited containers**: `docker ps` for running; `docker ps -a` for all including exited.
* **Get inside a running container**: `docker exec -it <container_name> /bin/sh` (or `/bin/bash`).
* **What is `ls -a`?**: Lists all files including hidden files starting with a dot (`.bashrc`, `.env`).
* **How to edit a file in Linux**: Open with `vim filename` (press `i` to insert, `Esc` then `:wq` to save and quit) or `nano filename` (`Ctrl+O` save, `Ctrl+X` exit).
* **Why Rapyder?**: Rapyder is an AWS Premier Tier Partner at the forefront of managed cloud services. I want hands-on exposure to enterprise client architectures, 24/7 incident handling, and FinOps practices.
* **Git vs GitHub**: Git is the local CLI tool; GitHub is the cloud platform hosting remote repositories with PR and CI/CD collaboration.
* **`ADD` vs `COPY` in Dockerfile**: `COPY` simply copies local files; `ADD` can also auto-extract local tarballs and download URLs. Best practice is `COPY`.
* **What does `df -u` mean?**: Trick question! There is no standard `-u` option in `df`. Standard options are `-h` (human-readable) and `-i` (inodes). In production, I verify options with `df --help`.
* **Define pipeline script**: Code defining CI/CD stages (build, test, deploy) stored directly in Git (Pipeline as Code).

---

## 1.4 Part 7 AWS Core & FinOps

* **IAM user vs role vs policy**: User = permanent identity for a person; Role = temporary identity assumed by a service (EC2) without keys; Policy = JSON document defining permissions.
* **Security group vs NACL**: Security group is instance-level and stateful (allow rules only); NACL is subnet-level and stateless (numbered allow and deny rules).
* **EBS vs S3 vs EFS**: EBS = block storage for one EC2; S3 = scalable object storage over HTTPS; EFS = shared NFS mounted by many Linux instances simultaneously.
* **CloudWatch vs CloudTrail**: CloudWatch monitors performance (metrics, logs, alarms); CloudTrail records who executed what API call (audit log).
* **How to reduce AWS costs**: Right-size instances, buy Savings Plans/Reserved Instances, migrate EBS from gp2 to gp3, delete unattached EBS volumes, and configure S3 lifecycle rules.
* **Region vs Availability Zone**: Region = geographical area (Mumbai); AZ = isolated datacenters within a Region with redundant power and networking.
* **High Availability vs Fault Tolerance**: HA = minimal downtime with rapid automatic recovery (Multi-AZ failover); FT = zero downtime via continuous live redundancy.

---

## 1.5 Part 7 Real-World Incident Troubleshooting Scenarios

* **EC2 not reachable via SSH**: Check 2/2 status checks $	o$ Security group port 22 $	o$ Route table IGW $	o$ Public IP $	o$ Local `.pem` permissions (`chmod 400`) $	o$ Use SSM Session Manager.
* **Website is slow or down**: Test with curl $	o$ Check ALB target health $	o$ CloudWatch CPU/memory metrics $	o$ Check Nginx error logs $	o$ Restart hung services or scale out $	o$ Escalate to L2.
* **CPU at 100%**: Run `top` or `ps aux --sort=-%cpu` $	o$ Identify PID $	o$ Check if runaway rogue process or genuine traffic $	o$ Collect thread dump, restart process, or scale out instance.
* **Disk full on Linux**: Run `df -h` to find full partition $	o$ Run `du -sh /var/* | sort -rh` $	o$ Clear old logs (`/var/log`) and run `docker system prune -f` $	o$ Expand EBS volume with `growpart` and `resize2fs`.
* **S3 Access Denied**: Check IAM policy permissions $	o$ S3 Bucket Policy $	o$ S3 Block Public Access settings $	o$ KMS key policy permissions $	o$ Explicit Deny always wins.
* **Share private S3 file temporarily**: Generate a pre-signed URL: `aws s3 presign s3://bucket/file --expires-in 3600`.
* **Back up EC2**: Create EBS snapshots (automated with AWS Backup or DLM) or create an AMI.
* **Accidental data deletion**: S3 = remove delete marker if versioning is on; EBS = restore volume from latest snapshot; RDS = Point-In-Time Restore (PITR).

---

## 1.6 Part 7 Linux & Networking Fundamentals

* **`top` vs `ps`**: `top` is real-time interactive live monitoring; `ps` is a one-time static process snapshot.
* **Hard link vs soft link**: Hard link shares the same inode (data survives if original name is deleted); Soft link (`ln -s`) is a path pointer that breaks if target is deleted.
* **`chmod 755`, `sudo`, `crontab`**: 755 = rwx for owner, rx for group/others; `sudo` runs commands as root; `crontab -e` schedules recurring jobs (`min hour day month dow command`).
* **Check ports, find file, check logs**: Ports: `ss -tulpn`; Find: `find / -name file.txt`; Logs: `tail -f /var/log/syslog` or `journalctl -u nginx -f`.
* **DNS, DHCP, IP, Subnet Mask, CIDR**: DNS = domain to IP; DHCP = auto-assigns IP configs; IP = network address; Subnet mask = separates network from host bits; CIDR = slash notation (`/24`).
* **URL in browser flow**: Browser cache $	o$ DNS query $	o$ TCP 3-way handshake (`SYN-SYNACK-ACK`) $	o$ TLS handshake $	o$ HTTP GET $	o$ Server responds $	o$ Browser renders.
* **TCP vs UDP**: TCP is reliable and connection-oriented (Web, SSH); UDP is connectionless and fast (DNS, video streaming).
* **`ping` vs `traceroute` vs `nslookup`**: `ping` tests reachability/RTT; `traceroute` shows each network hop; `nslookup` queries DNS resolution.

---

## 1.7 Part 7 Azure & GCP Multi-Cloud

* **Resource Group and Azure Monitor**: Resource Group is a logical management folder for related Azure resources; Azure Monitor tracks metrics, logs, and alert rules.
* **IaaS vs PaaS vs SaaS**: IaaS = you manage OS and apps (EC2, Azure VM); PaaS = provider manages OS/runtime, you deploy code (Elastic Beanstalk, App Service); SaaS = complete application (Microsoft 365, Gmail).
* **Public, Private, Hybrid Cloud**: Public = shared cloud infrastructure (AWS); Private = dedicated to one organization; Hybrid = on-premise connected to public cloud.
* **Multi-cloud**: Using multiple cloud providers to avoid vendor lock-in, optimize costs, and achieve disaster recovery.

---

## 1.8 Part 7 Containers, Kubernetes & DevOps Tools

* **Docker volume, Compose, Hub**: Volume = persistent data surviving container restarts; Compose = multi-container orchestration YAML; Hub = public container image registry.
* **Pod, Node, Cluster**: Pod = atomic unit with 1+ containers; Node = worker VM; Cluster = control plane + worker nodes.
* **ConfigMap, Secret, Ingress**: ConfigMap = non-sensitive plaintext configs; Secret = Base64-encoded sensitive data; Ingress = Layer 7 reverse proxy routing external traffic by host/path.
* **`CrashLoopBackOff` vs `Pending`**: `CrashLoopBackOff` = container keeps crashing (check `kubectl logs --previous`); `Pending` = scheduler cannot find node (insufficient CPU/RAM, taints, unbound PVC).
* **Git merge vs rebase; pull vs fetch**: `merge` combines branches with a merge commit; `rebase` replays commits linearly; `fetch` downloads commits without changing local code; `pull` is `fetch + merge`.
* **Ansible vs Jenkins**: Ansible is agentless configuration management over SSH; Jenkins is an automation server for CI/CD pipelines.

---

## 1.9 Part 7 ITSM, SLA Governance & Behavioral Excellence

* **Incident vs Problem vs Change Request**: Incident = unplanned disruption to fix immediately; Problem = underlying root cause to fix permanently; Change Request = planned, approved modification.
* **P1/P2/P3, Escalation, Bridge Call**: P1 = critical outage requiring immediate response and bridge call; Escalation = transferring ticket to L2 when approaching SLA limits; Bridge call = live call uniting all teams to resolve a P1.
* **Angry customer handling**: Listen actively without interrupting, acknowledge impact, communicate a clear action plan with realistic ETAs, provide updates every 15 minutes, and document in ticket.
* **KB Article and MTTR**: KB Article = documented SOP for known issues; MTTR = Mean Time to Resolve, measuring average outage duration.
* **Strengths & Weakness**: Strength = strong Linux/cloud fundamentals and calm troubleshooting under SLA pressure; Weakness = historically spent too long debugging alone, resolved by setting a strict 15-minute timebox before escalating to L2.
* **Questions to ask interviewer**:
  1. *"What ticketing and monitoring tools (e.g. ServiceNow, CloudWatch) will a Cloud Trainee work with daily?"*
  2. *"What does the mentorship path from L1 Trainee to L2 Cloud Engineer look like at Rapyder?"*

---

# PART 2: Ultra-Simple "Whiteboard" Manifests & Scripts

---

### 2.1 Minimal Single-Stage Dockerfile (Nginx)
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

### 2.2 Minimal Multi-Stage Dockerfile (Node.js)
```dockerfile
# Stage 1: Build
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Production Runner
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
EXPOSE 3000
CMD ["node", "dist/index.js"]
```

---

### 2.3 Minimal Docker Compose (`compose.yaml`)
```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
  db:
    image: redis:alpine
    ports:
      - "6379:6379"
```

---

### 2.4 Minimal Jenkins Declarative Pipeline (`Jenkinsfile`)
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to cloud...'
            }
        }
    }
}
```

---

### 2.5 Minimal GitHub Actions Pipeline (`ci.yml`)
```yaml
name: CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install && npm test
      - run: docker build -t myapp .
```

---

### 2.6 Minimal Kubernetes Pod (`pod.yaml`)
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: web
    image: nginx:alpine
```

---

### 2.7 Minimal Kubernetes Service (`service.yaml`)

#### ClusterIP (Internal):
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: ClusterIP
  selector:
    app: web
  ports:
  - port: 80
    targetPort: 80
```

#### NodePort (External):
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport
spec:
  type: NodePort
  selector:
    app: web
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30080
```

---

### 2.8 Minimal Kubernetes ReplicaSet (`replicaset.yaml`)
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: nginx:alpine
```

---

### 2.9 Minimal Kubernetes ReplicationController (`rc.yaml`)
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: my-rc
spec:
  replicas: 3
  selector:
    app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: nginx:alpine
```

---

### 2.10 Minimal Kubernetes Deployment (`deployment.yaml`)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: nginx:alpine
        ports:
        - containerPort: 80
```

---

### 2.11 Minimal Kubernetes DaemonSet (`daemonset.yaml`)
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: my-daemonset
spec:
  selector:
    matchLabels:
      app: agent
  template:
    metadata:
      labels:
        app: agent
    spec:
      containers:
      - name: agent
        image: fluent/fluent-bit:latest
```

---

### 2.12 Minimal Kubernetes Secret (`secret.yaml`)
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
stringData:
  DB_PASSWORD: "SuperSecretPassword123"
```

---

### 2.13 Minimal Kubernetes PV & PVC

#### PersistentVolume (`pv.yaml`):
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /data
```

#### PersistentVolumeClaim (`pvc.yaml`):
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

---

### 2.14 Minimal Terraform Script (AWS EC2)
```hcl
provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.micro"
  tags = {
    Name = "Simple-EC2"
  }
}
```

* **Core Commands**: `terraform init` $	o$ `terraform plan` $	o$ `terraform apply` $	o$ `terraform destroy`.

---

# PART 3: Quick-Revision Technology Cheatsheets

## 3.1 AWS Cloud Core Cheat Sheet
* **VPC**: Base `/16` network. Subnets reserve 5 IPs (.0, .1, .2, .3, .255).
* **Compute**: EC2 instances. Use IMDSv2 for metadata (`PUT` token first).
* **Storage**: EBS (gp3 baseline 3000 IOPS), S3 (11 9's durability), EFS (shared NFS).
* **Load Balancers**: ALB (Layer 7 HTTP), NLB (Layer 4 TCP).
* **Observability**: CloudWatch (performance/logs/alerts), CloudTrail (security audit API history).

## 3.2 Microsoft Azure & Multi-Cloud Cheat Sheet
* **Hierarchy**: Organization $	o$ Project $	o$ Resource Groups $	o$ Resources.
* **Pipelines**: Multi-stage YAML (`stages` $	o$ `jobs` $	o$ `steps`).
* **Agents**: Microsoft-Hosted (ephemeral) vs Self-Hosted (sitting in private VNet).
* **Security**: Workload Identity Federation (OIDC) eliminates hardcoded client secrets.

## 3.3 Linux Systems Administration Cheat Sheet
* **Diagnostics**: `top` (live CPU), `free -h` (RAM), `df -h` (disk space), `uptime` (load average).
* **Networking**: `ss -tulpn` (listening ports), `ip a` (IP addresses), `curl -Iv` (headers).
* **Permissions**: `chmod 755` (rwxr-xr-x), SUID (4000), SGID (2000), Sticky Bit (1000).
* **Services**: `systemctl start` (now), `systemctl enable` (on reboot), `journalctl -u <svc> -f` (logs).

## 3.4 Git Version Control & Reflog Cheat Sheet
* **3 Trees**: Working Directory $	o$ Staging Area (`git add`) $	o$ Repository (`git commit`).
* **Branching**: Fast-forward merge (no commit) vs 3-way merge (merge commit).
* **Reset**: `--soft` (keeps staged), `--mixed` (keeps unstaged), `--hard` (destructive).
* **Disaster Recovery**: `git reflog` tracks every HEAD movement; recover with `git reset --hard HEAD@{1}`.

## 3.5 Jenkins & CI/CD Automation Cheat Sheet
* **Architecture**: Controller (scheduler/UI) + Distributed Agents (runs builds). Never build on Master!
* **5 Triggers**: GitHub Webhook, Poll SCM (`H/15 * * * *`), Build Periodically (`H 2 * * *`), Upstream/Downstream, Remote Curl.
* **`/tmp` Crisis**: Relocate `-Djava.io.tmpdir` and invoke `cleanWs()` in post-actions.

## 3.6 Docker Container Engineering Cheat Sheet
* **Pillars**: Namespaces (isolation) + cgroups (resource limits).
* **Instructions**: `RUN` (build time), `CMD` (default runtime arguments), `ENTRYPOINT` (fixed executable).
* **Prune**: `docker system prune -f --filter "until=48h"`. Never use `--volumes` in automated cron!

## 3.7 Kubernetes Orchestration Cheat Sheet
* **Workloads**: Pod $	o$ ReplicaSet $	o$ Deployment $	o$ StatefulSet $	o$ DaemonSet.
* **Networking**: ClusterIP (internal), NodePort (external node port), Ingress (Layer 7 routing).
* **Probes**: Startup (boot check), Readiness (traffic gating), Liveness (kills/restarts deadlocks).
* **Diagnostics**: `kubectl describe pod` (events) and `kubectl logs --previous` (crash trace).

## 3.8 Terraform Infrastructure as Code Cheat Sheet
* **Lifecycle**: `init` $	o$ `plan` $	o$ `apply` $	o$ `destroy`.
* **State**: S3 remote backend + DynamoDB table for distributed locking.
* **Iterators**: Always prefer `for_each` over `count` to avoid array-shift destruction.
* **Modern 1.5+**: Declarative `import` blocks and `moved` blocks for zero-downtime refactors.

---

# PART 4: Real-Time Projects Deep Dive (From Your Resume)

## 4.1 TaskFlow V4.9.2 Cloud Platform (AWS / Docker / Supabase)
* **Architecture**: Multi-tier containerized platform with React 19 frontend, Python Flask 3.1 REST API, Gunicorn WSGI, unified behind an Nginx reverse proxy on Port 80.
* **Key Achievements**:
  * Eliminated CORS errors and masked internal application ports using Nginx reverse proxy directives.
  * Reduced Docker image footprint by 45% (down to 180MB) using multi-stage builds and non-root security contexts.
  * Engineered Docker Compose health-check dependencies (`condition: service_healthy`) to eliminate database connection race conditions.
  * Configured Nginx gzip compression and asset caching, reducing bundle transfer latency by 35%.

## 4.2 Azure DevOps CI/CD Automation Suite
* **Architecture**: Multi-stage YAML pipeline (Build $	o$ Test $	o$ Deploy) on Linux VMs with self-hosted agents, Apache `mod_proxy`, and LGTM observability stack.
* **Key Achievements**:
  * Automated unattended provisioning of Azure self-hosted runners using Linux `systemd` daemons.
  * Enforced outbound-only HTTPS 443 polling on runners, eliminating all inbound firewall rules and public attack surfaces.
  * Integrated the LGTM stack (Grafana, Loki, Promtail) for automated container log streaming and latency alerting.
  * Enforced Azure Boards governance with mandatory `AB#` work item linking and branch protection rules before pull request merges.
