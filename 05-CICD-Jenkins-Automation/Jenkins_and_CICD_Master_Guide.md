# 🚀 CI/CD Automation: Jenkins & Ansible Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers CI/CD Pipeline Automation, Declarative Jenkinsfile Engineering, Distributed Controller-Agent Architecture, GitHub Webhooks, Credentials Security, Ansible Agentless Configuration Management, Playbooks, Jinja2 Templating, Roles, and Ansible Vault.

---

## 📑 Table of Contents
- [1. Jenkins Core Architecture & Controller-Agent Model](#1-jenkins-core-architecture--controller-agent-model)
- [2. Jenkins Job Types & Declarative vs Scripted Pipelines](#2-jenkins-job-types--declarative-vs-scripted-pipelines)
- [3. Complete Production Declarative `Jenkinsfile`](#3-complete-production-declarative-jenkinsfile)
- [4. CI/CD Pipeline Stages & Webhook Triggers](#4-cicd-pipeline-stages--webhook-triggers)
- [5. Credentials Management & Secret Masking](#5-credentials-management--secret-masking)
- [6. Jenkins Shared Libraries (Enterprise Code Reuse)](#6-jenkins-shared-libraries-enterprise-code-reuse)
- [7. Ansible Architecture & Agentless Engine](#7-ansible-architecture--agentless-engine)
- [8. Ansible Inventory Management (INI & YAML)](#8-ansible-inventory-management-ini--yaml)
- [9. Ad-Hoc Commands & Core Modules Reference](#9-ad-hoc-commands--core-modules-reference)
- [10. Playbooks, Handlers, Loops, & Conditionals](#10-playbooks-handlers-loops--conditionals)
- [11. Jinja2 Templating & Dynamic Configurations](#11-jinja2-templating--dynamic-configurations)
- [12. Reusable Ansible Roles](#12-reusable-ansible-roles)
- [13. Ansible Vault: Production Secret Encryption](#13-ansible-vault-production-secret-encryption)
- [14. Senior DevOps Interview Q&A](#14-senior-devops-interview-qa)

---

## 1. Jenkins Core Architecture & Controller-Agent Model

### System Architecture
```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       JENKINS CONTROLLER (Master)                           │
│                                                                             │
│   • Web Dashboard & HTTP GUI                • Stores Job Configurations     │
│   • Monitors SCM & GitHub Webhooks          • Dispatches Builds to Agents   │
│   • Stores Build Logs & Test Reports        • Manages Plugins & Security    │
└───────────────────────┬─────────────────────────────┬───────────────────────┘
                        │ SSH / JNLP (Inbound TCP)    │ Dynamic Pod Provisioning
                        ▼                             ▼
┌───────────────────────────────────────┐ ┌───────────────────────────────────┐
│           Static Worker Agent         │ │     Dynamic Kubernetes Pod Agent  │
│         (Dedicated Linux EC2)         │ │     (Spun up on-demand, torn down)│
│                                       │ │                                   │
│   • Builds Docker Images              │ │   • Container 1: maven / node     │
│   • Runs Unit & Integration Tests     │ │   • Container 2: docker-cli       │
│   • Executes Security Scanners        │ │   • Container 3: kubectl / helm   │
└───────────────────────────────────────┘ └───────────────────────────────────┘
```

### Core Architecture Rules
* **Never Run Builds on Controller**: The controller handles scheduling, webhooks, and UI. Heavy builds on the controller exhaust CPU/memory and crash Jenkins.
* **Distributed Agent Types**:
  * **Static SSH Agents**: Dedicated EC2 instances with Java agent running.
  * **Dynamic Kubernetes Cloud Agents**: Controller spins up an isolated pod for each pipeline stage and immediately tears it down after completion (100% ephemeral).

---

## 2. Jenkins Job Types & Declarative vs Scripted Pipelines

### Comparison Matrix

| Feature | Declarative Pipeline (`pipeline { ... }`) | Scripted Pipeline (`node { ... }`) |
| :--- | :--- | :--- |
| **Syntax** | Structured, opinionated, easy to read | Groovy code, complex, imperatively programmed |
| **Error Handling** | Native `post { always, success, failure }` | Requires standard Groovy `try-catch-finally` |
| **Restart from Stage** | Native built-in support | Not supported out-of-the-box |
| **Extensibility** | Supports embedded `script { ... }` blocks | Unlimited Groovy language flexibility |
| **Industry Adoption**| **Standard for 95% of enterprise pipelines** | Legacy or highly dynamic bespoke pipelines |

---

## 3. Complete Production Declarative `Jenkinsfile`

```groovy
pipeline {
    agent {
        label 'docker-agent'
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    environment {
        DOCKER_REGISTRY  = 'devops-org'
        APP_IMAGE_NAME   = 'taskflow-backend'
        IMAGE_TAG        = "${BUILD_NUMBER}-${GIT_COMMIT[0..7]}"
        SONAR_HOST_URL   = 'https://sonarqube.internal'
    }

    stages {
        stage('Checkout & Lint') {
            steps {
                echo 'Checking out source code...'
                checkout scm
                sh 'npm run lint'
            }
        }

        stage('Unit Tests & Coverage') {
            steps {
                echo 'Executing automated test suites...'
                sh 'npm test -- --coverage'
            }
        }

        stage('SonarQube Static Analysis') {
            steps {
                withSonarQubeEnv('SonarQube-Server') {
                    sh 'sonar-scanner -Dsonar.projectKey=taskflow-api'
                }
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', 
                                                  usernameVariable: 'DOCKER_USER', 
                                                  passwordVariable: 'DOCKER_PASS')]) {
                    sh """echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin && docker build -t ${DOCKER_REGISTRY}/${APP_IMAGE_NAME}:${IMAGE_TAG} . && docker push ${DOCKER_REGISTRY}/${APP_IMAGE_NAME}:${IMAGE_TAG}"""
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig([credentialsId: 'k8s-cluster-credentials']) {
                    sh """
                        kubectl set image deployment/api-deployment                           api=${DOCKER_REGISTRY}/${APP_IMAGE_NAME}:${IMAGE_TAG}                           -n production
                        kubectl rollout status deployment/api-deployment -n production --timeout=300s
                    """
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo "Pipeline succeeded! Deployed tag: ${IMAGE_TAG}"
        }
        failure {
            echo "Pipeline failed on build: ${BUILD_NUMBER}. Triggering alerts."
        }
    }
}
```

---

## 4. CI/CD Pipeline Stages & Webhook Triggers

### 6 Standard Continuous Delivery Stages
* **1. Checkout**: Clones Git branch and validates commit checksum.
* **2. Lint & Static Analysis**: Runs Linters and SonarQube to detect code smells, vulnerabilities, and coverage gates.
* **3. Unit & Integration Testing**: Executes test harness; fails pipeline if coverage drops below threshold.
* **4. Artifact Packaging**: Compiles code and builds multi-stage Docker image with unique Git SHA tag.
* **5. Image Security Scan**: Runs Trivy or Aqua Security scan on container filesystem.
* **6. CD Deployment**: Deploys updated image tag to Kubernetes (via `kubectl` or ArgoCD GitOps).

### Trigger Mechanisms
* **GitHub Webhooks (Standard)**: Instant trigger via HTTP POST payload when developer pushes code or opens PR.
* **Poll SCM**: Periodic polling (e.g., `H/5 * * * *`); legacy and inefficient compared to Webhooks.
* **Cron Schedules**: Nightly automated builds (e.g., `H 0 * * *`).
* **Upstream Triggers**: Fires downstream pipeline when an upstream service build completes successfully.

---

## 5. Credentials Management & Secret Masking

### Security Best Practices
* **Never Plaintext in Code**: Never commit passwords, tokens, or private keys to `Jenkinsfile` or Git.
* **Jenkins Credentials Store**: Stores secrets encrypted on disk using AES-256 keys managed by Jenkins master.
* **Console Masking**: Jenkins automatically replaces credential values with `****` in console build logs.

### Accessing Credentials in Pipelines
```groovy
// 1. Username and Password
withCredentials([usernamePassword(credentialsId: 'my-cred-id', 
                                  usernameVariable: 'USER', 
                                  passwordVariable: 'PASS')]) {
    sh 'echo "Logging in as $USER"'
}

// 2. Secret Text (API Token)
withCredentials([string(credentialsId: 'slack-webhook-token', variable: 'SLACK_TOKEN')]) {
    sh 'curl -X POST -H "Authorization: Bearer $SLACK_TOKEN" ...'
}

// 3. Secret File (Kubeconfig or SSH Key)
withCredentials([file(credentialsId: 'prod-kubeconfig', variable: 'KUBECONFIG')]) {
    sh 'kubectl get nodes'
}
```

---

## 6. Jenkins Shared Libraries (Enterprise Code Reuse)

### Purpose
* Centralize standard pipeline logic (notifications, docker build-and-push, sonarqube gates) into a single Git repository shared across hundreds of microservices.

### Library Directory Structure
```text
jenkins-shared-library/
├── vars/
│   ├── buildAndPushDocker.groovy  # Custom pipeline step
│   └── notifySlack.groovy         # Custom alert step
└── src/
    └── org/company/utils/         # Groovy helper classes
```

### Invoking Shared Library in `Jenkinsfile`
```groovy
@Library('enterprise-shared-library@v2.0.0') _

pipeline {
    agent any
    stages {
        stage('Build & Push') {
            steps {
                buildAndPushDocker(imageName: 'user-service', registry: 'devops-org')
            }
        }
    }
    post {
        always {
            notifySlack()
        }
    }
}
```

---

## 7. Ansible Architecture & Agentless Engine

### Core Architecture
```text
┌─────────────────────────────────────────────────────────────┐
│                      Control Node                           │
│        (Ansible Installed: Python + SSH Client)             │
│                                                             │
│   ┌──────────────────┐  ┌──────────────────┐  ┌──────────┐  │
│   │    Inventory     │  │    Playbooks     │  │  Vault   │  │
│   │ (hosts.ini/yaml) │  │  (YAML Tasks)    │  │ (Secrets)│  │
│   └──────────────────┘  └──────────────────┘  └──────────┘  │
└──────────────────────────────┬──────────────────────────────┘
                               │ SSH (Linux) / WinRM (Windows)
                               │ (Zero client agent required!)
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                     Managed Target Nodes                    │
│                                                             │
│   ┌──────────────────────┐      ┌──────────────────────┐    │
│   │   Web Server (EC2)   │      │    DB Server (EC2)   │    │
│   │   • Python installed │      │   • Python installed │    │
│   │   • SSH authorized   │      │   • SSH authorized   │    │
│   └──────────────────────┘      └──────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

### Key Architectural Pillars
* **Agentless**: No background agent daemon (unlike Puppet or Chef); connects directly over standard SSH.
* **Idempotence**: Running a playbook 10 times produces the exact same outcome as running it once; only mutates state if changes are required (`ok` vs `changed`).
* **Declarative Tasks**: Uses human-readable YAML to define target state.

---

## 8. Ansible Inventory Management (INI & YAML)

### Inventory in INI Format (`inventory.ini`)
```ini
[webservers]
web1.internal ansible_host=10.0.1.10
web2.internal ansible_host=10.0.1.11

[databases]
db1.internal ansible_host=10.0.2.20

[production:children]
webservers
databases

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/devops-key.pem
ansible_python_interpreter=/usr/bin/python3
```

---

## 9. Ad-Hoc Commands & Core Modules Reference

### Ad-Hoc CLI Syntax
```bash
# Ping test connectivity to all inventory servers
ansible all -i inventory.ini -m ping

# Check memory utilization across webservers
ansible webservers -i inventory.ini -m command -a "free -m"

# Install nginx with root privileges
ansible webservers -i inventory.ini -m apt -a "name=nginx state=latest update_cache=yes" --become

# Restart service across all targets
ansible webservers -i inventory.ini -m service -a "name=nginx state=restarted" --become
```

### Core Ansible Modules

| Module | Purpose | Example Task Action |
| :--- | :--- | :--- |
| `ansible.builtin.apt` / `yum` | OS Package Management | `name: docker-ce state: present` |
| `ansible.builtin.service` / `systemd` | Service lifecycle control | `name: nginx state: started enabled: yes` |
| `ansible.builtin.copy` | Copies static file to target | `src: app.conf dest: /etc/app.conf` |
| `ansible.builtin.template` | Renders dynamic Jinja2 template | `src: nginx.conf.j2 dest: /etc/nginx/nginx.conf` |
| `ansible.builtin.user` | Manages Linux user accounts | `name: devops groups: sudo state: present` |
| `ansible.builtin.git` | Clones or updates Git repo | `repo: 'https://github.com/repo' dest: /app` |
| `community.docker.docker_container` | Manages Docker containers | `name: web image: nginx:alpine state: started` |

---

## 10. Playbooks, Handlers, Loops, & Conditionals

### Complete Full-Stack Web App Playbook (`deploy.yaml`)
```yaml
---
- name: Deploy Production Web Tier
  hosts: webservers
  become: true

  vars:
    http_port: 80
    app_directory: /var/www/html
    required_packages:
      - nginx
      - curl
      - git

  tasks:
    - name: Install required OS packages
      ansible.builtin.apt:
        name: "{{ item }}"
        state: present
        update_cache: yes
      loop: "{{ required_packages }}"

    - name: Render dynamic Nginx configuration from template
      ansible.builtin.template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/sites-available/default
      notify: Reload Nginx Service

    - name: Ensure Nginx is running and enabled on boot
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: yes

    - name: Create application directory
      ansible.builtin.file:
        path: "{{ app_directory }}"
        state: directory
        owner: www-data
        group: www-data
        mode: '0755'

  handlers:
    - name: Reload Nginx Service
      ansible.builtin.service:
        name: nginx
        state: reloaded
```

### Handlers Concept
* **Lazy Notification**: Handlers trigger **only when a notifying task actually makes a change** (`changed=true`).
* Handlers execute once at the very end of the play, preventing redundant service restarts.

---

## 11. Jinja2 Templating & Dynamic Configurations

### Template File (`templates/nginx.conf.j2`)
```nginx
server {
    listen {{ http_port }};
    server_name {{ server_domain | default('localhost') }};

    root {{ app_directory }};
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # Dynamic backend upstream proxy
    location /api/ {
        proxy_pass http://{{ backend_host }}:{{ backend_port }}/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---

## 12. Reusable Ansible Roles

### Standard Role Directory Structure
```text
roles/
└── nginx/
    ├── tasks/
    │   └── main.yaml       # Core sequence of tasks
    ├── handlers/
    │   └── main.yaml       # Notified restart/reload handlers
    ├── templates/
    │   └── nginx.conf.j2   # Jinja2 template files
    ├── vars/
    │   └── main.yaml       # High-priority role variables
    ├── defaults/
    │   └── main.yaml       # Overridable default variables
    └── meta/
        └── main.yaml       # Role dependencies and metadata
```

### Using Roles in a Playbook
```yaml
---
- name: Configure Production Web Cluster
  hosts: webservers
  become: true
  roles:
    - role: common_security
    - role: docker
    - role: nginx
```

---

## 13. Ansible Vault: Production Secret Encryption

### Vault CLI Commands
```bash
# Encrypt an existing sensitive variables file
ansible-vault encrypt vars/secrets.yaml

# Edit an encrypted file in-place using default editor
ansible-vault edit vars/secrets.yaml

# View encrypted contents in terminal
ansible-vault view vars/secrets.yaml

# Run playbook with password prompt
ansible-playbook -i inventory.ini deploy.yaml --ask-vault-pass

# Run playbook in CI/CD using secure password file
ansible-playbook -i inventory.ini deploy.yaml --vault-password-file ~/.vault_pass
```

---

## 14. Senior DevOps Interview Q&A

### Q1: What makes Ansible idempotent, and why does it matter?
* An idempotent task evaluates the target system first; if the system is already in the desired state, it takes **no action** (`ok: 1, changed: 0`).
* **Why it matters**: Allows engineers to safely execute playbooks repeatedly against production without restarting active services, creating duplicate users, or modifying intact configurations.

### Q2: What is the difference between Jenkins Multibranch Pipeline and standard Pipeline?
* **Standard Pipeline**: Points to a single fixed Git branch (e.g., `main`).
* **Multibranch Pipeline**: Automatically scans the entire Git repository, discovers any branch or Pull Request containing a `Jenkinsfile`, and automatically provisions dynamic build jobs per branch.

### Q3: How do you prevent sensitive secrets from leaking into Jenkins console output?
* Store secrets strictly in the Jenkins Credentials Store.
* Bind credentials via `withCredentials([usernamePassword(...)])` or `environment { SECRET = credentials('id') }`.
* Jenkins replaces matching credential strings with `****` in console output.
* **Caveat**: Avoid echoing commands with `set -x` in shell blocks or passing secrets via URL query parameters.
