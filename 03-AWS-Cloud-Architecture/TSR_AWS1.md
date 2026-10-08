# 📝 TSR AWS1

```text
AWS :
-----

DRAWBACKS OF TRADITIONAL SEREVRS...

> HIGH INVESTMENT
> HIGH MAINTAINENCE
> NO DISATER MANAGEMENT
> NO HIGH ASSESSIBILITY
> ON DEMAND SERVICES
> RESOURCE MANGEMENT
> SCALABILITY


## CLOUD COMPUTING : ACCESSING ALL THE COMPUTING SERVICES OVER THE INTERNET VIRTUALY IS CALLED CLOUD COMPUTING.

### ADVANTAGES OF CLOUD COMPUTING :

** 	> PAY AS YOU GO**
** 	> NO MAINTAINENCE**
** 	> DISASTER MANAGEMENT**
** 	> HIGH AVAILABILITY**
** 	> ON DEMAND SERVICES**
** 	> INCREASE IN RESOURCES**
** 	> HIGH SCALABILITY**


TYPES OF CLOUD COMPUTING :
=========================

> DEPLOYMENT MODEL



** 	+ PUBLIC CLOUD**
** 	+ PRIVATE CLOUD**
** 	+ HYBRID CLOUD**

> SERVICE MODEL

** 	+ IAAS**
** 	+ PAAS**
** 	+ SAAS**

AMAZON WEB SERVICES (AWS) :: 2006(-OFFICIAL RELEASE-)
============================

COST EFFECTIVE
USER FRIENDLY
MORE THEN 200 SERVICES
ON DEMAND SERVICE
HIGH AVAILABILITY


SERVICES PROVIDED BY AWS :
==========================

COMPUTE SERVICE
STORAGE SERVICE
NETWORK SERVICE
SECURITY
DATABASE SERVICE
MACHINE LEARNING
BIGDATA AND ANALYSIS
ACCELERATED COMPUTING


EC2 ::
---
CONNECT TO WINDOWS -

SESSION MANAGER
RDP CLIENT (REMOTE DESKTOP FILE)
EC2 SERIAL CONSOLE

AMI(AMAZON MACHINE IMAGE)
---

DIFFERENCE BETWEEN AMI AND TEMPLATE:

AMI CONTAIN SOFTWARE CONFIGURATION WHILE TEMPLATE CONTAIN HARDWARE CONFIGURATION.

EBS(ELASTIC BLOCK STORE)
---
EXTRA STORAGE SPACES PROVIDE TO OUR INSTACE ARE CALLED 'VOLUMES' IT CAN BE INCREASE BASED ON USER REQUIREMENT.
8 GB FOR DEFAULT LINUX AND 30 GB FOR WINDOWS .
HELPS IN BACKUP
VOLUMES ARE " AVAILABILITY ZONE SPECIFIC ". IT CAN BE ATTACHABLE AND DETACHABLE TO ANY INSTANCE
|| imp ||1072 MB = 1 Gib and 1024mb = 1GB
one instace can be connected to multiple volume but one volume can be attached to only one instance at a time it standard EBS volumes.
specialized EBS Multi-Attach feature for io1 and io2 volumes, which explicitly allows a single volume to be attached to multiple instances concurrently.
1 volume can be expand up to 16384 Gib.
root volume can be expanded but canbe take 6 hours to update.1-TiB volume can take around 6 hours to modify, but this is a guideline, not a strict rule.

Attach a volume to window ::
---
VOLUME ARE AVAILABITY ZONE SPECEFIC.
after attach >  go to server manager > wait for the file and storage serveice > disk > select volume > initialize >

BACKUPS FOR VOLUME :: SNAPSHOT
------------------------
THREE TYPES > OWNED BY ME > PUBLIC > PRIVATE
SNAPSOT IS USED TO STORE VOLUME .
ONE SNAPSHOT IS USED TO STORE ONE VOLUME AT A TIME.
SNAPSHOT CAN BE DONE FROM VOLUME , ALSO FROM A INSTANCE , IF THAT INSTANCE HAVE 'N' NO OF VOLUME THAT 'N' NO OF SNAPSHOT WILL BE CREATED.



STORAGE SERVICE
[-------------------------------]

TYPES ::
**+ OBJECT BASED STORAGE	--> S3 ( SIMPLE STORAGE SERVICE )**
\*\*+ BLOCK BASED STORAGE		--> EBS, INSTANCE STORE ( APPART FROM 'EBS' THE SMALL DEFAULT STORAGE ADDED WITH INSTACE )\*\*

	\*\*+ FILE BASED STORAGE		--> EFS ( ELASTIC FILE SYSTEM )\*\*

	\*\*+ ARCHIVE BASED STORAGE\*\*

































SIMPLE STORAGE SERVICE :: ( S3 )
[------------------------------------------]      [---------]

PROVIDES UNLIMITED STORAGE
USED TO TRANSFER ONPREMISE DATA DIRECT TO CLOUD
USED FOR STATIC HOSTING
USED FOR  BIG DATA ANALYSIS EX : BIGSTREAM, BIGDATA, DATA WAREHOUSE
MEDIA HOSTING EX : IMAGES , VIDEOS ETC CAN BE ACCESS THROUGH 'S3 URL'
EACH OBJECT MAX SIZE IS 5 TB.
STORAGE SPACE RELATED TO S3 IS CALLED AS BUCKET . OBJECT/DATA CAN BE STORE IN S3 ONLY USING BUCKET.
S3 IS GOLOBAL SO ITS BUCKET NAME SHOULD BE UNIQUE GLOBALLY.
IT CAN BE USED WITH INSTACE AND WITHOUT INSTACE ALSO . ACT LIKE SERVERLESS.


TYPES / CLASES OF S3 ::
======| |============

S3 STANDARD
S3 GLACIER 			--> CHEAPEST IN S3
S3 GLACIER DEEP ARCHIEVE	--> TO STORE ARCHIEVE FILES
S3 ONE ZONE -IA		--> THIS ONE IS AVAILABILITY ZONE SPECEFIC
S3 SNOWBALL			--> USED FOR ONPREMISE DATA TRANSFER


STATIC WEB HOSTING :
------ ---- ------
UPLOAD FILE TO YUOR BUCKET >> ALL FILES SHOULD BE ON A SAME BUCKET
GO TO  PROPERTIES >> STATIC WEB HOSTING >>
PERMISION >> ALLOW PUBLIC ACCESS
BUCKET POLICY >> S3 BUCKET POLICY >> PRINCIPAL ( * ) DEFAULT >> ACTION ( GET OBJECT ) >>  ARN/* >> ADD STATEMENT >> GENERATE
COPY/PASTE >> BUCKET POLICY

ROLES AE USE TO GIVE PERMISION FROM SERVICE TO SERVICE

NOTE ** ||
------------
REPLICATION RULE :: REPLICATION OF FILE IS STORE IN A DEFINED STORAGE CLASS AND THE ORIGINAL FILE DELETED FROM THE STANDARD.
LIFE CYCLE RULE :: IT DOESNOT COPY THE FILE BUT DELETE THE FILE AFTER THE SCHEDULE TIME PERIOD.


CROSS REGION REPLICATION ON S3 ::
-----	-----	---------------

COPYING OR CREATING THE REPLICATION OF THE OBJECT OF A BUCKET IN A REGION TO ANOTHER BUCKET OF ANOTHER REGION IS CALLED CROSS REGION REPLICATION.




VPC(VIRTUAL PRIVATE CLOUD)::
----------| |-------------

CREATING A PRIVATE WORKSPACE OVER A PUBLIC CLOUD IS CALLED VIRTUAL PRIVATE CLOUD.

4 MAIN COMPONENT OF VPC ||
------	-------- --------

SUBNET : DIVISION OF NETWORK IN T0 SUB PARTITION AND EACH PATITION IS CALLED SUBNET.
ROUTE TABLE : IT IS A COMPONENT OF VPC WHICH IS USED TO BUILD COMMUNICATION BETWEEN THE SUBNETS.
INTERNET GATEWAY : IT WILL HELP TO CONNECT YOUR VPC TO THE PUBLIC INTERNET(MOSTLY IPV4 0.0.0.0).
NAT GATEWAY : ALLOW OUTBOUND TRAFFIC WHILE CONNECTING IT SELF TO THE PUBLIC INTERNET AND BLOCKING THE INBOUND TRAFFIC




ACCESSING PRIVATE SUBNET AND PROVIDING INTERNET ACCESS TO IT USING NAT ::
--------||----------------||--------------------------------||--------

BASTION  HOST ( JUMP HOST )   CONCEPT::

**   ============|  |==========|  |=======**

VPC(190.0.0.0/21)

**- PUBLIC SUBNET ( 190.0.0.0/23 ) ----> \[ PUBLIC IP , PRIVATE IP ] , PUBLIC ROUT TABLE \[ IGW ACCESS 0.0.0.0/0 ]**
\*\*- PRIVATE SUBNET ( 190.0.2.0/23 ) ----> \\\[ PRIVATE IP ] , PRIVATE ROUTE TABLE \\\[ NAT GATEWAY WITH 0.0.0.0/0 AND AN  ELASTIC IP ONLY OTBOUND TRAFFIC ]\*\*



























PUBLIC SUBNET AND PRIVATE SUBNET MUST BE CONNECTED TO NAT GATEWAY
THEN ONLY WE CAN ACCES THE PRIVATE INSTANCE FROM  THE PUBLIC INSTANCE
WE MUST COPY THE PRIVATE INSTANCE KEY AND PASTE INSIDE THE PUBLIC INSTANCE  THEN BY THE PRIVATE IP OF PRIVATE INSTANCE WE CAN CREATE THE SSH CONNECTION.
FROM PRUBLIC SUBNET INSTANCE TO PRIVATE SUBNET INSTANCE




VPC   PEERING ::
====||========

VPC



172.31.0.0/16


190/23



LAMBDA FUNCTION ::
------	-------

CREATE INSTANCE USING BOTO-3:
PERFORM ACTION ON INSTANCE STATE:

 
import boto3
ec2=boto3.client('ec2')

def lambda_handler(event, context):
**instance\_id = 'instance ID'**

	**try:**

		**#check current state of instance**

		**instance\_state = ec2.describe\_instance(InstanceIDs=\[instance\_id])\['Reservation']\[0]\['Instance']\[0]\['State']\['Name']**

		

		**start or stop instance based on current state**

		**if instance\_state == 'stopped':**

					**ec2.start\_instance(InstanceIds=\[instance\_id])**

					**print(f"Started EC2 instance {instance\_id}")**



		**elif instace\_state == 'running':**

					**ec2.stop\_instance(InstanceIds=\[instance\_id])**

					**print(f"Stopped the nstance {instance\_id}")**



		**else:**

			**print(f"Instance {instance\_id} is in {Instance\_state} state , no action taken")**



	**except Exception as e:**

			**print(f"Error: {str(e)}")**







3. STOP MULTIPLE INSTANCE ON A REGION :

import boto3

def lambda_handler(event, context):
**#set the aws region**

	**region = 'region\_name'**



	**#create ec2 client**

	**ec2=boto3.client('ec2',region\_name=region)**



	**#get all running instance**

	**instance = ec2.describe\_instance(Filters=\[{'Name':'instance-state-name', 'Values': \['running']}])**



	**#stop each running instance**

	**for reservation in instances\['Reservation']:**

		**for instances in reservation\['Instances']:**

			**instance\_id= instance\['InstanceId']**

			**print(f"stopped instance: {instance\_id}")**

			**ec2.stop\_instances(InstanceIds=\[instance\_id])**




print(f"Ec2 instance stopped successfully.")



**S3 - BUCKET  ------------------------> lAMBDA -------------------------> NOTIFICATION**



				**trigger		   run			sns**





 










COUD WATCH :

☑️ --> OK STATE
🚥 --> INSUFFICIENT DATA
⚠️ --> ACTIVE (IN ALARM)





HOW TO SET ALARM ON CLOUDWATCH ::
=================================

SELECT METRICS ->


CLOUD SHELL ::
----- -----

CLI BASED INTERFACE USE TO MANAGE AND MAITAIN THE SERVICES THROUGH COMMAND

AUTO SCALLING ::
-------------

VERTICAL -> INCREASE IN THE CAPASITY
HORIZONTAL -> MULTIPLE SERVER TO DEVIDE THE LOAD

FIRST CREATE AUTO SCALE GROUP > AUTO SCALING >
```
