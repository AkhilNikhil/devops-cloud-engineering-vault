# 📖 Maven Interview Guide
> *Converted from `Maven Interview Guide.pdf` for high-readability on GitHub.*

---
## Page 1

Complete Maven Interview Guide
1. What is Maven?
Apache Maven is a build automation and project management tool primarily for Java projects. It
helps manage dependencies, builds, documentation, and reporting.
2. Why use Maven?
Simplifies the build process
Dependency management
Standard project structure
Integration with CI/CD tools
3. Difference between Maven and Ant
Feature Maven Ant
Build file pom.xml build.xml
Dependency management Yes No
Convention over configuration Yes No
Standard directory structure Yes Optional
4. What is a POM?
Project Object Model ( pom.xml ) contains project configuration, dependencies, plugins, and build
info.
5. Maven Repository
Stores project dependencies
Local: ~/.m2/repository
Central: https://repo.maven.apache.org/maven2
Remote/private repositories
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
1

## Page 2

6. Maven Project Structure
project
│-- src
│   │-- main
│   │   │-- java
│   │   │-- resources
│   │-- test
│       │-- java
│       │-- resources
│-- pom.xml
7. Maven Lifecycle
Default lifecycle: - validate → compile → test → package → verify → install → deploy
Clean lifecycle: - pre-clean → clean → post-clean
Site lifecycle: - pre-site → site → post-site → site-deploy
8. Maven Commands
Command Description
mvn compile Compile source code
mvn clean Remove target folder
mvn test Run unit tests
mvn package Package code (jar/war)
mvn install Install to local repo
mvn deploy Deploy to remote repo
mvn dependency:tree Show dependency tree
mvn archetype:generate Create new project
mvn site Generate documentation
mvn validate Validate project structure
2

## Page 3

9. Maven Dependencies
Declared in pom.xml : 
<dependencies>
<dependency>
<groupId>junit</groupId>
<artifactId>junit</artifactId>
<version>4.13.2</version>
<scope>test</scope>
</dependency>
</dependencies>
Scopes:
compile → all classpaths
test → only for testing
provided → runtime provided by container
runtime → only at runtime
10. Maven Plugins
Plugins add functionality to Maven, e.g., compiling, testing, packaging. 
<build>
<plugins>
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-compiler-plugin</artifactId>
<version>3.8.1</version>
<configuration>
<source>1.8</source>
<target>1.8</target>
</configuration>
</plugin>
</plugins>
</build>
Common plugins: maven-compiler-plugin , maven-surefire-plugin , maven-jar-plugin ,
maven-deploy-plugin
11. How Maven Works
Reads pom.xml
• 
• 
• 
• 
• 
• 
• 
• 
1. 
3

## Page 4

Resolves dependencies from local/remote repo
Executes build lifecycle phases (compile, test, package)
Generates artifact in target/
Optionally installs/deploys artifact
12. Steps to Build Maven Project
Install Maven: mvn -v
Create project: 
mvn archetype:generate -DgroupId=com.example -DartifactId=myapp -
DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
Navigate to project folder: cd myapp
Compile: mvn compile
Run tests: mvn test
Package: mvn package
Install locally: mvn install
Deploy remotely: mvn deploy
13. Best Practices
Follow convention over configuration
Keep dependencies updated
Use parent POMs for multi-module projects
Use proper dependency scopes
Commit pom.xml  but ignore ~/.m2/repository
14. Common Maven Interview Questions &
Answers
Q1. Explain Maven lifecycle. - Validate → compile → test → package → verify → install → deploy
Q2. Difference between  mvn install  and  mvn deploy . -  install  → adds artifact to local repo;
deploy  → uploads artifact to remote repository
Q3. What is pom.xml  and its structure? - XML file with project info, dependencies, plugins, build info.
Q4.  How  Maven  resolves  dependencies? -  First  checks  local  repo,  then  central/remote  repositories,
downloads if not present locally.
Q5. Explain Maven scopes. - compile, test, provided, runtime (as explained above)
2. 
3. 
4. 
5. 
1. 
2. 
3. 
4. 
5. 
6. 
7. 
8. 
• 
• 
• 
• 
• 
4

## Page 5

Q6. Difference between Maven and Gradle/Ant.  - Maven uses XML POM, convention over configuration,
automatic dependency management; Ant requires manual handling.
Q7. How to add an external jar dependency? - Declare in pom.xml  inside <dependencies> .
Q8.  What  is  a  Maven  plugin?  Name  common  plugins. -  Extends  Maven  functionality;  e.g.,  maven-
compiler-plugin , maven-surefire-plugin .
Q9. Difference between mvn clean install  and mvn package . - clean install  → cleans target
folder , builds, tests, and installs to local repo; package  → just builds jar/war in target folder .
Q10.  How  to  generate  a  Maven  project  using  archetypes?  -  mvn archetype:generate -
DgroupId=com.example  -DartifactId=myapp  -DarchetypeArtifactId=maven-archetype-
quickstart -DinteractiveMode=false
This guide covers  Maven fundamentals, working, commands, lifecycle, dependencies, plugins, and
common interview questions with answers.
5

