# 📖 NEXUS SETUP AND INTEGRATED TO JENKINS
> *Converted from `NEXUS SETUP AND INTEGRATED TO JENKINS.pdf` for high-readability on GitHub.*

---
## Page 1

NEXUS SETUP AND INTEGRATED 
TO JENKINS 
STEP-1: LAUNCH INSTANCE WITH T2.MEDIUM AND 8081 PORT AND 20 GB OF EBS VOLUME 
STEP-2: INSTALL JAVA AS THE NEXUS DEPENDENCY  
-→ (yum install java-17-amazon-corretto -y) 
STEP-3: CREATE A FOLDER (mkdir /app) 
SETP-4: GO TO FOLDER (cd /app) 
STEP-5: DOWNLOAD THE NEUXS 
 wget -O nexus.tar.gz https://download.sonatype.com/nexus/3/latest-unix.tar.gz 
STEP-6: UNTAR THE FILE (tar -zxvf nexus.tar.gz) 
STEP-7: RENAME THE NEXUS FILE (mv nexus-* nexus) 
STEP-8: ADD NEXUS USER (useradd nexus) 
STEP-9: CHANGE THE OWNERS OF THE FILES  
    (chown -R nexus:nexus file_names) 
 STEP-10: CHANGE nexus.rc file 
    (vim /app/nexus/bin/nexus.rc)  
   run_as_user="nexus"      <---- inside nexus.rc 
STEP-11: NOW START NEXUS SERVICE (./nexus/bin/nexus start )  
  AND SEE STATUS ( ./nexus/bin/nexus status )         
 -→ wait for 2 minutes and copy the public-ip of your nexus server and access it with 8081 port 
CLICK ON SIGN-IN

## Page 2

CLICK ON SIGN-IN 
IT WILL ASKS THE USER NAME & PASSWORD  
USERNAME: admin 
PASSWORD: cat /app/sonatype-work/nexus3/admin.password use this command in our server to get the 
password  and paste it into our nexus dashboard

## Page 3

NOW GO TO SERVER ADMINISTRATION AND CONFIGURATION 
 
 
SELECT REPOSITORIES  
 
SELECT CREATE-REPOSITORY

## Page 4

SELECT MAVEN2(HOSTED) 
 
GIVE REPOSITORY NAME AS myapp-releases and click on create repositories

## Page 5

now you can see our repository created in dashboard 
NOW GO TO JENKINS AND INSTALL PLUGIN "nexus artifactory uploader" 
ADD CREDENTIALS :  
and add description as nexus credentials 
CLICK ON TEST CONNECTION, THEN YOU WILL SEE THE MESSAGE 
NOW GO AND CREATE A JOB 
GIT: URL OF OUR PROJECT 
 
 
ADD BUILD STEP: invoke top-level maven targets

## Page 6

ADD BUILD STEP: Nexus artifact uploader

## Page 7

NOW GO TO POST BUILD ACTIONS: deploy war/ear to container

## Page 8

NOW SAVE AND BUILD THE JOB IF THE BUILD GETS SUCCESS: then we 
can see that war files are stored in nexus repository 
============================================================================================== 
Or or or or or or or or or or or or or or or 
============================================================================================== 
Install nexus platform plugin in jenkins  
Go to jenkins —> configuration system —> nexus 
Display name: nexus 
Server-id: nexus-repo 
Server url: public ip of nexus:8081 
Credentials: **** 
Test connection 
Go to job: 
Configure —> 
Add a build step: Nexus Repository Manager Publisher 
Nexus instance: auto update Nexus-repo: 
sample-releases packages:  
Group: search in pom.xlm 
Artifact id: search in pom.xlm 
Version: search in pom.xlm 
Package: war

## Page 9

Artifact: 
File path: target/myweb-8.2.5.war 
Extension: .war

