# ⚡ DevOps & Cloud Engineering: Quick Revision Cheatsheet

> **Rapid 10-Minute High-Yield Study Guide for Day-of-Interview Revision**  
> Covers High-Probability Architectural Differentiators, Tricky Conceptual Comparisons, and Core Talking Points.

---

## 🚀 1. The Core Differentiators (Top Interview Traps)

| Concept A | Concept B | The Killer Technical Answer |
| :--- | :--- | :--- |
| **`CMD`** | **`ENTRYPOINT`** | `ENTRYPOINT` sets the immutable base binary (e.g. `python app.py`). `CMD` provides default flags (e.g. `--port 8000`) that the CLI user can override at runtime. |
| **`COPY`** | **`ADD`** | `COPY` does a strict local byte-for-byte file copy (best practice). `ADD` auto-extracts local `.tar.gz` archives and downloads remote URLs (security risk). |
| **`LivenessProbe`** | **`ReadinessProbe`** | `LivenessProbe` failure **restarts/kills** the container (heals deadlocks). `ReadinessProbe` failure **removes pod from Service endpoints** (zero downtime; container stays alive). |
| **`Security Group`** | **`NACL`** | Security Groups are **stateful** and operate at the ENI/instance level. NACLs are **stateless** (require ephemeral port rules) and operate at the subnet boundary. |
| **`RDS Multi-AZ`** | **`Read Replica`** | Multi-AZ is **synchronous** failover for **Disaster Recovery** (standby instance is hidden). Read Replicas are **asynchronous** log-shipping for **read scaling** (active queries). |
| **`git merge`** | **`git rebase`** | `merge` preserves chronological non-linear history with a merge commit. `rebase` rewrites commit hashes into a linear history (Never rebase public branches!). |
| **`git fetch`** | **`git pull`** | `fetch` only downloads commits to remote tracking branches (`origin/main`). `pull` runs `fetch` followed immediately by `merge`. |
| **`ss`** | **`netstat`** | `netstat` is deprecated and reads slow `/proc/net`. `ss` communicates directly with Linux kernel Netlink sockets ($10\times$ faster). |
| **EBS `gp3`** | **EBS `gp2`** | `gp3` delivers baseline 3,000 IOPS and 125 MB/s throughput independently of volume size at 20% lower cost. `gp2` IOPS scale strictly with volume size. |

---

## ☸️ 2. Kubernetes Troubleshooting Sequence
1. **`kubectl get pods -o wide`** ➔ Identify crashing pods and node location.
2. **`kubectl describe pod <name>`** ➔ Check `Events:` at the bottom (shows OOMKilled, ImagePullBackOff, failed probes, scheduler predicates).
3. **`kubectl logs <name> --previous`** ➔ View logs of the container instance that just crashed.
4. **`kubectl exec -it <name> -- sh`** ➔ Check internal network connectivity and env variables (`nc -zv <db-service> 5432`).

---

## ☁️ 3. AWS Network Troubleshooting Sequence
If a private EC2 instance cannot connect to the internet:
1. Verify the Private Subnet Route Table has `0.0.0.0/0 -> nat-xxxxxxxx`.
2. Verify the NAT Gateway is physically deployed inside a **Public Subnet**.
3. Verify the Public Subnet Route Table has `0.0.0.0/0 -> igw-xxxxxxxx`.
4. Verify Outbound Security Group allows port 443/80.
5. Verify Subnet NACLs allow outbound traffic and inbound return traffic on **Ephemeral Ports (1024–65535)**.

---

## 🏗️ 4. Terraform State Golden Rules
1. **Always use Remote State** with S3 versioning and DynamoDB locking (`LockID` primary key).
2. **Stuck state lock?** Run `terraform force-unlock <LOCK_ID>`.
3. **Manual console changes (Drift)?** Run `terraform plan` to view drift; `terraform apply` to overwrite and reconcile.
4. **Delete from code without destroying cloud infra?** Run `terraform state rm <resource_address>`.

---

## 🔷 5. Azure DevOps Golden Rules
1. **Never use static credentials in pipelines:** Use Service Connections with Workload Identity Federation or Managed Identities.
2. **Protect `main` branch:** Require 2 reviewers, PR work item linkage, and successful Build Validation pipeline.
3. **Self-Hosted Agents:** Run as persistent `systemd` service on private Linux VMs for fast caching and private VNet network access.
