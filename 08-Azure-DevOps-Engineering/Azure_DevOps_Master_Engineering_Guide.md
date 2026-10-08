# 🔷 Azure DevOps & Observability: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Azure Boards Agile Governance, Repos Branch Policies, Multi-Stage YAML Pipelines, Self-Hosted Linux Agent Pools, Real Production Projects, Apache Reverse Proxy, and the LGTM Observability Stack.

---

## 📑 Table of Contents
- [Azure DevOps Platform Overview & 5 Core Services](#platform-overview)
- [Azure Boards: Agile Sprints, Epics, Features, User Stories](#azure-boards)
- [Azure Repos: Branch Policies & Pull Request Governance](#azure-repos)
- [Azure Pipelines: Multi-Stage Production YAML Blueprint](#azure-pipelines)
- [Self-Hosted Linux Agent Pool Setup & systemd Automation](#self-hosted-agents)
- [Apache Reverse Proxy & SSL Let's Encrypt Configuration](#apache-reverse-proxy)
- [The LGTM Enterprise Observability Stack (Loki, Grafana, Tempo, Mimir)](#lgtm-stack)
- [Production Troubleshooting Playbook & Senior Interview Q&A](#troubleshooting--qa)

---

SECTION 8: AZURE DEVOPS — COMPLETE GUIDE
Based on your actual project experience + complete theory for interviews
1. What is DevOps?
Definition:




DevOps is a culture + set of practices that unites Development (Dev) and Operations (Ops) to deliver software
faster, more reliably, and with higher quality.
Before DevOps:
Dev team wrote code → threw it over the wall to Ops
Ops had to figure out how to deploy it
Slow releases, blame culture, outages
Three words summarize DevOps: Collaborate. Automate. Deliver.
Note: DevOps is NOT just a tool. It is a mindset first, tools second.
DevOps Lifecycle (8 Stages):
Plan → Code → Build → Test → Release → Deploy → Operate → Monitor
  ↑                                                              │
  └──────────────── Feedback Loop ──────────────────────────────┘
Stage What happens
Plan Define features, user stories, sprints
Code Write code, commit to Git
Build Compile code, run automated builds (CI)
Test Run automated unit/integration tests
Release Package build artifact for deployment
Deploy Push to dev/staging/production (CD)
Operate Monitor running application
Monitor Collect metrics, logs, alerts — feed back into planning
2. What is Azure DevOps?
Definition:
Azure DevOps is Microsoft's cloud platform that provides ALL tools needed to practice DevOps in one place.
Available at dev.azure.com




5 Services of Azure DevOps:
Service Purpose
Azure Boards Plan work — tasks, bugs, sprints, Kanban boards
Azure Repos Store and manage code using Git
Azure Pipelines Build and deploy automatically (CI/CD)
Azure Test Plans Manual and automated testing management
Azure Artifacts Store and share code packages (NuGet, npm, etc.)
Key Terms:
Term Meaning
CI Automatically build and test code every push
CD Automatically deliver tested build to environment
Pipeline Series of automated steps to build/test/deploy
Repository Folder storing all code with version history
Sprint Fixed time period (2 weeks) to complete planned work
Build Agent Machine that runs pipeline steps
Artifact Output of a build (zip, jar, Docker image)
Environment Deployment target: Dev, Staging, Production
3. Azure DevOps Structure
Organization (dev.azure.com/YourOrg)
    ↓
Project (WebApp, MobileApp, InfraProject)
    ↓
Services (Boards, Repos, Pipelines, Artifacts, Test Plans)
Access Levels:




Level Access
Stakeholder (Free) View boards, add work items — no code/pipeline
Basic (Free for 5) Full access to Boards, Repos, Pipelines
Basic + Test Plans Adds Azure Test Plans
4. Azure Boards — Project Management
What is Azure Boards?
A project management tool to plan, track, and discuss work — similar to Jira or Trello.
Work Item Hierarchy (Agile Process):
Epic
  ↓ (large business objective)
Feature
  ↓ (functional component)
User Story
  ↓ (requirement from user's perspective)
Task / Bug
  (technical implementation / defect)
Work Item States:
New → Active → Resolved → Closed
Key Features:
Kanban Board — visual drag-and-drop workflow (Boards → Boards)
Backlog — prioritized list of all upcoming work (Boards → Backlogs)
Sprints — time-boxed delivery cycles (Boards → Sprints)
Queries — save custom filters (owner, state, priority, tags)
Dashboards — widgets for visibility (Sprint Burndown, Build History, Velocity)
Process Types:
Process Work Items Use When




Agile Epics, Features, Stories, Tasks, Bugs Most teams
Scrum Epics, Features, PBIs, Tasks, Bugs Sprint-focused
CMMI More formal, adds Change Requests Regulated industries
Basic Just Issues and Tasks Learning/small projects
Your Project — Azure Boards Setup:
In your Azure DevOps project you configured:
- Epics, Features, Tasks hierarchy for full project visibility
- Query Management for custom views tracking real-time task progress and bug fixes
- User roles and permissions for secure resource allocation
- PR templates to standardize code reviews and link every merge to a Task or Feature
5. Azure Repos — Source Control
What is Azure Repos?
A source control system within Azure DevOps to track and manage code changes. Supports Git (distributed)
and TFVC (centralized).
Git vs TFVC:
Feature Git (Distributed) TFVC (Centralized)
Local copy Full history Only current version
Offline work ✅  Yes ❌  No
Popularity Industry standard Legacy/enterprise
Branching Easy and fast Complex
Always use Git for modern projects.




Pull Request (PR) Workflow:
Developer creates feature branch
        ↓
Makes and pushes changes
        ↓
Creates Pull Request
        ↓
Reviewers review code (approve/reject/comment)
        ↓
All checks pass (policies)
        ↓
Merge to main
        ↓
Delete feature branch
Branch Policies (protect main branch):
# In Azure DevOps:
Project Settings → Repositories → Branch Policies → main
Policies to enable:
✅  Minimum reviewers: 2
✅  Check for linked work items
✅  Check for comment resolution
✅  Build validation (CI must pass before merge)
✅  Limit merge types (squash only)
PR Template — Your Project Setup:
# Create file at:
.azuredevops/pull_request_template.md
## What type of PR is this?
- [ ] Feature
- [ ] Bugfix
- [ ] Enhancement
## Description of changes
## Related Work Item / Issue
## Unit Testing




## Post-deployment tasks
IMPORTANT: Template must be in .azuredevops/  folder and merged to main branch to take effect.
6. Self-Hosted Agent — Complete Setup
What is an Agent?
A machine that runs your pipeline steps. When pipeline is triggered, Azure DevOps assigns an agent to execute
each job.
Microsoft-Hosted vs Self-Hosted:
Feature Microsoft Hosted Self-Hosted
Setup No setup needed Install manually
Cost 1800 free mins/month Unlimited
Tools Pre-installed common tools You control everything
Network Public internet only Can access private network
Speed Fresh VM each time (slower start) Persistent (faster)
Use when Simple CI, open source Corporate network, special tools
Self-Hosted Agent Setup — Your Project Steps:
# STEP 1 — Download Agent
# Azure DevOps → Organization Settings → Agent Pools → Default → New Agent
# Download: vsts-agent-linux-x64-4.x.x.tar.gz
# STEP 2 — Extract
mkdir ~/myagent
cd ~/myagent
tar -xvzf vsts-agent-linux-x64-4.x.x.tar.gz
# STEP 3 — Configure
./config.sh
# During setup, enter:
# Server URL:     https://dev.azure.com/my-org
# Auth type:      PAT (press Enter)




# PAT:            <paste your Personal Access Token>
# Agent pool:     Default
# Agent name:     myagent
# Work folder:    press Enter (_work)
# STEP 4 — Start Agent
./run.sh
# Expected output: Listening for Jobs
# STEP 5 — Verify Online
# Azure DevOps → Organization Settings → Agent Pools → Default
# Status: myagent → ONLINE (green)
Create PAT (Personal Access Token):
Azure DevOps → Profile → Personal Access Token → New Token
Scope: Agent Pools → Read & Manage
Copy token (shown only once!)
Common Agent Errors:
Error Reason Fix
Agent Offline run.sh not running ./run.sh
VS30063 Unauthorized Wrong PAT or permissions Recreate PAT with Agent Pools: Read & Manage
Pipeline uses Microsoft agent vmImage still in YAML Remove vmImage, use pool name
Agent not visible Wrong org URL Use https://dev.azure.com/
7. Azure Pipelines — Complete Guide
What is a Pipeline?
An automated workflow that builds, tests, and deploys your code.
Two ways to create:
Method Description
Classic Editor (GUI) Visual editor, drag-and-drop. Good for beginners.




YAML Pipeline Pipeline as code, stored in repo. Modern standard. ✅
YAML Basics
Rules:
Indentation: SPACES only (never tabs), 2 spaces per level
Case-sensitive: name  and Name  are different
Lists use dash: - item
Key-value: key: value  (space after colon is REQUIRED)
Comments: #
Pipeline Hierarchy:
Pipeline (azure-pipelines.yml)
  ↓
Stages (Build, Test, Deploy)
  ↓
Jobs (BuildJob, TestJob)
  ↓
Steps (script, task)
  ↓
Tasks (Docker@2, KubernetesManifest@0)
Basic Pipeline Structure
# azure-pipelines.yml
trigger:
- main                          # run when code pushed to main
pool:
  name: Default                 # self-hosted agent pool (YOUR PROJECT)
  # vmImage: 'ubuntu-latest'   # Microsoft-hosted (comment out for self-hosted)
variables:
  buildConfig: Release
  appName: myapp
stages:
- stage: Build
  displayName: Build Stage
  jobs:
  - job: BuildJob




    steps:
    - script: echo "Building $(appName)"
      displayName: 'Build Step'
- stage: Test
  displayName: Test Stage
  dependsOn: Build
  jobs:
  - job: TestJob
    steps:
    - script: echo "Running Tests"
      displayName: 'Test Step'
- stage: Deploy
  displayName: Deploy Stage
  dependsOn: Test
  condition: succeeded()
  jobs:
  - deployment: DeployJob
    environment: Production
    strategy:
      runOnce:
        deploy:
          steps:
          - script: echo "Deploying to Production"
Your Project — YAML Pipeline (Self-Hosted Agent)
# Your actual pipeline connecting to myagent
trigger:
- main
pool:
  name: Default
  demands:
  - Agent.Name -equals myagent    # specifically use YOUR agent
steps:
- script: echo Hello, world!
  displayName: 'Run a one-line script'
- script: |
    echo Running on self-hosted agent
    echo Agent Name: myagent
  displayName: 'Run a multi-line script'




Pipeline Triggers
# Push trigger (most common)
trigger:
- main
- develop
# PR trigger (validate before merge)
pr:
- main
# Scheduled trigger (nightly builds)
schedules:
- cron: "0 2 * * *"           # 2am every night
  displayName: Nightly Build
  branches:
    include:
    - main
# Manual only (no auto-trigger)
trigger: none
Multi-Stage Pipeline (Build → Test → Deploy)
trigger:
- main
pool:
  vmImage: 'ubuntu-latest'
stages:
# ── STAGE 1: BUILD ──
- stage: Build
  displayName: Build Stage
  jobs:
  - job: BuildJob
    steps:
    - script: echo "Running Build on Ubuntu"
      displayName: 'Build'
# ── STAGE 2: TEST ──
- stage: Test
  displayName: Test Stage
  dependsOn: Build
  jobs:




  - job: TestJob
    pool:
      vmImage: 'windows-latest'    # override to use Windows for testing
    steps:
    - script: echo "Running Tests on Windows"
# ── STAGE 3: UAT ──
- stage: UAT
  displayName: UAT Stage
  dependsOn: Test
  jobs:
  - job: UATJob
    steps:
    - script: echo "Running UAT"
# ── STAGE 4: PRODUCTION ──
- stage: Production
  displayName: Production Stage
  dependsOn: UAT
  jobs:
  - deployment: DeployProd
    environment: Production       # approval required here
    strategy:
      runOnce:
        deploy:
          steps:
          - script: echo "Deploying to Production"
Pool Assignment Rules
Stage-level pool → all jobs inherit it
Job-level pool → overrides stage pool
Stage Pool (Ubuntu)
   ↓
Job1 (Ubuntu — inherited)
Job2 (Windows — overridden at job level)
Pipeline Variables
# Inline variables
variables:
  appName: myapp
  buildConfig: Release
  tag: $(Build.BuildId)        # built-in variable




# Reference
steps:
- script: echo Building $(appName) version $(tag)
Built-in Variables:
Variable Value
$(Build.BuildId) Unique build ID
$(Build.BuildNumber) Human-readable build number
$(Build.SourceBranch) Branch that triggered (refs/heads/main)
$(Build.ArtifactStagingDirectory) Temp folder for build output
$(System.DefaultWorkingDirectory) Root folder where code is checked out
$(Agent.OS) OS of agent (Linux, Windows_NT)
Variable Groups and Secrets
# Variable Group (reusable across pipelines)
# Create: Pipelines → Library → Variable Group → SharedConfig
variables:
- group: SharedConfig          # reference group
- name: buildConfig
  value: Release
# Secret variables — encrypted, shows *** in logs
# Add in Pipeline UI → Variables tab → lock icon
# Reference same way: $(MySecret)
Environments and Approvals
# Create environments:
Pipelines → Environments → New Environment → Production
# Add approval:
Environment → ... → Approvals and Checks → Approval → assign approvers




# Pipeline pauses at that stage, sends email to approvers
# Approver clicks Approve or Reject
Complete CI/CD Pipeline — Docker + Jenkins style (Your Project Context)
trigger:
- main
pool:
  name: Default
variables:
  IMAGE_NAME: devops/myapp
  IMAGE_TAG: $(Build.BuildId)
stages:
- stage: Clone
  displayName: Clone Code
  jobs:
  - job: CloneJob
    steps:
    - checkout: self            # Azure DevOps auto-checks out code
- stage: Build
  displayName: Build Application
  dependsOn: Clone
  jobs:
  - job: BuildJob
    steps:
    - script: |
        npm install
        npm run build
      displayName: 'Build Code'
- stage: Test
  displayName: Run Tests
  dependsOn: Build
  jobs:
  - job: TestJob
    steps:
    - script: npm test
      displayName: 'Run Unit Tests'
- stage: DockerBuild
  displayName: Build Docker Image
  dependsOn: Test




  jobs:
  - job: DockerJob
    steps:
    - script: |
        docker build -t $(IMAGE_NAME):$(IMAGE_TAG) .
        docker tag $(IMAGE_NAME):$(IMAGE_TAG) $(IMAGE_NAME):latest
      displayName: 'Build Docker Image'
- stage: DockerPush
  displayName: Push to Registry
  dependsOn: DockerBuild
  jobs:
  - job: PushJob
    steps:
    - script: |
        docker login -u $(DOCKER_USER) -p $(DOCKER_PASS)
        docker push $(IMAGE_NAME):$(IMAGE_TAG)
        docker push $(IMAGE_NAME):latest
      displayName: 'Push Docker Image'
- stage: Deploy
  displayName: Deploy Container
  dependsOn: DockerPush
  jobs:
  - deployment: DeployJob
    environment: Production
    strategy:
      runOnce:
        deploy:
          steps:
          - script: |
              docker stop myapp || true
              docker rm myapp || true
              docker pull $(IMAGE_NAME):$(IMAGE_TAG)
              docker run -d --name myapp -p 80:3000 $(IMAGE_NAME):$(IMAGE_TAG)
            displayName: 'Deploy Container'
8. Your Project 1 — Azure DevOps CI/CD with Tomcat
What you built:
Deploy a web application to Apache Tomcat using Azure DevOps self-hosted agent.
Architecture:




 
Local Code
    ↓ git push
Azure DevOps Repo (main branch)
    ↓ pipeline triggered
Self-Hosted Agent (myagent on Azure VM)
    ↓ copy files
Tomcat ROOT (webapps/ROOT/)
    ↓
Website LIVE on Azure VM
Apache Tomcat Setup on Azure VM:
# Step 1 — Install Java
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
# Step 2 — Download Tomcat 11
cd /opt
sudo wget https://downloads.apache.org/tomcat/tomcat-11/v11.0.18/bin/apache-tomcat-11
sudo tar -xvzf apache-tomcat-11.0.18.tar.gz
sudo mv apache-tomcat-11.0.18 tomcat11
# Step 3 — Fix Permissions
sudo chown -R azureuser:azureuser /opt/tomcat11
# Step 4 — Give Execute Permission
cd /opt/tomcat11/bin
chmod +x *.sh
# Step 5 — Start Tomcat
./startup.sh
ss -tulnp | grep 8080          # verify running on port 8080
# Step 6 — Open Azure Network Rule
# Azure Portal → VM → Networking → Add inbound rule
# Port: 8080, Protocol: TCP, Action: Allow
# Step 7 — Access in browser
# http://<VM_PUBLIC_IP>:8080
Change Tomcat Port (8080 → 7789):




nano /opt/tomcat11/conf/server.xml
# Find: <Connector port="8080" ... />
# Change to: <Connector port="7789" ... />
# Restart
cd /opt/tomcat11/bin
./shutdown.sh && sleep 5 && ./startup.sh
ss -tulnp | grep 7789
Pipeline for Auto-Deploy to Tomcat:
trigger:
- main
pool:
  name: Default                 # self-hosted agent on Azure VM
steps:
- script: |
    cp index.html /opt/tomcat11/webapps/ROOT/index.html
  displayName: 'Deploy to Tomcat'
Common Errors and Fixes:
Error Reason Fix
gzip: not in gzip
format
Wrong download URL (HTML
downloaded)
Use correct apache.org URL
Permission denied Files owned by root sudo chown -R azureuser:azureuser
/opt/tomcat11
403 Access Denied Tomcat allows localhost only Remove RemoteAddrValve from context.xml
404 Not Found Page doesn't exist Check file is in correct webapps folder
Pipeline not
triggering
Push to wrong branch Check trigger is main , push to main
Pool not found Using agent name not pool
name
Use pool: name: Default
Git auth failed Password auth blocked Use PAT as password




Git Workflow for Your Project:
git branch                      # check current branch
git status                      # check changes
git add .
git commit -m "updated files"
git push origin main            # push to trigger pipeline
# If on feature branch, merge to main first:
git checkout main
git pull origin main
git merge feature
git push origin main            # now pipeline triggers
9. Your Project 2 — Multi-Port Reverse Proxy with LGTM Monitoring
What you built:
Multiple Tomcat instances behind Apache Reverse Proxy with LGTM stack monitoring.
Architecture:
Internet (Port 80)
    ↓
Apache HTTP Server (Reverse Proxy)
    ├── /project1 → Tomcat Instance 1 (Port 7789)
    └── /project2 → Tomcat Instance 2 (Port 8888)
Azure VM
├── Apache Reverse Proxy (Port 80)
├── Tomcat Instance 1 (Port 7789)
├── Tomcat Instance 2 (Port 8888)
├── Promtail (Log Collector)
├── Loki (Log Storage, Port 3100)
└── Grafana (Visualization, Port 3000)
Two Tomcat Instances Setup:
# Create two separate physical directories
cd /tmp
wget https://archive.apache.org/dist/tomcat/tomcat-11/v11.0.18/bin/apache-tomcat-11.0
tar -xvf apache-tomcat-11.0.18.tar.gz




 
sudo mv apache-tomcat-11.0.18 /opt/tomcat1
sudo cp -r /opt/tomcat1 /opt/tomcat2
sudo chown -R azureuser:azureuser /opt/tomcat1 /opt/tomcat2
# Configure unique ports in server.xml:
# Tomcat 1: port 7789
# Tomcat 2: port 8888 (also change shutdown port to 8006, AJP to 8010)
# Create project files
mkdir -p /opt/project1 /opt/project2
echo "<h1>Project 1 Works</h1>" > /opt/project1/index.html
echo "<h1>Project 2 Works</h1>" > /opt/project2/index.html
# Link to Tomcat webapps
ln -s /opt/project1 /opt/tomcat1/webapps/project1
ln -s /opt/project2 /opt/tomcat2/webapps/project2
# Start both
/opt/tomcat1/bin/startup.sh
/opt/tomcat2/bin/startup.sh
Apache Reverse Proxy Configuration:
# Enable modules
sudo a2enmod proxy proxy_http
# Create config
sudo nano /etc/apache2/sites-available/my-proxy.conf
<VirtualHost *:80>
    ProxyPreserveHost On
    # Route Project 1 to Tomcat 1
    ProxyPass /project1 http://127.0.0.1:7789/project1
    ProxyPassReverse /project1 http://127.0.0.1:7789/project1
    # Route Project 2 to Tomcat 2
    ProxyPass /project2 http://127.0.0.1:8888/project2
    ProxyPassReverse /project2 http://127.0.0.1:8888/project2
    ErrorLog ${APACHE_LOG_DIR}/proxy-error.log
</VirtualHost>




# Enable and restart
sudo a2dissite 000-default.conf
sudo a2ensite my-proxy.conf
sudo systemctl restart apache2
# Test
curl -I http://localhost:7789/project1/
curl -I http://localhost:8888/project2/
# Public: http://<Azure-Public-IP>/project1/
LGTM Stack — Monitoring Setup:
# Observability answers 3 questions:
# 1. What happened?              → LOGS   (Loki)
# 2. How is system performing?   → METRICS (Mimir)
# 3. How did request travel?     → TRACES  (Tempo)
# 4. How to visualize all this?  → Grafana
# Flow:
Apache/Tomcat → logs → Promtail → Loki → Grafana
# Install Grafana
sudo apt-get install -y apt-transport-https software-properties-common wget
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyri
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable mai
sudo apt-get update && sudo apt-get install -y grafana
sudo systemctl enable grafana-server && sudo systemctl start grafana-server
# Install Loki
sudo mkdir -p /opt/loki && cd /opt/loki
sudo curl -L -O https://github.com/grafana/loki/releases/download/v2.9.3/loki-linux-am
sudo apt install unzip -y && sudo unzip loki-linux-amd64.zip
sudo chmod +x loki-linux-amd64
sudo mkdir -p /tmp/loki/chunks /tmp/loki/rules
sudo chmod -R 777 /tmp/loki
# Install Promtail
sudo curl -L -O https://github.com/grafana/loki/releases/download/v2.9.3/promtail-linu
sudo unzip promtail-linux-amd64.zip
sudo chmod +x promtail-linux-amd64
sudo mv promtail-linux-amd64 /usr/local/bin/promtail
# Start services
sudo /opt/loki/loki-linux-amd64 -config.file=/etc/loki/loki-config.yaml &
sudo /usr/local/bin/promtail -config.file=/etc/loki/promtail-config.yaml &




 
# Quick start after VM reboot
sudo systemctl start grafana-server
sudo /opt/loki/loki-linux-amd64 -config.file=/etc/loki/loki-config.yaml &
sudo /usr/local/bin/promtail -config.file=/etc/loki/promtail-config.yaml &
# Access Grafana
# http://<VM-IP>:3000
# Login: admin / admin
# Add Loki datasource: Connections → Data Sources → Loki → URL: http://localhost:3100
10. Azure DevOps Key Concepts for Interviews
DORA Metrics (what interviewers love to ask):
Metric Description Elite
Deployment Frequency How often you deploy to production Multiple times per day
Lead Time for Changes Commit to production time Less than 1 hour
Change Failure Rate % of deployments causing incidents Less than 5%
Mean Time to Restore (MTTR) Recovery time from failure Less than 1 hour
DevOps vs Traditional (Waterfall):
Waterfall DevOps
Release cycle 6-12 months Hours to days
Teams Siloed Dev + Ops Unified
Testing End, manual Continuous, automated
Failure risk Very high Low
Interview One-Liners:
"Azure Boards is our project management tool where we track work using Epics → Features → User Stories
→ Tasks hierarchy."
"We used self-hosted agents on Azure VMs because we needed direct access to Tomcat deployed on the
same VM."




"PR templates standardized our code review process by ensuring every merge was linked to a specific work
item."
"We integrated the LGTM stack — Loki, Grafana, Tempo, Mimir — to monitor automation environment
health."
Azure DevOps — Advanced Topics
New content not covered previously. Adds Azure Artifacts, Test Plans, Key Vault, Pipeline Templates, IaC
with ARM/Bicep, Security, Monitoring, and AZ-400 prep.
A. Azure Artifacts — Package Management
What is Azure Artifacts?
A package management service that stores libraries your code depends on — npm, NuGet, Maven, PyPI — in a
private, secure feed hosted by Azure.
What is a Package?
Reusable code bundled and published so other projects can depend on it. Instead of copying code across
projects, you publish it as a package (e.g. v1.0.0) and reference it as a dependency.
What is a Feed?
A private container for your packages. Think of it as your own private npm registry or NuGet gallery.
Package Types:
Type Language Extension
NuGet .NET / C# .nupkg
npm JavaScript / Node.js package.json
Maven Java .jar
PyPI Python .whl
Universal Any file type zip, binary




 
 
Create a Feed:
Artifacts → + Create Feed → Name it → Set visibility → Add upstream sources → Create
Upstream Sources:
A feed can proxy public registries like npmjs.com or nuget.org. Your team fetches packages through your Azure
Artifacts feed — providing caching, security scanning, and control.
Commands:
# NuGet
dotnet pack                                          # create .nupkg file
dotnet nuget push *.nupkg --source MyFeed           # push to Azure Artifacts
dotnet restore                                       # download packages from feed
# npm
npm publish --registry https://pkgs.dev.azure.com/YourOrg/_packaging/MyFeed/npm/regist
Semantic Versioning:
MAJOR.MINOR.PATCH
1.0.0 → 2.0.0  Breaking change
1.0.0 → 1.1.0  New feature (backward compatible)
1.0.0 → 1.0.1  Bug fix only
Rule: Never overwrite an existing version. Always publish a new one.
B. Azure Test Plans — Manual Testing
What is Azure Test Plans?
A testing management tool to create test cases, organize them into test suites, execute tests manually, and
track results — all linked to your work items.
Terminology:
Term Meaning
Test Plan Container for all testing in a sprint or release




 
Test Suite Group of related test cases (e.g. Login Tests)
Test Case Specific scenario with steps to verify a feature
Test Step One action + expected result
Test Run Actual execution session
Test Result Passed, Failed, or Blocked
Workflow:
Create Test Plan → Create Test Suites → Write Test Cases (with steps) → Run Tests → Ma
Key Metrics:
Pass Rate — % of test cases that passed
Test Coverage — % of user stories covered by test cases
Traceability Matrix — shows which stories have test cases, gaps visible
C. Pipeline Variables, Groups & Key Vault
Types of Variables:
Type Description
Inline YAML Defined in YAML under variables:
Pipeline UI Defined in pipeline settings in Azure DevOps
Variable Groups Shared collection, reusable across pipelines
Secret Variables Encrypted, never shown in logs
Azure Key Vault Secrets from Key Vault linked to variable group
Inline Variables:
variables:
  buildConfig: Release
  appName: MyWebApp




steps:
  - script: echo Building $(appName) in $(buildConfig) mode
Variable Groups:
# Create: Pipelines → Library → + Variable Group → SharedConfig
variables:
  - group: SharedConfig          # reference group
  - name: buildConfig
    value: Release
Secret Variables:
# Add in Pipeline UI → Variables tab → click lock icon
# Reference same way: $(MySecret)
# Shows as *** in logs — NEVER hard-code secrets in YAML!
Azure Key Vault Integration:
Azure Portal → Create Key Vault → Add secrets (DatabasePassword, ApiKey)
Azure DevOps → Variable Group → Toggle "Link secrets from Azure Key Vault"
→ Select subscription and Key Vault → Choose which secrets to expose
→ Reference in YAML: $(DatabasePassword)
Runtime Parameters (user input when triggering):
parameters:
  - name: environment
    displayName: Target Environment
    type: string
    default: dev
    values:
      - dev
      - staging
      - production
# Reference: ${{ parameters.environment }}
Template expressions vs Runtime expressions:




Syntax When evaluated
Template parameter ${{ parameters.name }} When YAML is parsed
Pipeline variable $(variableName) When step actually runs
D. Pipeline Templates — Reusability
Why Templates?
Without templates you copy the same YAML steps across 10 pipelines. Change one step = update 10 files.
Templates solve this — define once, reuse everywhere.
Types:
Type Purpose
Step template Reusable set of steps
Job template Reusable job with its own steps
Stage template Reusable stage
Variable template Shared variable definitions
Step Template Example:
# templates/build-steps.yml
parameters:
  - name: configuration
    type: string
    default: Release
steps:
  - script: dotnet restore
    displayName: Restore
  - script: dotnet build --configuration ${{ parameters.configuration }}
    displayName: Build
  - script: dotnet test
    displayName: Test
Use in Main Pipeline:




stages:
  - stage: Build
    jobs:
      - job: BuildJob
        steps:
          - template: templates/build-steps.yml
            parameters:
              configuration: Release
Variable Template:
# templates/vars.yml
variables:
  appName: MyWebApp
  environment: production
# In main pipeline:
variables:
  - template: templates/vars.yml
  - name: buildConfig
    value: Release
extends — Enforce Company Standards:
# Force all pipelines to use a base template (security teams use this)
extends:
  template: templates/secure-pipeline.yml
  parameters:
    appName: MyApp
E. Environments & Deployment Strategies (Deep Dive)
Checks on Environments:
Check Description
Approvals Named person must approve before proceeding
Branch Control Must be running from approved branch (e.g. main only)




Business Hours Deployment only allowed during certain hours
Invoke Azure Function API must return success before proceeding
Query Work Items Block if open P1 bugs exist on the board
Setting up Environment Checks:
Pipelines → Environments → Select Environment → ... → Approvals and Checks
→ Add Approval → assign approvers
→ Add Branch Control → allow only: refs/heads/main
Deployment Job YAML:
jobs:
  - deployment: DeployToProduction
    displayName: Deploy to Production
    environment: Production           # records deployment history here
    strategy:
      runOnce:
        deploy:
          steps:
            - download: current
              artifact: drop
            - script: echo Deploying version $(Build.BuildNumber)
Deployment Strategies:
Strategy How It Works Use When
runOnce All instances updated at once Dev/Staging, simple deploys
rolling One instance at a time Medium risk, reduce downtime
canary 10% first, then 100% if healthy High risk, validate before full rollout
blue-green Two environments, switch traffic Critical, instant rollback needed
F. Service Connections — Connect to External Services
What is a Service Connection?




Stores credentials for external services securely so pipelines can access them without embedding secrets in
YAML.
Common Types:
Type Use
Azure Resource Manager Deploy to Azure (VMs, App Service, AKS)
Docker Registry Push/pull images from ACR, Docker Hub
GitHub Access GitHub repos
Kubernetes Deploy to K8s clusters
SSH Connect to Linux servers
SonarCloud Code quality analysis
Create Service Connection:
Project Settings → Service Connections → + New Service Connection
→ Select type → Authenticate → Name it → Save
Security Options:
Option When to use
Grant access to all pipelines Convenient, less secure
Restrict to specific pipelines More secure for production
Reference in YAML:
# Azure deployment
- task: AzureCLI@2
  inputs:
    azureSubscription: 'MyAzureServiceConnection'
# Docker push
- task: Docker@2
  inputs:
    containerRegistry: 'MyACRServiceConnection'




G. Security & RBAC in Azure DevOps
Permission Levels:
Level Controls
Organization Create projects, manage billing, manage users
Project Access to Boards, Repos, Pipelines within project
Object Specific repos, pipelines, environments, feeds
Built-in Security Groups:
Group Access
Project Administrators Full control — add members, manage settings
Build Administrators Manage and run all pipelines
Contributors Push code, create PRs, run pipelines
Readers Read-only — view everything, change nothing
Project Collection Administrators Organization-level full control
Branch Policies (Protect main):
Project Settings → Repositories → Select repo → Policies → Branch Policies → main
Add policies:
✅  Require minimum reviewers: 2
✅  Check for linked work items (PR must reference a User Story)
✅  Check for comment resolution (all comments resolved before merge)
✅  Limit merge types (squash only)
✅  Build validation (CI must pass before PR can be merged)
Personal Access Token (PAT):
User Settings (top right) → Personal Access Tokens → + New Token
→ Set expiry date
→ Select minimum scopes needed
→ Copy and store securely (shown only ONCE)
Use PAT for:




- Authenticating self-hosted agents
- Git clone via HTTPS
- REST API calls
- CI/CD tool authentication
H. Azure Container Registry (ACR) + AKS in Pipelines
Azure Container Registry (ACR):
Microsoft's private Docker registry on Azure. Push images to ACR and pull during deployment.
# Build and push to ACR in pipeline
- task: Docker@2
  displayName: Build and push image to ACR
  inputs:
    command: buildAndPush
    repository: myapp
    dockerfile: Dockerfile
    containerRegistry: MyACRServiceConnection    # service connection to ACR
    tags: |
      $(Build.BuildId)
      latest
Azure Kubernetes Service (AKS):
Microsoft's managed Kubernetes — Azure handles the control plane for free.
# Deploy to AKS in pipeline
- task: KubernetesManifest@0
  displayName: Deploy to AKS
  inputs:
    action: deploy
    kubernetesServiceConnection: MyAKSConnection
    namespace: production
    manifests: |
      manifests/deployment.yml
      manifests/service.yml
    containers: myacr.azurecr.io/myapp:$(Build.BuildId)
Complete End-to-End Pipeline (Code → ACR → AKS):




trigger:
  - main
variables:
  acrName: myappackregistry
  imageName: myapp
  tag: $(Build.BuildId)
pool:
  vmImage: ubuntu-latest
stages:
  # Stage 1 — Build Docker Image and Push to ACR
  - stage: Build
    displayName: Build and Push Image
    jobs:
      - job: BuildAndPush
        steps:
          - task: Docker@2
            displayName: Build and push to ACR
            inputs:
              command: buildAndPush
              repository: $(imageName)
              dockerfile: Dockerfile
              containerRegistry: ACRServiceConnection
              tags: |
                $(tag)
                latest
  # Stage 2 — Deploy to Staging
  - stage: DeployStaging
    dependsOn: Build
    displayName: Deploy to Staging
    jobs:
      - deployment: DeployStaging
        environment: Staging
        strategy:
          runOnce:
            deploy:
              steps:
                - task: KubernetesManifest@0
                  inputs:
                    action: deploy
                    kubernetesServiceConnection: AKSConnection
                    namespace: staging
                    manifests: manifests/deployment.yml
                    containers: $(acrName).azurecr.io/$(imageName):$(tag)




  # Stage 3 — Deploy to Production (with approval)
  - stage: DeployProduction
    dependsOn: DeployStaging
    displayName: Deploy to Production
    jobs:
      - deployment: DeployProduction
        environment: Production             # approval required here
        strategy:
          runOnce:
            deploy:
              steps:
                - task: KubernetesManifest@0
                  inputs:
                    action: deploy
                    kubernetesServiceConnection: AKSConnection
                    namespace: production
                    manifests: manifests/deployment.yml
                    containers: $(acrName).azurecr.io/$(imageName):$(tag)
I. Terraform with Azure Pipelines (Azure-native)
# Terraform pipeline using Azure DevOps tasks
steps:
  - task: TerraformInstaller@0
    inputs:
      terraformVersion: latest
  - task: TerraformTaskV2@2
    displayName: Terraform Init
    inputs:
      provider: azurerm
      command: init
      backendServiceArm: MyAzureServiceConnection
      backendAzureRmResourceGroupName: TerraformState-RG
      backendAzureRmStorageAccountName: tfstateaccount
      backendAzureRmContainerName: tfstate
      backendAzureRmKey: prod.terraform.tfstate    # store state in Azure Blob
  - task: TerraformTaskV2@2
    displayName: Terraform Plan
    inputs:
      provider: azurerm
      command: plan




      environmentServiceNameAzureRM: MyAzureServiceConnection
  - task: TerraformTaskV2@2
    displayName: Terraform Apply
    inputs:
      provider: azurerm
      command: apply
      environmentServiceNameAzureRM: MyAzureServiceConnection
ARM Templates vs Bicep vs Terraform:
Tool Language Multi-cloud Complexity
Terraform HCL ✅  Yes Medium
ARM Templates JSON Azure only High (verbose)
Bicep DSL (simpler JSON) Azure only Low (cleaner)
Pulumi TypeScript/Python ✅  Yes Medium
For interviews: Terraform is most popular. Bicep is Microsoft's modern alternative to ARM. You can
mention you use Terraform.
J. Monitoring — Azure Monitor + Application Insights + Dashboards
Azure Monitor:
Central monitoring platform for Azure. Collects metrics (CPU, memory, requests) and logs from applications and
infrastructure.
Component Purpose
Metrics Numeric values over time (CPU %, request count)
Logs Detailed event records (errors, warnings, traces)
Alerts Notify when metric crosses threshold (CPU > 80%)
Dashboards Visual charts and graphs
Workbooks Interactive reports combining metrics, logs, text




Application Insights (APM):
Automatically tracks: request rates, failure rates, response times, exceptions, user behavior — just add the SDK.
Azure Portal → Create Application Insights → Get Connection String
→ Add SDK to your app → Deploy → Live telemetry in minutes
Create Alert:
Azure Monitor → Alerts → + Create → Alert rule
→ Select resource (App Service, AKS)
→ Condition: HTTP 5xx errors > 10 per minute
→ Action group: send email / Teams notification / webhook
→ Severity: Critical / Error / Warning / Informational
Azure DevOps Dashboards:
Dashboards → + Add Widget
Useful widgets:
- Sprint Burndown (remaining work vs time)
- Build History (pass/fail trend)
- Deployment Status (what's deployed where)
- Lead Time (commit to production time)
- Velocity (story points per sprint)
- Work Item Count (bugs open, stories done)
DORA Metrics (Deep Dive):
Metric Elite Teams How to measure
Deployment Frequency Multiple times/day Count pipeline runs to prod
Lead Time for Changes < 1 hour Commit time → production time
Change Failure Rate < 5% % of deploys causing incidents
Mean Time to Restore < 1 hour Incident open → resolved time
K. AZ-400 Exam Prep (Microsoft DevOps Certification)




Exam Details:
Item Detail
Exam AZ-400: Designing and Implementing Microsoft DevOps Solutions
Questions 40-60 questions
Duration 120 minutes
Passing Score 700 / 1000
Cost ~USD 165
Prerequisites AZ-104 or AZ-204 recommended
Exam Domain Breakdown:
Domain Weight
Design and implement build/release pipelines ~40%
Design and implement source control ~15%
Design and implement IaC ~15%
Configure processes and communications ~10%
Develop a security and compliance plan ~10%
Implement an instrumentation strategy ~10%
Critical Topics to Master:
YAML pipeline structure: triggers, stages, jobs, steps, conditions, dependsOn
Variable groups, secret variables, Azure Key Vault integration
Branch policies: minimum reviewers, build validation, comment resolution
Service connections: types, security, scope
Deployment strategies: runOnce, rolling, canary, blue-green
Environment approvals and checks
Docker: Dockerfile, build, push, ACR, Docker@2 task
Kubernetes: AKS, kubectl, KubernetesManifest@0
Terraform: init, plan, apply, state backend in Azure Storage
Application Insights: SDK integration, alerts
DORA metrics: all four metrics and what they measure




Git strategies: branching models, merge types, PR workflow
Sample AZ-400 Practice Questions:
Q1: You need main branch to only receive code through PRs reviewed by at least 2 people. What do you
configure?
Answer: Branch policies on main branch → Require minimum reviewers = 2
Q2: Pipeline fails because it cannot authenticate to ACR. Most secure fix?
Answer: Create a Docker Registry service connection in Project Settings pointing to ACR, reference it in
YAML.
Q3: Deploy to production only if staging succeeds AND a human approves. What do you configure?
Answer: dependsOn: DeployStaging  + condition: succeeded()  on production stage +
Approval check on Production environment.
Q4: Two engineers run terraform apply simultaneously and state gets corrupted. Fix?
Answer: Configure backend to use Azure Blob Storage — it supports native state locking with Terraform.
Q5: Want canary deployment where 10% of users get new version first. What strategy?
Answer: Use canary deployment strategy in deployment job with incrementPercentage: 10.
Key Distinctions Interviewers and Exam Test:
Classic pipelines vs YAML pipelines — exam tests both
Service principal (secure) vs personal credentials (avoid)
Variable group (reusable) vs inline variable (single pipeline)
deployment job type vs regular job type — only deployment records to environment history
${{ parameters.name }}  (compile time) vs $(variableName)  (runtime)
Branch policy (protects branch) vs environment approval (gates deployment)
Free Study Resources:
learn.microsoft.com — official AZ-400 learning path
azuredevopslabs.com — free hands-on labs
docs.microsoft.com/azure/devops — official reference




L. Complete Azure DevOps Quick Reference
# NAVIGATION
dev.azure.com/YourOrg          → Your organization
Boards → Backlogs               → Plan work
Boards → Boards                 → Kanban workflow
Boards → Sprints                → Sprint planning
Repos → Files                   → Browse code
Repos → Pull Requests           → Code reviews
Pipelines → Pipelines           → CI/CD
Pipelines → Environments        → Deployment targets
Pipelines → Library             → Variable groups
Project Settings → Service Connections  → External service creds
Project Settings → Repositories → Branch policies
Organization Settings → Agent Pools     → Agents
# KEY CONCEPTS
CI:                Every push → auto build + test
CD:                Every successful build → auto deploy
Pipeline:          azure-pipelines.yml at repo root
Stage:             Major phase (Build/Test/Deploy)
Job:               Work unit inside stage (max 256/stage)
Step:              Single action (script or task)
Agent:             Machine that runs jobs
Environment:       Deployment target (Dev/Staging/Prod)
Artifact:          Build output (image, zip, jar)
Service Connection: Stored credentials for external services
Variable Group:    Shared variables across pipelines
PAT:               Personal Access Token for authentication

