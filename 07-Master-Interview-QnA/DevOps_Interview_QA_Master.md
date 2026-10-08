# DevOps Interview Preparation — Akhil B M
> Complete master document. All topics in one place. No redundancy.

---

## TABLE OF CONTENTS
1. [AWS Core Concepts](#section-1-aws)
2. [Kubernetes — Complete Guide](#section-2-kubernetes)
3. [Docker — Complete Guide](#section-3-docker)
4. [Jenkins — Complete Guide](#section-4-jenkins)
5. [Git — Complete Guide](#section-5-git)
6. [Linux — Complete Guide](#section-6-linux)

---
# SECTION 1: AWS CORE CONCEPTS

## Q1. What is IAM and why does it matter in DevOps?

**Answer:**
IAM (Identity and Access Management) is AWS's service for managing who can access what in your AWS environment. You create users or groups and assign them specific permissions to particular services like EC2 or S3.

The key principle is **least privilege** — you only give users the minimum access they actually need. This is crucial for security in DevOps environments where multiple team members need different levels of access.

**Key points to mention:**
- Create users, groups, and roles
- Attach policies to control access
- Principle of least privilege
- IAM roles can be assigned to EC2 instances (so apps can access AWS services without hardcoded credentials)

---

## Q2. What is the difference between IAM User and IAM Role?

**Answer:**
- **IAM User** — a permanent identity for a person. Has long-term credentials (username/password or access keys). Used for people who need permanent access.
- **IAM Role** — a temporary identity without credentials. A service or user assumes a role and gets temporary access keys for a specific task.

**DevOps use case:** Assign roles to EC2 instances so they can access S3 or DynamoDB without storing credentials inside the instance. Lambda functions also use roles to access other AWS services.

---

## Q3. What is the difference between Availability Zones and Regions?

**Answer:**
- **Region** — a completely separate geographic area with its own infrastructure (e.g., US East, Europe West, Asia Pacific)
- **Availability Zone (AZ)** — isolated data centers within a region. If one AZ goes down, your app in another AZ stays up.

**Why it matters for DevOps:**
- Deploy across multiple AZs for high availability
- Use multiple regions for disaster recovery
- Auto Scaling groups and Load Balancers automatically distribute across AZs

---

## Q4. What is the difference between a Security Group and a Network ACL?

**Answer:**

| Feature | Security Group | Network ACL |
|---|---|---|
| Level | Instance level | Subnet level |
| State | Stateful | Stateless |
| Rules | Allow only | Allow and Deny |
| Use case | Most common, day-to-day | Broad subnet-wide rules |

- **Stateful** — allow inbound, response goes out automatically
- **Stateless** — must define both inbound and outbound rules separately

**In practice:** Security Groups are used most of the time in DevOps.

---

## Q5. What is an Auto Scaling Group and why does a DevOps engineer care?

**Answer:**
An Auto Scaling Group automatically adds or removes EC2 instances based on demand. You define:
- **Minimum instances** — always running
- **Maximum instances** — cap on scaling
- **Desired capacity** — normal state
- **Scaling policies** — based on CloudWatch metrics like CPU usage

**Why DevOps cares:**
- Maintains performance during high traffic without manual intervention
- Reduces costs during low traffic by terminating unused instances
- Ensures high availability by replacing unhealthy instances automatically

---

## Q6. What is the difference between ALB and NLB?

**Answer:**

| Feature | ALB (Layer 7) | NLB (Layer 4) |
|---|---|---|
| OSI Layer | Layer 7 (Application) | Layer 4 (Transport) |
| Routing | Path-based, host-based | IP and port-based |
| Use case | Microservices, web apps | High performance, low latency |
| Protocol | HTTP/HTTPS | TCP/UDP |

- **ALB** — looks inside your request, routes based on path or hostname. Use for microservices.
- **NLB** — moves data super fast without inspecting it. Use for extreme speed needs.

**In practice:** Most DevOps teams use ALB for web applications.

---

## Q7. What is CloudWatch and how do you use it in DevOps?

**Answer:**
CloudWatch is AWS's native monitoring and observability service. It does three main things:

1. **Metrics** — tracks CPU, memory, network, disk usage of EC2, RDS, and other AWS services
2. **Alarms** — set thresholds so if CPU goes above 80%, it triggers an alert or Auto Scaling event
3. **Logs** — stream and search application and system logs for debugging

**In DevOps context:**
- Set alarms to trigger Auto Scaling
- Monitor pipeline health
- Debug application errors via log groups
- Create dashboards for visibility

> **Note for Akhil:** In your Azure DevOps project, you used the **LGTM stack (Loki, Grafana, Tempo, Mimir)** — this is essentially an open-source alternative to CloudWatch. Mention this in interviews to show broader monitoring experience.

---

## Q8. What is the difference between RDS and DynamoDB?

**Answer:**

| Feature | RDS | DynamoDB |
|---|---|---|
| Type | Relational (SQL) | NoSQL (key-value) |
| Schema | Fixed schema | Flexible schema |
| Scaling | Vertical (mostly) | Horizontal (automatic) |
| Use case | Structured data, complex queries | High-speed, large-scale, simple queries |
| Examples | MySQL, PostgreSQL, Aurora | Session data, IoT, gaming leaderboards |

> **Note for Akhil:** You worked with **PostgreSQL** (RDS equivalent) in your project. Mention that directly.

---

## Q9. What is S3 and how does it differ from EBS?

**Answer:**
- **S3 (Simple Storage Service)** — stores data as objects (files) in buckets. Cheap, infinitely scalable, accessed over HTTP. Used for backups, logs, artifacts, static assets.
- **EBS (Elastic Block Store)** — block storage directly attached to EC2 instances. Faster because it's directly connected. Used for databases and applications needing fast disk access.

**Use S3 for:** Storing Docker images, artifacts, logs, backups
**Use EBS for:** Database storage, OS volumes on EC2

---

## Q10. What is a VPC and why is it important for DevOps?

**Answer:**
A VPC (Virtual Private Cloud) is your own isolated network in AWS. You control:
- Subnets (public and private)
- Routing tables
- Internet Gateways
- Security Groups and ACLs
- Traffic flow between resources

**DevOps use:** Create a VPC with public subnets for load balancers and private subnets for databases. Control who can access what.

---

## Q11. What is the difference between a Public Subnet and a Private Subnet?

**Answer:**
- **Public Subnet** — has a route to an Internet Gateway. Instances here can be reached from the internet. Used for load balancers, bastion hosts.
- **Private Subnet** — no direct route to the internet. Instances here can't be reached externally. Used for databases, application servers.

**Bastion Host** — a public EC2 instance you SSH into first, then jump to private instances. Acts as a secure entry point.

---

## Q12. What is an Elastic IP?

**Answer:**
An Elastic IP is a static public IP address that stays attached to your instance even if you stop and restart it. Regular public IPs change when you stop an instance. Elastic IPs are assigned by AWS — you can't choose the specific number, but once assigned, it stays the same as long as you keep it.

**Use for:** Web servers, databases, or anything that needs a consistent IP address.

---


---
# SECTION 2: KUBERNETES — COMPLETE GUIDE

> Flow: Why Kubernetes → Architecture → Core Objects → Storage → Networking → Security → Advanced → Troubleshooting

---

## 1. Drawbacks of Docker (Standalone)

When you run Docker alone without any orchestration, you face these problems:

| Problem | Description |
|---|---|
| **No Auto-healing** | If a container crashes, it stays dead. You manually restart it. |
| **No Auto-scaling** | Can't automatically add more containers when load increases |
| **No Load Balancing** | No built-in way to distribute traffic across containers |
| **Single Host** | Docker runs on one machine — no clustering out of the box |
| **No Rolling Updates** | No way to update containers without downtime |
| **No Self-healing** | No health checks that restart unhealthy containers |
| **Complex Networking** | Connecting containers across multiple hosts is hard |
| **No Storage Management** | Volumes are manual and host-dependent |
| **No Secret Management** | No built-in secure way to manage passwords/keys |

---

## 2. Docker Swarm — Overcoming Docker's Drawbacks

Docker Swarm is Docker's native clustering tool. It groups multiple Docker hosts into a single virtual host.

**What Swarm adds over plain Docker:**
- Multi-host container management
- Basic load balancing
- Simple scaling (`docker service scale`)
- Basic rolling updates
- Service discovery

**But Swarm has its own limitations:**

| Docker Swarm Limitation | Kubernetes Solution |
|---|---|
| Limited auto-scaling (no CPU-based HPA) | Full HPA based on CPU/memory/custom metrics |
| Basic health checks | Liveness + Readiness + Startup probes |
| No built-in secrets encryption | Encrypted secrets, integration with Vault |
| Limited storage options | PV, PVC, StorageClass, dynamic provisioning |
| No RBAC | Full RBAC with roles and bindings |
| Small ecosystem | Massive ecosystem, CNCF projects |
| Less active development | Industry standard, massive community |
| No CRDs | Custom Resource Definitions to extend K8s |
| Basic networking | CNI plugins, Network Policies |
| No namespace isolation | Full namespace support with quotas |

---

## 3. What is Kubernetes?

**Definition:**
Kubernetes (K8s) is an open-source container orchestration platform originally created by Google, now maintained by the CNCF (Cloud Native Computing Foundation). It automates the deployment, scaling, and management of containerized applications.

**Key Features:**
- **Auto-healing** — restarts failed containers automatically
- **Auto-scaling** — HPA scales pods based on CPU/memory
- **Load Balancing** — distributes traffic across pods
- **Rolling Updates** — zero-downtime deployments
- **Self-healing** — replaces failed nodes/pods
- **Storage Orchestration** — automatically mounts storage
- **Secret & Config Management** — secure handling of sensitive data
- **Service Discovery** — built-in DNS for pod communication
- **Multi-cloud** — runs on AWS, Azure, GCP, on-premise
- **Declarative** — you define desired state, K8s makes it happen

**Why Kubernetes > Docker Swarm:**
- Industry standard (used by Google, Netflix, Airbnb)
- Much richer feature set
- Better auto-scaling
- Full RBAC
- Huge ecosystem (Helm, Istio, Argo, Prometheus)
- Better storage management
- More active development

---

## 4. Kubernetes Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    CONTROL PLANE (Master)                │
│                                                         │
│  ┌──────────────┐  ┌───────────────┐  ┌─────────────┐  │
│  │  API Server  │  │   Scheduler   │  │  Controller │  │
│  │  (Front door)│  │ (Assigns pods │  │  Manager    │  │
│  │              │  │  to nodes)    │  │  (Watches   │  │
│  └──────────────┘  └───────────────┘  │  state)     │  │
│                                       └─────────────┘  │
│  ┌──────────────────────────────────────────────────┐   │
│  │           etcd (Cluster Database)                │   │
│  │    Stores ALL cluster state and configuration    │   │
│  └──────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                          │
              kubectl commands → API Server
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
┌───────▼──────┐  ┌───────▼──────┐  ┌──────▼───────┐
│  Worker Node │  │  Worker Node │  │  Worker Node │
│              │  │              │  │              │
│  ┌─────────┐ │  │  ┌─────────┐ │  │  ┌─────────┐ │
│  │ kubelet │ │  │  │ kubelet │ │  │  │ kubelet │ │
│  └─────────┘ │  │  └─────────┘ │  │  └─────────┘ │
│  ┌─────────┐ │  │  ┌─────────┐ │  │  ┌─────────┐ │
│  │kube-    │ │  │  │kube-    │ │  │  │kube-    │ │
│  │proxy    │ │  │  │proxy    │ │  │  │proxy    │ │
│  └─────────┘ │  │  └─────────┘ │  │  └─────────┘ │
│  ┌─────────┐ │  │  ┌─────────┐ │  │  ┌─────────┐ │
│  │Container│ │  │  │Container│ │  │  │Container│ │
│  │Runtime  │ │  │  │Runtime  │ │  │  │Runtime  │ │
│  └─────────┘ │  │  └─────────┘ │  │  └─────────┘ │
│  [Pod][Pod]  │  │  [Pod][Pod]  │  │  [Pod][Pod]  │
└──────────────┘  └──────────────┘  └──────────────┘
```

### Control Plane Components

| Component | Role |
|---|---|
| **API Server** | Entry point for all commands (kubectl). Validates and processes requests. |
| **Scheduler** | Watches for unscheduled pods, assigns them to suitable worker nodes |
| **Controller Manager** | Runs controllers that maintain desired state (Deployment, ReplicaSet, Node controllers) |
| **etcd** | Distributed key-value store. Stores ALL cluster state. Source of truth. |

### Worker Node Components

| Component | Role |
|---|---|
| **kubelet** | Agent on each node. Receives pod specs from API server, ensures containers are running |
| **kube-proxy** | Manages network rules on nodes, handles Service networking and load balancing |
| **Container Runtime** | Runs containers — containerd, CRI-O (Docker was deprecated in K8s 1.24+) |

---

## 5. How kOps Creates a Kubernetes Cluster on AWS

**kOps (Kubernetes Operations)** — tool to provision, manage, and upgrade Kubernetes clusters on cloud providers.

```bash
# STEP 1 — Install kOps and kubectl
curl -Lo kops https://github.com/kubernetes/kops/releases/download/v1.28.0/kops-linux-amd64
chmod +x kops && sudo mv kops /usr/local/bin/

# STEP 2 — Create S3 bucket for kOps state store
aws s3 mb s3://akhil-kops-state-store
export KOPS_STATE_STORE=s3://akhil-kops-state-store

# STEP 3 — Create cluster config
kops create cluster \
  --name=mycluster.k8s.local \
  --state=s3://akhil-kops-state-store \
  --zones=us-east-1a,us-east-1b \
  --node-count=2 \
  --node-size=t3.medium \
  --master-size=t3.medium \
  --dns-zone=mycluster.k8s.local

# STEP 4 — Apply the cluster (actually creates AWS resources)
kops update cluster --name mycluster.k8s.local --yes --admin

# kOps automatically creates:
# - VPC, Subnets, Security Groups
# - EC2 instances for master and workers
# - IAM roles and policies
# - Route53 DNS records
# - ELB for API server
# - etcd on master nodes
# - Auto Scaling Groups for workers

# STEP 5 — Validate cluster is ready
kops validate cluster --wait 10m

# STEP 6 — Verify nodes
kubectl get nodes

# Common kOps operations
kops get clusters                          # list clusters
kops get ig                                # list instance groups
kops edit cluster mycluster.k8s.local      # edit cluster config
kops rolling-update cluster --yes          # apply changes
kops delete cluster --name=mycluster.k8s.local --yes  # delete cluster
```

---

## 6. Replication Controller vs ReplicaSet

### Replication Controller (Old — Deprecated)

**Definition:** Ensures a specified number of pod replicas are running at all times. If a pod dies, it creates a new one. If there are too many, it removes some.

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: rc1
spec:
  replicas: 3
  selector:
    app: myapp          # equality-based selector only
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: c1
        image: nginx
        ports:
        - containerPort: 80
```

### ReplicaSet (New — Use This)

**Definition:** Same as ReplicationController but supports **set-based selectors** (more powerful matching). Usually managed by a Deployment.

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: rs1
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp        # set-based selector
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: c1
        image: nginx
        ports:
        - containerPort: 80
```

### Differences

| Feature | ReplicationController | ReplicaSet |
|---|---|---|
| API version | v1 | apps/v1 |
| Selector type | Equality-based only | Set-based (matchLabels, matchExpressions) |
| Status | Deprecated | Current standard |
| Used by | Nothing (old) | Deployments |
| Direct use | Avoid | Avoid (use Deployments instead) |

### Commands

```bash
kubectl get rc                          # list replication controllers
kubectl get rs                          # list replica sets
kubectl describe rs rs1                 # details of replica set
kubectl scale rs rs1 --replicas=5       # scale replica set
kubectl delete rs rs1                   # delete replica set
```

---

## 7. Deployments — Complete Guide

**Definition:** A Deployment manages ReplicaSets and provides declarative updates. It's the standard way to run stateless applications.

```
Deployment → manages → ReplicaSet → manages → Pods
```

### Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dp1
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1          # max pods above desired during update
      maxUnavailable: 1    # max pods below desired during update
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: c1
        image: nginx:1.19
        ports:
        - containerPort: 80
        resources:
          requests:
            cpu: "250m"
            memory: "128Mi"
          limits:
            cpu: "500m"
            memory: "256Mi"
        livenessProbe:
          httpGet:
            path: /health
            port: 80
          initialDelaySeconds: 10
          periodSeconds: 5
        readinessProbe:
          httpGet:
            path: /ready
            port: 80
          initialDelaySeconds: 5
          periodSeconds: 3
```

### Deployment Commands

```bash
# Create / Apply
kubectl apply -f deployment.yaml              # create or update deployment
kubectl create deployment dp1 --image=nginx  # quick create

# View
kubectl get deployments                       # list deployments
kubectl get deploy                            # short form
kubectl describe deployment dp1               # detailed info
kubectl get pods -l app=myapp                 # pods of deployment

# Scale
kubectl scale deployment dp1 --replicas=5    # scale to 5 pods
kubectl autoscale deployment dp1 --min=2 --max=10 --cpu-percent=70  # HPA

# Update image
kubectl set image deployment/dp1 c1=nginx:1.20  # update container image

# Rollout management
kubectl rollout status deployment/dp1         # check rollout progress
kubectl rollout history deployment/dp1        # view revision history
kubectl rollout history deployment/dp1 --revision=2  # details of revision 2
kubectl rollout undo deployment/dp1           # rollback to previous version
kubectl rollout undo deployment/dp1 --to-revision=2  # rollback to revision 2
kubectl rollout pause deployment/dp1          # pause rollout
kubectl rollout resume deployment/dp1         # resume rollout

# Delete
kubectl delete deployment dp1                 # delete deployment
kubectl delete -f deployment.yaml             # delete from file

# Get deployment YAML
kubectl get deployment dp1 -o yaml            # view as YAML
kubectl get deployment dp1 -o json            # view as JSON
```

---

## 8. Kubernetes Services — 3 Types with YAML

**Definition:** A Service provides a stable network endpoint for a set of pods. Pods are ephemeral (IPs change), Services are stable.

### Type 1: ClusterIP (Internal Only)

```yaml
# clusterIP.yaml
apiVersion: v1
kind: Service
metadata:
  name: cip
spec:
  type: ClusterIP         # default type — internal access only
  selector:
    app: myapp
  ports:
  - port: 80              # Service port (what clients connect to)
    targetPort: 80        # Container port (where traffic goes)
```

```
Use when: Pod-to-Pod communication inside cluster
Access: Only from within the cluster
Example: Backend connecting to database
```

### Type 2: NodePort (External via Node IP)

```yaml
# nodeport.yaml
apiVersion: v1
kind: Service
metadata:
  name: np1
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
  - port: 80              # ClusterIP port
    targetPort: 80        # Container port
    nodePort: 31200       # Port on each node (30000-32767)
```

```
Use when: Need external access without cloud load balancer
Access: http://<node-ip>:31200
Example: Dev/test environments
```

### Type 3: LoadBalancer (Cloud Load Balancer)

```yaml
# loadbalancer.yaml
apiVersion: v1
kind: Service
metadata:
  name: lb1
spec:
  type: LoadBalancer
  selector:
    app: myapp
  ports:
  - port: 80
    targetPort: 80
    nodePort: 31200
```

```
Use when: Production, need external access with single endpoint
Access: Cloud provides external IP/DNS
Example: Production web app on AWS (creates ELB)
```

### Service Commands

```bash
kubectl get services                          # list services
kubectl get svc                               # short form
kubectl describe svc myservice                # service details
kubectl delete svc myservice                  # delete service
kubectl expose deployment dp1 --port=80 --type=LoadBalancer  # quick create
kubectl get endpoints                         # see which pods service routes to
```

### Pod + Service YAML (Combined)

```yaml
# backend-pod-and-service.yaml
apiVersion: v1
kind: Pod
metadata:
  name: backend-pod
  labels:
    app: backend
spec:
  containers:
  - name: backend
    image: node:18
    ports:
    - containerPort: 3000

---

apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  type: NodePort
  selector:
    app: backend          # matches pod label
  ports:
  - port: 80
    targetPort: 3000      # pod's container port
```

---

## 9. Namespaces

**Definition:** Namespaces logically partition a Kubernetes cluster into isolated environments. Resources in one namespace don't interact with another by default.

### Types of Namespaces

**Built-in namespaces:**

| Namespace | Purpose |
|---|---|
| `default` | Where resources go if you don't specify a namespace |
| `kube-system` | Kubernetes system components (API server, DNS, scheduler) |
| `kube-public` | Readable by all users, used for cluster info |
| `kube-node-lease` | Node heartbeat data (internal use) |

**Custom namespaces (you create these):**
- `dev` — development environment
- `staging` — staging environment
- `production` — production environment
- `monitoring` — Prometheus, Grafana

### Namespace YAML

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

### Namespace Commands

```bash
# Create
kubectl create namespace dev
kubectl apply -f namespace.yaml

# View
kubectl get namespaces                        # list all namespaces
kubectl get ns                                # short form
kubectl describe namespace dev               # details

# Use namespace
kubectl get pods -n dev                       # pods in dev namespace
kubectl get all -n kube-system               # all resources in kube-system
kubectl apply -f deployment.yaml -n dev       # deploy to dev namespace

# Set default namespace for session
kubectl config set-context --current --namespace=dev

# Delete
kubectl delete namespace dev                  # WARNING: deletes everything inside!

# Resource Quota per namespace
kubectl apply -f - <<EOF
apiVersion: v1
kind: ResourceQuota
metadata:
  name: dev-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "2"
    requests.memory: 4Gi
    limits.cpu: "4"
    limits.memory: 8Gi
EOF
```

---

## 10. Kubernetes Volumes — Complete Guide

### Volume Types Comparison

```
emptyDir    → Temporary, shared between containers in same pod, deleted when pod dies
hostPath    → Uses node's filesystem, persists beyond pod, tied to specific node
PV + PVC    → Fully persistent, independent of pods and nodes, production standard
ConfigMap   → Mount config files into pods
Secret      → Mount sensitive data into pods
```

### Type 1: emptyDir — Temporary Shared Volume

**Definition:** Created when a pod starts. Deleted when the pod is removed. Shared between all containers in the same pod. Used for caching, temporary processing.

```yaml
# emptydir-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dp1
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: c1
        image: httpd
        ports:
        - containerPort: 80
        volumeMounts:
        - name: v1
          mountPath: /usr/local/apache2/htdocs   # where volume appears in container
      volumes:
      - name: v1
        emptyDir: {}                              # empty, no source
```

```
Use when: Two containers in same pod need to share data temporarily
Example: Sidecar container processes logs before main container reads them
Lifecycle: Dies with the pod
```

### Type 2: hostPath — Node Filesystem Volume

**Definition:** Mounts a directory from the node's filesystem into the pod. Persists beyond pod restarts (as long as pod stays on same node). NOT recommended for production (node-specific).

```yaml
# hostpath-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dp1
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: c1
        image: httpd
        ports:
        - containerPort: 80
        volumeMounts:
        - name: v1
          mountPath: /usr/local/apache2/htdocs
      volumes:
      - name: v1
        hostPath:
          path: /home/centos/hostpath            # actual path on the node
          type: DirectoryOrCreate                # create if doesn't exist
```

```
Use when: DaemonSets collecting logs from node filesystem
Not for: Production databases (node-specific, not portable)
```

### Type 3: PersistentVolume (PV) + PersistentVolumeClaim (PVC)

**How it works:**

```
Admin creates PV ──→ Developer creates PVC ──→ Pod uses PVC
(actual storage)      (request for storage)
```

```yaml
# pv.yaml — Admin creates this (backed by AWS EBS)
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv1
spec:
  capacity:
    storage: 10Gi
  accessModes:
  - ReadWriteOnce                              # one node at a time
  persistentVolumeReclaimPolicy: Retain        # keep data after PVC deleted
  awsElasticBlockStore:
    volumeID: vol-xxxxxxxxxxxxxxxxx            # your actual EBS volume ID
    fsType: ext4
```

```yaml
# pvc.yaml — Developer creates this (requests 2Gi from available PVs)
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc1
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi                             # must be ≤ PV capacity
```

```yaml
# deployment-with-pvc.yaml — Pod uses PVC
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dp1
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: c1
        image: httpd
        ports:
        - containerPort: 80
        volumeMounts:
        - name: v1
          mountPath: /usr/local/apache2/htdocs
      volumes:
      - name: v1
        persistentVolumeClaim:
          claimName: pvc1                      # reference PVC by name
```

### Access Modes

| Mode | Description | Use case |
|---|---|---|
| ReadWriteOnce (RWO) | One node can read+write | Databases |
| ReadOnlyMany (ROX) | Many nodes can read | Shared config files |
| ReadWriteMany (RWX) | Many nodes can read+write | Shared file systems (NFS, EFS) |

### Reclaim Policies

| Policy | Meaning |
|---|---|
| Retain | Keep PV data after PVC deleted. Manual cleanup needed. |
| Delete | Delete PV and underlying storage when PVC deleted |
| Recycle | Wipe PV data and make available again (deprecated) |

### PV/PVC Commands

```bash
kubectl get pv                                # list persistent volumes
kubectl get pvc                               # list persistent volume claims
kubectl describe pv pv1                       # PV details
kubectl describe pvc pvc1                     # PVC details and binding status
kubectl delete pvc pvc1                       # delete PVC
kubectl get pvc -o wide                       # PVC with more info

# Check PVC status
# PENDING   = no matching PV found
# BOUND     = successfully bound to a PV
# LOST      = PV was deleted but PVC remains
```

---

## 11. DaemonSet

**Definition:** Ensures exactly ONE pod runs on EVERY node in the cluster. When a new node joins, DaemonSet automatically creates a pod there.

```yaml
# daemonset.yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: ds1
spec:
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: c1
        image: httpd
        ports:
        - containerPort: 80
```

```bash
kubectl get daemonsets                        # list daemonsets
kubectl get ds                                # short form
kubectl describe ds ds1                       # details
kubectl delete ds ds1                         # delete
```

```
Use for:
- Log collectors (Fluentd, Filebeat) — collect logs from every node
- Monitoring agents (Prometheus node-exporter) — metrics from every node
- Network plugins (CNI — Calico, Flannel) — networking on every node
- Security agents — run on every node
```

---

## 12. ConfigMap — Complete Guide

**Definition:** Stores non-sensitive configuration as key-value pairs. Injected into pods as environment variables or mounted as files.

### Imperative Way (Command line)

```bash
# Create from literal values
kubectl create configmap cm1 \
  --from-literal=app=myapp \
  --from-literal=env=production \
  --from-literal=port=8080

# Create from a file
kubectl create configmap cm1 --from-file=config.properties

# Create from env file
kubectl create configmap cm1 --from-env-file=.env

# View
kubectl get configmaps
kubectl get cm
kubectl describe cm cm1
kubectl get cm cm1 -o yaml
```

### Declarative Way (YAML)

```yaml
# configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: cm1
data:
  app: myapp
  environment: production
  port: "8080"
  config.properties: |       # multi-line file content
    db.host=localhost
    db.port=5432
    db.name=mydb
```

### Using ConfigMap in Deployment

**Method 1: As Environment Variables**

```yaml
spec:
  containers:
  - name: c1
    image: httpd
    envFrom:
    - configMapRef:
        name: cm1            # inject ALL keys as env vars
```

**Method 2: Specific Key as Env Var**

```yaml
spec:
  containers:
  - name: c1
    image: httpd
    env:
    - name: APP_NAME         # env var name in container
      valueFrom:
        configMapKeyRef:
          name: cm1          # configmap name
          key: app           # key in configmap
```

**Method 3: Mount as File**

```yaml
spec:
  containers:
  - name: c1
    image: httpd
    volumeMounts:
    - name: cm-volume
      mountPath: /etc/config  # ConfigMap keys become files here
  volumes:
  - name: cm-volume
    configMap:
      name: cm1
```

---

## 13. Secrets — Complete Guide

**Definition:** Like ConfigMap but for sensitive data (passwords, API keys, tokens). Values are base64 encoded. Can be encrypted at rest.

### Imperative Way

```bash
# Create from literal
kubectl create secret generic s1 \
  --from-literal=username=admin \
  --from-literal=password=MySecretPass123

# Create from file
kubectl create secret generic s1 --from-file=credentials.txt

# Create TLS secret (for HTTPS)
kubectl create secret tls tls-secret \
  --cert=server.crt \
  --key=server.key

# Create Docker registry secret
kubectl create secret docker-registry regcred \
  --docker-server=docker.io \
  --docker-username=akhil \
  --docker-password=mypassword

# View secrets (values are base64 encoded)
kubectl get secrets
kubectl describe secret s1          # shows keys but NOT values
kubectl get secret s1 -o yaml       # shows base64 encoded values

# Decode a secret value
kubectl get secret s1 -o jsonpath='{.data.password}' | base64 --decode
```

### Declarative Way

```yaml
# secret.yaml
apiVersion: v1
kind: Secret
metadata:
  name: s1
type: Opaque              # generic secret type
data:
  username: YWRtaW4=      # base64 encoded value of "admin"
  password: TXlTZWNyZXRQYXNzMTIz  # base64 of "MySecretPass123"

# Encode values: echo -n "admin" | base64
# Decode values: echo "YWRtaW4=" | base64 --decode
```

### Using Secrets in Deployment

**Method 1: All keys as env vars**

```yaml
spec:
  containers:
  - name: c1
    image: httpd
    envFrom:
    - secretRef:
        name: s1
```

**Method 2: Specific key as env var**

```yaml
spec:
  containers:
  - name: c1
    image: httpd
    env:
    - name: DB_PASSWORD
      valueFrom:
        secretKeyRef:
          name: s1
          key: password
```

**Method 3: Mount as file**

```yaml
spec:
  containers:
  - name: c1
    image: httpd
    volumeMounts:
    - name: secret-volume
      mountPath: /etc/secrets
      readOnly: true
  volumes:
  - name: secret-volume
    secret:
      secretName: s1
```

---

## 14. RBAC — Role Based Access Control (Complete)

**Definition:** RBAC controls WHO can do WHAT in Kubernetes. It's how you manage access and permissions.

```
┌──────────────────────────────────────────────────────┐
│                   RBAC DIAGRAM                       │
│                                                      │
│  WHO?              WHAT?           WHERE?            │
│  ┌──────────┐     ┌──────────┐    ┌──────────────┐  │
│  │  User    │     │  Role    │    │  Namespace   │  │
│  │  Group   │────▶│ (rules)  │────▶  (limited)   │  │
│  │ Service  │     └──────────┘    └──────────────┘  │
│  │ Account  │                                        │
│  └────┬─────┘     ┌─────────────┐  ┌─────────────┐  │
│       │           │ ClusterRole │  │   Cluster   │  │
│       └──────────▶│  (rules)    │──▶  (wide)      │  │
│                   └─────────────┘  └─────────────┘  │
│                                                      │
│  RoleBinding connects User ←→ Role (namespace)      │
│  ClusterRoleBinding connects User ←→ ClusterRole    │
└──────────────────────────────────────────────────────┘
```

### RBAC Memory Formula

```
ServiceAccount  = WHO (identity)
Role            = WHAT (permissions, namespace level)
RoleBinding     = CONNECTS WHO to WHAT (namespace)

ClusterRole         = WHAT (permissions, cluster-wide)
ClusterRoleBinding  = CONNECTS WHO to WHAT (cluster-wide)
```

### Step 1: ServiceAccount (WHO)

```yaml
# serviceaccount.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: dev-user
  namespace: default
```

```bash
kubectl apply -f serviceaccount.yaml
kubectl get serviceaccounts
kubectl get sa
```

### Step 2: Role (WHAT — Namespace Level)

```yaml
# role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: default
rules:
- apiGroups: [""]             # "" = core API group
  resources: ["pods"]         # what resource
  verbs: ["get", "list", "watch"]  # what actions allowed
```

**Common verbs:** `get`, `list`, `watch`, `create`, `update`, `patch`, `delete`

```bash
kubectl apply -f role.yaml
kubectl get roles
kubectl describe role pod-reader
```

### Step 3: RoleBinding (CONNECT)

```yaml
# rolebinding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: default
subjects:
- kind: ServiceAccount
  name: dev-user
  namespace: default
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

```bash
kubectl apply -f rolebinding.yaml
kubectl get rolebindings
kubectl describe rolebinding read-pods-binding

# Test if permission works
kubectl auth can-i list pods \
  --as=system:serviceaccount:default:dev-user \
  -n default
```

### Step 4: ClusterRole (WHAT — Cluster Wide)

```yaml
# clusterrole.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: node-reader
rules:
- apiGroups: [""]
  resources: ["nodes", "namespaces", "persistentvolumes"]
  verbs: ["get", "list", "watch"]
```

```bash
kubectl apply -f clusterrole.yaml
kubectl get clusterroles
```

### Step 5: ClusterRoleBinding (CONNECT — Cluster Wide)

```yaml
# clusterrolebinding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: node-reader-binding
subjects:
- kind: ServiceAccount
  name: dev-user
  namespace: default
roleRef:
  kind: ClusterRole
  name: node-reader
  apiGroup: rbac.authorization.k8s.io
```

```bash
kubectl apply -f clusterrolebinding.yaml
kubectl get clusterrolebindings

# Test cluster permission
kubectl auth can-i list nodes \
  --as=system:serviceaccount:default:dev-user

# Cleanup
kubectl delete -f serviceaccount.yaml
kubectl delete -f role.yaml
kubectl delete -f rolebinding.yaml
kubectl delete -f clusterrole.yaml
kubectl delete -f clusterrolebinding.yaml
```

---

## 15. Jobs and CronJobs

### Job — Run to Completion

**Definition:** A Job creates pods that run until successful completion. Used for batch tasks, migrations, backups.

```yaml
# job.yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: batch-job
spec:
  completions: 3          # run 3 successful completions
  parallelism: 1          # run 1 pod at a time
  template:
    spec:
      containers:
      - name: worker
        image: busybox
        command: ["sh", "-c", "echo Processing task && sleep 5"]
      restartPolicy: OnFailure   # restart on failure, Never = don't restart
```

```bash
kubectl apply -f job.yaml
kubectl get jobs
kubectl describe job batch-job
kubectl get pods --selector=job-name=batch-job
kubectl logs <pod-name>
kubectl delete job batch-job
```

### CronJob — Scheduled Jobs

**Definition:** Runs Jobs on a schedule (like Linux cron). Used for scheduled backups, cleanup tasks, reports.

```yaml
# cronjob.yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello-cron
spec:
  schedule: "* * * * *"        # every minute
  # schedule: "0 2 * * *"     # daily at 2am
  # schedule: "0 0 * * 0"     # every Sunday midnight
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox:1.28
            command:
            - /bin/sh
            - -c
            - date; echo "Backend is healthy and running in Bengaluru"
          restartPolicy: OnFailure
```

```
Cron Schedule Format:
┌───────── minute (0-59)
│ ┌─────── hour (0-23)
│ │ ┌───── day of month (1-31)
│ │ │ ┌─── month (1-12)
│ │ │ │ ┌─ day of week (0-6, Sun=0)
│ │ │ │ │
* * * * *

Examples:
"*/5 * * * *"   every 5 minutes
"0 * * * *"     every hour
"0 2 * * *"     daily at 2am
"0 0 * * 1"     every Monday midnight
```

```bash
kubectl get cronjobs
kubectl get cj
kubectl describe cj hello-cron
kubectl delete cj hello-cron
# Manually trigger a cronjob
kubectl create job manual-run --from=cronjob/hello-cron
```

---

## 16. StatefulSet — Complete Guide

**Definition:** A StatefulSet manages stateful applications. Unlike Deployments, each pod gets a **stable, unique identity** that persists across rescheduling.

### StatefulSet vs Deployment

| Feature | Deployment | StatefulSet |
|---|---|---|
| Pod names | Random (dp1-abc123) | Stable ordered (nginx-0, nginx-1, nginx-2) |
| Pod order | Created/deleted randomly | Created in order (0,1,2), deleted in reverse |
| Storage | Shared or no PVC | Each pod gets its OWN PVC |
| Network identity | Random IP | Stable hostname via headless service |
| Use case | Stateless (web, API) | Stateful (databases, Kafka, Elasticsearch) |
| Scaling | Any order | Ordered (one at a time) |

### StatefulSet YAML

```yaml
# headless-service.yaml (REQUIRED for StatefulSet)
apiVersion: v1
kind: Service
metadata:
  name: nginx-headless
  labels:
    app: nginx
spec:
  clusterIP: None           # headless — no single IP, each pod gets its own DNS
  selector:
    app: nginx
  ports:
  - port: 80
    name: web

---

# statefulset.yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: nginx-statefulset
spec:
  serviceName: "nginx-headless"   # must reference headless service
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: nginx-storage
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:           # each pod gets its OWN PVC automatically
  - metadata:
      name: nginx-storage
    spec:
      accessModes: ["ReadWriteOnce"]
      resources:
        requests:
          storage: 1Gi
```

### How StatefulSet DNS Works

```
nginx-0.nginx-headless.default.svc.cluster.local
nginx-1.nginx-headless.default.svc.cluster.local
nginx-2.nginx-headless.default.svc.cluster.local

Format: <pod-name>.<service-name>.<namespace>.svc.cluster.local
```

```bash
kubectl get statefulsets
kubectl get sts
kubectl scale sts nginx-statefulset --replicas=5
kubectl delete sts nginx-statefulset
```

---

## 17. Deployment Strategies

### Strategy 1: Recreate

**How it works:** Kill ALL old pods, then create all new pods. Simple but causes **downtime**.

```
Before: [v1][v1][v1]
During: [  ][  ][  ]  ← DOWNTIME
After:  [v2][v2][v2]
```

```yaml
spec:
  strategy:
    type: Recreate
```

```
Use when: Development environments, or when old and new versions CANNOT run together
Downtime: YES
Risk: High (if new version fails, downtime continues)
```

### Strategy 2: Rolling Update (Default)

**How it works:** Gradually replaces old pods with new ones. Zero downtime.

```
Start:  [v1][v1][v1]
Step 1: [v2][v1][v1]
Step 2: [v2][v2][v1]
Step 3: [v2][v2][v2]
```

```yaml
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1         # max EXTRA pods during update
      maxUnavailable: 1   # max pods DOWN during update
```

```
Use when: Most production deployments
Downtime: NO
Rollback: kubectl rollout undo deployment/dp1
```

### Strategy 3: Blue-Green Deployment

**How it works:** Two identical environments. Blue = live. Green = new. Switch traffic by updating Service selector.

```
        ┌─────────────┐
Users → │   Service   │
        └──────┬──────┘
               │
    selector: version=blue
               │
     ┌─────────▼──────────────────┐
     │  BLUE (v1) — LIVE          │
     │  [v1-pod][v1-pod][v1-pod]  │
     └────────────────────────────┘
     ┌────────────────────────────┐
     │  GREEN (v2) — STANDBY      │
     │  [v2-pod][v2-pod][v2-pod]  │
     └────────────────────────────┘

After switch (selector: version=green):
        ┌─────────────┐
Users → │   Service   │
        └──────┬──────┘
               │
    selector: version=green
               │
     ┌─────────▼──────────────────┐
     │  GREEN (v2) — NOW LIVE     │
     │  [v2-pod][v2-pod][v2-pod]  │
     └────────────────────────────┘
```

```yaml
# blue-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
      version: blue
  template:
    metadata:
      labels:
        app: myapp
        version: blue
    spec:
      containers:
      - name: myapp
        image: myapp:1.0
        ports:
        - containerPort: 80

---

# green-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-green
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
      version: green
  template:
    metadata:
      labels:
        app: myapp
        version: green
    spec:
      containers:
      - name: myapp
        image: myapp:2.0
        ports:
        - containerPort: 80

---

# service.yaml — switch traffic by changing version: blue → green
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
    version: blue       # ← change to 'green' to switch traffic
  ports:
  - port: 80
    targetPort: 80
```

```bash
# Blue-Green workflow
kubectl apply -f blue-deployment.yaml    # Step 1: Deploy blue (live)
kubectl apply -f service.yaml            # Step 2: Service points to blue
kubectl apply -f green-deployment.yaml   # Step 3: Deploy green (standby)
kubectl port-forward deploy/myapp-green 8080:80  # Step 4: Test green
# Step 5: Update service.yaml selector to version: green
kubectl apply -f service.yaml            # Step 6: Flip — traffic now goes to green
# Rollback: change selector back to blue, kubectl apply -f service.yaml
```

```
Downtime: NO (instant switch)
Rollback: Instant (just change selector back)
Cost: Double resources (both versions running)
```

### Strategy 4: Canary Deployment

**How it works:** Send a small percentage of traffic to new version. Gradually increase if stable.

```
        ┌─────────────┐
Users → │   Service   │
        └──────┬──────┘
               │
    ┌──────────┴──────────┐
    │                     │
    ▼  (90% traffic)      ▼  (10% traffic)
[v1][v1][v1][v1][v1]    [v2]
 STABLE (5 pods)         CANARY (1 pod)
```

```yaml
# stable-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-stable
spec:
  replicas: 9              # 90% of traffic
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
        version: stable
    spec:
      containers:
      - name: myapp
        image: myapp:1.0
        ports:
        - containerPort: 80

---

# canary-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-canary
spec:
  replicas: 1              # 10% of traffic
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
        version: canary
    spec:
      containers:
      - name: myapp
        image: myapp:2.0   # NEW version
        ports:
        - containerPort: 80

---

# service.yaml — routes to BOTH (selector only uses 'app: myapp')
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp             # matches BOTH stable and canary pods
  ports:
  - port: 80
    targetPort: 80
```

```
Downtime: NO
Risk: Low (only small % of users see new version)
Rollback: Scale canary to 0, scale stable back up
Use when: A/B testing, gradual rollout to production
```

### Deployment Strategy Comparison

| Strategy | Downtime | Rollback Speed | Resource Cost | Use Case |
|---|---|---|---|---|
| Recreate | YES | Slow | Normal | Dev/simple apps |
| Rolling Update | NO | Fast | Normal+slight | Most production apps |
| Blue-Green | NO | Instant | Double | Critical apps, instant rollback |
| Canary | NO | Fast | Normal+small | Risk-averse, A/B testing |

---

## 18. Kubernetes Troubleshooting Guide

### Most Important Debugging Commands

```bash
# Check everything at once
kubectl get all -n <namespace>
kubectl get events --sort-by='.lastTimestamp'     # sorted events
kubectl get events -n default | grep -i warning   # only warnings

# Pod debugging
kubectl get pods                                  # check pod status
kubectl describe pod <pod-name>                   # MOST USEFUL — events + details
kubectl logs <pod-name>                           # container logs
kubectl logs <pod-name> -c <container-name>       # specific container logs
kubectl logs <pod-name> --previous                # logs from crashed container
kubectl logs <pod-name> -f                        # follow live logs
kubectl exec -it <pod-name> -- /bin/bash          # shell into pod
kubectl exec -it <pod-name> -- /bin/sh            # if bash not available

# Node debugging
kubectl get nodes                                 # node status
kubectl describe node <node-name>                 # node details + conditions
kubectl top nodes                                 # CPU/memory usage
kubectl top pods                                  # pod resource usage
```

---

### Error 1: CrashLoopBackOff

**What it means:** Container keeps starting and crashing repeatedly. Kubernetes keeps trying (backing off with increasing delay).

```
STATUS: CrashLoopBackOff
```

**How to diagnose:**
```bash
kubectl describe pod <pod-name>      # check Events section for error
kubectl logs <pod-name>              # current container logs
kubectl logs <pod-name> --previous   # logs from CRASHED container (most useful)
```

**Common causes and fixes:**

| Cause | Fix |
|---|---|
| Application error on startup | Fix bug in your application code |
| Wrong command/entrypoint in Dockerfile | Fix CMD or ENTRYPOINT |
| Missing environment variable | Add required env var to pod spec |
| Missing ConfigMap or Secret | Create the ConfigMap/Secret |
| Wrong port in liveness probe | Fix probe port to match container port |
| Out of memory | Increase memory limits |
| Config file missing | Mount correct ConfigMap/volume |

```bash
# Debug: start with log from previous crash
kubectl logs <pod-name> --previous

# If logs are empty (crash before logging), override entrypoint
kubectl run debug --image=myapp:1.0 --command -- sleep 3600
kubectl exec -it debug -- /bin/sh    # manually explore what's wrong
```

---

### Error 2: ImagePullBackOff / ErrImagePull

**What it means:** Kubernetes can't pull the container image from the registry.

```
STATUS: ImagePullBackOff or ErrImagePull
```

**How to diagnose:**
```bash
kubectl describe pod <pod-name>      # check Events — will show pull error
```

**Common causes and fixes:**

| Cause | Fix |
|---|---|
| Wrong image name | Fix image name in deployment YAML |
| Wrong tag | Fix image tag (check if it exists in registry) |
| Image doesn't exist | Push image to registry first |
| Private registry — no credentials | Create docker-registry secret and add imagePullSecrets |
| Registry down | Wait or switch to different tag |

```bash
# Fix for private registry
kubectl create secret docker-registry regcred \
  --docker-server=docker.io \
  --docker-username=akhil \
  --docker-password=mypassword

# Add to pod spec:
spec:
  imagePullSecrets:
  - name: regcred
  containers:
  - name: c1
    image: private-repo/myapp:1.0
```

---

### Error 3: Pending Pods

**What it means:** Pod is waiting to be scheduled but can't be placed on any node.

```
STATUS: Pending
```

**How to diagnose:**
```bash
kubectl describe pod <pod-name>      # look at Events — shows why scheduling failed
kubectl get nodes                    # check node status
kubectl describe node <node-name>    # check node conditions and capacity
```

**Common causes and fixes:**

| Cause | Fix |
|---|---|
| Not enough CPU/memory on any node | Add more nodes or reduce pod requests |
| Node selector doesn't match any node | Fix nodeSelector or node labels |
| Taint on all nodes, no toleration | Add toleration or remove taint |
| PVC not bound (storage issue) | Fix PV/PVC — check storage class |
| All nodes are full | Scale up cluster (add nodes) |

```bash
kubectl describe pod <pod-name> | grep -A 10 "Events:"
# Look for: "0/3 nodes are available: 3 Insufficient memory"
# Or: "0/3 nodes are available: node(s) had taint"
```

---

### Error 4: NodeNotReady

**What it means:** A node is not accepting pods — it's in an unhealthy state.

```
STATUS: NotReady
```

**How to diagnose:**
```bash
kubectl get nodes                         # see NotReady status
kubectl describe node <node-name>         # check Conditions section
# Look for: MemoryPressure, DiskPressure, PIDPressure, NetworkUnavailable
```

**Common causes and fixes:**

| Cause | Fix |
|---|---|
| kubelet not running | SSH to node, `systemctl restart kubelet` |
| Network plugin (CNI) failed | Restart network plugin DaemonSet |
| Node out of disk | Free disk space, add storage |
| Node out of memory | Free memory or add more RAM |
| Node lost connectivity | Check network, restart node |

```bash
# SSH to the problem node
ssh ec2-user@<node-ip>
systemctl status kubelet
journalctl -u kubelet -f          # kubelet logs
systemctl restart kubelet
```

---

### Error 5: Unauthorized Error

**What it means:** You don't have permission to perform an action.

```
Error: Unauthorized / Forbidden
```

**How to diagnose:**
```bash
kubectl auth can-i get pods                    # check your permissions
kubectl auth can-i get pods -n production      # in specific namespace
kubectl auth can-i --list                      # list all your permissions
```

**Common causes and fixes:**

| Cause | Fix |
|---|---|
| kubeconfig wrong or expired | Re-download/refresh kubeconfig |
| Missing Role/ClusterRole | Create Role with needed permissions |
| Missing RoleBinding | Create RoleBinding to connect user to Role |
| Wrong namespace | Check if you're in the right namespace |
| ServiceAccount missing permissions | Create RBAC for the ServiceAccount |

---

### Error 6: OOMKilled (Out of Memory Killed)

**What it means:** Container used more memory than its limit — Linux kernel killed it.

```
STATUS: OOMKilled (last state reason)
```

**How to diagnose:**
```bash
kubectl describe pod <pod-name>
# Look for: Last State: Terminated, Reason: OOMKilled
kubectl top pods                               # check current memory usage
```

**Common causes and fixes:**

| Cause | Fix |
|---|---|
| Memory limit too low | Increase memory limits |
| Memory leak in application | Fix application memory leak |
| Sudden traffic spike | Set HPA to scale before OOM |

```yaml
# Fix: increase memory limit
resources:
  requests:
    memory: "256Mi"
  limits:
    memory: "512Mi"      # increase this
```

---

### Error 7: FailedScheduling

**What it means:** Scheduler can't find a suitable node for the pod.

```
Events: FailedScheduling
```

**Diagnosis:**
```bash
kubectl describe pod <pod-name>      # Events will show exact reason
```

**Common reasons:**
- `0/3 nodes are available: 3 Insufficient memory`
- `0/3 nodes are available: 3 node(s) had taint`
- `0/3 nodes are available: 3 node(s) didn't match node selector`

**Fix:** Based on the message — add nodes, remove taints, or fix node selectors.

---

### Error 8: Error Creating LoadBalancer

**What it means:** Kubernetes couldn't create a cloud load balancer.

**How to diagnose:**
```bash
kubectl describe service <service-name>      # check Events
```

**Common causes and fixes:**

| Cause | Fix |
|---|---|
| Insufficient IAM permissions | Add load balancer permissions to node IAM role |
| Cloud provider quota exceeded | Request quota increase |
| Wrong AWS region/zone config | Fix cluster config for correct region |
| Security group issue | Check security group allows required ports |

---

### Error 9: ContainerCreating (Stuck)

**What it means:** Container is stuck in creating state.

```
STATUS: ContainerCreating (for too long)
```

**How to diagnose:**
```bash
kubectl describe pod <pod-name>      # check Events
```

**Common causes and fixes:**

| Cause | Fix |
|---|---|
| Volume mount issue (PVC not bound) | Check PVC status, fix storage |
| ConfigMap/Secret doesn't exist | Create missing ConfigMap or Secret |
| Image being pulled (slow registry) | Wait, or use image pull policy |
| Network plugin not ready | Restart CNI DaemonSet |

```bash
kubectl get pvc                      # check if PVC is bound
kubectl get configmaps               # check if CM exists
kubectl get secrets                  # check if Secret exists
```

---

### General Troubleshooting Workflow

```
1. kubectl get pods                  → What is the STATUS?
2. kubectl describe pod <name>       → What do EVENTS say?
3. kubectl logs <pod-name>           → What does the APP say?
4. kubectl logs <name> --previous    → What did it say before crash?
5. kubectl exec -it <name> -- sh     → Can I get inside?
6. kubectl get events                → Anything unusual?
7. kubectl top pods / nodes          → Resource pressure?
8. kubectl describe node <name>      → Node healthy?
```

---

## 19. Essential kubectl Quick Reference

```bash
# GET (view resources)
kubectl get pods                      # pods in default namespace
kubectl get pods -n kube-system       # pods in specific namespace
kubectl get pods -A                   # pods in ALL namespaces
kubectl get pods -o wide              # with IP and node info
kubectl get pods -w                   # watch (live updates)
kubectl get all                       # all resources in namespace

# DESCRIBE (detailed info)
kubectl describe pod <name>
kubectl describe node <name>
kubectl describe service <name>
kubectl describe deployment <name>

# APPLY / CREATE
kubectl apply -f file.yaml            # create or update
kubectl create -f file.yaml           # create only (fails if exists)
kubectl apply -f ./directory/         # apply all YAMLs in directory
kubectl apply -f https://url/file.yaml  # apply from URL

# DELETE
kubectl delete pod <name>
kubectl delete -f file.yaml
kubectl delete pods --all             # delete all pods in namespace
kubectl delete pods -l app=myapp      # delete by label

# EXECUTE
kubectl exec -it <pod> -- bash        # shell into pod
kubectl exec -it <pod> -- cat /etc/config  # run command in pod
kubectl cp localfile.txt <pod>:/path/ # copy file to pod
kubectl cp <pod>:/path/file.txt .     # copy file from pod

# PORT FORWARD
kubectl port-forward pod/<name> 8080:80        # local:pod
kubectl port-forward service/<name> 8080:80    # forward service port

# LABELS
kubectl label pod <name> env=prod      # add label
kubectl get pods -l env=prod           # filter by label
kubectl get pods --show-labels         # show all labels

# SCALING
kubectl scale deployment dp1 --replicas=5
kubectl autoscale deployment dp1 --min=2 --max=10 --cpu-percent=80

# CONFIG
kubectl config get-contexts            # list available clusters/contexts
kubectl config use-context <name>      # switch cluster
kubectl config current-context         # show current context
```

---
---


---
# SECTION 3: DOCKER — COMPLETE GUIDE

## Docker Architecture

Docker has three main components:

1. **Docker Client** — the CLI you use. `docker build`, `docker run`, `docker push` etc. Sends commands to the daemon via REST API.
2. **Docker Daemon** — background service that does all the actual work — building images, running containers, managing networking and storage.
3. **Docker Registry** — stores images. Docker Hub (public), Amazon ECR, Azure ACR (private).

**Workflow:**
```
You write Dockerfile
→ docker build (client sends to daemon)
→ daemon builds image
→ docker push (push to registry)
→ others pull and run the image
```

---

## Q1. What is Docker and why does a DevOps engineer use it?

**Answer:**
Docker is a containerization platform that packages your application, dependencies, and runtime into a container — a lightweight, isolated environment. Instead of shipping your whole server setup, you ship a Docker image that runs the same everywhere — laptop, staging, production.

**Why better than VMs:**

| Feature | Virtual Machine | Docker Container |
|---|---|---|
| OS | Full OS per VM | Shares host OS kernel |
| Startup | Minutes | Seconds |
| Size | GBs | MBs |
| Portability | Low | High |
| Performance | Heavy | Lightweight |

**Key benefit:** Eliminates "works on my machine" problem. Same image runs identically everywhere.

---

## Q2. What is the difference between a Docker Image and a Docker Container?

**Answer:**
- **Docker Image** — a read-only blueprint/template with all the code, dependencies, and configuration. Built from a Dockerfile. Stored in a registry.
- **Docker Container** — a running instance of an image. The actual executing process with its own writable layer.

**Example:**
```bash
docker pull nginx                        # pull image from Docker Hub
docker run -d -p 80:80 --name mynginx nginx   # create and run a container from image
docker ps                                # see running containers
```

You can run multiple containers from one image — they're all isolated from each other.

---

## Q3. What is a Dockerfile and what are the key instructions?

**Answer:**
A Dockerfile is a text file with instructions to build a Docker image.

| Instruction | Purpose | Example |
|---|---|---|
| FROM | Base image to start with | `FROM node:18-alpine` |
| RUN | Execute commands during build | `RUN npm install` |
| COPY | Copy files from host into image | `COPY . /app` |
| WORKDIR | Set working directory | `WORKDIR /app` |
| EXPOSE | Declare port the container listens on | `EXPOSE 3000` |
| CMD | Default command when container starts | `CMD ["node", "app.js"]` |
| ENV | Set environment variables | `ENV NODE_ENV=production` |
| USER | Set non-root user for security | `USER node` |

**Example Dockerfile for a Node.js app:**
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
USER node
CMD ["node", "app.js"]
```

---

## Q4. What is the difference between COPY and ADD?

**Answer:**
- **COPY** — simply copies files from host into the image. Nothing extra. Preferred.
- **ADD** — does everything COPY does, plus extracts tar files automatically and can fetch from URLs.

**Best practice:** Always use COPY. Use ADD only when you need tar extraction.

```dockerfile
COPY ./app /app          # preferred - simple and predictable
ADD archive.tar.gz /app  # use only when you need auto-extraction
```

---

## Q5. What are Docker Layers and why do they matter?

**Answer:**
Each instruction in a Dockerfile creates a read-only layer. Layers stack on top of each other to form the final image.

**How caching works:**
```dockerfile
FROM node:18-alpine        # Layer 1 — cached unless base image changes
WORKDIR /app               # Layer 2 — cached
COPY package*.json ./      # Layer 3 — cached unless package.json changes
RUN npm install            # Layer 4 — cached unless layer 3 changes
COPY . .                   # Layer 5 — changes every time code changes
CMD ["node", "app.js"]     # Layer 6
```

**Optimization tip:** Put rarely changing instructions at top, frequently changing at bottom. This way `npm install` is cached and doesn't re-run every time you change your code.

**Container writable layer:** When you run a container, Docker adds a writable layer on top. Multiple containers from one image each get their own writable layer.

---

## Q6. What is the difference between RUN, CMD, and ENTRYPOINT?

**Answer:**

| Instruction | When it runs | Can be overridden? | Use for |
|---|---|---|---|
| RUN | Build time | N/A | Installing packages |
| CMD | Runtime (container start) | Yes, easily | Default arguments |
| ENTRYPOINT | Runtime (container start) | Only with --entrypoint flag | Main executable |

**Example:**
```dockerfile
RUN apt-get install -y curl        # runs during build, installs curl

ENTRYPOINT ["python3", "app.py"]   # always runs python3 app.py
CMD ["--debug"]                    # default argument, can be overridden

# Running: docker run myimage --prod
# Result: python3 app.py --prod   (CMD overridden, ENTRYPOINT stays)
```

---

## Q7. What is Docker Compose?

**Answer:**
Docker Compose lets you define and run multiple containers together as a single application using a `docker-compose.yml` file.

**Example docker-compose.yml (Frontend + Backend + Database):**
```yaml
version: '3.8'
services:
  frontend:
    build: ./frontend
    ports:
      - "80:80"
    depends_on:
      - backend

  backend:
    build: ./backend
    ports:
      - "3000:3000"
    environment:
      - DB_HOST=database
      - DB_PORT=5432
    depends_on:
      - database

  database:
    image: postgres:14
    environment:
      - POSTGRES_DB=myapp
      - POSTGRES_PASSWORD=secret
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
```

**Key commands:**
```bash
docker-compose up -d       # start all containers in background
docker-compose down        # stop and remove containers
docker-compose logs -f     # follow logs of all services
docker-compose ps          # list running services
docker-compose build       # rebuild images
```

**Use case:** Perfect for local development. In production, use Kubernetes.

---

## Q8. What is Docker Networking?

**Answer:**
Docker networking controls how containers communicate with each other and the outside world.

| Network Type | Description | Use case |
|---|---|---|
| Bridge | Default. Containers on same bridge can talk to each other | Most common, single host |
| Host | Container uses host machine's network directly | High performance, no isolation |
| Overlay | Containers across different machines communicate | Docker Swarm, multi-host |
| None | No networking | Complete isolation |

**Commands:**
```bash
docker network ls                          # list networks
docker network create mynetwork            # create custom bridge network
docker run --network mynetwork myapp       # run container on specific network
docker network inspect mynetwork           # inspect network details
```

**Example:** Two containers on same bridge network can communicate by container name:
```bash
# Container 1: backend
# Container 2: database
# backend can reach database using: postgres://database:5432
```

---

## Q9. What is a Docker Volume?

**Answer:**
A Docker volume is persistent storage that survives even after a container is deleted. Containers are ephemeral — when they stop, data inside is lost. Volumes store data outside the container.

**Types:**
- **Named Volume** — managed by Docker, stored in Docker's managed location. Best for production.
- **Bind Mount** — mounts a specific host directory into container. Good for development.

**Commands:**
```bash
docker volume create myvolume              # create named volume
docker volume ls                           # list volumes
docker volume inspect myvolume             # inspect volume details
docker volume rm myvolume                  # remove volume

# Run container with volume
docker run -v myvolume:/var/lib/postgresql/data postgres   # named volume
docker run -v /home/akhil/app:/app myapp                   # bind mount
```

**Example:** PostgreSQL database with persistent volume:
```bash
docker run -d \
  --name postgres \
  -e POSTGRES_PASSWORD=secret \
  -v pgdata:/var/lib/postgresql/data \
  postgres:14
# Even if container is deleted, data in pgdata volume remains
```

---

## Q10. What is a Docker Registry and types?

**Answer:**
A Docker registry is a centralized repository to store and manage Docker images.

| Registry | Type | Use case |
|---|---|---|
| Docker Hub | Public | Open source projects, base images |
| Amazon ECR | Private | AWS-based projects |
| Azure ACR | Private | Azure-based projects |
| Harbor | Self-hosted | On-premise enterprise |

**Commands:**
```bash
docker login                                    # login to Docker Hub
docker login <registry-url>                     # login to private registry

docker tag myapp:1.0 myrepo/myapp:1.0           # tag image
docker push myrepo/myapp:1.0                    # push to registry
docker pull myrepo/myapp:1.0                    # pull from registry
```

---

## Q11. What is a Multi-Stage Dockerfile?

**Answer:**
Multi-stage builds use multiple FROM statements — a build stage and a runtime stage. Build stage compiles code with all dev tools. Runtime stage copies only the built artifacts, keeping the final image small and secure.

**Example:**
```dockerfile
# Stage 1 - Build
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2 - Runtime (only artifacts, no dev tools)
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
EXPOSE 3000
CMD ["node", "dist/app.js"]
```

**Result:** Final image is tiny — no build tools, no source code, just what's needed to run.

---

## Q12. Docker Security Best Practices

**Answer:**
```dockerfile
# 1. Never run as root — use non-root user
USER node

# 2. Use specific base image versions, not latest
FROM node:18-alpine   # good
FROM node:latest      # bad

# 3. Use .dockerignore to exclude unnecessary files
# .dockerignore file:
node_modules
.git
*.log
.env

# 4. Don't hardcode secrets
ENV DB_PASSWORD=secret123   # BAD — visible in image history
# Use environment variables at runtime instead:
docker run -e DB_PASSWORD=secret123 myapp

# 5. Use multi-stage builds to reduce attack surface
# 6. Scan images for vulnerabilities
docker scan myapp:1.0

# 7. Set resource limits
docker run --memory="256m" --cpus="0.5" myapp
```

---

## Q13. Docker Troubleshooting Commands

**Answer:**
```bash
# View container logs
docker logs mycontainer              # view logs
docker logs -f mycontainer          # follow logs in real time
docker logs --tail 50 mycontainer   # last 50 lines

# Inspect container
docker inspect mycontainer          # full container details
docker stats                        # live CPU, memory usage of all containers
docker top mycontainer              # processes running inside container

# Debug inside container
docker exec -it mycontainer bash    # open bash shell inside container
docker exec -it mycontainer sh      # use sh if bash not available

# Container lifecycle
docker ps                           # list running containers
docker ps -a                        # list all containers (including stopped)
docker stop mycontainer             # stop container
docker start mycontainer            # start stopped container
docker restart mycontainer          # restart container
docker rm mycontainer               # remove stopped container
docker rm -f mycontainer            # force remove running container

# Image management
docker images                       # list all images
docker rmi myimage:1.0              # remove image
docker image prune                  # remove unused images
docker system prune                 # clean up everything unused
```

---

## Q14. What is the difference between Docker and containerd?

**Answer:**
- **Docker** — complete platform. Includes CLI, build tools, image management, networking, storage, and containerd underneath.
- **containerd** — lightweight container runtime. Just the core engine that runs containers. No CLI, no build tools.

Docker uses containerd under the hood. Kubernetes moved away from Docker and now uses containerd directly as its container runtime — simpler, faster, less overhead.

**For interviews:** Docker is the full toolset for developers. containerd is the leaner runtime that Kubernetes prefers in production.

---

## Q15. What is Container Orchestration and why do you need it?

**Answer:**
Container orchestration automates deploying, scaling, and managing containers across multiple machines. Without it, you'd manually manage each container — impossible at scale.

**What orchestration handles:**
- Deploying containers across multiple nodes
- Scaling up/down based on demand
- Restarting failed containers (self-healing)
- Zero-downtime updates
- Load balancing traffic
- Networking between containers
- Persistent storage management

**Tools:**
- **Kubernetes** — industry standard, most powerful
- **Docker Swarm** — simpler, built into Docker, less features

**For interviews:** Always say Kubernetes. It's what enterprise DevOps teams use.

---


---
# SECTION 4: JENKINS

## Q1. What is Jenkins and why does a DevOps engineer use it?

**Answer:**
Jenkins is an open-source automation server used to build CI/CD pipelines. It automatically triggers builds when code is pushed, runs tests, builds artifacts, and deploys to environments — without manual intervention.

**Integrations:** Git, Docker, Kubernetes, Nexus, Artifactory, SonarQube, Slack

**Why DevOps uses it:**
- Automates the entire release process
- Catches bugs early via automated testing
- Consistent, repeatable deployments
- Saves time — no manual build/deploy steps

---

## Q2. What are Jenkins Job Types?

**Answer:**

| Job Type | Description | Use case |
|---|---|---|
| Freestyle | Manual UI configuration, build steps defined in UI | Simple, legacy jobs |
| Pipeline | Jenkinsfile written in Groovy, Pipeline as Code | Modern standard |
| Multibranch Pipeline | Auto-creates pipelines for each Git branch | Feature branch workflows |

**For interviews:** Always talk about Pipeline jobs with Jenkinsfile — that's the industry standard.

---

## Q3. What is a Jenkinsfile?

**Answer:**
A Jenkinsfile is a text file written in Groovy that defines your entire CI/CD pipeline as code. It lives in your Git repo alongside your application code. This means your pipeline is version controlled.

**Example Jenkinsfile:**
```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/AkhilNikhil/myapp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build & Push') {
            steps {
                sh 'docker build -t myapp:1.0 .'
                sh 'docker push myrepo/myapp:1.0'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
```

**Benefits:** Version controlled, reviewable, consistent, reusable.

---

## Q4. What are Common CI/CD Pipeline Stages?

**Answer:**

| Stage | What it does |
|---|---|
| Checkout | Pull latest code from Git |
| Build | Compile code, create JAR/WAR/binary |
| Test | Run unit tests, integration tests |
| Code Quality | SonarQube scan for code smells, bugs |
| Security Scan | Check for vulnerabilities |
| Docker Build | Build Docker image |
| Push to Registry | Push image to ECR/ACR/Docker Hub |
| Deploy to Staging | Deploy to test environment |
| Deploy to Production | Deploy to live environment |

---

## Q5. What are Jenkins Triggers?

**Answer:**
Triggers tell Jenkins when to run a pipeline automatically.

| Trigger | How it works | Best for |
|---|---|---|
| Webhook | Git sends notification to Jenkins on code push. Instant. | Production — fastest |
| Poll SCM | Jenkins checks Git repo every X minutes for changes | Legacy systems |
| Scheduled | Runs on cron schedule (e.g., every night at 2am) | Nightly builds |
| Manual | Click "Build Now" in Jenkins UI | On-demand |
| Upstream Job | One pipeline triggers another | Pipeline chaining |

**Example Webhook trigger in Jenkinsfile:**
```groovy
pipeline {
    agent any
    triggers {
        githubPush()   // triggers on every GitHub push
    }
    stages { ... }
}
```

**Best practice:** Always use Webhooks — instant response when code is pushed.

---

## Q6. Declarative vs Scripted Pipeline

**Answer:**

| Feature | Declarative | Scripted |
|---|---|---|
| Syntax | Structured, fixed format | Full Groovy programming |
| Readability | Easy to read | Complex |
| Flexibility | Limited | Very flexible |
| Standard | Modern standard ✅ | Legacy |

**Declarative Example:**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn build'
            }
        }
    }
}
```

**Scripted Example:**
```groovy
node {
    stage('Build') {
        if (env.BRANCH_NAME == 'master') {
            sh 'mvn build'
        }
    }
}
```

**For interviews:** Always say Declarative is better — modern standard, easier to maintain.

---

## Q7. How to Manage Secrets in Jenkins?

**Answer:**
Never hardcode secrets in Jenkinsfile. Use Jenkins Credentials Store.

**Types of credentials:**
- Username/Password — Docker Hub, Git
- SSH Key — server access
- Secret Text — API tokens, keys
- Certificate — SSL certs

**Example using credentials in Jenkinsfile:**
```groovy
pipeline {
    agent any

    environment {
        DOCKER_CREDS = credentials('docker-hub-credentials')
    }

    stages {
        stage('Push Image') {
            steps {
                sh '''
                    echo $DOCKER_CREDS_PSW | docker login -u $DOCKER_CREDS_USR --password-stdin
                    docker push myrepo/myapp:1.0
                '''
            }
        }
    }
}
```

**Rule:** Credentials are injected at runtime — never visible in logs or Git history.

---

## Q8. What is Jenkins Master and Agent?

**Answer:**
- **Master (Controller)** — manages jobs, schedules builds, stores configurations, serves the UI. Does NOT run builds itself.
- **Agent (Worker)** — executes the actual build jobs. Can have multiple agents with different setups.

**Why use agents:**
- Master stays lightweight
- Scale by adding more agents
- Different agents for different jobs (Docker agent, Java agent, etc.)

**Example in Jenkinsfile:**
```groovy
pipeline {
    agent { label 'docker' }   // run only on agent labelled 'docker'
    stages { ... }
}

// OR
pipeline {
    agent any    // run on any available agent
    stages { ... }
}
```

---

## Q9. What is a Jenkins Shared Library?

**Answer:**
Reusable Groovy code shared across multiple pipelines. Write once, use everywhere.

**Structure:**
```
shared-library/
  vars/
    deploy.groovy    # reusable deploy function
    test.groovy      # reusable test function
```

**Usage in Jenkinsfile:**
```groovy
@Library('my-shared-library') _

pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                script {
                    deploy('production')   // call shared function
                }
            }
        }
    }
}
```

**Benefits:** No code duplication, update in one place, consistent across all teams.

---

## Q10. What is Blue Ocean in Jenkins?

**Answer:**
Blue Ocean is Jenkins's modern UI for visualizing pipelines. Traditional Jenkins UI is cluttered and hard to read. Blue Ocean shows pipelines as a visual flowchart.

**Features:**
- Visual pipeline view — each stage as a box
- Green = success, Red = failed
- See exactly which stage failed instantly
- Inline logs per stage
- Pull request integration

**For interviews:** Mention it as the modern Jenkins UI that improves pipeline visibility and troubleshooting.

---


---
# SECTION 5: GIT — COMPLETE GUIDE

> Flow: VCS Basics → Git Basics → Working Areas → Commands → Branching → Merging → Remote Repos → Undoing Changes → Advanced

---

## 1. What is Version Control System (VCS)?

**Definition:**
A Version Control System tracks and manages changes to files over time. It allows multiple developers to collaborate on the same codebase, keep history of every change, and revert to any previous state.

**Why DevOps needs VCS:**
- Every code change is tracked with who made it, when, and why
- Multiple developers can work on same project without overwriting each other's work
- Roll back to a stable version if something breaks
- Foundation of CI/CD — pipelines trigger from code changes in VCS

---

## 2. Types of VCS

### A) Local VCS
- Tracks changes only on your local machine
- No collaboration possible
- Example: RCS (old, rarely used)
- **Problem:** If your machine dies, everything is lost

### B) Centralized VCS (CVCS)
- One central server stores all versions
- Developers pull from and push to that single server
- Example: SVN (Subversion), CVS
- **Pros:** Simple, single source of truth
- **Cons:** Single point of failure — if server goes down, no one can work. No offline work.

### C) Distributed VCS (DVCS)
- Every developer has a full copy of the repository including complete history
- Example: **Git**, Mercurial
- **Pros:** Work offline, no single point of failure, faster operations, full history locally
- **Cons:** Slightly more complex to learn

> **Git is a Distributed VCS — this is why it's the industry standard.**

---

## 3. What is Git?

**Definition:**
Git is a free, open-source Distributed Version Control System created by Linus Torvalds in 2005. It tracks changes in source code, supports non-linear development through branching, and enables team collaboration.

**Key concepts:**
- Every change is a **commit** (a snapshot of your code at that point)
- Branches let you work on features without affecting main code
- Git is **local first** — most operations happen on your machine without internet

---

## 4. Git Workflow — The Four Areas

Understanding these four areas is the most important concept in Git:

```
Working Directory  →  Staging Area  →  Local Repository  →  Remote Repository
   (your files)      (git add)         (git commit)          (git push)
```

### A) Working Directory
- Where you actually write and edit your files
- Files here are either **tracked** (Git knows about them) or **untracked** (new files Git hasn't seen)
- Changes here are not saved to Git yet

### B) Staging Area (Index)
- A preparation zone before committing
- You **choose** which changes to include in the next commit
- Use `git add` to move changes from working directory to staging area
- Allows you to commit only specific changes, not everything

### C) Local Repository
- Your local Git database stored in the `.git` folder
- When you `git commit`, changes move from staging to local repo
- Contains full history of all commits
- Works completely offline

### D) Remote Repository
- A repository hosted on a server — GitHub, GitLab, Bitbucket, Azure Repos
- Use `git push` to send your local commits to remote
- Use `git pull` to get others' changes from remote
- The central collaboration point for teams

---

## 5. Git Setup — First Time Configuration

```bash
# Set your identity (required before first commit)
git config --global user.name "Akhil B M"
git config --global user.email "akhilbm13@gmail.com"

# Set default editor
git config --global core.editor vim

# Check all config
git config --list

# Initialize a new Git repo in current directory
git init

# Clone an existing remote repo to your machine
git clone https://github.com/username/repo.git

# Clone into a specific folder name
git clone https://github.com/username/repo.git my-folder
```

---

## 6. Basic Git Commands — Working Directory to Local Repo

### Checking Status
```bash
git status              # see which files are modified, staged, or untracked
git status -s           # short status view
```

### Tracking Files — git add (Working Directory → Staging Area)
```bash
git add filename.txt          # stage a specific file
git add .                     # stage ALL changes in current directory
git add *.js                  # stage all JS files
git add src/                  # stage all files in src folder
git add -p                    # interactively choose which changes to stage (patch mode)
```

### Committing — git commit (Staging Area → Local Repo)
```bash
git commit -m "Add login feature"           # commit with message
git commit -am "Fix bug"                    # add + commit tracked files in one step
git commit --amend -m "New message"         # fix last commit message (before push)
git commit --amend --no-edit               # add forgotten file to last commit
```

### Viewing History
```bash
git log                          # full commit history
git log --oneline                # compact one-line view
git log --oneline --graph        # visual branch graph
git log --oneline -5             # last 5 commits
git log --author="Akhil"         # commits by specific author
git log filename.txt             # history of a specific file
git show <commit-id>             # show details of a specific commit
```

### Viewing Differences
```bash
git diff                         # changes in working directory (not staged)
git diff --staged                # changes in staging area (ready to commit)
git diff main feature-branch     # compare two branches
git diff <commit1> <commit2>     # compare two commits
```

---

## 7. Branching — Working in Isolation

**What is a Branch?**
A branch is an independent line of development. You create a branch to work on a feature or bug fix without affecting the main codebase. When done, you merge it back.

**Default branch:** `main` or `master`

### Branch Commands
```bash
# View branches
git branch                    # list local branches
git branch -r                 # list remote branches
git branch -a                 # list all branches (local + remote)

# Create branch
git branch feature-login      # create new branch
git checkout -b feature-login # create AND switch to new branch (old way)
git switch -c feature-login   # create AND switch to new branch (new way)

# Switch branch
git checkout main             # switch to main branch (old way)
git switch main               # switch to main branch (new way)

# Rename branch
git branch -m old-name new-name

# Delete branch
git branch -d feature-login   # delete branch (safe — only if merged)
git branch -D feature-login   # force delete branch (even if not merged)

# Delete remote branch
git push origin --delete feature-login
```

### Branch Workflow Example
```bash
# 1. Create feature branch from main
git switch main
git pull origin main          # make sure main is up to date
git switch -c feature-login   # create feature branch

# 2. Work on feature
# ... edit files ...
git add .
git commit -m "Add login page"
git commit -m "Add login API"

# 3. Push feature branch to remote
git push origin feature-login

# 4. Create Pull Request on GitHub/GitLab
# 5. After review, merge to main
```

---

## 8. Merging

**What is Merging?**
Merging combines changes from one branch into another. You typically merge a feature branch into main when the feature is complete.

### Types of Merges

#### A) Fast-Forward Merge
Happens when the target branch has no new commits since the feature branch was created. Git simply moves the pointer forward. No merge commit created. Clean, linear history.

```bash
git switch main
git merge feature-login       # fast-forward if possible
```

```
Before:           After:
main: A-B         main: A-B-C-D
feature:   C-D
```

#### B) Three-Way Merge (2-Way Merge / Recursive Merge)
Happens when both branches have diverged — both have new commits. Git finds the common ancestor commit and creates a new **merge commit** that combines both.

```bash
git switch main
git merge feature-login       # creates a merge commit
git merge --no-ff feature-login  # force merge commit even if fast-forward possible
```

```
Before:           After:
main: A-B-E       main: A-B-E---M  (M = merge commit)
feature:   C-D          \   C-D-/
```

#### C) Squash Merge
Combines all feature branch commits into a single commit on main. Keeps history clean.

```bash
git merge --squash feature-login
git commit -m "Add login feature"   # one clean commit
```

---

## 9. Merge Conflict

**What is a Merge Conflict?**
A merge conflict happens when two branches modify the **same line** of the same file differently. Git can't decide which change to keep, so it asks you to resolve it manually.

**When does it happen?**
- Two developers edit the same line in the same file
- One developer deletes a file another developer modified
- Both branches rename the same file differently

### How to Resolve a Merge Conflict

```bash
# Step 1: Try to merge
git merge feature-login
# OUTPUT: CONFLICT (content): Merge conflict in app.js

# Step 2: Open the conflicted file — Git marks conflicts like this:
<<<<<<< HEAD (your current branch - main)
const port = 3000;
=======
const port = 8080;
>>>>>>> feature-login (incoming branch)

# Step 3: Manually edit the file to keep what you want:
const port = 3000;   # keep main's version
# OR
const port = 8080;   # keep feature's version
# OR combine both if needed

# Step 4: Remove the conflict markers <<<<<<<, =======, >>>>>>>

# Step 5: Stage the resolved file
git add app.js

# Step 6: Complete the merge
git commit -m "Merge feature-login — resolved port conflict"

# To abort a merge and go back to before
git merge --abort
```

---

## 10. Connecting to Remote Repository

**What is a Remote?**
A remote is a version of your repository hosted on a server (GitHub, GitLab, Azure Repos). `origin` is the default name for your remote.

### Remote Commands
```bash
# View remotes
git remote -v                              # list remotes with URLs
git remote show origin                     # details about origin

# Add remote
git remote add origin https://github.com/akhil/repo.git

# Change remote URL
git remote set-url origin https://github.com/akhil/new-repo.git

# Remove remote
git remote remove origin
```

---

## 11. Push, Pull, Fetch — Syncing with Remote

### git push — Local Repo → Remote
```bash
git push origin main                    # push main branch to origin
git push origin feature-login          # push feature branch
git push -u origin feature-login       # push and set upstream (track remote branch)
git push --force origin main           # force push (DANGEROUS — overwrites remote)
git push --force-with-lease            # safer force push (fails if remote has new commits)
git push origin --delete feature-login # delete remote branch
git push --tags                        # push all tags
```

### git pull — Remote → Local (fetch + merge in one step)
```bash
git pull origin main                   # pull latest changes from main
git pull                               # pull from tracked upstream branch
git pull --rebase origin main          # pull and rebase instead of merge
```

### git fetch — Download without Merging
```bash
git fetch origin                       # download all remote changes, don't merge
git fetch origin main                  # fetch specific branch
git fetch --all                        # fetch from all remotes

# After fetch, you can compare:
git diff main origin/main              # see what changed on remote
git merge origin/main                  # then manually merge when ready
```

**Key Difference:**
- `git pull` = `git fetch` + `git merge` — downloads AND merges automatically
- `git fetch` = downloads only, you decide when to merge — safer

### git clone — Copy Remote Repo to Local
```bash
git clone https://github.com/akhil/repo.git        # clone repo
git clone https://github.com/akhil/repo.git myapp  # clone into specific folder
git clone --branch develop repo.git               # clone specific branch
git clone --depth 1 repo.git                      # shallow clone (latest commit only, faster)
```

---

## 12. Undoing Changes

This is one of the most important topics in Git interviews.

### A) git checkout — Discard Working Directory Changes
```bash
git checkout -- filename.txt      # discard changes in working directory (old way)
git restore filename.txt          # discard changes in working directory (new way)
git restore .                     # discard ALL working directory changes
```
⚠️ **Warning:** This is permanent — you lose your unsaved changes.

### B) git reset — Unstage or Go Back in History

**Three modes:**

```bash
# 1. git reset --soft <commit>
# Moves HEAD back to that commit
# Changes go back to STAGING AREA (staged, ready to recommit)
git reset --soft HEAD~1           # undo last commit, keep changes staged
git reset --soft <commit-id>

# 2. git reset --mixed <commit> (DEFAULT)
# Moves HEAD back to that commit
# Changes go back to WORKING DIRECTORY (unstaged)
git reset HEAD~1                  # undo last commit, unstage changes
git reset HEAD filename.txt       # unstage a specific file

# 3. git reset --hard <commit>
# Moves HEAD back to that commit
# ALL changes are DELETED permanently
git reset --hard HEAD~1           # undo last commit, DELETE all changes
git reset --hard <commit-id>      # go back to specific commit, delete everything after
```

⚠️ **Warning:** `--hard` deletes your work permanently. Use with caution.

**When to use which:**
| Mode | Changes go to | Use when |
|---|---|---|
| --soft | Staging area | Want to recommit with different message |
| --mixed | Working directory | Want to re-edit before staging |
| --hard | DELETED | Want to completely undo, no going back |

### C) git revert — Safely Undo a Commit
```bash
git revert <commit-id>            # create a NEW commit that undoes the specified commit
git revert HEAD                   # revert last commit
git revert HEAD~3..HEAD           # revert last 3 commits
git revert --no-commit <commit-id> # revert without auto-committing
```

**Key difference from reset:**
- `git reset` — rewrites history (dangerous if already pushed)
- `git revert` — adds a new commit that undoes changes (safe, preserves history)

> **Rule:** Use `revert` for commits already pushed to remote. Use `reset` only for local commits not yet pushed.

### D) git rm — Remove Files from Git
```bash
git rm filename.txt               # remove file from working dir AND staging
git rm --cached filename.txt      # remove from Git tracking only, keep file locally
git rm -r foldername/             # remove entire folder

# Common use: stop tracking a file (e.g., accidentally committed .env)
git rm --cached .env
echo ".env" >> .gitignore
git commit -m "Remove .env from tracking"
```

---

## 13. git stash — Save Work Temporarily

**What is Stash?**
Stash temporarily saves your uncommitted changes so you can switch branches or do something else, then come back to your work.

```bash
git stash                         # stash current changes
git stash push -m "login work"   # stash with a name
git stash list                    # list all stashes
git stash pop                     # apply last stash and remove it from stash list
git stash apply                   # apply last stash but keep it in stash list
git stash apply stash@{2}         # apply specific stash
git stash drop stash@{0}          # delete specific stash
git stash clear                   # delete all stashes
```

**Example:**
```bash
# You're working on feature-login when urgent bug fix is needed
git stash                         # save your work
git switch main                   # switch to main
git switch -c hotfix-bug          # fix the bug
git commit -m "Fix critical bug"
git switch feature-login          # go back
git stash pop                     # restore your saved work
```

---

## 14. git cherry-pick — Pick Specific Commits

**What is Cherry-pick?**
Cherry-pick applies a specific commit from one branch to another. You pick only the commit you want, not the entire branch.

```bash
git cherry-pick <commit-id>            # apply specific commit to current branch
git cherry-pick <commit1> <commit2>    # apply multiple commits
git cherry-pick A..B                   # apply range of commits
git cherry-pick --no-commit <commit-id> # apply changes without committing
git cherry-pick --abort                # abort cherry-pick if conflict
```

**Example:**
```bash
# You fixed a bug in feature branch and want that fix in main too
git log feature-branch --oneline
# abc1234 Fix null pointer bug
# def5678 Add new feature

git switch main
git cherry-pick abc1234     # apply only the bug fix to main, not the feature
```

**When to use:**
- Bug fix in one branch needed in another
- Pick specific features without merging entire branch
- Backporting fixes to older release branches

---

## 15. git rebase — Rewrite History

**What is Rebase?**
Rebase moves or replays your commits on top of another branch. Creates a cleaner, linear history compared to merge commits.

```bash
git rebase main               # rebase current branch onto main
git rebase --interactive HEAD~3  # interactive rebase — edit last 3 commits
git rebase --abort            # abort rebase
git rebase --continue         # continue after resolving conflict
```

**Interactive rebase options:**
```bash
git rebase -i HEAD~3
# Opens editor with:
# pick abc1234 First commit
# pick def5678 Second commit
# pick ghi9012 Third commit

# Change 'pick' to:
# squash  — combine with previous commit
# reword  — edit commit message
# drop    — delete commit
# edit    — pause to amend
```

**Merge vs Rebase:**
| | Merge | Rebase |
|---|---|---|
| History | Preserves full history with merge commits | Creates clean linear history |
| Safety | Safe for shared branches | Never rebase shared/public branches |
| Use when | Merging feature to main | Keeping feature branch up to date with main |

> **Rule:** Never rebase commits that have been pushed to a shared remote branch.

---

## 16. git tag — Marking Releases

```bash
git tag                           # list all tags
git tag v1.0.0                    # create lightweight tag
git tag -a v1.0.0 -m "Release 1.0.0"  # create annotated tag (recommended)
git tag -a v1.0.0 <commit-id>    # tag a specific commit
git push origin v1.0.0           # push specific tag
git push origin --tags            # push all tags
git tag -d v1.0.0                 # delete local tag
git push origin --delete v1.0.0  # delete remote tag
```

**Use in DevOps:** Tag releases in CI/CD pipelines. When you tag a commit, the pipeline automatically builds and deploys that version.

---

## 17. .gitignore — Excluding Files from Git

**.gitignore** tells Git which files to never track.

```bash
# Example .gitignore file:
node_modules/       # dependency folders
.env                # environment variables (NEVER commit secrets)
*.log               # log files
dist/               # build output
.DS_Store           # Mac system files
*.jar               # compiled Java files
target/             # Maven build folder
__pycache__/        # Python cache

# Check what's being ignored
git status --ignored

# If you accidentally committed something:
git rm --cached filename
echo "filename" >> .gitignore
git commit -m "Remove accidentally committed file"
```

---

## 18. Git Branching Strategies

### A) Gitflow
Classic strategy with long-lived branches:
- `main` — production code only
- `develop` — integration branch
- `feature/*` — new features
- `release/*` — release preparation
- `hotfix/*` — urgent production fixes

### B) GitHub Flow (Recommended for DevOps)
Simpler, faster:
- `main` — always deployable
- `feature/*` — short-lived feature branches
- Create PR → review → merge to main → deploy

### C) Trunk Based Development
- Everyone commits directly to `main` (trunk)
- Very short-lived branches (hours, not days)
- Heavy use of feature flags
- Used by high-velocity teams like Google

---

## 19. Pull Request (PR) Workflow

```bash
# 1. Create feature branch
git switch -c feature-payment

# 2. Make changes and commit
git add .
git commit -m "Add payment gateway"

# 3. Push to remote
git push -u origin feature-payment

# 4. Create PR on GitHub/GitLab/Azure Repos
# — Add description of what changed and why
# — Link to task/ticket (in your Azure DevOps project you used PR templates)
# — Request reviewers

# 5. After review and approval — merge to main

# 6. Delete feature branch
git branch -d feature-payment
git push origin --delete feature-payment
```

---

## 20. Common Git Interview Questions

**Q: What is HEAD in Git?**
HEAD is a pointer to the current commit you're on. Usually points to the tip of your current branch. When you checkout a branch, HEAD moves to that branch's latest commit.

**Q: What is detached HEAD?**
When HEAD points directly to a commit instead of a branch. Happens when you `git checkout <commit-id>`. Any commits made in detached HEAD state can be lost. Create a branch to save work: `git switch -c new-branch`

**Q: Difference between git pull and git fetch?**
`git fetch` downloads changes but doesn't merge. `git pull` downloads AND merges. Use fetch when you want to review changes before merging.

**Q: How do you squash commits?**
```bash
git rebase -i HEAD~3    # interactively squash last 3 commits
# change 'pick' to 'squash' for commits to combine
```

**Q: How do you find which commit introduced a bug?**
```bash
git bisect start
git bisect bad              # current commit is bad
git bisect good <commit-id> # last known good commit
# Git checks out commits between — you test each one
git bisect good/bad         # mark each until bug is found
git bisect reset            # end bisect
```

---

## 21. Quick Reference — Most Used Git Commands

```bash
# DAILY WORKFLOW
git status                          # check what's changed
git add .                           # stage all changes
git commit -m "message"             # commit
git push origin branch-name         # push to remote
git pull origin main                # get latest changes

# BRANCHING
git switch -c feature-name          # create and switch to new branch
git switch main                     # go back to main
git merge feature-name              # merge feature into current branch
git branch -d feature-name          # delete branch after merge

# UNDOING
git restore filename                # discard working directory changes
git reset HEAD filename             # unstage a file
git reset --soft HEAD~1             # undo last commit, keep changes staged
git reset --hard HEAD~1             # undo last commit, DELETE changes
git revert <commit-id>              # safely undo pushed commit

# REMOTE
git remote -v                       # view remotes
git fetch origin                    # download without merging
git pull origin main                # download and merge
git push origin branch-name         # upload to remote
git clone <url>                     # copy remote repo locally

# INSPECTION
git log --oneline --graph           # visual history
git diff                            # see unstaged changes
git show <commit-id>                # see commit details
git blame filename                  # who changed each line

# ADVANCED
git stash                           # save work temporarily
git stash pop                       # restore saved work
git cherry-pick <commit-id>         # apply specific commit
git rebase main                     # rebase onto main
git tag -a v1.0.0 -m "Release"     # create release tag
```

---
---


---
# SECTION 6: LINUX — COMPLETE GUIDE

> Flow: Introduction → Distributions → Structure → Shell → File System → Commands → Users & Groups → Permissions → Compression → Filters → Networking → Advanced

---

## 1. What is Linux?

**Definition:**
Linux is a free, open-source Unix-like operating system kernel created by Linus Torvalds in 1991. It is the foundation of most servers, cloud infrastructure, containers, and DevOps tooling in the world.

**Key Features:**
- **Open Source** — source code is freely available, anyone can modify and distribute
- **Multi-user** — multiple users can log in and work simultaneously
- **Multi-tasking** — runs multiple processes at the same time
- **Secure** — strong permission model, less vulnerable to viruses
- **Stable** — servers run for years without rebooting
- **Portable** — runs on almost any hardware
- **Shell/CLI** — powerful command-line interface for automation
- **Free** — no licensing cost (huge for DevOps at scale)

**Why DevOps uses Linux:**
- Most cloud servers (AWS EC2, Azure VMs) run Linux
- Docker containers use Linux kernel
- Most DevOps tools (Jenkins, Kubernetes, Terraform) run natively on Linux
- Shell scripting enables powerful automation

---

## 2. Linux Distributions (Distros)

A Linux distribution = Linux kernel + package manager + default software + UI

| Distribution | Package Manager | Used For |
|---|---|---|
| Ubuntu | apt | Most popular, DevOps, beginners |
| RHEL (Red Hat) | yum / dnf | Enterprise production servers |
| CentOS | yum / dnf | Free RHEL alternative (deprecated) |
| Amazon Linux | yum / dnf | AWS EC2 instances |
| Debian | apt | Stable servers |
| Alpine | apk | Docker base images (tiny, ~5MB) |
| Kali Linux | apt | Security/penetration testing |
| Fedora | dnf | Cutting edge features |

> **For your resume:** You used Ubuntu and RHEL — mention both in interviews.

---

## 3. Linux Architecture / Structure

```
Hardware (CPU, RAM, Disk, Network)
         ↑
       Kernel  (core of OS — manages hardware, memory, processes)
         ↑
   System Libraries (glibc, etc.)
         ↑
      Shell  (command interpreter — bash, sh, zsh)
         ↑
   Applications / User Programs
         ↑
       User
```

**Components explained:**

- **Kernel** — the brain of Linux. Manages CPU, memory, I/O, processes, networking. You never interact with it directly.
- **Shell** — the interface between you and the kernel. You type commands → shell interprets → kernel executes.
- **System Libraries** — pre-written functions that programs use to talk to the kernel.
- **User Space** — where all applications run (your programs, services, tools).

---

## 4. Linux Shell

**What is a Shell?**
A shell is a command-line interpreter. You type commands, it passes them to the kernel for execution.

**Types of Shells:**
| Shell | Description |
|---|---|
| bash | Bourne Again Shell — most common, default on Ubuntu/RHEL |
| sh | Original Bourne Shell |
| zsh | Extended bash with better features, popular on Mac |
| fish | User-friendly shell with autocomplete |
| ksh | Korn Shell — used in some enterprise environments |

**Check your shell:**
```bash
echo $SHELL          # shows current shell path
echo $0              # shows current shell name
cat /etc/shells      # list all installed shells
chsh -s /bin/zsh     # change default shell
```

**Shell Prompt:**
```
akhil@server:~$
  │      │    │ └── $ = normal user, # = root user
  │      │    └──── ~ = home directory
  │      └───────── hostname
  └──────────────── username
```

---

## 5. Linux File System Structure

Everything in Linux is a file. The filesystem starts from root `/`.

```
/                    ← Root — top of entire filesystem
├── bin/             ← Essential binaries (ls, cp, mv, cat)
├── sbin/            ← System binaries (only root uses: fdisk, mount)
├── etc/             ← Configuration files (nginx.conf, passwd, hosts)
├── home/            ← User home directories (/home/akhil)
├── root/            ← Root user's home directory
├── var/             ← Variable data (logs, databases, mail)
│   └── log/         ← System and application logs
├── tmp/             ← Temporary files (cleared on reboot)
├── usr/             ← User programs and utilities
│   ├── bin/         ← Most user commands
│   └── local/       ← Locally installed software
├── opt/             ← Optional/third-party software
├── dev/             ← Device files (disks, terminals)
├── proc/            ← Virtual filesystem — running processes info
├── sys/             ← Virtual filesystem — kernel/hardware info
├── mnt/             ← Temporary mount points
├── media/           ← Removable media (USB, CD)
├── boot/            ← Boot loader files (kernel, grub)
└── lib/             ← Shared libraries
```

**Key directories to remember:**
- `/etc` — ALL config files live here
- `/var/log` — ALL logs live here
- `/home` — user files
- `/tmp` — temporary, cleared on reboot
- `/proc` — real-time system info (not real files)

---

## 6. Types of File Systems

| File System | Description | Used On |
|---|---|---|
| ext4 | Most common Linux filesystem, journaling | Ubuntu, Debian EC2 |
| xfs | High performance, large files | RHEL, Amazon Linux EC2 |
| btrfs | Modern, snapshots, RAID support | Advanced Linux |
| NTFS | Windows filesystem | Windows (readable on Linux) |
| FAT32 | Universal, USB drives | USB drives |
| tmpfs | In-memory filesystem | /tmp on modern Linux |
| NFS | Network File System — share files over network | Shared storage |
| EFS | AWS Elastic File System (NFS-based) | AWS shared storage |

---

## 7. Absolute Path vs Relative Path

**Absolute Path:**
- Always starts from root `/`
- Full path regardless of where you are
- Example: `/home/akhil/projects/app.js`

**Relative Path:**
- Starts from your current location
- Uses `.` (current dir) and `..` (parent dir)
- Example: `./projects/app.js` or `../etc/nginx.conf`

```bash
# You are in /home/akhil/
cd /etc/nginx          # absolute — goes from root
cd ../etc/nginx        # relative — goes up one level then to etc/nginx
cd ./projects          # relative — goes into projects in current dir

# Special symbols
.     # current directory
..    # parent directory
~     # home directory of current user
-     # previous directory
/     # root directory

# Examples
cd ~                   # go to home directory
cd -                   # go to previous directory
cd ../..               # go up two levels
```

---

## 8. File System Commands

### Navigation
```bash
pwd                          # print working directory (where am I?)
ls                           # list files
ls -l                        # long format (permissions, owner, size, date)
ls -a                        # show hidden files (starting with .)
ls -la                       # long format + hidden files
ls -lh                       # human readable file sizes
ls -lt                       # sort by modification time
ls -R                        # list recursively
```

### Create Files and Directories
```bash
touch filename.txt           # create empty file or update timestamp
touch file1 file2 file3      # create multiple files
mkdir dirname                # create directory
mkdir -p a/b/c               # create nested directories (parents)
mkdir -p project/{src,tests,docs}  # create multiple subdirs at once
```

### Copy — cp
```bash
cp file1 file2               # copy file1 to file2
cp file1 /path/to/dir/       # copy file to directory
cp -r dir1 dir2              # copy directory recursively
cp -p file1 file2            # copy and preserve permissions/timestamps
cp -i file1 file2            # interactive — ask before overwrite
cp -v file1 file2            # verbose — show what's being copied
cp *.txt /backup/            # copy all txt files to backup
```

### Move / Rename — mv
```bash
mv file1 file2               # rename file1 to file2
mv file1 /path/to/dir/       # move file to directory
mv dir1 dir2                 # rename directory
mv -i file1 file2            # ask before overwrite
mv -v file1 file2            # verbose
mv *.log /var/log/archive/   # move all log files
```

### Delete — rm
```bash
rm filename                  # delete file
rm -i filename               # ask before delete
rm -f filename               # force delete, no prompt
rm -r dirname                # delete directory recursively
rm -rf dirname               # force delete directory (DANGEROUS — no undo)
rm *.tmp                     # delete all .tmp files
```

### View File Content
```bash
cat filename                 # print entire file
cat -n filename              # with line numbers
less filename                # scroll through file (q to quit)
more filename                # page through file
head filename                # first 10 lines
head -n 20 filename          # first 20 lines
tail filename                # last 10 lines
tail -n 20 filename          # last 20 lines
tail -f /var/log/syslog      # follow log in real time (VERY useful for DevOps)
```

### File Information
```bash
file filename                # what type of file is it?
stat filename                # detailed file info (size, permissions, timestamps)
wc filename                  # count lines, words, characters
wc -l filename               # count lines only
du -sh dirname               # disk usage of directory (human readable)
du -sh *                     # disk usage of all items in current dir
df -h                        # disk space of all mounted filesystems
```

### Links
```bash
ln file1 hardlink            # create hard link (same inode)
ln -s file1 symlink          # create symbolic (soft) link (like a shortcut)
ls -l                        # symlinks shown with ->
readlink symlink             # show where symlink points
```

---

## 9. How to Add a Volume to an EC2 Instance

This is a common DevOps task — adding extra storage to your EC2 instance.

### Step 1 — Create and Attach EBS Volume (AWS Console or CLI)
```bash
# Using AWS CLI:
aws ec2 create-volume --size 20 --availability-zone us-east-1a --volume-type gp3
aws ec2 attach-volume --volume-id vol-xxxxxxxx --instance-id i-xxxxxxxx --device /dev/xvdf
```

### Step 2 — SSH into your EC2 instance and verify disk is attached
```bash
lsblk                        # list all block devices — you should see xvdf
fdisk -l                     # detailed disk info
```

### Step 3 — Format the Volume with a File System
```bash
mkfs.ext4 /dev/xvdf          # format with ext4
# OR
mkfs.xfs /dev/xvdf           # format with xfs (for RHEL/Amazon Linux)
```

### Step 4 — Create a Mount Point and Mount
```bash
mkdir /data                  # create directory to mount to
mount /dev/xvdf /data        # mount volume to /data
df -h                        # verify it's mounted
```

### Step 5 — Make it Persistent (survive reboots)
```bash
# Get UUID of the volume
blkid /dev/xvdf
# Output: /dev/xvdf: UUID="abc123..." TYPE="ext4"

# Add to /etc/fstab for auto-mount on reboot
echo "UUID=abc123...  /data  ext4  defaults,nofs  0  2" >> /etc/fstab

# Test fstab entry
mount -a                     # mount all entries in fstab
df -h                        # verify
```

### Unmount
```bash
umount /data                 # unmount volume
umount -l /data              # lazy unmount (if busy)
```

---

## 10. System Commands

### System Information
```bash
uname -a                     # all system info (kernel, hostname, arch)
uname -r                     # kernel version only
hostname                     # show hostname
hostnamectl                  # detailed hostname and OS info
hostnamectl set-hostname newname   # change hostname permanently
cat /etc/os-release          # OS details (name, version)
lscpu                        # CPU info
free -h                      # RAM usage (human readable)
uptime                       # how long system has been running
whoami                       # current logged in user
id                           # user ID, group ID, groups
w                            # who is logged in and what they're doing
last                         # login history
```

### Date and Time — timedatectl
```bash
date                         # current date and time
date "+%Y-%m-%d %H:%M:%S"   # formatted date
timedatectl                  # detailed time info including timezone
timedatectl list-timezones   # list all timezones
timedatectl set-timezone Asia/Kolkata   # set timezone (for India)
timedatectl set-ntp true     # enable NTP time sync
hwclock                      # hardware clock time
```

### Process Management
```bash
ps                           # processes of current terminal
ps aux                       # all running processes (a=all, u=user, x=no terminal)
ps aux | grep nginx          # find specific process
top                          # live process monitor (q to quit)
htop                         # better live monitor (install separately)
kill PID                     # send SIGTERM (graceful stop) to process
kill -9 PID                  # send SIGKILL (force stop) — cannot be ignored
kill -15 PID                 # send SIGTERM explicitly
killall nginx                # kill all processes named nginx
pkill nginx                  # kill by name pattern
pgrep nginx                  # find PID of process by name
nohup command &              # run command that survives logout
jobs                         # list background jobs
bg %1                        # put job 1 in background
fg %1                        # bring job 1 to foreground
```

### Service Management — systemctl
```bash
systemctl start nginx        # start service
systemctl stop nginx         # stop service
systemctl restart nginx      # restart service
systemctl reload nginx       # reload config without restart
systemctl status nginx       # check service status
systemctl enable nginx       # start on boot
systemctl disable nginx      # don't start on boot
systemctl is-active nginx    # is it running?
systemctl is-enabled nginx   # is it enabled on boot?
systemctl list-units --type=service   # list all services
journalctl -u nginx          # view logs for specific service
journalctl -u nginx -f       # follow logs for service
journalctl -n 50             # last 50 log lines
```

### Package Management
```bash
# Ubuntu/Debian (apt)
apt update                   # update package list
apt upgrade                  # upgrade all packages
apt install nginx            # install package
apt remove nginx             # remove package
apt purge nginx              # remove package + config files
apt search nginx             # search for package
dpkg -l                      # list installed packages

# RHEL/CentOS/Amazon Linux (yum/dnf)
yum update                   # update all packages
yum install nginx            # install package
yum remove nginx             # remove package
yum search nginx             # search package
yum list installed           # list installed packages
dnf install nginx            # same but newer (dnf replaces yum)
```

---

## 11. User Management Commands

**Linux has three types of users:**
- **Root** — superuser, UID 0, full access
- **System users** — created by services (nginx, mysql), UID 1-999
- **Regular users** — human users, UID 1000+

```bash
# User info files
cat /etc/passwd              # list of all users (username:x:UID:GID:info:home:shell)
cat /etc/shadow              # encrypted passwords (root only)

# Create user
useradd akhil                          # create user (no home dir by default on some distros)
useradd -m akhil                       # create user WITH home directory
useradd -m -s /bin/bash akhil          # with home dir and bash shell
useradd -m -u 1500 akhil              # with specific UID
useradd -m -g devops akhil            # with primary group
useradd -m -G docker,sudo akhil       # with supplementary groups

# Set/change password
passwd akhil                           # set password for user
passwd                                 # change your own password
passwd -l akhil                        # lock user account
passwd -u akhil                        # unlock user account
passwd -e akhil                        # force password change on next login

# Modify user
usermod -s /bin/zsh akhil             # change shell
usermod -d /home/newdir akhil         # change home directory
usermod -aG docker akhil              # add user to docker group (a = append, G = group)
usermod -aG sudo akhil                # give user sudo access
usermod -L akhil                      # lock user

# Delete user
userdel akhil                          # delete user (keeps home dir)
userdel -r akhil                       # delete user AND home directory

# Switch user
su akhil                               # switch to akhil (need akhil's password)
su -                                   # switch to root
sudo command                           # run single command as root
sudo su                                # become root using your password
sudo -u akhil command                  # run command as another user

# View who is logged in
who                                    # logged in users
w                                      # logged in users + what they're doing
id akhil                               # show UID, GID, groups of user
finger akhil                           # user info (if installed)
```

---

## 12. Group Management Commands

**Groups** allow you to manage permissions for multiple users at once.

```bash
# Group info file
cat /etc/group               # list all groups (groupname:x:GID:members)

# Create group
groupadd devops              # create group
groupadd -g 2000 devops      # create group with specific GID

# Modify group
groupmod -n newname devops   # rename group
groupmod -g 2001 devops      # change GID

# Delete group
groupdel devops              # delete group

# Add/remove user from group
usermod -aG devops akhil     # add akhil to devops group
gpasswd -a akhil devops      # add akhil to devops group
gpasswd -d akhil devops      # remove akhil from devops group

# View groups
groups                       # groups current user belongs to
groups akhil                 # groups a specific user belongs to
id akhil                     # UID, GID, all groups

# Primary vs Secondary groups
# Primary group: default group assigned when user creates files
# Secondary groups: additional groups for extra permissions
```

---

## 13. File Permissions

**Every file has three permission sets:**
```
-rwxrwxrwx  1  akhil  devops  4096  Jan 1  file.txt
│└──┘└──┘└──┘
│  │   │   └── others (everyone else)
│  │   └─────── group
│  └─────────── owner (user)
└────────────── file type (- = file, d = directory, l = symlink)
```

**Permission types:**
| Symbol | Number | Meaning | On File | On Directory |
|---|---|---|---|---|
| r | 4 | read | view content | list files |
| w | 2 | write | modify content | create/delete files |
| x | 1 | execute | run as program | enter directory (cd) |
| - | 0 | no permission | — | — |

**Numeric (Octal) representation:**
```
rwx = 4+2+1 = 7
rw- = 4+2+0 = 6
r-x = 4+0+1 = 5
r-- = 4+0+0 = 4
--- = 0+0+0 = 0

# Examples:
755 = rwxr-xr-x  (owner: all, group: read+execute, others: read+execute)
644 = rw-r--r--  (owner: read+write, group: read, others: read)
600 = rw-------  (owner: read+write, nobody else)
777 = rwxrwxrwx  (everyone full access — DANGEROUS, avoid in production)
```

### chmod — Change Permissions
```bash
# Numeric mode
chmod 755 script.sh          # rwxr-xr-x
chmod 644 config.txt         # rw-r--r--
chmod 600 private.key        # rw------- (SSH keys must be 600)
chmod 777 file               # AVOID in production
chmod -R 755 /var/www/       # recursive — apply to all files in directory

# Symbolic mode
chmod u+x script.sh          # add execute for owner (u=user, g=group, o=others, a=all)
chmod g+w file.txt           # add write for group
chmod o-r file.txt           # remove read for others
chmod a+r file.txt           # add read for everyone
chmod u=rwx,g=rx,o=r file   # set exact permissions
```

### chown — Change Owner
```bash
chown akhil file.txt             # change owner to akhil
chown akhil:devops file.txt      # change owner AND group
chown :devops file.txt           # change group only
chown -R akhil:devops /var/www/  # recursive change
```

### chgrp — Change Group
```bash
chgrp devops file.txt            # change group of file
chgrp -R devops /project/        # recursive
```

### umask — Default Permission Mask
```bash
umask                            # show current umask (usually 022)
umask 022                        # set umask
# umask 022 means new files get 644, new directories get 755
# 666 (file default) - 022 = 644
# 777 (dir default)  - 022 = 755
```

### Special Permissions
```bash
# SUID (Set User ID) — run file as owner, not as executor
chmod u+s script.sh          # sets SUID
chmod 4755 script.sh         # numeric

# SGID (Set Group ID) — files inherit group of directory
chmod g+s /shared/           # sets SGID on directory
chmod 2755 /shared/          # numeric

# Sticky Bit — only owner can delete their files in shared dir (like /tmp)
chmod +t /shared/            # sets sticky bit
chmod 1777 /tmp              # numeric (t shown as T if no execute)

# View special permissions
ls -l                        # s in execute position = SUID/SGID, t = sticky
```

---

## 14. ACL — setfacl and getfacl

**What is ACL?**
Standard Linux permissions only allow one owner and one group per file. ACL (Access Control List) gives you fine-grained control — set different permissions for multiple users and groups on the same file.

```bash
# Install ACL if needed
apt install acl              # Ubuntu
yum install acl              # RHEL

# Check if ACL is supported
mount | grep acl             # look for 'acl' in mount options

# getfacl — view ACL of a file
getfacl filename.txt
# Output:
# file: filename.txt
# owner: akhil
# group: devops
# user::rw-
# group::r--
# other::r--

# setfacl — set ACL
setfacl -m u:john:rwx file.txt       # give john rwx on file
setfacl -m u:jane:r-- file.txt       # give jane read only
setfacl -m g:qa:rx /testdir/         # give qa group rx on directory
setfacl -R -m u:john:rwx /project/  # recursive ACL
setfacl -x u:john file.txt           # remove ACL for john
setfacl -b file.txt                  # remove ALL ACLs from file

# Default ACL (inherited by new files in directory)
setfacl -d -m u:john:rwx /shared/   # any new file in /shared gets john's ACL

# Mask — limits effective permissions
setfacl -m m:rx file.txt            # set mask to rx (limits group + named users)
```

---

## 15. File Compression and Archiving

### tar — Tape Archive (most common in Linux)
```bash
# Create archive
tar -cvf archive.tar files/          # create tar (c=create, v=verbose, f=file)
tar -czvf archive.tar.gz files/      # create compressed tar.gz (z=gzip)
tar -cjvf archive.tar.bz2 files/     # create compressed tar.bz2 (j=bzip2)
tar -cJvf archive.tar.xz files/      # create compressed tar.xz (J=xz)

# Extract archive
tar -xvf archive.tar                 # extract tar
tar -xzvf archive.tar.gz             # extract tar.gz
tar -xzvf archive.tar.gz -C /path/  # extract to specific directory

# View contents without extracting
tar -tvf archive.tar                 # list contents

# Add to existing archive
tar -rvf archive.tar newfile.txt

# Memory trick: c=create, x=extract, t=list, v=verbose, f=filename, z=gzip
```

### gzip / gunzip
```bash
gzip file.txt                        # compress — creates file.txt.gz, removes original
gzip -k file.txt                     # compress, keep original
gzip -d file.txt.gz                  # decompress
gunzip file.txt.gz                   # decompress (same as gzip -d)
gzip -l file.txt.gz                  # show compression stats
gzip -9 file.txt                     # maximum compression
```

### zip / unzip
```bash
zip archive.zip file1 file2         # zip files
zip -r archive.zip folder/          # zip directory recursively
unzip archive.zip                   # extract zip
unzip archive.zip -d /path/         # extract to specific directory
unzip -l archive.zip                # list contents
```

### Other compression
```bash
bzip2 file.txt                      # compress with bzip2 (better ratio, slower)
bunzip2 file.txt.bz2                # decompress
xz file.txt                         # compress with xz (best ratio, slowest)
unxz file.txt.xz                    # decompress
```

---

## 16. Filter Commands and Regular Expressions

### grep — Search Text
```bash
grep "pattern" file.txt              # search for pattern in file
grep -i "pattern" file.txt           # case insensitive
grep -r "pattern" /var/log/          # recursive search in directory
grep -n "pattern" file.txt           # show line numbers
grep -v "pattern" file.txt           # invert — show lines that DON'T match
grep -c "pattern" file.txt           # count matching lines
grep -l "pattern" *.txt              # list files that contain pattern
grep -w "word" file.txt              # match whole word only
grep -A 3 "pattern" file.txt         # show 3 lines After match
grep -B 3 "pattern" file.txt         # show 3 lines Before match
grep -E "pattern1|pattern2" file     # extended regex (OR)
grep "^start" file.txt               # lines starting with "start"
grep "end$" file.txt                 # lines ending with "end"
grep "^$" file.txt                   # empty lines

# Real DevOps examples:
grep "ERROR" /var/log/app.log              # find errors in log
grep -i "failed" /var/log/syslog           # find failures
ps aux | grep nginx                         # find nginx process
cat /etc/passwd | grep "/bin/bash"          # users with bash shell
```

### Regular Expressions (Regex) Quick Reference
```
.       any single character
*       zero or more of previous
+       one or more of previous (use with -E)
?       zero or one of previous (use with -E)
^       start of line
$       end of line
[]      character class [abc] = a, b, or c
[^]     negated class [^abc] = not a, b, or c
|       OR (use with -E)
\       escape special character
{n}     exactly n times
{n,m}   between n and m times

# Examples:
grep "^[0-9]" file           # lines starting with digit
grep "[0-9]\{3\}" file       # exactly 3 digits
grep -E "error|fail" file    # lines with error OR fail
grep "\." file               # literal dot
```

### awk — Pattern Scanning and Processing
```bash
awk '{print $1}' file.txt           # print first column
awk '{print $1, $3}' file.txt       # print columns 1 and 3
awk -F: '{print $1}' /etc/passwd    # use : as delimiter, print first field
awk 'NR==5' file.txt                # print line 5
awk 'NR>=5 && NR<=10' file.txt      # print lines 5 to 10
awk '/pattern/ {print}' file        # print lines matching pattern
awk '{print NR, $0}' file           # print with line numbers
awk '{sum+=$1} END {print sum}' f   # sum first column
df -h | awk '{print $1, $5}'        # print disk name and usage %

# Real example — get usernames from /etc/passwd
awk -F: '{print $1}' /etc/passwd
```

### sed — Stream Editor
```bash
sed 's/old/new/' file.txt            # replace first occurrence per line
sed 's/old/new/g' file.txt           # replace ALL occurrences
sed 's/old/new/gi' file.txt          # replace all, case insensitive
sed -i 's/old/new/g' file.txt        # edit file IN PLACE (modifies actual file)
sed -i.bak 's/old/new/g' file.txt    # in place with backup (.bak)
sed '5d' file.txt                    # delete line 5
sed '/pattern/d' file.txt            # delete lines matching pattern
sed -n '5,10p' file.txt              # print lines 5 to 10 only
sed '5i\new line' file.txt           # insert line before line 5
sed '5a\new line' file.txt           # append line after line 5
sed 's/^/prefix/' file.txt           # add prefix to every line
sed 's/$/ suffix/' file.txt          # add suffix to every line

# Real DevOps example — update config file
sed -i 's/port=8080/port=80/' /etc/app.conf
```

### cut — Cut Columns from Text
```bash
cut -d: -f1 /etc/passwd             # cut field 1 using : as delimiter
cut -d, -f2,4 data.csv              # cut fields 2 and 4 from CSV
cut -c1-10 file.txt                 # cut first 10 characters
cut -d' ' -f1 file.txt              # cut first word
```

### sort — Sort Lines
```bash
sort file.txt                       # alphabetical sort
sort -r file.txt                    # reverse sort
sort -n file.txt                    # numerical sort
sort -u file.txt                    # sort and remove duplicates
sort -k2 file.txt                   # sort by second column
sort -t: -k3 -n /etc/passwd         # sort passwd by UID (field 3, numeric)
```

### uniq — Remove Duplicates
```bash
uniq file.txt                       # remove consecutive duplicates
uniq -c file.txt                    # count occurrences
uniq -d file.txt                    # show only duplicates
sort file.txt | uniq                # sort first, then remove all duplicates
sort file.txt | uniq -c | sort -rn  # count and sort by frequency
```

### tr — Translate Characters
```bash
tr 'a-z' 'A-Z' < file.txt          # lowercase to uppercase
tr -d '\n' < file.txt              # remove newlines
tr -s ' ' < file.txt               # squeeze multiple spaces into one
echo "hello" | tr 'a-z' 'A-Z'     # HELLO
```

### wc — Word Count
```bash
wc file.txt                        # lines, words, characters
wc -l file.txt                     # count lines only
wc -w file.txt                     # count words only
wc -c file.txt                     # count bytes
ls | wc -l                         # count files in directory
```

---

## 17. Find and Locate Commands

### find — Search Files in Real Time
```bash
# Basic find
find /path -name "filename"          # find by exact name
find /path -name "*.log"             # find by pattern
find /path -iname "*.Log"            # case insensitive name
find . -name "*.txt"                 # find in current directory

# Find by type
find /path -type f                   # files only
find /path -type d                   # directories only
find /path -type l                   # symbolic links only

# Find by size
find / -size +100M                   # files larger than 100MB
find / -size -1k                     # files smaller than 1KB
find / -size 50M                     # files exactly 50MB

# Find by time
find / -mtime -7                     # modified in last 7 days
find / -mtime +30                    # modified more than 30 days ago
find / -atime -1                     # accessed in last 24 hours
find / -newer file.txt               # files newer than file.txt

# Find by permissions
find / -perm 777                     # files with exactly 777
find / -perm /u+s                    # files with SUID set

# Find by owner
find /home -user akhil               # files owned by akhil
find /home -group devops             # files owned by devops group

# Find and execute action
find /tmp -name "*.tmp" -delete      # find and delete
find /var/log -name "*.log" -exec ls -lh {} \;   # find and run ls
find . -name "*.txt" -exec grep "error" {} \;    # find txt files and grep inside them

# Real DevOps examples:
find / -name "nginx.conf" 2>/dev/null          # find nginx config
find /var/log -name "*.log" -mtime +7 -delete  # delete logs older than 7 days
find / -perm /u+s -type f 2>/dev/null          # find all SUID files (security check)
```

### locate — Fast File Search (uses database)
```bash
locate filename                      # fast search using pre-built database
locate "*.conf"                      # search by pattern
locate -i filename                   # case insensitive
locate -c filename                   # count results only
locate -n 10 filename                # show only 10 results
```

### updatedb — Update locate Database
```bash
updatedb                             # update the locate database (run as root)
# locate uses a database built by updatedb — run this before locate if files are new
# updatedb runs automatically as a cron job daily
```

---

## 18. Piping and Redirection

### Piping — | (pass output of one command to another)
```bash
# Pipe takes stdout of left command and feeds it as stdin to right command
ls -l | grep ".txt"                  # list files, filter for .txt
ps aux | grep nginx                  # find nginx processes
cat /etc/passwd | grep "/bin/bash"   # users with bash shell
df -h | grep "/dev/xvda"            # find specific disk
cat access.log | grep "ERROR" | wc -l   # count errors in log
cat /etc/passwd | cut -d: -f1 | sort    # sorted list of usernames
ps aux | sort -k3 -rn | head -5     # top 5 CPU-consuming processes
```

### Redirection
```bash
# Output redirection
command > file.txt              # redirect stdout to file (OVERWRITES)
command >> file.txt             # redirect stdout to file (APPENDS)
command 2> error.txt            # redirect stderr to file
command 2>> error.txt           # append stderr to file
command > output.txt 2>&1       # redirect both stdout and stderr to file
command &> file.txt             # redirect both (shorthand)
command > /dev/null             # discard output (send to null)
command > /dev/null 2>&1        # discard all output

# Input redirection
command < file.txt              # use file as input
mysql -u root -p dbname < dump.sql   # import SQL dump

# Here document
cat << EOF > file.txt
This is line 1
This is line 2
EOF

# Pipe and redirection combined
grep "ERROR" /var/log/app.log | tail -100 > errors.txt   # save last 100 errors
ps aux | grep nginx | awk '{print $2}' | xargs kill      # kill nginx processes
```

---

## 19. Networking Commands

```bash
# Interface and IP info
ip addr                              # show all network interfaces and IPs
ip addr show eth0                    # show specific interface
ifconfig                             # older command (may need net-tools)
ip link                              # show link layer info
ip link set eth0 up                  # bring interface up
ip link set eth0 down                # bring interface down

# Routing
ip route                             # show routing table
ip route show                        # same
route -n                             # show routing table (older)
ip route add 192.168.1.0/24 via 10.0.0.1   # add static route
ip route del 192.168.1.0/24          # delete route

# DNS
nslookup google.com                  # DNS lookup
dig google.com                       # detailed DNS lookup
dig google.com A                     # lookup A record
dig google.com MX                    # lookup mail records
cat /etc/resolv.conf                 # DNS server config
cat /etc/hosts                       # local hostname resolution

# Connectivity
ping google.com                      # test connectivity (sends ICMP)
ping -c 4 google.com                 # ping 4 times then stop
ping -i 0.5 google.com               # ping every 0.5 seconds
traceroute google.com                # trace path to destination
mtr google.com                       # continuous traceroute

# Ports and Connections
netstat -tulpn                       # listening ports (t=tcp, u=udp, l=listening, p=process, n=numeric)
ss -tulpn                            # same but faster (modern replacement for netstat)
ss -s                                # socket statistics summary
lsof -i :80                          # what process is using port 80
lsof -i :8080                        # check specific port
netstat -an | grep ESTABLISHED       # active connections

# HTTP Requests
curl http://example.com              # basic HTTP GET
curl -I http://example.com           # headers only
curl -X POST -d '{"key":"val"}' -H "Content-Type: application/json" http://api
curl -o file.zip http://example.com/file.zip   # download file
curl -L http://example.com           # follow redirects
curl -u username:password http://api # basic auth
wget http://example.com/file.zip     # download file
wget -r http://example.com           # recursive download

# Firewall — UFW (Ubuntu)
ufw status                           # check firewall status
ufw enable                           # enable firewall
ufw disable                          # disable firewall
ufw allow 22                         # allow SSH
ufw allow 80/tcp                     # allow HTTP
ufw allow 443/tcp                    # allow HTTPS
ufw deny 8080                        # deny port 8080
ufw delete allow 8080               # remove rule
ufw allow from 192.168.1.0/24       # allow from subnet

# Firewall — iptables (lower level)
iptables -L                          # list all rules
iptables -A INPUT -p tcp --dport 80 -j ACCEPT    # allow port 80 in
iptables -A INPUT -p tcp --dport 22 -j ACCEPT    # allow SSH
iptables -A INPUT -j DROP            # drop everything else
iptables -F                          # flush (delete) all rules

# SSH
ssh akhil@192.168.1.10               # SSH to server
ssh -i key.pem ec2-user@ip           # SSH with key (AWS EC2)
ssh -p 2222 user@host                # SSH on custom port
scp file.txt user@host:/path/        # copy file to remote server
scp user@host:/path/file.txt .       # copy file from remote server
scp -r folder/ user@host:/path/      # copy directory to remote
ssh-keygen -t rsa -b 4096            # generate SSH key pair
ssh-copy-id user@host                # copy public key to remote server

# Network performance
iperf3 -s                            # start iperf server
iperf3 -c server-ip                  # test bandwidth to server
nload                                # real-time network traffic monitor
nethogs                              # network usage per process
```

---

## 20. Environment Variables

```bash
# View variables
env                                  # show all environment variables
printenv                             # same
printenv PATH                        # show specific variable
echo $HOME                           # print variable value
echo $PATH                           # print PATH

# Set variables
export MYVAR="hello"                 # set and export variable (available to child processes)
MYVAR="hello"                        # set but NOT exported (only in current shell)
export PATH=$PATH:/new/path          # add to PATH

# Permanent variables — add to ~/.bashrc or /etc/environment
echo 'export MYVAR="hello"' >> ~/.bashrc
source ~/.bashrc                     # reload bashrc

# Common environment variables
$HOME    # user's home directory
$PATH    # directories to search for commands
$USER    # current username
$SHELL   # current shell
$PWD     # current working directory
$EDITOR  # default text editor
$LANG    # system language
```

---

## 21. Text Editors

```bash
# vim (most important for DevOps)
vim filename                 # open file in vim

# vim modes:
# Normal mode  — default, navigate and run commands
# Insert mode  — press 'i' to enter, type text
# Command mode — press ':' to enter commands

# Essential vim commands:
i          # enter insert mode
Esc        # go back to normal mode
:w         # save file
:q         # quit (fails if unsaved changes)
:wq        # save and quit
:q!        # quit without saving (force)
:wq!       # save and quit (force)
dd         # delete current line
yy         # copy (yank) current line
p          # paste
u          # undo
Ctrl+r     # redo
/pattern   # search forward
n          # next search result
:%s/old/new/g  # replace all occurrences in file
gg         # go to top of file
G          # go to bottom of file
:set nu    # show line numbers

# nano (simpler editor)
nano filename                # open file
Ctrl+O                       # save
Ctrl+X                       # exit
Ctrl+W                       # search
Ctrl+K                       # cut line
Ctrl+U                       # paste
```

---

## 22. Log Management

```bash
# Important log files
/var/log/syslog              # general system logs (Ubuntu)
/var/log/messages            # general system logs (RHEL)
/var/log/auth.log            # authentication logs (Ubuntu)
/var/log/secure              # authentication logs (RHEL)
/var/log/kern.log            # kernel logs
/var/log/dmesg               # boot messages
/var/log/nginx/access.log    # nginx access log
/var/log/nginx/error.log     # nginx error log
/var/log/apache2/            # apache logs

# View logs
tail -f /var/log/syslog                  # follow live log
tail -100 /var/log/nginx/error.log       # last 100 lines
grep "ERROR" /var/log/app.log            # filter errors
grep "ERROR" /var/log/app.log | wc -l   # count errors
journalctl -f                            # follow systemd journal
journalctl -u nginx --since "1 hour ago" # nginx logs from last hour
journalctl --since "2024-01-01" --until "2024-01-02"  # date range
```

---

## 23. Shell Scripting Basics

```bash
#!/bin/bash                  # shebang — tells system to use bash

# Variables
NAME="Akhil"
echo "Hello, $NAME"

# Input
read -p "Enter name: " NAME

# Conditions
if [ $NAME == "Akhil" ]; then
    echo "Welcome Akhil"
elif [ $NAME == "John" ]; then
    echo "Welcome John"
else
    echo "Unknown user"
fi

# Loops
for i in 1 2 3 4 5; do
    echo "Number: $i"
done

for file in *.txt; do
    echo "Processing: $file"
done

while [ condition ]; do
    # commands
done

# Functions
greet() {
    echo "Hello, $1"    # $1 = first argument
}
greet "Akhil"

# Exit codes
echo $?          # 0 = success, non-zero = failure
exit 0           # exit script with success
exit 1           # exit script with failure

# Make script executable and run
chmod +x script.sh
./script.sh
bash script.sh
```

---

## 24. Quick Reference — Most Used Linux Commands

```bash
# NAVIGATION
pwd           cd           ls -la        cd ~

# FILE OPERATIONS
touch         mkdir -p     cp -r         mv           rm -rf
cat           less         head -n       tail -f      file

# PERMISSIONS
chmod 755     chown user:group    setfacl -m u:user:rwx    getfacl

# USER MANAGEMENT
useradd -m    passwd        usermod -aG    userdel -r
groupadd      gpasswd -a    groups         id

# PROCESSES
ps aux        top           kill -9       systemctl status
systemctl start/stop/restart/enable

# NETWORKING
ip addr       ping          curl          ss -tulpn
ufw allow     ssh           scp           dig

# SEARCH
grep -r       find / -name  locate        grep -i -n
awk           sed -i        cut           sort | uniq

# COMPRESSION
tar -czvf     tar -xzvf     zip -r        unzip        gzip

# DISK
df -h         du -sh        lsblk         mount        umount
mkfs.ext4     blkid

# LOGS
tail -f       journalctl -u    grep "ERROR"    /var/log/
```

---
---



---

## TOPICS TO ADD NEXT
- [ ] Terraform — complete guide
- [ ] Azure DevOps — complete guide  
- [ ] Ansible — complete guide
- [ ] AWS Scenario-based questions
- [ ] Networking deep dive

---
*Prepared for: Akhil B M | DevOps & Cloud Engineer*
*Keep going — you're doing great!*

---
---

# SECTION 3 ADDITION: DOCKER — EXPANDED GUIDE

> All new content. No duplication with existing Docker section above.

---

## A. VM vs Containers

### Virtual Machine (VM)
A VM is a full computer running inside your computer. It has its own OS, kernel, memory, CPU allocation — everything.

```
┌─────────────────────────────────────┐
│           Your Machine              │
│  ┌──────────────────────────────┐   │
│  │       Hypervisor             │   │
│  │  (VMware, VirtualBox, KVM)   │   │
│  │                              │   │
│  │  ┌──────────┐ ┌──────────┐  │   │
│  │  │   VM 1   │ │   VM 2   │  │   │
│  │  │ Guest OS │ │ Guest OS │  │   │
│  │  │  App A   │ │  App B   │  │   │
│  │  └──────────┘ └──────────┘  │   │
│  └──────────────────────────────┘   │
│         Host OS + Kernel            │
│              Hardware               │
└─────────────────────────────────────┘
```

### Container
A container shares the host OS kernel. It only packages the app and its dependencies — no full OS needed.

```
┌─────────────────────────────────────┐
│           Your Machine              │
│  ┌──────────────────────────────┐   │
│  │       Docker Engine          │   │
│  │                              │   │
│  │  ┌──────────┐ ┌──────────┐  │   │
│  │  │Container1│ │Container2│  │   │
│  │  │  App A   │ │  App B   │  │   │
│  │  │  Libs    │ │  Libs    │  │   │
│  │  └──────────┘ └──────────┘  │   │
│  └──────────────────────────────┘   │
│         Host OS + Kernel            │
│              Hardware               │
└─────────────────────────────────────┘
```

### VM vs Container Comparison

| Feature | Virtual Machine | Container |
|---|---|---|
| **Size** | GBs (full OS) | MBs (just app + libs) |
| **Startup time** | Minutes | Seconds |
| **OS** | Own full OS | Shares host OS kernel |
| **Isolation** | Strong (hardware level) | Good (process level) |
| **Performance** | Slower (overhead) | Near native speed |
| **Portability** | Less portable | Highly portable |
| **Resource usage** | Heavy | Lightweight |
| **Security** | More isolated | Less isolated |
| **Use case** | Full OS needed, strong isolation | Microservices, CI/CD |

**Pros of VMs:**
- Strong isolation — one VM crash doesn't affect others
- Run different OS (Windows VM on Linux host)
- Better security boundaries
- Good for stateful, long-running applications

**Cons of VMs:**
- Heavy — each VM needs full OS (GBs)
- Slow to start
- Wastes resources
- Hard to scale quickly

**Pros of Containers:**
- Lightweight — MBs not GBs
- Start in seconds
- Consistent across environments
- Easy to scale
- Perfect for microservices and CI/CD

**Cons of Containers:**
- Weaker isolation than VMs
- All containers share host kernel — kernel vulnerability affects all
- Stateful apps need extra setup (volumes)
- Networking more complex at scale

---

## B. Docker Architecture (Detailed)

```
┌─────────────────────────────────────────────────────┐
│                  Docker Client                       │
│         (docker build, docker run, docker push)      │
└────────────────────────┬────────────────────────────┘
                         │ REST API
┌────────────────────────▼────────────────────────────┐
│                  Docker Daemon (dockerd)             │
│                                                     │
│  ┌─────────────┐  ┌──────────┐  ┌───────────────┐  │
│  │   Images    │  │Containers│  │    Networks    │  │
│  │  (stored    │  │(running  │  │  (bridge,host, │  │
│  │  locally)   │  │instances)│  │   overlay)     │  │
│  └─────────────┘  └──────────┘  └───────────────┘  │
│                                                     │
│  ┌──────────────────────────────────────────────┐   │
│  │         containerd (container runtime)        │   │
│  └──────────────────────────────────────────────┘   │
└────────────────────────┬────────────────────────────┘
                         │ push/pull
┌────────────────────────▼────────────────────────────┐
│                  Docker Registry                     │
│         (Docker Hub, ECR, ACR, Harbor)               │
└─────────────────────────────────────────────────────┘
```

**Three main components:**
- **Docker Client** — CLI you use. Sends commands to daemon via REST API.
- **Docker Daemon (dockerd)** — background service. Does all the work — builds images, runs containers, manages networks and volumes.
- **Docker Registry** — stores and distributes images.

---

## C. Docker Image — Deep Dive

**What is a Docker Image?**
A Docker image is a read-only template used to create containers. It's built in layers — each instruction in the Dockerfile creates one layer.

```
Layer 4: COPY app files        ← your code
Layer 3: RUN npm install       ← dependencies
Layer 2: WORKDIR /app          ← set working dir
Layer 1: FROM node:18          ← base OS + Node
```

**Image Commands:**
```bash
docker images                          # list all local images
docker images -a                       # include intermediate images
docker pull nginx                      # pull from Docker Hub
docker pull nginx:1.21                 # pull specific version
docker pull myrepo/myapp:1.0          # pull from private registry
docker inspect nginx                   # detailed image info
docker history nginx                   # show layers of image
docker image ls                        # same as docker images
docker image rm nginx                  # remove image
docker rmi nginx                       # same as above
docker rmi -f nginx                    # force remove
docker image prune                     # remove unused images
docker image prune -a                  # remove ALL unused images
docker tag nginx:latest myrepo/nginx:v1  # tag image
docker save nginx > nginx.tar          # save image to file
docker load < nginx.tar                # load image from file
docker export container1 > app.tar     # export container filesystem
docker import app.tar myimage:v1       # import as image
```

---

## D. Dockerfile — All Instructions

```dockerfile
# ─────────────────────────────────────────
# DOCKERFILE COMPLETE INSTRUCTIONS GUIDE
# ─────────────────────────────────────────

# FROM — base image (REQUIRED, must be first)
FROM ubuntu:22.04
FROM node:18-alpine        # alpine = tiny base image
FROM scratch               # empty base (for compiled binaries)

# MAINTAINER — author info (deprecated, use LABEL instead)
MAINTAINER Akhil <akhilbm13@gmail.com>

# LABEL — metadata key-value pairs
LABEL maintainer="akhilbm13@gmail.com"
LABEL version="1.0"
LABEL description="My Node.js App"

# RUN — execute command during BUILD time (creates a layer)
RUN apt-get update && apt-get install -y curl    # combine to reduce layers
RUN npm install
RUN mkdir -p /app/logs

# COPY — copy files from host to image
COPY package.json /app/              # copy specific file
COPY src/ /app/src/                  # copy directory
COPY . /app/                         # copy everything

# ADD — like COPY but with extra powers
ADD app.tar.gz /app/                 # auto-extracts tar files
ADD https://example.com/file /app/   # download from URL
# Rule: Use COPY unless you need ADD's extra features

# WORKDIR — set working directory (creates it if doesn't exist)
WORKDIR /app
# All following commands run from /app

# ENV — set environment variables (available at runtime too)
ENV NODE_ENV=production
ENV PORT=3000
ENV DB_HOST=postgres-service

# ARG — build-time variables (NOT available at runtime)
ARG VERSION=1.0
ARG BUILD_DATE
# Usage: docker build --build-arg VERSION=2.0 .

# EXPOSE — document which port the app listens on (doesn't actually publish)
EXPOSE 3000
EXPOSE 80 443

# VOLUME — create mount point for external volumes
VOLUME ["/data"]
VOLUME /var/log/app

# USER — set user for following RUN/CMD/ENTRYPOINT (security best practice)
RUN useradd -m appuser
USER appuser
# Never run as root in production

# CMD — default command when container starts (can be overridden)
CMD ["node", "app.js"]              # exec form (preferred)
CMD node app.js                     # shell form
CMD ["npm", "start"]

# ENTRYPOINT — main executable (harder to override)
ENTRYPOINT ["node"]                 # exec form
ENTRYPOINT node                     # shell form
# Combined with CMD:
ENTRYPOINT ["node"]
CMD ["app.js"]                      # runs: node app.js
# docker run myimage server.js      # runs: node server.js (CMD overridden)

# HEALTHCHECK — how Docker checks if container is healthy
HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1

# ONBUILD — trigger instructions for child images
ONBUILD COPY . /app
ONBUILD RUN npm install

# STOPSIGNAL — signal to stop container
STOPSIGNAL SIGTERM

# SHELL — change default shell
SHELL ["/bin/bash", "-c"]
```

**Complete Production Dockerfile Example:**
```dockerfile
# Stage 1 - Build
FROM node:18 AS builder
LABEL maintainer="akhilbm13@gmail.com"
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# Stage 2 - Runtime
FROM node:18-alpine
ENV NODE_ENV=production
ENV PORT=3000
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
RUN useradd -m appuser
USER appuser
EXPOSE 3000
HEALTHCHECK --interval=30s CMD curl -f http://localhost:3000/health || exit 1
CMD ["node", "app.js"]
```

---

## E. Docker Registry — Complete Guide

**What is a Docker Registry?**
A registry is a server that stores and distributes Docker images. Think of it like GitHub but for Docker images.

**Types:**
| Registry | Type | URL |
|---|---|---|
| Docker Hub | Public/Private | hub.docker.com |
| Amazon ECR | Private (AWS) | AWS Console |
| Azure ACR | Private (Azure) | Azure Portal |
| GitHub Container Registry | Private | ghcr.io |
| Harbor | Self-hosted | Your server |

**Docker Hub — All Commands:**
```bash
# Login / Logout
docker login                                    # login to Docker Hub
docker login -u akhil -p mypassword            # with credentials
docker login registry.example.com             # login to private registry
docker logout                                  # logout

# Search
docker search nginx                            # search Docker Hub
docker search --filter=stars=100 nginx        # filter by stars

# Pull
docker pull nginx                              # latest tag
docker pull nginx:1.21                         # specific version
docker pull ubuntu:22.04                       # specific OS version

# Tag
docker tag myapp:latest akhil/myapp:1.0       # tag for Docker Hub
docker tag myapp:latest 123456.dkr.ecr.us-east-1.amazonaws.com/myapp:1.0  # for ECR

# Push
docker push akhil/myapp:1.0                   # push to Docker Hub
docker push 123456.dkr.ecr.us-east-1.amazonaws.com/myapp:1.0  # push to ECR

# Login to AWS ECR
aws ecr get-login-password --region us-east-1 | \
  docker login --username AWS --password-stdin \
  123456789.dkr.ecr.us-east-1.amazonaws.com
```

---

## F. Container Lifecycle

```
               docker create
                    ↓
             ┌─────────────┐
             │   CREATED   │ ← container created but not started
             └──────┬──────┘
                    │ docker start
                    ↓
             ┌─────────────┐
             │   RUNNING   │ ← container is executing
             └──────┬──────┘
           ┌────────┴────────┐
           │                 │
    docker pause      docker stop/kill
           │                 │
           ▼                 ▼
    ┌──────────────┐  ┌─────────────┐
    │    PAUSED    │  │   STOPPED   │ ← container stopped
    └──────┬───────┘  └──────┬──────┘
           │                 │
    docker unpause    docker start (restart)
           │                 │
           └────────┬────────┘
                    ↓
             ┌─────────────┐
             │   RUNNING   │
             └─────────────┘
                    
             docker rm → DELETED
```

**Lifecycle Commands:**
```bash
# Create (without starting)
docker create --name mycontainer nginx

# Start
docker start mycontainer

# Run (create + start in one step — most common)
docker run nginx                               # runs in foreground
docker run -d nginx                            # detached (background)
docker run -d --name web nginx                 # with name
docker run -d -p 8080:80 nginx                 # with port mapping
docker run -d -e ENV=production myapp          # with env variable
docker run -d -v myvolume:/data myapp          # with volume
docker run --rm nginx                          # auto-remove when stopped
docker run -it ubuntu bash                     # interactive terminal

# Stop (graceful — sends SIGTERM, waits, then SIGKILL)
docker stop mycontainer
docker stop -t 30 mycontainer                  # wait 30 seconds before kill

# Kill (immediate — sends SIGKILL)
docker kill mycontainer

# Restart
docker restart mycontainer

# Pause / Unpause
docker pause mycontainer
docker unpause mycontainer

# Remove
docker rm mycontainer                          # remove stopped container
docker rm -f mycontainer                       # force remove running container
docker rm $(docker ps -aq)                     # remove ALL stopped containers
docker container prune                         # remove all stopped containers

# View
docker ps                                      # running containers
docker ps -a                                   # all containers (including stopped)
docker ps -q                                   # only IDs

# Inspect and Debug
docker inspect mycontainer                     # full JSON details
docker logs mycontainer                        # logs
docker logs -f mycontainer                     # follow logs
docker logs --tail 50 mycontainer              # last 50 lines
docker exec -it mycontainer bash               # shell inside container
docker exec mycontainer ls /app                # run command without shell
docker top mycontainer                         # processes inside container
docker stats                                   # live resource usage
docker stats mycontainer                       # specific container stats
docker diff mycontainer                        # files changed vs image
docker cp mycontainer:/app/file.txt .          # copy file from container
docker cp file.txt mycontainer:/app/           # copy file to container
```

---

## G. Port Mapping

**Why port mapping?**
Containers run in their own isolated network. Port mapping connects a port on your host machine to a port inside the container.

```
Host Machine          Container
   :8080    ────────▶   :3000
   :8081    ────────▶   :3000  (two containers, same container port)
   :5432    ────────▶   :5432
```

```bash
# -p hostPort:containerPort
docker run -d -p 8080:3000 myapp           # host 8080 → container 3000
docker run -d -p 80:80 nginx               # host 80 → container 80
docker run -d -p 5432:5432 postgres        # database
docker run -d -p 8080:80 -p 8443:443 nginx # multiple ports

# -P (capital P) — publish ALL exposed ports to random host ports
docker run -d -P nginx

# Check port mappings
docker port mycontainer                    # see all port mappings
docker ps                                  # shows ports in output

# Bind to specific host IP
docker run -d -p 127.0.0.1:8080:80 nginx  # only localhost can access
docker run -d -p 0.0.0.0:8080:80 nginx    # any IP can access (default)
```

---

## H. Creating Image from a Running Container

Sometimes you make changes inside a running container and want to save that as a new image.

```bash
# Step 1 — Run a container and make changes
docker run -it ubuntu bash
# Inside container:
apt-get update && apt-get install -y nginx
exit

# Step 2 — Commit container as new image
docker commit container_name myimage:v1
docker commit -m "Added nginx" -a "Akhil" container_name myimage:v1

# Step 3 — Verify
docker images    # you'll see myimage:v1

# Note: This is NOT best practice — always use Dockerfile for reproducibility
# Use commit only for quick debugging or testing
```

---

## I. Full Deployment Workflow — Docker Only

**Scenario:** You have a Node.js app. Deploy it using Docker.

```bash
# ── STEP 1: Clone your code ──
git clone https://github.com/akhil/myapp.git
cd myapp

# ── STEP 2: Write Dockerfile ──
cat > Dockerfile << 'EOF'
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
EOF

# ── STEP 3: Build Docker image ──
docker build -t myapp:1.0 .
docker build -t myapp:1.0 -f Dockerfile.prod .   # specific dockerfile

# ── STEP 4: Test locally ──
docker run -d -p 3000:3000 --name myapp myapp:1.0
curl http://localhost:3000    # verify it works

# ── STEP 5: Tag for Docker Hub ──
docker tag myapp:1.0 akhil/myapp:1.0

# ── STEP 6: Login and Push ──
docker login
docker push akhil/myapp:1.0

# ── STEP 7: On production server — pull and run ──
docker pull akhil/myapp:1.0
docker run -d -p 80:3000 --name myapp akhil/myapp:1.0
```

---

## J. Full Deployment Workflow — Docker + Jenkins Pipeline

**Complete Jenkins Pipeline for Docker:**

```groovy
// Jenkinsfile
pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDS = credentials('docker-hub-credentials')
        IMAGE_NAME = "akhil/myapp"
        IMAGE_TAG = "${BUILD_NUMBER}"     // use Jenkins build number as tag
        SONAR_TOKEN = credentials('sonar-token')
        NEXUS_CREDS = credentials('nexus-credentials')
    }

    stages {

        // ── STAGE 1: Clone Code ──
        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/akhil/myapp.git'
            }
        }

        // ── STAGE 2: Build Code ──
        stage('Build Code') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        // ── STAGE 3: SonarQube Analysis ──
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=myapp \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://sonarqube:9000 \
                        -Dsonar.login=${SONAR_TOKEN}
                    '''
                }
            }
        }

        // ── STAGE 4: Quality Gate ──
        stage('Quality Gate') {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }

        // ── STAGE 5: Upload to Nexus ──
        stage('Upload Artifact to Nexus') {
            steps {
                sh '''
                    curl -u ${NEXUS_CREDS_USR}:${NEXUS_CREDS_PSW} \
                    --upload-file target/myapp.jar \
                    http://nexus:8081/repository/myapp-releases/myapp-${BUILD_NUMBER}.jar
                '''
            }
        }

        // ── STAGE 6: Build Docker Image ──
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                sh "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${IMAGE_NAME}:latest"
            }
        }

        // ── STAGE 7: Push to Docker Hub ──
        stage('Push Docker Image') {
            steps {
                sh '''
                    echo ${DOCKER_HUB_CREDS_PSW} | \
                    docker login -u ${DOCKER_HUB_CREDS_USR} --password-stdin
                    docker push ${IMAGE_NAME}:${IMAGE_TAG}
                    docker push ${IMAGE_NAME}:latest
                '''
            }
        }

        // ── STAGE 8: Deploy Container ──
        stage('Deploy Container') {
            steps {
                sh '''
                    docker stop myapp || true
                    docker rm myapp || true
                    docker pull ${IMAGE_NAME}:${IMAGE_TAG}
                    docker run -d \
                        --name myapp \
                        -p 80:3000 \
                        --restart=always \
                        -e NODE_ENV=production \
                        ${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment successful! App running on port 80"
        }
        failure {
            echo "Pipeline failed! Check logs."
            // Send email/Slack notification
        }
        always {
            sh 'docker image prune -f'    // cleanup unused images
        }
    }
}
```

**Pipeline Flow:**
```
Clone Code → Build Code → SonarQube → Quality Gate → Nexus → Docker Build → Docker Push → Deploy
```

---

## K. Docker Compose — Complete Guide

**What is Docker Compose?**
A tool to define and run multi-container applications using a single YAML file.

### Type 1 — Multiple Containers from Existing Images

```yaml
# docker-compose.yml
version: '3.8'

services:

  # Frontend
  frontend:
    image: nginx:latest
    container_name: frontend
    ports:
      - "80:80"
    volumes:
      - ./frontend:/usr/share/nginx/html
    networks:
      - appnetwork
    depends_on:
      - backend

  # Backend
  backend:
    image: node:18
    container_name: backend
    working_dir: /app
    command: node app.js
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DB_HOST=database
      - DB_PORT=5432
    networks:
      - appnetwork
    depends_on:
      - database

  # Database
  database:
    image: postgres:14
    container_name: database
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - appnetwork

volumes:
  pgdata:          # named volume for database persistence

networks:
  appnetwork:
    driver: bridge
```

### Type 2 — Multiple Containers with Custom Dockerfiles

```yaml
# docker-compose.yml (builds from Dockerfiles)
version: '3.8'

services:

  frontend:
    build:
      context: ./frontend      # folder containing Dockerfile
      dockerfile: Dockerfile   # Dockerfile name
    container_name: frontend
    ports:
      - "80:80"
    networks:
      - appnetwork

  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile.prod    # specific Dockerfile name
      args:
        - NODE_ENV=production         # build arguments
    container_name: backend
    ports:
      - "3000:3000"
    environment:
      - DB_HOST=database
    networks:
      - appnetwork
    depends_on:
      - database

  database:
    image: postgres:14
    container_name: database
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - appnetwork

volumes:
  pgdata:

networks:
  appnetwork:
    driver: bridge
```

**Docker Compose Commands:**
```bash
# Start
docker-compose up                      # start all (foreground)
docker-compose up -d                   # start all (background/detached)
docker-compose up --build              # rebuild images before starting
docker-compose up -d --build           # rebuild + detached

# Stop
docker-compose stop                    # stop containers (keep them)
docker-compose down                    # stop + remove containers
docker-compose down -v                 # stop + remove containers + volumes
docker-compose down --rmi all          # remove containers + images too

# View
docker-compose ps                      # list containers
docker-compose logs                    # all logs
docker-compose logs -f                 # follow all logs
docker-compose logs backend            # specific service logs
docker-compose logs -f backend         # follow specific service

# Scale
docker-compose up -d --scale backend=3  # run 3 backend containers

# Execute
docker-compose exec backend bash       # shell into service
docker-compose exec database psql -U admin  # run command in service

# Build only
docker-compose build                   # build all images
docker-compose build backend           # build specific service

# Pull latest images
docker-compose pull                    # pull all images
```

---

## L. Docker Volumes — Complete Guide

**What is a Docker Volume?**
Volumes provide persistent storage for containers. Data in volumes survives container restarts and deletions.

```
Container (ephemeral)
    ↓ writes to
Volume (persistent) ← survives container deletion
```

### Types of Storage

**1. Named Volume (Managed by Docker — Recommended)**
```bash
# Docker manages where data is stored
docker volume create myvolume
docker run -d -v myvolume:/data myapp
# Data lives in: /var/lib/docker/volumes/myvolume/_data
```

**2. Bind Mount (Host directory)**
```bash
# You control where data lives on host
docker run -d -v /home/akhil/data:/data myapp
docker run -d -v $(pwd):/app myapp    # current directory
```

**3. tmpfs Mount (In-memory, not persistent)**
```bash
docker run -d --tmpfs /tmp myapp      # stored in host memory only
```

**Volume Commands:**
```bash
# Create
docker volume create myvolume
docker volume create --driver local myvolume

# List
docker volume ls

# Inspect
docker volume inspect myvolume
# Shows mountpoint, driver, labels

# Remove
docker volume rm myvolume
docker volume prune                    # remove all unused volumes
docker volume prune -f                 # force (no confirmation)

# Use in run
docker run -d -v myvolume:/app/data myapp           # named volume
docker run -d -v /host/path:/container/path myapp   # bind mount
docker run -d -v myvolume:/data:ro myapp            # read-only volume

# Backup a volume
docker run --rm \
  -v myvolume:/data \
  -v $(pwd):/backup \
  ubuntu tar cvf /backup/backup.tar /data

# Restore a volume
docker run --rm \
  -v myvolume:/data \
  -v $(pwd):/backup \
  ubuntu tar xvf /backup/backup.tar -C /
```

---

## M. Docker Networking — All Types

**What is Docker Networking?**
Docker networking controls how containers communicate with each other and the outside world.

### 1. Bridge Network (Default)
```
Host Machine
├── docker0 (bridge interface, 172.17.0.1)
│   ├── container1 (172.17.0.2)
│   ├── container2 (172.17.0.3)
│   └── container3 (172.17.0.4)
└── eth0 (host network, connected to internet)
```
- Default network for all containers
- Containers on same bridge can communicate by IP
- Containers on custom bridge can communicate by **name**
- Isolated from other bridge networks

```bash
# Default bridge
docker run -d nginx                    # uses default bridge

# Custom bridge (recommended — allows DNS by name)
docker network create mybridge
docker run -d --network mybridge --name web nginx
docker run -d --network mybridge --name app myapp
# Now 'app' can reach 'web' by name: http://web:80
```

### 2. Host Network
```
Host Machine (192.168.1.10)
└── Container (shares host network stack)
    └── Uses host's IP and ports directly
```
- Container uses host's network directly
- No network isolation
- Fastest performance (no NAT overhead)
- Container port = host port (no -p needed)

```bash
docker run -d --network host nginx
# nginx now accessible on host's port 80 directly
# Cannot use -p with host network
```

### 3. None Network
- No networking at all
- Completely isolated container
- Use for maximum security or batch processing

```bash
docker run -d --network none myapp
# Container has no network access
```

### 4. Overlay Network
```
Host 1 (Swarm Manager)          Host 2 (Swarm Worker)
├── container1                   ├── container3
└── container2  ←─── overlay ──▶ └── container4
     (all containers can communicate across hosts)
```
- Used in Docker Swarm for multi-host networking
- Containers on different physical hosts communicate seamlessly
- Encrypted traffic between hosts

```bash
# Create overlay (requires Swarm mode)
docker swarm init
docker network create -d overlay myoverlay
docker service create --network myoverlay nginx
```

### 5. Macvlan Network
- Assigns a real MAC address to container
- Container appears as physical device on network
- Direct connection to physical network
- Used when containers need to be on physical LAN

```bash
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  -o parent=eth0 \
  mymacvlan

docker run -d --network mymacvlan --ip=192.168.1.100 nginx
```

**Networking Commands:**
```bash
# List networks
docker network ls

# Create network
docker network create mynetwork                          # bridge by default
docker network create --driver bridge mybridge
docker network create --driver overlay myoverlay
docker network create --subnet=172.20.0.0/16 mynet     # custom subnet

# Inspect
docker network inspect mynetwork
docker network inspect bridge                            # default bridge info

# Connect/Disconnect container to network
docker network connect mynetwork mycontainer
docker network disconnect mynetwork mycontainer

# Remove
docker network rm mynetwork
docker network prune                                     # remove unused networks

# Run container on specific network
docker run -d --network mynetwork --name web nginx
docker run -d --network mynetwork --name app myapp
# app can reach web using: http://web (by container name)
```

**Network Comparison:**
| Network | Isolation | Communication | Use Case |
|---|---|---|---|
| Bridge | Yes | By IP or name (custom) | Default, single host |
| Host | No | Shares host network | Performance critical |
| None | Complete | No networking | Batch, security |
| Overlay | Yes | Across multiple hosts | Docker Swarm |
| Macvlan | Yes | Direct to physical LAN | Legacy app integration |

---

## N. Multi-Stage Dockerfile (Already in Docker Section above — see Section 3 Q11)

> Refer to Section 3: Q11 — Multi-Stage Dockerfile for complete explanation and example.

---

---
---

# SECTION 7: TERRAFORM — COMPLETE GUIDE

> Infrastructure as Code (IaC) tool by HashiCorp. Write code to create cloud infrastructure.

---

## 1. What is Terraform?

**Definition:**
Terraform is an open-source Infrastructure as Code (IaC) tool by HashiCorp. It lets you define cloud infrastructure (EC2, VPC, S3, etc.) in human-readable configuration files and manage it through code.

**Why Terraform?**
- **Before Terraform:** Click through AWS Console manually to create resources. Hard to reproduce, no version control, error-prone.
- **With Terraform:** Write code once, run it anywhere. Version controlled, repeatable, consistent.

**Key Principle — Desired State:**
You declare WHAT you want (desired state). Terraform figures out HOW to create it and ensures the actual state matches desired state.

```
You write:  "I want 3 EC2 instances"
Terraform:  Checks current state → Creates what's missing → Reports changes
```

---

## 2. How Terraform Works

```
┌─────────────────────────────────────────────────────┐
│                    You (Developer)                   │
│              Write .tf configuration files           │
└────────────────────────┬────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────┐
│                  Terraform Core                      │
│                                                     │
│  ┌─────────────┐      ┌──────────────────────────┐  │
│  │   terraform  │      │    State File            │  │
│  │    plan      │      │  (terraform.tfstate)     │  │
│  │   apply      │      │  tracks what exists      │  │
│  │   destroy    │      └──────────────────────────┘  │
│  └─────────────┘                                    │
└────────────────────────┬────────────────────────────┘
                         │ API calls
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
      ┌───────┐      ┌───────┐      ┌───────┐
      │  AWS  │      │ Azure │      │  GCP  │
      │Provider│     │Provider│     │Provider│
      └───────┘      └───────┘      └───────┘
```

**Terraform Workflow:**
```
Write (.tf files) → Init → Plan → Apply → Destroy
```

1. **Write** — create `.tf` files declaring resources
2. **Init** — download provider plugins
3. **Plan** — preview what will be created/changed/destroyed
4. **Apply** — actually create the infrastructure
5. **Destroy** — tear down everything

---

## 3. Terraform Files

| File | Purpose |
|---|---|
| `main.tf` | Main resource definitions |
| `variables.tf` | Input variable declarations |
| `outputs.tf` | Output value definitions |
| `terraform.tfvars` | Variable values |
| `providers.tf` | Provider configuration |
| `backend.tf` | Remote state configuration |
| `terraform.tfstate` | State file (auto-generated, don't edit) |
| `.terraform/` | Downloaded providers (auto-generated) |
| `.terraform.lock.hcl` | Provider version lock file |

---

## 4. Terraform Commands

```bash
# ── SETUP ──
terraform init                    # initialize — download providers, setup backend
terraform init -upgrade           # upgrade providers to latest versions

# ── PREVIEW ──
terraform plan                    # show what will be created/changed/destroyed
terraform plan -out=tfplan        # save plan to file
terraform plan -var="env=prod"    # pass variable on command line
terraform plan -destroy           # preview destroy

# ── APPLY ──
terraform apply                   # apply changes (asks for confirmation)
terraform apply -auto-approve     # apply without confirmation (CI/CD)
terraform apply tfplan            # apply saved plan
terraform apply -var="env=prod"   # apply with variable

# ── DESTROY ──
terraform destroy                 # destroy all resources (asks confirmation)
terraform destroy -auto-approve   # destroy without confirmation
terraform destroy -target=aws_instance.web  # destroy specific resource

# ── STATE ──
terraform show                    # show current state
terraform state list              # list all resources in state
terraform state show aws_instance.web  # show specific resource state
terraform state rm aws_instance.web    # remove resource from state (without destroying)
terraform state mv aws_instance.old aws_instance.new  # rename in state
terraform refresh                 # sync state with real infrastructure

# ── IMPORT ──
terraform import aws_instance.web i-1234567890  # import existing resource into state

# ── VALIDATE & FORMAT ──
terraform validate                # check configuration syntax
terraform fmt                     # format .tf files
terraform fmt -recursive          # format all files recursively

# ── WORKSPACE ──
terraform workspace list          # list workspaces
terraform workspace new dev       # create new workspace
terraform workspace select prod   # switch workspace
terraform workspace show          # current workspace
terraform workspace delete dev    # delete workspace

# ── OUTPUT ──
terraform output                  # show all outputs
terraform output vpc_id           # show specific output

# ── GRAPH ──
terraform graph                   # generate dependency graph
terraform graph | dot -Tpng > graph.png  # visualize as image
```

---

## 5. Provider Configuration

```hcl
# providers.tf
terraform {
  required_version = ">= 1.0"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"        # any 5.x version
    }
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
  }

  # Remote state in S3 (for teams)
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "prod/terraform.tfstate"
    region = "us-east-1"
  }
}

# AWS Provider
provider "aws" {
  region     = "us-east-1"
  access_key = var.aws_access_key    # from variable
  secret_key = var.aws_secret_key    # from variable
  # Better: use AWS CLI profile or IAM role
  # profile = "default"
}
```

---

## 6. Resource Block — How to Create Infrastructure

**Syntax:**
```hcl
resource "provider_resourcetype" "local_name" {
  argument1 = value1
  argument2 = value2
}
```

**Examples:**
```hcl
# EC2 Instance
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  key_name      = "my-key"

  tags = {
    Name = "WebServer"
    Env  = "Production"
  }
}

# S3 Bucket
resource "aws_s3_bucket" "mybucket" {
  bucket = "akhil-my-bucket-2024"

  tags = {
    Name = "MyBucket"
  }
}

# Security Group
resource "aws_security_group" "web_sg" {
  name        = "web-sg"
  description = "Allow HTTP and SSH"
  vpc_id      = aws_vpc.main.id    # reference another resource

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

---

## 7. Creating a VPC — Complete Example

```hcl
# main.tf — Complete VPC Setup

# ── VPC ──
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Name = "main-vpc"
  }
}

# ── PUBLIC SUBNET ──
resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "us-east-1a"
  map_public_ip_on_launch = true    # auto-assign public IP

  tags = {
    Name = "public-subnet"
  }
}

# ── PRIVATE SUBNET ──
resource "aws_subnet" "private" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-east-1b"

  tags = {
    Name = "private-subnet"
  }
}

# ── INTERNET GATEWAY ──
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "main-igw"
  }
}

# ── ROUTE TABLE (for public subnet) ──
resource "aws_route_table" "public_rt" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }

  tags = {
    Name = "public-rt"
  }
}

# ── ASSOCIATE ROUTE TABLE WITH PUBLIC SUBNET ──
resource "aws_route_table_association" "public_rta" {
  subnet_id      = aws_subnet.public.id
  route_table_id = aws_route_table.public_rt.id
}

# ── SECURITY GROUP ──
resource "aws_security_group" "web_sg" {
  name   = "web-sg"
  vpc_id = aws_vpc.main.id

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "web-sg"
  }
}

# ── EC2 INSTANCE IN PUBLIC SUBNET ──
resource "aws_instance" "web" {
  ami                    = var.ami_id
  instance_type          = var.instance_type
  subnet_id              = aws_subnet.public.id
  vpc_security_group_ids = [aws_security_group.web_sg.id]
  key_name               = var.key_name

  tags = {
    Name = "web-server"
  }
}
```

---

## 8. Variables

**Why variables?**
Avoid hardcoding values. Reuse same code for different environments (dev, staging, prod).

### Declaring Variables (variables.tf)
```hcl
# variables.tf

variable "region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}

variable "ami_id" {
  description = "AMI ID for EC2"
  type        = string
  # no default — must be provided
}

variable "key_name" {
  description = "SSH key pair name"
  type        = string
}

variable "allowed_ports" {
  description = "List of allowed ports"
  type        = list(number)
  default     = [80, 443, 22]
}

variable "tags" {
  description = "Common tags"
  type        = map(string)
  default = {
    Project     = "MyApp"
    Environment = "dev"
    Owner       = "Akhil"
  }
}

variable "db_password" {
  description = "Database password"
  type        = string
  sensitive   = true    # won't show in logs or output
}
```

### Variable Types
| Type | Example |
|---|---|
| string | `"us-east-1"` |
| number | `3` |
| bool | `true` |
| list(string) | `["a", "b", "c"]` |
| map(string) | `{key = "value"}` |
| object | complex type |

### Using Variables (main.tf)
```hcl
provider "aws" {
  region = var.region
}

resource "aws_instance" "web" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_name
  tags          = var.tags
}
```

### Providing Variable Values

**Method 1 — terraform.tfvars file (most common):**
```hcl
# terraform.tfvars
region        = "us-east-1"
instance_type = "t3.medium"
ami_id        = "ami-0c55b159cbfafe1f0"
key_name      = "my-keypair"
db_password   = "supersecret"
```

**Method 2 — Command line:**
```bash
terraform apply -var="region=us-east-1" -var="instance_type=t3.medium"
```

**Method 3 — Environment variables:**
```bash
export TF_VAR_region="us-east-1"
export TF_VAR_instance_type="t3.medium"
terraform apply
```

**Method 4 — Different .tfvars for environments:**
```bash
terraform apply -var-file="dev.tfvars"
terraform apply -var-file="prod.tfvars"
```

---

## 9. Outputs

**Why outputs?**
Display useful information after apply. Share values between modules.

```hcl
# outputs.tf

output "vpc_id" {
  description = "ID of the VPC"
  value       = aws_vpc.main.id
}

output "public_subnet_id" {
  description = "ID of public subnet"
  value       = aws_subnet.public.id
}

output "instance_public_ip" {
  description = "Public IP of web server"
  value       = aws_instance.web.public_ip
}

output "instance_dns" {
  description = "Public DNS of web server"
  value       = aws_instance.web.public_dns
}

output "db_password" {
  value     = var.db_password
  sensitive = true            # won't show in terminal
}
```

```bash
terraform output                    # show all outputs
terraform output vpc_id             # show specific output
terraform output -json              # output as JSON
```

---

## 10. Terraform State

**What is State?**
Terraform keeps a state file (`terraform.tfstate`) that maps your configuration to real infrastructure. It tracks what exists so Terraform knows what to create, update, or delete.

```json
// terraform.tfstate (simplified)
{
  "resources": [
    {
      "type": "aws_instance",
      "name": "web",
      "instances": [
        {
          "attributes": {
            "id": "i-1234567890",
            "ami": "ami-0c55b159cbfafe1f0",
            "public_ip": "54.123.456.789"
          }
        }
      ]
    }
  ]
}
```

**Local State vs Remote State:**

| | Local State | Remote State |
|---|---|---|
| Location | terraform.tfstate on your machine | S3, Terraform Cloud |
| Team use | ❌ Not safe for teams | ✅ Multiple people can work |
| Locking | No | Yes (prevents conflicts) |
| Backup | Manual | Automatic |

**Remote State in S3 (for teams):**
```hcl
# backend.tf
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "prod/vpc/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-locks"    # for state locking
  }
}
```

---

## 11. Workspaces

**What is a Workspace?**
Workspaces let you manage multiple environments (dev, staging, prod) with the same configuration but separate state files.

```
default workspace  → terraform.tfstate
dev workspace      → terraform.tfstate.d/dev/terraform.tfstate
prod workspace     → terraform.tfstate.d/prod/terraform.tfstate
```

```bash
# Workspace commands
terraform workspace list              # list all workspaces
terraform workspace new dev           # create dev workspace
terraform workspace new staging       # create staging workspace
terraform workspace new prod          # create prod workspace
terraform workspace select dev        # switch to dev
terraform workspace show              # current workspace
terraform workspace delete dev        # delete workspace
```

**Using workspace in configuration:**
```hcl
# Use workspace name to set different values
resource "aws_instance" "web" {
  instance_type = terraform.workspace == "prod" ? "t3.large" : "t2.micro"

  tags = {
    Name        = "web-${terraform.workspace}"
    Environment = terraform.workspace
  }
}

# Or use locals
locals {
  instance_type = {
    dev     = "t2.micro"
    staging = "t2.medium"
    prod    = "t3.large"
  }
}

resource "aws_instance" "web" {
  instance_type = local.instance_type[terraform.workspace]
}
```

**Workspace workflow:**
```bash
# Deploy to dev
terraform workspace select dev
terraform apply -var-file="dev.tfvars"

# Deploy to prod
terraform workspace select prod
terraform apply -var-file="prod.tfvars"
```

---

## 12. Modules

**What is a Module?**
A module is a reusable package of Terraform code. Instead of rewriting the same VPC code for every project, write it once as a module and use it everywhere.

```
Without modules:           With modules:
project1/                  modules/
  main.tf (vpc code)         vpc/
  main.tf (ec2 code)           main.tf
project2/                      variables.tf
  main.tf (vpc code AGAIN)     outputs.tf
  main.tf (ec2 code AGAIN)
                           project1/
                             main.tf (calls vpc module)
                           project2/
                             main.tf (calls vpc module)
```

### Creating a Module

```hcl
# modules/vpc/main.tf
resource "aws_vpc" "main" {
  cidr_block = var.cidr_block
  tags = {
    Name = var.vpc_name
  }
}

resource "aws_subnet" "public" {
  vpc_id     = aws_vpc.main.id
  cidr_block = var.public_subnet_cidr
}
```

```hcl
# modules/vpc/variables.tf
variable "cidr_block" {
  type = string
}
variable "vpc_name" {
  type = string
}
variable "public_subnet_cidr" {
  type = string
}
```

```hcl
# modules/vpc/outputs.tf
output "vpc_id" {
  value = aws_vpc.main.id
}
output "subnet_id" {
  value = aws_subnet.public.id
}
```

### Using a Module

```hcl
# main.tf (in your project)

# Local module
module "vpc" {
  source             = "./modules/vpc"    # path to module
  cidr_block         = "10.0.0.0/16"
  vpc_name           = "prod-vpc"
  public_subnet_cidr = "10.0.1.0/24"
}

# Public registry module (Terraform Registry)
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "5.0.0"

  name = "my-vpc"
  cidr = "10.0.0.0/16"

  azs             = ["us-east-1a", "us-east-1b"]
  private_subnets = ["10.0.1.0/24", "10.0.2.0/24"]
  public_subnets  = ["10.0.4.0/24", "10.0.5.0/24"]

  enable_nat_gateway = true
}

# Use module outputs
resource "aws_instance" "web" {
  subnet_id = module.vpc.subnet_id
}
```

```bash
terraform init      # downloads modules
terraform plan
terraform apply
```

---

## 13. Terraform Meta-Arguments

```hcl
# count — create multiple resources
resource "aws_instance" "web" {
  count         = 3
  ami           = var.ami_id
  instance_type = "t2.micro"

  tags = {
    Name = "web-${count.index}"    # web-0, web-1, web-2
  }
}

# for_each — create resources from map or set
resource "aws_s3_bucket" "buckets" {
  for_each = toset(["dev", "staging", "prod"])
  bucket   = "myapp-${each.key}"
}

# depends_on — explicit dependency
resource "aws_instance" "web" {
  depends_on = [aws_vpc.main, aws_subnet.public]
  # ...
}

# lifecycle — control resource behavior
resource "aws_instance" "web" {
  # ...
  lifecycle {
    create_before_destroy = true    # create new before destroying old
    prevent_destroy       = true    # never allow destroy (production DBs)
    ignore_changes        = [tags]  # ignore changes to tags
  }
}
```

---

## 14. Data Sources

**What is a Data Source?**
Data sources let you fetch information about existing infrastructure (not managed by Terraform) and use it in your config.

```hcl
# Fetch existing VPC
data "aws_vpc" "existing" {
  id = "vpc-12345678"
}

# Fetch latest Amazon Linux AMI automatically
data "aws_ami" "amazon_linux" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }
}

# Use data source
resource "aws_instance" "web" {
  ami           = data.aws_ami.amazon_linux.id    # always latest AMI
  instance_type = "t2.micro"
  subnet_id     = data.aws_vpc.existing.id
}
```

---

## 15. Locals

**What are Locals?**
Local values are like variables but computed within the configuration. Used to avoid repetition.

```hcl
locals {
  env         = terraform.workspace
  app_name    = "myapp"
  common_tags = {
    Project     = local.app_name
    Environment = local.env
    Owner       = "Akhil"
    ManagedBy   = "Terraform"
  }
}

resource "aws_instance" "web" {
  ami           = var.ami_id
  instance_type = "t2.micro"
  tags          = local.common_tags    # reuse common tags everywhere
}

resource "aws_s3_bucket" "data" {
  bucket = "${local.app_name}-${local.env}-data"
  tags   = local.common_tags
}
```

---

## 16. Terraform Interview Q&A

**Q: What is the difference between terraform plan and terraform apply?**
`plan` shows what WILL happen (preview). `apply` actually makes the changes.

**Q: What is terraform state and why is it important?**
State file tracks the mapping between your config and real infrastructure. Without it, Terraform doesn't know what exists and would try to recreate everything.

**Q: What happens if you delete the state file?**
Terraform loses track of existing resources. Running apply would try to create duplicates. You'd need to import resources back using `terraform import`.

**Q: What is the difference between count and for_each?**
`count` creates resources by number. `for_each` creates resources from a map or set — better because resources have meaningful names not just indexes.

**Q: How do you manage secrets in Terraform?**
Use environment variables (TF_VAR_), mark variables as sensitive=true, use AWS Secrets Manager or HashiCorp Vault, never hardcode in .tf files.

**Q: What is a Terraform module?**
Reusable, self-contained package of Terraform code. Like a function in programming — write once, use many times.

**Q: How does Terraform handle dependencies?**
Automatically through resource references (implicit dependency). You can also use `depends_on` for explicit dependency.

---

## 17. Quick Reference — Terraform

```bash
# ESSENTIAL WORKFLOW
terraform init          # always first
terraform fmt           # format code
terraform validate      # check syntax
terraform plan          # preview
terraform apply         # create/update
terraform destroy       # tear down

# STATE
terraform state list
terraform state show <resource>
terraform output

# WORKSPACES
terraform workspace new dev
terraform workspace select prod
terraform workspace list

# IMPORT EXISTING RESOURCE
terraform import aws_instance.web i-1234567890
```

