# 📖 Kubernetes_File_Types_Simple_Guide
> *Converted from `Kubernetes_File_Types_Simple_Guide.pdf` for high-readability on GitHub.*

---
## Page 1

Kubernetes File Types - Simple Guide
1. Pod (pod.yaml)
Defines a single container or a group of containers that run together.
Example:
apiVersion: v1
kind: Pod
metadata:
name: nginx-pod
spec:
containers:
- name: nginx
image: nginx
2. Deployment (deployment.yaml)
Used to manage and update multiple pods easily.
Example:
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
spec:
replicas: 2
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
image: nginx
3. Service (service.yaml)
Exposes pods to network so they can communicate.
Example:
apiVersion: v1
kind: Service
metadata:
name: nginx-service
spec:
selector:
app: nginx
ports:
- port: 80
targetPort: 80
type: NodePort

## Page 2

4. ConfigMap (configmap.yaml)
Stores configuration data for pods.
Example:
apiVersion: v1
kind: ConfigMap
metadata:
name: app-config
data:
APP_ENV: dev
5. Secret (secret.yaml)
Stores passwords or tokens in Base64 format.
Example:
apiVersion: v1
kind: Secret
metadata:
name: db-secret
data:
username: YWRtaW4=
password: MTIzNDU2
6. Namespace (namespace.yaml)
Used to group and organize resources.
Example:
apiVersion: v1
kind: Namespace
metadata:
name: dev
7. DaemonSet (daemonset.yaml)
Runs one pod on every node.
Example:
apiVersion: apps/v1
kind: DaemonSet
metadata:
name: log-agent
spec:
template:
spec:
containers:
- name: agent
image: node-exporter
8. StatefulSet (statefulset.yaml)

## Page 3

Used for databases and apps that need stable storage.
Example:
apiVersion: apps/v1
kind: StatefulSet
metadata:
name: mysql
spec:
replicas: 2
serviceName: mysql
template:
spec:
containers:
- name: mysql
image: mysql
9. Ingress (ingress.yaml)
Manages external access using URLs.
Example:
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: web-ingress
spec:
rules:
- host: myapp.com
http:
paths:
- path: /
pathType: Prefix
backend:
service:
name: nginx-service
port:
number: 80
10. Job (job.yaml)
Runs a task once and stops.
Example:
apiVersion: batch/v1
kind: Job
metadata:
name: print-job
spec:
template:
spec:
containers:
- name: job
image: busybox
command: ['echo', 'Hello']
restartPolicy: Never

## Page 4

11. CronJob (cronjob.yaml)
Runs jobs on a schedule.
Example:
apiVersion: batch/v1
kind: CronJob
metadata:
name: hello-cron
spec:
schedule: "*/2 * * * *"
jobTemplate:
spec:
template:
spec:
containers:
- name: cron
image: busybox
args: ['echo', 'Hello']
restartPolicy: OnFailure

