# AKHIL'S DEVOPS PROJECTS - QUICK CHEAT SHEET

---

## PROJECT 1: AZURE DEVOPS + REVERSE PROXY + TOMCAT + LGTM

### ARCHITECTURE FLOW:
```
Developer pushes code to Azure Repo (main branch)
         ↓
Azure DevOps Pipeline triggers (self-hosted agent on same VM)
         ↓
Stage 1: BUILD
- Compile Java code
- Create WAR file
         ↓
Stage 2: TEST
- Run tests
         ↓
Stage 3: DEPLOY TO TOMCAT 1 (Port 7789)
- Copy WAR to /opt/tomcat1/webapps/
- Restart Tomcat 1
         ↓
Stage 4: DEPLOY TO TOMCAT 2 (Port 8888)
- Copy WAR to /opt/tomcat2/webapps/
- Restart Tomcat 2
         ↓
TRAFFIC FLOW:
User hits: http://your-vm-ip/project1
         ↓
Port 80 (Apache Reverse Proxy) receives request
         ↓
Apache reads ProxyPass config: /project1 → localhost:7789
         ↓
Forwards to Tomcat 1 (Port 7789)
         ↓
Tomcat processes, sends response back through Apache
         ↓
User gets response
```

### COMPONENTS:
- **Azure DevOps Boards:** Epics, Features, Tasks, Bug tracking
- **Azure DevOps Repos:** Git repository
- **Azure DevOps Pipelines:** YAML CI/CD pipeline
- **Self-hosted Agent:** Linux VM running pipeline jobs
- **Tomcat 1:** Port 7789 (isolated instance)
- **Tomcat 2:** Port 8888 (isolated instance)
- **Apache HTTP Server:** Port 80 (Reverse Proxy)
- **PostgreSQL:** Database (non-root user, encryption, backups)
- **UFW/Security Groups:** Only Port 80 exposed, internal ports hidden

### MONITORING (LGTM):
```
Promtail (Log Collector)
- Reads /opt/tomcat1/logs/catalina.out
- Reads /opt/tomcat2/logs/catalina.out
- Reads /var/log/apache2/access.log
         ↓
Loki (Log Storage)
- Stores all collected logs
         ↓
Grafana (Dashboard)
- Visualizes logs in real-time
- Create alerts
```

### KEY CONCEPTS:
✅ Context paths (single Tomcat) NOT scalable
✅ Separate instances = isolation, independent resources, security
✅ Reverse proxy routes traffic based on URL path
✅ Port 80 = public, Ports 7789/8888 = internal (UFW blocks them)
✅ Multi-stage pipeline = automated deployment to both instances
✅ LGTM = free monitoring (unlike CloudWatch which is paid)

### WHAT HAPPENS WHEN:
- **Code pushed** → Pipeline auto-triggers → Builds → Tests → Deploys to both Tomcats
- **Tomcat 1 crashes** → User gets error page (needs health checks + failover)
- **Need to restart Tomcat 1** → Only Project 1 affected, Project 2 keeps running
- **Need to monitor** → Check Grafana dashboard for logs/metrics

---

## PROJECT 2: KUBERNETES CLUSTER ON AWS USING KOPS

### ARCHITECTURE FLOW:
```
Step 1: SETUP KOPS
- Create EC2 instance (t2.medium, 8GB RAM)
- Give it IAM permissions to create AWS resources
- Install kOps on this EC2
         ↓
Step 2: CREATE CLUSTER
- Run: kops create cluster --name=myapp.k8s.local --zones=us-east-1a
- This CREATES but doesn't START yet
         ↓
Step 3: UPDATE CLUSTER
- Run: kops update cluster --name=myapp.k8s.local --yes
- This STARTS the cluster creation
- kOps creates: Master nodes, Worker nodes, VPC, Security Groups, Load Balancers
         ↓
Step 4: VALIDATE CLUSTER
- Run: kops validate cluster
- Check if cluster is healthy
         ↓
CLUSTER CREATED: 1 Master node + 2 Worker nodes
         ↓
Step 5: CONTAINERIZE APPLICATION
- Node.js backend → Dockerfile
- Apache frontend → Dockerfile
- Multi-Dockerfile approach (separate images)
         ↓
Step 6: PUSH IMAGES
- Push both images to container registry (ECR on AWS)
         ↓
Step 7: DEPLOY TO KUBERNETES
- Create Deployment manifests for frontend (3 replicas)
- Create Deployment manifests for backend (3 replicas)
- Create StatefulSet manifest for database (3 replicas)
- Apply manifests: kubectl apply -f manifest.yaml
         ↓
TRAFFIC FLOW:
User hits: http://your-loadbalancer-ip/
         ↓
AWS LoadBalancer (external)
         ↓
Frontend Service (LoadBalancer type)
         ↓
Frontend pods (3 replicas - round-robin load balanced)
         ↓
Frontend pod needs data → Calls backend
- URL: http://backend.default.svc.cluster.local:3000/api/todos
- Uses Kubernetes internal DNS
         ↓
Backend Service (ClusterIP type - internal only)
         ↓
Backend pods (3 replicas - round-robin load balanced)
         ↓
Backend needs to store/fetch data → Calls database
- URL: postgres.default.svc.cluster.local:5432
         ↓
Database Service (ClusterIP type)
         ↓
StatefulSet database pods
- postgres-0 (primary, writes to EBS volume in AZ-1a)
- postgres-1 (replica)
- postgres-2 (replica)
         ↓
Response flows back: Database → Backend → Frontend → User
```

### KUBERNETES RESOURCES CREATED:
```
Master Node (Control Plane):
- kube-apiserver (API)
- etcd (database for cluster state)
- kube-scheduler (decides which pod goes on which node)
- kube-controller-manager (runs controllers)

Worker Nodes (2 of them):
- kubelet (node agent)
- kube-proxy (networking)
- container runtime (Docker/containerd)

Deployments:
- frontend-deployment (3 replicas)
- backend-deployment (3 replicas)

StatefulSet:
- database-statefulset (3 replicas)

Services:
- frontend-service (LoadBalancer - external IP)
- backend-service (ClusterIP - internal DNS)
- database-service (ClusterIP - internal DNS)

PVC/PV (Persistent Storage):
- database-pvc (requests EBS volume)
- PV automatically created from EBS
```

### KEY CONCEPTS:
✅ kOps = automates Kubernetes cluster creation on AWS
✅ Master node = control plane (manages cluster)
✅ Worker nodes = run your pods
✅ Deployment = for stateless apps (frontend, backend)
✅ StatefulSet = for stateful apps (database with persistent storage)
✅ LoadBalancer Service = external access (public IP)
✅ ClusterIP Service = internal access (DNS-based)
✅ Round-robin = distributes requests evenly across pod replicas
✅ Persistent Volume = storage that survives pod restarts
✅ StatefulSet stable identity = postgres-0 always reconnects to same volume

### WHAT HAPPENS WHEN:
- **Pod crashes** → Kubernetes auto-restarts it (self-healing)
- **Traffic increases** → Manually scale: kubectl scale deployment frontend --replicas=5
- **Code updated** → kubectl set image deployment/backend backend=myimage:v2 (rolling update)
- **Need to rollback** → kubectl rollout undo deployment/backend
- **Database data lost** → StatefulSet reconnects to persistent volume, data is there
- **Entire AZ fails** → EBS becomes inaccessible (needs EFS or multi-AZ setup)

### LIMITATIONS IN YOUR PROJECT:
❌ EBS is AZ-specific (not multi-AZ resilient)
❌ Single master node (not HA - needs 3 masters for production)
❌ No auto-scaling (had to manually scale pods)
❌ No database replication set up (all 3 pods write to same volume)

### IMPROVEMENTS FOR PRODUCTION:
✅ Use EFS instead of EBS (multi-AZ)
✅ Multi-master setup (3 masters for HA)
✅ Enable cluster autoscaling (pods scale automatically)
✅ Set up master-slave database replication
✅ Use AWS Elastic Load Balancer (better integration)

---

## PROJECT 3: LGTM MONITORING STACK

### FLOW:
```
Promtail Installation (on same VM as Apache/Tomcat):
- Installed on server where logs are generated
- Configured with paths to read:
  * /var/log/apache2/access.log
  * /opt/tomcat1/logs/catalina.out
  * /opt/tomcat2/logs/catalina.out
         ↓
Log Collection:
- Promtail continuously watches these files
- Every new log line is captured
- Adds labels to logs (app=tomcat, service=backend, etc.)
         ↓
Send to Loki:
- Promtail sends logs to Loki (usually localhost:3100)
- Loki stores logs with timestamp + labels
         ↓
Loki (Log Storage):
- Stores logs efficiently
- Compresses old logs
- Indexes logs for fast searching
         ↓
Grafana Dashboard:
- Queries Loki: "Show me all ERROR logs from last hour"
- Displays results in dashboard
- Create alerts: "If error rate > 10%, send email"
         ↓
Monitoring:
- Real-time log visualization
- Search logs by keyword, timestamp, label
- Create graphs and dashboards
```

### LGTM COMPONENTS EXPLAINED:
```
Grafana = Frontend (Dashboard/UI)
  ├─ What it does: Display data visually
  ├─ What it queries: Loki, Mimir, Tempo
  └─ Use cases: Dashboards, alerts, graphs

Loki = Log Storage
  ├─ What it does: Store and index logs
  ├─ How data enters: Via Promtail
  └─ Use cases: Log searching, filtering, analysis

Promtail = Log Collector
  ├─ What it does: Read log files, send to Loki
  ├─ Installed on: Every server generating logs
  └─ Use cases: Apache logs, Tomcat logs, application logs

Mimir = Metrics Storage (optional in your project)
  ├─ What it does: Store CPU%, memory%, request count, etc.
  ├─ How data enters: Via Prometheus scraper
  └─ Use cases: System monitoring, performance analysis

Tempo = Traces Storage (optional in your project)
  ├─ What it does: Store distributed traces (request journey)
  ├─ How data enters: Via application instrumentation
  └─ Use cases: Request latency, bottleneck identification
```

### WHY LOKI INSTEAD OF CLOUDWATCH?
```
LOKI:
✅ Open source (FREE)
✅ Self-hosted (you control it)
✅ Works with ANY platform (AWS, Azure, on-premise, K8s)
✅ Lightweight
✅ Good for small to medium workloads

CLOUDWATCH:
❌ AWS-only (locked in)
❌ Paid service (costs money)
❌ Limited to AWS resources
✅ Better integration with AWS services
✅ More features (if you're all-in on AWS)

YOUR CHOICE: Loki (because you were on Azure + AWS mixed)
```

### MONITORING FLOW IN YOUR PROJECT:
```
Your applications (Apache, Tomcat)
         ↓
Generate logs (access.log, catalina.out)
         ↓
Promtail reads these files
         ↓
Promtail sends to Loki (Port 3100)
         ↓
You open Grafana (web browser)
         ↓
Grafana connects to Loki
         ↓
You create dashboard to visualize logs
         ↓
You see:
- Error messages
- Access patterns
- Performance issues
- Alerts (if configured)
```

---

## QUICK COMPARISON TABLE

| Aspect | Project 1 (Tomcat) | Project 2 (K8s) | Project 3 (LGTM) |
|--------|-------------------|-----------------|-----------------|
| **Infrastructure** | Single Azure VM | AWS K8s cluster | Monitoring |
| **Scaling** | Manual (add Tomcat) | Auto (via Deployment) | Not applicable |
| **High Availability** | No (single VM) | Yes (multiple nodes) | Not applicable |
| **Deployment** | Azure Pipeline | kubectl apply | Not applicable |
| **Database** | PostgreSQL on VM | PostgreSQL in K8s | N/A |
| **Main Benefit** | Simple, isolated apps | Scalable, resilient | Visibility |

---

## INTERVIEW ANSWERS (QUICK VERSION)

### Why your projects?
"I built these to learn enterprise DevOps patterns:
- **Project 1:** How to isolate and secure multiple applications on shared infrastructure
- **Project 2:** How to scale and manage containerized apps in production
- **Project 3:** How to monitor everything in real-time"

### Your strengths:
✅ Built actual projects (not just theory)
✅ Understands architecture patterns (isolation, scaling, monitoring)
✅ Hands-on with tools (Azure DevOps, Kubernetes, LGTM)
✅ Knows why certain choices (why StatefulSet, why Loki, why reverse proxy)

### Your gaps:
⚠️ Didn't implement full automation in Project 1
⚠️ Didn't handle multi-AZ resilience in Project 2
⚠️ Didn't implement metrics/traces in Project 3

### What you'd improve:
✅ Health checks + automatic failover in Project 1
✅ EFS for multi-AZ in Project 2
✅ Full LGTM stack with Mimir + Tempo in Project 3

---

## COMMON INTERVIEW QUESTIONS ABOUT YOUR PROJECTS

**Q: Walk me through Project 1**
A: "I deployed 2 isolated Tomcat instances (7789, 8888) behind an Apache reverse proxy on port 80. An Azure DevOps pipeline automates deployment. Loki + Grafana monitors the system."

**Q: Why not just use context paths?**
A: "Context paths share a single Java process. If one crashes, all go down. Separate instances isolate failures and allow independent scaling."

**Q: Walk me through Project 2**
A: "I provisioned a Kubernetes cluster on AWS using kOps with master + worker nodes. I deployed a Todo app with Node.js backend and Apache frontend (3 replicas each), PostgreSQL database (StatefulSet), and Kubernetes services for networking."

**Q: Why StatefulSet for database?**
A: "StatefulSet maintains stable pod identities. When a pod restarts, it reconnects to the same persistent volume, preventing data loss. Deployment would lose data."

**Q: What would you improve?**
A: "In Project 1, I'd add health checks + automatic failover. In Project 2, I'd use EFS instead of EBS for multi-AZ resilience and implement master-slave database replication."

---

## QUICK REFERENCE - TECHNICAL TERMS

```
ISOLATION = Separate processes/resources
REDUNDANCY = Multiple copies for failover
HIGH AVAILABILITY = System keeps running even if parts fail
SCALABILITY = Can handle more load by adding resources
LOAD BALANCING = Distribute requests evenly
SERVICE DISCOVERY = Automatic finding of services (DNS)
PERSISTENT STORAGE = Data survives pod/container restarts
SELF-HEALING = Automatic restart of failed components
IDEMPOTENCY = Running same operation multiple times = same result
DECLARATIVE = You describe WHAT, system handles HOW
```

---

## STUDY THIS AND YOU'RE READY! 💪

This cheat sheet covers:
✅ All 3 projects end-to-end
✅ Architecture flows
✅ Key concepts
✅ Interview answers
✅ What to improve
✅ Common questions

**Print this. Read it daily. By the end of next week, you'll have it memorized.**

Good luck, Akhil! 🚀
