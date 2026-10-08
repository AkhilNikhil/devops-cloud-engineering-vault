# 📘 Azure DevOps All-In-One Master Guide (Self-Hosted Agents, CI/CD, Boards & Releases)

> *Comprehensive Azure DevOps engineering documentation and hands-on guide.*

---

```text
AZURE DEVOPS – SELF HOSTED AGENT + PIPELINE (FULL STEPS)

========================================================
PART 1 — CREATE SELF-HOSTED AGENT
========================================================

STEP 1: Download Agent
--------------------------------------------------------
Download from Azure DevOps:
Organization Settings → Agent Pools → Default → New Agent

Example file:
vsts-agent-linux-x64-4.269.0.tar.gz
(or windows zip)

========================================================
STEP 2: Extract Agent
--------------------------------------------------------

Linux:
tar -xvzf vsts-agent-linux-x64-4.269.0.tar.gz

Windows:
unzip vsts-agent-win-x64-4.269.0.zip

========================================================
STEP 3: Go Inside Agent Folder
--------------------------------------------------------

cd ~/myagent

========================================================
STEP 4: Configure Agent
--------------------------------------------------------

Linux:
./config.sh

Windows:
config.cmd

Questions asked during setup:

Enter server URL:
https://dev.azure.com/akhilbm13

Authentication type:
Press ENTER (PAT)

Enter Personal Access Token:
<Paste PAT>

Enter agent pool:
Default

Enter agent name:
myagent

Enter work folder:
Press ENTER (_work)

========================================================
STEP 5: Start Agent
--------------------------------------------------------

Linux:
./run.sh

Windows:
run.cmd

Expected output:

Listening for Jobs

========================================================
STEP 6: Verify Agent Online
--------------------------------------------------------

Azure DevOps:
Organization Settings
→ Agent Pools
→ Default

Status should show:

myagent  → ONLINE (green)

========================================================
PART 2 — CREATE PIPELINE
========================================================

STEP 1:
--------------------------------------------------------
Go to:
Azure DevOps → Pipelines → New Pipeline

STEP 2:
--------------------------------------------------------
Select Repository (Azure Repos / GitHub)

STEP 3:
--------------------------------------------------------
Choose YAML pipeline.

STEP 4:
--------------------------------------------------------
Create file in repo:

azure-pipelines.yml

========================================================
PART 3 — CONNECT PIPELINE TO MYAGENT
========================================================

IMPORTANT:
Remove Microsoft hosted agent:

❌ vmImage: ubuntu-latest

Use self-hosted agent pool instead.

========================================================
FINAL WORKING YAML PIPELINE
========================================================

trigger:
- main

pool:
  name: Default
  demands:
  - Agent.Name -equals myagent

steps:
- script: echo Hello, world!
  displayName: 'Run a one-line script'

- script: |
    echo Running on self-hosted agent
    echo Agent Name: myagent
  displayName: 'Run a multi-line script'

========================================================
PART 4 — RUN PIPELINE
========================================================

1. Commit YAML file.
2. Push code to main branch.
3. Pipeline starts automatically.
4. Azure DevOps sends job to myagent.

========================================================
PART 5 — VERIFY PIPELINE USED YOUR AGENT
========================================================

Open pipeline logs.

You should see:

Agent name: myagent

OR

Running on self-hosted agent

========================================================
COMMON ISSUES + FIX
========================================================

1. Agent Offline
--------------------------------
Reason:
run.sh not running.

Fix:
./run.sh

--------------------------------------------------------

2. VS30063 Unauthorized
--------------------------------
Reason:
PAT missing permissions.

Fix:
Create PAT with:
Agent Pools → Read & Manage

--------------------------------------------------------

3. Pipeline uses Microsoft agent
--------------------------------
Reason:
vmImage still present.

Fix:
Use:

pool:
  name: Default

--------------------------------------------------------

4. Agent not visible
--------------------------------
Reason:
Wrong organization URL.

Correct format:
https://dev.azure.com/<organization>

========================================================
INTERVIEW LEVEL SUMMARY
========================================================

Self-hosted agent flow:

Download Agent
→ Extract
→ config.sh
→ Register to Agent Pool
→ run.sh
→ Agent Online
→ Pipeline uses Agent Pool

========================================================
END RESULT
========================================================

Azure Pipeline runs on YOUR machine (myagent)
instead of Microsoft hosted agents.
# END-TO-END DOCUMENTATION: ISOLATED TOMCAT INSTANCES WITH APACHE REVERSE PROXY
# Environment: Azure VM (Ubuntu)
# Goal: Port 80 (Public) -> Tomcat 1 (7789) & Tomcat 2 (8888)

---

## STEP 1: AZURE PORTAL CONFIGURATION (CRITICAL)
# Before touching the terminal, you must open the "Front Door" in Azure.
1. Log in to the Azure Portal.
2. Go to your **Virtual Machine** -> **Networking** (or "Network settings").
3. Click **Add inbound port rule**.
4. Set **Destination port ranges** to: 80
5. Set **Protocol** to: TCP
6. Set **Action** to: Allow
7. Set **Priority** to: 100 (or any available low number).
8. Click **Add**.
# NOTE: You do NOT need to open 7789 or 8888 publicly. Apache handles them internally.

---

## STEP 2: INSTALLATION (SCRATCH)
# Install Java Development Kit and Apache HTTP Server
sudo apt update && sudo apt upgrade -y
sudo apt install default-jdk apache2 -y

---

## STEP 3: TOMCAT SETUP & ISOLATION
# Download the Tomcat binary
cd /tmp
wget https://archive.apache.org/dist/tomcat/tomcat-11/v11.0.18/bin/apache-tomcat-11.0.18.tar.gz
tar -xvf apache-tomcat-11.0.18.tar.gz

# Create two separate physical directories for isolation
# DO NOT use "ln -s" for the tomcat folders or they will share one config file
sudo mv apache-tomcat-11.0.18 /opt/tomcat1
sudo cp -r /opt/tomcat1 /opt/tomcat2

# Assign ownership to the VM user (e.g., azureuser)
sudo chown -R azureuser:azureuser /opt/tomcat1 /opt/tomcat2

---

## STEP 4: CONFIGURE UNIQUE PORTS (server.xml)
# Instance 1 must use 7789; Instance 2 must use 8888.

# --- Tomcat 1 Configuration ---
# File: /opt/tomcat1/conf/server.xml
# 1. HTTP Connector: <Connector port="7789" protocol="HTTP/1.1" ... />

# --- Tomcat 2 Configuration ---
# File: /opt/tomcat2/conf/server.xml
# 1. Shutdown Port:  <Server port="8006" shutdown="SHUTDOWN">
# 2. HTTP Connector: <Connector port="8888" protocol="HTTP/1.1" ... />
# 3. AJP Connector:  <Connector port="8010" protocol="AJP/1.3" ... />

---

## STEP 5: PROJECT DEPLOYMENT (SYMBOLIC LINKS)
# Ensure your code is linked directly to avoid "404 Not Found" nesting issues.

# 1. Create source folders
mkdir -p /opt/project1 /opt/project2
echo "<h1>Project 1 Works</h1>" > /opt/project1/index.html
echo "<h1>Project 2 Works</h1>" > /opt/project2/index.html

# 2. Link source to Tomcat webapps
# Path: /opt/tomcat[X]/webapps/[URL_NAME]
ln -s /opt/project1 /opt/tomcat1/webapps/project1
ln -s /opt/project2 /opt/tomcat2/webapps/project2

# 3. Fix Ownership of the links (Critical for Tomcat access)
sudo chown -h azureuser:azureuser /opt/tomcat1/webapps/project1
sudo chown -h azureuser:azureuser /opt/tomcat2/webapps/project2

---

## STEP 6: APACHE REVERSE PROXY CONFIGURATION
# This maps the public URL to the internal Tomcat ports.

# 1. Enable Required Apache Modules
sudo a2enmod proxy
sudo a2enmod proxy_http

# 2. Create the Configuration File
sudo nano /etc/apache2/sites-available/my-proxy.conf

# 3. Paste this Configuration:
<VirtualHost *:80>
    ProxyPreserveHost On

    # Route for Project 1 (Port 7789)
    ProxyPass /project1 http://127.0.0.1:7789/project1
    ProxyPassReverse /project1 http://127.0.0.1:7789/project1

    # Route for Project 2 (Port 8888)
    ProxyPass /project2 http://127.0.0.1:8888/project2
    ProxyPassReverse /project2 http://127.0.0.1:8888/project2

    ErrorLog ${APACHE_LOG_DIR}/proxy-error.log
</VirtualHost>

# 4. Enable Proxy and Disable Default Site
sudo a2dissite 000-default.conf
sudo a2ensite my-proxy.conf
sudo systemctl restart apache2

---

## STEP 7: STARTUP AND VERIFICATION
# Start the engines
/opt/tomcat1/bin/startup.sh
/opt/tomcat2/bin/startup.sh

# Internal Verification
curl -I http://localhost:7789/project1/
curl -I http://localhost:8888/project2/

# Public Verification
# Visit: http://<Azure-Public-IP>/project1/
# Visit: http://<Azure-Public-IP>/project2/

---

## STEP 8: TROUBLESHOOTING CHECKLIST (To Avoid Errors)
# 1. 404 Error: Check nesting. Link should point to the folder WITH index.html.
#    Use "ls -l /opt/tomcat1/webapps/project1" to verify the target.
# 2. Cache Issues: If it doesn't update, clear the work dir:
#    rm -rf /opt/tomcat1/work/Catalina/localhost/project1
# 3. Permissions: If 403 Forbidden, ensure "azureuser" has "rx" permissions on /opt folders.
# 4. Firewall: Ensure Port 80 is open in Azure Networking (NSG). 

############################################################
# 🚀 COMPLETE REFERENCE GUIDE
# AZURE DEVOPS + TOMCAT + CI/CD AUTO DEPLOY
# (Everything you did — with errors & fixes)
############################################################

############################################################
# 1️⃣ INSTALL JAVA (REQUIRED FOR TOMCAT)
############################################################

sudo apt update
sudo apt install openjdk-17-jdk -y

# Verify
java -version


############################################################
# 2️⃣ DOWNLOAD & INSTALL TOMCAT 11
############################################################

cd /opt

# Check latest version (optional)
curl -s https://downloads.apache.org/tomcat/tomcat-11/ | grep v11

# Download (USE CORRECT URL)
sudo wget https://downloads.apache.org/tomcat/tomcat-11/v11.0.18/bin/apache-tomcat-11.0.18.tar.gz

# Extract
sudo tar -xvzf apache-tomcat-11.0.18.tar.gz

# Rename
sudo mv apache-tomcat-11.0.18 tomcat11


############################################################
# ❌ ERROR: gzip not in gzip format
# REASON: wrong download URL (HTML downloaded)
# FIX: use correct apache URL above
############################################################


############################################################
# 3️⃣ FIX PERMISSIONS (VERY IMPORTANT)
############################################################

# ERROR YOU FACED:
# Permission denied while entering bin/conf

# FIX:
sudo chown -R azureuser:azureuser /opt/tomcat11


############################################################
# 4️⃣ GIVE EXECUTE PERMISSION
############################################################

cd /opt/tomcat11/bin
chmod +x *.sh


############################################################
# 5️⃣ START TOMCAT
############################################################

./startup.sh

# Check running
ss -tulnp | grep 8080


############################################################
# 6️⃣ AZURE NETWORK RULE
############################################################
# Azure Portal:
# VM → Networking → Add inbound rule
# Port: 8080 (or custom port)
# Protocol: TCP
# Action: Allow


############################################################
# 7️⃣ ACCESS TOMCAT
############################################################

# Browser:
# http://<VM_PUBLIC_IP>:8080


############################################################
# ❌ ERROR: 403 ACCESS DENIED
############################################################
# REASON:
# Tomcat allows localhost only

# FIX:
nano /opt/tomcat11/webapps/<app>/META-INF/context.xml

# Remove or comment:
# <Valve className="org.apache.catalina.valves.RemoteAddrValve"
#        allow="127\.\d+\.\d+\.\d+|::1"/>

# Restart Tomcat after changes


############################################################
# ❌ ERROR: 404 NOT FOUND
############################################################
# REASON:
# Page does not exist (NOT a server issue)


############################################################
# 8️⃣ CHANGE TOMCAT PORT (OPTIONAL)
############################################################

nano /opt/tomcat11/conf/server.xml

# Change:
# <Connector port="8080" ... />

# To:
# <Connector port="7789" ... />

# Restart
cd /opt/tomcat11/bin
./shutdown.sh
sleep 5
./startup.sh

# Verify
ss -tulnp | grep 7789


############################################################
# 9️⃣ INSTALL AZURE DEVOPS AGENT (SELF HOSTED)
############################################################

# Download agent (inside VM)
mkdir ~/myagent
cd ~/myagent

# Extract agent package (example)
tar zxvf vsts-agent-linux-x64-*.tar.gz

# Configure
./config.sh

# Enter:
# Server URL: https://dev.azure.com/<orgname>
# Auth type: PAT
# Agent pool: Default
# Agent name: myagent

# Start agent
./run.sh


############################################################
# ❌ ERROR: VS30063 Unauthorized
############################################################
# REASON:
# Wrong PAT / no permissions

# FIX:
# Create PAT:
# Azure DevOps → Profile → Personal Access Token
# Scope: Code Read & Write


############################################################
# 🔟 CREATE PIPELINE (CI/CD)
############################################################

# File: azure-pipelines.yml

# IMPORTANT:
# Use POOL name NOT agent name

# CORRECT PIPELINE:

# ----------------------------------------------------------
# trigger:
# - main
#
# pool:
#   name: Default
#
# steps:
# - script: |
#     cp index.html /opt/tomcat11/webapps/ROOT/index.html
#   displayName: 'Deploy to Tomcat'
# ----------------------------------------------------------


############################################################
# ❌ ERROR: Could not find pool myagent
############################################################
# REASON:
# myagent = agent name
# pipeline needs POOL name

# FIX:
# pool:
#   name: Default


############################################################
# 1️⃣1️⃣ GIT WORKFLOW (VERY IMPORTANT)
############################################################

# Check branch
git branch

# Check changes
git status

# Commit changes
git add .
git commit -m "updated files"

# Push
git push origin feature


############################################################
# ❌ ERROR: Authentication failed
############################################################
# REASON:
# Azure DevOps blocks password login

# FIX:
# Use PAT as password


############################################################
# 1️⃣2️⃣ BRANCH PROBLEM YOU FACED
############################################################

# Pipeline trigger:
# trigger:
# - main

# BUT you pushed:
# feature branch

# RESULT:
# Pipeline NOT triggered


############################################################
# FIX — MERGE FEATURE → MAIN
############################################################

# If uncommitted changes exist:
git add .
git commit -m "save changes"

# Switch branch
git checkout main

# Pull latest
git pull origin main

# Merge feature
git merge feature

# Push main (IMPORTANT)
git push origin main


############################################################
# 1️⃣3️⃣ PIPELINE RUN CHECK
############################################################

# Azure DevOps:
# Pipelines → Runs → Click latest run


############################################################
# 1️⃣4️⃣ AFTER PIPELINE RUN
############################################################

# No need to restart Tomcat for HTML files

# Just refresh browser:
# http://<VM_PUBLIC_IP>:8080


############################################################
# 1️⃣5️⃣ VERIFY DEPLOYMENT
############################################################

cat /opt/tomcat11/webapps/ROOT/index.html


############################################################
# 1️⃣6️⃣ USEFUL TOMCAT COMMANDS
############################################################

# Start
/opt/tomcat11/bin/startup.sh

# Stop
/opt/tomcat11/bin/shutdown.sh

# Logs
tail -f /opt/tomcat11/logs/catalina.out


############################################################
# 🔥 QUICK ERROR REFERENCE (MOST IMPORTANT)
############################################################

# Permission denied
# -> sudo chown -R azureuser:azureuser /opt/tomcat11

# Pipeline not triggering
# -> check branch (main vs feature)

# Pool not found
# -> use pool name Default

# Git auth failed
# -> use PAT token

# 403 error
# -> remove RemoteAddrValve

# Old content showing
# -> wrong branch or not committed


############################################################
# ⭐ FINAL ARCHITECTURE YOU BUILT
############################################################

# Local System
#     ↓ git push
# Azure DevOps Repo
#     ↓ trigger pipeline
# Self-hosted Agent (Azure VM)
#     ↓ copy index.html
# Tomcat ROOT
#     ↓
# Website LIVE

############################################################
# END — FULL DEVOPS REFERENCE
############################################################



############################################################
# 🚀 APACHE TOMCAT 11 — COMPLETE SETUP GUIDE (AZURE VM)
# (Everything you did — step by step, easy to follow)
############################################################


##############################
# 1️⃣ INSTALL JAVA (REQUIRED)
##############################

sudo apt update
sudo apt install openjdk-17-jdk -y

# Verify Java
java -version


############################################################
# 2️⃣ DOWNLOAD TOMCAT 11
############################################################

cd /opt

# (Optional) check latest version
curl -s https://downloads.apache.org/tomcat/tomcat-11/ | grep v11

# Download Tomcat
sudo wget https://downloads.apache.org/tomcat/tomcat-11/v11.0.18/bin/apache-tomcat-11.0.18.tar.gz


############################################################
# 3️⃣ EXTRACT TOMCAT
############################################################

sudo tar -xvzf apache-tomcat-11.0.18.tar.gz

# Rename for easy path
sudo mv apache-tomcat-11.0.18 tomcat11


############################################################
# 4️⃣ FIX PERMISSIONS  (YOU FACED THIS ERROR)
############################################################
# ERROR:
# Permission denied while cd bin/conf

# REASON:
# Files owned by root because extraction used sudo

# FIX:
sudo chown -R azureuser:azureuser /opt/tomcat11


############################################################
# 5️⃣ GIVE EXECUTE PERMISSION
############################################################

cd /opt/tomcat11/bin
chmod +x *.sh


############################################################
# 6️⃣ START TOMCAT
############################################################

./startup.sh

# Expected:
# Tomcat started


############################################################
# 7️⃣ VERIFY TOMCAT RUNNING
############################################################

ss -tulnp | grep 8080

# Expected:
# LISTEN ... :8080 ... java


############################################################
# 8️⃣ AZURE NETWORK RULE (IMPORTANT)
############################################################
# Azure Portal:
# VM → Networking → Add inbound rule
# Port: 8080
# Protocol: TCP
# Action: Allow


############################################################
# 9️⃣ OPEN TOMCAT IN BROWSER
############################################################

# http://<VM_PUBLIC_IP>:8080


############################################################
# 🔟 COMMON ERRORS YOU FACED
############################################################

# ❌ gzip: not in gzip format
# REASON:
# Wrong download URL (HTML downloaded instead)

# FIX:
# Use correct apache download link


# ❌ Permission denied entering folders
# FIX:
sudo chown -R azureuser:azureuser /opt/tomcat11


# ❌ 403 Access Denied (docs/manager/examples)
# REASON:
# Tomcat allows only localhost by default

# FIX:
nano /opt/tomcat11/webapps/<app>/META-INF/context.xml

# Remove or comment this block:
# <Valve className="org.apache.catalina.valves.RemoteAddrValve"
#        allow="127\.\d+\.\d+\.\d+|::1"/>

# Restart Tomcat after change


############################################################
# 1️⃣1️⃣ CONFIGURE MANAGER USER (OPTIONAL)
############################################################

nano /opt/tomcat11/conf/tomcat-users.xml

# Add before </tomcat-users>

# <role rolename="manager-gui"/>
# <role rolename="admin-gui"/>
#
# <user username="tomcat"
#       password="tomcat123"
#       roles="manager-gui,admin-gui"/>

# Restart Tomcat


############################################################
# 1️⃣2️⃣ CHANGE TOMCAT PORT (8080 → 7789)
############################################################

nano /opt/tomcat11/conf/server.xml

# Find:
# <Connector port="8080" ... />

# Change to:
# <Connector port="7789" ... />

# Restart Tomcat
cd /opt/tomcat11/bin
./shutdown.sh
sleep 5
./startup.sh

# Verify new port
ss -tulnp | grep 7789


############################################################
# 1️⃣3️⃣ OPEN NEW PORT IN AZURE
############################################################
# Azure Portal:
# VM → Networking → Add inbound rule
# Port: 7789
# Protocol: TCP
# Action: Allow


############################################################
# 1️⃣4️⃣ ACCESS TOMCAT
############################################################

# http://<VM_PUBLIC_IP>:7789


############################################################
# 1️⃣5️⃣ USEFUL DAILY COMMANDS
############################################################

# Start Tomcat
/opt/tomcat11/bin/startup.sh

# Stop Tomcat
/opt/tomcat11/bin/shutdown.sh

# Check logs
tail -f /opt/tomcat11/logs/catalina.out


############################################################
# ⭐ FINAL RESULT (WHAT YOU ACHIEVED)
############################################################

# ✔ Installed Java
# ✔ Installed Tomcat 11
# ✔ Fixed permission issues
# ✔ Opened Azure networking ports
# ✔ Handled 403 / 404 errors
# ✔ Changed Tomcat port
# ✔ Accessed Tomcat from browser

############################################################
# END
############################################################




stakeholder role in azure similar to IAM roles in aws
developer role  

kubeadm setup github link:https://github.com/yeshwanthlm/Kubeadm-Installation-Guide


https://aex.dev.azure.com/me?mkt=en-GB


tomcat port number 7789

https://vendor-dev.nrl.co.in/grafana/login need to find the ip of this link

creating different  work type items after work item types defined feature a 
link parent child relation 
have to implement and 
tag management 




* maximum 5 bsic user we can give more than that we have pay or take subscription



repo in azure devops 

username:akhilbm13
password:"<YOUR_AZURE_DEVOPS_PAT_TOKEN>"



agent PAT = "<YOUR_PERSONAL_ACCESS_TOKEN>"


            https://dev.azure.com/akhilbm13/
            <YOUR_AZURE_DEVOPS_PAT_TOKEN>


    grafana , pramotheous , l


    LGTM observability STACK , signoz ,  

    in linux  networking 





SUMMARY OF AZURE DEVOPS BOARDS TUTORIAL VIDEO

========================================================
OVERVIEW
========================================================
This tutorial provides a comprehensive introduction to Azure DevOps Boards and explains 
how to manage projects, create requirements, and track progress throughout the software 
development lifecycle. The presenter shares practical experience and best practices gained 
from real project usage, including work related to Dynamics 365 and Power Platform.

========================================================
CORE CONCEPTS AND FEATURES
========================================================

Purpose:
Azure DevOps Boards helps teams track, manage, and collaborate on work items such as user 
stories, features, tasks, and bugs. It improves transparency and enables better workflow management.

Key Components:

1. Work Items
   - Units of work including epics, features, user stories, tasks, and bugs.

2. Kanban Boards
   - Visual workflow boards used to track progress and optimize delivery.

3. Backlogs
   - Prioritized lists of work items organized by size, team, or business value.

4. Sprints
   - Time-boxed iterations used to plan and deliver selected work items.

5. Dashboards and Reporting
   - Provide project metrics, progress tracking, and overall visibility.

========================================================
STEP-BY-STEP WORKFLOW TO GET STARTED
========================================================

Step 1: Sign Up and Create Organization
- Register on Azure DevOps.
- Create an organization that acts as a container for projects.

Step 2: Create Project
- Create a new project inside the organization.
- Default projects initially include limited work item types.

Step 3: Choose Work Item Process
- Select one process:
  * Basic
  * Agile (recommended)
  * Scrum
  * CMMI
- Agile process enables epics, features, user stories, bugs, and tasks.

Step 4: Create Work Items
- Use backlog or boards to create and organize epics, features, and user stories.

Step 5: Enable Preview Features
- Enable new board features in user settings for improved UI and functionality.

Step 6: Customize Boards
- Modify columns and workflow states such as:
  New → Active → Resolved → Closed
- Add fields like:
  Priority, Business Value, Effort, Ownership.

Step 7: Utilize Templates
- Use templates to prefill fields and speed up work item creation.

========================================================
WORK ITEM HIERARCHY AND MANAGEMENT
========================================================

Hierarchy Structure:

Epics
  -> High-level business initiatives or large work areas.

Features
  -> Functional components under epics.

User Stories
  -> Detailed functional requirements under features.

Tasks and Bugs
  -> Implementation work or issue tracking under user stories.

Capabilities:
- Create work items from backlog or boards.
- Move items through workflow stages.
- Add descriptions, acceptance criteria, comments, and tags.
- Assign ownership and effort estimates.

========================================================
BOARDS AND WORKFLOW CUSTOMIZATION
========================================================

- Boards display work items visually with drag-and-drop state updates.
- Workflow states can be customized, for example:
  New → In Analysis → In Development → In Testing → Done
- Columns can display:
  State, Tags, Priority, Parent Feature, Owner.
- Comments and tagging support collaboration and notifications.

========================================================
ADDITIONAL TOOLS AND TIPS
========================================================

Dashboards:
- Create dashboards with widgets to monitor project health.

Queries:
- Save custom filters based on owner, state, tags, or priority.

Extensions:
- Example: "Azure DevOps Boards Open in Excel"
- Enables bulk editing and importing via Excel.

Preview Features:
- Provides enhanced usability and new board experiences.

Additional advanced topics mentioned:
- Product backlog management
- Custom process configuration
- Kanban swimlanes and tags
- Customizing user story cards and fields

========================================================
KEY INSIGHTS
========================================================

- Choosing the correct work item process (especially Agile) unlocks full functionality.
- Customizing boards and workflow states improves visibility and efficiency.
- Hierarchical work item structure supports organized project tracking.
- Collaboration improves through comments, tagging, and shared dashboards.
- Extensions and integrations increase productivity.

========================================================
CONCLUSION
========================================================

Azure DevOps Boards is a powerful tool for managing software development workflows. 
By creating organizations, selecting the right process, and customizing boards, 
teams can effectively plan, track, and deliver work. Continuous learning and experimentation 
with Azure DevOps features help teams optimize project delivery and collaboration.






-==============================================================================================
------------------------------------------------------------------------------------------------
===============================================================================================


SUMMARY OF AZURE DEVOPS BOARDS TUTORIAL VIDEO (CLEAN + EASY FOLLOW VERSION)

========================================================
OVERVIEW
========================================================

This tutorial introduces Azure DevOps Boards and explains how to manage projects, create requirements, and track progress across the software development lifecycle.

Goal:
- Organize work clearly
- Track progress visually
- Improve collaboration
- Manage Agile workflows efficiently

Real-world context:
Used in enterprise projects including Dynamics 365 and Power Platform.

========================================================
CORE CONCEPTS AND FEATURES
========================================================

Purpose:
Azure DevOps Boards helps teams manage and track work items such as user stories, features, tasks, and bugs.

Main Components:

1) Work Items
   - Units of work:
     Epic → Feature → User Story → Task/Bug

2) Kanban Boards
   - Visual drag-and-drop workflow
   - Shows progress status

3) Backlogs
   - Prioritized list of upcoming work
   - Used for planning

4) Sprints
   - Time-boxed delivery cycles
   - Team commits work for a sprint

5) Dashboards & Reporting
   - Project visibility
   - Metrics and tracking widgets

========================================================
WORK ITEM HIERARCHY (IMPORTANT)
========================================================

Epics
  ↓
Features
  ↓
User Stories
  ↓
Tasks / Bugs

Meaning:

Epic:
- Large business objective.

Feature:
- Functional component inside Epic.

User Story:
- Requirement from user/business perspective.

Task:
- Technical implementation work.

Bug:
- Issue or defect tracking.

========================================================
STEP-BY-STEP WORKFLOW (FOLLOW THIS ORDER)
========================================================

STEP 1 — Sign Up & Create Organization
----------------------------------------
1. Go to Azure DevOps.
2. Create account.
3. Create Organization.

Organization = container holding multiple projects.

--------------------------------------------------------

STEP 2 — Create Project
----------------------------------------
1. Inside organization → New Project.
2. Enter project name.
3. Choose visibility.
4. Create project.

Note:
Default project has limited work item types.

--------------------------------------------------------

STEP 3 — Choose Work Item Process (VERY IMPORTANT)
----------------------------------------

Available processes:
- Basic
- Agile (RECOMMENDED)
- Scrum
- CMMI

Recommended:
Agile → enables Epics, Features, User Stories, Tasks, Bugs.

Why important:
Process selection controls available work item types and workflow.

--------------------------------------------------------

STEP 4 — Create Work Items
----------------------------------------

Go to:
Boards → Backlogs OR Boards → Boards

Create:

- Epic
- Feature
- User Story
- Task / Bug

Tip:
Always create hierarchy in order:
Epic → Feature → Story → Task.

--------------------------------------------------------

STEP 5 — Enable Preview Features
----------------------------------------

1. Click User Settings (top-right).
2. Preview Features.
3. Enable new board experience.

Benefits:
- Better UI
- Improved board usability.

--------------------------------------------------------

STEP 6 — Customize Boards (HIGHLY RECOMMENDED)
----------------------------------------

Modify workflow columns:

Example workflow:

New → Active → Resolved → Closed

OR

New → In Analysis → In Development → In Testing → Done

Add fields:

- Priority
- Business Value
- Effort
- Owner

Why:
Improves visibility and tracking clarity.

--------------------------------------------------------

STEP 7 — Use Templates
----------------------------------------

Templates help:

- Auto-fill common fields
- Faster work item creation
- Standardized process

Example:
User Story template with acceptance criteria pre-filled.

========================================================
BOARDS AND WORKFLOW CUSTOMIZATION
========================================================

Boards provide:

- Drag-and-drop movement.
- Visual progress tracking.
- Collaboration via comments.

Customizable columns:

- State
- Tags
- Priority
- Parent Feature
- Owner

Collaboration features:

- Comments
- Mentions
- Tags
- Notifications

========================================================
DAILY WORKFLOW (PRACTICAL TEAM FLOW)
========================================================

1. Product Owner creates Epics and Features.
2. Team creates User Stories.
3. Developers create Tasks.
4. Work moves across board columns.
5. Progress tracked visually.
6. Completed items move to Done/Closed.

========================================================
ADDITIONAL TOOLS AND TIPS
========================================================

Dashboards:
- Add widgets for visibility.
- Track sprint progress.
- Monitor project health.

Queries:
- Save filters:
  - Owner
  - State
  - Priority
  - Tags

Extensions:
Example:
"Azure DevOps Boards Open in Excel"

Use cases:
- Bulk editing
- Mass import/export.

Preview Features:
- Improved usability.
- Modern board interface.

Advanced topics mentioned:
- Product backlog management
- Custom process configuration
- Kanban swimlanes
- Custom card layouts

========================================================
BEST PRACTICES (REAL PROJECT TIPS)
========================================================

- Choose Agile process unless company mandates others.
- Keep board workflow simple.
- Use hierarchy correctly.
- Keep stories small and clear.
- Use tags consistently.
- Update board daily.
- Use dashboards for team visibility.
- Avoid too many custom states.

========================================================
COMMON BEGINNER MISTAKES
========================================================

❌ Creating tasks without user stories.
✔ Always link tasks to stories.

❌ Too many board columns.
✔ Keep workflow simple.

❌ Not assigning owners.
✔ Assign responsibility clearly.

❌ Ignoring backlog prioritization.
✔ Prioritize by business value.

========================================================
QUICK NAVIGATION CHEAT SHEET
========================================================

Azure DevOps Navigation:

Boards → Backlogs   → Plan work
Boards → Boards     → Track workflow
Boards → Sprints    → Sprint planning
Boards → Queries    → Filter work
Dashboards          → Metrics & reporting

========================================================
KEY INSIGHTS
========================================================

- Choosing the right process unlocks features.
- Board customization improves efficiency.
- Hierarchy enables clean project tracking.
- Comments + tags improve collaboration.
- Dashboards improve transparency.
- Extensions increase productivity.

========================================================
QUICK INTERVIEW REVISION (1-MINUTE)
========================================================

Azure Boards = Work tracking tool.

Hierarchy:
Epic → Feature → User Story → Task/Bug.

Main features:
- Backlogs
- Boards
- Sprints
- Dashboards
- Queries

Purpose:
Plan → Track → Collaborate → Deliver.

========================================================
CONCLUSION
========================================================

Azure DevOps Boards is a powerful project management tool for Agile teams. By creating organizations, selecting the correct process, structuring work items properly, and customizing boards, teams can efficiently plan, track, and deliver software. Consistent usage, clear hierarchy, and visual workflow management significantly improve team collaboration and delivery success.

========================================================
END OF SUMMARY (EASY FOLLOW VERSION)
========================================================

SUMMARY OF YAML PIPELINE CONCEPTS AND DESIGN IN AZURE DEVOPS

========================================================
OVERVIEW
========================================================
A pipeline automates building, testing, and deploying software.  
In Azure DevOps, pipelines can be created using:

1. Classic Editor (UI-based)
2. YAML Pipeline (code-based)

Main structure:
Pipeline → Stage → Job → Step → Task

========================================================
CORE CONCEPTS (SIMPLE)
========================================================

Pipeline:
- Full automation workflow.

Stage:
- Major phase (Build, Test, Deploy).

Job:
- Work unit running on an agent.

Agent:
- Machine that runs jobs (Microsoft-hosted or self-hosted).

Step:
- Small action inside a job.

Task:
- Actual operation (checkout code, build, test, deploy).

========================================================
PIPELINE FEATURES
========================================================

- Runs on Windows, Linux, macOS.
- Supports many programming languages.
- Cloud-based automation.
- Supports CI/CD workflows.

========================================================
TWO WAYS TO CREATE PIPELINES
========================================================

1) Classic Editor (Beginner Friendly)
- No YAML required.
- Select repo → add tasks → run pipeline.
- Good for learning pipeline concepts.

2) YAML Pipeline (Recommended)
- Pipeline defined in a .yml file.
- Stored inside repository.
- Version controlled and reusable.

========================================================
REQUIRED FILE (YAML PIPELINE)
========================================================

File name (common):
azure-pipelines.yml

Location:
- Root of the repository.

Example basic YAML:

--------------------------------------------------------
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- checkout: self

- script: echo "Hello World"
--------------------------------------------------------

What this does:
- Runs when code is pushed to main.
- Uses Ubuntu agent.
- Downloads source code.
- Runs a simple script.

========================================================
PIPELINE CREATION FLOW
========================================================

1. Go to Azure DevOps → Pipelines.
2. Click New Pipeline.
3. Select source repository.
4. Choose Classic or YAML.
5. If YAML → commit azure-pipelines.yml file.
6. Save and Run pipeline.
7. Check logs and status.

========================================================
IMPORTANT BEST PRACTICES
========================================================

- Understand Stage → Job → Step → Task.
- Beginners can start with Classic Editor.
- Move to YAML for automation.
- YAML file must be committed to repo.
- Pipelines can run manually or by trigger.

========================================================
COMMON BEGINNER ERRORS
========================================================

- Wrong YAML indentation.
- YAML file not pushed to repository.
- Wrong agent image.
- Missing trigger section.

========================================================
CONCLUSION
========================================================

Azure DevOps pipelines automate software delivery.  
Classic Editor helps beginners understand concepts, while YAML pipelines provide better control and automation.  

Understanding the pipeline structure and using a simple .yml file is the key to designing pipelines easily.




====================================================================================================
= second video
====================================================================================================

Summary of Designing a First Azure DevOps Pipeline Using YAML

This tutorial explains how to design a basic Azure DevOps pipeline using YAML, 
focusing on YAML syntax, pipeline structure, and creating a working pipeline from scratch.

============================================================
1. Key Concepts of YAML for Azure DevOps Pipelines
============================================================

- YAML (YAML Ain’t Markup Language) is a human-readable configuration language.
- File extensions: .yml or .yaml
- Case-sensitive.
- Uses indentation (spaces only, no tabs).

Rules:
- Lists (arrays): - item
- Key-value pairs: key: value
- Comments: # comment
- Supports nested structures (stages → jobs → steps).
- Wrong spacing or indentation breaks parsing.

Example:

trigger:
- master

pool:
  vmImage: 'ubuntu-latest'

============================================================
2. Azure DevOps Pipeline Structure
============================================================

Main components:

- trigger → defines when pipeline runs
- pool → defines build agent
- stages → logical phases (Build/Test/Deploy)
- jobs → units of work inside stages
- steps → commands/tasks executed

Execution hierarchy:

trigger
  ↓
pool
  ↓
stages
  ↓
jobs
  ↓
steps
  ↓
scripts/tasks

============================================================
3. Pipeline Creation Process (Azure DevOps Portal)
============================================================

1. Go to Azure DevOps → Pipelines.
2. Create New Pipeline.
3. Select repository.
4. Choose YAML.
5. Start with empty file.

Default file name:

azure-pipelines.yml

Place it at repository root.

============================================================
4. Defining Pipeline Components
============================================================

Trigger:

trigger:
- master

Manual run:

trigger: none

Pool:

pool:
  vmImage: 'ubuntu-latest'

Common agents:
- ubuntu-latest
- windows-latest
- macos-latest

Stages:

stages:
- stage: Stage1

Jobs:

jobs:
- job: BuildJob

Steps:

steps:
- script: echo a

============================================================
5. YAML Syntax Tips
============================================================

- Keep space after :
- Use correct indentation.
- Use - for list items.
- Use editor IntelliSense for validation.
- Red underline = syntax issue.

Correct:

pool:
  vmImage: 'ubuntu-latest'

Wrong:

pool:
vmImage:'ubuntu-latest'

============================================================
6. Writing Steps (Commands)
============================================================

Simple step:

steps:
- script: echo "Hello Pipeline"

Multiple commands:

steps:
- script: |
    echo "Start Build"
    pwd
    ls -la

Common commands:

echo "message"
pwd
ls -la
whoami

============================================================
7. Demonstration Summary
============================================================

- Default YAML removed and rewritten manually.
- Editor suggestions used to avoid errors.
- Fixed spacing/indentation issues.
- Pipeline executed successfully.
- YAML can be edited later.
- Emphasis on hierarchy: trigger → pool → stages → jobs → steps.
- First run should use simple echo to validate structure.

============================================================
8. Important Insights & Best Practices
============================================================

- Understand YAML basics before pipeline design.
- Use trigger: none for manual runs.
- Maintain consistent indentation.
- Stages/jobs/steps are nested arrays.
- Use comments for documentation.
- Start small (echo step) then expand.
- Use meaningful names (Build/Test/Deploy).

============================================================
9. YAML Pipeline Elements Summary
============================================================

trigger  → branch trigger/manual run
pool     → agent VM
stages   → pipeline phases
jobs     → work units
steps    → commands/tasks
script   → shell command execution
comments → documentation only

============================================================
10. Practical Pipeline Examples
============================================================

Minimal working pipeline:

trigger: none

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: Stage1
  jobs:
  - job: BuildJob
    steps:
    - script: echo "Pipeline Working"

------------------------------------------------------------

Multi-step example:

trigger: none

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: Build
  jobs:
  - job: BuildJob
    steps:
    - script: echo "Step 1: Start Build"
    - script: echo "Step 2: Run Tests"
    - script: echo "Step 3: Build Completed"

------------------------------------------------------------

Build + Test style example:

trigger:
- master

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: Build
  jobs:
  - job: BuildJob
    steps:
    - script: echo "Build running"

- stage: Test
  jobs:
  - job: TestJob
    steps:
    - script: echo "Tests running"

============================================================
11. Common Beginner Mistakes
============================================================

Wrong:

trigger:none

Correct:

trigger: none

Wrong indentation:

steps:
- script: echo a
  - script: echo b

Correct:

steps:
- script: echo a
- script: echo b

============================================================
12. Editing Pipeline After Creation
============================================================

1. Azure DevOps → Pipelines
2. Open pipeline
3. Click Edit
4. Modify azure-pipelines.yml
5. Save and Run

============================================================
13. Validation Tip
============================================================

- script: echo "Pipeline Working"

If this runs successfully, YAML structure is correct.

============================================================
14. Conclusion
============================================================

This tutorial builds foundational understanding of Azure DevOps YAML pipelines by 
  teaching syntax, hierarchy, and execution flow. Starting with simple scripts and 
  correct structure forms a strong base for building advanced DevOps automation pipelines.








=========================================================================================
video 4
=========================================================================================



Summary of Azure DevOps Pipeline Stages and Jobs

This video explains the concept and practical implementation of pipeline stages and 
jobs within Azure DevOps, focusing on Continuous Integration and Continuous Deployment 
(CI/CD) workflows using YAML pipelines.

============================================================
1. Core Concepts
============================================================

Pipeline:
A workflow that automates building, testing, and deploying software.

Stage:
A major division within a pipeline representing a logical boundary or phase (e.g., build, test, deploy).

Job:
A collection of steps that run sequentially within a stage. Multiple jobs can exist within a stage.

Step:
The smallest unit of work in the pipeline, such as running a script or command.

Implicit Stage and Job:
If no stages or jobs are explicitly defined in YAML, Azure DevOps creates one default stage
 and one job automatically.

Execution hierarchy:

Pipeline
  ↓
Stages
  ↓
Jobs
  ↓
Steps

============================================================
2. Key Insights
============================================================

- Every pipeline must have at least one stage; if none is defined, one implicit stage is created.
- A single stage can contain up to 256 jobs.
- The pool specifies the agent or VM image where the pipeline runs (example: ubuntu-latest).
- Without an explicit stage, the job runs inside an implicit stage.
- Stages are defined as an array under the stages: keyword.
- Each stage requires a valid alphanumeric name (hyphens allowed).
- Spaces or invalid characters in stage names cause errors.
- Each stage must contain at least one job.
- Jobs are defined as arrays within each stage.
- Stages and jobs run sequentially unless dependencies are configured.
- Example demo uses: echo "hello world".

Common errors shown:
- Invalid stage name.
- Stage defined without jobs.
- YAML indentation or structure issues.

============================================================
3. Timeline of Demonstration and Explanations
============================================================

00:00–01:22  Introduction to stages and CI/CD importance.
01:32–02:51  Every pipeline must have at least one stage; max 256 jobs.
02:13–03:37  Implicit stage/job concept.
03:38–06:25  Demo pipeline with implicit stage/job and echo script.
06:27–07:56  Viewing job execution logs in Azure DevOps UI.
07:29–09:13  Syntax for explicit stages and naming rules.
09:30–11:21  Defining jobs under stages; mandatory job rule.
11:26–12:44  Adding display names and improved YAML structure.
12:20–14:30  Running pipeline with two stages sequentially.

============================================================
4. YAML Structure Overview
============================================================

YAML Element   Description
pool           Defines the agent pool or VM image.
stages         Array defining pipeline stages.
stage          Individual stage with unique name.
jobs           Array inside stage containing jobs.
job            Individual job with steps.
steps          Commands/scripts executed inside a job.

============================================================
5. Basic Pipeline (Implicit Stage and Job)
============================================================

If stages are NOT defined, Azure DevOps creates them automatically.

Example:

trigger: none

pool:
  vmImage: 'ubuntu-latest'

steps:
- script: echo "hello world"

Flow:

Pipeline
  → implicit stage
    → implicit job
      → step execution

============================================================
6. Explicit Stage and Job Definition
============================================================

Single stage example:

trigger: none

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: Build
  jobs:
  - job: BuildJob
    steps:
    - script: echo "hello world"

Important:
- stage name must be valid (letters/numbers/hyphen).
- at least one job required.

============================================================
7. Multiple Stages Example (Sequential Execution)
============================================================

trigger: none

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: Build
  displayName: Build Stage
  jobs:
  - job: BuildJob
    steps:
    - script: echo "Running Build"

- stage: Test
  displayName: Test Stage
  jobs:
  - job: TestJob
    steps:
    - script: echo "Running Tests"

Execution order:

Build Stage
   ↓
Test Stage

============================================================
8. Jobs Inside a Stage
============================================================

A stage can contain multiple jobs (max 256).

Example:

stages:
- stage: Build
  jobs:
  - job: Job1
    steps:
    - script: echo "Job 1"

  - job: Job2
    steps:
    - script: echo "Job 2"

By default:
- jobs run sequentially unless dependencies are changed.

============================================================
9. Important Rules and Constraints
============================================================

- Stage names must be alphanumeric (hyphen allowed).
- No spaces or special characters in stage names.
- Every stage must contain at least one job.
- Jobs must contain steps.
- Pool definition is required to choose execution agent.
- Stages run sequentially by default.
- Pipelines without stages use implicit stage + job.

============================================================
10. Common Errors (From Demo)
============================================================

Invalid stage name:

stages:
- stage: Build Stage   # ❌ space not allowed

Correct:

stages:
- stage: Build-Stage   # ✔ valid

------------------------------------------------------------

Stage without jobs (ERROR):

stages:
- stage: Build

Correct:

stages:
- stage: Build
  jobs:
  - job: BuildJob
    steps:
    - script: echo "ok"

------------------------------------------------------------

Wrong indentation:

stages:
- stage: Build
jobs:
- job: Test

Correct indentation:

stages:
- stage: Build
  jobs:
  - job: Test

============================================================
11. Pipeline Execution Flow
============================================================

1. Pipeline starts.
2. Source code checkout.
3. Stage execution begins.
4. Jobs execute inside stage.
5. Steps run sequentially.
6. Logs displayed in Azure DevOps UI.
7. Final build status shown.
8. Cleanup tasks executed.

============================================================
12. Best Practices
============================================================

- Use explicit stages for real projects.
- Keep stage names simple and meaningful (Build/Test/Deploy).
- Start with one stage and expand gradually.
- Use displayName for readability.
- Validate YAML using editor suggestions.
- Keep indentation consistent (2 spaces recommended).
- Use simple echo scripts to verify structure first.

============================================================
13. Quick Reference (Interview Revision)
============================================================

Pipeline  → Full workflow
Stage     → Logical phase
Job       → Unit of execution
Step      → Command/script
Pool      → Agent machine
Implicit  → Auto-created stage/job when missing

============================================================
14. Key Takeaway
============================================================

Defining explicit pipeline stages and jobs in Azure DevOps YAML files is essential 
for organizing complex CI/CD workflows. Proper syntax, valid naming, and at least one 
job per stage are required to prevent errors. Implicit stages and jobs allow simple 
pipelines without explicit definitions, but explicit stages enable structured, multi-phase 
workflows required for real-world DevOps implementations.







==============================================================================================
video-5
===============================================================================================




Summary of Multi-Stage Pipeline Configuration (Azure DevOps / CI-CD YAML)

This tutorial explains how to configure a multi-stage pipeline in a CI/CD system, expanding from
 a single-stage single-job pipeline. The focus is on defining multiple stages, assigning agent pools 
 at stage and job levels, and controlling execution flow across environments.


============================================================
1. Core Concepts
============================================================

Multi-stage Pipeline:
A pipeline containing multiple stages to organize build, test, and deployment workflows.

Stage:
Logical grouping of jobs. Stages execute sequentially by default.

Job:
A unit of work inside a stage. Jobs contain steps and run on agents.

Step:
Smallest execution unit (script or task).

Pool (Agent):
Defines where jobs run (VM image or hosted agent).

Execution hierarchy:

Pipeline
  ↓
Stages
  ↓
Jobs
  ↓
Steps

============================================================
2. Stages vs Jobs
============================================================

Stages:
- High-level phases (Build, Test, UAT, Production).
- Execute one after another.
- Help structure complex pipelines.

Jobs:
- Work units inside stages.
- Can run on specific agents.
- Can override stage settings.

Example structure:

stages:
- stage: Build
  jobs:
  - job: BuildJob

============================================================
3. Pool (Agent) Assignment and Precedence
============================================================

Pool can be assigned at:

1) Stage level
2) Job level

Rules:

- If pool is defined at stage level → all jobs inherit it.
- If pool is defined at job level → it overrides stage pool.
- Job-level pool has higher precedence.

Stage-level pool example:

stages:
- stage: Build
  pool:
    vmImage: 'ubuntu-latest'
  jobs:
  - job: BuildJob
    steps:
    - script: echo "Build"

Job-level override example:

stages:
- stage: Test
  pool:
    vmImage: 'ubuntu-latest'
  jobs:
  - job: WindowsTest
    pool:
      vmImage: 'windows-latest'
    steps:
    - script: echo "Run on Windows"

============================================================
4. Sequential Execution
============================================================

Stages execute in order defined:

Stage A → Stage B → Stage C → Stage D

This allows:

- Build → Test → UAT → Production flow
- Controlled deployments
- Environment-based promotion

============================================================
5. Platform-Specific Agents
============================================================

Pipeline jobs can run on different OS agents:

- ubuntu-latest (Linux)
- windows-latest (Windows)
- macos-latest (Mac)

Example:

Build job → Ubuntu  
Test job → Windows

This enables cross-platform testing and deployment.

============================================================
6. Pipeline Structure Outline (From Tutorial)
============================================================

Stage A:
- Purpose: Build
- Job: Job A
- Pool: Stage-level
- Agent: Ubuntu-latest

Stage B:
- Purpose: Test
- Job: Job B
- Pool: Job-level override
- Agent: Windows hosted agent

Stage C:
- Purpose: UAT
- Job: Job C
- Pool: Stage-level
- Agent: Ubuntu-latest

Stage D:
- Purpose: Production
- Job: Job D
- Pool: Stage-level
- Agent: Ubuntu-latest

============================================================
7. Steps Demonstrated
============================================================

- Define multiple stages using stages:
- Assign pools at stage level.
- Override pools at job level.
- Run jobs sequentially across stages.
- Use different OS agents (Ubuntu + Windows).
- Save YAML and run pipeline.
- Observe execution order and logs.

============================================================
8. YAML Multi-Stage Example (Complete)
============================================================

trigger: none

stages:

- stage: StageA
  displayName: Build Stage
  pool:
    vmImage: 'ubuntu-latest'
  jobs:
  - job: JobA
    steps:
    - script: echo "Running Build on Ubuntu"

- stage: StageB
  displayName: Test Stage
  pool:
    vmImage: 'ubuntu-latest'
  jobs:
  - job: JobB
    pool:
      vmImage: 'windows-latest'
    steps:
    - script: echo "Running Test on Windows"

- stage: StageC
  displayName: UAT Stage
  pool:
    vmImage: 'ubuntu-latest'
  jobs:
  - job: JobC
    steps:
    - script: echo "Running UAT"

- stage: StageD
  displayName: Production Stage
  pool:
    vmImage: 'ubuntu-latest'
  jobs:
  - job: JobD
    steps:
    - script: echo "Deploying to Production"

============================================================
9. Important YAML Rules
============================================================

- stages must be an array.
- Duplicate stages keys cause errors.
- Each stage must contain at least one job.
- Correct indentation is mandatory.
- Stage names should be valid alphanumeric (hyphen allowed).

Wrong:

stages:
- stage: Build Stage   # space may cause issues

Correct:

stages:
- stage: Build-Stage

============================================================
10. Pool Inheritance Example (Concept)
============================================================

Stage pool:

stage: Build
pool: ubuntu

Jobs:

Job1 → ubuntu (inherited)
Job2 → windows (overridden)

Visual:

Stage Pool (Ubuntu)
   ↓
Job1 (Ubuntu inherited)
Job2 (Windows override)

============================================================
11. Execution Flow
============================================================

1. Pipeline starts.
2. Stage A runs.
3. Jobs execute inside stage.
4. Stage B starts after Stage A completes.
5. Continue sequentially until final stage.
6. Logs shown in Azure DevOps UI.
7. Final status displayed.

============================================================
12. Key Insights
============================================================

- Multi-stage pipelines organize complex workflows.
- Stage-level pool reduces duplication.
- Job-level pool gives flexibility.
- Different OS agents can be used in one pipeline.
- Sequential stages support real deployment lifecycles.
- Correct YAML structure prevents errors.

============================================================
13. Common Mistakes
============================================================

Duplicate stages key:

stages:
- stage: Build

stages:
- stage: Test   # ❌ invalid

------------------------------------------------------------

Missing jobs:

- stage: Build   # ❌ error

Correct:

- stage: Build
  jobs:
  - job: BuildJob

------------------------------------------------------------

Wrong indentation:

stage: Build
jobs:
- job: A

Correct:

- stage: Build
  jobs:
  - job: A

============================================================
14. Core Takeaways
============================================================

- Multi-stage pipelines structure CI/CD workflows clearly.
- Stages run sequentially by default.
- Pools can be assigned at stage or job level.
- Job-level pools override stage pools.
- YAML syntax and hierarchy must be correct.
- Different environments can run on different agents.

============================================================
15. Keywords (Quick Revision)
============================================================

Multi-stage pipeline
CI/CD pipeline
YAML configuration
Stage-level pool
Job-level pool
Sequential execution
Agent pool
Ubuntu VM
Windows agent
Microsoft-hosted agent

============================================================
16. Conclusion
============================================================

Multi-stage pipelines allow efficient organization of build, test, and deployment workflows. 
Understanding stage/job hierarchy, pool inheritance, and execution order is essential for 
designing scalable CI/CD automation. Proper YAML structure and pool precedence ensure jobs run 
on the correct environments and pipelines execute reliably.






=======================================================================================================
video-6
=======================================================================================================

================================================================
LGTM STACK – SIMPLE THEORY (EASY UNDERSTANDING)
================================================================

# Observability answers three main questions about a system

# 1. What happened?  → LOGS
# 2. How is the system performing? → METRICS
# 3. How did a request travel across services? → TRACES

# LGTM stack components

# L = Loki   → Stores logs
# G = Grafana → Visualizes logs/metrics/traces
# T = Tempo  → Distributed tracing
# M = Mimir  → Metrics storage

# In PHASE 1 we implement ONLY logging

# Grafana + Loki + Promtail


================================================================
LOGGING FLOW (HOW DATA MOVES)
================================================================

# Apache / Tomcat generate logs
# Promtail reads those logs
# Promtail pushes logs to Loki
# Grafana queries Loki and displays logs


Logs → Promtail → Loki → Grafana


================================================================
YOUR AZURE VM ARCHITECTURE
================================================================

# Everything runs on ONE Azure VM

Azure VM
 ├── Apache Reverse Proxy
 ├── Tomcat Instance 1
 ├── Tomcat Instance 2
 ├── Promtail (Log Collector)
 ├── Loki (Log Storage)
 └── Grafana (Visualization UI)

# Ports used

3000 → Grafana UI
3100 → Loki API


================================================================
THE ULTIMATE LGTM LOGGING GUIDE (PHASE 1)
Target: Single Azure VM | Apache + 2x Tomcat
================================================================


================================================================
1. PREREQUISITES & NETWORKING
================================================================

sudo systemctl start apache2
# Starts Apache reverse proxy so it begins generating logs

sudo /opt/tomcat1/bin/startup.sh
# Starts Tomcat instance 1 so application logs start being written

sudo /opt/tomcat2/bin/startup.sh
# Starts Tomcat instance 2 for multi-instance testing and log generation

# Azure Portal Inbound Rules

# Open port 3000 → Allows browser access to Grafana UI
# Open port 3100 → Allows Grafana and agents to communicate with Loki


================================================================
2. INSTALLATION
================================================================


### A. GRAFANA (The Eyes)

sudo apt-get update
# Updates package list so Ubuntu knows latest available software versions

sudo apt-get install -y apt-transport-https software-properties-common wget
# Installs required tools for downloading packages from HTTPS repositories

wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
# Downloads Grafana's GPG key and stores it so the system trusts Grafana packages

echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
# Adds the official Grafana repository to the system package sources

sudo apt-get update
# Refresh package lists so Ubuntu can see Grafana packages

sudo apt-get install -y grafana
# Installs Grafana server

sudo systemctl enable grafana-server
# Enables Grafana to automatically start when the VM boots

sudo systemctl start grafana-server
# Starts Grafana service immediately


### B. LOKI (The Brain)

sudo mkdir -p /opt/loki
# Creates a directory where Loki binaries and configs will be stored

cd /opt/loki
# Moves into the Loki installation directory

sudo curl -L -O https://github.com/grafana/loki/releases/download/v2.9.3/loki-linux-amd64.zip
# Downloads Loki binary package from Grafana GitHub releases

sudo apt install unzip -y
# Installs unzip utility required to extract downloaded archive

sudo unzip loki-linux-amd64.zip
# Extracts Loki binary from the zip archive

sudo chmod +x loki-linux-amd64
# Gives execute permission so Loki can run as a program


### C. DIRECTORY & PERMISSION FIX

sudo mkdir -p /tmp/loki/chunks
# Creates directory where Loki stores log chunks

sudo mkdir -p /tmp/loki/rules
# Creates directory used for Loki rule storage

sudo chmod -R 777 /tmp/loki
# Gives Loki full read/write permissions so it does not crash due to permission errors


### D. PROMTAIL (The Hands)

sudo curl -L -O https://github.com/grafana/loki/releases/download/v2.9.3/promtail-linux-amd64.zip
# Downloads Promtail log agent from Grafana GitHub

sudo unzip promtail-linux-amd64.zip
# Extracts Promtail binary

sudo chmod +x promtail-linux-amd64
# Gives execute permission to Promtail binary

sudo mv promtail-linux-amd64 /usr/local/bin/promtail
# Moves Promtail binary into system PATH so it can be executed globally


================================================================
3. CONFIGURATION FILES
================================================================


### CREATE LOKI CONFIG

sudo mkdir -p /etc/loki
# Creates directory where Loki configuration files will be stored

sudo tee /etc/loki/loki-config.yaml <<EOF
# Creates Loki configuration file defining storage, schema, and server settings

auth_enabled: false
server:
  http_listen_port: 3100

common:
  instance_addr: 127.0.0.1
  path_prefix: /tmp/loki

  storage:
    filesystem:
      chunks_directory: /tmp/loki/chunks
      rules_directory: /tmp/loki/rules

  replication_factor: 1

  ring:
    kvstore:
      store: inmemory

schema_config:
  configs:
    - from: 2020-10-24
      store: boltdb-shipper
      object_store: filesystem
      schema: v11
      index:
        prefix: index_
        period: 24h
EOF


### CREATE PROMTAIL CONFIG

sudo tee /etc/loki/promtail-config.yaml <<EOF
# Creates Promtail configuration telling it which log files to monitor

server:
  http_listen_port: 9080

positions:
  filename: /tmp/positions.yaml

clients:
  - url: http://localhost:3100/loki/api/v1/push

scrape_configs:

- job_name: apache
  static_configs:
  - targets: [localhost]
    labels:
      job: apache
      __path__: /var/log/apache2/*.log

- job_name: tomcat_instances
  static_configs:
  - targets: [localhost]
    labels:
      job: tomcat
      __path__: /opt/tomcat*/logs/*.out
EOF


================================================================
4. EXECUTION & VERIFICATION
================================================================

sudo /opt/loki/loki-linux-amd64 -config.file=/etc/loki/loki-config.yaml
# Starts Loki log storage service using the created configuration

sudo /usr/local/bin/promtail -config.file=/etc/loki/promtail-config.yaml
# Starts Promtail agent which begins reading logs and sending them to Loki


================================================================
HEALTH CHECKS
================================================================

curl http://localhost:3100/ready
# Checks if Loki service is running and ready to receive logs


================================================================
GRAFANA UI
================================================================

# Open browser

http://<VM-IP>:3000

# Default login

admin
admin


================================================================
ADD LOKI DATA SOURCE
================================================================

# Navigate inside Grafana

Connections → Data Sources → Loki

# Configure

URL → http://localhost:3100

# Click

Save & Test


================================================================
VIEW LOGS
================================================================

Explore → Select Loki

Label Browser → job

Choose

apache
or
tomcat

# You will now see logs from Apache and Tomcat in Grafana








================================================================
5. VM RESTART / SERVICE MANAGEMENT
================================================================

# When the Azure VM stops or restarts, some services must be started again.
# Grafana starts automatically because we enabled the system service earlier.
# Loki and Promtail were started manually, so they must be started again.


----------------------------------------------------------------
CHECK IF GRAFANA IS RUNNING
----------------------------------------------------------------

sudo systemctl status grafana-server
# Checks Grafana service status to confirm if it started automatically after VM reboot


----------------------------------------------------------------
START GRAFANA MANUALLY (if needed)
----------------------------------------------------------------

sudo systemctl start grafana-server
# Starts Grafana service if it did not start automatically


----------------------------------------------------------------
START LOKI AFTER VM REBOOT
----------------------------------------------------------------

sudo /opt/loki/loki-linux-amd64 -config.file=/etc/loki/loki-config.yaml
# Starts Loki log database service using the previously created configuration file


----------------------------------------------------------------
START PROMTAIL AFTER VM REBOOT
----------------------------------------------------------------

sudo /usr/local/bin/promtail -config.file=/etc/loki/promtail-config.yaml
# Starts Promtail log agent so it resumes reading logs and pushing them to Loki


----------------------------------------------------------------
VERIFY LOKI AFTER RESTART
----------------------------------------------------------------

curl http://localhost:3100/ready
# Checks if Loki is running and ready to receive logs


----------------------------------------------------------------
STOP SERVICES SAFELY
----------------------------------------------------------------

pkill loki-linux-amd64
# Stops the Loki process if it is running

pkill promtail
# Stops the Promtail agent


----------------------------------------------------------------
STOP GRAFANA SERVICE
----------------------------------------------------------------

sudo systemctl stop grafana-server
# Stops Grafana service safely


----------------------------------------------------------------
RESTART ALL SERVICES MANUALLY
----------------------------------------------------------------

sudo systemctl restart grafana-server
# Restarts Grafana UI service

sudo /opt/loki/loki-linux-amd64 -config.file=/etc/loki/loki-config.yaml
# Starts Loki again

sudo /usr/local/bin/promtail -config.file=/etc/loki/promtail-config.yaml
# Starts Promtail again


================================================================
QUICK START AFTER VM REBOOT
================================================================

# If VM restarts, run these commands in order

sudo systemctl start grafana-server
sudo /opt/loki/loki-linux-amd64 -config.file=/etc/loki/loki-config.yaml
sudo /usr/local/bin/promtail -config.file=/etc/loki/promtail-config.yaml


================================================================
ACCESS DASHBOARD AGAIN
================================================================

Grafana UI

http://<VM-IP>:3000

Login

admin
admin




- Cloud platforms: AWS (EC2, S3, RDS, VPC), Azure (VMs, VNet, Azure SQL)
- CI/CD & automation: Azure DevOps (Pipelines, Boards, Repos), Jenkins, GitHub Actions
- Containers & orchestration: Docker, Kubernetes
- Infrastructure as code: Terraform, Shell Scripting (Bash), YAML
- Middleware & web servers: Apache HTTP Server, Apache Tomcat, Reverse Proxy
- Databases & security: PostgreSQL, UFW, Security Groups, IAM/ RBAC
- Version control & logging: Git, LGTM Stack (Loki, Grafana, Tempo, Mimir)
- Operating systems: Linux (Ubuntu/ RHEL), System Hardening, Ulimit Tuning

```
