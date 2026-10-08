# 📘 LGTM (Loki, Grafana, Tempo, Mimir) Observability Stack Guide

> *Comprehensive Azure DevOps engineering documentation and hands-on guide.*

---

```text
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
