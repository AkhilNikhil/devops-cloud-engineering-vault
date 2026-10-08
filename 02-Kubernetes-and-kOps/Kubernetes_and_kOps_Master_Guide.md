# ☸️ Kubernetes & kOps: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Kubernetes Architecture, Control Plane Internals, Worker Node Agents, kOps on AWS EC2 Setup, Workload Objects, Networking & Ingress, Storage, Probes, and Troubleshooting.

---

## 📑 Table of Contents
- [Why Kubernetes? (Docker Drawbacks & Orchestration)](#1-drawbacks-of-docker-standalone)
- [Docker Swarm vs Kubernetes](#2-docker-swarm--overcoming-dockers-drawbacks)
- [Kubernetes Master & Worker Architecture](#4-kubernetes-architecture)
- [How kOps Creates a Kubernetes Cluster on AWS (Step-by-Step)](#5-how-kops-creates-a-kubernetes-cluster-on-aws)
- [Core Kubernetes Objects (Pods, Deployments, Services)](#core-workload-objects)
- [Probes: Startup, Liveness, and Readiness](#probes-deep-dive)
- [Storage: PV, PVC, and StorageClasses](#storage-in-kubernetes)
- [Production Diagnostic & Troubleshooting Playbook](#troubleshooting-playbook)
- [High-Yield Technical Interview Q&A](#interview-qa)

---

SECTION 2: KUBERNETES — COMPLETE GUIDE
Flow: Why Kubernetes → Architecture → Core Objects → Storage → Networking → Security → Advanced →
Troubleshooting




1. Drawbacks of Docker (Standalone)
When you run Docker alone without any orchestration, you face these problems:
Problem Description
No Auto-healing If a container crashes, it stays dead. You manually restart it.
No Auto-scaling Can't automatically add more containers when load increases
No Load Balancing No built-in way to distribute traffic across containers
Single Host Docker runs on one machine — no clustering out of the box
No Rolling Updates No way to update containers without downtime
No Self-healing No health checks that restart unhealthy containers
Complex Networking Connecting containers across multiple hosts is hard
No Storage Management Volumes are manual and host-dependent
No Secret Management No built-in secure way to manage passwords/keys
2. Docker Swarm — Overcoming Docker's Drawbacks
Docker Swarm is Docker's native clustering tool. It groups multiple Docker hosts into a single virtual host.
What Swarm adds over plain Docker:
Multi-host container management
Basic load balancing
Simple scaling ( docker service scale )
Basic rolling updates
Service discovery
But Swarm has its own limitations:
Docker Swarm Limitation Kubernetes Solution
Limited auto-scaling (no CPU-based HPA) Full HPA based on CPU/memory/custom metrics




Basic health checks Liveness + Readiness + Startup probes
No built-in secrets encryption Encrypted secrets, integration with Vault
Limited storage options PV, PVC, StorageClass, dynamic provisioning
No RBAC Full RBAC with roles and bindings
Small ecosystem Massive ecosystem, CNCF projects
Less active development Industry standard, massive community
No CRDs Custom Resource Definitions to extend K8s
Basic networking CNI plugins, Network Policies
No namespace isolation Full namespace support with quotas
3. What is Kubernetes?
Definition:
Kubernetes (K8s) is an open-source container orchestration platform originally created by Google, now
maintained by the CNCF (Cloud Native Computing Foundation). It automates the deployment, scaling, and
management of containerized applications.
Key Features:
Auto-healing — restarts failed containers automatically
Auto-scaling — HPA scales pods based on CPU/memory
Load Balancing — distributes traffic across pods
Rolling Updates — zero-downtime deployments
Self-healing — replaces failed nodes/pods
Storage Orchestration — automatically mounts storage
Secret & Config Management — secure handling of sensitive data
Service Discovery — built-in DNS for pod communication
Multi-cloud — runs on AWS, Azure, GCP, on-premise
Declarative — you define desired state, K8s makes it happen
Why Kubernetes > Docker Swarm:
Industry standard (used by Google, Netflix, Airbnb)
Much richer feature set




Better auto-scaling
Full RBAC
Huge ecosystem (Helm, Istio, Argo, Prometheus)
Better storage management
More active development
4. Kubernetes Architecture
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
Control Plane Components
Component Role
API Server Entry point for all commands (kubectl). Validates and processes requests.
Scheduler Watches for unscheduled pods, assigns them to suitable worker nodes
Controller Manager Runs controllers that maintain desired state (Deployment, ReplicaSet, Node controllers)
etcd Distributed key-value store. Stores ALL cluster state. Source of truth.
Worker Node Components
Component Role
kubelet Agent on each node. Receives pod specs from API server, ensures containers are running
kube-proxy Manages network rules on nodes, handles Service networking and load balancing
Container Runtime Runs containers — containerd, CRI-O (Docker was deprecated in K8s 1.24+)
5. How kOps Creates a Kubernetes Cluster on AWS
kOps (Kubernetes Operations) — tool to provision, manage, and upgrade Kubernetes clusters on cloud
providers.
# STEP 1 — Install kOps and kubectl
curl -Lo kops https://github.com/kubernetes/kops/releases/download/v1.28.0/kops-linux-
chmod +x kops && sudo mv kops /usr/local/bin/
# STEP 2 — Create S3 bucket for kOps state store
aws s3 mb s3://devops-kops-state-store
export KOPS_STATE_STORE=s3://devops-kops-state-store
# STEP 3 — Create cluster config
kops create cluster \
  --name=mycluster.k8s.local \
  --state=s3://devops-kops-state-store \




 
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
6. Replication Controller vs ReplicaSet
Replication Controller (Old — Deprecated)
Definition: Ensures a specified number of pod replicas are running at all times. If a pod dies, it creates a new
one. If there are too many, it removes some.
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
ReplicaSet (New — Use This)
Definition: Same as ReplicationController but supports set-based selectors (more powerful matching). Usually
managed by a Deployment.
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
Differences
Feature ReplicationController ReplicaSet
API version v1 apps/v1
Selector type Equality-based only Set-based (matchLabels, matchExpressions)




Status Deprecated Current standard
Used by Nothing (old) Deployments
Direct use Avoid Avoid (use Deployments instead)
Commands
kubectl get rc                          # list replication controllers
kubectl get rs                          # list replica sets
kubectl describe rs rs1                 # details of replica set
kubectl scale rs rs1 --replicas=5       # scale replica set
kubectl delete rs rs1                   # delete replica set
7. Deployments — Complete Guide
Definition: A Deployment manages ReplicaSets and provides declarative updates. It's the standard way to run
stateless applications.
Deployment → manages → ReplicaSet → manages → Pods
Deployment YAML
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
Deployment Commands
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
8. Kubernetes Services — 3 Types with YAML
Definition: A Service provides a stable network endpoint for a set of pods. Pods are ephemeral (IPs change),
Services are stable.
Type 1: ClusterIP (Internal Only)
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
Use when: Pod-to-Pod communication inside cluster
Access: Only from within the cluster
Example: Backend connecting to database




Type 2: NodePort (External via Node IP)
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
Use when: Need external access without cloud load balancer
Access: http://<node-ip>:31200
Example: Dev/test environments
Type 3: LoadBalancer (Cloud Load Balancer)
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
Use when: Production, need external access with single endpoint
Access: Cloud provides external IP/DNS
Example: Production web app on AWS (creates ELB)
Service Commands




kubectl get services                          # list services
kubectl get svc                               # short form
kubectl describe svc myservice                # service details
kubectl delete svc myservice                  # delete service
kubectl expose deployment dp1 --port=80 --type=LoadBalancer  # quick create
kubectl get endpoints                         # see which pods service routes to
Pod + Service YAML (Combined)
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
9. Namespaces
Definition: Namespaces logically partition a Kubernetes cluster into isolated environments. Resources in one
namespace don't interact with another by default.




Types of Namespaces
Built-in namespaces:
Namespace Purpose
default Where resources go if you don't specify a namespace
kube-system Kubernetes system components (API server, DNS, scheduler)
kube-public Readable by all users, used for cluster info
kube-node-lease Node heartbeat data (internal use)
Custom namespaces (you create these):
dev  — development environment
staging  — staging environment
production  — production environment
monitoring  — Prometheus, Grafana
Namespace YAML
apiVersion: v1
kind: Namespace
metadata:
  name: dev
Namespace Commands
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




 
 
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
10. Kubernetes Volumes — Complete Guide
Volume Types Comparison
emptyDir    → Temporary, shared between containers in same pod, deleted when pod dies
hostPath    → Uses node's filesystem, persists beyond pod, tied to specific node
PV + PVC    → Fully persistent, independent of pods and nodes, production standard
ConfigMap   → Mount config files into pods
Secret      → Mount sensitive data into pods
Type 1: emptyDir — Temporary Shared Volume
Definition: Created when a pod starts. Deleted when the pod is removed. Shared between all containers in the
same pod. Used for caching, temporary processing.
# emptydir-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:




 
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
Use when: Two containers in same pod need to share data temporarily
Example: Sidecar container processes logs before main container reads them
Lifecycle: Dies with the pod
Type 2: hostPath — Node Filesystem Volume
Definition: Mounts a directory from the node's filesystem into the pod. Persists beyond pod restarts (as long as
pod stays on same node). NOT recommended for production (node-specific).
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
Use when: DaemonSets collecting logs from node filesystem
Not for: Production databases (node-specific, not portable)
Type 3: PersistentVolume (PV) + PersistentVolumeClaim (PVC)
How it works:
Admin creates PV ──→ Developer creates PVC ──→ Pod uses PVC
(actual storage)      (request for storage)
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
Access Modes
Mode Description Use case
ReadWriteOnce (RWO) One node can read+write Databases
ReadOnlyMany (ROX) Many nodes can read Shared config files




ReadWriteMany (RWX) Many nodes can read+write Shared file systems (NFS, EFS)
Reclaim Policies
Policy Meaning
Retain Keep PV data after PVC deleted. Manual cleanup needed.
Delete Delete PV and underlying storage when PVC deleted
Recycle Wipe PV data and make available again (deprecated)
PV/PVC Commands
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
11. DaemonSet
Definition: Ensures exactly ONE pod runs on EVERY node in the cluster. When a new node joins, DaemonSet
automatically creates a pod there.
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
kubectl get daemonsets                        # list daemonsets
kubectl get ds                                # short form
kubectl describe ds ds1                       # details
kubectl delete ds ds1                         # delete
Use for:
- Log collectors (Fluentd, Filebeat) — collect logs from every node
- Monitoring agents (Prometheus node-exporter) — metrics from every node
- Network plugins (CNI — Calico, Flannel) — networking on every node
- Security agents — run on every node
12. ConfigMap — Complete Guide
Definition: Stores non-sensitive configuration as key-value pairs. Injected into pods as environment variables
or mounted as files.
Imperative Way (Command line)
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
Declarative Way (YAML)
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
Using ConfigMap in Deployment
Method 1: As Environment Variables
spec:
  containers:
  - name: c1
    image: httpd
    envFrom:
    - configMapRef:
        name: cm1            # inject ALL keys as env vars
Method 2: Specific Key as Env Var
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
Method 3: Mount as File
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
13. Secrets — Complete Guide
Definition: Like ConfigMap but for sensitive data (passwords, API keys, tokens). Values are base64 encoded.
Can be encrypted at rest.
Imperative Way
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
  --docker-username=devops \
  --docker-password=mypassword




# View secrets (values are base64 encoded)
kubectl get secrets
kubectl describe secret s1          # shows keys but NOT values
kubectl get secret s1 -o yaml       # shows base64 encoded values
# Decode a secret value
kubectl get secret s1 -o jsonpath='{.data.password}' | base64 --decode
Declarative Way
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
Using Secrets in Deployment
Method 1: All keys as env vars
spec:
  containers:
  - name: c1
    image: httpd
    envFrom:
    - secretRef:
        name: s1
Method 2: Specific key as env var
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
Method 3: Mount as file
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
14. RBAC — Role Based Access Control (Complete)
Definition: RBAC controls WHO can do WHAT in Kubernetes. It's how you manage access and permissions.
┌──────────────────────────────────────────────────────┐
│                   RBAC DIAGRAM                       │
│                                                      │
│  WHO?              WHAT?           WHERE?            │
│  ┌──────────┐     ┌──────────┐    ┌──────────────┐  │
│  │  User    │     │  Role    │    │  Namespace   │  │
│  │  Group   │──── ▶ │ (rules)  │──── ▶   (limited)   │  │
│  │ Service  │     └──────────┘    └──────────────┘  │
│  │ Account  │                                        │
│  └────┬─────┘     ┌─────────────┐  ┌─────────────┐  │
│       │           │ ClusterRole │  │   Cluster   │  │
│       └────────── ▶ │  (rules)    │── ▶   (wide)      │  │
│                   └─────────────┘  └─────────────┘  │
│                                                      │
│  RoleBinding connects User ←→ Role (namespace)      │
│  ClusterRoleBinding connects User ←→ ClusterRole    │
└──────────────────────────────────────────────────────┘




RBAC Memory Formula
ServiceAccount  = WHO (identity)
Role            = WHAT (permissions, namespace level)
RoleBinding     = CONNECTS WHO to WHAT (namespace)
ClusterRole         = WHAT (permissions, cluster-wide)
ClusterRoleBinding  = CONNECTS WHO to WHAT (cluster-wide)
Step 1: ServiceAccount (WHO)
# serviceaccount.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: dev-user
  namespace: default
kubectl apply -f serviceaccount.yaml
kubectl get serviceaccounts
kubectl get sa
Step 2: Role (WHAT — Namespace Level)
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
Common verbs: get , list , watch , create , update , patch , delete
kubectl apply -f role.yaml
kubectl get roles
kubectl describe role pod-reader




Step 3: RoleBinding (CONNECT)
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
kubectl apply -f rolebinding.yaml
kubectl get rolebindings
kubectl describe rolebinding read-pods-binding
# Test if permission works
kubectl auth can-i list pods \
  --as=system:serviceaccount:default:dev-user \
  -n default
Step 4: ClusterRole (WHAT — Cluster Wide)
# clusterrole.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: node-reader
rules:
- apiGroups: [""]
  resources: ["nodes", "namespaces", "persistentvolumes"]
  verbs: ["get", "list", "watch"]
kubectl apply -f clusterrole.yaml
kubectl get clusterroles




Step 5: ClusterRoleBinding (CONNECT — Cluster Wide)
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
15. Jobs and CronJobs
Job — Run to Completion
Definition: A Job creates pods that run until successful completion. Used for batch tasks, migrations, backups.
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
kubectl apply -f job.yaml
kubectl get jobs
kubectl describe job batch-job
kubectl get pods --selector=job-name=batch-job
kubectl logs <pod-name>
kubectl delete job batch-job
CronJob — Scheduled Jobs
Definition: Runs Jobs on a schedule (like Linux cron). Used for scheduled backups, cleanup tasks, reports.
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
kubectl get cronjobs
kubectl get cj
kubectl describe cj hello-cron
kubectl delete cj hello-cron
# Manually trigger a cronjob
kubectl create job manual-run --from=cronjob/hello-cron
16. StatefulSet — Complete Guide
Definition: A StatefulSet manages stateful applications. Unlike Deployments, each pod gets a stable, unique
identity that persists across rescheduling.
StatefulSet vs Deployment
Feature Deployment StatefulSet
Pod names Random (dp1-abc123) Stable ordered (nginx-0, nginx-1, nginx-2)
Pod order Created/deleted randomly Created in order (0,1,2), deleted in reverse
Storage Shared or no PVC Each pod gets its OWN PVC
Network identity Random IP Stable hostname via headless service
Use case Stateless (web, API) Stateful (databases, Kafka, Elasticsearch)




Scaling Any order Ordered (one at a time)
StatefulSet YAML
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
How StatefulSet DNS Works
nginx-0.nginx-headless.default.svc.cluster.local
nginx-1.nginx-headless.default.svc.cluster.local
nginx-2.nginx-headless.default.svc.cluster.local
Format: <pod-name>.<service-name>.<namespace>.svc.cluster.local
kubectl get statefulsets
kubectl get sts
kubectl scale sts nginx-statefulset --replicas=5
kubectl delete sts nginx-statefulset
17. Deployment Strategies
Strategy 1: Recreate
How it works: Kill ALL old pods, then create all new pods. Simple but causes downtime.
Before: [v1][v1][v1]
During: [  ][  ][  ]  ← DOWNTIME
After:  [v2][v2][v2]
spec:
  strategy:
    type: Recreate
Use when: Development environments, or when old and new versions CANNOT run together
Downtime: YES




 
Risk: High (if new version fails, downtime continues)
Strategy 2: Rolling Update (Default)
How it works: Gradually replaces old pods with new ones. Zero downtime.
Start:  [v1][v1][v1]
Step 1: [v2][v1][v1]
Step 2: [v2][v2][v1]
Step 3: [v2][v2][v2]
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1         # max EXTRA pods during update
      maxUnavailable: 1   # max pods DOWN during update
Use when: Most production deployments
Downtime: NO
Rollback: kubectl rollout undo deployment/dp1
Strategy 3: Blue-Green Deployment
How it works: Two identical environments. Blue = live. Green = new. Switch traffic by updating Service selector.
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




 
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
# Blue-Green workflow
kubectl apply -f blue-deployment.yaml    # Step 1: Deploy blue (live)
kubectl apply -f service.yaml            # Step 2: Service points to blue
kubectl apply -f green-deployment.yaml   # Step 3: Deploy green (standby)
kubectl port-forward deploy/myapp-green 8080:80  # Step 4: Test green
# Step 5: Update service.yaml selector to version: green
kubectl apply -f service.yaml            # Step 6: Flip — traffic now goes to green
# Rollback: change selector back to blue, kubectl apply -f service.yaml
Downtime: NO (instant switch)
Rollback: Instant (just change selector back)
Cost: Double resources (both versions running)
Strategy 4: Canary Deployment
How it works: Send a small percentage of traffic to new version. Gradually increase if stable.




        ┌─────────────┐
Users → │   Service   │
        └──────┬──────┘
               │
    ┌──────────┴──────────┐
    │                     │
    ▼  (90% traffic)      ▼  (10% traffic)
[v1][v1][v1][v1][v1]    [v2]
 STABLE (5 pods)         CANARY (1 pod)
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
Downtime: NO
Risk: Low (only small % of users see new version)
Rollback: Scale canary to 0, scale stable back up
Use when: A/B testing, gradual rollout to production
Deployment Strategy Comparison
Strategy Downtime Rollback Speed Resource Cost Use Case
Recreate YES Slow Normal Dev/simple apps
Rolling Update NO Fast Normal+slight Most production apps
Blue-Green NO Instant Double Critical apps, instant rollback
Canary NO Fast Normal+small Risk-averse, A/B testing
18. Kubernetes Troubleshooting Guide




Most Important Debugging Commands
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
Error 1: CrashLoopBackOff
What it means: Container keeps starting and crashing repeatedly. Kubernetes keeps trying (backing off with
increasing delay).
STATUS: CrashLoopBackOff
How to diagnose:
kubectl describe pod <pod-name>      # check Events section for error
kubectl logs <pod-name>              # current container logs
kubectl logs <pod-name> --previous   # logs from CRASHED container (most useful)
Common causes and fixes:
Cause Fix
Application error on startup Fix bug in your application code




Wrong command/entrypoint in Dockerfile Fix CMD or ENTRYPOINT
Missing environment variable Add required env var to pod spec
Missing ConfigMap or Secret Create the ConfigMap/Secret
Wrong port in liveness probe Fix probe port to match container port
Out of memory Increase memory limits
Config file missing Mount correct ConfigMap/volume
# Debug: start with log from previous crash
kubectl logs <pod-name> --previous
# If logs are empty (crash before logging), override entrypoint
kubectl run debug --image=myapp:1.0 --command -- sleep 3600
kubectl exec -it debug -- /bin/sh    # manually explore what's wrong
Error 2: ImagePullBackOff / ErrImagePull
What it means: Kubernetes can't pull the container image from the registry.
STATUS: ImagePullBackOff or ErrImagePull
How to diagnose:
kubectl describe pod <pod-name>      # check Events — will show pull error
Common causes and fixes:
Cause Fix
Wrong image name Fix image name in deployment YAML
Wrong tag Fix image tag (check if it exists in registry)
Image doesn't exist Push image to registry first
Private registry — no credentials Create docker-registry secret and add imagePullSecrets




 
Registry down Wait or switch to different tag
# Fix for private registry
kubectl create secret docker-registry regcred \
  --docker-server=docker.io \
  --docker-username=devops \
  --docker-password=mypassword
# Add to pod spec:
spec:
  imagePullSecrets:
  - name: regcred
  containers:
  - name: c1
    image: private-repo/myapp:1.0
Error 3: Pending Pods
What it means: Pod is waiting to be scheduled but can't be placed on any node.
STATUS: Pending
How to diagnose:
kubectl describe pod <pod-name>      # look at Events — shows why scheduling failed
kubectl get nodes                    # check node status
kubectl describe node <node-name>    # check node conditions and capacity
Common causes and fixes:
Cause Fix
Not enough CPU/memory on any node Add more nodes or reduce pod requests
Node selector doesn't match any node Fix nodeSelector or node labels
Taint on all nodes, no toleration Add toleration or remove taint
PVC not bound (storage issue) Fix PV/PVC — check storage class




All nodes are full Scale up cluster (add nodes)
kubectl describe pod <pod-name> | grep -A 10 "Events:"
# Look for: "0/3 nodes are available: 3 Insufficient memory"
# Or: "0/3 nodes are available: node(s) had taint"
Error 4: NodeNotReady
What it means: A node is not accepting pods — it's in an unhealthy state.
STATUS: NotReady
How to diagnose:
kubectl get nodes                         # see NotReady status
kubectl describe node <node-name>         # check Conditions section
# Look for: MemoryPressure, DiskPressure, PIDPressure, NetworkUnavailable
Common causes and fixes:
Cause Fix
kubelet not running SSH to node, systemctl restart kubelet
Network plugin (CNI) failed Restart network plugin DaemonSet
Node out of disk Free disk space, add storage
Node out of memory Free memory or add more RAM
Node lost connectivity Check network, restart node
# SSH to the problem node
ssh ec2-user@<node-ip>
systemctl status kubelet
journalctl -u kubelet -f          # kubelet logs
systemctl restart kubelet




Error 5: Unauthorized Error
What it means: You don't have permission to perform an action.
Error: Unauthorized / Forbidden
How to diagnose:
kubectl auth can-i get pods                    # check your permissions
kubectl auth can-i get pods -n production      # in specific namespace
kubectl auth can-i --list                      # list all your permissions
Common causes and fixes:
Cause Fix
kubeconfig wrong or expired Re-download/refresh kubeconfig
Missing Role/ClusterRole Create Role with needed permissions
Missing RoleBinding Create RoleBinding to connect user to Role
Wrong namespace Check if you're in the right namespace
ServiceAccount missing permissions Create RBAC for the ServiceAccount
Error 6: OOMKilled (Out of Memory Killed)
What it means: Container used more memory than its limit — Linux kernel killed it.
STATUS: OOMKilled (last state reason)
How to diagnose:
kubectl describe pod <pod-name>
# Look for: Last State: Terminated, Reason: OOMKilled
kubectl top pods                               # check current memory usage
Common causes and fixes:




Cause Fix
Memory limit too low Increase memory limits
Memory leak in application Fix application memory leak
Sudden traffic spike Set HPA to scale before OOM
# Fix: increase memory limit
resources:
  requests:
    memory: "256Mi"
  limits:
    memory: "512Mi"      # increase this
Error 7: FailedScheduling
What it means: Scheduler can't find a suitable node for the pod.
Events: FailedScheduling
Diagnosis:
kubectl describe pod <pod-name>      # Events will show exact reason
Common reasons:
0/3 nodes are available: 3 Insufficient memory
0/3 nodes are available: 3 node(s) had taint
0/3 nodes are available: 3 node(s) didn't match node selector
Fix: Based on the message — add nodes, remove taints, or fix node selectors.
Error 8: Error Creating LoadBalancer
What it means: Kubernetes couldn't create a cloud load balancer.
How to diagnose:




kubectl describe service <service-name>      # check Events
Common causes and fixes:
Cause Fix
Insufficient IAM permissions Add load balancer permissions to node IAM role
Cloud provider quota exceeded Request quota increase
Wrong AWS region/zone config Fix cluster config for correct region
Security group issue Check security group allows required ports
Error 9: ContainerCreating (Stuck)
What it means: Container is stuck in creating state.
STATUS: ContainerCreating (for too long)
How to diagnose:
kubectl describe pod <pod-name>      # check Events
Common causes and fixes:
Cause Fix
Volume mount issue (PVC not bound) Check PVC status, fix storage
ConfigMap/Secret doesn't exist Create missing ConfigMap or Secret
Image being pulled (slow registry) Wait, or use image pull policy
Network plugin not ready Restart CNI DaemonSet
kubectl get pvc                      # check if PVC is bound
kubectl get configmaps               # check if CM exists
kubectl get secrets                  # check if Secret exists




General Troubleshooting Workflow
1. kubectl get pods                  → What is the STATUS?
2. kubectl describe pod <name>       → What do EVENTS say?
3. kubectl logs <pod-name>           → What does the APP say?
4. kubectl logs <name> --previous    → What did it say before crash?
5. kubectl exec -it <name> -- sh     → Can I get inside?
6. kubectl get events                → Anything unusual?
7. kubectl top pods / nodes          → Resource pressure?
8. kubectl describe node <name>      → Node healthy?
19. Essential kubectl Quick Reference
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


---

## 🚀 Modern 2026 Production Kubernetes Blueprint

### 1. Container Runtime: containerd
* `dockershim` is permanently deprecated. Modern Kubernetes nodes communicate directly with **`containerd`** via the Container Runtime Interface (CRI), reducing memory overhead and process hopping.

### 2. Modern Ingress Specification (`networking.k8s.io/v1`)
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
  namespace: production
  annotations:
    kubernetes.io/ingress.class: nginx
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  rules:
    - host: api.cloudvault.net
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: payment-api-svc
                port:
                  number: 80
```
