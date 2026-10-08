# 📘 Azure Application Deployment & Configuration

> *Comprehensive Azure DevOps engineering documentation and hands-on guide.*

---

```text
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
```
