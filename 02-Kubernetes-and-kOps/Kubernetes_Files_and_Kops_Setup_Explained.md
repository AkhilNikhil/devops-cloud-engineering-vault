# 📖 Kubernetes_Files_and_Kops_Setup_Explained
> *Converted from `Kubernetes_Files_and_Kops_Setup_Explained.pdf` for high-readability on GitHub.*

---
## Page 1

Kubernetes Files and Kops Setup Explained
1. Kubernetes File Types
Kubernetes uses YAML configuration files to define and manage resources. Each file describes
how a specific component of the cluster should behave. Below are the main file types with
examples and explanations.
→ Pod File
A Pod is the smallest deployable unit in Kubernetes that contains one or more containers sharing
the same network and storage space.
Example:
apiVersion: v1
kind: Pod
metadata:
name: mypod
spec:
containers:
- name: nginx-container
image: nginx
ports:
- containerPort: 80
→ Deployment File
Used to manage a set of identical Pods. It ensures that a specified number of Pods are running at
all times.
Example:
apiVersion: apps/v1
kind: Deployment
metadata:
name: my-deployment
spec:
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
→ Service File

## Page 2

A Service exposes Pods to the network. It allows external or internal access to your applications.
Example:
apiVersion: v1
kind: Service
metadata:
name: my-service
spec:
selector:
app: nginx
ports:
- protocol: TCP
port: 80
targetPort: 80
type: LoadBalancer
→ Namespace File
Namespaces help organize and isolate resources within the same cluster.
Example:
apiVersion: v1
kind: Namespace
metadata:
name: dev-environment
→ ConfigMap File
Stores configuration data in key-value pairs for your applications.
Example:
apiVersion: v1
kind: ConfigMap
metadata:
name: app-config
data:
APP_ENV: production
APP_DEBUG: "false"
→ Secret File
Used to store sensitive information like passwords or tokens.
Example:
apiVersion: v1
kind: Secret
metadata:
name: db-secret
type: Opaque
data:
username: YWRtaW4=
password: MTIzNDU2
→ Ingress File
Ingress manages external access to services within a cluster, typically via HTTP/HTTPS.
Example:

## Page 3

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: example-ingress
spec:
rules:
- host: myapp.example.com
http:
paths:
- path: /
pathType: Prefix
backend:
service:
name: my-service
port:
number: 80
2. Kops Setup on AWS Explained
To create and manage Kubernetes clusters on AWS using Kops, you need to install a few essential
tools. Each command below has a purpose in setting up the environment.
1. Install AWS CLI
Command:
sudo yum install -y awscli
Explanation:
The AWS Command Line Interface (CLI) allows you to interact with AWS services directly from the
terminal. It's needed by Kops to create resources such as EC2 instances, S3 buckets, and
networking components.
2. Download Kops Binary
Command:
curl -LO https://github.com/kubernetes/kops/releases/latest/download/kops-linux-amd64
Explanation:
This downloads the latest Linux binary of Kops from its official GitHub release page. Kops is the
main tool for managing Kubernetes clusters on AWS.
3. Install Kops
Command:
sudo install -m 0755 kops-linux-amd64 /usr/local/bin/kops
Explanation:
This installs the downloaded binary into the /usr/local/bin directory, making it available globally as a
command-line tool.
4. Download kubectl
Command:
curl -LO "https://dl.k8s.io/release/$(curl -L -s
https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

## Page 4

Explanation:
Kubectl is the Kubernetes command-line tool used to interact with clusters — for example,
deploying applications, viewing logs, or scaling pods.
5. Install kubectl
Command:
sudo install -m 0755 kubectl /usr/local/bin/kubectl
Explanation:
This installs kubectl globally, giving you direct control over the Kubernetes cluster that Kops
creates.
■ Summary:
 Kubernetes YAML files define how components like Pods, Services, and Deployments behave.
 Kops helps create production-grade Kubernetes clusters on AWS.
 AWS CLI, Kops, and Kubectl work together — AWS CLI manages AWS resources, Kops
provisions the cluster, and Kubectl controls it.

