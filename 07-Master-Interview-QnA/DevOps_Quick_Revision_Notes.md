# 📘 DevOps Quick Revision Notes

> *High-yield guide extracted from `DevOps Quick Revision Notes.pdf` for mobile & web GitHub viewing.*

---

## Section / Page 1

DevOps Quick Revision — Interview Ready
Read this in 15–30 minutes. Deep notes available in the full document.
1. AWS
IAM — Controls WHO can access WHAT in AWS
Users (permanent), Roles (temporary, for services), Policies (permissions)
Key principle: Least Privilege — give minimum access needed
EC2 — Virtual server in the cloud
Connect Linux: SSH with key pair | Connect Windows: RDP / Session Manager
AMI = Software config (OS + apps) | Launch Template = Hardware config
EBS — Block storage attached to EC2 (like external hard drive)
AZ-specific | Default: 8GB Linux, 30GB Windows | Backup via Snapshots
S3 — Object storage (files stored in buckets)
Global, bucket name must be unique | Max object size: 5TB
Classes: Standard → IA → One Zone-IA → Glacier → Deep Archive (cheapest)
Used for: backups, static websites, logs, big data
VPC — Your private network in AWS
Public Subnet → has Internet Gateway (internet access)
Private Subnet → no direct internet, uses NAT Gateway (outbound only)
Bastion Host → jump server to access private instances
Security Group vs NACL
Security Group: instance-level, stateful, allow only
NACL: subnet-level, stateless, allow + deny
Auto Scaling — Adds/removes EC2 based on demand
Min, Max, Desired capacity | Triggered by CloudWatch metrics
ALB vs NLB
ALB: Layer 7 (HTTP/HTTPS), path/host-based routing → microservices
NLB: Layer 4 (TCP/UDP), ultra-low latency → high performance
CloudWatch — AWS monitoring
4/14/26, 12:55 PM DevOps Quick Revision Notes
file:///C:/Users/anush/Downloads/Quick_Revision.html 1/9

## Section / Page 2

Metrics (CPU, memory) | Alarms (trigger actions) | Logs (app logs)
RDS vs DynamoDB — RDS: relational SQL | DynamoDB: NoSQL, auto-scales
Lambda — Serverless, runs code on events, no EC2 needed, pay per use
Cloud Models — IaaS (EC2), PaaS (Beanstalk), SaaS (Gmail)
2. Kubernetes
What is K8s? — Container orchestration: auto-healing, auto-scaling, load balancing, rolling updates
Architecture
Master: API Server, Scheduler, Controller Manager, etcd
Worker: kubelet, kube-proxy, container runtime (containerd)
Pod — Smallest unit, wraps one or more containers, shares IP
Deployment → manages ReplicaSets → manages Pods
Rolling update, rollback, version history
ReplicaSet — Ensures desired number of Pods always running
Services (3 types)
ClusterIP → internal only (Pod-to-Pod)
NodePort → external via node IP:port
LoadBalancer → external via cloud LB (creates AWS ELB)
Volumes
emptyDir → temporary, shared between containers in Pod (lost when Pod dies)
hostPath → mounts node directory into Pod
PV (PersistentVolume) → storage resource | PVC (Claim) → request for storage
ConfigMap — Non-sensitive config (env vars, files)
Secret — Sensitive data (passwords, keys) — base64 encoded
Namespace — Logical isolation (dev, staging, prod)
DaemonSet — One Pod per node (log collectors, monitoring agents)
StatefulSet vs Deployment
Deployment: random Pod names, stateless (web, API)
StatefulSet: stable identity (db-0, db-1), own PVC per Pod (databases)
RBAC — ServiceAccount (WHO) → Role/ClusterRole (WHAT) → RoleBinding (CONNECT)
HPA — Scales Pod count based on CPU/memory automatically
Ingress — HTTP router in front of multiple Services (path/host-based)
Deployment Strategies
4/14/26, 12:55 PM DevOps Quick Revision Notes
file:///C:/Users/anush/Downloads/Quick_Revision.html 2/9

## Section / Page 3

Recreate → downtime, kills all then creates
RollingUpdate → gradual, zero downtime (default)
Blue-Green → two environments, instant switch
Canary → small % first, then full rollout
Troubleshooting
CrashLoopBackOff → kubectl logs pod --previous  — app crashing
ImagePullBackOff → wrong image name or missing registry credentials
Pending → insufficient resources or PVC not bound
OOMKilled → increase memory limits
NodeNotReady → check kubelet, node disk/memory
Key Commands
kubectl get pods/nodes/svc/deploy
kubectl describe pod <name>
kubectl logs <pod> -f
kubectl exec -it <pod> -- bash
kubectl apply -f file.yaml
kubectl rollout undo deployment/<name>
kubectl scale deployment/<name> --replicas=5
3. Docker
Image — Read-only blueprint | Container — Running instance of image
Dockerfile Key Instructions
FROM (base image), RUN (build-time commands), COPY (copy files)
WORKDIR (set dir), EXPOSE (document port), CMD (start command)
ENTRYPOINT (fixed main command), ENV (env vars), ARG (build args)
Multi-stage build — Build in one stage, copy only artifacts to runtime stage → smaller image
Docker Networking
Bridge (default, same host) | Host (no isolation) | None (no network)
Overlay (multi-host, Swarm) | Macvlan (physical LAN)
Docker Volumes — Named volume (managed by Docker), Bind mount (host dir), tmpfs (memory)
Docker Compose — Run multi-container apps with one YAML file
docker-compose up -d  | docker-compose down  | docker-compose logs
VM vs Container — VM: full OS (GBs, minutes to start) | Container: shared kernel (MBs, seconds)
Key Commands
4/14/26, 12:55 PM DevOps Quick Revision Notes
file:///C:/Users/anush/Downloads/Quick_Revision.html 3/9

## Section / Page 4

docker build -t name:tag .
docker run -d -p 8080:80 --name app image
docker ps / docker ps -a
docker logs -f container
docker exec -it container bash
docker push repo/image:tag
docker volume create / ls / rm
docker network ls / create / inspect
4. Jenkins
What is Jenkins? — Open-source CI/CD automation server
Jenkinsfile — Pipeline as code (Groovy), stored in repo
Job Types — Freestyle (GUI), Pipeline (Jenkinsfile), Multibranch
Declarative vs Scripted — Declarative: modern, structured (use this) | Scripted: full Groovy flexibility
Triggers — Webhook (instant on push), Poll SCM, Schedule (cron), Manual
Pipeline Stages — Checkout → Build → Test → SonarQube → Nexus → Docker Build → Push → Deploy
Credentials — Store secrets in Jenkins (never hardcode in Jenkinsfile)
Master/Agent — Master orchestrates, Agents run the actual jobs
5. Git
4 Areas — Working Dir → Staging (git add) → Local Repo (git commit) → Remote (git push)
Key Commands
git init / git clone <url>
git add . / git commit -m "msg"
git push origin branch / git pull origin main
git branch -b feature / git switch -c feature
git merge feature / git rebase main
git stash / git stash pop
git log --oneline --graph
git reset --soft/--mixed/--hard HEAD~1
git revert <commit-id>
git cherry-pick <commit-id>
Merge vs Rebase — Merge: preserves history | Rebase: clean linear history (never rebase shared branches)
PR Workflow — Feature branch → Push → PR → Review → Approve → Merge → Delete branch
Branching Strategies — GitFlow (main/develop/feature) | GitHub Flow (main + short-lived branches)
4/14/26, 12:55 PM DevOps Quick Revision Notes
file:///C:/Users/anush/Downloads/Quick_Revision.html 4/9

## Section / Page 5

Reset types — --soft  keeps changes staged | --mixed  keeps in working dir | --hard  deletes everything
6. Linux
File System — /etc  configs | /var/log  logs | /home  users | /tmp  temp | /opt  apps
Permissions — rwx  = 4+2+1 | chmod 755 file  | chown user:group file
755 = owner full, group+others read+execute | 644 = owner read+write, others read
User Management
useradd -m user / userdel -r user
passwd user / usermod -aG docker user
groups user / id user
Process Management
ps aux | grep process
top / htop
kill -9 PID / pkill name
systemctl start/stop/restart/status/enable service
File Commands
ls -la / pwd / cd / mkdir -p / rm -rf
cp -r / mv / cat / tail -f / head -n 20
grep -r "pattern" / grep -i / grep -v
find / -name "*.log" / find . -type f -mtime -7
chmod / chown / setfacl -m u:user:rwx file
Networking
ip addr / ping / curl / ss -tulpn
ufw allow 22 / ufw enable
ssh -i key.pem user@ip / scp file user@ip:/path
Piping & Redirection
cmd > file  (overwrite) | cmd >> file  (append) | cmd 2>&1  (stderr to stdout)
cmd | grep pattern | wc -l  (pipe chain)
Add Volume to EC2 — lsblk → mkfs.ext4 /dev/xvdf → mkdir /data → mount /dev/xvdf /data → add to
/etc/fstab
4/14/26, 12:55 PM DevOps Quick Revision Notes
file:///C:/Users/anush/Downloads/Quick_Revision.html 5/9

## Section / Page 6

7. Terraform
What is Terraform? — IaC tool (HashiCorp), declare desired state, Terraform creates it
Workflow — init → plan → apply → destroy
Key Files — main.tf  (resources), variables.tf  (inputs), outputs.tf  (outputs), terraform.tfvars
(values)
Key Commands
terraform init       # download providers
terraform plan       # preview changes
terraform apply      # create infrastructure
terraform destroy    # delete all
terraform state list # see what exists
terraform output     # show outputs
terraform workspace new/select/list
Resource Block
resource "aws_instance" "web" {
  ami           = var.ami_id
  instance_type = "t2.micro"
}
Variables — declare in variables.tf , values in terraform.tfvars , reference as var.name
State — terraform.tfstate  tracks what exists → store in S3 for teams (remote state)
Workspaces — Separate state per environment (dev/staging/prod)
Modules — Reusable Terraform code (like functions), use once, reference everywhere
8. Azure DevOps
5 Services — Boards (plan) | Repos (code) | Pipelines (CI/CD) | Test Plans | Artifacts
Azure Boards Hierarchy — Epic → Feature → User Story → Task/Bug
Self-Hosted Agent Setup
Download agent → extract → ./config.sh → enter org URL + PAT → ./run.sh
Pool name: Default (NOT agent name)
YAML Pipeline Structure
trigger → pool → stages → jobs → steps → tasks
4/14/26, 12:55 PM DevOps Quick Revision Notes
file:///C:/Users/anush/Downloads/Quick_Revision.html 6/9

## Section / Page 7

Multi-stage Pipeline — Build → Test → Deploy (use dependsOn  + condition: succeeded() )
Variables — Inline | Pipeline UI | Variable Groups (Library) | Key Vault (secrets)
Environments + Approvals — Add human gate before production deployment
Your Project 1 (Tomcat) — git push → pipeline triggers → agent copies files → Tomcat serves app
Your Project 2 (Reverse Proxy + LGTM)
Apache → routes /project1 to Tomcat1:7789, /project2 to Tomcat2:8888
LGTM: Promtail collects logs → Loki stores → Grafana visualizes
9. Ansible
What is Ansible? — Agentless config management, uses SSH, push-based, YAML playbooks
Key Concepts — Inventory (server list) | Playbook (tasks) | Module (pre-built action) | Role (reusable) | Handler
(runs on notify) | Vault (secrets)
Ad-hoc Commands
ansible all -m ping
ansible webservers -m shell -a "uptime"
ansible all -m apt -a "name=nginx state=present" --become
Playbook Structure
- name: Setup
  hosts: webservers
  become: yes
  tasks:
    - name: Install nginx
      apt: name=nginx state=present
      notify: Restart nginx
  handlers:
    - name: Restart nginx
      service: name=nginx state=restarted
Idempotent — Run same playbook 10 times = same result (won't break things)
10. Networking
OSI 7 Layers (top to bottom) — Application | Presentation | Session | Transport | Network | Data Link | Physical
Memory trick — "All People Seem To Need Data Processing"
Data names — Data | Data | Data | Segment | Packet | Frame | Bit
4/14/26, 12:55 PM DevOps Quick Revision Notes
file:///C:/Users/anush/Downloads/Quick_Revision.html 7/9

## Section / Page 8

TCP vs UDP
TCP: reliable, connection-oriented, ordered (HTTP, SSH, FTP)
UDP: fast, connectionless, no guarantee (DNS, streaming, gaming)
TCP 3-Way Handshake — SYN → SYN-ACK → ACK (establishes connection)
Key Protocols/Ports
SSH: 22   HTTP: 80    HTTPS: 443
FTP: 21   DNS: 53     SMTP: 25
RDP: 3389 MySQL: 3306 PostgreSQL: 5432
DNS — Translates domain names to IP addresses (A record, CNAME, MX, TXT)
DHCP DORA — Discover → Offer → Request → Acknowledge (auto-assigns IP)
IPv4 vs IPv6 — IPv4: 32-bit, 4.3B addresses | IPv6: 128-bit, 340 undecillion, built-in security
Private IP Ranges — 10.x.x.x | 172.16-31.x.x | 192.168.x.x
Devices — Hub: Layer 1 (broadcasts all) | Switch: Layer 2 (MAC-based) | Router: Layer 3 (IP-based)
NAT — Maps private IPs to public IP (PAT = multiple private → one public using ports)
VLAN — Logical network segmentation on a switch (reduces broadcast, improves security)
VPN — Encrypted tunnel over public internet for secure private communication
11. Your Project Explanations (Practice These!)
Project 1 — Kubernetes Multi-Tier App (AWS kOps)
"I containerized a Node.js backend and Apache frontend using Docker with separate Dockerfiles for isolation.
I provisioned a high-availability Kubernetes cluster on AWS using kOps, managing the full lifecycle. Frontend
was exposed via LoadBalancer Service, backend via ClusterIP, and they communicate using Kubernetes
internal DNS. For the PostgreSQL database I used a StatefulSet with PersistentVolume backed by AWS
EBS so data survives Pod restarts."
Project 2 — Azure DevOps CI/CD + Reverse Proxy + LGTM
"I set up two Tomcat instances on an Azure VM on ports 7789 and 8888, and configured Apache HTTP
Server as a Reverse Proxy to route /project1 and /project2 through a single Port 80 entry point. I automated
deployments using Azure DevOps CI/CD pipelines with a self-hosted agent running on the same VM. I
managed the project using Azure Boards with Epics and Features for full traceability and PR templates for
standardized code reviews. I also integrated the LGTM stack — Promtail, Loki, and Grafana — for real-time
log monitoring."
4/14/26, 12:55 PM DevOps Quick Revision Notes
file:///C:/Users/anush/Downloads/Quick_Revision.html 8/9

## Section / Page 9

Quick Interview Tips
When they ask "Tell me about yourself" — 90 seconds max, mention your 2 projects, end with enthusiasm
When you don't know something — "I haven't worked with that directly, but based on my experience with
[similar], I understand it works by..."
Always connect to your projects — Don't just define concepts, say "In my kOps project I used..."
Top 5 questions you WILL get:
1. Walk me through your CI/CD pipeline end to end
2. What happens when a Pod crashes in Kubernetes?
3. Difference between Docker and VM
4. How does Terraform manage state?
5. What is least privilege in IAM?
Study this sheet in 15-30 min → then open full notes for anything you need to go deeper
4/14/26, 12:55 PM DevOps Quick Revision Notes
file:///C:/Users/anush/Downloads/Quick_Revision.html 9/9

