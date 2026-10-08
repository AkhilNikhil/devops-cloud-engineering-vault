# ⚡ Enterprise Cloud Consulting — Quick Revision Cheatsheet & Day-of-Interview Guide

**Candidate:** Akhil B M  
**Company:** Enterprise Cloud Consulting Pvt Ltd  
**Headquarters:** Bengaluru, India  
**Status:** AWS Premier Tier Services Partner (Top AWS Partner Tier)  
**Target Roles:** Cloud Engineer / Associate Cloud Engineer / DevOps Trainee  

---

## 🏢 1. About Enterprise AWS (Why It Matters in Your Interview)
* **What Enterprise AWS Does:** End-to-end cloud consulting, enterprise cloud migration to AWS, 24/7 Managed Cloud Operations, DevOps/DevSecOps automation, FinOps (Cost Optimization), and Generative AI on AWS (Bedrock).
* **Key Talking Point:** Enterprise AWS is an **AWS Premier Tier Partner**—the highest recognition in the AWS partner network. They value candidates who understand **AWS architecture best practices**, **cost optimization (FinOps)**, and **real-world troubleshooting**.
* **Culture & Expectations:** They look for strong fundamentals over memorization, willingness to work in rotational shifts for managed services, and hands-on debugging ability.

---

## 🚇 2. Travel & Walk-In Day Logistics (Bengaluru, India)
* **Metro Route:** Take the **Namma Metro Purple Line** and deboard at **M.G. Road Metro Station** (Exit towards Church Street / Trinity side).
* **Timing:** Arrive **45–60 minutes before scheduled start time**. Walk-ins at Bengaluru tech companies often see large queues; being in the first batch gets you interviewed when interviewers are fresh.
* **Dress Code:** Smart Formal or Business Casual (collared shirt, formal trousers, formal shoes).
* **Documents to Carry in Folder:**
  1. 3 Printed copies of your Resume.
  2. Government ID (Aadhaar Card / PAN Card).
  3. Degree Certificate / Provisional Degree & Marks cards copies.
  4. Project links & GitHub profile printed / bookmarked.
  5. Notepad & blue/black pen for whiteboard/architecture problems.

---

## 🎙️ 3. Your 60-Second Elevator Pitch (Memorize This)
> *"Good morning / afternoon. My name is Akhil B M. I am a Cloud and DevOps Engineer based here in Bengaluru.*  
> *My technical foundation centers around architecting resilient AWS infrastructure, automating CI/CD delivery pipelines, and container orchestration with Docker and Kubernetes.*  
> *Recently, I engineered **TaskFlow**, a multi-tier production application on AWS EC2 orchestrated with Docker Compose and Nginx, featuring automated MySQL persistent volume management and zero-downtime healthcheck gates. I've also built automated multi-stage pipelines in Azure DevOps with security scanning, and managed Kubernetes clusters using kOps.*  
> *I know Enterprise AWS is an AWS Premier Tier Partner at the forefront of cloud migration and FinOps. I want to bring my hands-on troubleshooting skills and passion for AWS automation to contribute to your client delivery from day one."*

---

## 📐 4. Top 15 "Must-Know" Architectural Rules

### Rule 1: Security Groups vs NACLs
* **Security Group:** Instance/ENI level, **Stateful** (return traffic is automatically allowed), Allow rules only.
* **NACL:** Subnet level, **Stateless** (both inbound and outbound ephemeral ports must be allowed), Allow & Deny rules in numerical order.

### Rule 2: Public vs Private Subnets
* **Public Subnet:** Route Table points `0.0.0.0/0` to an **Internet Gateway (IGW)**. (Used for ALBs & Bastions).
* **Private Subnet:** Route Table points `0.0.0.0/0` to a **NAT Gateway** in a public subnet. (Used for App servers & Databases).

### Rule 3: IAM Security
* **Never hardcode AWS keys on EC2.** Always attach an **IAM Role** via Instance Profile so the instance fetches temporary rotating credentials from Instance Metadata (IMDSv2).

### Rule 4: FinOps Cost Savings (Enterprise AWS Special)
* Migrate EBS volumes from `gp2` to `gp3` (instant 20% cost savings + custom baseline IOPS).
* Delete unattached EBS volumes and unassociated Elastic IPs.
* Implement S3 Lifecycle policies (transition to S3 Glacier / Deep Archive).
* Use EC2 Spot Instances for fault-tolerant workers and CI/CD runners (up to 90% savings).
* Use Savings Plans for steady baseline production workloads (up to 72% savings).

### Rule 5: Multi-AZ vs Read Replicas
* **Multi-AZ:** Synchronous replication for **High Availability & Disaster Recovery**. Standby DB cannot serve queries.
* **Read Replicas:** Asynchronous replication for **Read Scalability**. Serves `SELECT` queries to offload the primary database.

### Rule 6: Linux Triage Sequence (When Server is Slow)
1. `uptime` / `top`: Check CPU load averages and CPU hogs.
2. `free -m`: Check available RAM and swap usage.
3. `df -h` & `df -i`: Check disk space and inode saturation.
4. `iostat -xz 1 5`: Check disk I/O wait.
5. `dmesg -T | tail -50`: Check for OOM Killer events.

### Rule 7: CrashLoopBackOff in Kubernetes
1. `kubectl describe pod <name>` &rarr; Check Events for OOMKilled or mount failures.
2. `kubectl logs <name> --previous` &rarr; Check standard error logs from the crashed container.
3. Verify environment variables, database strings, ConfigMaps, and Secrets.

### Rule 8: Docker Image Optimization
* Use **Multi-stage builds** (compile in builder, run in minimal runtime).
* Use minimal base images (`alpine` or `slim`).
* Chain `RUN` commands with `&&` and clear package caches (`rm -rf /var/lib/apt/lists/*`).

---

## 🛠️ 5. Akhil's STAR Project Explanations

### Project 1: TaskFlow Containerized Platform on AWS EC2
* **Situation:** Needed to deploy a multi-tier production task management platform (React/Vite, Flask API, MySQL 8.0, Nginx) on a resource-constrained AWS EC2 instance.
* **Task:** Ensure zero downtime, persistent data storage, and automated health checks.
* **Action:**
  * Implemented an Nginx reverse proxy masking backend port 5000 and eliminating CORS.
  * Encrypted sensitive JWT secrets using `openssl rand -hex 32`.
  * **Solved Incident:** EC2 ran out of space (`Error 28: No space left on device`) because a 2GB swap file combined with local Docker Vite builds filled the default 8GB EBS volume, crashing MySQL InnoDB initialization.
  * **Resolution:** Resized swap to 512MB, transitioned CI/CD to pull pre-built optimized multi-stage images from Docker Hub, and added `condition: service_healthy` in Docker Compose so Nginx and Flask wait for MySQL ping checks before starting.
* **Result:** 100% reliable startup, zero database race conditions, and stable operation on minimal EC2 compute.

### Project 2: Kubernetes Cluster Management with kOps
* **Situation:** Needed complete control over Kubernetes cluster provisioning without incurring managed EKS hourly fees.
* **Task:** Deploy and manage a production-grade Kubernetes cluster on AWS EC2 using kOps.
* **Action:**
  * Configured AWS IAM permissions, S3 state store bucket, and Route 53 DNS.
  * Provisioned master and worker nodes using `kops create cluster`.
  * Configured Ingress Controllers, Namespaces, ConfigMaps, Secrets, and Rolling Updates.
* **Result:** Full operational understanding of the Kubernetes control plane (etcd, kube-apiserver, scheduler) with zero managed EKS cluster fees.

---

## 💬 6. Golden Rules for the Interview Room
1. **Never Bluff:** If you don't know a specific AWS service or command, say:
   > *"I haven't worked with that specific feature in production yet, but based on AWS architecture principles, I would check the CloudWatch logs and official AWS documentation to resolve it."*
2. **Be Structured:** When troubleshooting, follow the network/OS stack: Network &rarr; Firewall &rarr; OS &rarr; Application &rarr; Database.
3. **Show Enthusiasm for Learning:** Mention your hands-on drive and readiness for rotational shifts and cloud certifications (AWS Solutions Architect Associate).
