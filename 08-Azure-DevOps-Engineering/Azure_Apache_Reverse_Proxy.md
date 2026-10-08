# 📘 Azure VM Apache Reverse Proxy Setup

> *Comprehensive Azure DevOps engineering documentation and hands-on guide.*

---

```text
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
```
