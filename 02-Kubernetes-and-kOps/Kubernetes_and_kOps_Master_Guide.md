# ☸️ Kubernetes & kOps Production Engineering: The Definitive Master Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Control Plane & Worker Node Internals, AWS kOps Cluster Provisioning, Core Workloads (Pods, Deployments, StatefulSets, DaemonSets), Services & Ingress, Storage (PV/PVC/StorageClass), RBAC Security, ConfigMaps & Secrets, Deployment Strategies (Rolling, Canary, Blue-Green), and Production Troubleshooting Playbooks.

---

## 📑 Table of Contents
- [1. Why Kubernetes? (Docker Drawbacks & Orchestration)](#1-why-kubernetes-docker-drawbacks--orchestration)
- [2. Kubernetes Architecture Internals](#2-kubernetes-architecture-internals)
- [3. AWS Kubernetes Cluster Provisioning with kOps](#3-aws-kubernetes-cluster-provisioning-with-kops)
- [4. Pods, ReplicaSets, and Deployments](#4-pods-replicasets-and-deployments)
- [5. Kubernetes Services (ClusterIP, NodePort, LoadBalancer)](#5-kubernetes-services-clusterip-nodeport-loadbalancer)
- [6. Modern Ingress Networking (`networking.k8s.io/v1`)](#6-modern-ingress-networking-networkingk8siov1)
- [7. Persistent Storage Architecture (PV, PVC, StorageClass)](#7-persistent-storage-architecture-pv-pvc-storageclass)
- [8. ConfigMaps & Secrets Management](#8-configmaps--secrets-management)
- [9. Role-Based Access Control (RBAC) & ServiceAccounts](#9-role-based-access-control-rbac--serviceaccounts)
- [10. Specialized Workloads: DaemonSets, StatefulSets, & Jobs](#10-specialized-workloads-daemonsets-statefulsets--jobs)
- [11. Production Deployment Strategies (Rolling, Blue-Green, Canary)](#11-production-deployment-strategies-rolling-blue-green-canary)
- [12. Production Troubleshooting Playbook](#12-production-troubleshooting-playbook)
- [13. Essential `kubectl` CLI Quick Reference](#13-essential-kubectl-cli-quick-reference)
- [14. Senior DevOps Interview Q&A](#14-senior-devops-interview-qa)

---

## 1. Why Kubernetes? (Docker Drawbacks & Orchestration)

### Limitations of Standalone Docker
* **Single-Host Limitation**: Containers run on only one physical or virtual machine; no native pooling of cluster compute resources.
* **No Self-Healing**: If a container process crashes or a host server dies, manual human intervention is required to restart it.
* **Manual Scaling**: Increasing container instances requires manual CLI commands per host with no auto-scaling.
* **Zero-Downtime Updates**: Deploying new image versions causes temporary connection drops and service downtime.
* **Complex Networking**: Cross-host container communication requires custom complex overlay network configurations.

### Docker Swarm vs Kubernetes Comparison

| Capability | Docker Swarm | Kubernetes (K8s) |
| :--- | :--- | :--- |
| **Setup & Complexity** | Simple, integrated directly into Docker CLI | Complex initial setup, steep learning curve |
| **Scaling Capacity** | Best for small-to-medium clusters (< 500 nodes) | Massive enterprise scale (5,000+ nodes) |
| **Ecosystem & Community** | Limited third-party tooling | Industry standard (CNCF ecosystem, Helm, ArgoCD) |
| **Auto-Scaling** | Basic manual scaling | Dynamic HPA (Horizontal Pod Autoscaler) & VPA |
| **Storage & Networking** | Basic overlay networking | Rich CNI plugins (Calico, Flannel, AWS VPC CNI) |
| **Enterprise Adoption** | Low | Universal industry standard across cloud providers |

---

## 2. Kubernetes Architecture Internals

### High-Level Cluster Architecture
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
│   ┌──────────────┐                                                          │
│   │  etcd Store  │ (Consistent, distributed key-value database: state/specs)│
│   └──────────────┘                                                          │
└──────────┬──────────────────────────────────────────────────────────────────┘
           │ gRPC / HTTPS
           ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         WORKER NODES (Compute Plane)                        │
│                                                                             │
│   ┌────────────────────────────────┐     ┌──────────────────────────────┐   │
│   │          Worker Node 1         │     │         Worker Node 2        │   │
│   │  ┌──────────┐  ┌────────────┐  │     │  ┌──────────┐  ┌──────────┐  │   │
│   │  │ kubelet  │  │ kube-proxy │  │     │  │ kubelet  │  │kube-proxy│  │   │
│   │  └────┬─────┘  └─────┬──────┘  │     │  └────┬─────┘  └────┬─────┘  │   │
│   │       ▼              ▼         │     │       ▼             ▼        │   │
│   │  ┌──────────────────────────┐  │     │  ┌────────────────────────┐  │   │
│   │  │ containerd CRI / Pods    │  │     │  │ containerd CRI / Pods  │  │   │
│   │  └──────────────────────────┘  │     │  └────────────────────────┘  │   │
│   └────────────────────────────────┘     └──────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Control Plane Components
* **`kube-apiserver`**:
  * Front door of the cluster; exposes the Kubernetes REST API.
  * Authenticates, authorizes, and validates all cluster operations from `kubectl` and internal components.
  * Only component that reads from or writes to `etcd`.
* **`etcd`**:
  * Distributed, highly-available key-value store.
  * Single source of truth containing cluster configuration, specifications, and actual runtime states.
* **`kube-scheduler`**:
  * Watches for unscheduled pods and selects the optimal worker node to run them.
  * Considers resource requests/limits, affinity/anti-affinity rules, taints/tolerations, and node availability.
* **`kube-controller-manager` (KCM)**:
  * Runs continuous reconciliation control loops comparing actual state with desired state.
  * Sub-controllers: Node Controller, ReplicaSet Controller, EndpointSlice Controller, ServiceAccount Controller.
* **`cloud-controller-manager` (CCM)**:
  * Integrates with underlying cloud provider APIs to provision cloud load balancers, EBS volumes, and routes.

### Worker Node Components
* **`kubelet`**:
  * Primary agent running on every worker node.
  * Receives `PodSpec` objects from API server and communicates with container runtime via CRI to ensure containers run healthy.
  * Reports node status and pod health back to API server.
* **`kube-proxy`**:
  * Network proxy running on each node managing iptables or IPVS packet forwarding rules.
  * Directs traffic sent to Service virtual IPs (ClusterIP) to backend pod endpoints.
* **Container Runtime (CRI)**:
  * Low-level software executing containers (e.g., `containerd`, `CRI-O`).

---

## 3. AWS Kubernetes Cluster Provisioning with kOps

### What is kOps (Kubernetes Operations)?
* Production-grade CLI tool for provisioning, upgrading, and managing self-managed Kubernetes clusters on AWS and GCE.
* Automates creation of AWS EC2 instances, Auto Scaling Groups (ASGs), VPCs, Route53 records, and IAM roles.

### 5-Step Production kOps Provisioning Workflow
```bash
# 1. Create a versioned S3 bucket for cluster state storage
aws s3api create-bucket   --bucket devops-kops-state-store   --region us-east-1

aws s3api put-bucket-versioning   --bucket devops-kops-state-store   --versioning-configuration Status=Enabled

# 2. Export environment variables
export KOPS_STATE_STORE=s3://devops-kops-state-store
export CLUSTER_NAME=k8s.cloudvault.internal

# 3. Create cluster definition
kops create cluster   --name=${CLUSTER_NAME}   --state=${KOPS_STATE_STORE}   --zones=us-east-1a,us-east-1b   --node-count=2   --node-size=t3.medium   --control-plane-size=t3.medium   --dns=private

# 4. Apply and build cloud infrastructure in AWS
kops update cluster --name ${CLUSTER_NAME} --yes --admin

# 5. Validate cluster readiness
kops validate cluster --wait 10m
```

---

## 4. Pods, ReplicaSets, and Deployments

### The Hierarchy of Compute Workloads
* **Pod**: Smallest deployable unit in Kubernetes; encapsulates one or more co-located containers sharing network namespaces and storage.
* **ReplicaSet**: Ensures a specified number of identical pod replicas are running at all times using label selectors.
* **Deployment**: Higher-level controller managing ReplicaSets; provides declarative updates, rolling upgrades, and instant rollbacks.

### Production Deployment Manifest (`deployment.yaml`)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-deployment
  namespace: production
  labels:
    app: api-server
spec:
  replicas: 3
  revisionHistoryLimit: 5
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  selector:
    matchLabels:
      app: api-server
  template:
    metadata:
      labels:
        app: api-server
    spec:
      containers:
        - name: api
          image: myrepo/api:v1.2.0
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 8080
          resources:
            requests:
              cpu: "250m"
              memory: "256Mi"
            limits:
              cpu: "500m"
              memory: "512Mi"
          readinessProbe:
            httpGet:
              path: /health/ready
              port: 8080
            initialDelaySeconds: 10
            periodSeconds: 5
          livenessProbe:
            httpGet:
              path: /health/live
              port: 8080
            initialDelaySeconds: 15
            periodSeconds: 10
```

### Deployment Rollout Commands
```bash
# Check status of rolling update
kubectl rollout status deployment/api-deployment -n production

# View deployment rollout history with revisions
kubectl rollout history deployment/api-deployment -n production

# Undo update and rollback to previous stable revision
kubectl rollout undo deployment/api-deployment -n production

# Rollback to a specific historical revision number
kubectl rollout undo deployment/api-deployment --to-revision=2 -n production
```

---

## 5. Kubernetes Services (ClusterIP, NodePort, LoadBalancer)

### Service Types Matrix

| Service Type | Scope & Visibility | How Traffic Enters | Production Use Case |
| :--- | :--- | :--- | :--- |
| **`ClusterIP`** | Internal only (Default) | Virtual IP inside cluster network | Internal microservice communication, databases |
| **`NodePort`** | Cluster-wide on Node IPs | Dedicated port per node (`30000-32767`) | Non-HTTP legacy apps, internal testing |
| **`LoadBalancer`**| Public Internet / Cloud | Provisions AWS NLB/ALB or GCP LB | Exposing external edge services directly |

### Production Service Manifest (`service.yaml`)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: api-service
  namespace: production
  labels:
    app: api-server
spec:
  type: ClusterIP
  selector:
    app: api-server
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 8080
```

---

## 6. Modern Ingress Networking (`networking.k8s.io/v1`)

### Why Ingress?
* Instead of creating an expensive separate Cloud Load Balancer per microservice, **Ingress** acts as a smart layer 7 reverse proxy routing traffic based on hostnames and URL paths using a single load balancer.

### Ingress Manifest (`ingress.yaml`)
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: edge-ingress
  namespace: production
  annotations:
    kubernetes.io/ingress.class: nginx
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  rules:
    - host: api.cloudvault.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: api-service
                port:
                  number: 80
```

---

## 7. Persistent Storage Architecture (PV, PVC, StorageClass)

### The Storage Abstraction Workflow
```text
┌────────────────────────┐      ┌────────────────────────┐      ┌────────────────────────┐
│      StorageClass      │─────►│ PersistentVolumeClaim  │─────►│    PersistentVolume    │
│ (Dynamic AWS EBS/gp3)  │      │     (PVC - Request)    │      │    (PV - Actual Disk)  │
└────────────────────────┘      └────────────────────────┘      └────────────────────────┘
```

* **StorageClass (SC)**: Defines the storage provisioner (e.g., AWS EBS CSI `ebs.csi.aws.com`), disk type (`gp3`), and IOPS profile.
* **PersistentVolumeClaim (PVC)**: The developer's request for storage (e.g., *"give me 50Gi of ReadWriteOnce storage"*).
* **PersistentVolume (PV)**: The physical cloud disk bound to the claim.

### Storage Manifests
```yaml
# 1. Dynamic StorageClass
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-ebs-gp3
provisioner: ebs.csi.aws.com
volumeBindingMode: WaitForFirstConsumer
parameters:
  type: gp3
  iops: "3000"
  throughput: "125"

---
# 2. PersistentVolumeClaim
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgres-pvc
  namespace: production
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: fast-ebs-gp3
  resources:
    requests:
      storage: 20Gi
```

---

## 8. ConfigMaps & Secrets Management

### Decoupling Configuration from Container Images
* **ConfigMap**: Stores plain-text key-value configuration pairs, environment variables, or configuration files (e.g., `nginx.conf`).
* **Secret**: Stores sensitive data (passwords, tokens, SSH keys, TLS certificates); base64 encoded by default.

### ConfigMap & Secret Manifests
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: production
data:
  ENVIRONMENT: "production"
  LOG_LEVEL: "info"
  MAX_CONNECTIONS: "100"

---
apiVersion: v1
kind: Secret
metadata:
  name: app-secrets
  namespace: production
type: Opaque
stringData:
  DATABASE_PASSWORD: "SuperSecureProductionPassword123"
```

---

## 9. Role-Based Access Control (RBAC) & ServiceAccounts

### RBAC Core Elements
* **`ServiceAccount`**: Identity allocated to in-cluster processes and pods.
* **`Role`**: Namespaced list of permitted API actions (`get`, `list`, `watch`, `create`, `delete`) on resources.
* **`RoleBinding`**: Attaches a Role to a User, Group, or ServiceAccount within a specific namespace.
* **`ClusterRole` & `ClusterRoleBinding`**: Cluster-wide permissions (spanning all namespaces and non-namespaced nodes).

### RBAC Manifest Example
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: production
rules:
  - apiGroups: [""]
    resources: ["pods", "pods/log"]
    verbs: ["get", "list", "watch"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: production
subjects:
  - kind: ServiceAccount
    name: monitoring-agent
    namespace: production
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## 10. Specialized Workloads: DaemonSets, StatefulSets, & Jobs

### 1. `DaemonSet`
* Ensures that **all (or selected) worker nodes run exactly one copy** of a pod.
* **Use Cases**: Node monitoring agents (`prometheus-node-exporter`), log collectors (`fluent-bit`), networking daemons (`kube-proxy`, CNI plugins).

### 2. `StatefulSet`
* Manages stateful applications requiring **stable, unique network identifiers** and **persistent, ordered storage**.
* Pod naming follows predictable ordinal numbers: `kafka-0`, `kafka-1`, `kafka-2`.
* Utilizes `volumeClaimTemplates` so each replica receives its own dedicated persistent disk.
* **Use Cases**: Distributed databases (PostgreSQL HA, MongoDB, Cassandra, Kafka, ZooKeeper).

### 3. `Job` & `CronJob`
* **`Job`**: Runs batch tasks until completion (ensures pods terminate cleanly with exit code 0).
* **`CronJob`**: Schedules jobs on a periodic time basis using standard crontab syntax.

---

## 11. Production Deployment Strategies (Rolling, Blue-Green, Canary)

### Strategy Comparison Matrix

| Strategy | Downtime | Resource Cost | Rollback Speed | Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **RollingUpdate** | Zero | Minimal (surge +1) | Moderate (`rollout undo`) | Low (Native K8s) |
| **Recreate** | Brief downtime | Low (destroys old first)| Slow (rebuild required) | Lowest |
| **Blue-Green** | Zero | Double (100% blue + 100% green)| Instant (switch Service selector)| Moderate |
| **Canary** | Zero | Minimal (route 5-10% traffic) | Fast (delete canary pods)| Advanced (requires Service Mesh/Ingress) |

---

## 12. Production Troubleshooting Playbook

### The 8-Step Emergency Diagnostic Sequence
* **Step 1: Check Pod Status**: `kubectl get pods -n <namespace> -o wide`
* **Step 2: Inspect Kubernetes Events**: `kubectl describe pod <pod-name> -n <namespace>`
* **Step 3: Read Application Logs**: `kubectl logs <pod-name> -n <namespace> --tail=100`
* **Step 4: Check Previous Crashed Run**: `kubectl logs <pod-name> -n <namespace> --previous`
* **Step 5: Shell into Container**: `kubectl exec -it <pod-name> -n <namespace> -- sh`
* **Step 6: Check Cluster-Wide Events**: `kubectl get events -n <namespace> --sort-by='.metadata.creationTimestamp'`
* **Step 7: Check CPU & Memory Pressure**: `kubectl top pods -n <namespace>` and `kubectl top nodes`
* **Step 8: Check Worker Node Health**: `kubectl describe node <node-name>`

### Common Kubernetes Error Codes & Solutions

| Error Code | Primary Root Cause | Exact Remediation Action |
| :--- | :--- | :--- |
| **`CrashLoopBackOff`** | Application crashed on startup (bad env, failed DB connection, unhandled exception) | Run `kubectl logs <pod> --previous` to inspect the exact fatal application stack trace. |
| **`ImagePullBackOff`** | Incorrect image name/tag, or missing registry secret | Verify image tag on Docker Hub/ECR; ensure `imagePullSecrets` is attached. |
| **`Pending`** | Insufficient CPU/Memory on worker nodes, or node selector mismatch | Run `kubectl describe pod <pod>`; add worker nodes or reduce resource requests. |
| **`OOMKilled` (Exit 137)** | Container exceeded memory limit defined in `resources.limits.memory` | Increase memory limit in Deployment manifest or optimize container memory leaks. |
| **`CreateContainerConfigError`** | Referenced ConfigMap or Secret does not exist | Run `kubectl describe pod <pod>`; verify missing Secret or ConfigMap names. |

---

## 13. Essential `kubectl` CLI Quick Reference

```bash
# Cluster Inspection
kubectl cluster-info
kubectl get nodes -o wide

# Pod & Workload Inspection
kubectl get pods -A
kubectl get pods -n production -l app=api-server
kubectl get deployment,svc,ingress -n production

# Detailed Inspection & Logs
kubectl describe pod <pod-name> -n production
kubectl logs -f <pod-name> -n production
kubectl logs -f deployment/api-deployment -n production

# Live Shell & Port Forwarding
kubectl exec -it <pod-name> -n production -- /bin/sh
kubectl port-forward svc/api-service 8080:80 -n production

# Scaling & Updates
kubectl scale deployment/api-deployment --replicas=5 -n production
kubectl set image deployment/api-deployment api=myrepo/api:v1.3.0 -n production
kubectl rollout status deployment/api-deployment -n production
kubectl rollout undo deployment/api-deployment -n production
```

---

## 14. Senior DevOps Interview Q&A

### Q1: What happens under the hood when a pod is created?
* Operator runs `kubectl apply -f pod.yaml` sending request to `kube-apiserver`.
* `kube-apiserver` authenticates user, validates manifest, and writes pod spec to `etcd`.
* `kube-scheduler` detects new pod with no `nodeName` assigned; evaluates nodes (filtering and scoring) and writes node assignment back to `kube-apiserver`.
* `kubelet` on the assigned worker node detects pod scheduled to itself; calls container runtime via CRI (`containerd`) to pull image and run containers.
* `kubelet` invokes CNI plugin to assign pod IP address; reports running state back to `kube-apiserver`.

### Q2: What is the exact difference between Liveness and Readiness probes?
* **Liveness Probe**: Checks if the container process is alive. If it fails, `kubelet` kills and restarts the container based on restart policy.
* **Readiness Probe**: Checks if the container is ready to accept user network traffic. If it fails, Kubernetes leaves the container alive but **removes its IP from the Service endpoint list**, preventing user requests from routing to it during warmup or high load.

### Q3: Why should you avoid using NodePort in enterprise production?
* Exposes ports in a narrow restricted range (`30000-32767`).
* Leaves node host ports exposed to network port scans.
* Binds port exclusively per node (two services cannot share the same port).
* **Enterprise Standard**: Use `ClusterIP` combined with an `Ingress Controller` (Nginx, Traefik, AWS ALB Controller) backed by TLS certificates.
