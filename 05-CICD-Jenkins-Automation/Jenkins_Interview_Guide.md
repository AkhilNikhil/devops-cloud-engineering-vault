# 📖 Jenkins Interview Guide
> *Converted from `Jenkins Interview Guide.pdf` for high-readability on GitHub.*

---
## Page 1

Complete Jenkins Interview Guide with Tomcat and Nexus
1. Basics of Jenkins
Q1. What is Jenkins?  - Jenkins is an open-source automation server used for Continuous Integration (CI)
and Continuous Deployment (CD) to automate builds, testing, and deployment.
Q2.  Why  use  Jenkins? -  Automates  repetitive  tasks  -  Integrates  with  tools  like  Git,  Maven,  Docker ,
Kubernetes, Tomcat, and Nexus - Supports pipelines and workflow automation - Open-source and highly
extensible via plugins
Q3. Jenkins Architecture - Master: Controls tasks, schedules jobs, manages slaves, stores build info - Slave
(Agent): Executes jobs assigned by master - Plugins: Extend Jenkins functionality
Q4. Difference between Jenkins and other CI tools  - Jenkins is open-source, highly extensible, supports
custom pipelines, whereas other CI tools may be paid or cloud-specific with limited plugins
2. Jenkins Installation & Setup
Steps: 1. Install Java (Jenkins requires Java 8+) 
sudo apt update
sudo apt install openjdk-11-jdk
java -version
2. Install Jenkins 
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/
sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins
3. Start Jenkins 
sudo systemctl start jenkins
sudo systemctl enable jenkins
4. Access Jenkins: http://localhost:8080  5. Use initial admin password 
1

## Page 2

sudo cat /var/lib/jenkins/secrets/initialAdminPassword
6. Install suggested plugins and create admin user
3. Jenkins Jobs & Pipelines
Q5. What is a Jenkins Job? - A task Jenkins executes (build, test, deploy, or pipeline execution)
Q6. Types of Jenkins Jobs:  - Freestyle Project: Simple build task - Pipeline: Complex workflow automation
using Jenkinsfile - Multibranch Pipeline: Automatically detects branches in Git - Folder: Organize jobs
4. Jenkins Pipelines
Q7. What is a Jenkins Pipeline? - Defines workflow for build, test, and deploy using code (Jenkinsfile)
Declarative Pipeline Syntax:
pipeline {
agent any
stages {
stage('Build') { steps { echo 'Building...' } }
stage('Test') { steps { echo 'Testing...' } }
stage('Deploy') { steps { echo 'Deploying...' } }
}
}
5. Jenkins Integration with Git, Maven, Tomcat,
and Nexus
Git Integration: 1. Install Git plugin 2. Create a new Freestyle project 3. Under Source Code Management,
choose Git and provide repo URL 4. Add Build Triggers (Poll SCM or webhook for GitHub) 5. Add build steps
(e.g., mvn clean install )
Maven Integration: - Install Maven plugin - Configure Maven tool in Jenkins - Use Maven build steps in
Freestyle or Pipeline
2

## Page 3

Tomcat Deployment: 1. Install Deploy to Container Plugin 2. Add Post-build action → Deploy war/ear to
container 3. Configure Tomcat URL, credentials, and target path 4. Jenkins automatically deploys WAR file
to Tomcat after build
Nexus Integration:  1. Install  Nexus Artifact Uploader Plugin  2. Add build step to upload artifacts to
Nexus repository 3. Configure Nexus URL, repository, and credentials 4. Artifacts like JAR/WAR files are
pushed to Nexus automatically
6. Build Triggers
Poll SCM: H/5 * * * *  (every 5 minutes)
Build after other projects
GitHub/GitLab webhooks
7. Jenkins Plugins
Git Plugin → integrate Git repositories
Pipeline Plugin → pipelines as code
Maven Integration Plugin → build Maven projects
Deploy to Container Plugin → deploy to Tomcat
Nexus Artifact Uploader Plugin → push artifacts to Nexus
Slack Notification Plugin → notifications
Docker Pipeline Plugin → build/deploy Docker images
8. Jenkins Configuration as Code
Define Jenkins settings in Jenkinsfile or YAML
Enables versioning and reproducibility
9. Jenkinsfile Example (Maven + Git + Tomcat +
Nexus)
pipeline {
agent any
tools { maven 'Maven3' }
stages {
stage('Checkout') { steps { git url: 'https://github.com/user/
• 
• 
• 
• 
• 
• 
• 
• 
• 
• 
• 
• 
3

## Page 4

repo.git', branch: 'main' } }
stage('Build') { steps { sh 'mvn clean install' } }
stage('Test') { steps { sh 'mvn test' } }
stage('Deploy to Tomcat') {
steps { deploy adapters: [tomcat9(credentialsId: 'tomcat-creds',
url: 'http://tomcat-server:8080')], contextPath: '/', war: '**/*.war' }
}
stage('Upload to Nexus') {
steps { nexusArtifactUploader artifacts: [[artifactId: 'myapp',
classifier: '', file: 'target/myapp.war', type: 'war']], credentialsId: 'nexus-
creds', groupId: 'com.example', nexusUrl: 'http://nexus-server:8081',
nexusVersion: 'nexus3', protocol: 'http', repository: 'releases' }
}
}
}
10. Jenkins CLI Commands
Command Description
java -jar jenkins-cli.jar -s http://localhost:8080 build 
jobname Trigger build
java -jar jenkins-cli.jar -s http://localhost:8080 list-jobs List all jobs
java -jar jenkins-cli.jar -s http://localhost:8080 get-job 
jobname Get job config
java -jar jenkins-cli.jar -s http://localhost:8080 delete-job 
jobname Delete a job
java -jar jenkins-cli.jar -s http://localhost:8080 create-job 
jobname < config.xml
Create job from
config
11. Common Jenkins Interview Questions &
Answers
Q1. What is Jenkins and why do we use it? - Open-source automation server for CI/CD to automate builds,
tests, deployments, and integrate with tools like Maven, Tomcat, and Nexus.
Q2. Types of Jenkins Jobs? - Freestyle, Pipeline, Multibranch Pipeline, Folder
4

## Page 5

Q3. Difference between Freestyle and Pipeline job?  - Freestyle: GUI-based task, limited automation -
Pipeline: Code-defined workflow, supports complex automation
Q4. What is a Jenkinsfile? - Script defining pipeline stages and steps
Q5. Declarative vs Scripted Pipeline?  - Declarative: Easy to read, structured, with pipeline {}  block -
Scripted: Flexible Groovy-based scripting, more control
Q6. Trigger Jenkins build from GitHub push? - Configure GitHub webhook → Build triggers in Jenkins job
Q7. Explain Jenkins architecture. - Master controls jobs, slaves execute jobs, plugins extend functionality
Q8.  Integrate  Jenkins  with  Maven,  Tomcat,  Nexus? -  Use  respective  plugins  and  configure  build/
deployment steps in Pipeline or Freestyle job
Q9. Schedule periodic builds? - Poll SCM ( H/5 * * * * ) or Build periodically  option
Q10. What is Jenkins plugin and how to install it?  - Extends Jenkins functionality; install via Manage
Jenkins → Manage Plugins
Q11. Difference between  mvn install  and Jenkins pipeline build?  -  mvn install  → local build;
Jenkins  pipeline  build  → automated  workflow  including  stages,  builds,  tests,  deployment,  and  artifact
management
Q12.  How  to  handle  credentials  securely  in  Jenkins? -  Use  Jenkins  Credentials  plugin  for  secrets,
passwords, and tokens
Q13. How to deploy artifacts to Tomcat using Jenkins?  - Use Deploy to Container plugin, configure
Tomcat URL, credentials, and WAR file
Q14. How to upload artifacts to Nexus from Jenkins?  - Use Nexus Artifact Uploader plugin, configure
Nexus URL, repository, and credentials
This guide covers  Jenkins basics, architecture, installation, jobs, pipelines, plugins, CLI commands,
Tomcat deployment, Nexus integration, and common interview questions with answers.
5

