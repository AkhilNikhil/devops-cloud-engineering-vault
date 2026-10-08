# 📖 Kops_and_Kubectl_Installation_and_Setup_on_AWS
> *Converted from `Kops_and_Kubectl_Installation_and_Setup_on_AWS.pdf` for high-readability on GitHub.*

---
## Page 1

■ Kops & Kubectl Installation on AWS EC2 - Step-by-Step (With Full Explanation)
1■■ Install AWS CLI
Command:
sudo yum install -y awscli
■ Explanation:
- Installs the AWS Command Line Interface (CLI) on your EC2 instance.
- yum is the package manager for Amazon Linux / RHEL systems.
- The -y flag auto-confirms installation.
- AWS CLI allows you to authenticate and interact with AWS resources directly from your terminal.
- Kops internally uses the AWS CLI to:
  - Create EC2 instances (for master & worker nodes),
  - Create S3 buckets (for state store),
  - Create IAM roles,
  - Manage VPCs and networking.
■ Verify Installation:
aws --version
2■■ Download the Kops Binary
Command:
curl -LO https://github.com/kubernetes/kops/releases/latest/download/kops-linux-amd64
■ Explanation:
- curl downloads files from URLs.
- -L → follows redirects (since GitHub release URLs often redirect).
- -O → saves the file with its original name (kops-linux-amd64).
- This fetches the latest stable release of Kops for Linux (64-bit).
Why it’s needed:
Kops (Kubernetes Operations) automates the setup of Kubernetes clusters on AWS (and other clouds).
It handles:
- VPC and subnet creation,
- EC2 instance provisioning,
- Cluster networking,
- Generating cluster manifests.
■ Check file:
ls -l kops-linux-amd64
3■■ Install Kops to System Path
Command:
sudo install -m 0755 kops-linux-amd64 /usr/local/bin/kops
■ Explanation:
- Moves the downloaded binary to /usr/local/bin, a directory included in your PATH.
- -m 0755 sets permissions:
  - 7 (read/write/execute) for owner,
  - 5 (read/execute) for group and others.
- This allows you to run kops from any directory globally.
■ Verify Installation:
kops version
4■■ Download Kubectl (Kubernetes CLI Tool)
Command:
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
■ Explanation:
- Downloads the latest stable version of kubectl.
- The inner command $(curl -L -s https://dl.k8s.io/release/stable.txt) dynamically fetches the current stable Kubernetes version.

## Page 2

- Then it constructs the complete download URL for that version’s binary.
Why it’s needed:
- kubectl is the official CLI tool to interact with Kubernetes clusters.
- Once Kops creates the cluster, kubectl is used to:
  - Deploy workloads (pods, services, deployments),
  - Manage configurations,
  - Monitor cluster status.
■ Check download:
ls -l kubectl
5■■ Install Kubectl Globally
Command:
sudo install -m 0755 kubectl /usr/local/bin/kubectl
■ Explanation:
- Installs kubectl to /usr/local/bin, making it accessible system-wide.
- Sets proper executable permissions using 0755.
■ Verify Installation:
kubectl version --client
■■ Additional AWS Setup Required for Kops
Before creating the cluster, ensure these are ready ■
Component | Purpose | Required
-----------|----------|----------
IAM User / Role | Grants permissions to manage EC2, S3, IAM, Route53 | ■ Yes
S3 Bucket | Stores cluster state and configuration files | ■ Yes
Route53 Hosted Zone | Used for DNS names (e.g., cluster.k8s.local) | ■■ Optional
SSH Key Pair | Provides secure SSH access to master and worker nodes | ■ Yes
Ubuntu AMI | Defines OS image for EC2 nodes | ■ Yes
AWS CLI Configured | Provides credentials to Kops via aws configure | ■ Yes
■ Example AWS Setup Commands
1. Create S3 Bucket for State Store
aws s3 mb s3://my-kops-state-store --region us-east-1
export KOPS_STATE_STORE=s3://my-kops-state-store
2. Generate SSH Key Pair
ssh-keygen -t rsa
This creates:
~/.ssh/id_rsa → private key
~/.ssh/id_rsa.pub → public key used by Kops for SSH access
■ Create the Cluster
Command:
kops create cluster --name=mycluster.k8s.local --state=s3://my-kops-state-store --zones=us-east-1a --master-size=t3.medium --node-size=t3.micro --node-count=2 --image=ami-01637463b2cbe7cb6 --yes
Explanation:
- --name → name of the cluster (must end with .k8s.local if no Route53 domain).
- --state → where Kops stores configuration (S3 bucket).
- --zones → AWS availability zones for nodes.
- --master-size & --node-size → EC2 instance types.
- --node-count → number of worker nodes.
- --yes → confirms creation without prompting.
■ After creation:

## Page 3

Use kubectl to check your cluster:
kubectl get nodes
kubectl get pods --all-namespaces

