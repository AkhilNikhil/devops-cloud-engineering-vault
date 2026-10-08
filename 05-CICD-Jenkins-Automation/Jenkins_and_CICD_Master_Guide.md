# 🔄 CI/CD & Configuration Automation: Jenkins & Ansible Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Continuous Integration & Delivery, Jenkins Controller-Agent Architecture, Declarative Pipelines, SonarQube & Nexus Integration, and Ansible Agentless Configuration Management.

---

## 📑 Table of Contents
- [PART 1: JENKINS CI/CD AUTOMATION](#part-1-jenkins-cicd-automation)
  - [Why Jenkins & CI/CD Foundations](#why-jenkins)
  - [Jenkins Controller-Agent Distributed Architecture](#jenkins-architecture)
  - [Declarative Pipeline Syntax & Best Practices](#declarative-pipelines)
  - [Quality & Artifact Governance (SonarQube & Nexus)](#sonarqube--nexus)
  - [Complete Production Jenkinsfile Blueprint](#production-jenkinsfile)
- [PART 2: ANSIBLE CONFIGURATION MANAGEMENT](#part-2-ansible-configuration-management)
  - [Why Ansible? (Agentless Architecture over SSH)](#why-ansible)
  - [Ansible Inventory & Host Management](#ansible-inventory)
  - [Playbooks, Tasks, Modules & Idempotency](#ansible-playbooks)
  - [Ansible Roles & Reusability](#ansible-roles)
- [Production Troubleshooting & Interview Q&A](#troubleshooting--interview-qa)

---

# PART 1: JENKINS CI/CD AUTOMATION

SECTION 4: JENKINS




Q1. What is Jenkins and why does a DevOps engineer use it?
Answer:
Jenkins is an open-source automation server used to build CI/CD pipelines. It automatically triggers builds when
code is pushed, runs tests, builds artifacts, and deploys to environments — without manual intervention.
Integrations: Git, Docker, Kubernetes, Nexus, Artifactory, SonarQube, Slack
Why DevOps uses it:
Automates the entire release process
Catches bugs early via automated testing
Consistent, repeatable deployments
Saves time — no manual build/deploy steps
Q2. What are Jenkins Job Types?
Answer:
Job Type Description Use case
Freestyle Manual UI configuration, build steps defined in UI Simple, legacy jobs
Pipeline Jenkinsfile written in Groovy, Pipeline as Code Modern standard
Multibranch Pipeline Auto-creates pipelines for each Git branch Feature branch workflows
For interviews: Always talk about Pipeline jobs with Jenkinsfile — that's the industry standard.
Q3. What is a Jenkinsfile?
Answer:
A Jenkinsfile is a text file written in Groovy that defines your entire CI/CD pipeline as code. It lives in your Git
repo alongside your application code. This means your pipeline is version controlled.
Example Jenkinsfile:
pipeline {
    agent any




    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/devops-org/myapp.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Docker Build & Push') {
            steps {
                sh 'docker build -t myapp:1.0 .'
                sh 'docker push myrepo/myapp:1.0'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
Benefits: Version controlled, reviewable, consistent, reusable.




Q4. What are Common CI/CD Pipeline Stages?
Answer:
Stage What it does
Checkout Pull latest code from Git
Build Compile code, create JAR/WAR/binary
Test Run unit tests, integration tests
Code Quality SonarQube scan for code smells, bugs
Security Scan Check for vulnerabilities
Docker Build Build Docker image
Push to Registry Push image to ECR/ACR/Docker Hub
Deploy to Staging Deploy to test environment
Deploy to Production Deploy to live environment
Q5. What are Jenkins Triggers?
Answer:
Triggers tell Jenkins when to run a pipeline automatically.
Trigger How it works Best for
Webhook Git sends notification to Jenkins on code push. Instant. Production — fastest
Poll SCM Jenkins checks Git repo every X minutes for changes Legacy systems
Scheduled Runs on cron schedule (e.g., every night at 2am) Nightly builds
Manual Click "Build Now" in Jenkins UI On-demand
Upstream Job One pipeline triggers another Pipeline chaining
Example Webhook trigger in Jenkinsfile:




pipeline {
    agent any
    triggers {
        githubPush()   // triggers on every GitHub push
    }
    stages { ... }
}
Best practice: Always use Webhooks — instant response when code is pushed.
Q6. Declarative vs Scripted Pipeline
Answer:
Feature Declarative Scripted
Syntax Structured, fixed format Full Groovy programming
Readability Easy to read Complex
Flexibility Limited Very flexible
Standard Modern standard ✅ Legacy
Declarative Example:
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn build'
            }
        }
    }
}
Scripted Example:
node {
    stage('Build') {




 
        if (env.BRANCH_NAME == 'master') {
            sh 'mvn build'
        }
    }
}
For interviews: Always say Declarative is better — modern standard, easier to maintain.
Q7. How to Manage Secrets in Jenkins?
Answer:
Never hardcode secrets in Jenkinsfile. Use Jenkins Credentials Store.
Types of credentials:
Username/Password — Docker Hub, Git
SSH Key — server access
Secret Text — API tokens, keys
Certificate — SSL certs
Example using credentials in Jenkinsfile:
pipeline {
    agent any
    environment {
        DOCKER_CREDS = credentials('docker-hub-credentials')
    }
    stages {
        stage('Push Image') {
            steps {
                sh '''
                    echo $DOCKER_CREDS_PSW | docker login -u $DOCKER_CREDS_USR --passw
                    docker push myrepo/myapp:1.0
                '''
            }
        }
    }
}
Rule: Credentials are injected at runtime — never visible in logs or Git history.




Q8. What is Jenkins Master and Agent?
Answer:
Master (Controller) — manages jobs, schedules builds, stores configurations, serves the UI. Does NOT run
builds itself.
Agent (Worker) — executes the actual build jobs. Can have multiple agents with different setups.
Why use agents:
Master stays lightweight
Scale by adding more agents
Different agents for different jobs (Docker agent, Java agent, etc.)
Example in Jenkinsfile:
pipeline {
    agent { label 'docker' }   // run only on agent labelled 'docker'
    stages { ... }
}
// OR
pipeline {
    agent any    // run on any available agent
    stages { ... }
}
Q9. What is a Jenkins Shared Library?
Answer:
Reusable Groovy code shared across multiple pipelines. Write once, use everywhere.
Structure:
shared-library/
  vars/
    deploy.groovy    # reusable deploy function
    test.groovy      # reusable test function
Usage in Jenkinsfile:




@Library('my-shared-library') _
pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                script {
                    deploy('production')   // call shared function
                }
            }
        }
    }
}
Benefits: No code duplication, update in one place, consistent across all teams.
Q10. What is Blue Ocean in Jenkins?
Answer:
Blue Ocean is Jenkins's modern UI for visualizing pipelines. Traditional Jenkins UI is cluttered and hard to read.
Blue Ocean shows pipelines as a visual flowchart.
Features:
Visual pipeline view — each stage as a box
Green = success, Red = failed
See exactly which stage failed instantly
Inline logs per stage
Pull request integration
For interviews: Mention it as the modern Jenkins UI that improves pipeline visibility and troubleshooting.


---

# PART 2: ANSIBLE CONFIGURATION MANAGEMENT

SECTION 9: ANSIBLE — COMPLETE GUIDE
Configuration Management tool. Write once, apply to hundreds of servers.




1. What is Ansible?
Definition:
Ansible is an open-source automation tool for configuration management, application deployment, and task
automation. You write simple YAML files called Playbooks and Ansible executes them on remote servers.
Why Ansible?
Before Ansible: SSH into each server manually, run commands one by one. With 100 servers, it's a
nightmare.
With Ansible: Write a playbook once. Run it on all 100 servers simultaneously.
Key Features:
Agentless — no software to install on target servers. Uses SSH.
Idempotent — running the same playbook twice gives the same result. Won't break things.
Simple YAML — easy to read and write
Push-based — Ansible controller pushes commands to servers
Large community — thousands of pre-built modules
2. How Ansible Works
┌─────────────────────────────────────┐
│         Ansible Control Node        │
│  (your machine / Jenkins server)    │
│                                     │
│  Inventory file  ← list of servers  │
│  Playbook        ← what to do       │
│  ansible command ← execute          │
└──────────────┬──────────────────────┘
               │ SSH (no agent needed)
    ┌──────────┼──────────────────────┐
    ▼          ▼                      ▼
┌────────┐ ┌────────┐           ┌────────┐
│Server 1│ │Server 2│    ...    │Server N│
│(target)│ │(target)│           │(target)│
└────────┘ └────────┘           └────────┘
Ansible Push vs Chef/Puppet Pull:
Ansible Chef/Puppet




Architecture Push (control → nodes) Pull (nodes fetch config)
Agent No agent needed Agent required on each node
Language YAML Ruby DSL
Learning curve Easy Steeper
3. Ansible Key Components
Component Description
Control Node Machine where Ansible is installed and run from
Managed Nodes Target servers Ansible configures (no Ansible needed)
Inventory List of managed nodes (IP/hostname)
Playbook YAML file containing automation tasks
Play A set of tasks targeting a group of hosts
Task A single unit of work (install nginx, copy file)
Module Pre-built function for a task (apt, yum, copy, service)
Role Reusable, organized collection of tasks
Handler Task that runs only when notified (restart service)
Variable Dynamic values used in playbooks
Template Jinja2 files with variables for config files
Vault Encrypted storage for secrets
Galaxy Community repository for roles
4. Installation




# Install Ansible on Control Node (Ubuntu)
sudo apt update
sudo apt install ansible -y
# Verify
ansible --version
# Install on RHEL/CentOS
sudo yum install epel-release -y
sudo yum install ansible -y
# Install via pip
pip install ansible
# Key files
/etc/ansible/hosts          # default inventory file
/etc/ansible/ansible.cfg    # default configuration
5. Inventory — Define Your Servers
What is Inventory?
A file listing all the servers Ansible manages. Can be a simple text file or dynamic (from AWS, Azure).
Static Inventory (hosts file):
# /etc/ansible/hosts  OR  inventory.ini
# Simple list
192.168.1.10
192.168.1.11
server1.example.com
# Groups
[webservers]
web1.example.com
web2.example.com
192.168.1.20
[dbservers]
db1.example.com
db2.example.com
[appservers]




app1.example.com ansible_user=ubuntu ansible_port=22
# Group of groups
[production:children]
webservers
dbservers
# Variables for group
[webservers:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
http_port=80
YAML Inventory:
# inventory.yml
all:
  children:
    webservers:
      hosts:
        web1:
          ansible_host: 192.168.1.10
          ansible_user: ubuntu
        web2:
          ansible_host: 192.168.1.11
    dbservers:
      hosts:
        db1:
          ansible_host: 192.168.1.20
          ansible_user: ubuntu
Inventory Commands:
ansible-inventory --list                    # list all hosts
ansible-inventory --graph                   # tree view
ansible all --list-hosts                    # list hosts
ansible webservers --list-hosts            # list hosts in group
6. Ad-Hoc Commands
What are Ad-Hoc Commands?




Quick one-liner commands to run a task on servers without writing a playbook.
# Syntax
ansible <hosts/group> -m <module> -a "<arguments>"
# Test connectivity (ping all servers)
ansible all -m ping
ansible webservers -m ping
# Run shell command
ansible all -m shell -a "uptime"
ansible webservers -m shell -a "df -h"
ansible dbservers -m shell -a "free -h"
# Install package
ansible webservers -m apt -a "name=nginx state=present" --become
ansible webservers -m yum -a "name=nginx state=present" --become
# Copy file
ansible webservers -m copy -a "src=/local/file.txt dest=/remote/file.txt"
# Create directory
ansible all -m file -a "path=/opt/myapp state=directory mode=0755"
# Restart service
ansible webservers -m service -a "name=nginx state=restarted" --become
# Gather facts about servers
ansible all -m setup
ansible web1 -m setup -a "filter=ansible_os_family"
# Check free memory
ansible all -m setup -a "filter=ansible_memfree_mb"
# Options
-i inventory.ini    # specify inventory file
--become            # sudo (run as root)
-u ubuntu           # specify username
-k                  # ask for password
--private-key       # SSH key file
-v / -vv / -vvv    # verbose output
7. Playbooks — The Heart of Ansible




What is a Playbook?
A YAML file containing one or more plays. Each play targets a group of hosts and runs a series of tasks.
Basic Playbook Structure
---
- name: My First Playbook
  hosts: webservers          # target group from inventory
  become: yes                # sudo
  vars:
    http_port: 80
    app_name: myapp
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
        update_cache: yes
    - name: Start nginx service
      service:
        name: nginx
        state: started
        enabled: yes
    - name: Create web directory
      file:
        path: /var/www/{{ app_name }}
        state: directory
        mode: '0755'
    - name: Copy index.html
      copy:
        src: files/index.html
        dest: /var/www/{{ app_name }}/index.html
        mode: '0644'
Run Playbook:
ansible-playbook playbook.yml                          # run playbook
ansible-playbook playbook.yml -i inventory.ini        # custom inventory
ansible-playbook playbook.yml --check                 # dry run (no changes)
ansible-playbook playbook.yml --diff                  # show what changed
ansible-playbook playbook.yml -v                      # verbose
ansible-playbook playbook.yml --tags install          # run only tagged tasks




ansible-playbook playbook.yml --skip-tags restart    # skip tagged tasks
ansible-playbook playbook.yml --limit web1            # run only on web1
8. Common Ansible Modules
# ── PACKAGE MANAGEMENT ──
- name: Install package (Ubuntu/Debian)
  apt:
    name: nginx
    state: present     # present/absent/latest
    update_cache: yes
- name: Install package (RHEL/CentOS)
  yum:
    name: nginx
    state: present
- name: Install pip package
  pip:
    name: flask
    state: present
# ── FILE OPERATIONS ──
- name: Create directory
  file:
    path: /opt/myapp
    state: directory
    mode: '0755'
    owner: ubuntu
    group: ubuntu
- name: Create file
  file:
    path: /opt/myapp/app.py
    state: touch
- name: Delete file
  file:
    path: /tmp/oldfile.txt
    state: absent
- name: Copy file from control to managed
  copy:
    src: files/nginx.conf




    dest: /etc/nginx/nginx.conf
    mode: '0644'
    backup: yes          # backup existing file
- name: Copy inline content to file
  copy:
    content: "Hello World"
    dest: /var/www/html/index.html
- name: Download file from URL
  get_url:
    url: https://example.com/file.zip
    dest: /opt/file.zip
# ── SERVICE MANAGEMENT ──
- name: Start and enable service
  service:
    name: nginx
    state: started
    enabled: yes
- name: Restart service
  service:
    name: nginx
    state: restarted
- name: Stop service
  service:
    name: nginx
    state: stopped
# ── COMMAND EXECUTION ──
- name: Run shell command
  shell: echo "Hello" > /tmp/hello.txt
- name: Run command (safer, no shell features)
  command: ls -la /opt
- name: Run script
  script: scripts/setup.sh
# ── USER MANAGEMENT ──
- name: Create user
  user:
    name: deploy
    shell: /bin/bash
    home: /home/deploy
    create_home: yes
    groups: sudo




    append: yes
- name: Delete user
  user:
    name: olduser
    state: absent
    remove: yes          # removes home directory
# ── GIT ──
- name: Clone git repository
  git:
    repo: https://github.com/devops/myapp.git
    dest: /opt/myapp
    version: main
# ── TEMPLATE ──
- name: Deploy config from template
  template:
    src: templates/nginx.conf.j2
    dest: /etc/nginx/nginx.conf
    mode: '0644'
# ── DOCKER ──
- name: Pull Docker image
  docker_image:
    name: nginx
    tag: latest
    source: pull
- name: Run Docker container
  docker_container:
    name: myapp
    image: nginx:latest
    ports:
      - "80:80"
    state: started
# ── DEBUG ──
- name: Print variable
  debug:
    msg: "The value is {{ my_variable }}"
- name: Print all facts
  debug:
    var: ansible_facts




9. Variables in Ansible
# ── INLINE VARIABLES ──
- name: Deploy App
  hosts: webservers
  vars:
    app_name: myapp
    app_port: 3000
    app_version: "1.0"
  tasks:
    - name: Print app info
      debug:
        msg: "Deploying {{ app_name }} v{{ app_version }} on port {{ app_port }}"
# ── VARIABLE FILES ──
- name: Deploy App
  hosts: webservers
  vars_files:
    - vars/main.yml
    - vars/secrets.yml
# vars/main.yml
app_name: myapp
app_port: 3000
db_host: postgres-server
db_port: 5432
# vars/secrets.yml (use Ansible Vault to encrypt this)
db_password: supersecret
api_key: abc123xyz
Variable Precedence (highest to lowest):
1. Command line (-e "var=value")
2. Task vars
3. Block vars
4. Role and include vars
5. Play vars_files
6. Play vars
7. Host facts
8. Inventory host vars




9. Inventory group vars
10. Role defaults
10. Handlers — Run on Notification
What is a Handler?
A task that runs ONLY when notified by another task. Prevents unnecessary restarts.
- name: Configure Nginx
  hosts: webservers
  become: yes
  tasks:
    - name: Copy nginx config
      copy:
        src: files/nginx.conf
        dest: /etc/nginx/nginx.conf
      notify: Restart Nginx        # triggers handler only if file changed
    - name: Install nginx
      apt:
        name: nginx
        state: present
      notify:
        - Start Nginx
        - Enable Nginx
  handlers:
    - name: Restart Nginx
      service:
        name: nginx
        state: restarted
    - name: Start Nginx
      service:
        name: nginx
        state: started
    - name: Enable Nginx
      service:
        name: nginx
        enabled: yes




Key point: Handler runs ONCE even if notified multiple times. And runs at END of play.
11. Conditionals and Loops
tasks:
  # ── CONDITIONALS (when) ──
  - name: Install on Ubuntu only
    apt:
      name: nginx
      state: present
    when: ansible_os_family == "Debian"
  - name: Install on RHEL only
    yum:
      name: nginx
      state: present
    when: ansible_os_family == "RedHat"
  - name: Only run in production
    shell: deploy.sh
    when: environment == "production"
  - name: Multiple conditions
    apt:
      name: nginx
      state: present
    when:
      - ansible_os_family == "Debian"
      - ansible_distribution_major_version == "20"
  # ── LOOPS ──
  - name: Install multiple packages
    apt:
      name: "{{ item }}"
      state: present
    loop:
      - nginx
      - git
      - curl
      - vim
  - name: Create multiple users
    user:
      name: "{{ item.name }}"




      groups: "{{ item.group }}"
    loop:
      - { name: alice, group: sudo }
      - { name: bob, group: docker }
      - { name: charlie, group: dev }
  - name: Create multiple directories
    file:
      path: "{{ item }}"
      state: directory
    loop:
      - /opt/app
      - /opt/logs
      - /opt/config
12. Templates — Jinja2
What is a Template?
A file with placeholders (variables) that Ansible fills in. Used for config files that differ per environment.
{# templates/nginx.conf.j2 #}
server {
    listen {{ http_port }};
    server_name {{ server_name }};
    
    location / {
        proxy_pass http://{{ app_host }}:{{ app_port }};
    }
    
    access_log /var/log/nginx/{{ app_name }}_access.log;
}
{# Conditional in template #}
{% if enable_ssl %}
    listen 443 ssl;
    ssl_certificate /etc/ssl/{{ app_name }}.crt;
{% endif %}
{# Loop in template #}
upstream backend {
{% for server in backend_servers %}
    server {{ server }}:{{ app_port }};




{% endfor %}
}
# Use template in playbook
- name: Deploy nginx config
  template:
    src: templates/nginx.conf.j2
    dest: /etc/nginx/sites-available/{{ app_name }}.conf
  vars:
    http_port: 80
    server_name: myapp.example.com
    app_host: localhost
    app_port: 3000
  notify: Restart Nginx
13. Roles — Reusable Ansible Code
What is a Role?
A structured way to organize playbooks into reusable components. Like a module.
Role Directory Structure:
roles/
└── nginx/
    ├── tasks/
    │   └── main.yml       # main tasks
    ├── handlers/
    │   └── main.yml       # handlers
    ├── templates/
    │   └── nginx.conf.j2  # templates
    ├── files/
    │   └── index.html     # static files
    ├── vars/
    │   └── main.yml       # variables
    ├── defaults/
    │   └── main.yml       # default variables (lowest priority)
    └── meta/
        └── main.yml       # role metadata, dependencies
Create Role:




ansible-galaxy init nginx         # creates role structure
ansible-galaxy init docker
ansible-galaxy init deploy-app
Use Role in Playbook:
- name: Setup Web Server
  hosts: webservers
  become: yes
  roles:
    - nginx              # apply nginx role
    - docker             # apply docker role
    - { role: deploy-app, app_name: myapp }   # with variables
Install Community Roles:
ansible-galaxy install geerlingguy.nginx      # install from Galaxy
ansible-galaxy install -r requirements.yml    # install from file
ansible-galaxy list                           # list installed roles
14. Ansible Vault — Secrets Management
What is Vault?
Encrypts sensitive files (passwords, keys) so you can safely store them in Git.
# Create encrypted file
ansible-vault create secrets.yml
# Edit encrypted file
ansible-vault edit secrets.yml
# Encrypt existing file
ansible-vault encrypt vars/secrets.yml
# Decrypt file
ansible-vault decrypt vars/secrets.yml
# View encrypted file
ansible-vault view secrets.yml




# Change vault password
ansible-vault rekey secrets.yml
# Run playbook with vault
ansible-playbook playbook.yml --ask-vault-pass
ansible-playbook playbook.yml --vault-password-file ~/.vault_pass
15. Complete Playbook — Deploy Full Stack App
---
# deploy-app.yml — Deploy Node.js app with Nginx on Ubuntu
- name: Deploy Full Stack Application
  hosts: webservers
  become: yes
  vars_files:
    - vars/main.yml
    - vars/secrets.yml
  vars:
    app_name: myapp
    app_dir: /opt/{{ app_name }}
    app_port: 3000
    nginx_port: 80
    node_version: "18"
    git_repo: https://github.com/devops/myapp.git
  tasks:
    # ── SYSTEM SETUP ──
    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 3600
    - name: Install system dependencies
      apt:
        name:
          - curl
          - git
          - nginx
          - ufw
        state: present




    # ── NODE.JS ──
    - name: Add NodeSource repository
      shell: curl -fsSL https://deb.nodesource.com/setup_{{ node_version }}.x | bash -
    - name: Install Node.js
      apt:
        name: nodejs
        state: present
    # ── APPLICATION ──
    - name: Create app directory
      file:
        path: "{{ app_dir }}"
        state: directory
        owner: ubuntu
        mode: '0755'
    - name: Clone application code
      git:
        repo: "{{ git_repo }}"
        dest: "{{ app_dir }}"
        version: main
        force: yes
      become_user: ubuntu
    - name: Install npm dependencies
      npm:
        path: "{{ app_dir }}"
      become_user: ubuntu
    - name: Set environment variables
      copy:
        content: |
          NODE_ENV=production
          PORT={{ app_port }}
          DB_HOST={{ db_host }}
          DB_PASSWORD={{ db_password }}
        dest: "{{ app_dir }}/.env"
        mode: '0600'
    # ── NGINX ──
    - name: Deploy nginx config
      template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/sites-available/{{ app_name }}
      notify: Restart Nginx
    - name: Enable nginx site
      file:




        src: /etc/nginx/sites-available/{{ app_name }}
        dest: /etc/nginx/sites-enabled/{{ app_name }}
        state: link
      notify: Restart Nginx
    - name: Remove default nginx site
      file:
        path: /etc/nginx/sites-enabled/default
        state: absent
      notify: Restart Nginx
    # ── FIREWALL ──
    - name: Allow HTTP
      ufw:
        rule: allow
        port: "80"
        proto: tcp
    - name: Allow SSH
      ufw:
        rule: allow
        port: "22"
        proto: tcp
    - name: Enable UFW
      ufw:
        state: enabled
    # ── START APP ──
    - name: Install PM2 (process manager)
      npm:
        name: pm2
        global: yes
    - name: Start application with PM2
      shell: pm2 start app.js --name {{ app_name }} || pm2 restart {{ app_name }}
      args:
        chdir: "{{ app_dir }}"
      become_user: ubuntu
    - name: Save PM2 config
      shell: pm2 save
      become_user: ubuntu
  handlers:
    - name: Restart Nginx
      service:




        name: nginx
        state: restarted
16. Ansible for DevOps — Key Use Cases
1. Provision and configure EC2 instances:
- name: Configure EC2 instances
  hosts: aws_ec2
  tasks:
    - name: Install Docker
      apt:
        name: docker.io
        state: present
    - name: Start Docker
      service:
        name: docker
        state: started
        enabled: yes
2. Deploy Docker containers:
- name: Deploy App Container
  hosts: all
  tasks:
    - name: Pull latest image
      docker_image:
        name: devops/myapp:latest
        source: pull
    - name: Run container
      docker_container:
        name: myapp
        image: devops/myapp:latest
        ports: ["80:3000"]
        restart_policy: always
        state: started
3. Configure multiple servers at once:
# Apply to all 100 servers simultaneously




ansible-playbook configure-servers.yml -i production-inventory.ini
17. Ansible Commands Quick Reference
# ── AD-HOC ──
ansible all -m ping                               # test connectivity
ansible webservers -m shell -a "uptime"          # run command
ansible all -m setup                              # gather facts
ansible all -m apt -a "name=nginx state=present" --become
# ── PLAYBOOK ──
ansible-playbook playbook.yml                     # run playbook
ansible-playbook playbook.yml --check            # dry run
ansible-playbook playbook.yml --diff             # show changes
ansible-playbook playbook.yml -v                 # verbose
ansible-playbook playbook.yml --tags install     # run tagged tasks
ansible-playbook playbook.yml --limit web1       # target one host
ansible-playbook playbook.yml -e "env=prod"      # extra variables
# ── INVENTORY ──
ansible-inventory --list                          # list all hosts
ansible-inventory --graph                         # tree view
# ── GALAXY (ROLES) ──
ansible-galaxy init myrole                        # create role structure
ansible-galaxy install geerlingguy.nginx         # download role
ansible-galaxy list                               # list installed roles
# ── VAULT ──
ansible-vault create secrets.yml                 # create encrypted file
ansible-vault edit secrets.yml                   # edit encrypted file
ansible-vault encrypt vars.yml                   # encrypt existing file
ansible-playbook playbook.yml --ask-vault-pass  # run with vault password
# ── CONFIG ──
ansible --version                                 # show version
ansible-config list                               # show all config
ansible-config dump                               # show active config
18. Ansible Interview Q&A




Q: What is Ansible and how is it different from Chef/Puppet?
Ansible is agentless — no software needed on managed nodes. It uses SSH to push configurations. Chef and
Puppet use a pull model where agents on each node fetch config from a server.
Q: What is idempotency in Ansible?
Running the same playbook multiple times produces the same result. If nginx is already installed, Ansible won't
install it again. This prevents unintended changes.
Q: What is the difference between a task and a handler?
A task always runs when the play executes. A handler only runs when notified by a task, and only if that task
made a change. Used for things like restarting services.
Q: What is Ansible Vault?
A feature to encrypt sensitive data like passwords and API keys so they can be safely stored in version control.
Q: What is an Ansible Role?
A structured, reusable way to organize tasks, handlers, templates, and variables. Like a function in programming
— write once, use many times.
Q: How do you handle different environments in Ansible?
Use separate inventory files (dev-inventory.ini, prod-inventory.ini) and separate variable files. Run: ansible-
playbook playbook.yml -i prod-inventory.ini
DOCUMENT STATUS & STUDY PLAN
✅  What's Covered in This Document
# Section Topics Covered Status
1 AWS Core IAM, Regions, AZs, Security Groups, ACLs, Auto Scaling, ALB vs NLB,
CloudWatch, RDS vs DynamoDB, S3 vs EBS, VPC, Subnets, Elastic IP
✅
Complete
2 Kubernetes Docker drawbacks, Swarm vs K8s, K8s features, Architecture, kOps, RC vs RS,
Deployments, Services (ClusterIP/NodePort/LB), Volumes
(emptyDir/hostPath/PV/PVC), Namespaces, DaemonSet, ConfigMap,
✅
Complete




Secrets, RBAC, Jobs, CronJobs, Troubleshooting (9 errors), Deployment
Strategies (Recreate/Rolling/Blue-Green/Canary), StatefulSet
3 Docker VM vs Container, Docker Architecture, Images, Dockerfile (all instructions),
Registry, Container Lifecycle, Port Mapping, Compose (2 types), Volumes (3
types), Networking (Bridge/Host/None/Overlay/Macvlan), Multi-stage,
Jenkins Pipeline, Security
✅
Complete
4 Jenkins What is Jenkins, Job types, Jenkinsfile, Pipeline stages, Triggers, Declarative
vs Scripted, Credentials, Master/Agent, Shared Libraries, Blue Ocean
✅
Complete
5 Git VCS types, Git workflow, 4 working areas, Setup, Basic commands,
Branching, Merging (3 types), Merge conflicts, Remote repo,
Push/Pull/Fetch/Clone, Undoing changes, Stash, Cherry-pick, Rebase, Tags,
.gitignore, Branching strategies, PR workflow
✅
Complete
6 Linux Features, Distros, Architecture, Shell types, File system structure, File system
types, Absolute/Relative path, File commands, Volume on EC2, System
commands, User management, Group management, File permissions, ACL
(setfacl/getfacl), Compression, Filter commands + Regex,
find/locate/updatedb, Piping/Redirection, Networking commands
✅
Complete
7 Terraform What is Terraform, How it works, Files, Commands, Providers, Resource
blocks, VPC creation, Variables (all types), Outputs, State (local vs remote),
Workspaces, Modules, Meta-arguments, Data sources, Locals, Interview
Q&A
✅
Complete
8 Azure
DevOps
DevOps culture, Azure DevOps 5 services, Boards
(Epics/Features/Stories/Tasks), Repos, Branch policies, PR templates, Self-
hosted agent setup, YAML pipelines, Triggers, Variables, Multi-stage
pipelines, Environments, Approvals, DORA metrics, Your Project 1 (Tomcat
CI/CD), Your Project 2 (Reverse Proxy + LGTM)
✅
Complete
9 Ansible What is Ansible, Architecture, Components, Installation, Inventory, Ad-hoc
commands, Playbooks, Common modules, Variables, Handlers,
Conditionals/Loops, Templates (Jinja2), Roles, Vault, Complete deploy
playbook, DevOps use cases, Interview Q&A
✅
Complete
❌  Things Still Missing / To Add Later
Topic Priority Why Important
AWS Scenario-based questions 🔴  High Interviewers love scenarios




AWS Lambda basics 🟡  Medium Serverless trending
AWS EKS (managed Kubernetes) 🟡  Medium Alternative to kOps
Networking deep dive (OSI, DNS, TCP/IP) 🟡  Medium DevOps fundamentals
SonarQube basics 🟡  Medium On your Jenkins pipeline
Nexus basics 🟡  Medium Artifact management
GitHub Actions vs Jenkins vs Azure Pipelines 🟡  Medium Common interview comparison
PostgreSQL basics 🟢  Low On your resume
Apache Tomcat deep dive 🟢  Low Your project experience covers it
Mock interview questions (all topics) 🔴  High Practice makes perfect
📊  Document Statistics
Metric Value
Total Sections 9
Estimated Pages 190-200 pages
Topics Covered 150+
Commands Included 500+
YAML Examples 40+
Based on Your Resume ✅  Yes
📅  Suggested Study Plan
Phase 1 — Foundation (Week 1)
Go through these first — you have hands-on experience:




Day 1: Git (Section 5) — you used this daily
Day 2: Linux (Section 6) — you did system hardening
Day 3: Docker (Section 3) — you containerized apps
Day 4: Kubernetes (Section 2) — your kOps project
Day 5: Azure DevOps (Section 8) — your strongest project
Day 6-7: Revise everything from Week 1
Phase 2 — Tools (Week 2)
Day 8:  Jenkins (Section 4)
Day 9:  Terraform (Section 7)
Day 10: Ansible (Section 9)
Day 11: AWS (Section 1)
Day 12: Practice explaining your 3 projects out loud
Day 13-14: Mock interview questions
Phase 3 — Interview Prep (Week 3)
Day 15: Practice project explanations (record yourself)
Day 16: Scenario-based questions (AWS, K8s)
Day 17: Common DevOps interview patterns
Day 18: HR questions + salary negotiation
Day 19: Apply for jobs
Day 20: Keep applying, keep practicing
💡  How to Use This Document
Step 1: Read each section once (don't memorize yet)
Step 2: Read again, highlight commands you don't know
Step 3: Practice commands in terminal
Step 4: Try to explain each concept out loud (like in an interview)
Step 5: Focus on your PROJECT explanations — interviewers will go deep
Step 6: Go through this document 3-4 times minimum
🎯  Interview Preparation Tips




Top 5 things interviewers ask for DevOps roles:
1. "Tell me about your projects" — Practice this 10 times out loud
2. "What happens when a Pod crashes?" — Kubernetes troubleshooting
3. "How does your CI/CD pipeline work?" — End to end explanation
4. "What is the difference between..." — comparison questions
5. "How would you handle [scenario]?" — problem solving
Your Strongest Cards to Play:
✅  Kubernetes cluster using kOps on AWS (rare experience)
✅  Multi-tier app (Node.js + Apache + PostgreSQL) on K8s
✅  LGTM stack monitoring (shows you go beyond basics)
✅  Multi-port reverse proxy with Apache (middleware knowledge)
✅  Azure DevOps full pipeline with self-hosted agent
What to say when you don't know something:
"I haven't worked with that directly, but based on my experience with [similar thing], I understand it works
by..."
🚀  You're Doing Great, DevOpsEngineer!
This document is your complete DevOps preparation bible.
Go through it multiple times, practice out loud, and you'll be ready.
Remember: Consistency beats intensity. 2 hours every day beats 14 hours on Sunday.
Document prepared by Claude for DevOps & Cloud Engineer — DevOps & Cloud Engineer
Keep going. You've got this! 💪





