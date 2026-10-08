# 📘 DevOps Master Engineering Guide V2

> *High-yield guide extracted from `Akhil_DevOps_MASTER_V2.pdf` for mobile & web GitHub viewing.*

---

## Section / Page 1

AKHIL
 
B
 
M
 
DevOps
 
&
 
Cloud
 
Engineer
 
Complete
 
Interview
 
Master
 
Guide
 
Projects
 
+
 
Theory
 
+
 
Commands
 
+
 
Quick
 
Revision
 
+
 
Deep
 
Notes
 
 
AWS
  
|
  
Kubernetes
  
|
  
Docker
  
|
  
Azure
 
DevOps
  
|
  
Jenkins
  
|
  
Git
  
|
  
Linux
  
|
  
Terraform
  
|
  
Ansible
  
|
  
Networking
 
 
 
PART
 
1
 
Quick
 
Revision
 
~15
 
pages
 
|
 
Read
 
before
 
every
 
interview
 
PART
 
2
 
Full
 
Deep
 
Notes
 
100+
 
pages
 
|
 
Deep
 
study
 
over
 
5
 
days
 
 
 
All
 
3
 
Resume
 
Projects
 
Covered
 
Fully

## Section / Page 2

⚡
  
PART
 
1:
 
QUICK
 
REVISION
  
⚡
 
Read
 
this
 
BEFORE
 
every
 
interview
 
—
 
covers
 
everything
 
at
 
a
 
glance
 
in
 
~15
 
pages
 
 
1.
 
AWS
 
—
 
Core
 
Services
 
at
 
a
 
Glance
 
Service
 
What
 
It
 
Does
 
Key
 
Point
 
for
 
Interview
 
IAM
 
Controls
 
WHO
 
can
 
access
 
WHAT
 
in
 
AWS
 
Users=permanent,
 
Roles=temporary
 
for
 
services.
 
Least
 
Privilege
 
always.
 
EC2
 
Virtual
 
servers
 
in
 
the
 
cloud
 
Linux:
 
SSH
 
with
 
.pem
 
key
 
|
 
Windows:
 
RDP
 
port
 
3389
 
EBS
 
Block
 
storage
 
attached
 
to
 
EC2
 
AZ-specific.
 
Default
 
8GB
 
Linux/30GB
 
Windows.
 
Backup
 
via
 
Snapshots.
 
S3
 
Object
 
storage
 
in
 
buckets
 
Global,
 
unique
 
bucket
 
names.
 
Max
 
5TB.
 
Classes:
 
Standard→Glacier.
 
VPC
 
Your
 
private
 
isolated
 
network
 
Public
 
subnet=internet.
 
Private=internal.
 
NAT
 
for
 
outbound
 
only.
 
ALB
 
Layer
 
7
 
load
 
balancer
 
(HTTP/HTTPS)
 
Path/host-based
 
routing
 
→
 
microservices,
 
web
 
apps
 
NLB
 
Layer
 
4
 
load
 
balancer
 
(TCP/UDP)
 
Ultra-low
 
latency,
 
high
 
throughput.
 
Extreme
 
performance.
 
CloudWatch
 
AWS
 
monitoring
 
service
 
Metrics,
 
Alarms,
 
Logs.
 
You
 
used
 
LGTM
 
instead
 
—
 
mention
 
why.
 
RDS
 
Managed
 
relational
 
database
 
PostgreSQL,
 
MySQL,
 
Aurora.
 
YOU
 
used
 
PostgreSQL
 
in
 
Project
 
1.
 
DynamoDB
 
Managed
 
NoSQL
 
database
 
Auto-scales
 
horizontally.
 
Key-value
 
+
 
document
 
store.
 
Lambda
 
Serverless
 
compute
 
Event-triggered,
 
no
 
servers,
 
pay
 
per
 
invocation
 
millisecond.
 
Auto
 
Scaling
 
Automatically
 
adds/removes
 
EC2
 
Min,
 
Max,
 
Desired
 
capacity.
 
Triggered
 
by
 
CloudWatch
 
alarms.
 
Route
 
53
 
DNS
 
service
 
Translates
 
domains
 
to
 
IPs.
 
A
 
record,
 
CNAME,
 
MX,
 
TXT
 
records.
 
Elastic
 
IP
 
Static
 
public
 
IP
 
address
 
Stays
 
same
 
after
 
instance
 
stop/start.
 
Costs
 
money
 
when
 
unused.
 
 
Security
 
Group
 
vs
 
NACL
 
Feature
 
Security
 
Group
 
NACL
 
Level
 
Instance
 
level
 
(attached
 
to
 
EC2)
 
Subnet
 
level
 
(attached
 
to
 
subnet)
 
State
 
Stateful
 
—
 
response
 
automatically
 
allowed
 
Stateless
 
—
 
must
 
define
 
both
 
inbound
 
AND
 
outbound
 
Rules
 
Allow
 
only
 
—
 
no
 
deny
 
rules
 
Allow
 
AND
 
deny
 
rules

## Section / Page 3

Feature
 
Security
 
Group
 
NACL
 
Order
 
All
 
rules
 
evaluated
 
together
 
Rules
 
evaluated
 
in
 
order
 
(lowest
 
number
 
first)
 
Use
 
case
 
Day-to-day,
 
most
 
common
 
Broad
 
subnet-wide
 
rules,
 
extra
 
security
 
layer
 
 
Public
 
vs
 
Private
 
Subnet
 
 
Public
 
Subnet
 
Private
 
Subnet
 
Internet
 
Gateway
 
Has
 
route
 
to
 
IGW
 
No
 
route
 
to
 
IGW
 
External
 
access
 
Instances
 
can
 
have
 
public
 
IPs
 
No
 
public
 
IPs
 
Use
 
for
 
Load
 
balancers,
 
bastion
 
hosts
 
Databases,
 
app
 
servers,
 
internal
 
services
 
Outbound
 
internet
 
Yes
 
(via
 
IGW)
 
Only
 
via
 
NAT
 
Gateway
 
(outbound
 
only)
 
 
2.
 
Kubernetes
 
—
 
Core
 
Concepts
 
at
 
a
 
Glance
 
Component
 
Where
 
Role
 
API
 
Server
 
Master
 
Entry
 
point
 
for
 
ALL
 
kubectl
 
commands.
 
Front
 
door
 
of
 
K8s.
 
Scheduler
 
Master
 
Assigns
 
unscheduled
 
pods
 
to
 
worker
 
nodes
 
based
 
on
 
resources
 
Controller
 
Manager
 
Master
 
Runs
 
all
 
controllers
 
—
 
maintains
 
desired
 
state
 
of
 
everything
 
etcd
 
Master
 
Distributed
 
key-value
 
DB.
 
Stores
 
ALL
 
cluster
 
state.
 
Source
 
of
 
truth.
 
kubelet
 
Worker
 
Node
 
agent.
 
Gets
 
pod
 
specs
 
from
 
API
 
server.
 
Ensures
 
containers
 
run.
 
kube-proxy
 
Worker
 
Manages
 
network
 
rules
 
on
 
node.
 
Handles
 
service
 
routing
 
+
 
LB.
 
Container
 
Runtime
 
Worker
 
Actually
 
runs
 
containers
 
—
 
containerd
 
(Docker
 
deprecated
 
K8s
 
1.24+)
 
 
Object
 
What
 
It
 
Is
 
Your
 
Project
 
Pod
 
Smallest
 
unit.
 
1+
 
containers
 
share
 
IP+storage.
 
postgres-0,
 
nginx
 
pods
 
Deployment
 
Manages
 
ReplicaSets.
 
Rolling
 
updates,
 
rollback.
 
Frontend
 
+
 
Backend
 
(3
 
replicas
 
each)
 
ReplicaSet
 
Ensures
 
N
 
pods
 
always
 
running.
 
Managed
 
by
 
Deployment.
 
Created
 
automatically
 
by
 
Deployments

## Section / Page 4

Object
 
What
 
It
 
Is
 
Your
 
Project
 
StatefulSet
 
Stable
 
pod
 
identity,
 
own
 
PVC
 
per
 
pod.
 
PostgreSQL
 
DB
 
(postgres-0,1,2)
 
DaemonSet
 
One
 
pod
 
per
 
node.
 
Log
 
collectors,
 
monitoring.
 
Could
 
use
 
for
 
Promtail
 
ConfigMap
 
Non-sensitive
 
config
 
(env
 
vars,
 
files).
 
DB
 
connection
 
strings
 
(non-secret)
 
Secret
 
Sensitive
 
data
 
—
 
base64
 
encoded.
 
DB
 
passwords,
 
API
 
keys
 
Namespace
 
Logical
 
isolation
 
within
 
cluster.
 
dev,
 
staging,
 
prod
 
separation
 
 
Service
 
Types
 
Type
 
Access
 
DNS
 
Your
 
Project
 
ClusterIP
 
Internal
 
only
 
—
 
no
 
external
 
svc-name.namespace.sv
c.cluster.local
 
Backend
 
+
 
DB
 
services
 
NodePort
 
External
 
via
 
NodeIP:30000-32767
 
Same
 
as
 
ClusterIP
 
Dev/test
 
only
 
LoadBalancer
 
External
 
via
 
cloud
 
LB
 
(AWS
 
ELB)
 
External
 
IP
 
assigned
 
Frontend
 
service
 
ExternalName
 
Maps
 
to
 
external
 
DNS
 
Maps
 
to
 
external
 
FQDN
 
Access
 
external
 
APIs
 
 
Deployment
 
vs
 
StatefulSet
 
—
 
Critical
 
Difference
 
Feature
 
Deployment
 
StatefulSet
 
Pod
 
names
 
Random
 
(nginx-7d6b8c9-abc)
 
Stable
 
ordered
 
(postgres-0,
 
postgres-1)
 
Storage
 
Shared
 
PVC
 
or
 
none
 
Own
 
dedicated
 
PVC
 
per
 
pod
 
—
 
data
 
survives
 
Startup/shutdown
 
Any
 
order
 
Ordered
 
—
 
0
 
first,
 
then
 
1,
 
then
 
2
 
Use
 
case
 
Stateless:
 
web,
 
API,
 
frontend
 
Stateful:
 
databases,
 
Kafka,
 
Zookeeper
 
Identity
 
No
 
stable
 
identity
 
needed
 
Stable
 
identity
 
required
 
(reconnects
 
to
 
same
 
PV)
 
Why
 
StatefulSet
 
for
 
PostgreSQL
 
(YOUR
 
answer):
 
StatefulSet
 
gives
 
each
 
pod
 
a
 
stable
 
identity.
 
postgres-0
 
always
 
reconnects
 
to
 
its
 
own
 
EBS
 
volume
 
after
 
restart.
 
A
 
Deployment
 
would
 
assign
 
random
 
pod
 
names
 
and
 
lose
 
the
 
volume
 
binding
 
—
 
your
 
data
 
would
 
disappear
 
on
 
pod
 
restart.
 
 
kubectl
 
—
 
Essential
 
Commands
 
#
 
GET
 
RESOURCES
 
kubectl
 
get
 
pods
              
#
 
list
 
pods
 
in
 
current
 
namespace
 
kubectl
 
get
 
pods
 
-A
           
#
 
all
 
namespaces
 
kubectl
 
get
 
pods
 
-o
 
wide
      
#
 
with
 
IP
 
+
 
node
 
info
 
kubectl
 
get
 
nodes
             
#
 
list
 
nodes
 
kubectl
 
get
 
svc
               
#
 
services
 
kubectl
 
get
 
deploy
            
#
 
deployments

## Section / Page 5

kubectl
 
get
 
pvc
               
#
 
persistent
 
volume
 
claims
 
 
#
 
DEBUGGING
 
kubectl
 
describe
 
pod
 
<name>
   
#
 
detailed
 
info
 
+
 
Events
 
(most
 
useful)
 
kubectl
 
logs
 
<pod>
 
-f
         
#
 
follow
 
logs
 
in
 
real
 
time
 
kubectl
 
logs
 
<pod>
 
--previous
 
#
 
logs
 
from
 
crashed
 
container
 
kubectl
 
exec
 
-it
 
<pod>
 
--
 
bash
 
#
 
shell
 
into
 
running
 
pod
 
 
#
 
DEPLOY
 
&
 
MANAGE
 
kubectl
 
apply
 
-f
 
file.yaml
    
#
 
create/update
 
from
 
file
 
kubectl
 
delete
 
-f
 
file.yaml
   
#
 
delete
 
from
 
file
 
kubectl
 
scale
 
deployment/app
 
--replicas=5
 
kubectl
 
set
 
image
 
deployment/app
 
app=myimage:v2
  
#
 
rolling
 
update
 
kubectl
 
rollout
 
undo
 
deployment/app
              
#
 
rollback
 
kubectl
 
rollout
 
status
 
deployment/app
            
#
 
check
 
rollout
 
 
Deployment
 
Strategies
 
Strategy
 
How
 
Downtime
 
When
 
to
 
Use
 
Recreate
 
Kill
 
all,
 
create
 
all
 
new
 
Yes
 
Non-production,
 
quick
 
dev
 
environments
 
RollingUpdate
 
Replace
 
pods
 
one
 
by
 
one
 
(default)
 
No
 
Most
 
production
 
deployments
 
Blue-Green
 
Two
 
identical
 
envs,
 
switch
 
traffic
 
No
 
Zero-risk
 
switch,
 
easy
 
rollback
 
Canary
 
5%
 
traffic
 
new
 
version
 
first
 
No
 
Testing
 
new
 
features
 
safely
 
in
 
prod
 
 
Troubleshooting
 
Quick
 
Reference
 
Error
 
Root
 
Cause
 
First
 
Command
 
to
 
Run
 
CrashLoopBackOff
 
App
 
crashes
 
on
 
startup
 
(code
 
bug,
 
missing
 
config,
 
wrong
 
cmd)
 
kubectl
 
logs
 
<pod>
 
--previous
 
ImagePullBackOff
 
Wrong
 
image
 
name,
 
tag,
 
or
 
missing
 
registry
 
credentials
 
kubectl
 
describe
 
pod
 
<name>
 
—
 
check
 
Events
 
Pending
 
No
 
node
 
with
 
enough
 
CPU/RAM,
 
or
 
PVC
 
not
 
bound
 
kubectl
 
describe
 
pod
 
<name>
 
—
 
check
 
Events
 
OOMKilled
 
Container
 
exceeded
 
memory
 
limit
 
Increase
 
memory
 
limits
 
in
 
deployment
 
spec
 
NodeNotReady
 
kubelet
 
crash,
 
disk
 
full,
 
memory
 
exhausted
 
on
 
node
 
kubectl
 
describe
 
node
 
<name>
 
 
3.
 
Docker
 
—
 
Quick
 
Reference
 
Concept
 
Definition
 
Image
 
Read-only
 
blueprint
 
built
 
from
 
Dockerfile.
 
Stored
 
in
 
registry.

## Section / Page 6

Concept
 
Definition
 
Container
 
Running
 
instance
 
of
 
image.
 
Has
 
its
 
own
 
writable
 
layer.
 
Dockerfile
 
Instructions
 
to
 
build
 
image
 
layer
 
by
 
layer.
 
Each
 
instruction
 
=
 
one
 
layer.
 
Registry
 
Stores
 
images.
 
Docker
 
Hub
 
(public),
 
ECR
 
(AWS),
 
ACR
 
(Azure).
 
Layer
 
Each
 
Dockerfile
 
instruction
 
creates
 
immutable
 
layer.
 
Cached
 
for
 
speed.
 
 
Dockerfile
 
Instructions
 
—
 
Quick
 
Reference
 
Instruction
 
When
 
Purpose
 
Example
 
FROM
 
Build
 
start
 
Base
 
image
 
FROM
 
node:18-alpine
 
RUN
 
Build
 
time
 
Install
 
packages,
 
run
 
commands
 
RUN
 
npm
 
install
 
COPY
 
Build
 
time
 
Copy
 
files
 
from
 
host
 
to
 
image
 
COPY
 
app.js
 
/app/
 
ADD
 
Build
 
time
 
Like
 
COPY
 
but
 
extracts
 
tar,
 
fetches
 
URLs
 
ADD
 
app.tar.gz
 
/app/
 
WORKDIR
 
Build
 
time
 
Set
 
working
 
directory
 
WORKDIR
 
/app
 
EXPOSE
 
Documentati
on
 
Document
 
port
 
(does
 
NOT
 
publish)
 
EXPOSE
 
3000
 
ENV
 
Build+Runti
me
 
Set
 
environment
 
variables
 
ENV
 
NODE_ENV=production
 
ARG
 
Build
 
only
 
Build-time
 
variables
 
(not
 
in
 
final
 
image)
 
ARG
 
VERSION=1.0
 
CMD
 
Runtime
 
Default
 
start
 
command
 
—
 
CAN
 
be
 
overridden
 
CMD
 
["node","app.js"]
 
ENTRYPOIN
T
 
Runtime
 
Fixed
 
main
 
command
 
—
 
needs
 
--entrypoint
 
to
 
override
 
ENTRYPOINT
 
["java","-jar"]
 
USER
 
Runtime
 
Run
 
as
 
non-root
 
user
 
(security
 
best
 
practice)
 
USER
 
node
 
 
Docker
 
Commands
 
—
 
Must
 
Know
 
#
 
BUILD
 
docker
 
build
 
-t
 
myapp:1.0
 
.
         
#
 
build
 
from
 
Dockerfile
 
in
 
current
 
dir
 
docker
 
build
 
-t
 
myapp:1.0
 
-f
 
Dockerfile.prod
 
.
   
#
 
custom
 
Dockerfile
 
 
#
 
RUN
 
docker
 
run
 
-d
 
-p
 
8080:80
 
--name
 
app
 
myapp:1.0
    
#
 
background,
 
port
 
map
 
docker
 
run
 
-it
 
--rm
 
ubuntu
 
bash
                   
#
 
interactive,
 
remove
 
on
 
exit
 
docker
 
run
 
-e
 
DB_HOST=localhost
 
myapp:1.0
         
#
 
pass
 
env
 
var
 
docker
 
run
 
-v
 
/host/path:/container/path
 
myapp
    
#
 
bind
 
mount
 
 
#
 
MANAGE
 
CONTAINERS
 
docker
 
ps
               
#
 
running
 
containers
 
docker
 
ps
 
-a
            
#
 
all
 
containers
 
(including
 
stopped)

## Section / Page 7

docker
 
stop
 
<name>
      
#
 
graceful
 
stop
 
(SIGTERM)
 
docker
 
kill
 
<name>
      
#
 
force
 
stop
 
(SIGKILL)
 
docker
 
rm
 
<name>
        
#
 
remove
 
stopped
 
container
 
docker
 
rm
 
-f
 
<name>
     
#
 
force
 
remove
 
running
 
container
 
 
#
 
IMAGES
 
docker
 
images
           
#
 
list
 
local
 
images
 
docker
 
pull
 
nginx:latest
         
#
 
pull
 
from
 
registry
 
docker
 
push
 
myrepo/myapp:1.0
     
#
 
push
 
to
 
registry
 
docker
 
rmi
 
myapp:1.0
             
#
 
remove
 
image
 
 
#
 
LOGS
 
&
 
DEBUG
 
docker
 
logs
 
-f
 
<name>
            
#
 
follow
 
logs
 
docker
 
exec
 
-it
 
<name>
 
bash
      
#
 
shell
 
into
 
container
 
docker
 
inspect
 
<name>
            
#
 
detailed
 
container
 
info
 
docker
 
stats
                     
#
 
live
 
resource
 
usage
 
 
#
 
VOLUMES
 
docker
 
volume
 
create
 
mydata
      
#
 
create
 
named
 
volume
 
docker
 
volume
 
ls
                 
#
 
list
 
volumes
 
docker
 
volume
 
rm
 
mydata
          
#
 
remove
 
volume
 
 
VM
 
vs
 
Container
 
 
Virtual
 
Machine
 
Docker
 
Container
 
OS
 
Full
 
OS
 
per
 
instance
 
(GBs)
 
Shares
 
host
 
OS
 
kernel
 
(MBs)
 
Startup
 
time
 
Minutes
 
Seconds
 
Size
 
Gigabytes
 
Megabytes
 
Isolation
 
Full
 
hardware
 
isolation
 
Process-level
 
isolation
 
(namespaces+cgroups)
 
Performance
 
Heavy
 
overhead
 
Near-native
 
performance
 
Use
 
case
 
Full
 
environment
 
isolation
 
Microservices,
 
CI/CD,
 
consistent
 
deployments
 
 
4.
 
Git
 
—
 
All
 
Commands
 
You
 
Need
 
The
 
4
 
Areas
 
(Most
 
Important
 
Concept)
 
Working
 
Directory
 
→
 
Staging
 
Area
 
(git
 
add)
 
→
 
Local
 
Repo
 
(git
 
commit)
 
→
 
Remote
 
(git
 
push)
 
 
#
 
SETUP
 
git
 
config
 
--global
 
user.name
 
"Akhil
 
B
 
M"
 
git
 
config
 
--global
 
user.email
 
"akhilbm13@gmail.com"
 
git
 
init
                     
#
 
new
 
repo
 
git
 
clone
 
<url>
              
#
 
clone
 
remote
 
repo
 
 
#
 
DAILY
 
WORKFLOW
 
git
 
status
                   
#
 
see
 
what
 
changed
 
git
 
add
 
.
                    
#
 
stage
 
all
 
changes
 
git
 
add
 
filename
             
#
 
stage
 
specific
 
file

## Section / Page 8

git
 
add
 
-p
                   
#
 
interactively
 
choose
 
changes
 
git
 
commit
 
-m
 
"message"
      
#
 
commit
 
staged
 
changes
 
git
 
commit
 
-am
 
"message"
     
#
 
add+commit
 
tracked
 
files
 
git
 
push
 
origin
 
branch
       
#
 
push
 
to
 
remote
 
git
 
pull
 
origin
 
main
         
#
 
fetch
 
+
 
merge
 
from
 
remote
 
 
#
 
BRANCHING
 
git
 
branch
                   
#
 
list
 
local
 
branches
 
git
 
branch
 
-a
                
#
 
list
 
all
 
branches
 
(local+remote)
 
git
 
switch
 
-c
 
feature
        
#
 
create
 
and
 
switch
 
(modern
 
way)
 
git
 
checkout
 
-b
 
feature
      
#
 
create
 
and
 
switch
 
(old
 
way)
 
git
 
switch
 
main
              
#
 
switch
 
to
 
branch
 
git
 
merge
 
feature
            
#
 
merge
 
branch
 
into
 
current
 
git
 
rebase
 
main
              
#
 
rebase
 
current
 
onto
 
main
 
git
 
branch
 
-d
 
feature
        
#
 
delete
 
local
 
branch
 
(safe)
 
git
 
push
 
origin
 
--delete
 
feature
  
#
 
delete
 
remote
 
branch
 
 
#
 
VIEWING
 
HISTORY
 
git
 
log
 
--oneline
 
--graph
    
#
 
visual
 
branch
 
history
 
git
 
log
 
--oneline
 
-10
        
#
 
last
 
10
 
commits
 
git
 
diff
                     
#
 
working
 
dir
 
changes
 
(not
 
staged)
 
git
 
diff
 
--staged
            
#
 
staged
 
changes
 
(ready
 
to
 
commit)
 
git
 
show
 
<commit-id>
         
#
 
show
 
specific
 
commit
 
details
 
 
#
 
UNDOING
 
CHANGES
 
git
 
reset
 
--soft
 
HEAD~1
      
#
 
undo
 
commit,
 
keep
 
changes
 
STAGED
 
git
 
reset
 
--mixed
 
HEAD~1
     
#
 
undo
 
commit,
 
keep
 
changes
 
in
 
working
 
dir
 
git
 
reset
 
--hard
 
HEAD~1
      
#
 
undo
 
commit,
 
DELETE
 
changes
 
PERMANENTLY
 
git
 
revert
 
<commit-id>
       
#
 
safe
 
undo
 
—
 
creates
 
new
 
commit
 
(use
 
on
 
shared
 
branches)
 
git
 
cherry-pick
 
<commit-id>
  
#
 
apply
 
specific
 
commit
 
from
 
another
 
branch
 
git
 
stash
                    
#
 
save
 
uncommitted
 
changes
 
temporarily
 
git
 
stash
 
pop
                
#
 
restore
 
stashed
 
changes
 
git
 
stash
 
list
               
#
 
list
 
all
 
stashes
 
 
#
 
REMOTE
 
git
 
remote
 
-v
                
#
 
show
 
remote
 
URLs
 
git
 
remote
 
add
 
origin
 
<url>
  
#
 
add
 
remote
 
git
 
fetch
 
origin
             
#
 
download
 
changes
 
(dont
 
merge)
 
 
Merge
 
vs
 
Rebase
 
 
Merge
 
Rebase
 
History
 
Preserves
 
full
 
history
 
with
 
merge
 
commit
 
Creates
 
clean
 
linear
 
history
 
—
 
no
 
merge
 
commits
 
When
 
to
 
use
 
Merging
 
feature
 
branches
 
to
 
main
 
Cleaning
 
up
 
local
 
commits
 
before
 
PR
 
Safe
 
on
 
shared
 
branches?
 
YES
 
NO
 
—
 
never
 
rebase
 
public/shared
 
branches
 
Command
 
git
 
merge
 
feature
 
git
 
rebase
 
main
 
 
Reset
 
Types
 
—
 
Critical
 
Difference

## Section / Page 9

Reset
 
Type
 
Commit
 
Undone?
 
Changes
 
in
 
Staging?
 
Changes
 
in
 
Working
 
Dir?
 
Use
 
When
 
--soft
 
Yes
 
YES
 
—
 
still
 
staged
 
YES
 
—
 
still
 
there
 
Want
 
to
 
redo
 
the
 
commit
 
message
 
--mixed
 
(default)
 
Yes
 
No
 
—
 
unstaged
 
YES
 
—
 
still
 
there
 
Want
 
to
 
re-stage
 
selectively
 
--hard
 
Yes
 
No
 
—
 
gone
 
No
 
—
 
DELETED
 
permanently
 
Completely
 
undo
 
and
 
start
 
fresh
 
 
5.
 
Linux
 
—
 
Essential
 
Commands
 
File
 
System
 
Key
 
Directories
 
Directory
 
Contains
 
DevOps
 
Relevance
 
/etc
 
All
 
config
 
files
 
(nginx.conf,
 
hosts,
 
passwd)
 
Edit
 
Tomcat,
 
Apache,
 
PostgreSQL
 
configs
 
here
 
/var/log
 
All
 
log
 
files
 
Apache,
 
Tomcat,
 
system
 
logs
 
—
 
where
 
you
 
debug
 
/home
 
User
 
home
 
directories
 
Your
 
scripts
 
and
 
projects
 
/opt
 
Third-party
 
applications
 
Where
 
you
 
installed
 
Tomcat,
 
Loki,
 
Grafana
 
/tmp
 
Temporary
 
files
 
—
 
cleared
 
on
 
reboot
 
Temp
 
storage
 
for
 
scripts
 
/proc
 
Virtual
 
filesystem
 
—
 
live
 
process
 
info
 
CPU,
 
memory,
 
network
 
info
 
at
 
runtime
 
/usr/local/bin
 
Locally
 
installed
 
executables
 
Where
 
you
 
moved
 
Promtail,
 
kOps,
 
kubectl
 
 
Permissions
 
—
 
Must
 
Know
 
Permission
 
Octal
 
Meaning
 
rwxrwxrwx
 
777
 
Everyone
 
has
 
full
 
access
 
(NEVER
 
use
 
in
 
production)
 
rwxr-xr-x
 
755
 
Owner:
 
full
 
|
 
Group+Others:
 
read+execute
 
rw-r--r--
 
644
 
Owner:
 
read+write
 
|
 
Group+Others:
 
read
 
only
 
rwx------
 
700
 
Owner:
 
full
 
|
 
No
 
one
 
else
 
can
 
access
 
rw-------
 
600
 
Owner:
 
read+write
 
only
 
|
 
Common
 
for
 
SSH
 
keys
 
 
#
 
PERMISSIONS
 
chmod
 
755
 
file
              
#
 
change
 
permissions
 
using
 
octal
 
chmod
 
+x
 
script.sh
         
#
 
add
 
execute
 
permission
 
chown
 
user:group
 
file
       
#
 
change
 
owner
 
and
 
group
 
chown
 
-R
 
azureuser:azureuser
 
/opt/tomcat1
  
#
 
recursive
 
(YOUR
 
project)

## Section / Page 10

#
 
FILES
 
ls
 
-la
                     
#
 
list
 
all
 
including
 
hidden,
 
long
 
format
 
find
 
/
 
-name
 
"*.log"
       
#
 
find
 
log
 
files
 
find
 
.
 
-type
 
f
 
-mtime
 
-7
   
#
 
files
 
modified
 
in
 
last
 
7
 
days
 
grep
 
-r
 
"ERROR"
 
/var/log/
  
#
 
search
 
recursively
 
tail
 
-f
 
/var/log/syslog
    
#
 
follow
 
log
 
in
 
real
 
time
 
cat
 
file
 
|
 
grep
 
pattern
 
|
 
wc
 
-l
  
#
 
count
 
matching
 
lines
 
 
#
 
PROCESSES
 
ps
 
aux
                     
#
 
all
 
running
 
processes
 
ps
 
aux
 
|
 
grep
 
java
         
#
 
find
 
java
 
processes
 
top
                        
#
 
live
 
process
 
monitor
 
kill
 
-9
 
PID
                
#
 
force
 
kill
 
process
 
(SIGKILL)
 
pkill
 
tomcat
               
#
 
kill
 
by
 
name
 
pattern
 
nohup
 
./run.sh
 
&
           
#
 
run
 
in
 
background,
 
survives
 
logout
 
 
#
 
SERVICES
 
(systemctl)
 
systemctl
 
start
 
nginx
      
#
 
start
 
service
 
systemctl
 
stop
 
nginx
       
#
 
stop
 
service
 
systemctl
 
restart
 
nginx
    
#
 
restart
 
service
 
systemctl
 
status
 
nginx
     
#
 
check
 
if
 
running
 
+
 
recent
 
logs
 
systemctl
 
enable
 
nginx
     
#
 
start
 
automatically
 
on
 
boot
 
journalctl
 
-u
 
nginx
 
-f
     
#
 
follow
 
service
 
logs
 
 
#
 
NETWORKING
 
ip
 
addr
                    
#
 
show
 
network
 
interfaces
 
+
 
IPs
 
ss
 
-tulpn
                  
#
 
show
 
listening
 
ports
 
+
 
PIDs
 
ufw
 
allow
 
80
               
#
 
allow
 
port
 
in
 
firewall
 
ufw
 
status
                 
#
 
check
 
firewall
 
rules
 
curl
 
-I
 
http://localhost:7789/project1/
  
#
 
test
 
HTTP
 
response
 
ssh
 
-i
 
key.pem
 
azureuser@<ip>
            
#
 
SSH
 
into
 
server
 
 
#
 
DISK
 
df
 
-h
                      
#
 
disk
 
space
 
usage
 
du
 
-sh
 
/opt/*
              
#
 
size
 
of
 
each
 
directory
 
lsblk
                      
#
 
list
 
block
 
devices
 
 
6.
 
Terraform
 
—
 
Quick
 
Reference
 
Command
 
Action
 
Notes
 
terraform
 
init
 
Download
 
providers,
 
initialize
 
backend
 
Run
 
once
 
per
 
project
 
/
 
after
 
adding
 
providers
 
terraform
 
plan
 
Preview:
 
shows
 
+create,
 
~modify,
 
-destroy
 
Always
 
run
 
before
 
apply.
 
Save
 
with
 
-out=tfplan
 
terraform
 
apply
 
Create/update
 
infrastructure
 
Asks
 
for
 
confirmation.
 
Use
 
-auto-approve
 
for
 
CI/CD.
 
terraform
 
destroy
 
Delete
 
ALL
 
managed
 
resources
 
Dangerous!
 
Use
 
-target
 
to
 
destroy
 
specific
 
resource.
 
terraform
 
validate
 
Check
 
syntax
 
Run
 
before
 
plan
 
terraform
 
fmt
 
Format
 
.tf
 
files
 
Run
 
before
 
committing

## Section / Page 11

Command
 
Action
 
Notes
 
terraform
 
state
 
list
 
Show
 
all
 
tracked
 
resources
 
Debug
 
what
 
Terraform
 
knows
 
about
 
terraform
 
output
 
Show
 
output
 
values
 
After
 
apply
 
terraform
 
import
 
Import
 
existing
 
infra
 
into
 
state
 
Bring
 
existing
 
resources
 
under
 
TF
 
management
 
terraform
 
workspace
 
new/select
 
Create/switch
 
environment
 
dev,
 
staging,
 
prod
 
separate
 
states
 
 
Key
 
Files
 
File
 
Purpose
 
main.tf
 
Resource
 
definitions
 
—
 
your
 
EC2,
 
VPC,
 
S3,
 
etc.
 
variables.tf
 
Input
 
variable
 
declarations
 
(name,
 
type,
 
description,
 
default)
 
terraform.tfvars
 
Variable
 
values
 
—
 
one
 
per
 
environment.
 
DO
 
NOT
 
commit
 
secrets.
 
outputs.tf
 
Output
 
value
 
definitions
 
—
 
expose
 
resource
 
IDs,
 
IPs
 
after
 
apply
 
backend.tf
 
Remote
 
state
 
config
 
(S3
 
+
 
DynamoDB
 
locking
 
for
 
teams)
 
terraform.tfstate
 
Current
 
state
 
—
 
auto-generated.
 
NEVER
 
edit
 
manually.
 
Store
 
in
 
S3.
 
 
State
 
Management
 
for
 
Teams:
 
Store
 
terraform.tfstate
 
in
 
an
 
S3
 
bucket
 
with
 
DynamoDB
 
table
 
for
 
state
 
locking.
 
This
 
prevents
 
two
 
people
 
from
 
running
 
terraform
 
apply
 
at
 
the
 
same
 
time
 
and
 
corrupting
 
state.
 
 
7.
 
Azure
 
DevOps
 
—
 
Quick
 
Reference
 
Service
 
Purpose
 
You
 
Used?
 
Azure
 
Boards
 
Plan:
 
Epics,
 
Features,
 
User
 
Stories,
 
Tasks,
 
Bugs,
 
Kanban,
 
Sprints
 
YES
 
—
 
fully
 
Azure
 
Repos
 
Git
 
source
 
control
 
with
 
PR
 
policies
 
and
 
PR
 
templates
 
YES
 
—
 
fully
 
Azure
 
Pipelines
 
CI/CD
 
with
 
YAML
 
pipelines,
 
self-hosted
 
agents
 
YES
 
—
 
fully
 
Azure
 
Test
 
Plans
 
Manual
 
+
 
automated
 
testing
 
management
 
Theory
 
only
 
Azure
 
Artifacts
 
Package
 
registry
 
(npm,
 
NuGet,
 
Maven)
 
Theory
 
only
 
 
Work
 
Item
 
Hierarchy
 
Epic
 
→
 
Feature
 
→
 
User
 
Story
 
→
 
Task
 
/
 
Bug

## Section / Page 12

Level
 
What
 
It
 
Represents
 
Example
 
from
 
Your
 
Project
 
Epic
 
Large
 
business
 
objective
 
Build
 
Complete
 
CI/CD
 
Infrastructure
 
on
 
Azure
 
Feature
 
Functional
 
component
 
Automated
 
Tomcat
 
Deployment
 
Pipeline
 
User
 
Story
 
Requirement
 
from
 
user
 
perspective
 
As
 
a
 
developer,
 
I
 
want
 
code
 
auto-deployed
 
on
 
push
 
to
 
main
 
Task
 
Technical
 
work
 
item
 
Configure
 
self-hosted
 
agent
 
+
 
YAML
 
pipeline
 
Bug
 
Defect
 
to
 
fix
 
Pipeline
 
not
 
triggering
 
—
 
pushed
 
to
 
feature
 
not
 
main
 
 
YAML
 
Pipeline
 
Structure
 
trigger
 
→
 
pool
 
→
 
stages
 
→
 
jobs
 
→
 
steps
 
→
 
tasks
 
trigger:
 
-
 
main
                          
#
 
trigger
 
on
 
push
 
to
 
main
 
branch
 
 
pool:
 
  
name:
 
Default
                 
#
 
USE
 
POOL
 
NAME,
 
not
 
agent
 
name!
 
  
demands:
 
  
-
 
Agent.Name
 
-equals
 
myagent
  
#
 
target
 
specific
 
agent
 
 
stages:
 
-
 
stage:
 
Build
 
  
displayName:
 
"Build
 
Stage"
 
  
jobs:
 
  
-
 
job:
 
BuildJob
 
    
steps:
 
    
-
 
script:
 
mvn
 
clean
 
package
 
      
displayName:
 
"Compile
 
Java"
 
 
-
 
stage:
 
Deploy
 
  
dependsOn:
 
Build
 
  
condition:
 
succeeded()
         
#
 
only
 
if
 
Build
 
passed
 
  
jobs:
 
  
-
 
job:
 
DeployJob
 
    
steps:
 
    
-
 
script:
 
cp
 
target/*.war
 
/opt/tomcat1/webapps/
 
 
Self-Hosted
 
Agent
 
Setup
 
Summary
 
Step
 
Command/Action
 
1.
 
Download
 
Organization
 
Settings
 
→
 
Agent
 
Pools
 
→
 
Default
 
→
 
New
 
Agent
 
2.
 
Extract
 
tar
 
zxvf
 
vsts-agent-linux-x64-*.tar.gz
 
3.
 
Configure
 
./config.sh
 
→
 
Enter
 
URL,
 
PAT,
 
Pool:
 
Default,
 
Name:
 
myagent
 
4.
 
Start
 
./run.sh
 
→
 
Shows
 
"Listening
 
for
 
Jobs"

## Section / Page 13

Step
 
Command/Action
 
5.
 
Verify
 
Azure
 
DevOps
 
→
 
Agent
 
Pools
 
→
 
Default
 
→
 
myagent
 
shows
 
ONLINE
 
(green)
 
 
8.
 
Networking
 
—
 
Quick
 
Reference
 
OSI
 
Model
 
—
 
All
 
7
 
Layers
 
Memory
 
trick:
 
"All
 
People
 
Seem
 
To
 
Need
 
Data
 
Processing"
 
(Application
 
to
 
Physical)
 
Layer
 
Name
 
Protocols/Examples
 
Your
 
Project
 
7
 
Application
 
HTTP,
 
HTTPS,
 
FTP,
 
SMTP,
 
DNS,
 
SSH
 
Apache
 
on
 
port
 
80
 
6
 
Presentation
 
SSL/TLS,
 
encryption,
 
compression
 
HTTPS
 
certificates
 
5
 
Session
 
Session
 
establishment,
 
authentication
 
Stateful
 
connections
 
4
 
Transport
 
TCP
 
(reliable),
 
UDP
 
(fast),
 
port
 
numbers
 
Port
 
80,
 
7789,
 
8888
 
3
 
Network
 
IP,
 
routing,
 
ICMP
 
VPC
 
routing,
 
subnets
 
2
 
Data
 
Link
 
Ethernet,
 
MAC
 
addresses,
 
frames
 
VM
 
network
 
interfaces
 
1
 
Physical
 
Cables,
 
fiber,
 
radio,
 
electrical
 
signals
 
Azure
 
datacenter
 
cables
 
 
Key
 
Ports
 
—
 
Including
 
Your
 
Project
 
Ports
 
Protocol
 
Port
 
Your
 
Project?
 
SSH
 
22
 
Connect
 
to
 
Azure
 
VM
 
HTTP
 
80
 
Apache
 
Reverse
 
Proxy
 
(public)
 
HTTPS
 
443
 
Secure
 
HTTP
 
FTP
 
21
 
File
 
transfer
 
DNS
 
53
 
Domain
 
name
 
resolution
 
SMTP
 
25
 
Email
 
RDP
 
3389
 
Windows
 
EC2
 
access
 
MySQL
 
3306
 
MySQL
 
DB
 
PostgreSQL
 
5432
 
YOUR
 
database
 
in
 
both
 
projects
 
Tomcat
 
Instance
 
1
 
7789
 
YOUR
 
project
 
—
 
internal
 
only
 
Tomcat
 
Instance
 
2
 
8888
 
YOUR
 
project
 
—
 
internal
 
only
 
Grafana
 
3000
 
YOUR
 
LGTM
 
stack
 
dashboard
 
Loki
 
3100
 
YOUR
 
LGTM
 
stack
 
log
 
storage

## Section / Page 14

Protocol
 
Port
 
Your
 
Project?
 
Promtail
 
9080
 
YOUR
 
LGTM
 
log
 
collector
 
Kubernetes
 
API
 
6443
 
K8s
 
master
 
API
 
server
 
 
TCP
 
vs
 
UDP
 
 
TCP
 
UDP
 
Connection
 
3-way
 
handshake:
 
SYN→SYN-ACK→ACK
 
Connectionless
 
—
 
no
 
handshake
 
Reliability
 
Guaranteed
 
delivery,
 
ordered
 
packets
 
Best-effort
 
—
 
packets
 
may
 
be
 
lost
 
or
 
reordered
 
Speed
 
Slower
 
(overhead
 
for
 
reliability)
 
Faster
 
(no
 
overhead)
 
Use
 
cases
 
HTTP,
 
HTTPS,
 
SSH,
 
FTP,
 
PostgreSQL
 
DNS,
 
video
 
streaming,
 
gaming,
 
VoIP
 
 
9.
 
Your
 
3
 
Projects
 
—
 
30-Second
 
Answers
 
PROJECT
 
1
 
—
 
Azure
 
DevOps
 
+
 
Reverse
 
Proxy
 
+
 
Tomcat
 
+
 
LGTM:
 
I
 
deployed
 
two
 
isolated
 
Apache
 
Tomcat
 
instances
 
on
 
an
 
Azure
 
VM
 
—
 
Tomcat
 
1
 
on
 
port
 
7789
 
and
 
Tomcat
 
2
 
on
 
port
 
8888.
 
Apache
 
HTTP
 
Server
 
acts
 
as
 
a
 
reverse
 
proxy
 
on
 
port
 
80,
 
routing
 
/project1
 
to
 
Tomcat
 
1
 
and
 
/project2
 
to
 
Tomcat
 
2.
 
UFW
 
ensures
 
only
 
port
 
80
 
is
 
publicly
 
accessible
 
—
 
internal
 
ports
 
are
 
hidden.
 
An
 
Azure
 
DevOps
 
multi-stage
 
YAML
 
pipeline
 
with
 
a
 
self-hosted
 
agent
 
automates
 
the
 
full
 
Build
 
→
 
Test
 
→
 
Deploy
 
lifecycle.
 
PostgreSQL
 
is
 
the
 
database
 
with
 
non-root
 
users
 
and
 
encrypted
 
passwords.
 
The
 
LGTM
 
stack
 
(Promtail
 
→
 
Loki
 
→
 
Grafana)
 
provides
 
real-time
 
log
 
monitoring.
 
 
PROJECT
 
2
 
—
 
Kubernetes
 
Multi-Tier
 
App
 
on
 
AWS
 
via
 
kOps:
 
I
 
containerized
 
a
 
Node.js
 
backend
 
and
 
Apache
 
frontend
 
using
 
separate
 
Dockerfiles
 
for
 
service
 
isolation.
 
I
 
provisioned
 
a
 
Kubernetes
 
cluster
 
on
 
AWS
 
using
 
kOps
 
—
 
it
 
auto-created
 
the
 
master
 
node,
 
two
 
worker
 
nodes,
 
VPC,
 
security
 
groups,
 
and
 
ELB.
 
Deployed
 
frontend
 
with
 
Deployment
 
(3
 
replicas)
 
via
 
LoadBalancer
 
service
 
for
 
public
 
access.
 
Backend
 
deployed
 
via
 
ClusterIP
 
—
 
only
 
reachable
 
internally
 
via
 
K8s
 
DNS
 
(backend.default.svc.cluster.local:3000).
 
PostgreSQL
 
runs
 
as
 
a
 
StatefulSet
 
with
 
PVC
 
per
 
pod
 
backed
 
by
 
EBS
 
volumes,
 
so
 
data
 
persists
 
across
 
pod
 
restarts.
 
 
PROJECT
 
3
 
—
 
LGTM
 
Observability
 
Stack
 
(Part
 
of
 
Project
 
1):
 
Installed
 
Promtail
 
on
 
the
 
VM
 
as
 
a
 
log
 
collector.
 
It
 
reads
 
Apache
 
and
 
Tomcat
 
log
 
files
 
in
 
real-time
 
and
 
ships
 
them
 
to
 
Loki
 
(log
 
storage)
 
on
 
port
 
3100.
 
Grafana
 
on
 
port
 
3000
 
queries
 
Loki
 
and
 
displays
 
logs
 
in
 
dashboards
 
with
 
alerting.
 
Chose
 
LGTM
 
over
 
CloudWatch
 
because
 
it
 
is
 
free,
 
open-source,
 
and
 
works
 
across
 
both
 
AWS
 
and
 
Azure
 
—
 
CloudWatch
 
is
 
AWS-only
 
and
 
paid.
 
 
Why
 
Each
 
Key
 
Decision
 
Was
 
Made
 
Decision
 
Why
 
—
 
Your
 
Answer
 
Separate
 
Tomcat
 
instances
 
vs
 
context
 
paths
 
Context
 
paths
 
share
 
one
 
JVM
 
process.
 
If
 
it
 
crashes,
 
all
 
apps
 
die.
 
Separate
 
instances
 
=
 
fault
 
isolation,
 
independent
 
restart,
 
independent
 
resource
 
allocation.
 
StatefulSet
 
vs
 
Deployment
 
for
 
PostgreSQL
 
StatefulSet
 
gives
 
stable
 
pod
 
identity
 
(postgres-0
 
always
 
reconnects
 
to
 
its
 
own
 
PV).
 
Deployment
 
uses
 
random
 
names
 
and
 
loses
 
volume
 
binding
 
on
 
restart.
 
Loki
 
vs
 
CloudWatch
 
Loki:
 
free,
 
open-source,
 
works
 
across
 
AWS+Azure.
 
CloudWatch:
 
AWS-only,
 
paid.
 
My
 
project
 
used
 
both
 
clouds,
 
so
 
Loki
 
was
 
the
 
right
 
choice.

## Section / Page 15

Decision
 
Why
 
—
 
Your
 
Answer
 
Self-hosted
 
agent
 
vs
 
Microsoft-hosted
 
Self-hosted
 
agent
 
runs
 
on
 
the
 
same
 
VM
 
as
 
Tomcat,
 
so
 
it
 
can
 
copy
 
WAR
 
files
 
directly
 
without
 
SSH
 
hops.
 
Faster,
 
more
 
secure,
 
no
 
external
 
network
 
needed.
 
ClusterIP
 
for
 
backend
 
Backend
 
does
 
not
 
need
 
direct
 
external
 
access.
 
Only
 
frontend
 
calls
 
it
 
via
 
internal
 
K8s
 
DNS.
 
ClusterIP
 
is
 
more
 
secure
 
—
 
not
 
exposed
 
publicly.
 
3
 
replicas
 
for
 
frontend+backend
 
High
 
availability:
 
if
 
one
 
pod
 
crashes,
 
2
 
others
 
handle
 
traffic
 
while
 
K8s
 
restarts
 
the
 
failed
 
one.
 
No
 
downtime.
 
 
10.
 
Top
 
Interview
 
Questions
 
—
 
Full
 
Answers
 
Q:
 
Walk
 
me
 
through
 
your
 
CI/CD
 
pipeline
 
end
 
to
 
end
 
Developer
 
pushes
 
code
 
to
 
Azure
 
Repos
 
main
 
branch
 
→
 
Azure
 
DevOps
 
Pipeline
 
triggers
 
automatically
 
→
 
self-hosted
 
agent
 
on
 
the
 
VM
 
picks
 
up
 
the
 
job
 
→
 
Stage
 
1
 
compiles
 
Java
 
code
 
and
 
creates
 
WAR
 
file
 
→
 
Stage
 
2
 
runs
 
automated
 
tests
 
→
 
Stage
 
3
 
copies
 
WAR
 
to
 
Tomcat
 
1
 
at
 
port
 
7789
 
and
 
restarts
 
it
 
→
 
Stage
 
4
 
copies
 
WAR
 
to
 
Tomcat
 
2
 
at
 
port
 
8888.
 
Apache
 
reverse
 
proxy
 
on
 
port
 
80
 
routes
 
public
 
traffic
 
based
 
on
 
URL
 
path.
 
If
 
any
 
stage
 
fails,
 
subsequent
 
stages
 
are
 
skipped
 
due
 
to
 
condition:
 
succeeded().
 
 
Q:
 
What
 
happens
 
when
 
a
 
Pod
 
crashes
 
in
 
Kubernetes?
 
The
 
kubelet
 
on
 
the
 
worker
 
node
 
detects
 
the
 
crash
 
and
 
reports
 
it
 
to
 
the
 
API
 
server.
 
The
 
Controller
 
Manager
 
notices
 
the
 
ReplicaSet
 
has
 
fewer
 
pods
 
than
 
the
 
desired
 
replica
 
count.
 
Kubernetes
 
schedules
 
a
 
new
 
pod
 
on
 
an
 
available
 
worker
 
node.
 
The
 
new
 
pod
 
starts,
 
pulls
 
the
 
image,
 
and
 
runs.
 
This
 
entire
 
self-healing
 
process
 
usually
 
completes
 
in
 
10-30
 
seconds.
 
If
 
the
 
pod
 
keeps
 
crashing,
 
it
 
enters
 
CrashLoopBackOff
 
with
 
exponential
 
backoff
 
delays.
 
 
Q:
 
Difference
 
between
 
Docker
 
and
 
VM
 
VMs
 
run
 
a
 
full
 
OS
 
per
 
instance
 
—
 
gigabytes
 
of
 
disk,
 
minutes
 
to
 
start,
 
heavy
 
overhead.
 
Containers
 
share
 
the
 
host
 
OS
 
kernel
 
using
 
Linux
 
namespaces
 
and
 
cgroups
 
—
 
megabytes,
 
seconds
 
to
 
start,
 
near-native
 
performance.
 
VMs
 
provide
 
full
 
hardware
 
isolation;
 
containers
 
provide
 
process-level
 
isolation.
 
For
 
modern
 
microservices
 
and
 
CI/CD,
 
containers
 
are
 
preferred.
 
VMs
 
are
 
still
 
useful
 
when
 
you
 
need
 
full
 
OS
 
isolation
 
or
 
different
 
OS
 
types.
 
 
Q:
 
How
 
does
 
Terraform
 
manage
 
state?
 
Terraform
 
writes
 
the
 
current
 
state
 
of
 
all
 
managed
 
infrastructure
 
to
 
terraform.tfstate.
 
On
 
every
 
plan
 
or
 
apply,
 
it
 
compares
 
this
 
state
 
file
 
with
 
your
 
.tf
 
configuration
 
and
 
the
 
actual
 
infrastructure
 
to
 
determine
 
what
 
changes
 
need
 
to
 
be
 
made
 
—
 
what
 
to
 
create,
 
modify,
 
or
 
destroy.
 
For
 
teams,
 
we
 
store
 
state
 
in
 
an
 
S3
 
bucket
 
with
 
a
 
DynamoDB
 
table
 
for
 
state
 
locking.
 
This
 
prevents
 
two
 
engineers
 
from
 
running
 
terraform
 
apply
 
simultaneously,
 
which
 
would
 
corrupt
 
the
 
state
 
file.
 
 
Q:
 
What
 
is
 
least
 
privilege
 
in
 
IAM?
 
Give
 
users,
 
services,
 
and
 
applications
 
only
 
the
 
minimum
 
permissions
 
they
 
need
 
to
 
perform
 
their
 
specific
 
job
 
—
 
nothing
 
more.
 
This
 
limits
 
the
 
blast
 
radius
 
if
 
credentials
 
are
 
compromised.
 
In
 
practice:
 
use
 
specific
 
resource
 
ARNs
 
instead
 
of
 
wildcards
 
(*)
 
in
 
policies,
 
create
 
separate
 
IAM
 
roles
 
for
 
each
 
service
 
(EC2
 
role,
 
Lambda
 
role,
 
etc.),
 
review
 
and
 
prune
 
permissions
 
regularly,
 
and
 
prefer
 
roles
 
over
 
users
 
for
 
services.
 
 
Q:
 
What
 
would
 
you
 
improve
 
in
 
your
 
projects?
 
Project
 
1:
 
Add
 
health
 
checks
 
with
 
automatic
 
failover,
 
implement
 
HTTPS
 
with
 
SSL
 
certificates,
 
add
 
Mimir
 
for
 
metrics
 
and
 
Tempo
 
for
 
traces
 
to
 
complete
 
the
 
full
 
LGTM
 
stack.
 
Project
 
2:
 
Replace
 
EBS
 
with
 
EFS
 
for
 
multi-AZ
 
persistent

## Section / Page 16

storage,
 
set
 
up
 
three
 
master
 
nodes
 
for
 
HA
 
control
 
plane,
 
enable
 
Horizontal
 
Pod
 
Autoscaler
 
for
 
automatic
 
pod
 
scaling
 
based
 
on
 
CPU/memory,
 
implement
 
PostgreSQL
 
master-slave
 
replication.
 
Overall:
 
add
 
centralized
 
alerting,
 
runbooks
 
for
 
incident
 
response,
 
and
 
GitOps
 
workflow
 
with
 
ArgoCD.
 
 
Q:
 
Why
 
did
 
you
 
choose
 
Azure
 
DevOps
 
over
 
Jenkins?
 
For
 
this
 
project,
 
Azure
 
DevOps
 
made
 
sense
 
because
 
the
 
entire
 
infrastructure
 
was
 
on
 
Azure
 
—
 
VMs,
 
networking,
 
storage.
 
Azure
 
DevOps
 
provides
 
native
 
integration
 
with
 
Azure
 
resources,
 
built-in
 
Boards
 
for
 
project
 
tracking,
 
and
 
a
 
unified
 
platform
 
for
 
Repos,
 
Pipelines,
 
and
 
Artifacts.
 
Jenkins
 
would
 
have
 
required
 
additional
 
setup
 
and
 
integration.
 
That
 
said,
 
I
 
also
 
have
 
experience
 
with
 
Jenkins
 
from
 
my
 
internship
 
—
 
I
 
can
 
work
 
with
 
either
 
tool.
 
 
Q:
 
How
 
is
 
your
 
monitoring
 
different
 
from
 
CloudWatch?
 
CloudWatch
 
is
 
AWS-native
 
and
 
paid.
 
My
 
project
 
used
 
both
 
AWS
 
and
 
Azure,
 
so
 
I
 
needed
 
a
 
platform-agnostic
 
solution.
 
The
 
LGTM
 
stack
 
—
 
Loki
 
for
 
log
 
storage,
 
Grafana
 
for
 
visualization,
 
Promtail
 
as
 
the
 
log
 
collector
 
—
 
is
 
completely
 
open-source
 
and
 
free.
 
It
 
runs
 
on
 
any
 
platform.
 
Promtail
 
reads
 
log
 
files
 
from
 
disk
 
and
 
pushes
 
them
 
to
 
Loki,
 
which
 
indexes
 
them
 
with
 
labels.
 
Grafana
 
queries
 
Loki
 
using
 
LogQL
 
and
 
displays
 
results
 
in
 
dashboards.
 
The
 
key
 
advantage
 
is
 
that
 
the
 
same
 
stack
 
monitors
 
both
 
my
 
Azure
 
VM
 
services
 
and
 
AWS
 
Kubernetes
 
cluster
 
in
 
one
 
unified
 
Grafana
 
dashboard.

## Section / Page 17

📚
  
PART
 
2:
 
FULL
 
DEEP
 
NOTES
  
📚
 
Complete
 
study
 
material
 
—
 
100+
 
pages
 
covering
 
everything
 
in
 
depth.
 
Study
 
over
 
5
 
days.
 
 
SECTION
 
1:
 
AWS
 
—
 
Complete
 
Deep
 
Guide
 
Key
 
Insight:
 
AWS
 
is
 
the
 
most
 
critical
 
cloud
 
platform
 
for
 
DevOps.
 
You
 
have
 
real
 
project
 
experience
 
here
 
—
 
always
 
connect
 
theory
 
to
 
your
 
Kubernetes
 
project
 
on
 
AWS.
 
 
1.1
 
Cloud
 
Computing
 
Fundamentals
 
Cloud
 
computing
 
=
 
accessing
 
computing
 
services
 
(servers,
 
storage,
 
databases,
 
networking,
 
analytics,
 
AI)
 
over
 
the
 
internet
 
on
 
a
 
pay-as-you-go
 
basis.
 
No
 
upfront
 
hardware
 
costs.
 
Cloud
 
Service
 
Models
 
Model
 
What
 
You
 
Get
 
You
 
Manage
 
Examples
 
IaaS
 
(Infrastructure
 
as
 
a
 
Service)
 
VMs,
 
storage,
 
networking
 
OS,
 
middleware,
 
applications,
 
data
 
EC2,
 
Azure
 
VMs,
 
Google
 
Compute
 
Engine
 
PaaS
 
(Platform
 
as
 
a
 
Service)
 
Runtime,
 
middleware,
 
OS
 
Applications
 
and
 
data
 
only
 
Elastic
 
Beanstalk,
 
Azure
 
App
 
Service,
 
Heroku
 
SaaS
 
(Software
 
as
 
a
 
Service)
 
Complete
 
application
 
Nothing
 
—
 
just
 
use
 
it
 
Gmail,
 
Salesforce,
 
Office
 
365,
 
Jira
 
Cloud
 
Deployment
 
Models
 
Model
 
Description
 
Use
 
Case
 
Public
 
Cloud
 
Resources
 
hosted
 
by
 
AWS/Azure/GCP.
 
Shared
 
infrastructure.
 
Most
 
companies
 
—
 
lower
 
cost,
 
no
 
maintenance
 
Private
 
Cloud
 
Your
 
own
 
data
 
center
 
with
 
cloud-like
 
features.
 
Banks,
 
hospitals
 
—
 
strict
 
compliance
 
requirements
 
Hybrid
 
Cloud
 
Mix
 
of
 
public
 
and
 
private
 
cloud.
 
Sensitive
 
data
 
private,
 
scalable
 
workloads
 
public
 
Multi-Cloud
 
Using
 
multiple
 
providers
 
(AWS
 
+
 
Azure
 
together).
 
Your
 
Project
 
1
 
(Azure)
 
+
 
Project
 
2
 
(AWS)
 
=
 
Multi-cloud!
 
 
1.2
 
IAM
 
—
 
Identity
 
and
 
Access
 
Management
 
IAM
 
is
 
the
 
first
 
thing
 
you
 
learn
 
in
 
AWS
 
and
 
the
 
last
 
thing
 
you
 
master.
 
It
 
controls
 
every
 
access
 
to
 
every
 
resource.
 
IAM
 
Components
 
Component
 
Description
 
Example
 
User
 
Permanent
 
identity
 
for
 
a
 
human
 
or
 
application.
 
Has
 
credentials.
 
akhil-dev
 
user
 
for
 
your
 
account
 
Group
 
Collection
 
of
 
users
 
with
 
the
 
same
 
permissions.
 
developers
 
group
 
with
 
S3
 
+
 
EC2
 
access

## Section / Page 18

Component
 
Description
 
Example
 
Role
 
Temporary
 
identity
 
without
 
long-term
 
credentials.
 
Assumed
 
by
 
services.
 
EC2
 
role
 
that
 
allows
 
access
 
to
 
S3
 
Policy
 
JSON
 
document
 
defining
 
permissions.
 
Attached
 
to
 
User/Group/Role.
 
AmazonS3ReadOnlyAccess
 
policy
 
Policy
 
Types
 
•
 
AWS
 
Managed
 
Policies
 
—
 
pre-built
 
by
 
AWS
 
(AmazonEC2FullAccess,
 
AmazonS3ReadOnly)
 
•
 
Customer
 
Managed
 
Policies
 
—
 
you
 
create
 
custom
 
policies
 
for
 
specific
 
needs
 
•
 
Inline
 
Policies
 
—
 
directly
 
embedded
 
in
 
a
 
user/role
 
(not
 
reusable)
 
 
Least
 
Privilege
 
Principle:
 
Always
 
grant
 
minimum
 
permissions
 
needed.
 
Never
 
use
 
*
 
in
 
production
 
policies.
 
Regularly
 
audit
 
and
 
remove
 
unused
 
permissions.
 
Use
 
IAM
 
Access
 
Analyzer
 
to
 
find
 
over-permissive
 
policies.
 
IAM
 
Best
 
Practices
 
•
 
✅
 
Never
 
use
 
root
 
account
 
for
 
daily
 
work
 
—
 
create
 
an
 
IAM
 
admin
 
user
 
•
 
✅
 
Enable
 
MFA
 
on
 
root
 
and
 
all
 
admin
 
accounts
 
•
 
✅
 
Use
 
roles
 
for
 
EC2
 
instances
 
—
 
no
 
hardcoded
 
credentials
 
•
 
✅
 
Use
 
groups
 
to
 
assign
 
permissions
 
—
 
not
 
individual
 
users
 
•
 
✅
 
Rotate
 
access
 
keys
 
regularly
 
•
 
✅
 
Use
 
IAM
 
Access
 
Analyzer
 
to
 
identify
 
unused
 
permissions
 
 
1.3
 
EC2
 
—
 
Elastic
 
Compute
 
Cloud
 
Instance
 
Types
 
Family
 
Optimized
 
For
 
Examples
 
Use
 
Case
 
t
 
(Burstable)
 
Balanced,
 
low-cost
 
t2.micro,
 
t3.medium
 
Dev,
 
test,
 
small
 
workloads.
 
YOUR
 
kOps
 
EC2.
 
m
 
(General)
 
Balanced
 
CPU+RAM
 
m5.large,
 
m6i.xlarge
 
Web
 
servers,
 
small
 
databases
 
c
 
(Compute)
 
CPU-optimized
 
c5.xlarge,
 
c6g.2xlarge
 
High-traffic
 
web,
 
batch
 
processing
 
r
 
(Memory)
 
RAM-optimized
 
r5.large,
 
r6g.4xlarge
 
In-memory
 
databases,
 
big
 
data
 
analytics
 
i
 
(Storage)
 
Storage/IO
 
optimized
 
i3.large,
 
i3en.xlarge
 
High-speed
 
databases,
 
data
 
warehouses
 
Purchasing
 
Options
 
•
 
On-Demand
 
—
 
pay
 
by
 
hour/second.
 
Most
 
flexible.
 
No
 
commitment.
 
Highest
 
price.
 
•
 
Reserved
 
Instances
 
—
 
1
 
or
 
3
 
year
 
commitment.
 
Up
 
to
 
75%
 
discount
 
vs
 
On-Demand.
 
•
 
Spot
 
Instances
 
—
 
use
 
unused
 
EC2
 
capacity.
 
Up
 
to
 
90%
 
discount.
 
Can
 
be
 
terminated
 
anytime.
 
•
 
Savings
 
Plans
 
—
 
flexible
 
commitment
 
to
 
specific
 
$/hour
 
usage.
 
Covers
 
EC2,
 
Lambda,
 
Fargate.

## Section / Page 19

1.4
 
VPC
 
—
 
Virtual
 
Private
 
Cloud
 
VPC
 
Components
 
Deep
 
Dive
 
Component
 
Description
 
Your
 
Use
 
VPC
 
Isolated
 
virtual
 
network
 
in
 
AWS.
 
You
 
define
 
CIDR
 
(e.g.,
 
10.0.0.0/16).
 
kOps
 
auto-created
 
VPC
 
for
 
K8s
 
cluster
 
Subnet
 
Subdivision
 
of
 
VPC.
 
Public
 
(internet
 
access)
 
or
 
Private
 
(no
 
internet).
 
kOps
 
created
 
subnets
 
for
 
nodes
 
Internet
 
Gateway
 
Attached
 
to
 
VPC.
 
Routes
 
traffic
 
from
 
public
 
subnets
 
to
 
internet.
 
kOps
 
attached
 
IGW
 
automatically
 
NAT
 
Gateway
 
In
 
public
 
subnet.
 
Allows
 
private
 
instances
 
to
 
reach
 
internet
 
(outbound
 
only).
 
Private
 
K8s
 
nodes
 
pull
 
images
 
via
 
NAT
 
Route
 
Table
 
Rules
 
that
 
direct
 
traffic.
 
Each
 
subnet
 
has
 
one.
 
Public:
 
0.0.0.0/0
 
→
 
IGW
 
Security
 
Group
 
Stateful
 
firewall
 
at
 
instance/ENI
 
level.
 
Allow
 
only.
 
Ports
 
80,
 
22
 
open
 
for
 
K8s
 
nodes
 
NACL
 
Stateless
 
firewall
 
at
 
subnet
 
level.
 
Allow
 
+
 
Deny.
 
Additional
 
subnet-level
 
security
 
VPC
 
Peering
 
Connect
 
two
 
VPCs
 
privately.
 
Traffic
 
stays
 
on
 
AWS
 
backbone.
 
Connect
 
separate
 
project
 
VPCs
 
Endpoint
 
Private
 
connection
 
to
 
AWS
 
services
 
(S3,
 
DynamoDB)
 
without
 
internet.
 
Secure
 
S3
 
access
 
from
 
private
 
subnet
 
 
1.5
 
S3
 
—
 
Simple
 
Storage
 
Service
 
S3
 
Storage
 
Classes
 
(Cost
 
Optimization)
 
Storage
 
Class
 
Access
 
Pattern
 
Retrieval
 
Time
 
Use
 
Case
 
Standard
 
Frequent
 
access
 
Milliseconds
 
Active
 
data,
 
frequently
 
accessed
 
files
 
Standard-IA
 
Infrequent
 
but
 
fast
 
access
 
Milliseconds
 
Monthly
 
reports,
 
older
 
backups
 
One
 
Zone-IA
 
Infrequent,
 
single
 
AZ
 
Milliseconds
 
Recreatable
 
data,
 
lower
 
redundancy
 
OK
 
Intelligent-Tiering
 
Unknown
 
access
 
pattern
 
Milliseconds
 
Auto-moves
 
between
 
tiers
 
based
 
on
 
usage
 
Glacier
 
Instant
 
Archival,
 
rare
 
access
 
Milliseconds
 
Archive
 
needing
 
quick
 
retrieval
 
Glacier
 
Flexible
 
Archival,
 
rare
 
access
 
Minutes
 
to
 
hours
 
Regulatory
 
archives,
 
long-term
 
backups
 
Glacier
 
Deep
 
Archive
 
Rarely
 
if
 
ever
 
accessed
 
12+
 
hours
 
Legal
 
compliance,
 
7+
 
year
 
retention
 
S3
 
Key
 
Features
 
•
 
Versioning
 
—
 
keep
 
all
 
versions
 
of
 
every
 
object.
 
Enable
 
for
 
important
 
buckets.
 
•
 
Lifecycle
 
policies
 
—
 
auto-transition
 
objects
 
to
 
cheaper
 
classes,
 
auto-delete
 
after
 
X
 
days.
 
•
 
Bucket
 
policies
 
—
 
resource-based
 
policies
 
applied
 
to
 
the
 
bucket
 
(public
 
access
 
control).
 
•
 
Presigned
 
URLs
 
—
 
temporary
 
URL
 
granting
 
time-limited
 
access
 
to
 
private
 
objects.
 
•
 
S3
 
Static
 
Website
 
Hosting
 
—
 
serve
 
HTML/CSS/JS
 
directly
 
from
 
S3.

## Section / Page 20

•
 
Cross-Region
 
Replication
 
—
 
auto-replicate
 
objects
 
to
 
another
 
region
 
for
 
DR.
 
 
1.6
 
Load
 
Balancing
 
Deep
 
Dive
 
Feature
 
ALB
 
(Application
 
LB)
 
NLB
 
(Network
 
LB)
 
CLB
 
(Classic
 
LB
 
—
 
deprecated)
 
OSI
 
Layer
 
Layer
 
7
 
(Application)
 
Layer
 
4
 
(Transport)
 
Layer
 
4+7
 
(Legacy)
 
Protocol
 
HTTP,
 
HTTPS,
 
gRPC
 
TCP,
 
UDP,
 
TLS
 
HTTP,
 
HTTPS,
 
TCP
 
Routing
 
Path,
 
host,
 
header,
 
query
 
string
 
IP+Port
 
only
 
Basic
 
round-robin
 
Performance
 
Good
 
Extreme
 
(millions
 
req/sec)
 
Basic
 
Target
 
types
 
Instances,
 
IPs,
 
Lambda
 
Instances,
 
IPs
 
Instances
 
only
 
Use
 
case
 
Web
 
apps,
 
microservices,
 
REST
 
APIs
 
High-performance,
 
gaming,
 
IoT
 
Legacy,
 
avoid
 
for
 
new
 
Your
 
project
 
Frontend
 
K8s
 
service
 
used
 
ALB
 
Extreme
 
latency
 
scenarios
 
Not
 
used
 
 
1.7
 
Auto
 
Scaling
 
Auto
 
Scaling
 
Group
 
(ASG)
 
•
 
Min
 
capacity
 
—
 
always
 
running.
 
Ensures
 
baseline
 
availability.
 
•
 
Desired
 
capacity
 
—
 
target
 
number.
 
ASG
 
tries
 
to
 
maintain
 
this.
 
•
 
Max
 
capacity
 
—
 
cap
 
on
 
scaling.
 
Controls
 
costs.
 
 
Scaling
 
Policies
 
Policy
 
Type
 
How
 
It
 
Works
 
Use
 
Case
 
Target
 
Tracking
 
Maintain
 
a
 
metric
 
target
 
(e.g.,
 
CPU
 
=
 
50%)
 
Most
 
common
 
—
 
simple,
 
automatic
 
Step
 
Scaling
 
Scale
 
by
 
X
 
instances
 
when
 
metric
 
crosses
 
threshold
 
More
 
control
 
over
 
scaling
 
amount
 
Scheduled
 
Scale
 
at
 
specific
 
times
 
(e.g.,
 
9am
 
=
 
10
 
instances,
 
6pm
 
=
 
2)
 
Predictable
 
traffic
 
patterns
 
Predictive
 
ML-based
 
prediction
 
of
 
future
 
traffic
 
Proactive
 
scaling
 
before
 
traffic
 
spike
 
 
1.8
 
RDS,
 
DynamoDB,
 
ElastiCache
 
Service
 
Type
 
Key
 
Features
 
Your
 
Use
 
RDS
 
Relational
 
SQL
 
Managed
 
MySQL/PostgreSQL/Auro
ra.
 
Multi-AZ.
 
Read
 
Replicas.
 
PostgreSQL
 
concept
 
(you
 
ran
 
it
 
on
 
VM)

## Section / Page 21

Service
 
Type
 
Key
 
Features
 
Your
 
Use
 
Aurora
 
Relational
 
SQL
 
(AWS
 
native)
 
5x
 
faster
 
than
 
MySQL,
 
auto-scales
 
storage,
 
serverless
 
option.
 
Understanding
 
only
 
DynamoDB
 
NoSQL
 
key-value
 
Fully
 
managed,
 
auto-scales,
 
single-digit
 
ms
 
latency,
 
serverless.
 
Understanding
 
only
 
ElastiCache
 
In-memory
 
cache
 
Redis
 
or
 
Memcached.
 
Reduces
 
DB
 
load.
 
Session
 
storage.
 
Understanding
 
only
 
 
1.9
 
Other
 
AWS
 
Services
 
You
 
Should
 
Know
 
Service
 
Category
 
Key
 
Points
 
Lambda
 
Serverless
 
Event-triggered
 
functions.
 
Pay
 
per
 
100ms
 
execution.
 
No
 
servers.
 
ECS
 
Container
 
Orchestration
 
AWS-managed
 
Docker.
 
Simpler
 
than
 
K8s.
 
Fargate
 
=
 
serverless
 
containers.
 
EKS
 
Managed
 
Kubernetes
 
AWS-managed
 
K8s
 
control
 
plane.
 
You
 
can
 
use
 
instead
 
of
 
kOps.
 
CloudTrail
 
Audit
 
Logs
 
every
 
API
 
call
 
in
 
your
 
account.
 
Who
 
did
 
what,
 
when.
 
SNS
 
Messaging
 
Pub/Sub.
 
Fan-out.
 
Triggers
 
Lambda,
 
emails,
 
SMS
 
on
 
events.
 
SQS
 
Queue
 
Decouples
 
services.
 
Messages
 
persist
 
until
 
processed.
 
Dead-letter
 
queues.
 
Secrets
 
Manager
 
Security
 
Stores
 
and
 
rotates
 
secrets
 
(DB
 
passwords,
 
API
 
keys).
 
Better
 
than
 
SSM.
 
Systems
 
Manager
 
Operations
 
Patch
 
Manager,
 
Parameter
 
Store,
 
Session
 
Manager
 
(SSH
 
without
 
keys).
 
CloudFormation
 
IaC
 
AWS-native
 
IaC.
 
Like
 
Terraform
 
but
 
only
 
AWS.
 
JSON/YAML
 
templates.

## Section / Page 22

SECTION
 
2:
 
Kubernetes
 
—
 
Complete
 
Deep
 
Guide
 
Your
 
Project:
 
You
 
provisioned
 
a
 
real
 
K8s
 
cluster
 
on
 
AWS
 
using
 
kOps
 
with
 
Node.js
 
backend
 
+
 
Apache
 
frontend
 
+
 
PostgreSQL
 
StatefulSet.
 
Every
 
concept
 
here
 
connects
 
to
 
that
 
real
 
experience.
 
 
2.1
 
Why
 
Kubernetes?
 
Problem
 
→
 
Solution
 
Docker
 
Standalone
 
Problem
 
Kubernetes
 
Solution
 
Container
 
crashes
 
→
 
stays
 
dead
 
(no
 
auto-restart)
 
Auto-healing
 
—
 
kubelet
 
detects
 
crash,
 
restarts
 
pod
 
automatically
 
Cannot
 
add
 
containers
 
automatically
 
on
 
load
 
HPA
 
—
 
scales
 
pod
 
count
 
based
 
on
 
CPU/memory
 
metrics
 
No
 
traffic
 
distribution
 
between
 
containers
 
Built-in
 
load
 
balancing
 
across
 
pod
 
replicas
 
via
 
Services
 
Single
 
host
 
—
 
no
 
multi-node
 
clustering
 
Multi-node
 
cluster
 
—
 
pods
 
distributed
 
across
 
many
 
machines
 
Updating
 
=
 
downtime
 
(stop
 
old,
 
start
 
new)
 
Rolling
 
updates
 
—
 
gradual
 
pod
 
replacement,
 
zero
 
downtime
 
No
 
health
 
checks
 
Liveness,
 
Readiness,
 
Startup
 
probes
 
Complex
 
cross-host
 
networking
 
CNI
 
plugins
 
+
 
Kubernetes
 
networking
 
model
 
Manual
 
storage
 
management
 
PV/PVC
 
abstraction
 
with
 
dynamic
 
provisioning
 
 
2.2
 
Kubernetes
 
Architecture
 
—
 
Deep
 
Dive
 
Control
 
Plane
 
Components
 
Component
 
Function
 
Interview
 
Note
 
kube-apiserver
 
The
 
front
 
door.
 
All
 
kubectl
 
commands
 
→
 
REST
 
calls
 
to
 
API
 
server.
 
Validates
 
and
 
persists
 
objects
 
to
 
etcd.
 
ALL
 
communication
 
goes
 
through
 
API
 
server
 
—
 
nothing
 
talks
 
to
 
etcd
 
directly
 
etcd
 
Distributed
 
key-value
 
store.
 
Stores
 
all
 
cluster
 
state.
 
THE
 
source
 
of
 
truth.
 
If
 
etcd
 
is
 
lost,
 
the
 
cluster
 
state
 
is
 
lost
 
—
 
backup
 
etcd
 
in
 
production
 
kube-scheduler
 
Watches
 
for
 
pods
 
with
 
no
 
node
 
assigned.
 
Picks
 
best
 
node
 
based
 
on
 
CPU/RAM/taints/affinity.
 
Does
 
NOT
 
start
 
pods
 
—
 
just
 
assigns
 
them
 
to
 
nodes
 
(kubelet
 
starts
 
them)
 
kube-controller-ma
nager
 
Runs
 
all
 
controllers
 
in
 
one
 
process:
 
Deployment,
 
ReplicaSet,
 
Node,
 
Endpoints,
 
ServiceAccount
 
controllers.
 
Each
 
controller
 
watches
 
state
 
and
 
reconciles
 
to
 
desired
 
state
 
cloud-controller-m
anager
 
Handles
 
cloud-specific
 
logic:
 
creates
 
LoadBalancers,
 
manages
 
routes,
 
handles
 
node
 
lifecycle.
 
On
 
AWS:
 
creates
 
ELB
 
when
 
you
 
create
 
LoadBalancer
 
Service
 
Worker
 
Node
 
Components

## Section / Page 23

Component
 
Function
 
Interview
 
Note
 
kubelet
 
Node
 
agent.
 
Receives
 
pod
 
specs
 
from
 
API
 
server.
 
Starts/stops
 
containers
 
via
 
container
 
runtime.
 
Reports
 
node+pod
 
status.
 
kubelet
 
is
 
what
 
makes
 
pods
 
actually
 
run
 
—
 
brain
 
of
 
the
 
worker
 
node
 
kube-proxy
 
Runs
 
on
 
every
 
node.
 
Maintains
 
iptables/IPVS
 
rules
 
for
 
Service
 
routing.
 
Load
 
balances
 
traffic
 
across
 
pod
 
endpoints.
 
Not
 
a
 
proxy
 
in
 
the
 
traditional
 
sense
 
—
 
it
 
manages
 
networking
 
RULES
 
Container
 
Runtime
 
Actually
 
runs
 
containers.
 
containerd
 
(standard),
 
CRI-O.
 
Docker
 
was
 
deprecated
 
as
 
runtime
 
in
 
K8s
 
1.24.
 
Docker
 
CLI
 
still
 
works
 
—
 
Docker
 
Engine
 
was
 
the
 
runtime,
 
containerd
 
is
 
what
 
K8s
 
uses
 
now
 
 
2.3
 
Pod
 
Deep
 
Dive
 
A
 
Pod
 
is
 
the
 
atomic
 
unit
 
of
 
Kubernetes
 
—
 
you
 
don't
 
run
 
containers
 
directly,
 
you
 
run
 
Pods.
 
Pod
 
Lifecycle
 
States
 
State
 
Meaning
 
Pending
 
Pod
 
accepted
 
but
 
not
 
yet
 
running.
 
Waiting
 
for
 
scheduling,
 
image
 
pull,
 
or
 
volume
 
attachment.
 
Running
 
Pod
 
has
 
been
 
bound
 
to
 
a
 
node,
 
all
 
containers
 
created,
 
at
 
least
 
one
 
is
 
running.
 
Succeeded
 
All
 
containers
 
exited
 
with
 
code
 
0.
 
Final
 
state
 
for
 
batch
 
jobs.
 
Failed
 
All
 
containers
 
terminated,
 
at
 
least
 
one
 
exited
 
with
 
non-zero
 
code.
 
Unknown
 
Cannot
 
determine
 
pod
 
state
 
(node
 
communication
 
issue).
 
CrashLoopBackOff
 
Container
 
keeps
 
crashing.
 
K8s
 
retries
 
with
 
exponential
 
backoff
 
(10s,
 
20s,
 
40s...
 
max
 
5min).
 
Health
 
Probes
 
Probe
 
Type
 
Purpose
 
When
 
Pod
 
is
 
Restarted
 
Liveness
 
Probe
 
Is
 
the
 
container
 
alive
 
(not
 
deadlocked)?
 
Yes
 
—
 
if
 
liveness
 
check
 
fails,
 
container
 
is
 
restarted
 
Readiness
 
Probe
 
Is
 
the
 
container
 
ready
 
to
 
receive
 
traffic?
 
No
 
restart
 
—
 
removed
 
from
 
Service
 
endpoints
 
until
 
ready
 
Startup
 
Probe
 
Has
 
the
 
container
 
finished
 
starting?
 
(slow
 
apps)
 
Yes
 
—
 
if
 
startup
 
probe
 
fails,
 
container
 
is
 
killed
 
and
 
restarted
 
livenessProbe:
 
  
httpGet:
 
    
path:
 
/health
 
    
port:
 
8080
 
  
initialDelaySeconds:
 
30
   
#
 
wait
 
30s
 
before
 
first
 
check
 
  
periodSeconds:
 
10
         
#
 
check
 
every
 
10
 
seconds

## Section / Page 24

Probe
 
Type
 
Purpose
 
When
 
Pod
 
is
 
Restarted
 
  
failureThreshold:
 
3
       
#
 
restart
 
after
 
3
 
consecutive
 
failures
 
 
readinessProbe:
 
  
httpGet:
 
    
path:
 
/ready
 
    
port:
 
8080
 
  
initialDelaySeconds:
 
5
 
  
periodSeconds:
 
5
 
 
2.4
 
Deployments
 
—
 
Complete
 
Guide
 
Deployment
 
→
 
manages
 
→
 
ReplicaSet
 
→
 
manages
 
→
 
Pods.
 
Deployments
 
are
 
THE
 
standard
 
way
 
to
 
run
 
stateless
 
applications.
 
apiVersion:
 
apps/v1
 
kind:
 
Deployment
 
metadata:
 
  
name:
 
frontend
 
  
namespace:
 
default
 
spec:
 
  
replicas:
 
3
 
  
selector:
 
    
matchLabels:
 
      
app:
 
frontend
 
  
strategy:
 
    
type:
 
RollingUpdate
 
    
rollingUpdate:
 
      
maxSurge:
 
1
         
#
 
max
 
pods
 
ABOVE
 
desired
 
during
 
update
 
      
maxUnavailable:
 
1
   
#
 
max
 
pods
 
BELOW
 
desired
 
during
 
update
 
  
template:
 
    
metadata:
 
      
labels:
 
        
app:
 
frontend
 
    
spec:
 
      
containers:
 
      
-
 
name:
 
frontend
 
        
image:
 
myrepo/frontend:1.0
 
        
ports:
 
        
-
 
containerPort:
 
80
 
        
resources:
 
          
requests:
 
            
cpu:
 
"250m"
      
#
 
0.25
 
CPU
 
cores
 
guaranteed
 
            
memory:
 
"128Mi"
  
#
 
128MB
 
RAM
 
guaranteed
 
          
limits:
 
            
cpu:
 
"500m"
      
#
 
max
 
0.5
 
CPU
 
cores
 
            
memory:
 
"256Mi"
  
#
 
max
 
256MB
 
—
 
OOMKilled
 
if
 
exceeded
 
 
2.5
 
StatefulSet
 
—
 
Complete
 
Guide
 
StatefulSets
 
are
 
for
 
applications
 
that
 
need
 
stable
 
identity
 
and
 
persistent
 
storage
 
—
 
databases,
 
message
 
queues,
 
distributed
 
systems.

## Section / Page 25

What
 
StatefulSet
 
Provides
 
•
 
✅
 
Stable,
 
unique
 
pod
 
names:
 
postgres-0,
 
postgres-1,
 
postgres-2
 
(never
 
random)
 
•
 
✅
 
Stable
 
network
 
identity:
 
postgres-0.postgres-service.default.svc.cluster.local
 
•
 
✅
 
Own
 
PersistentVolumeClaim
 
per
 
pod
 
via
 
volumeClaimTemplates
 
•
 
✅
 
Ordered
 
deployment:
 
0
 
starts
 
first,
 
then
 
1,
 
then
 
2
 
•
 
✅
 
Ordered
 
deletion:
 
2
 
first,
 
then
 
1,
 
then
 
0
 
 
apiVersion:
 
apps/v1
 
kind:
 
StatefulSet
 
metadata:
 
  
name:
 
postgres
 
spec:
 
  
serviceName:
 
postgres-service
    
#
 
headless
 
service
 
for
 
stable
 
DNS
 
  
replicas:
 
3
 
  
selector:
 
    
matchLabels:
 
      
app:
 
postgres
 
  
template:
 
    
metadata:
 
      
labels:
 
        
app:
 
postgres
 
    
spec:
 
      
containers:
 
      
-
 
name:
 
postgres
 
        
image:
 
postgres:14
 
        
ports:
 
        
-
 
containerPort:
 
5432
 
        
env:
 
        
-
 
name:
 
POSTGRES_PASSWORD
 
          
valueFrom:
 
            
secretKeyRef:
 
              
name:
 
postgres-secret
 
              
key:
 
password
 
        
volumeMounts:
 
        
-
 
name:
 
postgres-data
 
          
mountPath:
 
/var/lib/postgresql/data
 
  
volumeClaimTemplates:
                   
#
 
creates
 
PVC
 
for
 
EACH
 
pod
 
  
-
 
metadata:
 
      
name:
 
postgres-data
 
    
spec:
 
      
accessModes:
 
["ReadWriteOnce"]
 
      
resources:
 
        
requests:
 
          
storage:
 
10Gi
                   
#
 
backed
 
by
 
EBS
 
in
 
your
 
project
 
 
2.6
 
Services
 
—
 
Complete
 
Guide
 
How
 
Services
 
Work
 
Services
 
provide
 
stable
 
networking
 
for
 
pods.
 
Pods
 
are
 
ephemeral
 
—
 
they
 
get
 
new
 
IPs
 
on
 
restart.
 
Services
 
give
 
a
 
stable
 
IP/DNS
 
that
 
always
 
routes
 
to
 
healthy
 
pods.
 
#
 
LoadBalancer
 
Service
 
(frontend
 
—
 
your
 
project)
 
apiVersion:
 
v1
 
kind:
 
Service
 
metadata:

## Section / Page 26

name:
 
frontend-service
 
spec:
 
  
type:
 
LoadBalancer
 
  
selector:
 
    
app:
 
frontend
 
  
ports:
 
  
-
 
port:
 
80
 
    
targetPort:
 
80
 
#
 
Creates
 
AWS
 
ELB
 
automatically
 
via
 
cloud-controller-manager
 
 
#
 
ClusterIP
 
Service
 
(backend
 
—
 
your
 
project)
 
apiVersion:
 
v1
 
kind:
 
Service
 
metadata:
 
  
name:
 
backend-service
 
spec:
 
  
type:
 
ClusterIP
   
#
 
default,
 
internal
 
only
 
  
selector:
 
    
app:
 
backend
 
  
ports:
 
  
-
 
port:
 
3000
 
    
targetPort:
 
3000
 
#
 
Accessible
 
as:
 
backend-service.default.svc.cluster.local:3000
 
 
2.7
 
Persistent
 
Storage
 
Storage
 
Chain
 
StorageClass
 
→
 
PersistentVolume
 
(PV)
 
→
 
PersistentVolumeClaim
 
(PVC)
 
→
 
Pod
 
Object
 
What
 
It
 
Is
 
Who
 
Creates
 
It
 
StorageClass
 
Template
 
for
 
dynamic
 
provisioning
 
(which
 
type
 
of
 
storage
 
to
 
create)
 
Admin
 
/
 
cloud
 
provider
 
PersistentVolume
 
(PV)
 
Actual
 
storage
 
resource
 
(EBS
 
volume,
 
NFS
 
share,
 
etc.)
 
Admin
 
or
 
auto-created
 
by
 
StorageClass
 
PersistentVolumeClaim
 
(PVC)
 
Pod's
 
request
 
for
 
storage
 
("I
 
need
 
10GB
 
ReadWriteOnce")
 
Developer
 
in
 
pod/StatefulSet
 
spec
 
Access
 
Modes
 
Mode
 
Meaning
 
Use
 
Case
 
ReadWriteOnce
 
(RWO)
 
One
 
node
 
can
 
read+write.
 
One
 
pod
 
at
 
a
 
time.
 
EBS
 
volumes
 
—
 
databases.
 
YOUR
 
project.
 
ReadOnlyMany
 
(ROX)
 
Multiple
 
nodes
 
can
 
read.
 
No
 
writing.
 
Shared
 
read-only
 
config
 
data
 
ReadWriteMany
 
(RWX)
 
Multiple
 
nodes
 
can
 
read+write
 
simultaneously.
 
EFS,
 
NFS
 
—
 
shared
 
storage
 
across
 
pods
 
Your
 
Project
 
Limitation:
 
You
 
used
 
EBS
 
(ReadWriteOnce)
 
for
 
PostgreSQL.
 
EBS
 
is
 
AZ-specific
 
—
 
if
 
us-east-1a
 
fails,
 
your
 
DB
 
becomes
 
inaccessible.
 
Production
 
fix:
 
use
 
EFS
 
(ReadWriteMany,
 
multi-AZ)
 
or
 
implement
 
database
 
replication.

## Section / Page 27

2.8
 
ConfigMap
 
and
 
Secrets
 
#
 
ConfigMap
 
—
 
non-sensitive
 
config
 
apiVersion:
 
v1
 
kind:
 
ConfigMap
 
metadata:
 
  
name:
 
app-config
 
data:
 
  
DB_HOST:
 
"postgres-service.default.svc.cluster.local"
 
  
DB_PORT:
 
"5432"
 
  
LOG_LEVEL:
 
"info"
 
 
#
 
Secret
 
—
 
sensitive
 
data
 
(base64
 
encoded)
 
apiVersion:
 
v1
 
kind:
 
Secret
 
metadata:
 
  
name:
 
postgres-secret
 
type:
 
Opaque
 
data:
 
  
password:
 
cGFzc3dvcmQxMjM=
   
#
 
base64
 
of
 
"password123"
 
  
#
 
echo
 
-n
 
"password123"
 
|
 
base64
 
 
#
 
Use
 
in
 
Pod
 
envFrom:
 
-
 
configMapRef:
 
    
name:
 
app-config
 
-
 
secretRef:
 
    
name:
 
postgres-secret
 
 
2.9
 
Advanced
 
K8s
 
Concepts
 
HPA
 
—
 
Horizontal
 
Pod
 
Autoscaler
 
Automatically
 
scales
 
pod
 
count
 
based
 
on
 
CPU/memory
 
usage
 
or
 
custom
 
metrics.
 
kubectl
 
autoscale
 
deployment
 
backend
 
--cpu-percent=70
 
--min=2
 
--max=10
 
#
 
OR
 
use
 
YAML:
 
apiVersion:
 
autoscaling/v2
 
kind:
 
HorizontalPodAutoscaler
 
metadata:
 
  
name:
 
backend-hpa
 
spec:
 
  
scaleTargetRef:
 
    
apiVersion:
 
apps/v1
 
    
kind:
 
Deployment
 
    
name:
 
backend
 
  
minReplicas:
 
2
 
  
maxReplicas:
 
10
 
  
metrics:
 
  
-
 
type:
 
Resource
 
    
resource:
 
      
name:
 
cpu
 
      
target:
 
        
type:
 
Utilization
 
        
averageUtilization:
 
70
   
#
 
scale
 
when
 
CPU
 
>
 
70%
 
RBAC
 
—
 
Role-Based
 
Access
 
Control

## Section / Page 28

Object
 
Purpose
 
ServiceAccount
 
WHO
 
makes
 
the
 
request
 
(identity
 
for
 
pods/processes)
 
Role
 
WHAT
 
actions
 
are
 
allowed
 
on
 
WHICH
 
resources
 
(namespace-scoped)
 
ClusterRole
 
Same
 
as
 
Role
 
but
 
cluster-wide
 
RoleBinding
 
CONNECTS
 
ServiceAccount
 
to
 
Role
 
ClusterRoleBinding
 
CONNECTS
 
ServiceAccount
 
to
 
ClusterRole
 
(cluster-wide)
 
Ingress
 
Ingress
 
is
 
an
 
HTTP
 
router
 
that
 
sits
 
in
 
front
 
of
 
multiple
 
Services.
 
Instead
 
of
 
creating
 
a
 
LoadBalancer
 
per
 
service
 
(expensive),
 
one
 
Ingress
 
controller
 
handles
 
all
 
HTTP/HTTPS
 
routing.
 
apiVersion:
 
networking.k8s.io/v1
 
kind:
 
Ingress
 
metadata:
 
  
name:
 
app-ingress
 
  
annotations:
 
    
kubernetes.io/ingress.class:
 
"nginx"
 
spec:
 
  
rules:
 
  
-
 
host:
 
myapp.example.com
 
    
http:
 
      
paths:
 
      
-
 
path:
 
/api
 
        
pathType:
 
Prefix
 
        
backend:
 
          
service:
 
            
name:
 
backend-service
 
            
port:
 
              
number:
 
3000
 
      
-
 
path:
 
/
 
        
pathType:
 
Prefix
 
        
backend:
 
          
service:
 
            
name:
 
frontend-service
 
            
port:
 
              
number:
 
80
 
 
2.10
 
kOps
 
—
 
Your
 
Project
 
Setup
 
(Complete)
 
#
 
STEP
 
1:
 
Install
 
kOps
 
and
 
kubectl
 
on
 
EC2
 
(t2.medium,
 
needs
 
IAM
 
permissions)
 
curl
 
-Lo
 
kops
 
https://github.com/kubernetes/kops/releases/download/v1.28.0/kops-linux-amd64
 
chmod
 
+x
 
kops
 
&&
 
sudo
 
mv
 
kops
 
/usr/local/bin/
 
 
#
 
STEP
 
2:
 
Create
 
S3
 
bucket
 
for
 
kOps
 
state
 
store
 
aws
 
s3
 
mb
 
s3://akhil-kops-state-store
 
export
 
KOPS_STATE_STORE=s3://akhil-kops-state-store
 
 
#
 
STEP
 
3:
 
Create
 
cluster
 
config
 
(does
 
NOT
 
create
 
resources
 
yet)
 
kops
 
create
 
cluster
 
\
 
  
--name=mycluster.k8s.local
 
\

## Section / Page 29

--state=s3://akhil-kops-state-store
 
\
 
  
--zones=us-east-1a
 
\
 
  
--node-count=2
 
\
 
  
--node-size=t3.medium
 
\
 
  
--master-size=t3.medium
 
 
#
 
STEP
 
4:
 
Apply
 
—
 
actually
 
creates
 
AWS
 
resources
 
kops
 
update
 
cluster
 
--name
 
mycluster.k8s.local
 
--yes
 
--admin
 
#
 
kOps
 
creates:
 
VPC,
 
Subnets,
 
Security
 
Groups,
 
EC2
 
instances,
 
IAM
 
roles,
 
#
 
ELB
 
for
 
API
 
server,
 
etcd,
 
Auto
 
Scaling
 
Groups
 
 
#
 
STEP
 
5:
 
Validate
 
cluster
 
is
 
ready
 
(takes
 
~5-10
 
minutes)
 
kops
 
validate
 
cluster
 
--wait
 
10m
 
 
#
 
STEP
 
6:
 
Verify
 
kubectl
 
get
 
nodes
 
 
#
 
COMMON
 
OPERATIONS
 
kops
 
get
 
clusters
                  
#
 
list
 
clusters
 
kops
 
edit
 
cluster
 
mycluster.k8s.local
  
#
 
edit
 
config
 
kops
 
rolling-update
 
cluster
 
--yes
  
#
 
apply
 
changes
 
kops
 
delete
 
cluster
 
--name=mycluster.k8s.local
 
--yes
  
#
 
delete
 
everything

## Section / Page 30

SECTION
 
3:
 
Docker
 
—
 
Complete
 
Deep
 
Guide
 
 
3.1
 
Docker
 
Architecture
 
Component
 
Role
 
Communication
 
Docker
 
Client
 
(CLI)
 
What
 
you
 
type:
 
docker
 
build,
 
docker
 
run,
 
docker
 
push
 
Sends
 
commands
 
to
 
Docker
 
daemon
 
via
 
REST
 
API
 
over
 
UNIX
 
socket
 
Docker
 
Daemon
 
(dockerd)
 
Does
 
all
 
the
 
work:
 
builds
 
images,
 
runs
 
containers,
 
manages
 
volumes/networks
 
Listens
 
on
 
/var/run/docker.sock
 
Docker
 
Registry
 
Stores
 
images.
 
Docker
 
Hub
 
(public
 
default).
 
ECR/ACR
 
(private).
 
Daemon
 
pulls/pushes
 
images
 
over
 
HTTPS
 
 
3.2
 
Docker
 
Layers
 
and
 
Caching
 
Every
 
Dockerfile
 
instruction
 
creates
 
an
 
immutable
 
read-only
 
layer.
 
Layers
 
are
 
cached
 
—
 
if
 
a
 
layer
 
hasn't
 
changed,
 
Docker
 
reuses
 
it,
 
making
 
builds
 
faster.
 
Layer
 
Optimization
 
Rule:
 
Put
 
instructions
 
that
 
change
 
RARELY
 
at
 
the
 
TOP
 
(FROM,
 
package
 
installs).
 
Put
 
instructions
 
that
 
change
 
OFTEN
 
at
 
the
 
BOTTOM
 
(COPY
 
source
 
code).
 
This
 
way,
 
changing
 
your
 
code
 
only
 
rebuilds
 
the
 
last
 
few
 
layers
 
—
 
not
 
all
 
of
 
npm
 
install.
 
#
 
INEFFICIENT
 
—
 
code
 
change
 
triggers
 
npm
 
install
 
every
 
time
 
FROM
 
node:18-alpine
 
WORKDIR
 
/app
 
COPY
 
.
 
.
              
#
 
COPY
 
everything
 
(if
 
any
 
file
 
changes,
 
npm
 
install
 
re-runs)
 
RUN
 
npm
 
install
 
CMD
 
["node","app.js"]
 
 
#
 
OPTIMIZED
 
—
 
npm
 
install
 
is
 
cached
 
unless
 
package.json
 
changes
 
FROM
 
node:18-alpine
 
WORKDIR
 
/app
 
COPY
 
package*.json
 
./
 
#
 
ONLY
 
copy
 
package
 
files
 
first
 
RUN
 
npm
 
install
       
#
 
cached
 
unless
 
package.json
 
changes
 
COPY
 
.
 
.
              
#
 
copy
 
source
 
code
 
(changes
 
often,
 
only
 
rebuilds
 
from
 
here)
 
CMD
 
["node","app.js"]
 
 
3.3
 
Multi-Stage
 
Dockerfile
 
—
 
Your
 
Project
 
Pattern
 
Build
 
in
 
a
 
large
 
builder
 
stage,
 
copy
 
ONLY
 
the
 
final
 
artifact
 
to
 
a
 
minimal
 
runtime
 
image.
 
Result:
 
much
 
smaller
 
production
 
images.
 
#
 
Stage
 
1:
 
Build
 
(large
 
image
 
with
 
all
 
build
 
tools)
 
FROM
 
maven:3.9-eclipse-temurin-17
 
AS
 
builder
 
WORKDIR
 
/app
 
COPY
 
pom.xml
 
.
 
RUN
 
mvn
 
dependency:go-offline
   
#
 
cache
 
dependencies
 
COPY
 
src/
 
src/
 
RUN
 
mvn
 
package
 
-DskipTests
     
#
 
build
 
the
 
WAR
 
file

## Section / Page 31

#
 
Stage
 
2:
 
Runtime
 
(small
 
image,
 
just
 
JRE)
 
FROM
 
eclipse-temurin:17-jre-alpine
 
WORKDIR
 
/app
 
COPY
 
--from=builder
 
/app/target/app.war
 
.
   
#
 
copy
 
only
 
the
 
WAR
 
USER
 
nobody
                                  
#
 
run
 
as
 
non-root
 
(security)
 
EXPOSE
 
8080
 
CMD
 
["java","-jar","app.war"]
 
 
#
 
Result:
 
Final
 
image
 
is
 
~200MB
 
instead
 
of
 
~800MB
 
with
 
full
 
maven+JDK
 
 
3.4
 
Docker
 
Compose
 
—
 
Full
 
Example
 
version:
 
"3.8"
 
 
services:
 
  
frontend:
 
    
build:
 
./frontend
 
    
ports:
 
    
-
 
"80:80"
 
    
depends_on:
 
    
-
 
backend
 
    
networks:
 
    
-
 
app-network
 
 
  
backend:
 
    
build:
 
./backend
 
    
ports:
 
    
-
 
"3000:3000"
 
    
environment:
 
    
-
 
DB_HOST=database
 
    
-
 
DB_PORT=5432
 
    
-
 
DB_PASSWORD=${DB_PASSWORD}
   
#
 
from
 
.env
 
file
 
    
depends_on:
 
    
-
 
database
 
    
networks:
 
    
-
 
app-network
 
 
  
database:
 
    
image:
 
postgres:14
 
    
environment:
 
    
-
 
POSTGRES_DB=myapp
 
    
-
 
POSTGRES_PASSWORD=${DB_PASSWORD}
 
    
volumes:
 
    
-
 
db-data:/var/lib/postgresql/data
 
    
networks:
 
    
-
 
app-network
 
 
volumes:
 
  
db-data:
     
#
 
named
 
volume
 
—
 
persists
 
across
 
container
 
restarts
 
 
networks:
 
  
app-network:
 
#
 
custom
 
network
 
—
 
containers
 
resolve
 
each
 
other
 
by
 
service
 
name
 
 
3.5
 
Docker
 
Networking
 
Details

## Section / Page 32

Network
 
Type
 
Isolation
 
Communication
 
Use
 
Case
 
bridge
 
(default)
 
Isolated
 
from
 
host
 
Containers
 
on
 
same
 
bridge
 
can
 
communicate
 
by
 
name
 
Local
 
development
 
—
 
most
 
common
 
host
 
No
 
isolation
 
from
 
host
 
Container
 
uses
 
host
 
IP
 
directly
 
High
 
performance,
 
avoid
 
when
 
possible
 
none
 
Complete
 
isolation
 
No
 
networking
 
at
 
all
 
Maximum
 
security,
 
batch
 
jobs
 
overlay
 
Multi-host
 
Containers
 
across
 
different
 
Docker
 
hosts
 
(Swarm)
 
Docker
 
Swarm
 
clustering
 
macvlan
 
Custom
 
MAC
 
Container
 
gets
 
its
 
own
 
MAC/IP
 
on
 
physical
 
network
 
Legacy
 
apps
 
needing
 
physical
 
network
 
 
3.6
 
Docker
 
Security
 
Best
 
Practices
 
•
 
✅
 
Use
 
official
 
base
 
images
 
—
 
don't
 
use
 
random
 
images
 
from
 
Docker
 
Hub
 
•
 
✅
 
Use
 
non-root
 
user
 
—
 
USER
 
node
 
or
 
USER
 
nobody
 
in
 
Dockerfile
 
•
 
✅
 
Scan
 
images
 
for
 
vulnerabilities
 
—
 
docker
 
scout,
 
Trivy,
 
Snyk
 
•
 
✅
 
Use
 
multi-stage
 
builds
 
to
 
minimize
 
attack
 
surface
 
•
 
✅
 
Never
 
store
 
secrets
 
in
 
Dockerfile
 
—
 
use
 
Docker
 
secrets
 
or
 
env
 
vars
 
at
 
runtime
 
•
 
✅
 
Use
 
.dockerignore
 
—
 
exclude
 
.git,
 
node_modules,
 
secrets
 
from
 
build
 
context
 
•
 
✅
 
Pin
 
image
 
tags
 
—
 
FROM
 
node:18.20.2-alpine,
 
not
 
FROM
 
node:latest
 
•
 
❌
 
Never
 
use
 
FROM
 
node:latest
 
in
 
production
 
—
 
could
 
break
 
with
 
updates
 
•
 
❌
 
Never
 
expose
 
unnecessary
 
ports
 
—
 
EXPOSE
 
only
 
what
 
the
 
app
 
actually
 
uses

## Section / Page 33

SECTION
 
4:
 
Jenkins
 
—
 
Complete
 
Deep
 
Guide
 
 
4.1
 
What
 
is
 
Jenkins?
 
Jenkins
 
is
 
the
 
most
 
popular
 
open-source
 
CI/CD
 
automation
 
server.
 
It
 
integrates
 
with
 
Git,
 
Docker,
 
Kubernetes,
 
SonarQube,
 
Nexus,
 
Slack,
 
and
 
hundreds
 
of
 
other
 
tools
 
via
 
plugins.
 
Jenkins
 
Architecture
 
Component
 
Role
 
Your
 
Azure
 
Equivalent
 
Master/Controller
 
Orchestrates
 
everything.
 
Schedules
 
jobs.
 
Serves
 
UI.
 
Stores
 
configs.
 
Does
 
NOT
 
run
 
builds.
 
Azure
 
DevOps
 
server
 
itself
 
Agents/Nodes
 
Execute
 
the
 
actual
 
build
 
jobs.
 
Can
 
be
 
static
 
(always-on)
 
or
 
dynamic
 
(spin
 
up,
 
run,
 
terminate).
 
Your
 
self-hosted
 
agent
 
(myagent)
 
Pipeline
 
Automated
 
series
 
of
 
steps:
 
checkout
 
→
 
build
 
→
 
test
 
→
 
deploy
 
Your
 
multi-stage
 
YAML
 
pipeline
 
Plugins
 
Extend
 
Jenkins
 
with
 
1800+
 
integrations
 
Azure
 
DevOps
 
tasks/extensions
 
 
4.2
 
Jenkinsfile
 
—
 
Complete
 
Example
 
pipeline
 
{
 
  
agent
 
any
   
//
 
OR:
 
agent
 
{
 
label
 
"docker-agent"
 
}
 
 
  
environment
 
{
 
    
DOCKER_CREDS
 
=
 
credentials("docker-hub-creds")
  
//
 
Jenkins
 
credential
 
store
 
    
APP_VERSION
  
=
 
"1.0.${BUILD_NUMBER}"
 
  
}
 
 
  
triggers
 
{
 
    
githubPush()
   
//
 
trigger
 
on
 
every
 
GitHub
 
push
 
  
}
 
 
  
stages
 
{
 
    
stage("Checkout")
 
{
 
      
steps
 
{
 
        
git
 
branch:
 
"main",
 
url:
 
"https://github.com/AkhilNikhil/myapp.git"
 
      
}
 
    
}
 
 
    
stage("Build")
 
{
 
      
steps
 
{
 
        
sh
 
"mvn
 
clean
 
package
 
-DskipTests"
 
        
archiveArtifacts
 
artifacts:
 
"target/*.jar",
 
fingerprint:
 
true
 
      
}
 
    
}
 
 
    
stage("Test")
 
{
 
      
steps
 
{
 
        
sh
 
"mvn
 
test"

## Section / Page 34

}
 
      
post
 
{
 
        
always
 
{
 
          
junit
 
"target/surefire-reports/*.xml"
  
//
 
publish
 
test
 
results
 
        
}
 
      
}
 
    
}
 
 
    
stage("Docker
 
Build
 
&
 
Push")
 
{
 
      
steps
 
{
 
        
sh
 
"""
 
          
docker
 
build
 
-t
 
myapp:${APP_VERSION}
 
.
 
          
echo
 
$DOCKER_CREDS_PSW
 
|
 
docker
 
login
 
-u
 
$DOCKER_CREDS_USR
 
--password-stdin
 
          
docker
 
push
 
myrepo/myapp:${APP_VERSION}
 
        
"""
 
      
}
 
    
}
 
 
    
stage("Deploy
 
to
 
K8s")
 
{
 
      
steps
 
{
 
        
sh
 
"kubectl
 
set
 
image
 
deployment/app
 
app=myrepo/myapp:${APP_VERSION}"
 
        
sh
 
"kubectl
 
rollout
 
status
 
deployment/app"
 
      
}
 
    
}
 
  
}
 
 
  
post
 
{
 
    
success
 
{
 
echo
 
"Pipeline
 
SUCCEEDED!
 
Version:
 
${APP_VERSION}"
 
}
 
    
failure
 
{
 
echo
 
"Pipeline
 
FAILED!
 
Check
 
logs."
 
}
 
    
always
  
{
 
cleanWs()
 
}
  
//
 
clean
 
workspace
 
after
 
every
 
build
 
  
}
 
}
 
 
4.3
 
Jenkins
 
vs
 
Azure
 
DevOps
 
Pipelines
 
Feature
 
Jenkins
 
Azure
 
DevOps
 
Pipelines
 
Type
 
Open-source,
 
self-hosted
 
(you
 
manage
 
the
 
server)
 
SaaS
 
—
 
Microsoft
 
manages
 
it
 
Setup
 
Need
 
to
 
install
 
and
 
maintain
 
Jenkins
 
server
 
Zero
 
setup
 
—
 
ready
 
to
 
use
 
Pricing
 
Free
 
(server
 
+
 
plugins)
 
Free
 
tier
 
+
 
paid
 
for
 
more
 
parallel
 
jobs
 
Integrations
 
1800+
 
plugins
 
Native
 
Azure,
 
good
 
GitHub
 
integration
 
Configuration
 
Jenkinsfile
 
(Groovy)
 
azure-pipelines.yml
 
(YAML)
 
Learning
 
curve
 
Higher
 
(server
 
management
 
+
 
Groovy)
 
Lower
 
(YAML
 
is
 
simpler)
 
Best
 
for
 
Complex
 
pipelines,
 
on-prem
 
CI/CD
 
Azure-native
 
projects
 
(like
 
your
 
Project
 
1)
 
Your
 
Experience
 
Internship
 
(Jenkins
 
+
 
GitHub)
 
Your
 
main
 
projects
 
(Azure
 
DevOps)

## Section / Page 35

Interview
 
tip:
 
You
 
can
 
use
 
BOTH.
 
Say:
 
"I
 
used
 
Jenkins
 
in
 
my
 
internship
 
for
 
CI/CD
 
with
 
GitHub.
 
For
 
my
 
Azure
 
DevOps
 
projects,
 
I
 
chose
 
Azure
 
Pipelines
 
because
 
it
 
integrates
 
natively
 
with
 
Azure
 
VMs
 
and
 
provides
 
Boards,
 
Repos,
 
and
 
Pipelines
 
in
 
one
 
platform."

## Section / Page 36

SECTION
 
5:
 
Git
 
—
 
Complete
 
Deep
 
Guide
 
 
5.1
 
Git
 
vs
 
Other
 
VCS
 
Type
 
Example
 
How
 
It
 
Works
 
Problem
 
Local
 
VCS
 
RCS
 
Tracks
 
changes
 
only
 
on
 
your
 
machine
 
If
 
machine
 
dies,
 
everything
 
lost.
 
No
 
collaboration.
 
Centralized
 
VCS
 
SVN,
 
CVS
 
One
 
server
 
stores
 
all
 
history.
 
Everyone
 
pulls
 
from
 
it.
 
Single
 
point
 
of
 
failure.
 
No
 
offline
 
work.
 
Distributed
 
VCS
 
Git,
 
Mercurial
 
Every
 
developer
 
has
 
FULL
 
copy
 
including
 
ALL
 
history.
 
Slightly
 
more
 
complex
 
—
 
but
 
solved
 
all
 
other
 
problems
 
Git
 
is
 
distributed
 
—
 
this
 
is
 
why
 
it's
 
the
 
industry
 
standard.
 
Full
 
history,
 
offline
 
work,
 
no
 
single
 
point
 
of
 
failure.
 
 
5.2
 
Git
 
Branching
 
Strategies
 
GitFlow
 
(Complex,
 
Large
 
Teams)
 
Branch
 
Purpose
 
main
 
Production-ready
 
code
 
only.
 
Tagged
 
with
 
version
 
numbers.
 
develop
 
Integration
 
branch.
 
Features
 
merged
 
here
 
first.
 
feature/*
 
Each
 
new
 
feature
 
gets
 
its
 
own
 
branch.
 
Merges
 
into
 
develop.
 
release/*
 
Release
 
preparation
 
(version
 
bumps,
 
bugfixes).
 
Merges
 
into
 
main
 
+
 
develop.
 
hotfix/*
 
Emergency
 
production
 
fixes.
 
Branches
 
from
 
main.
 
Merges
 
to
 
main
 
+
 
develop.
 
GitHub
 
Flow
 
(Simple,
 
Most
 
Teams)
 
•
 
main
 
—
 
always
 
deployable.
 
Protected
 
branch.
 
•
 
feature
 
branches
 
—
 
short-lived,
 
one
 
feature/bug
 
fix
 
per
 
branch
 
•
 
PR
 
→
 
review
 
→
 
merge
 
to
 
main
 
→
 
auto-deploy
 
Your
 
Azure
 
DevOps
 
Setup
 
•
 
Main
 
branch
 
with
 
pipeline
 
trigger
 
(trigger:
 
-
 
main
 
in
 
your
 
YAML)
 
•
 
Feature
 
branches
 
for
 
development
 
→
 
PR
 
→
 
merge
 
to
 
main
 
•
 
PR
 
template
 
in
 
.azuredevops/
 
folder
 
•
 
Branch
 
policies:
 
require
 
at
 
least
 
1
 
reviewer,
 
no
 
self-approval,
 
linked
 
work
 
item
 
 
5.3
 
Merge
 
vs
 
Rebase
 
—
 
Deep
 
Dive

## Section / Page 37

#
 
Scenario:
 
You
 
are
 
on
 
feature
 
branch,
 
main
 
has
 
new
 
commits
 
 
#
 
MERGE
 
approach:
 
git
 
checkout
 
feature
 
git
 
merge
 
main
 
#
 
Creates
 
a
 
"merge
 
commit"
 
that
 
ties
 
the
 
histories
 
together
 
#
 
History:
 
non-linear,
 
shows
 
true
 
branching
 
history
 
#
 
Result:
 
A---B---C---M
 
(M
 
is
 
merge
 
commit)
 
#
              
\
   
/
 
#
               
D---E
 
(feature
 
commits)
 
 
#
 
REBASE
 
approach:
 
git
 
checkout
 
feature
 
git
 
rebase
 
main
 
#
 
Moves
 
feature
 
commits
 
ON
 
TOP
 
of
 
latest
 
main
 
#
 
History:
 
linear,
 
cleaner,
 
no
 
merge
 
commits
 
#
 
Result:
 
A---B---C---D---E
 
(feature
 
commits
 
replayed
 
on
 
top)
 
 
#
 
GOLDEN
 
RULE:
 
NEVER
 
rebase
 
public/shared
 
branches
 
#
 
Rebase
 
rewrites
 
commit
 
history
 
(new
 
commit
 
IDs)
 
#
 
If
 
others
 
have
 
the
 
old
 
commits,
 
their
 
history
 
diverges
 
=
 
conflicts
 
nightmare
 
 
5.4
 
Advanced
 
Git
 
Commands
 
#
 
INTERACTIVE
 
REBASE
 
—
 
clean
 
up
 
commits
 
before
 
PR
 
git
 
rebase
 
-i
 
HEAD~3
    
#
 
interactive
 
rebase
 
last
 
3
 
commits
 
#
 
Options
 
in
 
editor:
 
pick,
 
squash
 
(s),
 
fixup
 
(f),
 
reword
 
(r),
 
drop
 
(d)
 
 
#
 
SQUASH
 
multiple
 
commits
 
into
 
one
 
git
 
rebase
 
-i
 
HEAD~3
 
#
 
change
 
"pick"
 
to
 
"squash"
 
on
 
all
 
but
 
first
 
commit
 
#
 
→
 
all
 
3
 
commits
 
become
 
1
 
clean
 
commit
 
 
#
 
CHERRY-PICK
 
—
 
apply
 
specific
 
commit
 
from
 
another
 
branch
 
git
 
cherry-pick
 
abc1234
  
#
 
apply
 
that
 
commit
 
to
 
current
 
branch
 
 
#
 
BISECT
 
—
 
find
 
which
 
commit
 
introduced
 
a
 
bug
 
git
 
bisect
 
start
 
git
 
bisect
 
bad
           
#
 
current
 
commit
 
has
 
bug
 
git
 
bisect
 
good
 
v1.0
     
#
 
v1.0
 
was
 
working
 
#
 
Git
 
checks
 
out
 
middle
 
commit
 
—
 
you
 
test
 
and
 
mark
 
good/bad
 
#
 
Binary
 
search
 
finds
 
the
 
exact
 
commit
 
that
 
broke
 
things
 
 
#
 
REFLOG
 
—
 
recover
 
"lost"
 
commits
 
git
 
reflog
               
#
 
shows
 
ALL
 
moves
 
HEAD
 
made
 
git
 
checkout
 
HEAD@{2}
    
#
 
go
 
back
 
to
 
where
 
HEAD
 
was
 
2
 
moves
 
ago
 
 
#
 
GIT
 
HOOKS
 
—
 
run
 
scripts
 
before/after
 
git
 
events
 
#
 
.git/hooks/pre-commit
 
—
 
run
 
linting
 
before
 
every
 
commit
 
#
 
.git/hooks/pre-push
 
—
 
run
 
tests
 
before
 
every
 
push
 
 
#
 
WORKTREE
 
—
 
multiple
 
branches
 
checked
 
out
 
simultaneously
 
git
 
worktree
 
add
 
../feature-branch
 
feature
  
#
 
second
 
working
 
dir

## Section / Page 38

SECTION
 
6:
 
Linux
 
—
 
Complete
 
Deep
 
Guide
 
 
6.1
 
Linux
 
Architecture
 
Layer
 
Component
 
Role
 
Hardware
 
CPU,
 
RAM,
 
Disk,
 
Network
 
Physical
 
resources
 
the
 
OS
 
manages
 
Kernel
 
Linux
 
Kernel
 
Core
 
of
 
OS.
 
Manages
 
hardware,
 
memory,
 
processes,
 
I/O,
 
networking.
 
System
 
Libraries
 
glibc,
 
etc.
 
Pre-written
 
functions
 
programs
 
use
 
to
 
talk
 
to
 
kernel
 
Shell
 
bash,
 
sh,
 
zsh
 
Command
 
interpreter
 
—
 
translates
 
your
 
commands
 
to
 
kernel
 
calls
 
Applications
 
nginx,
 
docker,
 
kubectl
 
User-space
 
programs
 
that
 
run
 
on
 
top
 
of
 
everything
 
Distributions
 
You
 
Should
 
Know
 
Distro
 
Package
 
Manager
 
Used
 
In
 
Ubuntu
 
apt
 
/
 
apt-get
 
Your
 
Azure
 
VM.
 
Most
 
popular
 
for
 
DevOps.
 
RHEL
 
/
 
CentOS
 
yum
 
/
 
dnf
 
Enterprise
 
servers,
 
AWS
 
Amazon
 
Linux
 
Amazon
 
Linux
 
2
 
yum
 
/
 
dnf
 
Default
 
AMI
 
for
 
AWS
 
EC2
 
Alpine
 
Linux
 
apk
 
Docker
 
base
 
images
 
—
 
tiny
 
(~5MB)
 
Debian
 
apt
 
Stable
 
servers,
 
base
 
for
 
Ubuntu
 
 
6.2
 
Complete
 
File
 
System
 
Commands
 
#
 
READING
 
FILES
 
cat
 
file.txt
              
#
 
print
 
entire
 
file
 
cat
 
-n
 
file.txt
           
#
 
with
 
line
 
numbers
 
less
 
file.txt
             
#
 
paginated
 
view
 
(q
 
to
 
quit,
 
/search)
 
head
 
-n
 
20
 
file.txt
       
#
 
first
 
20
 
lines
 
tail
 
-n
 
20
 
file.txt
       
#
 
last
 
20
 
lines
 
tail
 
-f
 
/var/log/syslog
   
#
 
follow
 
file
 
in
 
real
 
time
 
(great
 
for
 
logs)
 
 
#
 
SEARCHING
 
grep
 
"ERROR"
 
/var/log/app.log
               
#
 
search
 
in
 
file
 
grep
 
-r
 
"ERROR"
 
/var/log/
                   
#
 
search
 
recursively
 
grep
 
-i
 
"error"
 
file.txt
                    
#
 
case-insensitive
 
grep
 
-v
 
"DEBUG"
 
file.txt
                    
#
 
invert
 
(lines
 
WITHOUT
 
DEBUG)
 
grep
 
-n
 
"error"
 
file.txt
                    
#
 
show
 
line
 
numbers
 
grep
 
-c
 
"error"
 
file.txt
                    
#
 
count
 
matching
 
lines
 
grep
 
-A
 
3
 
"FATAL"
 
file.txt
                  
#
 
3
 
lines
 
After
 
match
 
grep
 
-B
 
2
 
"FATAL"
 
file.txt
                  
#
 
2
 
lines
 
Before
 
match

## Section / Page 39

#
 
FIND
 
find
 
/
 
-name
 
"*.log"
                        
#
 
find
 
by
 
name
 
find
 
/var/log
 
-type
 
f
 
-mtime
 
-7
             
#
 
files
 
modified
 
<
 
7
 
days
 
ago
 
find
 
/opt
 
-name
 
"*.war"
 
-user
 
azureuser
     
#
 
by
 
name
 
and
 
owner
 
find
 
.
 
-name
 
"*.sh"
 
-exec
 
chmod
 
+x
 
{}
 
\;
   
#
 
find
 
and
 
execute
 
command
 
 
#
 
SORTING
 
AND
 
COUNTING
 
sort
 
file.txt
                               
#
 
sort
 
alphabetically
 
sort
 
-r
 
file.txt
                            
#
 
reverse
 
sort
 
sort
 
-n
 
numbers.txt
                         
#
 
numeric
 
sort
 
uniq
 
sorted.txt
                             
#
 
remove
 
duplicate
 
lines
 
wc
 
-l
 
file.txt
                              
#
 
count
 
lines
 
wc
 
-w
 
file.txt
                              
#
 
count
 
words
 
 
#
 
AWK
 
AND
 
SED
 
awk
 
"{print
 
$1}"
 
file.txt
                   
#
 
print
 
first
 
column
 
awk
 
-F:
 
"{print
 
$1}"
 
/etc/passwd
            
#
 
split
 
by
 
:
 
print
 
first
 
field
 
sed
 
"s/old/new/g"
 
file.txt
                  
#
 
replace
 
all
 
"old"
 
with
 
"new"
 
sed
 
-i
 
"s/8080/7789/g"
 
server.xml
           
#
 
in-place
 
replace
 
(YOUR
 
project)
 
 
6.3
 
Process
 
and
 
Service
 
Management
 
#
 
VIEWING
 
PROCESSES
 
ps
 
aux
                              
#
 
all
 
running
 
processes,
 
all
 
users
 
ps
 
aux
 
|
 
grep
 
java
                  
#
 
find
 
java
 
processes
 
(Tomcat)
 
pgrep
 
tomcat
                        
#
 
get
 
PID
 
of
 
tomcat
 
top
                                 
#
 
live
 
monitor
 
(q
 
to
 
quit)
 
htop
                                
#
 
better
 
live
 
monitor
 
(arrow
 
keys)
 
 
#
 
KILLING
 
PROCESSES
 
kill
 
PID
                            
#
 
SIGTERM
 
—
 
ask
 
process
 
to
 
stop
 
gracefully
 
kill
 
-9
 
PID
                         
#
 
SIGKILL
 
—
 
force
 
stop
 
(cannot
 
ignore)
 
kill
 
-15
 
PID
                        
#
 
SIGTERM
 
explicitly
 
pkill
 
tomcat
                        
#
 
kill
 
by
 
name
 
killall
 
java
                        
#
 
kill
 
all
 
java
 
processes
 
 
#
 
BACKGROUND
 
PROCESSES
 
command
 
&
                           
#
 
run
 
in
 
background
 
nohup
 
./run.sh
 
&
                    
#
 
run
 
in
 
background,
 
survive
 
logout
 
jobs
                                
#
 
list
 
background
 
jobs
 
fg
 
%1
                               
#
 
bring
 
job
 
1
 
to
 
foreground
 
bg
 
%1
                               
#
 
send
 
job
 
to
 
background
 
 
#
 
SYSTEMCTL
 
(your
 
most
 
used
 
service
 
tool)
 
systemctl
 
start
 
apache2
             
#
 
start
 
service
 
systemctl
 
stop
 
apache2
              
#
 
stop
 
service
 
systemctl
 
restart
 
apache2
           
#
 
restart
 
(stop
 
+
 
start)
 
systemctl
 
reload
 
apache2
            
#
 
reload
 
config
 
without
 
restart
 
systemctl
 
status
 
apache2
            
#
 
check
 
status
 
+
 
recent
 
logs
 
systemctl
 
enable
 
apache2
            
#
 
auto-start
 
on
 
boot
 
systemctl
 
disable
 
apache2
           
#
 
do
 
not
 
auto-start
 
systemctl
 
is-active
 
apache2
         
#
 
returns
 
"active"
 
or
 
"inactive"
 
journalctl
 
-u
 
apache2
 
-f
            
#
 
follow
 
logs
 
for
 
specific
 
service
 
journalctl
 
-u
 
apache2
 
--since
 
today
 
#
 
logs
 
since
 
today

## Section / Page 40

#
 
PACKAGE
 
MANAGEMENT
 
#
 
Ubuntu/Debian
 
(apt)
 
apt
 
update
                          
#
 
refresh
 
package
 
list
 
apt
 
upgrade
 
-y
                      
#
 
upgrade
 
all
 
packages
 
apt
 
install
 
nginx
 
-y
                
#
 
install
 
package
 
apt
 
remove
 
nginx
                    
#
 
remove
 
package
 
(keep
 
config)
 
apt
 
purge
 
nginx
                     
#
 
remove
 
package
 
+
 
config
 
files
 
 
#
 
RHEL/CentOS/Amazon
 
Linux
 
(yum)
 
yum
 
update
 
-y
 
yum
 
install
 
nginx
 
-y
 
yum
 
remove
 
nginx
 
 
6.4
 
User
 
and
 
Permission
 
Management
 
#
 
USER
 
MANAGEMENT
 
useradd
 
-m
 
akhil
                    
#
 
create
 
user
 
with
 
home
 
directory
 
useradd
 
-m
 
-s
 
/bin/bash
 
akhil
       
#
 
with
 
bash
 
shell
 
passwd
 
akhil
                        
#
 
set
 
password
 
for
 
user
 
usermod
 
-aG
 
docker
 
akhil
            
#
 
add
 
user
 
to
 
docker
 
group
 
usermod
 
-aG
 
sudo
 
akhil
              
#
 
give
 
sudo
 
access
 
userdel
 
-r
 
akhil
                    
#
 
delete
 
user
 
+
 
home
 
directory
 
id
 
akhil
                            
#
 
show
 
user
 
ID,
 
group
 
memberships
 
groups
 
akhil
                        
#
 
show
 
groups
 
user
 
belongs
 
to
 
su
 
-
 
akhil
                          
#
 
switch
 
to
 
user
 
akhil
 
sudo
 
command
                        
#
 
run
 
command
 
as
 
root
 
 
#
 
KEY
 
FILES
 
cat
 
/etc/passwd
                     
#
 
list
 
of
 
all
 
users
 
(username:x:UID:GID:info:home:shell)
 
cat
 
/etc/group
                      
#
 
list
 
of
 
all
 
groups
 
cat
 
/etc/shadow
                     
#
 
encrypted
 
passwords
 
(root
 
only)
 
 
#
 
PERMISSION
 
MANAGEMENT
 
chmod
 
755
 
file
                      
#
 
rwxr-xr-x
 
chmod
 
+x
 
script.sh
                  
#
 
add
 
execute
 
for
 
everyone
 
chmod
 
u+w,g-w
 
file
                  
#
 
add
 
write
 
for
 
user,
 
remove
 
for
 
group
 
chown
 
azureuser:azureuser
 
file
      
#
 
change
 
owner
 
and
 
group
 
chown
 
-R
 
azureuser
 
/opt/tomcat1
     
#
 
recursive
 
(YOUR
 
project
 
fix)
 
 
#
 
SPECIAL
 
PERMISSIONS
 
setuid
 
(s
 
on
 
owner
 
execute)
         
#
 
file
 
runs
 
as
 
file
 
owner,
 
not
 
caller
 
setgid
 
(s
 
on
 
group
 
execute)
         
#
 
file
 
runs
 
as
 
file
 
group
 
sticky
 
bit
 
(t
 
on
 
others
 
execute)
    
#
 
only
 
file
 
owner
 
can
 
delete
 
(used
 
on
 
/tmp)
 
 
#
 
ULIMIT
 
(YOUR
 
PROJECT)
 
ulimit
 
-n
                           
#
 
check
 
current
 
open
 
file
 
limit
 
ulimit
 
-n
 
65535
                     
#
 
increase
 
for
 
current
 
session
 
ulimit
 
-u
                           
#
 
max
 
processes
 
 
#
 
PERMANENT
 
ULIMIT
 
(edit
 
/etc/security/limits.conf)
 
#
 
azureuser
 
soft
 
nofile
 
65535
 
#
 
azureuser
 
hard
 
nofile
 
65535
 
 
6.5
 
Networking
 
Commands

## Section / Page 41

#
 
NETWORK
 
INFORMATION
 
ip
 
addr
                             
#
 
show
 
network
 
interfaces
 
+
 
IPs
 
ip
 
addr
 
show
 
eth0
                   
#
 
specific
 
interface
 
ip
 
route
                            
#
 
routing
 
table
 
ip
 
route
 
show
 
default
               
#
 
default
 
gateway
 
hostname
 
-I
                         
#
 
show
 
all
 
IPs
 
 
#
 
CONNECTIVITY
 
TESTING
 
ping
 
8.8.8.8
                        
#
 
test
 
connectivity
 
ping
 
-c
 
4
 
google.com
                
#
 
send
 
only
 
4
 
packets
 
traceroute
 
google.com
               
#
 
trace
 
route
 
to
 
host
 
curl
 
-I
 
https://google.com
          
#
 
HTTP
 
headers
 
only
 
curl
 
-v
 
https://google.com
          
#
 
verbose
 
—
 
shows
 
TLS
 
handshake
 
wget
 
https://example.com/file.zip
   
#
 
download
 
file
 
 
#
 
PORT
 
AND
 
SOCKET
 
INFO
 
ss
 
-tulpn
                           
#
 
show
 
listening
 
ports
 
+
 
process
 
names
 
ss
 
-tulpn
 
|
 
grep
 
:80
                
#
 
who
 
is
 
listening
 
on
 
port
 
80
 
ss
 
-tulpn
 
|
 
grep
 
:7789
              
#
 
check
 
Tomcat
 
1
 
(YOUR
 
project)
 
netstat
 
-tulpn
                      
#
 
older
 
alternative
 
to
 
ss
 
 
#
 
FIREWALL
 
(UFW
 
—
 
YOUR
 
PROJECT)
 
ufw
 
status
                          
#
 
show
 
firewall
 
rules
 
ufw
 
allow
 
80
                        
#
 
allow
 
HTTP
 
(YOUR
 
public
 
port)
 
ufw
 
allow
 
22
                        
#
 
allow
 
SSH
 
ufw
 
deny
 
7789
                       
#
 
block
 
Tomcat
 
1
 
from
 
public
 
(YOUR
 
project)
 
ufw
 
enable
                          
#
 
enable
 
firewall
 
ufw
 
disable
                         
#
 
disable
 
firewall
 
 
#
 
SSH
 
ssh
 
-i
 
~/.ssh/key.pem
 
azureuser@20.1.2.3
    
#
 
SSH
 
into
 
server
 
ssh-keygen
 
-t
 
rsa
 
-b
 
4096
                   
#
 
generate
 
SSH
 
key
 
pair
 
ssh-copy-id
 
user@server
                      
#
 
copy
 
public
 
key
 
to
 
server
 
scp
 
file.txt
 
user@server:/path/
              
#
 
copy
 
file
 
to
 
remote
 
server
 
scp
 
-r
 
dir/
 
user@server:/path/
               
#
 
copy
 
directory
 
recursively

## Section / Page 42

SECTION
 
7:
 
Terraform
 
—
 
Complete
 
Deep
 
Guide
 
 
7.1
 
Terraform
 
Core
 
Concepts
 
Concept
 
Explanation
 
Desired
 
State
 
You
 
declare
 
WHAT
 
infrastructure
 
you
 
want.
 
Terraform
 
determines
 
HOW
 
to
 
create
 
it.
 
State
 
File
 
terraform.tfstate
 
tracks
 
what
 
Terraform
 
has
 
created.
 
The
 
"ground
 
truth"
 
of
 
your
 
infrastructure.
 
Plan
 
Terraform
 
compares
 
desired
 
state
 
(your
 
.tf
 
files)
 
vs
 
actual
 
state
 
(tfstate
 
+
 
real
 
infra)
 
→
 
shows
 
delta
 
Provider
 
Plugin
 
that
 
knows
 
how
 
to
 
talk
 
to
 
AWS/Azure/GCP
 
APIs.
 
Downloads
 
via
 
terraform
 
init.
 
Resource
 
A
 
piece
 
of
 
infrastructure
 
(EC2
 
instance,
 
S3
 
bucket,
 
VPC,
 
security
 
group).
 
Data
 
Source
 
Read-only
 
query
 
of
 
existing
 
infrastructure
 
(find
 
existing
 
VPC
 
ID,
 
latest
 
AMI,
 
etc.)
 
Module
 
Reusable
 
group
 
of
 
resources.
 
Like
 
a
 
function
 
—
 
write
 
once,
 
use
 
everywhere.
 
Variable
 
Input
 
parameters
 
to
 
customize
 
your
 
Terraform
 
code.
 
Output
 
Values
 
to
 
expose
 
after
 
apply
 
(IP
 
address,
 
ARN,
 
etc.)
 
Workspace
 
Separate
 
state
 
per
 
environment
 
(dev,
 
staging,
 
prod)
 
using
 
same
 
code.
 
 
7.2
 
Complete
 
Terraform
 
Example
 
#
 
providers.tf
 
terraform
 
{
 
  
required_version
 
=
 
">=
 
1.5"
 
  
required_providers
 
{
 
    
aws
 
=
 
{
 
      
source
  
=
 
"hashicorp/aws"
 
      
version
 
=
 
"~>
 
5.0"
 
    
}
 
  
}
 
  
backend
 
"s3"
 
{
                    
#
 
remote
 
state
 
for
 
teams
 
    
bucket
         
=
 
"my-tf-state"
 
    
key
            
=
 
"prod/terraform.tfstate"
 
    
region
         
=
 
"us-east-1"
 
    
dynamodb_table
 
=
 
"tf-state-lock"
   
#
 
prevents
 
concurrent
 
applies
 
  
}
 
}
 
 
provider
 
"aws"
 
{
 
  
region
 
=
 
var.aws_region
 
}
 
 
#
 
variables.tf

## Section / Page 43

variable
 
"aws_region"
 
{
 
  
description
 
=
 
"AWS
 
region
 
to
 
deploy
 
to"
 
  
type
        
=
 
string
 
  
default
     
=
 
"us-east-1"
 
}
 
 
variable
 
"instance_type"
 
{
 
  
description
 
=
 
"EC2
 
instance
 
type"
 
  
type
        
=
 
string
 
  
default
     
=
 
"t2.micro"
 
}
 
 
#
 
main.tf
 
resource
 
"aws_vpc"
 
"main"
 
{
 
  
cidr_block
 
=
 
"10.0.0.0/16"
 
  
tags
 
=
 
{
 
Name
 
=
 
"main-vpc"
 
}
 
}
 
 
resource
 
"aws_subnet"
 
"public"
 
{
 
  
vpc_id
            
=
 
aws_vpc.main.id
    
#
 
reference
 
another
 
resource
 
  
cidr_block
        
=
 
"10.0.1.0/24"
 
  
availability_zone
 
=
 
"us-east-1a"
 
  
tags
 
=
 
{
 
Name
 
=
 
"public-subnet"
 
}
 
}
 
 
resource
 
"aws_instance"
 
"web"
 
{
 
  
ami
           
=
 
data.aws_ami.ubuntu.id
  
#
 
from
 
data
 
source
 
  
instance_type
 
=
 
var.instance_type
       
#
 
from
 
variable
 
  
subnet_id
     
=
 
aws_subnet.public.id
 
  
tags
 
=
 
{
 
Name
 
=
 
"WebServer"
 
}
 
}
 
 
#
 
Data
 
source
 
—
 
read
 
existing
 
data
 
data
 
"aws_ami"
 
"ubuntu"
 
{
 
  
most_recent
 
=
 
true
 
  
filter
 
{
 
    
name
   
=
 
"name"
 
    
values
 
=
 
["ubuntu/images/hvm-ssd/ubuntu-22.04-amd64-server-*"]
 
  
}
 
  
owners
 
=
 
["099720109477"]
  
#
 
Canonical
 
(Ubuntu
 
publisher)
 
}
 
 
#
 
outputs.tf
 
output
 
"instance_public_ip"
 
{
 
  
description
 
=
 
"Public
 
IP
 
of
 
web
 
server"
 
  
value
       
=
 
aws_instance.web.public_ip
 
}
 
 
7.3
 
Terraform
 
State
 
Deep
 
Dive
 
The
 
state
 
file
 
is
 
the
 
most
 
critical
 
piece
 
of
 
Terraform.
 
It
 
maps
 
your
 
configuration
 
to
 
real-world
 
resources.
 
•
 
✅
 
Always
 
store
 
state
 
in
 
S3
 
+
 
DynamoDB
 
locking
 
for
 
teams
 
•
 
✅
 
Never
 
edit
 
terraform.tfstate
 
manually
 
—
 
use
 
terraform
 
state
 
commands
 
•
 
✅
 
Add
 
terraform.tfstate
 
to
 
.gitignore
 
—
 
never
 
commit
 
state
 
to
 
Git
 
•
 
❌
 
NEVER
 
delete
 
the
 
state
 
file
 
—
 
you'll
 
lose
 
track
 
of
 
all
 
resources

## Section / Page 44

#
 
STATE
 
MANAGEMENT
 
COMMANDS
 
terraform
 
state
 
list
                        
#
 
list
 
all
 
tracked
 
resources
 
terraform
 
state
 
show
 
aws_instance.web
       
#
 
show
 
specific
 
resource
 
state
 
terraform
 
state
 
rm
 
aws_instance.web
         
#
 
remove
 
from
 
state
 
(does
 
NOT
 
destroy
 
real
 
resource)
 
terraform
 
state
 
mv
 
aws_instance.old
 
aws_instance.new
  
#
 
rename
 
in
 
state
 
terraform
 
import
 
aws_instance.web
 
i-1234567890
  
#
 
import
 
existing
 
resource
 
terraform
 
refresh
                            
#
 
sync
 
state
 
with
 
real
 
infra
 
 
7.4
 
Modules
 
Modules
 
make
 
Terraform
 
DRY
 
(Don't
 
Repeat
 
Yourself).
 
Create
 
once,
 
use
 
with
 
different
 
variables
 
for
 
each
 
environment.
 
#
 
modules/ec2/main.tf
 
(reusable
 
module)
 
resource
 
"aws_instance"
 
"this"
 
{
 
  
ami
           
=
 
var.ami_id
 
  
instance_type
 
=
 
var.instance_type
 
  
tags
          
=
 
var.tags
 
}
 
 
#
 
Root
 
main.tf
 
—
 
using
 
the
 
module
 
module
 
"web_server"
 
{
 
  
source
        
=
 
"./modules/ec2"
 
  
ami_id
        
=
 
"ami-12345678"
 
  
instance_type
 
=
 
"t2.micro"
 
  
tags
          
=
 
{
 
Name
 
=
 
"WebServer",
 
Env
 
=
 
"prod"
 
}
 
}
 
 
module
 
"db_server"
 
{
 
  
source
        
=
 
"./modules/ec2"
 
  
ami_id
        
=
 
"ami-12345678"
 
  
instance_type
 
=
 
"t2.large"
    
#
 
different
 
size
 
for
 
DB
 
  
tags
          
=
 
{
 
Name
 
=
 
"DBServer",
 
Env
 
=
 
"prod"
 
}
 
}

## Section / Page 45

SECTION
 
8:
 
Azure
 
DevOps
 
—
 
Complete
 
Deep
 
Guide
 
THIS
 
IS
 
YOUR
 
STRONGEST
 
AREA!
 
You
 
have
 
hands-on
 
experience
 
with
 
Azure
 
Boards,
 
Repos,
 
and
 
Pipelines.
 
Connect
 
every
 
answer
 
to
 
your
 
real
 
project
 
experience.
 
Be
 
confident
 
here.
 
 
8.1
 
Azure
 
Boards
 
—
 
Deep
 
Dive
 
Agile
 
Process
 
—
 
Work
 
Item
 
Hierarchy
 
Level
 
Work
 
Item
 
Description
 
Your
 
Example
 
1
 
(High
est)
 
Epic
 
Large
 
business
 
objective
 
spanning
 
multiple
 
sprints
 
Build
 
Production-Grade
 
CI/CD
 
Infrastructure
 
2
 
Feature
 
Functional
 
component
 
delivering
 
business
 
value
 
Automated
 
Multi-Stage
 
Tomcat
 
Deployment
 
3
 
User
 
Story
 
Requirement
 
from
 
user
 
perspective.
 
"As
 
a
 
[role],
 
I
 
want
 
[feature]
 
so
 
that
 
[benefit]."
 
As
 
a
 
developer,
 
I
 
want
 
code
 
auto-deployed
 
to
 
Tomcat
 
when
 
I
 
push
 
to
 
main
 
4
 
Task
 
Technical
 
implementation
 
step.
 
~1-4
 
hours
 
each.
 
Configure
 
azure-pipelines.yml
 
with
 
4
 
stages
 
4
 
Bug
 
Defect
 
to
 
investigate
 
and
 
fix.
 
Has
 
severity
 
+
 
priority.
 
Pipeline
 
not
 
triggering
 
—
 
pushed
 
to
 
feature
 
not
 
main
 
 
Boards
 
Views
 
View
 
What
 
It
 
Shows
 
Use
 
Case
 
Boards
 
(Kanban)
 
Cards
 
in
 
columns:
 
New
 
→
 
Active
 
→
 
Resolved
 
→
 
Closed.
 
Drag
 
and
 
drop.
 
Day-to-day
 
work
 
tracking
 
Backlogs
 
Prioritized
 
list
 
of
 
all
 
work
 
items.
 
Estimate
 
story
 
points/effort.
 
Sprint
 
planning,
 
backlog
 
grooming
 
Sprints
 
Work
 
planned
 
for
 
current
 
sprint.
 
Sprint
 
burndown
 
chart.
 
Active
 
sprint
 
management
 
Queries
 
Custom
 
filtered
 
views.
 
Save
 
and
 
share.
 
Find
 
all
 
bugs
 
assigned
 
to
 
you,
 
all
 
open
 
features,
 
etc.
 
Dashboards
 
Widgets:
 
Sprint
 
burndown,
 
build
 
history,
 
work
 
item
 
charts.
 
Team
 
visibility,
 
management
 
reports
 
 
8.2
 
Azure
 
Repos
 
—
 
Deep
 
Dive
 
Branch
 
Policies
 
(Production
 
Setup)
 
•
 
Minimum
 
number
 
of
 
reviewers
 
—
 
require
 
1-2
 
approvals
 
before
 
merge
 
•
 
Prevent
 
self-approval
 
—
 
reviewer
 
cannot
 
approve
 
their
 
own
 
PR
 
•
 
Require
 
linked
 
work
 
item
 
—
 
every
 
PR
 
must
 
reference
 
an
 
Epic/Feature/Task

## Section / Page 46

•
 
Build
 
validation
 
—
 
run
 
CI
 
pipeline
 
successfully
 
before
 
merge
 
is
 
allowed
 
•
 
Require
 
up-to-date
 
branch
 
—
 
feature
 
branch
 
must
 
be
 
current
 
with
 
main
 
 
PR
 
Template
 
Setup
 
(Your
 
Project)
 
#
 
Create
 
this
 
file
 
in
 
your
 
repo:
 
#
 
.azuredevops/pull_request_template.md
 
 
##
 
What
 
type
 
of
 
PR
 
is
 
this?
 
-
 
[
 
]
 
Feature
 
-
 
[
 
]
 
Bugfix
 
-
 
[
 
]
 
Enhancement
 
-
 
[
 
]
 
Configuration
 
 
##
 
Description
 
of
 
changes
 
Explain
 
what
 
was
 
changed
 
and
 
why.
 
 
##
 
Related
 
Work
 
Item
 
Closes
 
#(work
 
item
 
ID)
 
 
##
 
Testing
 
done
 
Describe
 
how
 
you
 
tested
 
this.
 
 
##
 
Post-deployment
 
tasks
 
Any
 
manual
 
steps
 
needed
 
after
 
merge?
 
 
#
 
IMPORTANT:
 
#
 
1.
 
Folder
 
must
 
be
 
named:
 
.azuredevops
 
(exactly)
 
#
 
2.
 
File
 
must
 
be
 
named:
 
pull_request_template.md
 
(exactly)
 
#
 
3.
 
Commit
 
to
 
the
 
DEFAULT
 
(main)
 
branch
 
—
 
only
 
then
 
does
 
it
 
auto-load
 
 
8.3
 
Azure
 
Pipelines
 
—
 
Complete
 
Guide
 
Pipeline
 
Variables
 
—
 
All
 
Types
 
Variable
 
Type
 
Where
 
Defined
 
Security
 
Use
 
Case
 
Inline
 
(YAML)
 
In
 
azure-pipelines.yml
 
Not
 
secure
 
—
 
visible
 
in
 
repo
 
Non-sensitive:
 
app
 
name,
 
timeout
 
values
 
Pipeline
 
UI
 
Pipeline
 
→
 
Edit
 
→
 
Variables
 
tab
 
Can
 
mark
 
as
 
"secret"
 
(masked
 
in
 
logs)
 
Env-specific
 
values
 
per
 
pipeline
 
Variable
 
Groups
 
Pipelines
 
→
 
Library
 
→
 
Variable
 
Groups
 
Can
 
link
 
to
 
Key
 
Vault
 
Shared
 
across
 
multiple
 
pipelines
 
Azure
 
Key
 
Vault
 
Azure
 
Key
 
Vault
 
(external)
 
Fully
 
encrypted,
 
RBAC
 
controlled
 
Database
 
passwords,
 
API
 
keys,
 
certificates
 
 
Environments
 
and
 
Approvals
 
Environments
 
provide
 
deployment
 
targets
 
with
 
approval
 
gates
 
and
 
history
 
tracking.
 
#
 
In
 
YAML:
 
deploy
 
to
 
"production"
 
environment
 
stages:
 
-
 
stage:
 
Deploy_Production

## Section / Page 47

jobs:
 
  
-
 
deployment:
 
DeployProd
        
#
 
deployment
 
job
 
(not
 
regular
 
job)
 
    
environment:
 
production
        
#
 
must
 
exist
 
in
 
Azure
 
DevOps
 
Environments
 
    
strategy:
 
      
runOnce:
 
        
deploy:
 
          
steps:
 
          
-
 
script:
 
echo
 
"Deploying
 
to
 
production"
 
 
#
 
In
 
Azure
 
DevOps
 
portal:
 
#
 
Pipelines
 
→
 
Environments
 
→
 
production
 
→
 
Approvals
 
and
 
checks
 
#
 
Add:
 
"Required
 
approvers"
 
—
 
pipeline
 
pauses
 
until
 
someone
 
approves
 
#
 
Great
 
for:
 
preventing
 
accidental
 
prod
 
deployments
 
 
Multi-Stage
 
Pipeline
 
with
 
Dependencies
 
trigger:
 
-
 
main
 
 
pool:
 
  
name:
 
Default
 
  
demands:
 
  
-
 
Agent.Name
 
-equals
 
myagent
 
 
variables:
 
  
WAR_PATH:
 
target/myapp.war
 
  
TOMCAT1_WEBAPPS:
 
/opt/tomcat1/webapps/
 
  
TOMCAT2_WEBAPPS:
 
/opt/tomcat2/webapps/
 
 
stages:
 
-
 
stage:
 
Build
 
  
displayName:
 
"Build
 
Java
 
WAR"
 
  
jobs:
 
  
-
 
job:
 
BuildJob
 
    
steps:
 
    
-
 
checkout:
 
self
 
    
-
 
script:
 
|
 
        
mvn
 
clean
 
package
 
-DskipTests
 
        
echo
 
"WAR
 
file
 
size:
 
$(du
 
-sh
 
$(WAR_PATH))"
 
      
displayName:
 
"Maven
 
Build"
 
 
-
 
stage:
 
Test
 
  
displayName:
 
"Run
 
Tests"
 
  
dependsOn:
 
Build
 
  
condition:
 
succeeded()
 
  
jobs:
 
  
-
 
job:
 
TestJob
 
    
steps:
 
    
-
 
script:
 
mvn
 
test
 
      
displayName:
 
"Run
 
Unit
 
Tests"
 
 
-
 
stage:
 
Deploy_Tomcat1
 
  
displayName:
 
"Deploy
 
to
 
Tomcat
 
1
 
(Port
 
7789)"
 
  
dependsOn:
 
Test
 
  
condition:
 
succeeded()
 
  
jobs:
 
  
-
 
job:
 
Deploy1

## Section / Page 48

steps:
 
    
-
 
script:
 
|
 
        
cp
 
$(WAR_PATH)
 
$(TOMCAT1_WEBAPPS)
 
        
/opt/tomcat1/bin/shutdown.sh
 
        
sleep
 
5
 
        
/opt/tomcat1/bin/startup.sh
 
        
sleep
 
10
 
        
curl
 
-f
 
http://localhost:7789/myapp/
 
||
 
exit
 
1
 
      
displayName:
 
"Deploy
 
+
 
Verify
 
Tomcat
 
1"
 
 
-
 
stage:
 
Deploy_Tomcat2
 
  
displayName:
 
"Deploy
 
to
 
Tomcat
 
2
 
(Port
 
8888)"
 
  
dependsOn:
 
Deploy_Tomcat1
 
  
condition:
 
succeeded()
 
  
jobs:
 
  
-
 
job:
 
Deploy2
 
    
steps:
 
    
-
 
script:
 
|
 
        
cp
 
$(WAR_PATH)
 
$(TOMCAT2_WEBAPPS)
 
        
/opt/tomcat1/bin/shutdown.sh
 
        
sleep
 
5
 
        
/opt/tomcat2/bin/startup.sh
 
        
sleep
 
10
 
        
curl
 
-f
 
http://localhost:8888/myapp/
 
||
 
exit
 
1
 
      
displayName:
 
"Deploy
 
+
 
Verify
 
Tomcat
 
2"

## Section / Page 49

SECTION
 
9:
 
Your
 
3
 
Projects
 
—
 
Complete
 
Documentation
 
These
 
ARE
 
your
 
interview.
 
Interviewers
 
will
 
spend
 
60-70%
 
of
 
the
 
time
 
on
 
your
 
projects.
 
Know
 
every
 
component,
 
every
 
decision,
 
every
 
trade-off.
 
Own
 
this
 
section
 
completely.
 
 
PROJECT
 
1:
 
Azure
 
DevOps
 
+
 
Reverse
 
Proxy
 
+
 
Tomcat
 
+
 
LGTM
 
Complete
 
Architecture
 
CODE
 
FLOW:
 
Developer
 
writes
 
code
 
(Java
 
Web
 
App)
 
    
|
 
    
v
 
(git
 
push
 
to
 
main
 
branch)
 
Azure
 
Repos
 
(Git
 
repository)
 
    
|
 
    
v
 
(webhook
 
triggers
 
pipeline)
 
Azure
 
DevOps
 
Pipeline
 
    
|--
 
Stage
 
1:
 
BUILD
 
    
|
   
mvn
 
clean
 
package
 
→
 
creates
 
myapp.war
 
    
|
 
    
|--
 
Stage
 
2:
 
TEST
 
    
|
   
mvn
 
test
 
→
 
runs
 
unit
 
tests
 
    
|
 
    
|--
 
Stage
 
3:
 
DEPLOY
 
TOMCAT
 
1
 
(Port
 
7789)
 
    
|
   
cp
 
myapp.war
 
/opt/tomcat1/webapps/
 
    
|
   
restart
 
Tomcat
 
1
 
    
|
 
    
|--
 
Stage
 
4:
 
DEPLOY
 
TOMCAT
 
2
 
(Port
 
8888)
 
        
cp
 
myapp.war
 
/opt/tomcat2/webapps/
 
        
restart
 
Tomcat
 
2
 
 
TRAFFIC
 
FLOW:
 
User
 
browser
 
    
|
 
    
v
 
HTTP
 
request
 
to
 
http://<VM-IP>/project1
 
Azure
 
NSG
 
(allows
 
port
 
80
 
only)
 
    
|
 
    
v
 
Port
 
80
 
Apache
 
HTTP
 
Server
 
(Reverse
 
Proxy)
 
    
|
 
Reads
 
ProxyPass
 
config:
 
    
|--
 
/project1
 
→
 
http://127.0.0.1:7789/project1
 
    
|--
 
/project2
 
→
 
http://127.0.0.1:8888/project2
 
    
|
 
    
v
 
Forwards
 
internally
 
to
 
port
 
7789
 
Tomcat
 
1
 
(Port
 
7789
 
—
 
not
 
exposed
 
publicly)
 
    
|
 
    
v
 
Processes
 
request
 
    
|
 
Reads/writes
 
PostgreSQL
 
DB
 
    
|
 
    
v
 
Response
 
back
 
through
 
Apache
 
→
 
User
 
 
UFW
 
FIREWALL:
 
Port
 
80
 
OPEN
   
—
 
public
 
access
 
via
 
Apache
 
Port
 
22
 
OPEN
   
—
 
SSH
 
for
 
admin
 
access
 
Port
 
7789
 
CLOSED
 
—
 
Tomcat
 
1
 
internal
 
only
 
Port
 
8888
 
CLOSED
 
—
 
Tomcat
 
2
 
internal
 
only

## Section / Page 50

Port
 
5432
 
CLOSED
 
—
 
PostgreSQL
 
internal
 
only
 
 
Complete
 
Tomcat
 
Setup
 
Steps
 
#
 
1.
 
Install
 
Java
 
and
 
Apache
 
sudo
 
apt
 
update
 
&&
 
sudo
 
apt
 
upgrade
 
-y
 
sudo
 
apt
 
install
 
default-jdk
 
apache2
 
-y
 
 
#
 
2.
 
Download
 
Tomcat
 
cd
 
/tmp
 
wget
 
https://archive.apache.org/dist/tomcat/tomcat-11/v11.0.18/bin/apache-tomcat-11.0.18
.tar.gz
 
tar
 
-xvf
 
apache-tomcat-11.0.18.tar.gz
 
 
#
 
3.
 
Create
 
TWO
 
SEPARATE
 
instances
 
(physical
 
copies
 
—
 
NOT
 
symlinks)
 
sudo
 
mv
 
apache-tomcat-11.0.18
 
/opt/tomcat1
 
sudo
 
cp
 
-r
 
/opt/tomcat1
 
/opt/tomcat2
 
 
#
 
4.
 
Fix
 
ownership
 
(CRITICAL
 
—
 
extract
 
with
 
sudo
 
sets
 
root
 
as
 
owner)
 
sudo
 
chown
 
-R
 
azureuser:azureuser
 
/opt/tomcat1
 
/opt/tomcat2
 
 
#
 
5.
 
Give
 
execute
 
permission
 
chmod
 
+x
 
/opt/tomcat1/bin/*.sh
 
chmod
 
+x
 
/opt/tomcat2/bin/*.sh
 
 
#
 
6.
 
Configure
 
Tomcat
 
1
 
ports
 
in
 
server.xml
 
#
 
/opt/tomcat1/conf/server.xml:
 
#
   
<Server
 
port="8005"
 
...>
    
(shutdown
 
port
 
—
 
default)
 
#
   
<Connector
 
port="7789"
 
...>
 
(HTTP
 
connector)
 
 
#
 
7.
 
Configure
 
Tomcat
 
2
 
ports
 
in
 
server.xml
 
(must
 
be
 
DIFFERENT)
 
#
 
/opt/tomcat2/conf/server.xml:
 
#
   
<Server
 
port="8006"
 
...>
    
(different
 
shutdown
 
port)
 
#
   
<Connector
 
port="8888"
 
...>
 
(different
 
HTTP
 
connector)
 
 
#
 
8.
 
Deploy
 
applications
 
via
 
symbolic
 
links
 
mkdir
 
-p
 
/opt/project1
 
/opt/project2
 
echo
 
"<h1>Project
 
1
 
Works</h1>"
 
>
 
/opt/project1/index.html
 
echo
 
"<h1>Project
 
2
 
Works</h1>"
 
>
 
/opt/project2/index.html
 
ln
 
-s
 
/opt/project1
 
/opt/tomcat1/webapps/project1
 
ln
 
-s
 
/opt/project2
 
/opt/tomcat2/webapps/project2
 
 
#
 
9.
 
Start
 
both
 
instances
 
/opt/tomcat1/bin/startup.sh
 
/opt/tomcat2/bin/startup.sh
 
 
#
 
10.
 
Verify
 
running
 
curl
 
-I
 
http://localhost:7789/project1/
 
curl
 
-I
 
http://localhost:8888/project2/
 
 
Apache
 
Reverse
 
Proxy
 
Complete
 
Setup
 
#
 
Enable
 
proxy
 
modules
 
sudo
 
a2enmod
 
proxy
 
proxy_http

## Section / Page 51

#
 
Create
 
virtual
 
host
 
config
 
sudo
 
nano
 
/etc/apache2/sites-available/my-proxy.conf
 
 
<VirtualHost
 
*:80>
 
    
ProxyPreserveHost
 
On
 
 
    
#
 
Project
 
1
 
→
 
Tomcat
 
1
 
(Port
 
7789)
 
    
ProxyPass
 
/project1
 
http://127.0.0.1:7789/project1
 
    
ProxyPassReverse
 
/project1
 
http://127.0.0.1:7789/project1
 
 
    
#
 
Project
 
2
 
→
 
Tomcat
 
2
 
(Port
 
8888)
 
    
ProxyPass
 
/project2
 
http://127.0.0.1:8888/project2
 
    
ProxyPassReverse
 
/project2
 
http://127.0.0.1:8888/project2
 
 
    
ErrorLog
 
${APACHE_LOG_DIR}/proxy-error.log
 
    
CustomLog
 
${APACHE_LOG_DIR}/proxy-access.log
 
combined
 
</VirtualHost>
 
 
#
 
Enable
 
site,
 
disable
 
default
 
sudo
 
a2dissite
 
000-default.conf
 
sudo
 
a2ensite
 
my-proxy.conf
 
sudo
 
systemctl
 
restart
 
apache2
 
 
LGTM
 
Stack
 
Complete
 
Setup
 
#
 
1.
 
Install
 
Grafana
 
sudo
 
apt-get
 
install
 
-y
 
apt-transport-https
 
software-properties-common
 
wget
 
wget
 
-q
 
-O
 
-
 
https://apt.grafana.com/gpg.key
 
|
 
gpg
 
--dearmor
 
|
 
sudo
 
tee
 
/etc/apt/keyrings/grafana.gpg
 
>
 
/dev/null
 
echo
 
"deb
 
[signed-by=/etc/apt/keyrings/grafana.gpg]
 
https://apt.grafana.com
 
stable
 
main"
 
|
 
sudo
 
tee
 
/etc/apt/sources.list.d/grafana.list
 
sudo
 
apt-get
 
update
 
&&
 
sudo
 
apt-get
 
install
 
-y
 
grafana
 
sudo
 
systemctl
 
enable
 
grafana-server
 
sudo
 
systemctl
 
start
 
grafana-server
 
 
#
 
2.
 
Install
 
Loki
 
sudo
 
mkdir
 
-p
 
/opt/loki
 
&&
 
cd
 
/opt/loki
 
sudo
 
curl
 
-L
 
-O
 
https://github.com/grafana/loki/releases/download/v2.9.3/loki-linux-amd64.zip
 
sudo
 
apt
 
install
 
unzip
 
-y
 
&&
 
sudo
 
unzip
 
loki-linux-amd64.zip
 
sudo
 
chmod
 
+x
 
loki-linux-amd64
 
sudo
 
mkdir
 
-p
 
/tmp/loki/chunks
 
/tmp/loki/rules
 
sudo
 
chmod
 
-R
 
777
 
/tmp/loki
 
 
#
 
3.
 
Install
 
Promtail
 
sudo
 
curl
 
-L
 
-O
 
https://github.com/grafana/loki/releases/download/v2.9.3/promtail-linux-amd64.zip
 
sudo
 
unzip
 
promtail-linux-amd64.zip
 
sudo
 
chmod
 
+x
 
promtail-linux-amd64
 
sudo
 
mv
 
promtail-linux-amd64
 
/usr/local/bin/promtail
 
 
#
 
4.
 
Promtail
 
config
 
(/etc/loki/promtail-config.yaml)
 
server:
 
  
http_listen_port:
 
9080
 
positions:
 
  
filename:
 
/tmp/positions.yaml

## Section / Page 52

clients:
 
  
-
 
url:
 
http://localhost:3100/loki/api/v1/push
 
scrape_configs:
 
-
 
job_name:
 
apache
 
  
static_configs:
 
  
-
 
targets:
 
[localhost]
 
    
labels:
 
      
job:
 
apache
 
      
__path__:
 
/var/log/apache2/*.log
 
-
 
job_name:
 
tomcat
 
  
static_configs:
 
  
-
 
targets:
 
[localhost]
 
    
labels:
 
      
job:
 
tomcat
 
      
__path__:
 
/opt/tomcat*/logs/*.out
 
 
#
 
5.
 
Start
 
Loki
 
and
 
Promtail
 
sudo
 
/opt/loki/loki-linux-amd64
 
-config.file=/etc/loki/loki-config.yaml
 
&
 
sudo
 
/usr/local/bin/promtail
 
-config.file=/etc/loki/promtail-config.yaml
 
&
 
 
#
 
6.
 
Verify
 
curl
 
http://localhost:3100/ready
   
#
 
should
 
return
 
"ready"
 
 
#
 
7.
 
Access
 
Grafana:
 
http://<VM-IP>:3000
  
(admin/admin)
 
#
 
Add
 
Loki
 
data
 
source:
 
Connections
 
→
 
Data
 
Sources
 
→
 
Loki
 
→
 
URL:
 
http://localhost:3100
 
 
#
 
RESTART
 
AFTER
 
VM
 
REBOOT:
 
sudo
 
systemctl
 
start
 
grafana-server
 
sudo
 
/opt/loki/loki-linux-amd64
 
-config.file=/etc/loki/loki-config.yaml
 
&
 
sudo
 
/usr/local/bin/promtail
 
-config.file=/etc/loki/promtail-config.yaml
 
&
 
 
Complete
 
Troubleshooting
 
Guide
 
—
 
Project
 
1
 
Error/Problem
 
Root
 
Cause
 
Solution
 
403
 
Access
 
Denied
 
on
 
Tomcat
 
RemoteAddrValve
 
blocks
 
all
 
IPs
 
except
 
localhost
 
Comment
 
out
 
the
 
Valve
 
block
 
in
 
/opt/tomcat1/webapps/<app>/META-INF/context.x
ml,
 
restart
 
Tomcat
 
404
 
Not
 
Found
 
Symlink
 
points
 
to
 
wrong
 
folder
 
or
 
nesting
 
issue
 
ls
 
-la
 
/opt/tomcat1/webapps/project1
 
—
 
verify
 
it
 
points
 
to
 
folder
 
containing
 
index.html
 
directly
 
Permission
 
Denied
 
entering
 
/opt/tomcat1
 
Files
 
owned
 
by
 
root
 
(extracted
 
with
 
sudo)
 
sudo
 
chown
 
-R
 
azureuser:azureuser
 
/opt/tomcat1
 
/opt/tomcat2
 
Port
 
conflict
 
—
 
both
 
Tomcats
 
same
 
port
 
server.xml
 
shutdown
 
port
 
conflict
 
(both
 
on
 
8005)
 
Change
 
Tomcat
 
2
 
server.xml:
 
Server
 
port="8006"
 
Pipeline
 
not
 
triggering
 
Pushed
 
to
 
feature
 
branch
 
not
 
main
 
git
 
checkout
 
main;
 
git
 
merge
 
feature;
 
git
 
push
 
origin
 
main
 
Git
 
authentication
 
failed
 
Azure
 
DevOps
 
blocks
 
password
 
login
 
Use
 
PAT
 
token
 
as
 
Git
 
password
 
Agent
 
Offline
 
run.sh
 
not
 
running
 
cd
 
~/myagent
 
&&
 
./run.sh
 
VS30063
 
Unauthorized
 
PAT
 
missing
 
Agent
 
Pools:
 
Read
 
&
 
Manage
 
scope
 
Create
 
new
 
PAT
 
with
 
correct
 
permissions

## Section / Page 53

Error/Problem
 
Root
 
Cause
 
Solution
 
Pool
 
not
 
found
 
error
 
Used
 
agent
 
name
 
instead
 
of
 
pool
 
name
 
in
 
YAML
 
Use
 
pool:
 
name:
 
Default
 
(not
 
demands
 
with
 
pool
 
name)
 
Old
 
content
 
showing
 
after
 
deploy
 
Tomcat
 
work
 
directory
 
cache
 
rm
 
-rf
 
/opt/tomcat1/work/Catalina/localhost/myapp
 
Loki
 
not
 
ready
 
Port
 
3100
 
not
 
open
 
in
 
Azure
 
NSG
 
Azure
 
Portal
 
→
 
VM
 
→
 
Networking
 
→
 
Add
 
inbound
 
rule
 
port
 
3100
 
Grafana
 
cant
 
see
 
logs
 
Promtail
 
not
 
running
 
or
 
wrong
 
log
 
paths
 
Check
 
promtail-config.yaml
 
paths,
 
restart
 
promtail
 
 
PROJECT
 
2:
 
Kubernetes
 
Multi-Tier
 
App
 
on
 
AWS
 
via
 
kOps
 
Complete
 
Architecture
 
—
 
Traffic
 
Flow
 
SETUP
 
FLOW:
 
1.
 
Launch
 
EC2
 
t2.medium
 
→
 
install
 
kOps
 
+
 
kubectl
 
+
 
awscli
 
2.
 
Create
 
S3
 
bucket
 
for
 
kOps
 
state
 
store
 
3.
 
kops
 
create
 
cluster
 
→
 
defines
 
cluster
 
config
 
in
 
S3
 
4.
 
kops
 
update
 
cluster
 
--yes
 
→
 
kOps
 
creates
 
AWS
 
resources:
 
   
-
 
VPC
 
+
 
subnets
 
+
 
route
 
tables
 
+
 
IGW
 
   
-
 
Security
 
Groups
 
(master
 
+
 
worker)
 
   
-
 
EC2:
 
1
 
master
 
(t3.medium)
 
+
 
2
 
workers
 
(t3.medium)
 
   
-
 
IAM
 
roles
 
for
 
master
 
+
 
worker
 
   
-
 
ELB
 
for
 
Kubernetes
 
API
 
server
 
   
-
 
Auto
 
Scaling
 
Groups
 
for
 
workers
 
5.
 
kubectl
 
get
 
nodes
 
→
 
verify
 
3
 
nodes
 
(1
 
master
 
+
 
2
 
workers)
 
6.
 
Docker
 
build
 
→
 
push
 
to
 
ECR
 
7.
 
kubectl
 
apply
 
-f
 
manifests/
 
→
 
pods
 
running
 
 
TRAFFIC
 
FLOW:
 
External
 
User
 
    
|
 
    
v
 
HTTP
 
request
 
AWS
 
ELB
 
(created
 
automatically
 
by
 
LoadBalancer
 
service)
 
    
|
 
    
v
 
Forwards
 
to
 
one
 
of
 
the
 
worker
 
nodes
 
NodePort
 
on
 
Worker
 
Node
 
    
|
 
    
v
 
kube-proxy
 
routes
 
to
 
pod
 
endpoint
 
Frontend
 
Pod
 
(Apache
 
—
 
3
 
replicas
 
in
 
round-robin)
 
    
|
 
    
v
 
API
 
call
 
to
 
http://backend-service.default.svc.cluster.local:3000/api/todos
 
Kubernetes
 
internal
 
DNS
 
resolves
 
→
 
ClusterIP
 
    
|
 
    
v
 
kube-proxy
 
routes
 
to
 
pod
 
endpoint
 
Backend
 
Pod
 
(Node.js
 
—
 
3
 
replicas
 
in
 
round-robin)
 
    
|
 
    
v
 
Database
 
query
 
to
 
postgres.default.svc.cluster.local:5432
 
Kubernetes
 
internal
 
DNS
 
resolves
 
→
 
ClusterIP
 
    
|
 
    
v
 
Routes
 
to
 
StatefulSet
 
pod
 
PostgreSQL
 
Pod
 
(postgres-0,
 
postgres-1,
 
or
 
postgres-2)
 
    
|
 
    
v
 
Reads/writes
 
to
 
EBS
 
volume
 
(/var/lib/postgresql/data)

## Section / Page 54

Response
 
flows
 
back:
 
DB
 
→
 
Backend
 
→
 
Frontend
 
→
 
ELB
 
→
 
User
 
 
Project
 
Limitations
 
and
 
Production
 
Improvements
 
Current
 
Limitation
 
Why
 
It
 
Matters
 
Production
 
Fix
 
EBS
 
volumes
 
are
 
AZ-specific
 
If
 
us-east-1a
 
goes
 
down,
 
all
 
EBS
 
volumes
 
become
 
inaccessible
 
→
 
DB
 
down
 
Use
 
EFS
 
(multi-AZ
 
NFS)
 
or
 
set
 
up
 
DB
 
replication
 
across
 
AZs
 
Single
 
master
 
node
 
If
 
master
 
fails,
 
cluster
 
cannot
 
accept
 
new
 
commands
 
(running
 
pods
 
continue
 
but
 
no
 
new
 
deployments)
 
3
 
master
 
nodes
 
in
 
different
 
AZs
 
for
 
HA
 
control
 
plane
 
No
 
Horizontal
 
Pod
 
Autoscaler
 
Traffic
 
spike
 
→
 
pods
 
overloaded
 
→
 
slow
 
app
 
HPA:
 
auto-scale
 
pods
 
when
 
CPU
 
>
 
70%
 
No
 
Cluster
 
Autoscaler
 
Node
 
capacity
 
exhausted
 
→
 
new
 
pods
 
stuck
 
in
 
Pending
 
Enable
 
Cluster
 
Autoscaler
 
→
 
auto-adds
 
worker
 
nodes
 
No
 
database
 
replication
 
All
 
3
 
postgres
 
pods
 
write
 
to
 
their
 
own
 
volume
 
independently
 
Set
 
up
 
PostgreSQL
 
streaming
 
replication
 
(primary
 
→
 
replicas)
 
No
 
Ingress
 
controller
 
One
 
LoadBalancer
 
per
 
Service
 
=
 
expensive
 
($$$)
 
Use
 
nginx-ingress
 
controller
 
—
 
one
 
LB
 
routes
 
all
 
services
 
by
 
path/host
 
No
 
resource
 
limits
 
initially
 
Pods
 
can
 
consume
 
unlimited
 
CPU/RAM
 
→
 
starves
 
other
 
pods
 
Add
 
requests+limits
 
to
 
all
 
containers
 
No
 
monitoring
 
No
 
visibility
 
into
 
pod
 
health
 
or
 
performance
 
Add
 
Prometheus
 
+
 
Grafana
 
to
 
K8s
 
cluster
 
Images
 
pushed
 
to
 
ECR
 
manually
 
Error-prone,
 
not
 
automated
 
Automate
 
image
 
build+push
 
in
 
CI/CD
 
pipeline

## Section / Page 55

SECTION
 
10:
 
Ansible
 
—
 
Complete
 
Deep
 
Guide
 
 
10.1
 
Ansible
 
Key
 
Components
 
Component
 
File/Location
 
Purpose
 
Inventory
 
inventory.ini
 
or
 
inventory.yml
 
Lists
 
all
 
managed
 
servers
 
with
 
IPs/hostnames
 
and
 
groups
 
Playbook
 
*.yml
 
YAML
 
file
 
with
 
ordered
 
list
 
of
 
plays
 
(tasks
 
for
 
hosts)
 
Role
 
roles/<name>/
 
Reusable,
 
organized
 
collection
 
of
 
tasks,
 
handlers,
 
vars,
 
templates
 
Handler
 
handlers/main.yml
 
in
 
role
 
Task
 
that
 
runs
 
ONLY
 
when
 
notified.
 
Deduplicated
 
(runs
 
once
 
even
 
if
 
notified
 
multiple
 
times)
 
Variable
 
group_vars/,
 
host_vars/,
 
vars:
 
Dynamic
 
values
 
used
 
throughout
 
playbooks
 
Template
 
templates/*.j2
 
Jinja2
 
template
 
files
 
—
 
variables
 
rendered
 
before
 
deploying
 
to
 
server
 
Module
 
Built-in
 
or
 
Galaxy
 
Pre-built
 
actions:
 
apt,
 
yum,
 
service,
 
copy,
 
template,
 
shell,
 
command,
 
git
 
Vault
 
ansible-vault
 
Encrypts
 
sensitive
 
files
 
(passwords,
 
API
 
keys).
 
AES-256
 
encryption.
 
Galaxy
 
galaxy.ansible.com
 
Community
 
hub
 
for
 
sharing
 
roles.
 
Like
 
npm
 
for
 
Ansible.
 
 
10.2
 
Inventory
 
File
 
#
 
inventory.ini
 
[webservers]
 
web1
 
ansible_host=10.0.1.10
 
ansible_user=ubuntu
 
ansible_ssh_private_key_file=~/.ssh/key.pem
 
web2
 
ansible_host=10.0.1.11
 
ansible_user=ubuntu
 
ansible_ssh_private_key_file=~/.ssh/key.pem
 
 
[databases]
 
db1
 
ansible_host=10.0.2.10
 
ansible_user=ubuntu
 
 
[all:vars]
 
ansible_python_interpreter=/usr/bin/python3
 
 
#
 
ansible.cfg
 
—
 
set
 
default
 
inventory
 
[defaults]
 
inventory
 
=
 
./inventory.ini
 
remote_user
 
=
 
ubuntu
 
private_key_file
 
=
 
~/.ssh/key.pem

## Section / Page 56

10.3
 
Complete
 
Playbook
 
Example
 
---
 
-
 
name:
 
Setup
 
Web
 
Server
 
Stack
 
  
hosts:
 
webservers
 
  
become:
 
yes
                    
#
 
run
 
as
 
sudo
 
  
vars:
 
    
http_port:
 
80
 
    
app_dir:
 
/opt/myapp
 
 
  
tasks:
 
  
-
 
name:
 
Update
 
package
 
cache
 
    
apt:
 
      
update_cache:
 
yes
 
      
cache_valid_time:
 
3600
     
#
 
skip
 
update
 
if
 
done
 
<
 
1
 
hour
 
ago
 
 
  
-
 
name:
 
Install
 
required
 
packages
 
    
apt:
 
      
name:
 
      
-
 
nginx
 
      
-
 
git
 
      
-
 
python3
 
      
state:
 
present
 
 
  
-
 
name:
 
Create
 
app
 
directory
 
    
file:
 
      
path:
 
"{{
 
app_dir
 
}}"
 
      
state:
 
directory
 
      
owner:
 
www-data
 
      
mode:
 
"0755"
 
 
  
-
 
name:
 
Copy
 
nginx
 
config
 
from
 
template
 
    
template:
 
      
src:
 
nginx.conf.j2
 
      
dest:
 
/etc/nginx/sites-available/myapp.conf
 
    
notify:
 
Reload
 
nginx
          
#
 
trigger
 
handler
 
if
 
config
 
changed
 
 
  
-
 
name:
 
Enable
 
site
 
    
file:
 
      
src:
 
/etc/nginx/sites-available/myapp.conf
 
      
dest:
 
/etc/nginx/sites-enabled/myapp.conf
 
      
state:
 
link
 
    
notify:
 
Reload
 
nginx
 
 
  
-
 
name:
 
Ensure
 
nginx
 
is
 
started
 
and
 
enabled
 
    
service:
 
      
name:
 
nginx
 
      
state:
 
started
 
      
enabled:
 
yes
 
 
  
handlers:
 
  
-
 
name:
 
Reload
 
nginx
 
    
service:
 
      
name:
 
nginx
 
      
state:
 
reloaded
            
#
 
runs
 
ONLY
 
when
 
notified,
 
ONCE
 
per
 
play
 
 
10.4
 
Ansible
 
Vault
 
—
 
Managing
 
Secrets

## Section / Page 57

#
 
CREATE
 
encrypted
 
file
 
ansible-vault
 
create
 
secrets.yml
 
#
 
Enter
 
vault
 
password
 
when
 
prompted,
 
then
 
edit
 
file
 
normally
 
 
#
 
EDIT
 
encrypted
 
file
 
ansible-vault
 
edit
 
secrets.yml
 
 
#
 
VIEW
 
encrypted
 
file
 
ansible-vault
 
view
 
secrets.yml
 
 
#
 
ENCRYPT
 
existing
 
file
 
ansible-vault
 
encrypt
 
vars.yml
 
 
#
 
DECRYPT
 
file
 
ansible-vault
 
decrypt
 
vars.yml
 
 
#
 
USE
 
vault
 
in
 
playbook
 
run
 
ansible-playbook
 
site.yml
 
--ask-vault-pass
     
#
 
prompt
 
for
 
password
 
ansible-playbook
 
site.yml
 
--vault-password-file
 
~/.vault_pass
  
#
 
file

## Section / Page 58

SECTION
 
11:
 
Networking
 
—
 
Complete
 
Deep
 
Guide
 
 
11.1
 
DNS
 
—
 
How
 
It
 
Really
 
Works
 
DNS
 
Resolution
 
Steps
 
(What
 
happens
 
when
 
you
 
type
 
google.com)
 
1.
 
Browser
 
checks
 
local
 
cache
 
—
 
did
 
I
 
resolve
 
this
 
recently?
 
2.
 
OS
 
checks
 
/etc/hosts
 
file
 
—
 
is
 
there
 
a
 
manual
 
entry?
 
3.
 
Query
 
sent
 
to
 
Recursive
 
Resolver
 
(your
 
ISP
 
or
 
8.8.8.8)
 
4.
 
Recursive
 
Resolver
 
checks
 
its
 
cache
 
—
 
already
 
know
 
this?
 
5.
 
Queries
 
Root
 
DNS
 
Server
 
—
 
"who
 
handles
 
.com?"
 
6.
 
Queries
 
.com
 
TLD
 
Name
 
Server
 
—
 
"who
 
handles
 
google.com?"
 
7.
 
Queries
 
Google's
 
Authoritative
 
Name
 
Server
 
—
 
"what
 
is
 
google.com?"
 
8.
 
Returns
 
A
 
record
 
(IP
 
address)
 
→
 
browser
 
connects
 
to
 
that
 
IP
 
 
DNS
 
Record
 
Types
 
Record
 
Purpose
 
Example
 
A
 
Maps
 
hostname
 
to
 
IPv4
 
address
 
google.com
 
→
 
142.250.80.46
 
AAAA
 
Maps
 
hostname
 
to
 
IPv6
 
address
 
google.com
 
→
 
2607:f8b0:4004:c09::65
 
CNAME
 
Alias
 
—
 
maps
 
to
 
another
 
hostname
 
www.google.com
 
→
 
google.com
 
MX
 
Mail
 
exchange
 
server
 
for
 
domain
 
gmail.com
 
→
 
mail.google.com
 
(priority
 
5)
 
TXT
 
Text
 
data
 
(verification,
 
SPF,
 
DKIM)
 
google.com
 
→
 
"v=spf1
 
include:..."
 
NS
 
Name
 
servers
 
for
 
domain
 
google.com
 
→
 
ns1.google.com
 
PTR
 
Reverse
 
DNS
 
—
 
IP
 
to
 
hostname
 
142.250.80.46
 
→
 
lax17s56-in-f14.1e100.net
 
 
11.2
 
How
 
HTTPS
 
Works
 
(TLS
 
Handshake)
 
9.
 
Client
 
sends:
 
"Hello,
 
I
 
support
 
TLS
 
1.3,
 
here
 
are
 
my
 
cipher
 
suites"
 
10.
 
Server
 
responds:
 
"Let's
 
use
 
AES-256.
 
Here's
 
my
 
SSL
 
certificate"
 
11.
 
Client
 
verifies
 
certificate
 
against
 
trusted
 
Certificate
 
Authorities
 
(CAs)
 
12.
 
Client
 
generates
 
session
 
key,
 
encrypts
 
with
 
server's
 
public
 
key,
 
sends
 
it
 
13.
 
Server
 
decrypts
 
with
 
its
 
private
 
key
 
—
 
both
 
now
 
have
 
same
 
session
 
key
 
14.
 
All
 
subsequent
 
communication
 
encrypted
 
with
 
session
 
key
 
(symmetric
 
encryption)
 
 
11.3
 
NAT
 
—
 
How
 
It
 
Works
 
NAT
 
(Network
 
Address
 
Translation)
 
allows
 
multiple
 
devices
 
to
 
share
 
one
 
public
 
IP.
 
Type
 
Description
 
SNAT
 
(Source
 
NAT)
 
Changes
 
source
 
IP
 
when
 
leaving
 
private
 
network.
 
Used
 
by
 
NAT
 
Gateway.

## Section / Page 59

Type
 
Description
 
DNAT
 
(Destination
 
NAT)
 
Changes
 
destination
 
IP
 
—
 
used
 
for
 
port
 
forwarding.
 
Load
 
balancers.
 
PAT
 
(Port
 
Address
 
Translation)
 
Multiple
 
private
 
IPs
 
→
 
one
 
public
 
IP,
 
differentiated
 
by
 
port
 
numbers.
 
 
11.4
 
Subnetting
 
(For
 
AWS
 
VPC
 
Setup)
 
CIDR
 
IP
 
Range
 
Usable
 
IPs
 
Use
 
Case
 
/8
 
X.0.0.0
 
-
 
X.255.255.255
 
16.7
 
million
 
Very
 
large
 
networks
 
(unlikely)
 
/16
 
X.Y.0.0
 
-
 
X.Y.255.255
 
65,534
 
VPC
 
CIDR
 
—
 
your
 
entire
 
network
 
/24
 
X.Y.Z.0
 
-
 
X.Y.Z.255
 
254
 
Subnet
 
—
 
one
 
AZ,
 
one
 
tier
 
/32
 
Single
 
IP
 
1
 
(the
 
IP
 
itself)
 
Specific
 
IP
 
in
 
security
 
rules
 
 
11.5
 
How
 
Kubernetes
 
Networking
 
Works
 
K8s
 
Network
 
Model
 
(3
 
Rules)
 
•
 
Every
 
pod
 
gets
 
its
 
own
 
IP
 
address
 
•
 
All
 
pods
 
can
 
communicate
 
with
 
all
 
other
 
pods
 
—
 
no
 
NAT
 
•
 
Nodes
 
can
 
communicate
 
with
 
all
 
pods
 
—
 
no
 
NAT
 
 
How
 
Services
 
Work
 
Internally
 
kube-proxy
 
on
 
each
 
node
 
maintains
 
iptables
 
rules.
 
When
 
traffic
 
arrives
 
for
 
a
 
Service
 
ClusterIP,
 
iptables
 
DNAT
 
rules
 
redirect
 
it
 
to
 
one
 
of
 
the
 
pod
 
endpoints
 
(load
 
balancing).

## Section / Page 60

SECTION
 
12:
 
Interview
 
Preparation
 
—
 
Complete
 
Guide
 
 
12.1
 
Your
 
Introduction
 
(Polished
 
—
 
90
 
Seconds)
 
TEMPLATE:
 
"I
 
am
 
Akhil
 
B
 
M,
 
a
 
DevOps
 
and
 
Cloud
 
Engineer
 
from
 
Bengaluru.
 
I
 
completed
 
my
 
B.E.
 
in
 
Information
 
Science
 
from
 
BMS
 
Institute
 
of
 
Technology
 
and
 
a
 
DevOps
 
internship
 
at
 
JSpiders
 
where
 
I
 
worked
 
with
 
Jenkins,
 
Docker,
 
Kubernetes,
 
and
 
AWS.
 
I
 
hold
 
an
 
AWS
 
With
 
DevOps
 
certification
 
and
 
an
 
Oracle
 
Fusion
 
AI
 
Agent
 
Studio
 
certification.
 
I
 
have
 
built
 
three
 
production-grade
 
projects:
 
a
 
Kubernetes
 
multi-tier
 
application
 
on
 
AWS
 
using
 
kOps,
 
an
 
Azure
 
DevOps
 
CI/CD
 
pipeline
 
with
 
Apache
 
reverse
 
proxy
 
and
 
isolated
 
Tomcat
 
instances,
 
and
 
an
 
LGTM
 
observability
 
stack
 
for
 
real-time
 
log
 
monitoring.
 
I
 
specialize
 
in
 
CI/CD
 
automation,
 
containerization,
 
and
 
Linux
 
system
 
hardening.
 
I
 
am
 
very
 
interested
 
in
 
this
 
role
 
because
 
[specific
 
reason
 
based
 
on
 
company]."
 
 
12.2
 
Handling
 
Difficult
 
Questions
 
When
 
you
 
don't
 
know
 
something
 
"I
 
haven't
 
worked
 
with
 
[X]
 
directly
 
in
 
my
 
projects,
 
but
 
based
 
on
 
my
 
experience
 
with
 
[similar
 
technology],
 
I
 
understand
 
it
 
works
 
by
 
[explanation].
 
I
 
would
 
get
 
up
 
to
 
speed
 
quickly
 
by
 
[learning
 
approach
 
—
 
documentation,
 
hands-on
 
practice]."
 
 
When
 
asked
 
about
 
weaknesses
 
/
 
project
 
gaps
 
Be
 
honest
 
and
 
follow
 
with
 
what
 
you'd
 
improve.
 
Example:
 
"In
 
my
 
Kubernetes
 
project,
 
I
 
didn't
 
implement
 
auto-scaling.
 
For
 
production,
 
I
 
would
 
configure
 
HPA
 
to
 
automatically
 
scale
 
pods
 
based
 
on
 
CPU
 
utilization
 
and
 
enable
 
Cluster
 
Autoscaler
 
to
 
add
 
worker
 
nodes
 
when
 
capacity
 
is
 
exhausted."
 
 
12.3
 
Comprehensive
 
Q&A
 
Question
 
Your
 
Answer
 
(Key
 
Points)
 
What
 
is
 
DevOps?
 
Culture
 
+
 
practices
 
uniting
 
Dev
 
and
 
Ops.
 
Plan→Code→Build→Test→Release→Deploy→Operate→Monitor
 
feedback
 
loop.
 
Goal:
 
faster,
 
reliable
 
software
 
delivery.
 
CI
 
vs
 
CD?
 
CI:
 
auto-build+test
 
every
 
push.
 
CD
 
(Delivery):
 
auto-deploy
 
to
 
staging.
 
CD
 
(Deployment):
 
auto-deploy
 
to
 
production.
 
What
 
is
 
a
 
container?
 
Isolated
 
process
 
using
 
Linux
 
namespaces
 
(isolation)
 
+
 
cgroups
 
(resource
 
limits).
 
Shares
 
host
 
kernel.
 
Packages
 
app
 
+
 
dependencies.
 
Docker
 
image
 
vs
 
container?
 
Image
 
=
 
read-only
 
blueprint
 
(Dockerfile
 
build
 
output).
 
Container
 
=
 
running
 
instance
 
with
 
writable
 
layer
 
on
 
top.
 
What
 
is
 
Kubernetes?
 
Container
 
orchestration
 
platform.
 
Auto-healing,
 
auto-scaling,
 
rolling
 
updates,
 
load
 
balancing,
 
service
 
discovery,
 
storage
 
management.
 
What
 
is
 
a
 
Service
 
in
 
K8s?
 
Stable
 
networking
 
endpoint
 
for
 
a
 
group
 
of
 
pods.
 
Pods
 
get
 
new
 
IPs
 
on
 
restart
 
—
 
Service
 
provides
 
stable
 
IP/DNS.
 
What
 
is
 
etcd?
 
Distributed
 
key-value
 
store.
 
Stores
 
ALL
 
Kubernetes
 
cluster
 
state.
 
If
 
etcd
 
fails,
 
cluster
 
cannot
 
function.
 
What
 
is
 
idempotency?
 
Running
 
the
 
same
 
operation
 
multiple
 
times
 
produces
 
the
 
same
 
result.
 
Terraform
 
apply,
 
Ansible
 
playbooks
 
are
 
idempotent.

## Section / Page 61

Question
 
Your
 
Answer
 
(Key
 
Points)
 
What
 
is
 
immutable
 
infrastructure?
 
Don't
 
update
 
running
 
servers
 
—
 
replace
 
them.
 
Build
 
new
 
image,
 
deploy
 
new
 
container/instance,
 
terminate
 
old
 
one.
 
Pull
 
vs
 
Push
 
in
 
config
 
management?
 
Push
 
(Ansible):
 
controller
 
pushes
 
config
 
to
 
servers.
 
Pull
 
(Chef/Puppet):
 
servers
 
fetch
 
config
 
from
 
central
 
server
 
on
 
schedule.
 
Blue-Green
 
vs
 
Canary?
 
Blue-Green:
 
instant
 
full
 
traffic
 
switch
 
between
 
two
 
identical
 
environments.
 
Canary:
 
gradually
 
shift
 
%
 
of
 
traffic
 
to
 
new
 
version
 
(5%→25%→100%).
 
What
 
is
 
a
 
reverse
 
proxy?
 
Server
 
that
 
receives
 
requests
 
and
 
forwards
 
them
 
to
 
backend
 
servers.
 
Hides
 
backend
 
topology,
 
handles
 
SSL,
 
load
 
balancing.
 
Apache,
 
Nginx.
 
What
 
is
 
a
 
load
 
balancer?
 
Distributes
 
traffic
 
across
 
multiple
 
servers
 
to
 
prevent
 
overload.
 
ALB
 
(L7,
 
URL
 
routing),
 
NLB
 
(L4,
 
extreme
 
speed).
 
What
 
is
 
IaC?
 
Infrastructure
 
as
 
Code:
 
manage
 
servers/networks
 
via
 
code
 
files
 
(Terraform,
 
CloudFormation).
 
Version
 
controlled,
 
repeatable,
 
consistent.
 
Terraform
 
vs
 
Ansible?
 
Terraform:
 
provisioning
 
infrastructure
 
(create
 
EC2,
 
VPC,
 
RDS).
 
Ansible:
 
configuring
 
servers
 
(install
 
software,
 
copy
 
files,
 
manage
 
services).
 
What
 
is
 
GitOps?
 
Use
 
Git
 
as
 
the
 
single
 
source
 
of
 
truth
 
for
 
infrastructure
 
and
 
application
 
state.
 
Changes
 
via
 
PRs.
 
ArgoCD/Flux
 
auto-sync
 
cluster
 
to
 
Git
 
state.
 
 
12.4
 
Scenario-Based
 
Questions
 
Scenario:
 
Production
 
is
 
down.
 
How
 
do
 
you
 
debug?
 
15.
 
Check
 
monitoring/alerts
 
first
 
—
 
is
 
there
 
a
 
dashboard
 
showing
 
the
 
issue?
 
16.
 
Check
 
application
 
logs:
 
kubectl
 
logs
 
<pod>
 
-f
 
or
 
tail
 
-f
 
/var/log/app.log
 
17.
 
Check
 
pod
 
status:
 
kubectl
 
get
 
pods
 
—
 
any
 
CrashLoopBackOff
 
or
 
Pending?
 
18.
 
Describe
 
the
 
problematic
 
pod:
 
kubectl
 
describe
 
pod
 
<name>
 
—
 
check
 
Events
 
19.
 
Check
 
recent
 
deployments:
 
kubectl
 
rollout
 
history
 
deployment/app
 
20.
 
Rollback
 
if
 
deployment
 
caused
 
it:
 
kubectl
 
rollout
 
undo
 
deployment/app
 
21.
 
Communicate
 
status
 
to
 
stakeholders
 
while
 
investigating
 
22.
 
Fix
 
root
 
cause,
 
document
 
incident,
 
update
 
runbook
 
 
Scenario:
 
New
 
developer
 
joins.
 
How
 
do
 
you
 
onboard
 
them
 
to
 
CI/CD?
 
Show
 
them:
 
How
 
to
 
clone
 
the
 
repo
 
→
 
create
 
feature
 
branch
 
→
 
make
 
changes
 
→
 
push
 
→
 
create
 
PR
 
with
 
PR
 
template
 
→
 
link
 
to
 
work
 
item
 
→
 
review
 
process
 
→
 
merge
 
to
 
main
 
→
 
watch
 
pipeline
 
run
 
automatically.
 
Walk
 
them
 
through
 
the
 
YAML
 
pipeline
 
structure.
 
Explain
 
the
 
self-hosted
 
agent
 
and
 
why
 
it's
 
on
 
the
 
same
 
VM
 
as
 
Tomcat.
 
Show
 
Grafana
 
dashboard
 
for
 
monitoring
 
their
 
deployments.
 
 
Scenario:
 
How
 
would
 
you
 
add
 
HTTPS
 
to
 
your
 
Project
 
1?
 
23.
 
Get
 
SSL
 
certificate
 
—
 
free
 
from
 
Let's
 
Encrypt
 
using
 
certbot
 
24.
 
Install:
 
sudo
 
apt
 
install
 
certbot
 
python3-certbot-apache
 
25.
 
Run:
 
sudo
 
certbot
 
--apache
 
-d
 
yourdomain.com
 
26.
 
Certbot
 
automatically
 
updates
 
Apache
 
config
 
with
 
SSL
 
+
 
redirects
 
HTTP
 
to
 
HTTPS
 
27.
 
Apache
 
handles
 
SSL
 
termination
 
→
 
forwards
 
HTTP
 
to
 
Tomcat
 
internally

## Section / Page 62

SECTION
 
13:
 
Study
 
Plan
 
&
 
How
 
to
 
Use
 
This
 
Guide
 
 
Day
 
Focus
 
Morning
 
(2
 
hrs)
 
Evening
 
(2
 
hrs)
 
Day
 
1
 
Foundation
 
+
 
Projects
 
Read
 
PART
 
1
 
completely
 
(QR
 
sections
 
1-5)
 
Read
 
QR
 
sections
 
6-10
 
+
 
Section
 
9
 
(Projects
 
full
 
details)
 
Day
 
2
 
AWS
 
+
 
Kubernetes
 
AWS
 
Deep
 
Guide
 
(Section
 
1)
 
Kubernetes
 
Deep
 
Guide
 
(Section
 
2)
 
Day
 
3
 
Docker
 
+
 
Jenkins
 
+
 
Git
 
Docker
 
Deep
 
(Section
 
3)
 
+
 
Jenkins
 
(Section
 
4)
 
Git
 
Deep
 
(Section
 
5)
 
—
 
all
 
commands
 
Day
 
4
 
Linux
 
+
 
Terraform
 
+
 
Azure
 
Linux
 
Deep
 
(Section
 
6)
 
+
 
Terraform
 
(Section
 
7)
 
Azure
 
DevOps
 
Deep
 
(Section
 
8)
 
—
 
YOUR
 
strongest
 
section
 
Day
 
5
 
Ansible
 
+
 
Networking
 
+
 
Interview
 
Ansible
 
(Section
 
10)
 
+
 
Networking
 
(Section
 
11)
 
Interview
 
Prep
 
(Section
 
12)
 
—
 
practice
 
all
 
answers
 
aloud
 
Day
 
6
 
(Revi
ew)
 
Mock
 
Interview
 
Day
 
Re-read
 
PART
 
1
 
completely
 
Practice
 
project
 
answers
 
aloud.
 
Time
 
yourself.
 
Befor
e
 
Inter
view
 
Quick
 
Refresh
 
Re-read
 
PART
 
1
 
(20
 
min)
 
Practice
 
3
 
project
 
answers
 
aloud
 
 
What
 
to
 
Memorize
 
(Priority
 
Order)
 
MUST
 
KNOW
 
(Cannot
 
go
 
to
 
interview
 
without
 
these)
 
•
 
✅
 
Project
 
1
 
architecture
 
flow
 
—
 
code
 
to
 
browser,
 
step
 
by
 
step
 
•
 
✅
 
Project
 
2
 
architecture
 
flow
 
—
 
kOps
 
to
 
pod
 
to
 
EBS
 
•
 
✅
 
Why
 
StatefulSet
 
for
 
DB
 
(not
 
Deployment)
 
•
 
✅
 
Why
 
separate
 
Tomcat
 
instances
 
(not
 
context
 
paths)
 
•
 
✅
 
Why
 
Loki
 
instead
 
of
 
CloudWatch
 
•
 
✅
 
Why
 
self-hosted
 
agent
 
(not
 
Microsoft-hosted)
 
•
 
✅
 
kubectl
 
top
 
10
 
commands
 
—
 
recite
 
from
 
memory
 
•
 
✅
 
Self-hosted
 
agent
 
setup
 
steps
 
(4
 
steps)
 
•
 
✅
 
Your
 
90-second
 
introduction
 
—
 
memorize
 
it
 
 
SHOULD
 
KNOW
 
•
 
✅
 
OSI
 
7
 
layers
 
with
 
protocols
 
•
 
✅
 
Security
 
Group
 
vs
 
NACL
 
differences
 
•
 
✅
 
Terraform
 
workflow:
 
init
 
→
 
plan
 
→
 
apply
 
→
 
destroy
 
•
 
✅
 
Git
 
reset:
 
--soft
 
vs
 
--mixed
 
vs
 
--hard
 
•
 
✅
 
Docker
 
layer
 
caching
 
optimization
 
•
 
✅
 
Jenkins
 
declarative
 
pipeline
 
structure
 
•
 
✅
 
K8s
 
troubleshooting:
 
CrashLoopBackOff,
 
ImagePullBackOff,
 
Pending,
 
OOMKilled

## Section / Page 63

GOOD
 
TO
 
KNOW
 
•
 
✅
 
Ansible
 
idempotency
 
and
 
push
 
vs
 
pull
 
model
 
•
 
✅
 
TCP
 
3-way
 
handshake
 
•
 
✅
 
S3
 
storage
 
classes
 
•
 
✅
 
HPA,
 
RBAC,
 
Ingress
 
in
 
K8s
 
•
 
✅
 
Terraform
 
modules
 
and
 
state
 
management
 
 
Interview
 
Day
 
Strategy
 
•
 
Connect
 
EVERYTHING
 
to
 
your
 
projects
 
—
 
"I
 
used
 
this
 
in
 
my
 
kOps
 
project..."
 
•
 
Never
 
just
 
define
 
—
 
explain
 
WHY
 
you
 
used
 
it
 
that
 
way
 
•
 
Mention
 
project
 
limitations
 
honestly
 
—
 
shows
 
engineering
 
maturity
 
•
 
For
 
gaps:
 
"Haven't
 
used
 
that
 
directly,
 
but
 
based
 
on
 
[X],
 
I
 
understand..."
 
•
 
Ask
 
clarifying
 
questions
 
on
 
complex
 
scenarios
 
—
 
shows
 
thoughtfulness
 
•
 
At
 
end
 
of
 
interview:
 
ask
 
about
 
their
 
tech
 
stack,
 
CI/CD
 
process,
 
monitoring
 
tools
 
 
FINAL
 
REMINDER:
 
You
 
have
 
built
 
3
 
REAL,
 
production-grade
 
projects.
 
Most
 
candidates
 
at
 
your
 
level
 
only
 
have
 
theory.
 
You
 
have
 
actual
 
hands-on
 
experience
 
with
 
Azure
 
DevOps,
 
Kubernetes,
 
Apache,
 
Tomcat,
 
PostgreSQL,
 
LGTM,
 
and
 
AWS.
 
Walk
 
into
 
that
 
interview
 
room
 
CONFIDENTLY.
 
You
 
earned
 
this.
 
🚀

