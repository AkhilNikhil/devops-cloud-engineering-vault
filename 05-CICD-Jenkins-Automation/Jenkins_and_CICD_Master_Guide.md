# 🚀 CI/CD Automation: Jenkins & Ansible Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers CI/CD Pipeline Automation, Controller-Agent Architecture, The 5 Jenkins Build Triggers, Cron Scheduling & Weather Reports, The Production `/tmp` Low Memory Out-of-Space Crisis Resolution, Maven Lifecycle & Nexus Publishing, Declarative Jenkinsfile Engineering, Role-Based Access Control, Ansible Agentless Configuration Management, Playbooks, Jinja2 Templating, and Ansible Vault.

---

## 📑 Table of Contents
- [1. Jenkins Origins & Controller-Agent Architecture](#1-jenkins-origins--controller-agent-architecture)
- [2. The 5 Jenkins Build Trigger Types](#2-the-5-jenkins-build-trigger-types)
- [3. Jenkins Cron Scheduling & Weather Report Indicators](#3-jenkins-cron-scheduling--weather-report-indicators)
- [4. Production Crisis Resolution: The Jenkins `/tmp` Low Memory Issue](#4-production-crisis-resolution-the-jenkins-tmp-low-memory-issue)
- [5. Maven Lifecycle, Artifact Formats, & Nexus Publishing](#5-maven-lifecycle-artifact-formats--nexus-publishing)
- [6. Jenkins Security: Role-Based Authorization Strategy](#6-jenkins-security-role-based-authorization-strategy)
- [7. Declarative vs Scripted Pipelines](#7-declarative-vs-scripted-pipelines)
- [8. Complete Production Declarative `Jenkinsfile` Blueprint](#8-complete-production-declarative-jenkinsfile-blueprint)
- [9. Continuous Delivery vs Continuous Deployment](#9-continuous-delivery-vs-continuous-deployment)
- [10. Ansible Architecture & Agentless Operations](#10-ansible-architecture--agentless-operations)
- [11. Ansible Inventory Management & Ad-Hoc Commands](#11-ansible-inventory-management--ad-hoc-commands)
- [12. Ansible Playbooks, Handlers, & Jinja2 Templating](#12-ansible-playbooks-handlers--jinja2-templating)
- [13. Ansible Vault Secret Encryption](#13-ansible-vault-secret-encryption)
- [14. Senior DevOps Interview Q&A](#14-senior-devops-interview-qa)

---

## 1. Jenkins Origins & Controller-Agent Architecture

### Origins & Evolution
* **Hudson (2004)**: Created by Kohsuke Kawaguchi at Sun Microsystems as an open-source Java continuous integration server.
* **The Jenkins Fork (2011)**: Following Oracle's acquisition of Sun Microsystems, a trademark dispute led the community and Kohsuke to fork Hudson into **Jenkins**, which became the dominant open-source CI/CD platform globally.

### System Architecture: Controller & Distributed Agents
```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       JENKINS CONTROLLER (Master Node)                      │
│                                                                             │
│   • Web Dashboard UI & API Endpoints         • Manages Job Configurations   │
│   • Receives GitHub Webhook Payloads         • Dispatches Builds to Agents  │
│   • Stores Build History & Artifact Logs     • Manages Plugins & Security   │
└───────────────────────┬─────────────────────────────┬───────────────────────┘
                        │ SSH / JNLP (Port 50000)     │ Kubernetes Cloud Plugin
                        ▼                             ▼
┌───────────────────────────────────────┐ ┌───────────────────────────────────┐
│         Static EC2 Linux Agent        │ │    Dynamic Ephemeral K8s Pod Agent│
│                                       │ │                                   │
│   • Dedicated VM with Java Agent      │ │   • Container 1: maven / node     │
│   • Executes Heavy Builds & Tests     │ │   • Container 2: docker-cli       │
│   • Builds and Pushes Docker Images   │ │   • Container 3: kubectl / helm   │
│   • Cleans Workspace Post-Build       │ │   • Destroyed immediately on exit │
└───────────────────────────────────────┘ └───────────────────────────────────┘
```

### Golden Operational Rules
* **Never Run Builds on Controller**:
  * The controller coordinates scheduling, webhooks, and UI.
  * Running compilers and Docker builds on the controller exhausts memory/CPU, freezing the UI and dropping cluster webhooks.
* **Controller-Agent Connection Types**:
  * **SSH (Outbound from Controller)**: Controller connects directly to agent via private SSH key.
  * **Inbound JNLP / TCP (Port 50000)**: Agent initiates connection back to controller (ideal for agents behind firewalls or private subnets).

---

## 2. The 5 Jenkins Build Trigger Types

Understanding how and when Jenkins triggers builds is a critical system administration topic.

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       THE 5 JENKINS BUILD TRIGGERS                          │
├─────────────────────────────────────────────────────────────────────────────┤
│ 1. GitHub Hook Trigger for GITScm  │ Instant event-driven push via Webhooks │
│ 2. Poll SCM                        │ Scheduled check for Git commits (diff) │
│ 3. Build Periodically              │ Scheduled cron build unconditionally   │
│ 4. Build After Other Projects      │ Upstream / Downstream pipeline chain   │
│ 5. Trigger Builds Remotely         │ HTTP API call via authentication token │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Detailed Breakdown of Each Trigger

#### 1. GitHub Hook Trigger for GITScm Polling (Webhooks)
* **Mechanism**: Event-driven. When a developer pushes commits to GitHub or opens a pull request, GitHub instantly sends an HTTP `POST` JSON payload to Jenkins.
* **Payload URL**: `http://<jenkins-url>:8080/github-webhook/`.
* **Advantage**: Zero lag; instant build execution with zero polling overhead.

#### 2. Poll SCM
* **Mechanism**: Scheduled polling. Jenkins wakes up on a specified cron schedule, connects to the Git repository, and checks if the latest commit hash differs from the previous build.
* **Behavior**: If new commits exist $	o$ **triggers build**. If no commits exist $	o$ **does nothing**.
* **Use Case**: On-premise repositories behind strict corporate firewalls that cannot receive inbound webhooks from external Git providers.

#### 3. Build Periodically
* **Mechanism**: Unconditional time-based execution. Jenkins triggers a build strictly based on a cron schedule, **regardless of whether new commits were pushed or not**.
* **Use Case**: Nightly integration builds, end-of-day security vulnerability scans, weekly performance regression test suites.

#### 4. Build After Other Projects Are Built (Upstream / Downstream)
* **Mechanism**: Pipeline chaining. Executes this job automatically when one or more designated upstream jobs finish.
* **Trigger Conditions**: Can trigger only on `SUCCESS`, on `UNSTABLE`, or even on `FAILURE`.
* **Use Case**: Triggering integration testing after a core microservice artifact has successfully built and packaged.

#### 5. Trigger Builds Remotely (External API Token)
* **Mechanism**: External HTTP invocation. Allows external third-party systems or bash scripts to trigger a build via a parameterized REST API call.
* **URL Syntax**:
  ```bash
  curl -X POST "http://jenkins.example.com/job/app-deploy/build?token=SECRET_DEPLOY_TOKEN_2026"
  ```

---

## 3. Jenkins Cron Scheduling & Weather Report Indicators

### Cron Expression Syntax
Jenkins uses standard 5-field cron notation with special hash extension:

```text
 ┌───────────── Minute (0 - 59)
 │ ┌─────────── Hour (0 - 23)
 │ │ ┌───────── Day of Month (1 - 31)
 │ │ │ ┌─────── Month (1 - 12)
 │ │ │ │ ┌───── Day of Week (0 - 7, where 0 and 7 are Sunday)
 │ │ │ │ │
 * * * * *
```

* **Common Examples**:
  * `0 2 * * *` — Every day at 2:00 AM.
  * `H/15 * * * *` — Every 15 minutes.
  * `0 0 * * 1-5` — Midnight every weekday (Monday through Friday).
* **The `H` (Hash) Symbol in Jenkins**:
  * If 50 jobs are scheduled at `0 0 * * *`, they all launch at midnight simultaneously, crashing the CPU.
  * Using `H 0 * * *` allows Jenkins to hash the job name and distribute start times between 00:00 and 00:59, flattening resource consumption.

### Jenkins Health Weather Report Indicators
Jenkins displays a weather icon next to each job representing **recent build health stability** (calculated over the last 5 builds):

| Icon | Health State | Success Rate | Meaning |
| :--- | :--- | :--- | :--- |
| ☀️ **Sunny** | Excellent | **100% Success** | Last 5 out of 5 builds succeeded |
| ⛅ **Cloud & Sun** | Good | **80% Success** | 4 out of 5 builds succeeded |
| ☁️ **Cloudy** | Fair / Degraded | **50% Success** | Half of recent builds are failing |
| 🌧️ **Rain** | Poor | **35% Success** | Most recent builds are failing |
| ⛈️ **Thunder / Storm** | Critical Failure | **0% Success** | All recent builds failed repeatedly |

---

## 4. Production Crisis Resolution: The Jenkins `/tmp` Low Memory Issue

A classic real-world incident experienced in enterprise build clusters running on Linux worker nodes.

### The Problem & Root Cause
* During heavy Maven Java compilation, Docker layer unpacking, or npm builds, extensive temporary files and extraction caches are written to `/tmp`.
* On many Linux distributions, `/tmp` is mounted by default as a virtual **`tmpfs` in-memory filesystem** with a small default allocation (e.g., 512MB or 1GB).
* When `/tmp` fills to 100%, builds crash catastrophically with errors:
  * `java.io.IOException: No space left on device`
  * `Fatal error: could not create JVM temporary directory`

### Step-by-Step Production Emergency Resolution

#### Step 1: Stop Services
```bash
# Gracefully stop Jenkins agent process
sudo systemctl stop jenkins-agent.service
```

#### Step 2: Unmount Existing Exhausted `/tmp`
```bash
sudo umount /tmp
```

#### Step 3: Configure Permanent Sized `/tmp` in `/etc/fstab`
```bash
# Edit the filesystem table
sudo nano /etc/fstab

# Add or update the tmpfs entry with explicit 3GB or larger allocation
tmpfs   /tmp    tmpfs   defaults,size=3G,mode=1777   0   0
```

#### Step 4: Remount & Validate
```bash
# Remount all filesystems defined in fstab
sudo mount -a

# Validate new 3GB capacity
df -h /tmp
```

#### Step 5: Restart Jenkins Agent
```bash
sudo systemctl start jenkins-agent.service
sudo systemctl status jenkins-agent.service
```

---

## 5. Maven Lifecycle, Artifact Formats, & Nexus Publishing

### Apache Maven Build Lifecycle
Maven is a build automation and dependency management tool for Java projects governed by a `pom.xml` configuration file.

```text
validate ──► compile ──► test ──► package ──► verify ──► install ──► deploy
```
1. **`validate`**: Validates project structure and verifies all required `pom.xml` details are available.
2. **`compile`**: Compiles source code (`.java` files) into bytecode (`.class` files) under `target/classes`.
3. **`test`**: Runs unit tests (e.g., JUnit) without packaging.
4. **`package`**: Packages compiled code into distributable binaries (`target/*.jar` or `target/*.war`).
5. **`verify`**: Runs integration test checks against the packaged artifact.
6. **`install`**: Installs package into local machine repository (`~/.m2/repository`).
7. **`deploy`**: Copies final package to remote enterprise artifact repository (**Nexus OSS** or **JFrog Artifactory**).

### Artifact Formats Comparison
* **JAR (Java Archive)**: Contains compiled Java libraries, classes, and resources. Executable standalone via `java -jar app.jar` (e.g., Spring Boot).
* **WAR (Web Application Archive)**: Contains web components (servlets, JSP, XML, HTML, JS) designed to deploy inside a Servlet container (Apache Tomcat, WildFly).
* **EAR (Enterprise Archive)**: Bundles multiple JAR and WAR modules for Java EE enterprise servers.

### Nexus OSS (Artifact Repository Management)
* Centralized, version-controlled repository to store build artifacts, preventing rebuilds and enabling instant rollback to known binary versions.
* Maven deployment configuration inside `pom.xml`:
  ```xml
  <distributionManagement>
    <repository>
      <id>nexus-releases</id>
      <url>http://nexus.internal:8081/repository/maven-releases/</url>
    </repository>
  </distributionManagement>
  ```

---

## 6. Jenkins Security: Role-Based Authorization Strategy

By default, Jenkins grants all logged-in users administrative access. Production Jenkins enforces strict Role-Based Access Control via the **Role-based Authorization Strategy** plugin.

### The 3 Core Role Types
* **Global Roles**:
  * Cross-system permissions: `Admin`, `Read-Only`, `Job-Creator`.
  * Controls access to Jenkins system settings, plugin management, and credential viewing.
* **Project Roles (Item Roles)**:
  * Pattern-matched permissions using Regex (e.g., `payment-.*` or `mobile-.*`).
  * Restricts developers to viewing, configuring, and building only their specific microservice jobs.
* **Agent / Node Roles**:
  * Controls which teams can configure or execute builds on specific worker nodes (e.g., restricting GPU build agents to AI engineers).

---

## 7. Declarative vs Scripted Pipelines

```text
┌───────────────────────────────┬─────────────────────────────────────────────┐
│ Declarative Pipeline          │ Scripted Pipeline                           │
├───────────────────────────────┼─────────────────────────────────────────────┤
│ Modern standard (Blue Ocean)  │ Legacy traditional Groovy DSL               │
│ Enclosed in pipeline { ... }  │ Enclosed in node { ... }                    │
│ Strict, predictable syntax    │ Arbitrary procedural Groovy logic           │
│ Pre-execution syntax checking │ Errors caught only during runtime execution │
│ Restartable from failed stage │ Cannot easily restart stages                │
└───────────────────────────────┴─────────────────────────────────────────────┘
```

---

## 8. Complete Production Declarative `Jenkinsfile` Blueprint

```groovy
pipeline {
    agent {
        label 'linux-docker-agent'
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
    }

    environment {
        REGISTRY = 'registry.hub.docker.com'
        IMAGE_NAME = 'akhil/taskflow-api'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
        DOCKER_CREDS = credentials('dockerhub-credentials')
        SONAR_CREDS = credentials('sonarqube-token')
    }

    stages {
        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

        stage('Code Quality & SonarQube') {
            steps {
                withSonarQubeEnv('SonarQube-Server') {
                    sh 'mvn clean verify sonar:sonar'
                }
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Build & Package Artifact') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                    docker build -t ${IMAGE_NAME}:${IMAGE_TAG} -t ${IMAGE_NAME}:latest .
                """
            }
        }

        stage('Security Scan (Docker Scout)') {
            steps {
                sh "docker scout cves ${IMAGE_NAME}:${IMAGE_TAG} --exit-code --only-severity critical"
            }
        }

        stage('Push Image to Registry') {
            steps {
                sh """
                    echo ${DOCKER_CREDS_PSW} | docker login -u ${DOCKER_CREDS_USR} --password-stdin
                    docker push ${IMAGE_NAME}:${IMAGE_TAG}
                    docker push ${IMAGE_NAME}:latest
                """
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh """
                    kubectl set image deployment/taskflow-backend                         api-server=${IMAGE_NAME}:${IMAGE_TAG} -n production
                    kubectl rollout status deployment/taskflow-backend -n production
                """
            }
        }
    }

    post {
        success {
            slackSend channel: '#devops-deployments', color: 'good',
                message: "Build SUCCESS: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] deployed successfully."
        }
        failure {
            slackSend channel: '#devops-deployments', color: 'danger',
                message: "Build FAILURE: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] failed."
        }
        always {
            cleanWs()
        }
    }
}
```

---

## 9. Continuous Delivery vs Continuous Deployment

```text
Code ──► Build ──► Test ──► Staging ──► [ MANUAL APPROVAL GATE ] ──► Production  = Continuous Delivery
Code ──► Build ──► Test ──► Staging ──────────────────────────────► Production  = Continuous Deployment
```

* **Continuous Delivery (CDel)**: Every commit automatically builds, tests, and stages. Releasing to actual production requires an explicit **manual human approval gate** (e.g., QA sign-off or Product Manager release).
* **Continuous Deployment (CDep)**: Zero human intervention. Every commit that passes the automated automated test suite and quality gates is automatically deployed straight to live production users.

---

## 10. Ansible Architecture & Agentless Operations

Ansible is an open-source IT automation engine for configuration management, application deployment, and infrastructure provisioning.

### Why Ansible is "Agentless"
* **No Agent Daemons**: Unlike Chef, Puppet, or SaltStack, Ansible does not require any background agent software installed on managed target nodes.
* **Protocol**: Communicates over standard **SSH (port 22)** on Linux nodes and **WinRM** on Windows.
* **Idempotency**: Running an Ansible playbook multiple times produces the exact same end state without applying redundant changes or corrupting configurations.

---

## 11. Ansible Inventory Management & Ad-Hoc Commands

### Inventory File (`hosts.ini`)
```ini
[webservers]
web1.production.internal ansible_host=10.0.1.50
web2.production.internal ansible_host=10.0.1.51

[databases]
db1.production.internal  ansible_host=10.0.2.100

[production:children]
webservers
databases

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/devops_key.pem
ansible_python_interpreter=/usr/bin/python3
```

### Essential Ad-Hoc Commands
* `ansible all -m ping -i hosts.ini` — Test SSH connectivity across all inventory hosts.
* `ansible webservers -m command -a "uptime" -i hosts.ini` — Run arbitrary shell command.
* `ansible webservers -m apt -a "name=nginx state=latest update_cache=yes" -b -i hosts.ini` — Upgrade package.

---

## 12. Ansible Playbooks, Handlers, & Jinja2 Templating

### Production Nginx Playbook Blueprint
```yaml
---
- name: Configure Production Web Servers
  hosts: webservers
  become: true
  vars:
    http_port: 80
    app_root: /var/www/taskflow

  tasks:
    - name: Install Nginx Web Server
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Deploy Dynamic Nginx Configuration from Template
      template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/sites-available/default
        mode: '0644'
      notify: Reload Nginx Service

    - name: Ensure Nginx is Running and Enabled
      systemd:
        name: nginx
        state: started
        enabled: yes

  handlers:
    - name: Reload Nginx Service
      systemd:
        name: nginx
        state: reloaded
```

---

## 13. Ansible Vault Secret Encryption

Ansible Vault protects sensitive tokens, database passwords, and private SSH keys from being exposed in Git repositories.

* **Encrypt a Secrets File**:
  ```bash
  ansible-vault encrypt vars/secrets.yml
  ```
* **View / Edit Encrypted File**:
  ```bash
  ansible-vault edit vars/secrets.yml
  ```
* **Execute Playbook with Vault Password**:
  ```bash
  ansible-playbook -i hosts.ini site.yml --ask-vault-pass
  ```

---

## 14. Senior DevOps Interview Q&A

### Q1: What is the difference between Poll SCM and GitHub Webhooks?
* **GitHub Webhook**: Event-driven push from GitHub to Jenkins immediately when code is pushed. Zero delay, zero wasted CPU overhead.
* **Poll SCM**: Scheduled cron job inside Jenkins that periodically connects to GitHub to check for changes. Can introduce latency (up to polling interval) and wastes CPU cycles if no changes exist.

### Q2: How did you diagnose and resolve Jenkins running out of space on worker nodes?
* Root cause was the `/tmp` directory mounted on a small virtual `tmpfs` partition in memory, which was exhausted by Maven builds unpacking jar dependencies.
* Resolved by stopping the Jenkins agent service, unmounting `/tmp`, adding `tmpfs /tmp tmpfs defaults,size=3G,mode=1777 0 0` in `/etc/fstab`, executing `mount -a`, and restarting the agent service.

### Q3: What is the significance of the `H` symbol in Jenkins cron triggers?
* The `H` symbol distributes job executions using a hash of the project name across the time window. This prevents all scheduled jobs from launching at the exact same minute and overloading system CPU and RAM.
