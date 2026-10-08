# 📘 Azure DevOps Self-Hosted Agent Pool Setup Guide

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
```
