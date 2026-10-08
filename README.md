# 🚀 DevOps & Cloud Engineering Master Vault

Welcome to the **DevOps & Cloud Engineering Master Vault**. This repository is a centralized, production-grade knowledge base covering containerization, Kubernetes cluster orchestration, multi-cloud architecture (AWS & Azure), Infrastructure as Code (Terraform), CI/CD automation pipelines, Linux systems administration, and senior technical interview preparation.

Every technical domain has been **consolidated into a single authoritative master guide**—eliminating redundant documents, outdated commands, and cognitive clutter.

---

## 🗺️ Recommended 8-Phase Study Roadmap

Follow this progressive learning roadmap to move smoothly from operating system fundamentals through cloud architecture and hands-on coding:

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

* **Phase 1 (Foundations):** [06-Linux-and-Git](#-06-linux-and-git) ➔ Kernel internals, process management (`fork`/`exec`/zombies), file permissions, modern networking (`ss`/`ip`), bash strict mode, and Git DAG object model.
* **Phase 2 (Containers):** [01-Docker](#-01-docker) ➔ Linux namespaces/cgroups, Overlay2 CoW filesystem, multi-stage builds, non-root security, and Docker Compose orchestration.
* **Phase 3 (Orchestration):** [02-Kubernetes-and-kOps](#-02-kubernetes-and-kops) ➔ Control plane mechanics, containerd runtime, Pods/Deployments/Services, Ingress, probes, and self-managed kOps on AWS EC2.
* **Phase 4 (Cloud Architecture):** [03-AWS-Cloud-Architecture](#-03-aws-cloud-architecture) ➔ Multi-tier VPC isolation, IMDSv2 token security, EBS `gp3`, S3 lifecycle rules, IAM least privilege, RDS/Aurora, and FinOps cost optimization.
* **Phase 5 (Infrastructure as Code):** [04-Terraform-IaC](#-04-terraform-iac) ➔ Modern Terraform 1.5+ (`import`, `moved`), AWS Provider v5.x decoupled resources, S3 backend with DynamoDB state locking, and disaster recovery.
* **Phase 6 (Automation & Multi-Cloud):** [05-CICD-Jenkins-Automation](#-05-cicd-jenkins-automation) & [08-Azure-DevOps-Engineering](#-08-azure-devops-engineering) ➔ Declarative Jenkinsfiles, SonarQube quality gates, Nexus publishing, Azure Boards, multi-stage YAML pipelines, and self-hosted Linux agent pools.
* **Phase 7 (Hands-On Coding Drill):** [HANDS_ON_CODE_PRACTICE.md](07-Master-Interview-QnA/HANDS_ON_CODE_PRACTICE.md) ➔ Write production Dockerfiles, Compose specs, K8s manifests, Terraform HCL, and Jenkinsfiles from memory without looking at notes.
* **Phase 8 (Master Technical Review):** [640QA_Master_Systems_Engineering_Guide.md](07-Master-Interview-QnA/640QA_Master_Systems_Engineering_Guide.md) ➔ The complete 640-question technical interview encyclopedia spanning all 12 engineering domains.

---

## 📑 Repository Master Catalog

### 🐳 01-Docker
* 📄 [`Docker_Master_Engineering_Guide.md`](01-Docker/Docker_Master_Engineering_Guide.md)
  * **Layer 1:** VMs vs Containers, Linux Namespaces (`pid`, `net`, `mnt`), and `cgroups` resource limits.
  * **Layer 2:** Docker Engine daemon architecture (`dockerd`, `containerd`, `containerd-shim`, `runc`).
  * **Layer 3:** Overlay2 union filesystem, Layer caching, and Volume vs Bind mount vs tmpfs mechanics.
  * **Layer 4:** Modern Multi-Stage Dockerfile template with non-root security (`USER 10001`).
  * **Layer 5:** Modern Docker Compose specification (`compose.yaml` with healthchecks).
  * **Layer 6:** Production command cheat sheet and troubleshooting playbook (Exit Code 137 OOMKilled, port conflicts).

---

### ☸️ 02-Kubernetes-and-kOps
* 📄 [`Kubernetes_and_kOps_Master_Guide.md`](02-Kubernetes-and-kOps/Kubernetes_and_kOps_Master_Guide.md)
  * **Layer 1:** Control Plane components (`kube-apiserver`, `etcd` Raft quorum, `kube-scheduler`, `kube-controller-manager`).
  * **Layer 2:** Worker Node architecture (`kubelet`, `kube-proxy` iptables/IPVS, `containerd` runtime).
  * **Layer 3:** Core workloads (Pods, Deployments, StatefulSets, DaemonSets, Jobs).
  * **Layer 4:** Cluster networking: `ClusterIP`, `NodePort`, `LoadBalancer`, and `networking.k8s.io/v1` Ingress.
  * **Layer 5:** Probes (`startup`, `liveness`, `readiness`) and Auto-Scaling (`HPA v2`).
  * **Layer 6:** Production kOps cluster setup on AWS EC2 with Route53 private DNS and S3 state store.
  * **Layer 7:** Production YAML blueprint with resource limits and non-root security context.
  * **Layer 8:** Troubleshooting guide (`CrashLoopBackOff`, `OOMKilled`, `ImagePullBackOff`, `Pending`).

---

### ☁️ 03-AWS-Cloud-Architecture
* 📄 [`AWS_Cloud_Architecture_Master_Guide.md`](03-AWS-Cloud-Architecture/AWS_Cloud_Architecture_Master_Guide.md)
  * **Layer 1:** Well-Architected Framework (Security, Reliability, Cost Optimization, Performance).
  * **Layer 2:** Multi-Tier VPC Networking (Public, Private App, Private Isolated DB subnets, IGW, NAT Gateways, S3 Gateway Endpoints).
  * **Layer 3:** EC2 Compute, AWS Graviton3/4 arm64, and mandatory IMDSv2 token hardening.
  * **Layer 4:** Storage architectures: EBS `gp3` (independent 3,000 IOPS baseline) and S3 Intelligent-Tiering/Glacier lifecycles.
  * **Layer 5:** IAM governance: Principle of Least Privilege, temporary STS AssumeRole credentials, and Instance Profiles.
  * **Layer 6:** High-availability databases: RDS Multi-AZ synchronous DR vs asynchronous Read Replicas, and Amazon Aurora distributed storage.
  * **Layer 7:** FinOps cost optimization and production AWS troubleshooting playbook.

---

### 🏗️ 04-Terraform-IaC
* 📄 [`Terraform_IaC_Master_Guide.md`](04-Terraform-IaC/Terraform_IaC_Master_Guide.md)
  * **Layer 1:** Declarative IaC principles, state files, and idempotency.
  * **Layer 2:** AWS Provider v5.x decoupled resources (standalone `aws_s3_bucket_versioning`).
  * **Layer 3:** Remote State Backend (S3 encrypted state + DynamoDB `LockID` state locking).
  * **Layer 4:** Modern Terraform 1.5+ features: declarative `import` blocks, `moved` blocks for safe refactoring, and `check` validation blocks.
  * **Layer 5:** Modular architecture, variable validation, and lifecycle rules (`create_before_destroy`, `prevent_destroy`).
  * **Layer 6:** State disaster recovery (`force-unlock`, `state rm`, `state list`).

---

### 🔄 05-CICD-Jenkins-Automation
* 📄 [`Jenkins_and_CICD_Master_Guide.md`](05-CICD-Jenkins-Automation/Jenkins_and_CICD_Master_Guide.md)
  * **Layer 1:** Distributed Controller-Agent architecture with dynamic ephemeral build agents.
  * **Layer 2:** Declarative vs Scripted pipeline architecture comparison.
  * **Layer 3:** SonarQube quality gate enforcement and Nexus artifact publishing.
  * **Layer 4:** Complete end-to-end Declarative Jenkinsfile blueprint (Checkout, Build, Scan, Publish, Containerize, Deploy).
  * **Layer 5:** Credentials management, Shared Libraries (`vars/`), and pipeline troubleshooting.

---

### 🐧 06-Linux-and-Git
* 📄 [`Linux_Master_Engineering_Guide.md`](06-Linux-and-Git/Linux_Master_Engineering_Guide.md)
  * Kernel vs User Space, Process creation (`fork`/`exec`), Zombie process table leaks vs Orphan re-parenting.
  * Octal permissions (`755`, `644`, `600`), SUID, SGID, and Sticky Bit.
  * Modern `systemd` service management and `journalctl` log inspection.
  * Modern networking tools: `ss -tulnp` (replacing legacy `netstat`), `ip addr`, `ip route`.
  * Performance diagnosis: Load averages, `free -h` available memory, and `iostat` disk saturation.
  * Production Bash strict mode template (`set -euo pipefail` with traps).
* 📄 [`Git_Master_Engineering_Guide.md`](06-Linux-and-Git/Git_Master_Engineering_Guide.md)
  * Git object model (Blobs, Trees, Commits, Tags).
  * The Three Trees (Working Directory, Staging Index, Repository).
  * `git merge` (non-linear with merge commit) vs `git rebase` (linear history with rewritten hashes).
  * Disaster recovery: Rescuing hard-reset commits via `git reflog` and detached HEAD recovery.
  * GitFlow branching governance and pull request policies.

---

### 🎯 07-Master-Interview-QnA
* 📄 [`640QA_Master_Systems_Engineering_Guide.md`](07-Master-Interview-QnA/640QA_Master_Systems_Engineering_Guide.md)
  * **The Master Encyclopedia:** All 640 questions and detailed technical answers spanning all 12 domains:
    1. AWS Cloud & Core Infrastructure (Q1–Q103)
    2. Azure Cloud & DevOps Essentials (Q104–Q147)
    3. Docker Containerization (Q148–Q218)
    4. Kubernetes Orchestration (Q219–Q304)
    5. Terraform Infrastructure as Code (Q305–Q339)
    6. Jenkins CI/CD Automation (Q340–Q367)
    7. Git Version Control & Workflow (Q368–Q410)
    8. Linux Systems Administration (Q411–Q485)
    9. Computer Networking & Protocols (Q486–Q553)
    10. Maven Build & Architecture (Q554–Q590)
    11. Cloud-Native & Observability (Q591–Q625)
    12. DevOps Scenarios & Incident Response (Q626–Q640)
* 📄 [`HANDS_ON_CODE_PRACTICE.md`](07-Master-Interview-QnA/HANDS_ON_CODE_PRACTICE.md)
  * Practice writing production code from memory without looking at notes (Multi-stage Dockerfile, Compose, Kubernetes Deployment/Service, Terraform S3/VPC, Declarative Jenkinsfile).
* 📄 [`DevOps_Interview_Quick_Cheatsheet.md`](07-Master-Interview-QnA/DevOps_Interview_Quick_Cheatsheet.md)
  * Rapid 10-minute revision sheet for the morning of technical interviews.
* 📄 [`Projects_Architecture_Cheatsheet.md`](07-Master-Interview-QnA/Projects_Architecture_Cheatsheet.md)
  * Deep-dive architectural talking points for your real-world resume projects.
* 📄 [`Taskflow_Full_Stack_DevOps_Project_Guide.md`](07-Master-Interview-QnA/Taskflow_Full_Stack_DevOps_Project_Guide.md)
  * Complete full-stack project case study (React, Node.js, MySQL, Docker Compose, CI/CD).

---

### 🔷 08-Azure-DevOps-Engineering
* 📄 [`Azure_DevOps_Master_Engineering_Guide.md`](08-Azure-DevOps-Engineering/Azure_DevOps_Master_Engineering_Guide.md)
  * **Layer 1:** Azure Boards Agile project governance (Epics, Features, User Stories, Tasks, Sprints).
  * **Layer 2:** Azure Repos branch policies (2 reviewers, work item linkage, build validation gates, squash merges).
  * **Layer 3:** Multi-stage production YAML pipeline (Build & Test stage -> Protected Environment deployment stage).
  * **Layer 4:** Self-Hosted Linux Agent Pool setup automation on Ubuntu with `systemd` service integration.
  * **Layer 5:** Apache reverse proxy configuration (`mod_proxy`, `ProxyPass`, SSL Let's Encrypt, WebSockets).
  * **Layer 6:** LGTM Observability stack (Loki log aggregator, Grafana dashboards, Tempo distributed tracing, Mimir metrics).
