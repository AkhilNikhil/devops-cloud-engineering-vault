# 🚀 DevOps & Cloud Engineering Master Vault

Welcome to the **DevOps & Cloud Engineering Master Vault**. This repository is a centralized, production-grade knowledge base covering containerization, Kubernetes cluster orchestration, multi-cloud architecture (AWS & Azure), Infrastructure as Code (Terraform), CI/CD automation pipelines, Linux systems administration, and senior technical interview preparation.

Every technical domain has been **consolidated into authoritative master guides**—engineered with deep point-by-point explanations, diagrams, step-by-step production runbooks, and zero outdated information.

---

## 🗺️ Recommended 8-Phase Study Roadmap

```mermaid
flowchart LR
    P1["1. Linux & Git"] --> P2["2. Docker"]
    P2 --> P3["3. Kubernetes & kOps"]
    P3 --> P4["4. AWS Cloud"]
    P4 --> P5["5. Terraform IaC"]
    P5 --> P6["6. CI/CD & Azure DevOps"]
    P6 --> P7["7. Hands-on Coding Drill"]
    P7 --> P8["8. 640Q&A Master Review"]
```

* **Phase 1 (Foundations):** [06-Linux-and-Git](#-06-linux-and-git) ➔ Kernel internals, process lifecycle, permissions & special bits (SUID, SGID, Sticky), `systemctl enable` vs `start`, diagnostics (`free`, `df`, `vmstat`, `iostat`), text power tools (`grep`, `awk`, `sed`), and complete Git branch, undo (`reset`, `revert`), stash, and `reflog` recovery.
* **Phase 2 (Containers):** [01-Docker](#-01-docker) ➔ Linux namespaces & cgroups, multi-stage builds (Node.js & Python), Compose v2 orchestration, storage volumes & `system prune`, user-defined bridge DNS, modern security with **Docker Scout** (CVE scanning) and **Docker Init**.
* **Phase 3 (Orchestration):** [02-Kubernetes-and-kOps](#-02-kubernetes-and-kops) ➔ Control plane & worker node internals, why Swarm failed vs K8s won, production **AWS kOps cluster setup via Operator Instances**, workload evolution (Pods $	o$ RC $	o$ RS $	o$ Deployments), Services, Ingress v1, PV/PVC/StorageClass, and HPA auto-scaling.
* **Phase 4 (Cloud Architecture):** [03-AWS-Cloud-Architecture](#-03-aws-cloud-architecture) ➔ **Complete binary CIDR subnetting math** (Class A/B/C, /16 to /28, AWS 5 reserved IPs), multi-tier VPC isolation, Security Groups vs NACLs, EC2 connection methods (SSM vs SSH), AMI vs Launch Template, EBS vs Snapshot, S3 storage tiers & lifecycle, and Aurora Multi-AZ.
* **Phase 5 (Infrastructure as Code):** [04-Terraform-IaC](#-04-terraform-iac) ➔ Declarative HCL, S3 backend with DynamoDB state locking, modern Terraform 1.5+ (`import`, `moved`), AWS Provider v5.x decoupled resources, meta-arguments, and disaster recovery.
* **Phase 6 (Automation & Multi-Cloud):** [05-CICD-Jenkins-Automation](#-05-cicd-jenkins-automation) & [08-Azure-DevOps-Engineering](#-08-azure-devops-engineering) ➔ The 5 Jenkins build triggers, cron scheduling & weather reports, the **production `/tmp` low memory out-of-space crisis resolution**, Maven lifecycle & Nexus publishing, Declarative Jenkinsfiles, Ansible agentless automation, and Azure DevOps multi-stage YAML pipelines.
* **Phase 7 (Hands-On Coding Drill):** Practice writing production Dockerfiles, Compose specs, K8s manifests, Terraform HCL, and Jenkinsfiles from memory.
* **Phase 8 (Master Technical Review):** [640QA_Master_Systems_Engineering_Guide.md](07-Master-Interview-QnA/640QA_Master_Systems_Engineering_Guide.md) ➔ The complete 640-question technical interview encyclopedia spanning all 12 engineering domains.

---

## 📑 Repository Master Catalog

### 🐳 01-Docker
* 📄 [`Docker_Master_Engineering_Guide.md`](01-Docker/Docker_Master_Engineering_Guide.md)
  * **Layer 1:** VMs vs Containers, Linux Namespaces (`pid`, `net`, `mnt`, `ipc`, `uts`, `user`), and `cgroups` resource limits.
  * **Layer 2:** Daemon engine architecture (`dockerd`, `containerd`, `containerd-shim`, `runc`).
  * **Layer 3:** Complete Dockerfile instructions reference (`FROM`, `WORKDIR`, `COPY` vs `ADD`, `RUN`, `ENV` vs `ARG`, `EXPOSE`, `USER`).
  * **Layer 4:** RUN vs CMD vs ENTRYPOINT (exec form vs shell form, signal propagation).
  * **Layer 5:** Storage systems: Named Volumes, Bind Mounts, and tmpfs memory mounts.
  * **Layer 6:** Docker maintenance & cleanup: `docker system prune` flags (`-a`, `--volumes`, `--filter`).
  * **Layer 7:** Networking: User-defined bridge DNS resolution vs default bridge.
  * **Layer 8:** Modern Tooling: **Docker Scout** (CVE & vulnerability scanning) and **Docker Init** (automated scaffolding).
  * **Layer 9:** Multi-Stage Dockerfile templates for **Node.js** (non-root `USER 10001`, alpine) and **Python** (builder wheel caching to slim).
  * **Layer 10:** Production Docker Compose v2 specification (`compose.yaml` with healthchecks and network isolation).
  * **Layer 11:** Production troubleshooting playbook (Exit Code 137 OOMKilled, port conflicts, volume permission errors).

---

### ☸️ 02-Kubernetes-and-kOps
* 📄 [`Kubernetes_and_kOps_Master_Guide.md`](02-Kubernetes-and-kOps/Kubernetes_and_kOps_Master_Guide.md)
  * **Layer 1:** Orchestration Evolution: Standalone Docker drawbacks $	o$ Docker Swarm bottlenecks $	o$ Kubernetes.
  * **Layer 2:** Control Plane components (`kube-apiserver`, `etcd` Raft quorum, `kube-scheduler`, `kube-controller-manager`, `cloud-controller-manager`).
  * **Layer 3:** Worker Node architecture (`kubelet`, `kube-proxy` iptables/IPVS, `containerd` CRI runtime).
  * **Layer 4:** Production **AWS kOps cluster setup via Operator Instances** (S3 state store, gossip domains, multi-zone node pools).
  * **Layer 5:** Workload Evolution: Pods $	o$ ReplicationController (RC) $	o$ ReplicaSets (RS) $	o$ Deployments.
  * **Layer 6:** Cluster networking: `ClusterIP`, `NodePort`, `LoadBalancer`, and `networking.k8s.io/v1` Ingress with TLS.
  * **Layer 7:** Persistent storage: Dynamic provisioning via `StorageClass`, `PVC`, and `PV`.
  * **Layer 8:** Configuration management: `ConfigMaps` and `Secrets`.
  * **Layer 9:** Health probes (Startup, Readiness, Liveness) and Horizontal Pod Autoscaler (`HPA v2`).
  * **Layer 10:** Specialized workloads: DaemonSets, StatefulSets, Jobs, and CronJobs.
  * **Layer 11:** Complete `kubectl` command reference and troubleshooting playbook (`CrashLoopBackOff`, `ImagePullBackOff`, `Pending`).

---

### ☁️ 03-AWS-Cloud-Architecture
* 📄 [`AWS_Cloud_Architecture_Master_Guide.md`](03-AWS-Cloud-Architecture/AWS_Cloud_Architecture_Master_Guide.md)
  * **Layer 1:** Cloud service models (IaaS, PaaS, SaaS) and deployment models (Public, Private, Hybrid, Cloud Bursting).
  * **Layer 2:** Global infrastructure: Regions, Availability Zones (< 2ms fiber), and Edge Locations (CloudFront CDN & WAF).
  * **Layer 3:** **Complete Binary CIDR Subnetting Math**:
    * IPv4 32-bit structure and Class A, B, C, D, E breakdown.
    * The subnetting formula ($2^n$ subnets, $2^h - 2$ hosts).
    * **The AWS 5 Reserved IPs per subnet rule** (Network, Router, DNS, Future, Broadcast).
    * Step-by-step CIDR reference table from `/16` (65,531 usable) down to `/28` (11 usable).
  * **Layer 4:** Multi-tier VPC architecture: Internet Gateway, Public/Private Route Tables, and NAT Gateway vs NAT Instance.
  * **Layer 5:** Security Groups (stateful) vs Network ACLs (stateless, numbered rules).
  * **Layer 6:** EC2 Compute: **AMI vs Launch Template** detailed comparison table.
  * **Layer 7:** The 4 EC2 connection methods: SSM Session Manager, SSH with `.pem`, EC2 Instance Connect, and EC2 Serial Console.
  * **Layer 8:** Elastic Block Store (EBS) Volumes vs Snapshots (`gp3`, `io2 Block Express`, multi-attach).
  * **Layer 9:** S3 Object Storage: Storage classes, Lifecycle Transition rules, and Cross-Region Replication (CRR).
  * **Layer 10:** IAM security: Least privilege, Role-based delegation, policy evaluation precedence.
  * **Layer 11:** Elastic Load Balancing (ALB Layer 7 vs NLB Layer 4) and Auto Scaling Groups (ASG).
  * **Layer 12:** Managed databases: Amazon RDS Multi-AZ vs Aurora vs DynamoDB.
  * **Layer 13:** Modern security standards: IMDSv2 token security and CloudWatch observability.

---

### 🏗️ 04-Terraform-IaC
* 📄 [`Terraform_IaC_Master_Guide.md`](04-Terraform-IaC/Terraform_IaC_Master_Guide.md)
  * **Layer 1:** Core IaC principles and declarative vs imperative paradigms.
  * **Layer 2:** Architecture: Core engine, provider plugins, state mapping, and dependency graph.
  * **Layer 3:** Complete production VPC walkthrough in HCL.
  * **Layer 4:** Remote backend governance: Amazon S3 with DynamoDB state locking.
  * **Layer 5:** Variables, outputs, locals, and modular architecture.
  * **Layer 6:** Meta-arguments: `count`, `for_each`, `depends_on`, and `lifecycle` blocks.
  * **Layer 7:** Modern Terraform 1.5+ features: `import` blocks, `moved` refactoring, and AWS Provider v5.x decoupled resources.

---

### 🚀 05-CICD-Jenkins-Automation
* 📄 [`Jenkins_and_CICD_Master_Guide.md`](05-CICD-Jenkins-Automation/Jenkins_and_CICD_Master_Guide.md)
  * **Layer 1:** Origins: Hudson to Jenkins fork (2011) and Controller-Agent distributed architecture.
  * **Layer 2:** **The 5 Jenkins Build Triggers**:
    1. GitHub Hook Trigger for GITScm (Webhooks).
    2. Poll SCM (Scheduled Git polling).
    3. Build periodically (Unconditional scheduled cron).
    4. Build after other projects are built (Upstream / Downstream).
    5. Trigger builds remotely (REST API token).
  * **Layer 3:** Cron scheduling syntax (`* * * * *`) and the `H` hash symbol.
  * **Layer 4:** Jenkins Weather Report stability indicators (Sunny, Cloud & Sun, Cloudy, Rain, Storm).
  * **Layer 5:** **Production Emergency Crisis Runbook: The `/tmp` Low Memory Issue** (root cause, `fstab` 3GB tmpfs reallocation, remounting).
  * **Layer 6:** Apache Maven build lifecycle (`compile`, `test`, `package`, `deploy`), artifact formats (JAR, WAR, EAR), and Nexus OSS publishing.
  * **Layer 7:** Security: Role-Based Authorization Strategy plugin (Global, Project, Agent roles).
  * **Layer 8:** Complete production Declarative `Jenkinsfile` blueprint with SonarQube quality gates, Docker Scout scanning, and Kubernetes deployment.
  * **Layer 9:** Ansible agentless configuration management: Inventory files (`hosts.ini`), ad-hoc commands, Playbooks, Handlers, Jinja2 templating, and Ansible Vault encryption.

---

### 🐧 06-Linux-and-Git
* 📄 [`Linux_Master_Engineering_Guide.md`](06-Linux-and-Git/Linux_Master_Engineering_Guide.md)
  * **Layer 1:** Linux kernel architecture and Filesystem Hierarchy Standard (FHS).
  * **Layer 2:** POSIX file permissions, octal calculation, and special bits (SUID 4000, SGID 2000, Sticky Bit 1000).
  * **Layer 3:** Process management, signals (`SIGHUP 1`, `SIGTERM 15`, `SIGKILL 9`), and `systemd` administration (**`systemctl enable` vs `systemctl start`**).
  * **Layer 4:** System resource diagnostics: CPU (`top`, `uptime`), Memory (`free -h`), Disk (`df -h`, `du`), I/O (`vmstat`, `iostat`).
  * **Layer 5:** File location utilities: `which` vs `whereis` vs `locate` vs `find`.
  * **Layer 6:** Text processing power tools: `grep`, `awk` column filtering & math, `sed` in-place replacements.
  * **Layer 7:** OSI 7-Layer vs TCP/IP 4-Layer model, TCP 3-way handshake, and network CLI toolchain (`ss -tulpn`, `curl`, `dig`, `tcpdump`).
* 📄 [`Git_Master_Engineering_Guide.md`](06-Linux-and-Git/Git_Master_Engineering_Guide.md)
  * **Layer 1:** Centralized vs Distributed VCS architecture.
  * **Layer 2:** The 4 Git working areas: Working Directory, Staging Area, Local Repository, and Remote Repository.
  * **Layer 3:** Categorized CLI reference: Setup, Staging, Commits, Inspection, Branching, Remotes.
  * **Layer 4:** Branching strategies: Trunk-Based Development vs GitFlow.
  * **Layer 5:** `git merge` (three-way merge commit) vs `git rebase` (linear history rewriting).
  * **Layer 6:** Undoing changes safely: `git restore` vs `git reset` (`--soft`, `--mixed`, `--hard`) vs `git revert`.
  * **Layer 7:** Advanced power tools: `git stash` operations, `git cherry-pick`, and interactive squashing (`git rebase -i`).
  * **Layer 8:** Disaster recovery: Recovering lost commits and deleted branches via **`git reflog`**.

---

### 🎯 07-Master-Interview-QnA
* 📄 [`640QA_Master_Systems_Engineering_Guide.md`](07-Master-Interview-QnA/640QA_Master_Systems_Engineering_Guide.md) (444 KB)
  * The definitive 640-question technical interview encyclopedia spanning Linux, Git, Docker, Kubernetes, AWS, Terraform, Jenkins, Ansible, Azure DevOps, Python scripting, Database engineering, and Systems Architecture.
* 📄 [`Taskflow_Full_Stack_DevOps_Project_Guide.md`](07-Master-Interview-QnA/Taskflow_Full_Stack_DevOps_Project_Guide.md) (210 KB)
  * End-to-end full-stack containerized enterprise task and team collaboration system architecture guide with database migrations, Docker Compose, and cloud deployment runbooks.
* 📄 [`Projects_Architecture_Cheatsheet.md`](07-Master-Interview-QnA/Projects_Architecture_Cheatsheet.md)
* 📄 [`DevOps_Interview_Quick_Cheatsheet.md`](07-Master-Interview-QnA/DevOps_Interview_Quick_Cheatsheet.md)

---

### 🔷 08-Azure-DevOps-Engineering
* 📄 [`Azure_DevOps_Master_Engineering_Guide.md`](08-Azure-DevOps-Engineering/Azure_DevOps_Master_Engineering_Guide.md)
  * **Layer 1:** The 5 core services: Azure Boards, Azure Repos, Azure Pipelines, Azure Test Plans, Azure Artifacts.
  * **Layer 2:** Multi-stage YAML pipeline architecture (Stages $	o$ Jobs $	o$ Steps).
  * **Layer 3:** Microsoft-Hosted vs Self-Hosted Linux build agents.
  * **Layer 4:** Service Connections: Azure Resource Manager (ARM) with Workload Identity Federation (OIDC).
  * **Layer 5:** Variable Groups & Azure Key Vault secret linking.
  * **Layer 6:** Environment approval gates and deployment strategies (RunOnce, Rolling, Canary).
