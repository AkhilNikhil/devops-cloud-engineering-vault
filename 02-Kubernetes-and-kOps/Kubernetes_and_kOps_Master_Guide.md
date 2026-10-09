# ☸️ Kubernetes & kOps Production Engineering: The Definitive Master Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Container Orchestration Evolution (Docker Drawbacks to Swarm to K8s), Control Plane & Worker Node Internals, Production AWS kOps Cluster Architecture & Operator Instances, Workload Lifecycle (Pods, ReplicationController, ReplicaSets, Deployments), Services & Modern Ingress (`networking.k8s.io/v1`), Storage (PV/PVC/StorageClass), ConfigMaps & Secrets, Probes & HPA Auto-Scaling, Complete `kubectl` CLI Reference, and Production Troubleshooting.

---

## 📑 Table of Contents
- [1. Orchestration Evolution: Docker to Swarm to Kubernetes](#1-orchestration-evolution-docker-to-swarm-to-kubernetes)
- [2. Kubernetes Platforms Landscape](#2-kubernetes-platforms-landscape)
- [3. Kubernetes Architecture Internals](#3-kubernetes-architecture-internals)
- [4. Production AWS Cluster Orchestration with kOps](#4-production-aws-cluster-orchestration-with-kops)
- [5. Workload Evolution: Pods to Deployments](#5-workload-evolution-pods-to-deployments)
- [6. Kubernetes Services Networking](#6-kubernetes-services-networking)
- [7. Modern Ingress Networking (`networking.k8s.io/v1`)](#7-modern-ingress-networking-networkingk8siov1)
- [8. Persistent Storage Architecture (PV, PVC, StorageClass)](#8-persistent-storage-architecture-pv-pvc-storageclass)
- [9. Configuration & Secrets Management](#9-configuration--secrets-management)
- [10. Health Probes & Auto-Scaling (HPA v2)](#10-health-probes--auto-scaling-hpa-v2)
- [11. Specialized Workloads: DaemonSets, StatefulSets, & Jobs](#11-specialized-workloads-daemonsets-statefulsets--jobs)
- [12. Essential `kubectl` CLI Command Reference](#12-essential-kubectl-cli-command-reference)
- [13. Production Troubleshooting Playbook](#13-production-troubleshooting-playbook)
- [14. Senior DevOps Interview Q&A](#14-senior-devops-interview-qa)

---

## 1. Orchestration Evolution: Docker to Swarm to Kubernetes

Understanding why the industry shifted from standalone Docker to Docker Swarm and ultimately to Kubernetes is a fundamental interview topic.

```text
┌─────────────────────────┐      ┌─────────────────────────┐      ┌─────────────────────────┐
│    Standalone Docker    │  ──► │      Docker Swarm       │  ──► │     Kubernetes (K8s)    │
│  • Single-host only     │      │  • Multi-host cluster   │      │  • Multi-host enterprise│
│  • No auto-healing      │      │  • Load balancing       │      │  • Auto-healing & HPA   │
│  • Manual scaling       │      │  • No dynamic scaling   │      │  • Declarative rollouts │
│  • Downtime on updates  │      │  • CLI-only, limited    │      │  • Vast CNCF ecosystem  │
└─────────────────────────┘      └─────────────────────────┘      └─────────────────────────┘
```

> **💡 Real-World Analogy (Easy to Remember)**:  
> * **Standalone Docker**: A solo food truck. If the truck engine dies, business stops completely.  
> * **Docker Swarm**: A small fleet of 3 food trucks coordinated via a group chat. Works okay, but cannot dynamically hire drivers during lunch rush or auto-fix a broken engine.  
> * **Kubernetes**: An automated airport terminal dispatch system with computerized scheduling, automated backup flights, dynamic gate routing, and self-repairing escalators.

### 1. Drawbacks of Standalone Docker
* **Single-Host Limitation**: Containers run bound to a single physical server or virtual machine; cannot pool CPU/RAM across multiple hosts.
* **No Auto-Healing**: If a container application crashes or the underlying host dies, human operator intervention is required to restart it.
* **No Auto-Scaling**: Cannot dynamically scale container replica counts up or down based on real-time traffic spikes or CPU load.
* **Update Downtime**: Updating a container requires stopping the old container, causing service downtime during deployments.
* **Complex Multi-Host Networking**: Connecting containers across different host servers requires complex manual network tunneling.

### 2. Docker Swarm: Advantages & Critical Limitations
* **What Docker Swarm Introduced**:
  * Native clustering integrated directly into the Docker engine (`docker swarm init`).
  * Basic multi-host networking and ingress routing mesh.
  * Basic declarative service management and auto-restart.
* **Why Enterprise Adopted Kubernetes Over Swarm**:
  * **No Dynamic Auto-Scaling**: Swarm cannot automatically scale replicas based on CPU or custom metric thresholds.
  * **Limited Ecosystem**: Lacked rich third-party controllers, CRDs, service meshes (Istio), and GitOps tools (ArgoCD).
  * **CLI-Centric & Maintenance Headache**: Managing rolling updates, zero-downtime rollbacks, and storage volume plugins proved fragile at scale.

### 3. Kubernetes (K8s - The Pilot)
* Open-source container orchestration platform originally engineered by Google (based on Borg) and donated to the CNCF (Cloud Native Computing Foundation).
* **Core Capabilities**:
  * **Auto-Scaling**: Dynamic Horizontal Pod Autoscaling (HPA) and Vertical Pod Autoscaling (VPA).
  * **Auto-Healing**: Constantly reconciles desired state vs actual state; restarts failed containers, reschedules evicted pods.
  * **Automated Rollouts & Rollbacks**: Zero-downtime canary and rolling updates with instant automated rollback if health checks fail.
  * **Universal Portability**: Identical declarative YAML manifests run across local laptops, AWS, Azure, Google Cloud, and bare metal.

---

## 2. Kubernetes Platforms Landscape

| Platform | Target Environment | Key Characteristics |
| :--- | :--- | :--- |
| **kOps (Kubernetes Operations)** | Production AWS / OpenStack | **Golden standard for self-managed production clusters** on EC2; provisions VPCs, Auto Scaling Groups, IAM, and EBS automatically. |
| **EKS / AKS / GKE** | Cloud Managed | Managed Control Plane; cloud provider manages `kube-apiserver` and `etcd` high availability for a monthly fee. |
| **kubeadm** | Production Bare-Metal / VMs | Standard low-level tool for bootstrapping production-conformant clusters manually. |
| **Minikube** | Local Developer Laptop | Spins up a single-node VM running all Kubernetes components for quick local experimentation. |
| **k3s** | Edge / IoT / Lightweight Dev | Stripped-down binary under 100MB; replaces `etcd` with SQLite, perfect for CI runner sandboxes. |
| **KillerKoda** | Interactive Browser Playground | On-demand sandboxed Kubernetes environments in the browser; ideal for CKA/CKAD exam prep. |

---

## 3. Kubernetes Architecture Internals

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       CONTROL PLANE (Master Nodes)                          │
│                                                                             │
│   ┌──────────────┐     ┌──────────────┐     ┌───────────────────────────┐   │
│   │  API Server  │◄────┤  Scheduler   │     │ Controller Manager (KCM)  │   │
│   │ (kube-apiserver)   │(kube-scheduler)    │(Node, Replica, Endpoint)  │   │
│   └──────┬───────┘     └──────────────┘     └───────────────────────────┘   │
│          │                                                                  │
│          ▼                                                                  │
│   ┌──────────────┐                          ┌───────────────────────────┐   │
│   │     etcd     │                          │  Cloud Controller (CCM)   │   │
│   │ (State Store)│                          │  (AWS ELB, Route53, EBS)  │   │
│   └──────────────┘                          └───────────────────────────┘   │
└──────────┬──────────────────────────────────────────────────────────────────┘
           │ HTTPS (Port 6443)
           ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                          WORKER NODES                                       │
│                                                                             │
│   ┌───────────────────────────┐             ┌───────────────────────────┐   │
│   │          kubelet          │             │        kube-proxy         │   │
│   │ (Node Agent -> CRI API)   │             │ (iptables / IPVS rules)   │   │
│   └─────────────┬─────────────┘             └───────────────────────────┘   │
│                 │                                                           │
│                 ▼                                                           │
│   ┌───────────────────────────┐             ┌───────────────────────────┐   │
│   │     containerd / runc     │             │     CNI Plugin (Network)  │   │
│   │  (Container Execution)    │             │  (Calico / AWS VPC CNI)   │   │
│   └─────────────┬─────────────┘             └───────────────────────────┘   │
│                 ▼                                                           │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │   POD: [Pause Container (IPC/NET)] + [App Container] + [Sidecar]    │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Control Plane Components (The Brain)
* **`kube-apiserver`**:
  * The front door and central communication hub of the cluster.
  * Exposes the Kubernetes HTTP REST API on port 6443.
  * Every internal component (`scheduler`, `kubelet`, `kubectl`) communicates exclusively through the API Server; no component accesses `etcd` directly.
* **`etcd`**:
  * Distributed, highly-consistent key-value storage engine.
  * Stores the entire cluster state, configuration, and secrets.
  * Uses the **Raft consensus algorithm**; requires an odd number of master nodes (3 or 5) to survive quorum partitions: $	ext{Quorum} = \lfloor N/2 
floor + 1$.
* **`kube-scheduler`**:
  * Responsible for placing unscheduled pods onto optimal worker nodes.
  * Evaluates node filtering (taints, tolerations, resource availability) and scoring (pod affinity/anti-affinity, image locality).
* **`kube-controller-manager` (KCM)**:
  * Continuously runs reconciliation control loops: `Actual State == Desired State`.
  * Contains Node Controller, ReplicaSet Controller, EndpointSlice Controller, and ServiceAccount Controller.
* **`cloud-controller-manager` (CCM)**:
  * Integrates with cloud provider APIs to provision AWS Network Load Balancers, EBS persistent volume mounts, and route tables.

### Worker Node Components (The Workhorses)
* **`kubelet`**:
  * Primary node agent running directly on the Linux host OS (systemd service).
  * Watches for PodSpecs assigned to its node and instructs the container runtime via CRI (Container Runtime Interface) to start or stop containers.
  * Executes container Liveness/Readiness probes and reports node health back to `kube-apiserver`.
* **`kube-proxy`**:
  * Network proxy running on every worker node.
  * Programs Linux `iptables` or `IPVS` packet-filtering rules to route Service virtual IPs (`ClusterIP`) to individual backend pod IPs.
* **Container Runtime (`containerd` / `CRI-O`)**:
  * Low-level container engine responsible for pulling images, unpacking layers, and invoking `runc`.

---

## 4. Production AWS Cluster Orchestration with kOps

**kOps (Kubernetes Operations)** is the premier open-source tool for provisioning, managing, and upgrading enterprise-grade, highly-available Kubernetes clusters on AWS EC2.

### The "Operator Instance" Architectural Pattern
In production kOps setups, operations are executed from a dedicated **Operator Instance** (or DevOps Bastion) rather than logging into control plane servers:
* **Decoupled Management**: You never SSH into master or worker nodes directly to perform cluster tasks.
* **API Security**: The operator instance holds admin IAM roles and communicates securely with the `kube-apiserver` endpoint.
* **Reproducibility**: The operator instance maintains the version-controlled kOps configuration and state repository.

```text
┌───────────────────────┐
│   Operator Instance   │
│  (DevOps Management)  │
│  • kops CLI           │
│  • kubectl CLI        │
└──────────┬────────────┘
           │ 1. kops create cluster (writes manifest to S3)
           │ 2. kubectl apply (sends instructions to API Server)
           ▼
┌─────────────────────────────────────────────────────────────┐
│                      AWS Cloud Infrastructure               │
│                                                             │
│   ┌─────────────────────────┐   ┌────────────────────────┐  │
│   │ S3 Bucket (State Store) │   │ Auto Scaling Group     │  │
│   │  kops-state-vault-...   │   │ (Control Plane Master) │  │
│   └─────────────────────────┘   └───────────┬────────────┘  │
│                                             │               │
│                                             ▼               │
│                                 ┌────────────────────────┐  │
│                                 │ Auto Scaling Group     │  │
│                                 │ (Worker Nodes Pool)    │  │
│                                 └────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### Complete Step-by-Step kOps Cluster Lifecycle

#### Step 1: Set Up Prerequisites
```bash
# 1. Set environment variables
export CLUSTER_NAME="production.k8s.local" # Gossip-based domain (zero Route53 cost)
export KOPS_STATE_STORE="s3://enterprise-kops-state-vault-2026"

# 2. Create S3 state storage bucket with versioning and encryption
aws s3api create-bucket --bucket enterprise-kops-state-vault-2026 --region us-east-1
aws s3api put-bucket-versioning --bucket enterprise-kops-state-vault-2026   --versioning-configuration Status=Enabled
```

#### Step 2: Generate Cluster Manifest
```bash
kops create cluster   --name=${CLUSTER_NAME}   --state=${KOPS_STATE_STORE}   --zones=us-east-1a,us-east-1b   --control-plane-size=t3.medium   --node-size=t3.medium   --control-plane-count=1   --node-count=2   --dns=none   --networking=calico
```

#### Step 3: Review and Deploy Infrastructure
```bash
# Preview cloud resources (dry run)
kops update cluster --name=${CLUSTER_NAME}

# Execute build: Provisions EC2 instances, VPC, Subnets, SG, IAM, and EBS volumes
kops update cluster --name=${CLUSTER_NAME} --yes --admin
```

#### Step 4: Validate Cluster Health
```bash
# Validates API server responsiveness and node Ready state
kops validate cluster --wait 10m
```

#### Step 5: Clean Teardown
```bash
# Safely terminates all AWS cloud instances, volumes, and security groups
kops delete cluster --name=${CLUSTER_NAME} --yes
```

---

## 5. Workload Evolution: Pods to Deployments

### Why Raw Pods Are Never Run in Production
* A Pod is the smallest deployable compute unit in Kubernetes.
* **Raw Pod Drawback**: If a worker node crashes, dies, or undergoes maintenance, raw standalone pods are **permanently terminated**—they are **never rescheduled or auto-healed**!
* **Rule**: Production applications must always be wrapped in higher-level workload controllers (**Deployments**, **StatefulSets**, or **DaemonSets**).

### Imperative vs Declarative Workflows
* **Imperative (Manual CLI Commands)**:
  ```bash
  # Imperative pod launch
  kubectl run web-pod --image=nginx:alpine --port=80

  # Imperative scale
  kubectl scale deployment web-deploy --replicas=5
  ```
* **Declarative (Production Manifest Files)**:
  * Uses YAML files committed to Git (Infrastructure as Code / GitOps).
  * Applied via `kubectl apply -f manifest.yaml`.
  * Preserves audit trails, enables peer reviews, and supports clean automated rollbacks.

### Workload Evolution Timeline
```text
1. ReplicationController (RC) [Deprecated / Legacy]
   • First generation replication mechanism.
   • Matched pods using Equality-Based selectors only (e.g., tier = frontend).

2. ReplicaSet (RS) [Current Low-Level]
   • Replaced ReplicationController.
   • Supports Set-Based selectors (e.g., environment in (prod, staging)).
   • Rarely created directly; managed automatically by Deployments.

3. Deployment [Production Standard]
   • Manages ReplicaSets declaratively.
   • Provides declarative rolling updates, pause/resume, and zero-downtime rollbacks.
```

### Production Deployment Manifest Blueprint
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: taskflow-backend
  namespace: production
  labels:
    app: taskflow
    tier: backend
spec:
  replicas: 3
  revisionHistoryLimit: 5
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1        # Max pods allowed ABOVE desired replica count during rollout
      maxUnavailable: 0  # Zero downtime: No pods destroyed until new pods pass Readiness probe
  selector:
    matchLabels:
      app: taskflow
      tier: backend
  template:
    metadata:
      labels:
        app: taskflow
        tier: backend
    spec:
      containers:
        - name: api-server
          image: akhil/taskflow-backend:v1.2.0
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 5000
              name: http
          env:
            - name: DB_HOST
              value: "mysql-service"
            - name: DB_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: db-credentials
                  key: password
          resources:
            requests:
              cpu: "100m"
              memory: "128Mi"
            limits:
              cpu: "500m"
              memory: "512Mi"
          readinessProbe:
            httpGet:
              path: /health
              port: 5000
            initialDelaySeconds: 5
            periodSeconds: 10
          livenessProbe:
            httpGet:
              path: /health
              port: 5000
            initialDelaySeconds: 15
            periodSeconds: 20
```

---

## 6. Kubernetes Services Networking

Pods are ephemeral; when a pod is rescheduled, it receives a new, dynamic private IP address. A **Service** provides a stable, permanent virtual IP address and DNS name that load-balances traffic across dynamic backend pod replicas.

### The 4 Service Types

| Service Type | Scope | How It Works |
| :--- | :--- | :--- |
| **`ClusterIP`** | Internal Only | **Default type**. Allocates an internal cluster IP reachable only within the Kubernetes cluster. |
| **`NodePort`** | External | Exposes the service on a static high port (`30000-32767`) across **every single worker node's IP**. |
| **`LoadBalancer`** | External | Interacts with cloud provider APIs (AWS, Azure) to provision an external Cloud Load Balancer (e.g. AWS NLB) pointing to NodePorts. |
| **`ExternalName`** | Internal | Maps the service DNS name to an external CNAME record (e.g., `db.external-provider.com`) without proxying. |

### Service Manifest Example (`ClusterIP`)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: taskflow-backend-svc
  namespace: production
spec:
  type: ClusterIP
  selector:
    app: taskflow
    tier: backend
  ports:
    - name: http
      port: 80         # Port exposed on the Service ClusterIP
      targetPort: 5000 # Port where application container listens inside pod
```

---

## 7. Modern Ingress Networking (`networking.k8s.io/v1`)

A NodePort or LoadBalancer service per application gets prohibitively expensive on public clouds. An **Ingress** acts as a smart application-layer (Layer 7) reverse proxy and router, terminating SSL/TLS and directing external traffic to multiple internal `ClusterIP` services using a single public IP.

### Production Ingress Manifest Blueprint
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: taskflow-ingress
  namespace: production
  annotations:
    kubernetes.io/ingress.class: nginx
    cert-manager.io/cluster-issuer: letsencrypt-prod
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
spec:
  tls:
    - hosts:
        - app.taskflow.com
      secretName: taskflow-tls-secret
  rules:
    - host: app.taskflow.com
      http:
        paths:
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: taskflow-backend-svc
                port:
                  number: 80
          - path: /
            pathType: Prefix
            backend:
              service:
                name: taskflow-frontend-svc
                port:
                  number: 80
```

---

## 8. Persistent Storage Architecture (PV, PVC, StorageClass)

Containers have ephemeral storage. Persistent storage in Kubernetes decouples infrastructure storage provisioning from developer pod definitions.

```text
┌─────────────────────────────────┐
│     Cloud Storage Backend       │ (AWS EBS gp3, Azure Disk, NFS)
└────────────────┬────────────────┘
                 │ Provisioned dynamically by
                 ▼
┌─────────────────────────────────┐
│          StorageClass           │ (Defines provisioner, volume type, reclaimPolicy)
└────────────────┬────────────────┘
                 │ Satisfies
                 ▼
┌─────────────────────────────────┐
│   PersistentVolumeClaim (PVC)   │ (Developer request: "I need 20Gi ReadWriteOnce")
└────────────────┬────────────────┘
                 │ Bound to
                 ▼
┌─────────────────────────────────┐
│     PersistentVolume (PV)       │ (Actual cluster storage volume)
└────────────────┬────────────────┘
                 │ Mounted inside
                 ▼
┌─────────────────────────────────┐
│           Application POD       │
└─────────────────────────────────┘
```

### 1. StorageClass (Dynamic Provisioner)
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-ebs-gp3
provisioner: ebs.csi.aws.com
volumeBindingMode: WaitForFirstConsumer
reclaimPolicy: Retain
parameters:
  type: gp3
  iops: "3000"
  throughput: "125"
```

### 2. PersistentVolumeClaim (PVC)
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-data-pvc
  namespace: production
spec:
  accessModes:
    - ReadWriteOnce # Mounted by single node for read/write
  storageClassName: fast-ebs-gp3
  resources:
    requests:
      storage: 20Gi
```

---

## 9. Configuration & Secrets Management

Never bake configuration values or credentials into container images. Kubernetes cleanly separates code from configuration.

### 1. ConfigMaps (Non-Sensitive Configuration)
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: production
data:
  APP_ENV: "production"
  LOG_LEVEL: "info"
  MAX_CONNECTIONS: "100"
```

### 2. Secrets (Sensitive Credentials)
* Base64 encoded in manifests; stored in `etcd` (must enable encryption at rest).
```bash
# Create secret imperatively
kubectl create secret generic db-credentials   --from-literal=username=dbadmin   --from-literal=password=SuperSecret2026!
```

---

## 10. Health Probes & Auto-Scaling (HPA v2)

### The 3 Health Probes
* **Startup Probe**: Tests if a slow-starting legacy application has booted. Disables liveness and readiness checks until it succeeds.
* **Readiness Probe**: Tests if the container is ready to accept user traffic. If it fails, Kubernetes immediately **removes the pod IP from all Service endpoints** (no traffic sent; container is NOT restarted).
* **Liveness Probe**: Tests if the container process is still functioning or in a deadlock. If it fails, Kubernetes **kills the container and restarts it** according to the restart policy.

### Horizontal Pod Autoscaler (`HPA v2`)
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: taskflow-hpa
  namespace: production
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: taskflow-backend
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 75
```

---

## 11. Specialized Workloads: DaemonSets, StatefulSets, & Jobs

* **`DaemonSet`**:
  * Guarantees that **exactly one copy of a pod runs on every worker node** (or a subset matching node selectors).
  * Ideal for: Node monitoring agents (`prometheus-node-exporter`), log collectors (`fluentbit`), network CNI plugins (`calico-node`).
* **`StatefulSet`**:
  * Designed for stateful clustered systems (Kafka, Elasticsearch, ZooKeeper).
  * Provides **predictable, ordered pod hostnames** (`db-0`, `db-1`, `db-2`), stable DNS names, and dedicated PersistentVolumeClaims per replica.
* **`Job` / `CronJob`**:
  * **Job**: Runs a pod to completion (e.g., database schema migrations) and exits cleanly.
  * **CronJob**: Runs a job on a repeating scheduled cron timetable (e.g., nightly backups).

---

## 12. Essential `kubectl` CLI Command Reference

### Resource Inspection
* `kubectl get nodes -o wide` — List cluster worker and master nodes with OS, kernel, and IP details.
* `kubectl get pods -A` — List pods across all namespaces.
* `kubectl get pods -o wide` — View pod IP addresses and the exact worker node each pod is running on.
* `kubectl describe pod <pod_name>` — View lifecycle events, scheduling decisions, and probe failures.
* `kubectl api-resources` — List all available Kubernetes resource types, API versions, and short names.

### Debugging & Troubleshooting
* `kubectl logs -f <pod_name>` — Tail container stdout/stderr logs.
* `kubectl logs -f <pod_name> -c <container_name>` — Tail logs for a specific container in a multi-container pod.
* `kubectl logs <pod_name> --previous` — View crash logs of the previously terminated container instance.
* `kubectl exec -it <pod_name> -- bash` — Open interactive bash shell inside container.
* `kubectl top nodes` / `kubectl top pods` — View real-time CPU and Memory utilization (requires Metrics Server).

### Maintenance & Operations
* `kubectl apply -f manifest.yaml` — Declaratively create or update resources.
* `kubectl rollout status deployment/<name>` — Monitor live rolling update progression.
* `kubectl rollout undo deployment/<name>` — Instantly roll back to the previous deployment revision.
* `kubectl cordon <node_name>` — Mark node as unschedulable (no new pods placed).
* `kubectl drain <node_name> --ignore-daemonsets --delete-emptydir-data` — Safely evict all running pods from node for maintenance.

---

## 13. Production Troubleshooting Playbook

### Scenario 1: `CrashLoopBackOff`
* **Root Cause**: The application container starts, fails or encounters an unhandled exception, and crashes repeatedly.
* **Diagnosis**:
  ```bash
  kubectl describe pod <pod_name>   # Check Exit Code and Last State
  kubectl logs <pod_name> --previous # Inspect application crash stack trace
  ```
* **Common Causes**: Missing environment variable, database connection refused, bad configuration syntax, OOM killed.

### Scenario 2: `ImagePullBackOff` / `ErrImagePull`
* **Root Cause**: Kubernetes worker node cannot download the specified container image.
* **Diagnosis**:
  ```bash
  kubectl describe pod <pod_name>
  ```
* **Common Causes**: Image tag does not exist on registry, image name typo, missing `imagePullSecrets` for private registries, or Docker Hub rate limits.

### Scenario 3: Pod Stuck in `Pending`
* **Root Cause**: The `kube-scheduler` cannot find a suitable worker node to schedule the pod.
* **Diagnosis**: Look at the bottom `Events` section of `kubectl describe pod <pod_name>`.
* **Common Causes**: Insufficient cluster CPU/Memory requests, node taints not tolerated by pod, `nodeSelector` matches zero nodes, or PersistentVolumeClaim unbound.

---

## 14. Senior DevOps Interview Q&A

### Q1: What is the exact difference between a ReplicaSet and a Deployment?
* A **ReplicaSet** guarantees that a specified number of identical pod replicas are running at any given time using set-based label selectors. However, ReplicaSets do not have native rolling update mechanisms.
* A **Deployment** is a higher-level orchestrator that declaratively manages underlying ReplicaSets. When you update an image tag in a Deployment, it creates a new ReplicaSet, scales it up, and gradually scales down the old ReplicaSet, enabling zero-downtime rolling updates and automated rollbacks.

### Q2: What happens when a container fails a Liveness Probe vs a Readiness Probe?
* **Liveness Probe Failure**: Kubernetes marks the container as unhealthy, terminates the process, and automatically restarts it based on the Pod's `restartPolicy`.
* **Readiness Probe Failure**: Kubernetes **does NOT restart the container**. Instead, it strips the pod's IP address from all matching Service EndpointSlices, preventing incoming user traffic from reaching the pod until it reports healthy again.

### Q3: Why is `etcd` sensitive to disk I/O and latency?
* `etcd` uses the Raft consensus protocol. Every write operation (e.g., updating a pod state) requires a majority quorum of `etcd` peers to acknowledge writing the entry to their Write-Ahead Log (WAL) on disk.
* High disk write latency causes Raft heartbeat election timeouts, leading to leader thrashing, cluster-wide latency spikes, and transient API Server errors. Production `etcd` nodes must run on dedicated NVMe SSDs with low disk latency.

### Q4: ClusterIP vs NodePort vs LoadBalancer vs Ingress — when do you use each?
* **ClusterIP**: Internal cluster communication only. Default type. Used for microservice-to-microservice and database connections.
* **NodePort**: Opens a static port (30000–32767) on every worker node's IP. Used for debugging or legacy on-prem routing.
* **LoadBalancer**: Provisions a dedicated cloud load balancer (AWS NLB/ALB) per service. Expensive if you have dozens of microservices.
* **Ingress**: A single Layer 7 reverse proxy/load balancer routing traffic to dozens of internal ClusterIP services based on hostnames (`api.example.com`) and URL paths (`/orders`), with SSL termination.

### Q5: How do you diagnose and resolve a Pod stuck in `CrashLoopBackOff`?
1. Inspect logs of the container that just crashed: `kubectl logs <pod-name> --previous`.
2. Inspect exit code and reason via `kubectl describe pod <pod-name>`.
   * Exit Code `137`: Killed by OOM killer -> increase memory requests/limits.
   * Exit Code `1`: Application exception (syntax error, missing config/secret, unhandled database timeout).
   * Exit Code `0`: Completed background command without keeping foreground process running.
3. Validate linked Secrets and ConfigMaps exist and have correct keys.

### Q6: How do you troubleshoot a Pod stuck in `Pending` state?
1. Run `kubectl describe pod <pod-name>` and look at `Events` at the bottom.
2. **Insufficient Resources**: If events say `0/6 nodes available: Insufficient cpu/memory`, worker nodes are overcommitted. Fix: Add worker nodes (scale ASG) or reduce Pod resource requests.
3. **Taints and Tolerations**: Worker nodes have taints that the Pod does not tolerate.
4. **Unbound PVC**: If using persistent storage, the PVC is waiting for volume provisioning (`WaitForFirstConsumer`).

### Q7: What is the difference between a Deployment, StatefulSet, and DaemonSet?
* **Deployment**: For stateless applications (REST APIs, web apps). Pods are interchangeable, have random hashes in names (`web-78dfb9-4k2ln`), and share no unique identities.
* **StatefulSet**: For stateful workloads (PostgreSQL, Kafka, Elasticsearch). Pods have stable, predictable ordinal names (`db-0`, `db-1`), dedicated persistent volume claims, and ordered graceful rollouts/terminations.
* **DaemonSet**: Ensures exactly one copy of a Pod runs on every single worker node (or nodes matching nodeSelectors). Used for log collectors (Fluentd, Promtail), node monitoring (node-exporter), and CNI agents (aws-node, Calico).

### Q8: Why are Kubernetes Secrets not secure by default, and how do you secure them in production?
* **Default Vulnerability**: Kubernetes Secrets are merely **base64-encoded strings**, not encrypted! Anyone with RBAC access to `kubectl get secret -o yaml` can decode them trivially (`base64 -d`). In addition, by default `etcd` stores secrets unencrypted on disk.
* **Production Hardening**:
  1. **Encryption at Rest**: Enable KMS envelope encryption in `kube-apiserver` encryption provider config so `etcd` stores ciphertext.
  2. **External Secrets Operator (ESO)** or **AWS Secrets Manager / HashiCorp Vault**: Sync secrets dynamically from enterprise secret stores into memory.
  3. **Sealed Secrets**: Encrypt secrets with public key GitOps workflow so they can safely live in Git repositories.

### Q9: What happens when a Worker Node crashes in a Kubernetes cluster?
1. `kubelet` stops sending periodic heartbeats to `kube-apiserver`.
2. After `node-monitor-grace-period` (default 40s), the **Node Lifecycle Controller** marks the node `NotReady`.
3. After `pod-eviction-timeout` (default 5 minutes), the controller initiates eviction of all Pods on that node.
4. For Deployments, the ReplicaSet controller notices current replicas < desired replicas, and schedules replacement pods onto remaining healthy worker nodes.
5. For StatefulSets, replacement pods are not rescheduled immediately to avoid data corruption (split-brain) until the node is confirmed dead or deleted.

### Q10: How does the Horizontal Pod Autoscaler (HPA v2) interact with Metrics Server and Resource Requests?
* HPA requires the **Metrics Server** to query container CPU/RAM utilization from `kubelet`'s Summary API every 15–30 seconds.
* **Crucial Prerequisite**: HPA computes percentage utilization against the Pod's **`resources.requests`**, NOT `limits`!
* If a Pod does not have `requests.cpu` defined in its manifest, **HPA cannot calculate utilization and autoscaling fails!**
* HPA uses the formula: Desired Replicas = ceil(Current Replicas * (Current Metric Value / Target Metric Value)).
