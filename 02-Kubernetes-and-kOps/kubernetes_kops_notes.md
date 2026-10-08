# 📖 kubernetes_kops_notes
> *Converted from `kubernetes_kops_notes.pdf` for high-readability on GitHub.*

---
## Page 1

Kubernetes & Kops Complete Notes
Kubernetes (K8s) Overview

Container Orchestration tool used to manage containerized applications.

Ensures high availability, scalability, and automated deployments.
Key Kubernetes Components

Master Node - manages cluster

Worker Node - runs applications

etcd - key-value store for cluster state

Kube-apiserver - API server

Kube-scheduler - schedules pods to nodes

Kube-controller-manager - controls cluster state

Kubelet - runs on each node, manages containers

kube-proxy - manages networking
Important Kubernetes Objects

Pod - smallest deployable unit

ReplicaSet - ensures number of pod replicas

Deployment - manages ReplicaSets

Service - exposes app inside/outside cluster

Namespace - logical separation

ConfigMap & Secret - config data storage
Important Kubernetes Commands

kubectl get nodes/pods/services

kubectl apply -f file.yaml

kubectl describe pod

kubectl logs

kubectl delete -f file.yaml
Kops Overview

Kops = Kubernetes Operations

Used to create, manage, and destroy K8s clusters on AWS
Steps to Create Cluster Using Kops

1. Create S3 bucket for state storage

2. Export S3 bucket as KOPS_STATE_STORE

3. Create cluster: kops create cluster --zones

4. Update/Deploy cluster: kops update cluster --yes

5. Validate cluster: kops validate cluster
Important Kops Commands

## Page 2


kops get cluster

kops get ig

kops update cluster --yes

kops validate cluster

kops delete cluster --yes

