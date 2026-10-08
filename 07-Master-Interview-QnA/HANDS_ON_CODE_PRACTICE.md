# 🛠️ Enterprise AWS DevOps Hands-On Code Practice & Memorization Blueprint

Use this document to **memorize** each production manifest, understand **why each line exists**, and then **practice typing it** into the empty box below each section.

---

## 📌 TASK 1: Multi-Stage Dockerfile (Node.js)

### 💡 Complete Model Answer (Memorize This)
```dockerfile
# Stage 1: Build Stage (installs dev tools, compiles code)
FROM node:18-alpine AS builder
WORKDIR /app

# Cache layer: Only re-runs npm ci if package files change
COPY package*.json ./
RUN npm ci

# Copy rest of application code and compile
COPY . .
RUN npm run build

# Stage 2: Production Runner (Lean, clean & secure)
FROM node:18-alpine
WORKDIR /app
ENV NODE_ENV=production

# Security: Never run containers as root in production!
USER node

# Copy only build output and production dependencies from builder stage
COPY --from=builder --chown=node:node /app/package*.json ./
COPY --from=builder --chown=node:node /app/node_modules ./node_modules
COPY --from=builder --chown=node:node /app/dist ./dist

EXPOSE 3000
CMD ["node", "dist/index.js"]
```
"================================================================="
FROM node:18-alpine AS builder
WORKDIR /app

COPY package* .json ./
RUN npm ci

COPY . .
RUN npm run build 

FROM node:18-alpine 
WORKDIR /app
ENV NODE_ENV=production

USER node

COPY --from=builder --chown=node:node /app/package*.json ./
COPY --from=builder --chown=node:node /app/node_modules ./node_modules
COPY --from=builder --chown=node:node /app/dist ./dist

EXPOSE 3000
CMD ["node","dist/index.js"]




### 🧠 Why Each Line Exists (What Interviewers Check For):
1. **`FROM ... AS builder`**: Names the stage so Stage 2 can reference it with `--from=builder`.
2. **`COPY package*.json ./` followed by `RUN npm ci`**: **Docker Layer Caching**. If application source code changes but dependencies don't, Docker skips `npm ci` and builds instantly.
3. **`npm ci` vs `npm install`**: `npm ci` uses `package-lock.json` strictly for deterministic, reproducible builds without modifying dependencies.
4. **`USER node`**: Switches away from `root` user. If a vulnerability is exploited in your app, attacker doesn't get root access to host VM kernel.
5. **`COPY --from=builder --chown=node:node`**: Copies ONLY compiled JS files (`dist`) and node_modules, throwing away Git files, TypeScript compilers, test files, and linters, dropping image size by ~80% (from 1GB to <120MB).

```dockerfile
# 👉 TYPE YOUR DOCKERFILE BELOW THIS LINE FROM MEMORY:




```

---

## 📌 TASK 2: Docker Compose (Web App + Database)

### 💡 Complete Model Answer (Memorize This)
```yaml
version: '3.8'

services:
  web-app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: Enterprise AWS_web
    restart: always
    ports:
      - "80:3000"          # HostPort : ContainerPort
    environment:
      - DB_HOST=db        # Uses the service name 'db' as DNS hostname
      - DB_USER=appuser
      - DB_PASSWORD=secretpass
      - DB_NAME=companydb
    depends_on:
      - db
    networks:
      - app-network

  db:
    image: mysql:8.0
    container_name: Enterprise AWS_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: companydb
      MYSQL_USER: appuser
      MYSQL_PASSWORD: secretpass
    volumes:
      - db_data:/var/lib/mysql   # Named volume for persistence
    networks:
      - app-network

volumes:
  db_data:                 # Declares the named volume

networks:
  app-network:             # Isolated bridge network
    driver: bridge
```

### 🧠 Why Each Line Exists:
1. **`DB_HOST=db`**: Docker's internal DNS automatically resolves the service name `db` to the container's IP address on the shared bridge network.
2. **`volumes: - db_data:/var/lib/mysql`**: Containers are ephemeral. If MySQL crashes or restarts, without a named volume, all database records are wiped out.
3. **`depends_on: - db`**: Ensures Docker starts the database container before launching the application container.
4. **`ports: - "80:3000"`**: Binds host machine port 80 to container internal port 3000. Notice `db` does *not* expose its port 3306 to the host (security best practice—db is only accessible within `app-network`).

```yaml
# 👉 TYPE YOUR DOCKER COMPOSE BELOW THIS LINE FROM MEMORY:




```

---

## 📌 TASK 3: Kubernetes Deployment & Service

### 💡 Complete Model Answer (Memorize This)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: auth-service-deploy
  namespace: production
  labels:
    app: auth-service
spec:
  replicas: 3
  selector:
    matchLabels:
      app: auth-service          # MUST match template.metadata.labels!
  template:
    metadata:
      labels:
        app: auth-service        # Pod label used by ReplicaSet & Service
    spec:
      containers:
      - name: auth-container
        image: 123456789012.dkr.ecr.ap-south-1.amazonaws.com/auth-service:v1.0.0
        ports:
        - containerPort: 8080
        resources:
          requests:
            cpu: "250m"          # Guaranteed 0.25 vCPU
            memory: "256Mi"      # Guaranteed 256MB RAM
          limits:
            cpu: "500m"          # Throttled if exceeding 0.5 vCPU
            memory: "512Mi"      # OOMKilled (Exit 137) if exceeding 512MB RAM
        livenessProbe:
          httpGet:
            path: /healthz
            port: 8080
          initialDelaySeconds: 15
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8080
          initialDelaySeconds: 5
          periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: auth-service
  namespace: production
spec:
  type: ClusterIP                # Internal DNS service
  selector:
    app: auth-service            # Routes traffic to pods with this label
  ports:
  - protocol: TCP
    port: 80                     # Service port inside cluster
    targetPort: 8080             # Container port on the pod
```

### 🧠 Why Each Line Exists:
1. **The Golden Selector Rule**: `spec.selector.matchLabels.app` **must be identical** to `spec.template.metadata.labels.app`. If they differ, `kubectl apply` errors out immediately.
2. **Requests vs Limits**:
   * `requests`: Kube-scheduler uses this to decide which EC2 node has enough room to place the pod.
   * `limits`: Linux cgroups enforce this. If CPU exceeds limit, pod is throttled (slowed down). If Memory exceeds limit, kernel triggers **OOMKilled (`Exit Code 137`)**.
3. **Liveness vs Readiness Probe**:
   * `livenessProbe`: "Is the app dead/frozen?" If fails ➔ kubelet **restarts** container.
   * `readinessProbe`: "Is the app ready to accept user requests?" If fails ➔ pod is **removed from Service endpoints** (no traffic routed to it), but pod is NOT killed.
4. **Service `port` vs `targetPort`**:
   * `port` = 80: What other microservices call (`http://auth-service:80`).
   * `targetPort` = 8080: The actual port listening inside the container (`containerPort`).

```yaml
# 👉 TYPE YOUR K8S DEPLOYMENT & SERVICE BELOW THIS LINE FROM MEMORY:




```

---

## 📌 TASK 4: Terraform AWS (S3 Bucket & VPC)

### 💡 Complete Model Answer (Memorize This)
```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "ap-south-1"  # Mumbai
}

# ------------------------------------------------------------------------------
# PART 1: PRODUCTION S3 BUCKET (Modern AWS Provider v4/v5 format)
# ------------------------------------------------------------------------------
resource "aws_s3_bucket" "prod_bucket" {
  bucket = "Enterprise AWS-prod-data-storage-2026"

  tags = {
    Environment = "Production"
    ManagedBy   = "Terraform"
  }
}

# 1. Enable Versioning (Protects against accidental deletes/overwrites)
resource "aws_s3_bucket_versioning" "prod_ver" {
  bucket = aws_s3_bucket.prod_bucket.id
  versioning_configuration {
    status = "Enabled"
  }
}

# 2. Server-Side Encryption (KMS / AES256)
resource "aws_s3_bucket_server_side_encryption_configuration" "prod_enc" {
  bucket = aws_s3_bucket.prod_bucket.id

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}

# 3. Block Public Access (Enterprise AWS Security Baseline)
resource "aws_s3_bucket_public_access_block" "prod_block" {
  bucket = aws_s3_bucket.prod_bucket.id

  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}

# ------------------------------------------------------------------------------
# PART 2: CORE VPC & NETWORKING
# ------------------------------------------------------------------------------
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = { Name = "main-vpc" }
}

resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id
  tags   = { Name = "main-igw" }
}

resource "aws_subnet" "public_1" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "ap-south-1a"
  map_public_ip_on_launch = true

  tags = { Name = "public-subnet-1" }
}

resource "aws_route_table" "public_rt" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }

  tags = { Name = "public-rt" }
}

resource "aws_route_table_association" "public_assoc" {
  subnet_id      = aws_subnet.public_1.id
  route_table_id = aws_route_table.public_rt.id
}
```

### 🧠 Why Each Line Exists:
1. **Separated S3 Resources**: In modern Terraform (`hashicorp/aws >= 4.0`), AWS deprecated declaring versioning and encryption inside the `aws_s3_bucket` block. Using independent resources (`aws_s3_bucket_versioning`, `aws_s3_bucket_server_side_encryption_configuration`, `aws_s3_bucket_public_access_block`) proves you write modern, up-to-date IaC.
2. **`aws_s3_bucket_public_access_block`**: A premier partner requirement. All 4 flags must be `true` to guarantee no accidental public data leaks.
3. **Route Table `0.0.0.0/0` -> `igw.id`**: Without this entry pointing to the Internet Gateway, subnets cannot route outbound Internet traffic even if `map_public_ip_on_launch` is true.

```hcl
# 👉 TYPE YOUR TERRAFORM CODE BELOW THIS LINE FROM MEMORY:




```

---

## 📌 TASK 5: Declarative Jenkinsfile (CI/CD Pipeline)

### 💡 Complete Model Answer (Memorize This)
```groovy
pipeline {
    agent any

    environment {
        AWS_REGION     = 'ap-south-1'
        ECR_REGISTRY   = '123456789012.dkr.ecr.ap-south-1.amazonaws.com'
        IMAGE_NAME     = 'auth-service'
        IMAGE_TAG      = "${BUILD_NUMBER}"
        KUBECONFIG_ID  = 'k8s-cluster-credentials'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/company/auth-service.git'
            }
        }

        stage('Code Quality & Test') {
            steps {
                sh 'npm ci'
                sh 'npm test'
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                script {
                    sh "docker build -t ${ECR_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG} ."
                    sh "aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_REGISTRY}"
                    sh "docker push ${ECR_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig([credentialsId: "${KUBECONFIG_ID}"]) {
                    sh """
                        kubectl set image deployment/auth-service-deploy auth-container=${ECR_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG} -n production
                        kubectl rollout status deployment/auth-service-deploy -n production --timeout=120s
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded! Deployed image tag: ${IMAGE_TAG}"
        }
        failure {
            echo "Pipeline failed! Alerting DevOps team on Slack."
        }
    }
}
```

### 🧠 Why Each Line Exists:
1. **Declarative Syntax Structure**: Must follow `pipeline { agent ... environment { ... } stages { stage('...') { steps { ... } } } post { ... } }`.
2. **`aws ecr get-login-password | docker login ...`**: ECR authentication tokens expire every 12 hours. Piping the auth token securely to Docker stdin ensures clean, non-interactive login without saving passwords to disk.
3. **`kubectl rollout status ... --timeout=120s`**: Crucial production step! `kubectl set image` returns immediately (async). `kubectl rollout status` waits and validates that the new pods actually become healthy. If they crash-loop, the pipeline **fails immediately**, preventing silent broken deployments.
4. **`post { failure { ... } }`**: Used in production to trigger webhooks (Slack, PagerDuty, or email notifications) when a build breaks.

```groovy
// 👉 TYPE YOUR JENKINSFILE BELOW THIS LINE FROM MEMORY:




```
