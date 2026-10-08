# 📘 DevOps Master Study Guide

> *High-yield guide extracted from `Akhil_DevOps_Master_Study_Guide.pdf` for mobile & web GitHub viewing.*

---

## Section / Page 1

AKHIL
 
B
 
M
 
DevOps
 
Interview
 
Master
 
Guide
 
Complete
 
Study
 
Document
 
—
 
Projects
 
+
 
Theory
 
+
 
Quick
 
Revision
 
 
 
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

## Section / Page 2

⚡
 
PART
 
1:
 
QUICK
 
REVISION
 
—
 
Read
 
in
 
20
 
Minutes
 
HOW
 
TO
 
USE:
 
Read
 
PART
 
1
 
before
 
every
 
interview.
 
It
 
covers
 
everything
 
at
 
a
 
glance.
 
For
 
deeper
 
reading,
 
go
 
to
 
PART
 
2.
 
 
1.
 
AWS
 
—
 
Core
 
Concepts
 
Service
 
What
 
It
 
Does
 
Key
 
Point
 
IAM
 
Controls
 
who
 
can
 
access
 
what
 
Least
 
privilege
 
principle
 
EC2
 
Virtual
 
servers
 
in
 
the
 
cloud
 
Connect
 
Linux:
 
SSH
 
|
 
Windows:
 
RDP
 
EBS
 
Block
 
storage
 
attached
 
to
 
EC2
 
AZ-specific,
 
backup
 
via
 
Snapshots
 
S3
 
Object
 
storage
 
in
 
buckets
 
Global,
 
max
 
5TB
 
per
 
object
 
VPC
 
Your
 
private
 
network
 
in
 
AWS
 
Public
 
subnet
 
=
 
internet,
 
Private
 
=
 
internal
 
ALB
 
Layer
 
7
 
HTTP/HTTPS
 
load
 
balancer
 
Path/host-based
 
routing
 
→
 
microservices
 
NLB
 
Layer
 
4
 
TCP/UDP
 
load
 
balancer
 
Ultra-low
 
latency,
 
high
 
performance
 
CloudWatch
 
AWS
 
monitoring
 
service
 
Metrics,
 
Alarms,
 
Logs
 
RDS
 
Relational
 
database
 
(SQL)
 
PostgreSQL,
 
MySQL,
 
Aurora
 
DynamoDB
 
NoSQL
 
database
 
Auto-scales,
 
key-value
 
store
 
Lambda
 
Serverless
 
compute
 
Event-triggered,
 
no
 
EC2
 
needed
 
 
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
 
Subnet
 
level
 
State
 
Stateful
 
(allow
 
only)
 
Stateless
 
(allow
 
+
 
deny)
 
Use
 
Most
 
common
 
day-to-day
 
Broad
 
subnet-wide
 
rules
 
 
2.
 
Kubernetes
 
—
 
Core
 
Concepts
 
Component
 
Role
 
API
 
Server
 
Entry
 
point
 
for
 
all
 
kubectl
 
commands
 
Scheduler
 
Assigns
 
pods
 
to
 
worker
 
nodes
 
Controller
 
Manager
 
Maintains
 
desired
 
state
 
etcd
 
Cluster
 
database
 
—
 
source
 
of
 
truth
 
kubelet
 
Node
 
agent
 
—
 
ensures
 
containers
 
run
 
kube-proxy
 
Handles
 
networking
 
and
 
service
 
routing
 
 
Service
 
Types

## Section / Page 3

Type
 
Access
 
Use
 
Case
 
ClusterIP
 
Internal
 
only
 
Pod-to-Pod
 
communication
 
NodePort
 
External
 
via
 
node
 
IP:port
 
Dev/test
 
access
 
LoadBalancer
 
External
 
via
 
cloud
 
LB
 
Production
 
public
 
access
 
 
Key
 
kubectl
 
Commands
 
kubectl
 
get
 
pods/nodes/svc/deploy
 
kubectl
 
describe
 
pod
 
<name>
 
kubectl
 
logs
 
<pod>
 
-f
 
kubectl
 
exec
 
-it
 
<pod>
 
--
 
bash
 
kubectl
 
apply
 
-f
 
file.yaml
 
kubectl
 
rollout
 
undo
 
deployment/<name>
 
kubectl
 
scale
 
deployment/<name>
 
--replicas=5
 
 
3.
 
Docker
 
—
 
Quick
 
Reference
 
Command
 
What
 
It
 
Does
 
docker
 
build
 
-t
 
name:tag
 
.
 
Build
 
image
 
from
 
Dockerfile
 
docker
 
run
 
-d
 
-p
 
8080:80
 
--name
 
app
 
image
 
Run
 
container
 
in
 
background
 
docker
 
ps
 
/
 
docker
 
ps
 
-a
 
List
 
running
 
/
 
all
 
containers
 
docker
 
logs
 
-f
 
container
 
Follow
 
container
 
logs
 
docker
 
exec
 
-it
 
container
 
bash
 
Shell
 
into
 
container
 
docker
 
push
 
repo/image:tag
 
Push
 
image
 
to
 
registry
 
 
VM
 
vs
 
Container
 
 
VM
 
Container
 
OS
 
Full
 
OS
 
(GBs)
 
Shared
 
kernel
 
(MBs)
 
Start
 
time
 
Minutes
 
Seconds
 
Isolation
 
Full
 
isolation
 
Process-level
 
isolation
 
 
4.
 
Git
 
—
 
Key
 
Commands
 
git
 
init
 
/
 
git
 
clone
 
<url>
 
git
 
add
 
.
 
/
 
git
 
commit
 
-m
 
"msg"
 
git
 
push
 
origin
 
branch
 
/
 
git
 
pull
 
origin
 
main
 
git
 
checkout
 
-b
 
feature
 
/
 
git
 
switch
 
-c
 
feature
 
git
 
merge
 
feature
 
/
 
git
 
rebase
 
main
 
git
 
stash
 
/
 
git
 
stash
 
pop
 
git
 
reset
 
--soft/--mixed/--hard
 
HEAD~1
 
git
 
revert
 
<commit-id>
 
 
Merge
 
=
 
preserves
 
history
 
|
 
Rebase
 
=
 
clean
 
linear
 
history
 
(never
 
rebase
 
shared
 
branches)

## Section / Page 4

5.
 
Linux
 
—
 
Essential
 
Commands
 
Category
 
Commands
 
Permissions
 
chmod
 
755
 
file
 
|
 
chown
 
user:group
 
file
 
|
 
rwx
 
=
 
4+2+1
 
Process
 
ps
 
aux
 
|
 
top
 
|
 
kill
 
-9
 
PID
 
|
 
pkill
 
name
 
Files
 
ls
 
-la
 
|
 
find
 
/
 
-name
 
"*.log"
 
|
 
grep
 
-r
 
"pattern"
 
Services
 
systemctl
 
start/stop/restart/status/enable
 
service
 
Networking
 
ip
 
addr
 
|
 
ss
 
-tulpn
 
|
 
ufw
 
allow
 
22
 
|
 
ssh
 
-i
 
key.pem
 
user@ip
 
 
6.
 
Terraform
 
—
 
Quick
 
Reference
 
Command
 
Action
 
terraform
 
init
 
Download
 
providers
 
terraform
 
plan
 
Preview
 
changes
 
terraform
 
apply
 
Create
 
infrastructure
 
terraform
 
destroy
 
Delete
 
all
 
resources
 
terraform
 
state
 
list
 
See
 
what
 
exists
 
 
Workflow:
 
init
 
→
 
plan
 
→
 
apply
 
→
 
destroy
 
State:
 
terraform.tfstate
 
tracks
 
what
 
exists
 
→
 
store
 
in
 
S3
 
for
 
teams
 
(remote
 
state)
 
 
7.
 
Azure
 
DevOps
 
—
 
Quick
 
Reference
 
Service
 
Purpose
 
Azure
 
Boards
 
Plan
 
work
 
—
 
tasks,
 
bugs,
 
sprints,
 
Kanban
 
boards
 
Azure
 
Repos
 
Store
 
and
 
manage
 
code
 
using
 
Git
 
Azure
 
Pipelines
 
Build
 
and
 
deploy
 
automatically
 
(CI/CD)
 
Azure
 
Test
 
Plans
 
Manual
 
and
 
automated
 
testing
 
Azure
 
Artifacts
 
Store
 
and
 
share
 
code
 
packages
 
 
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
 
pool:
  
name:
 
Default
   
←
 
Use
 
POOL
 
name,
 
NOT
 
agent
 
name
 
 
8.
 
Networking
 
—
 
Quick
 
Reference

## Section / Page 5

Protocol
 
Port
 
SSH
 
22
 
HTTP
 
80
 
HTTPS
 
443
 
FTP
 
21
 
DNS
 
53
 
RDP
 
3389
 
MySQL
 
3306
 
PostgreSQL
 
5432
 
 
TCP:
 
reliable,
 
ordered
 
(HTTP,
 
SSH)
 
|
 
UDP:
 
fast,
 
no
 
guarantee
 
(DNS,
 
streaming)
 
OSI
 
Layers
 
(top-down):
 
Application
 
|
 
Presentation
 
|
 
Session
 
|
 
Transport
 
|
 
Network
 
|
 
Data
 
Link
 
|
 
Physical
 
 
9.
 
Your
 
Projects
 
—
 
30-Second
 
Answers
 
Project
 
1
 
(Azure
 
DevOps
 
+
 
Reverse
 
Proxy
 
+
 
LGTM):
 
I
 
set
 
up
 
two
 
Tomcat
 
instances
 
(ports
 
7789
 
and
 
8888)
 
behind
 
an
 
Apache
 
Reverse
 
Proxy
 
on
 
port
 
80
 
on
 
an
 
Azure
 
VM.
 
An
 
Azure
 
DevOps
 
multi-stage
 
CI/CD
 
pipeline
 
with
 
a
 
self-hosted
 
agent
 
automates
 
deployments.
 
Promtail
 
+
 
Loki
 
+
 
Grafana
 
monitors
 
all
 
logs
 
in
 
real
 
time.
 
Project
 
2
 
(Kubernetes
 
on
 
AWS
 
via
 
kOps):
 
I
 
containerized
 
a
 
Node.js
 
backend
 
and
 
Apache
 
frontend
 
using
 
Docker.
 
Provisioned
 
a
 
Kubernetes
 
cluster
 
on
 
AWS
 
with
 
kOps
 
(1
 
master
 
+
 
2
 
workers).
 
Deployed
 
frontend
 
(LoadBalancer
 
Service),
 
backend
 
(ClusterIP),
 
and
 
PostgreSQL
 
(StatefulSet
 
with
 
EBS
 
persistent
 
volume).
 
3
 
replicas
 
each
 
for
 
HA.
 
Project
 
3
 
(LGTM
 
Monitoring):
 
Installed
 
Promtail
 
on
 
the
 
VM
 
to
 
collect
 
Apache
 
and
 
Tomcat
 
logs
 
→
 
Loki
 
stores
 
them
 
→
 
Grafana
 
visualizes
 
in
 
real
 
time
 
with
 
dashboards
 
and
 
alerts.
 
Free,
 
open-source
 
alternative
 
to
 
AWS
 
CloudWatch.
 
 
10.
 
Top
 
5
 
Interview
 
Questions
 
—
 
Answer
 
Templates
 
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
 
builds
 
the
 
Java
 
WAR
 
→
 
Stage
 
2
 
runs
 
tests
 
→
 
Stage
 
3
 
deploys
 
to
 
Tomcat
 
1
 
(7789)
 
→
 
Stage
 
4
 
deploys
 
to
 
Tomcat
 
2
 
(8888).
 
Apache
 
reverse
 
proxy
 
routes
 
public
 
traffic
 
through
 
port
 
80.
 
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
 
crash.
 
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
 
desired.
 
Kubernetes
 
automatically
 
schedules
 
a
 
new
 
pod
 
on
 
an
 
available
 
node.
 
This
 
is
 
called
 
self-healing.
 
Q:
 
Difference
 
between
 
Docker
 
and
 
VM
 
VMs
 
have
 
a
 
full
 
OS
 
per
 
instance
 
(GBs,
 
minutes
 
to
 
start).
 
Containers
 
share
 
the
 
host
 
kernel
 
(MBs,
 
seconds
 
to
 
start).
 
Docker
 
provides
 
process-level
 
isolation.
 
VMs
 
provide
 
full
 
hardware
 
isolation.
 
For
 
most
 
web
 
apps
 
and
 
microservices,
 
containers
 
are
 
preferred.
 
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
 
infrastructure
 
to
 
terraform.tfstate.
 
On
 
each
 
run,
 
it
 
compares
 
the
 
state
 
file
 
with
 
your
 
configuration
 
and
 
the
 
real
 
infrastructure
 
to
 
determine
 
what
 
changes
 
to
 
make.
 
For
 
teams,
 
store
 
state
 
in
 
S3
 
with
 
DynamoDB
 
locking
 
to
 
prevent
 
concurrent
 
conflicts.
 
Q:
 
What
 
is
 
least
 
privilege
 
in
 
IAM?

## Section / Page 6

Give
 
users
 
and
 
services
 
only
 
the
 
minimum
 
permissions
 
they
 
need
 
to
 
do
 
their
 
job.
 
No
 
more,
 
no
 
less.
 
This
 
limits
 
the
 
blast
 
radius
 
if
 
an
 
account
 
is
 
compromised.
 
In
 
practice:
 
use
 
specific
 
resource
 
ARNs
 
in
 
policies
 
instead
 
of
 
wildcards,
 
create
 
separate
 
roles
 
for
 
each
 
service.

## Section / Page 7

PART
 
2
 
—
 
SECTION
 
1:
 
AWS
 
—
 
COMPLETE
 
GUIDE
 
Key
 
Insight:
 
AWS
 
is
 
the
 
most
 
important
 
cloud
 
platform
 
for
 
DevOps.
 
Know
 
IAM,
 
EC2,
 
VPC,
 
and
 
S3
 
deeply.
 
Everything
 
else
 
follows.
 
 
1.1
 
IAM
 
—
 
Identity
 
and
 
Access
 
Management
 
What
 
is
 
IAM?
 
IAM
 
controls
 
WHO
 
can
 
access
 
WHAT
 
in
 
your
 
AWS
 
environment.
 
It
 
is
 
the
 
security
 
backbone
 
of
 
everything
 
you
 
build.
 
IAM
 
Components
 
•
 
Users
 
—
 
permanent
 
identity
 
for
 
a
 
person
 
(has
 
long-term
 
credentials)
 
•
 
Groups
 
—
 
collection
 
of
 
users
 
with
 
shared
 
permissions
 
•
 
Roles
 
—
 
temporary
 
identity
 
without
 
credentials.
 
Services
 
assume
 
roles
 
for
 
temporary
 
access
 
•
 
Policies
 
—
 
JSON
 
documents
 
that
 
define
 
permissions
 
(allow/deny)
 
 
Key
 
Principle:
 
Least
 
Privilege
 
Give
 
users
 
and
 
services
 
only
 
the
 
minimum
 
permissions
 
they
 
need.
 
Never
 
use
 
wildcards
 
(*)
 
in
 
production
 
policies.
 
DevOps
 
Use
 
Case
 
•
 
Assign
 
IAM
 
roles
 
to
 
EC2
 
instances
 
so
 
apps
 
access
 
S3/DynamoDB
 
without
 
hardcoded
 
credentials
 
•
 
Lambda
 
functions
 
use
 
roles
 
to
 
access
 
other
 
AWS
 
services
 
•
 
Create
 
separate
 
users
 
for
 
humans;
 
use
 
roles
 
for
 
services
 
 
1.2
 
EC2
 
—
 
Elastic
 
Compute
 
Cloud
 
What
 
is
 
EC2?
 
EC2
 
is
 
a
 
virtual
 
server
 
in
 
the
 
cloud.
 
You
 
choose
 
the
 
OS,
 
CPU,
 
RAM,
 
and
 
storage.
 
You
 
pay
 
per
 
hour.
 
Connecting
 
to
 
EC2
 
•
 
Linux:
 
SSH
 
with
 
key
 
pair
 
(.pem
 
file)
 
—
 
ssh
 
-i
 
key.pem
 
ec2-user@ip
 
•
 
Windows:
 
RDP
 
(Remote
 
Desktop
 
Protocol)
 
or
 
Session
 
Manager
 
Key
 
Concepts
 
•
 
AMI
 
(Amazon
 
Machine
 
Image)
 
—
 
OS
 
+
 
pre-installed
 
software
 
snapshot.
 
What
 
you
 
launch
 
from.
 
•
 
Instance
 
Type
 
—
 
defines
 
CPU
 
+
 
RAM
 
(t2.micro,
 
m5.large,
 
c5.xlarge)
 
•
 
Launch
 
Template
 
—
 
saves
 
your
 
instance
 
configuration
 
for
 
reuse
 
•
 
Auto
 
Scaling
 
Group
 
—
 
automatically
 
adds/removes
 
EC2
 
based
 
on
 
CloudWatch
 
metrics
 
 
EBS
 
—
 
Elastic
 
Block
 
Store
 
•
 
Block
 
storage
 
directly
 
attached
 
to
 
EC2
 
(like
 
an
 
external
 
hard
 
drive)
 
•
 
AZ-specific
 
—
 
cannot
 
share
 
between
 
AZs
 
without
 
effort
 
•
 
Default:
 
8GB
 
Linux,
 
30GB
 
Windows
 
•
 
Backup
 
via
 
Snapshots
 
→
 
stored
 
in
 
S3
 
 
1.3
 
VPC
 
—
 
Virtual
 
Private
 
Cloud

## Section / Page 8

What
 
is
 
VPC?
 
Your
 
own
 
isolated
 
private
 
network
 
in
 
AWS.
 
You
 
control
 
subnets,
 
routing,
 
security,
 
and
 
traffic
 
flow.
 
Component
 
Purpose
 
Public
 
Subnet
 
Has
 
Internet
 
Gateway
 
—
 
instances
 
reachable
 
from
 
internet.
 
Use
 
for
 
LBs,
 
bastion
 
hosts.
 
Private
 
Subnet
 
No
 
direct
 
internet.
 
Use
 
for
 
databases,
 
app
 
servers.
 
Internet
 
Gateway
 
Allows
 
public
 
subnet
 
traffic
 
to
 
reach
 
the
 
internet
 
NAT
 
Gateway
 
Allows
 
private
 
instances
 
to
 
initiate
 
outbound
 
internet
 
traffic
 
only
 
Bastion
 
Host
 
Jump
 
server
 
in
 
public
 
subnet
 
—
 
SSH
 
into
 
it,
 
then
 
hop
 
to
 
private
 
instances
 
Security
 
Group
 
Instance-level
 
firewall
 
—
 
stateful,
 
allow
 
rules
 
only
 
NACL
 
Subnet-level
 
firewall
 
—
 
stateless,
 
allow
 
+
 
deny
 
rules
 
 
1.4
 
S3
 
—
 
Simple
 
Storage
 
Service
 
What
 
is
 
S3?
 
Object
 
storage
 
—
 
files
 
stored
 
in
 
buckets,
 
accessed
 
over
 
HTTP.
 
Infinitely
 
scalable.
 
Max
 
object
 
size:
 
5TB.
 
Storage
 
Classes
 
•
 
Standard
 
—
 
frequent
 
access,
 
highest
 
cost
 
•
 
Standard-IA
 
—
 
infrequent
 
access,
 
lower
 
cost
 
•
 
One
 
Zone-IA
 
—
 
infrequent,
 
only
 
one
 
AZ
 
(cheaper,
 
less
 
resilient)
 
•
 
Glacier
 
—
 
archival,
 
retrieval
 
takes
 
minutes-hours
 
•
 
Glacier
 
Deep
 
Archive
 
—
 
cheapest,
 
retrieval
 
takes
 
12+
 
hours
 
Use
 
Cases
 
•
 
Backups
 
and
 
snapshots
 
•
 
Static
 
website
 
hosting
 
•
 
Docker
 
image
 
artifact
 
storage
 
•
 
Application
 
logs
 
and
 
big
 
data
 
 
1.5
 
Load
 
Balancers
 
Feature
 
ALB
 
(Layer
 
7)
 
NLB
 
(Layer
 
4)
 
OSI
 
Layer
 
Layer
 
7
 
(Application)
 
Layer
 
4
 
(Transport)
 
Protocol
 
HTTP/HTTPS
 
TCP/UDP
 
Routing
 
Path-based,
 
host-based
 
IP
 
and
 
port-based
 
Use
 
case
 
Microservices,
 
web
 
apps
 
High
 
performance,
 
low
 
latency
 
Speed
 
Slight
 
overhead
 
from
 
inspection
 
Extremely
 
fast
 
 
1.6
 
CloudWatch
 
—
 
Monitoring
 
•
 
Metrics
 
—
 
CPU,
 
memory,
 
network,
 
disk
 
usage

## Section / Page 9

•
 
Alarms
 
—
 
trigger
 
actions
 
when
 
threshold
 
exceeded
 
(e.g.,
 
CPU
 
>
 
80%
 
→
 
scale
 
out)
 
•
 
Logs
 
—
 
stream
 
and
 
search
 
application/system
 
logs
 
•
 
Dashboards
 
—
 
visual
 
monitoring
 
Your
 
Project
 
Context:
 
You
 
used
 
LGTM
 
stack
 
(Loki,
 
Grafana)
 
instead
 
of
 
CloudWatch
 
because
 
it
 
is
 
open-source
 
and
 
works
 
across
 
AWS
 
+
 
Azure.
 
Mention
 
this
 
in
 
interviews
 
—
 
it
 
shows
 
you
 
chose
 
tools
 
intentionally.
 
 
1.7
 
Other
 
AWS
 
Services
 
Service
 
Type
 
Key
 
Points
 
RDS
 
Relational
 
SQL
 
database
 
PostgreSQL,
 
MySQL,
 
Aurora.
 
Vertical
 
scaling.
 
You
 
used
 
PostgreSQL.
 
DynamoDB
 
NoSQL
 
database
 
Fully
 
managed,
 
auto-scales,
 
key-value
 
store
 
Lambda
 
Serverless
 
compute
 
Event-triggered,
 
no
 
EC2
 
needed,
 
pay
 
per
 
execution
 
Elastic
 
IP
 
Static
 
public
 
IP
 
Stays
 
the
 
same
 
even
 
after
 
instance
 
stop/start
 
Route
 
53
 
DNS
 
service
 
Translates
 
domain
 
names
 
to
 
IP
 
addresses
 
SQS
 
Message
 
queue
 
Decouples
 
services,
 
async
 
communication
 
SNS
 
Notification
 
service
 
Pub/sub
 
messaging,
 
triggers
 
Lambda/email/SMS

## Section / Page 10

SECTION
 
2:
 
KUBERNETES
 
—
 
COMPLETE
 
GUIDE
 
Your
 
Project:
 
You
 
used
 
kOps
 
to
 
provision
 
a
 
Kubernetes
 
cluster
 
on
 
AWS
 
with
 
Node.js
 
backend
 
+
 
Apache
 
frontend
 
+
 
PostgreSQL
 
StatefulSet.
 
Always
 
connect
 
theory
 
to
 
this.
 
 
2.1
 
Why
 
Kubernetes?
 
Without
 
orchestration,
 
Docker
 
standalone
 
has
 
problems:
 
•
 
❌
 
No
 
auto-healing
 
—
 
container
 
crashes,
 
stays
 
dead
 
•
 
❌
 
No
 
auto-scaling
 
—
 
cannot
 
add
 
containers
 
automatically
 
on
 
load
 
•
 
❌
 
No
 
load
 
balancing
 
—
 
no
 
traffic
 
distribution
 
•
 
❌
 
Single
 
host
 
—
 
no
 
clustering
 
•
 
❌
 
No
 
rolling
 
updates
 
—
 
downtime
 
required
 
Kubernetes
 
solves
 
ALL
 
of
 
these.
 
 
2.2
 
Kubernetes
 
Architecture
 
Control
 
Plane
 
(Master
 
Node)
 
Component
 
Role
 
API
 
Server
 
Entry
 
point
 
for
 
all
 
kubectl
 
commands.
 
Validates
 
and
 
processes
 
requests.
 
Scheduler
 
Watches
 
for
 
unscheduled
 
pods,
 
assigns
 
them
 
to
 
suitable
 
worker
 
nodes
 
Controller
 
Manager
 
Runs
 
controllers
 
that
 
maintain
 
desired
 
state
 
(Deployment,
 
ReplicaSet,
 
Node)
 
etcd
 
Distributed
 
key-value
 
store.
 
Stores
 
ALL
 
cluster
 
state.
 
The
 
source
 
of
 
truth.
 
 
Worker
 
Nodes
 
Component
 
Role
 
kubelet
 
Agent
 
on
 
each
 
node.
 
Receives
 
pod
 
specs
 
from
 
API
 
server,
 
ensures
 
containers
 
run
 
kube-proxy
 
Manages
 
network
 
rules,
 
handles
 
Service
 
networking
 
and
 
load
 
balancing
 
Container
 
Runtime
 
Runs
 
containers
 
—
 
containerd
 
(Docker
 
deprecated
 
in
 
K8s
 
1.24+)
 
 
2.3
 
Core
 
Kubernetes
 
Objects
 
Pod
 
The
 
smallest
 
deployable
 
unit
 
in
 
Kubernetes.
 
Wraps
 
one
 
or
 
more
 
containers.
 
Containers
 
in
 
a
 
Pod
 
share
 
IP
 
and
 
storage.
 
Deployment
 
Manages
 
ReplicaSets
 
which
 
manage
 
Pods.
 
Handles
 
rolling
 
updates,
 
rollbacks,
 
and
 
version
 
history.

## Section / Page 11

kubectl
 
create
 
deployment
 
nginx
 
--image=nginx
 
kubectl
 
set
 
image
 
deployment/nginx
 
nginx=nginx:1.21
  
#
 
rolling
 
update
 
kubectl
 
rollout
 
undo
 
deployment/nginx
                 
#
 
rollback
 
ReplicaSet
 
Ensures
 
the
 
desired
 
number
 
of
 
Pod
 
replicas
 
are
 
always
 
running.
 
Usually
 
managed
 
by
 
a
 
Deployment.
 
StatefulSet
 
vs
 
Deployment
 
Feature
 
Deployment
 
StatefulSet
 
Pod
 
names
 
Random
 
(e.g.,
 
nginx-abc123)
 
Stable
 
(e.g.,
 
postgres-0,
 
postgres-1)
 
Storage
 
Shared
 
or
 
no
 
persistent
 
storage
 
Own
 
PVC
 
per
 
pod
 
—
 
data
 
survives
 
restart
 
Use
 
case
 
Stateless
 
apps
 
(web,
 
API)
 
Stateful
 
apps
 
(databases,
 
Kafka)
 
Scaling
 
Any
 
order
 
Ordered
 
(0,
 
1,
 
2...)
 
Your
 
Project:
 
You
 
used
 
StatefulSet
 
for
 
PostgreSQL
 
so
 
that
 
each
 
pod
 
reconnects
 
to
 
its
 
own
 
persistent
 
EBS
 
volume
 
after
 
restart.
 
This
 
prevents
 
data
 
loss.
 
 
2.4
 
Services
 
Type
 
Access
 
Use
 
Case
 
ClusterIP
 
Internal
 
only
 
(no
 
external
 
access)
 
Pod-to-Pod:
 
backend,
 
database
 
NodePort
 
External
 
via
 
NodeIP:Port
 
(30000-32767)
 
Dev/test,
 
limited
 
external
 
LoadBalancer
 
External
 
via
 
cloud
 
Load
 
Balancer
 
Production
 
public
 
endpoints
 
ExternalName
 
Maps
 
to
 
external
 
DNS
 
name
 
Access
 
external
 
services
 
by
 
name
 
Your
 
Project:
 
Frontend
 
used
 
LoadBalancer
 
(gets
 
AWS
 
ELB
 
with
 
public
 
IP).
 
Backend
 
used
 
ClusterIP
 
(internal
 
DNS:
 
backend.default.svc.cluster.local:3000).
 
Database
 
used
 
ClusterIP
 
(postgres.default.svc.cluster.local:5432).
 
 
2.5
 
Storage
 
Volume
 
Types
 
•
 
emptyDir
 
—
 
temporary
 
storage
 
shared
 
between
 
containers
 
in
 
a
 
pod.
 
Lost
 
when
 
pod
 
dies.
 
•
 
hostPath
 
—
 
mounts
 
a
 
directory
 
from
 
the
 
worker
 
node
 
into
 
the
 
pod.
 
•
 
PersistentVolume
 
(PV)
 
—
 
actual
 
storage
 
resource
 
(e.g.,
 
EBS
 
volume
 
on
 
AWS).
 
•
 
PersistentVolumeClaim
 
(PVC)
 
—
 
request
 
for
 
storage
 
by
 
a
 
pod.
 
K8s
 
matches
 
PVC
 
to
 
PV.
 
 
StatefulSet
 
Storage:
 
Each
 
StatefulSet
 
pod
 
gets
 
its
 
own
 
PVC
 
via
 
volumeClaimTemplates.
 
When
 
pod-0
 
restarts,
 
it
 
always
 
reconnects
 
to
 
the
 
same
 
PV
 
—
 
stable
 
identity.
 
 
2.6
 
ConfigMap
 
and
 
Secrets
 
ConfigMap

## Section / Page 12

Stores
 
non-sensitive
 
configuration
 
(environment
 
variables,
 
config
 
files).
 
Decouples
 
config
 
from
 
the
 
container
 
image.
 
Secret
 
Stores
 
sensitive
 
data
 
(passwords,
 
API
 
keys).
 
Base64
 
encoded
 
(not
 
encrypted
 
by
 
default
 
—
 
enable
 
encryption
 
at
 
rest
 
for
 
production).
 
 
2.7
 
Advanced
 
Concepts
 
Concept
 
Description
 
Namespace
 
Logical
 
isolation
 
(dev,
 
staging,
 
prod)
 
within
 
one
 
cluster
 
DaemonSet
 
One
 
pod
 
per
 
node
 
—
 
use
 
for
 
log
 
collectors,
 
monitoring
 
agents
 
HPA
 
Horizontal
 
Pod
 
Autoscaler
 
—
 
scales
 
pod
 
count
 
based
 
on
 
CPU/memory
 
Ingress
 
HTTP
 
router
 
—
 
path/host-based
 
routing
 
to
 
multiple
 
services
 
RBAC
 
ServiceAccount
 
(WHO)
 
→
 
Role
 
(WHAT
 
permissions)
 
→
 
RoleBinding
 
(CONNECT)
 
 
2.8
 
Deployment
 
Strategies
 
Strategy
 
How
 
It
 
Works
 
Downtime
 
Recreate
 
Kill
 
all
 
old
 
pods,
 
create
 
new
 
ones
 
Yes
 
—
 
avoid
 
in
 
production
 
RollingUpdate
 
Replace
 
pods
 
gradually
 
(default)
 
No
 
—
 
gradual
 
replacement
 
Blue-Green
 
Two
 
environments,
 
switch
 
traffic
 
instantly
 
No
 
—
 
instant
 
switchover
 
Canary
 
Send
 
small
 
%
 
of
 
traffic
 
to
 
new
 
version
 
first
 
No
 
—
 
safe
 
progressive
 
rollout
 
 
2.9
 
Troubleshooting
 
Guide
 
Error
 
Cause
 
Fix
 
CrashLoopBackOff
 
App
 
crashing
 
on
 
start
 
kubectl
 
logs
 
pod
 
--previous
 
ImagePullBackOff
 
Wrong
 
image
 
name
 
or
 
missing
 
credentials
 
Check
 
image
 
name
 
and
 
registry
 
secret
 
Pending
 
Insufficient
 
resources
 
or
 
PVC
 
not
 
bound
 
kubectl
 
describe
 
pod
 
—
 
check
 
Events
 
section
 
OOMKilled
 
Container
 
exceeded
 
memory
 
limit
 
Increase
 
memory
 
limits
 
in
 
spec
 
NodeNotReady
 
Node
 
issue
 
Check
 
kubelet,
 
node
 
disk/memory
 
 
2.10
 
kOps
 
—
 
Your
 
Project
 
Setup
 
kOps
 
(Kubernetes
 
Operations)
 
is
 
a
 
tool
 
to
 
provision
 
and
 
manage
 
Kubernetes
 
clusters
 
on
 
AWS.
 
#
 
Step
 
1:
 
Install
 
kOps
 
on
 
EC2
 
(t2.medium,
 
IAM
 
permissions
 
needed)

## Section / Page 13

kops
 
create
 
cluster
 
--name=myapp.k8s.local
 
--zones=us-east-1a
 
kops
 
update
 
cluster
 
--name=myapp.k8s.local
 
--yes
   
#
 
actually
 
creates
 
it
 
kops
 
validate
 
cluster
                                
#
 
check
 
health
 
 
Cluster
 
Resources
 
Created
 
by
 
kOps
 
•
 
Master
 
node
 
(control
 
plane):
 
API
 
Server,
 
etcd,
 
Scheduler,
 
Controller
 
Manager
 
•
 
2
 
Worker
 
nodes:
 
kubelet,
 
kube-proxy,
 
container
 
runtime
 
•
 
VPC,
 
Security
 
Groups,
 
Load
 
Balancers
 
—
 
all
 
auto-created
 
by
 
kOps
 
 
Project
 
Limitations
 
(Be
 
Honest
 
in
 
Interviews)
 
•
 
❌
 
EBS
 
is
 
AZ-specific
 
—
 
not
 
multi-AZ
 
resilient
 
•
 
❌
 
Single
 
master
 
node
 
—
 
not
 
HA
 
(needs
 
3
 
for
 
production)
 
•
 
❌
 
Manual
 
scaling
 
only
 
—
 
no
 
cluster
 
autoscaler
 
configured
 
What
 
You
 
Would
 
Improve
 
•
 
✅
 
Use
 
EFS
 
instead
 
of
 
EBS
 
for
 
multi-AZ
 
persistent
 
storage
 
•
 
✅
 
Multi-master
 
setup
 
(3
 
masters)
 
for
 
high
 
availability
 
•
 
✅
 
Enable
 
Cluster
 
Autoscaler
 
for
 
automatic
 
pod
 
scaling
 
•
 
✅
 
Set
 
up
 
database
 
master-slave
 
replication

## Section / Page 14

SECTION
 
3:
 
DOCKER
 
—
 
COMPLETE
 
GUIDE
 
 
3.1
 
Core
 
Concepts
 
Term
 
Definition
 
Image
 
Read-only
 
blueprint
 
built
 
from
 
a
 
Dockerfile
 
Container
 
Running
 
instance
 
of
 
an
 
image
 
Dockerfile
 
Instructions
 
to
 
build
 
an
 
image
 
layer
 
by
 
layer
 
Registry
 
Repository
 
for
 
storing
 
images
 
(Docker
 
Hub,
 
ECR,
 
ACR)
 
Layer
 
Each
 
Dockerfile
 
instruction
 
creates
 
an
 
immutable
 
layer
 
 
3.2
 
Dockerfile
 
Instructions
 
Instruction
 
Purpose
 
Example
 
FROM
 
Base
 
image
 
FROM
 
openjdk:17-jdk-slim
 
RUN
 
Execute
 
command
 
at
 
build
 
time
 
RUN
 
apt-get
 
install
 
-y
 
curl
 
COPY
 
Copy
 
files
 
from
 
host
 
to
 
image
 
COPY
 
app.jar
 
/app/app.jar
 
ADD
 
Like
 
COPY
 
but
 
can
 
unzip
 
and
 
fetch
 
URLs
 
ADD
 
app.tar.gz
 
/app/
 
WORKDIR
 
Set
 
working
 
directory
 
WORKDIR
 
/app
 
EXPOSE
 
Document
 
port
 
(does
 
not
 
publish)
 
EXPOSE
 
8080
 
ENV
 
Set
 
environment
 
variables
 
ENV
 
JAVA_HOME=/usr/lib/jvm/java-17
 
ARG
 
Build-time
 
variables
 
(not
 
in
 
final
 
image)
 
ARG
 
VERSION=1.0
 
CMD
 
Default
 
start
 
command
 
(overridable)
 
CMD
 
["java",
 
"-jar",
 
"app.jar"]
 
ENTRYPOINT
 
Fixed
 
main
 
command
 
(not
 
overridable)
 
ENTRYPOINT
 
["java",
 
"-jar"]
 
 
RUN
 
vs
 
CMD
 
vs
 
ENTRYPOINT
 
•
 
RUN
 
—
 
executes
 
during
 
image
 
BUILD.
 
Used
 
for
 
installing
 
packages.
 
•
 
CMD
 
—
 
default
 
command
 
when
 
container
 
STARTS.
 
Can
 
be
 
overridden
 
by
 
docker
 
run
 
arguments.
 
•
 
ENTRYPOINT
 
—
 
fixed
 
command.
 
CMD
 
becomes
 
arguments
 
to
 
ENTRYPOINT
 
when
 
both
 
are
 
set.
 
 
3.3
 
Multi-Stage
 
Build
 
Build
 
in
 
one
 
stage,
 
copy
 
only
 
the
 
final
 
artifact
 
to
 
a
 
smaller
 
runtime
 
image.
 
Reduces
 
image
 
size
 
dramatically.
 
FROM
 
maven:3.9
 
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
 
COPY
 
src/
 
src/

## Section / Page 15

RUN
 
mvn
 
package
 
-DskipTests
 
 
FROM
 
openjdk:17-jdk-slim
 
WORKDIR
 
/app
 
COPY
 
--from=builder
 
/app/target/app.jar
 
.
 
CMD
 
["java",
 
"-jar",
 
"app.jar"]
 
Your
 
Project:
 
You
 
containerized
 
Node.js
 
backend
 
and
 
Apache
 
frontend
 
with
 
separate
 
Dockerfiles
 
for
 
service
 
isolation
 
in
 
your
 
Kubernetes
 
project.
 
 
3.4
 
Docker
 
Networking
 
Network
 
Description
 
Use
 
Case
 
bridge
 
Default.
 
Containers
 
on
 
same
 
host
 
can
 
communicate
 
Local
 
development
 
host
 
Container
 
shares
 
host
 
network
 
namespace
 
Maximum
 
performance,
 
no
 
isolation
 
none
 
No
 
network
 
access
 
Isolated
 
batch
 
jobs
 
overlay
 
Multi-host
 
networking
 
for
 
Docker
 
Swarm
 
Distributed
 
services
 
 
3.5
 
Docker
 
Volumes
 
•
 
Named
 
volumes
 
—
 
managed
 
by
 
Docker
 
(docker
 
volume
 
create).
 
Best
 
for
 
databases.
 
•
 
Bind
 
mounts
 
—
 
mount
 
a
 
specific
 
host
 
directory
 
into
 
a
 
container.
 
•
 
tmpfs
 
—
 
memory-only
 
storage.
 
Not
 
persisted.
 
Fast.
 
 
3.6
 
Docker
 
Compose
 
Runs
 
multi-container
 
applications
 
defined
 
in
 
a
 
single
 
docker-compose.yml
 
file.
 
docker-compose
 
up
 
-d
     
#
 
start
 
all
 
services
 
in
 
background
 
docker-compose
 
down
      
#
 
stop
 
and
 
remove
 
containers
 
docker-compose
 
logs
      
#
 
view
 
logs
 
for
 
all
 
services
 
docker-compose
 
ps
        
#
 
list
 
running
 
services

## Section / Page 16

SECTION
 
4:
 
JENKINS
 
—
 
COMPLETE
 
GUIDE
 
 
4.1
 
What
 
is
 
Jenkins?
 
Jenkins
 
is
 
an
 
open-source
 
CI/CD
 
automation
 
server.
 
It
 
automates
 
the
 
entire
 
software
 
pipeline:
 
build,
 
test,
 
and
 
deploy.
 
 
4.2
 
Jenkins
 
Architecture
 
•
 
Master
 
—
 
orchestrates
 
pipelines,
 
schedules
 
jobs,
 
manages
 
agents
 
•
 
Agents
 
(nodes)
 
—
 
execute
 
the
 
actual
 
pipeline
 
jobs
 
on
 
remote
 
machines
 
For
 
your
 
Azure
 
DevOps
 
project,
 
the
 
self-hosted
 
agent
 
is
 
similar
 
to
 
a
 
Jenkins
 
agent.
 
 
4.3
 
Jenkinsfile
 
—
 
Pipeline
 
as
 
Code
 
A
 
Jenkinsfile
 
is
 
a
 
Groovy-based
 
script
 
stored
 
in
 
the
 
repository.
 
Two
 
types:
 
•
 
Declarative
 
Pipeline
 
—
 
modern,
 
structured,
 
easier
 
to
 
read
 
(recommended)
 
•
 
Scripted
 
Pipeline
 
—
 
full
 
Groovy
 
flexibility,
 
more
 
complex
 
 
Declarative
 
Pipeline
 
Structure
 
pipeline
 
{
 
  
agent
 
any
 
  
stages
 
{
 
    
stage("Build")
 
{
 
      
steps
 
{
 
        
sh
 
"mvn
 
clean
 
package"
 
      
}
 
    
}
 
    
stage("Test")
 
{
 
      
steps
 
{
 
        
sh
 
"mvn
 
test"
 
      
}
 
    
}
 
    
stage("Deploy")
 
{
 
      
steps
 
{
 
        
sh
 
"docker
 
build
 
-t
 
myapp
 
.
 
&&
 
docker
 
push
 
myapp"
 
      
}
 
    
}
 
  
}
 
}
 
 
4.4
 
Jenkins
 
Triggers
 
Trigger
 
How
 
It
 
Works
 
Webhook
 
GitHub/GitLab
 
sends
 
HTTP
 
request
 
to
 
Jenkins
 
on
 
every
 
push
 
—
 
instant

## Section / Page 17

Poll
 
SCM
 
Jenkins
 
checks
 
repo
 
on
 
a
 
schedule
 
(e.g.,
 
every
 
5
 
min)
 
Schedule
 
Cron
 
syntax
 
(e.g.,
 
H
 
2
 
*
 
*
 
*
 
=
 
daily
 
at
 
2am)
 
Manual
 
Build
 
button
 
in
 
Jenkins
 
UI
 
 
4.5
 
Credentials
 
Management
 
Store
 
secrets
 
in
 
Jenkins
 
Credential
 
Store
 
—
 
NEVER
 
hardcode
 
passwords
 
in
 
Jenkinsfile.
 
withCredentials([usernamePassword(credentialsId:
 
"docker-hub",
 
...)])
 
 
4.6
 
Common
 
Pipeline
 
Stages
 
Checkout
 
→
 
Build
 
→
 
Test
 
→
 
SonarQube
 
(code
 
quality)
 
→
 
Nexus
 
(artifact
 
store)
 
→
 
Docker
 
Build
 
→
 
Push
 
→
 
Deploy

## Section / Page 18

SECTION
 
5:
 
GIT
 
—
 
COMPLETE
 
GUIDE
 
 
5.1
 
Git
 
4
 
Areas
 
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
 
 
5.2
 
Essential
 
Commands
 
Command
 
Action
 
git
 
init
 
Initialize
 
new
 
repository
 
git
 
clone
 
<url>
 
Clone
 
remote
 
repository
 
git
 
status
 
Show
 
changed
 
files
 
git
 
add
 
.
 
Stage
 
all
 
changes
 
git
 
commit
 
-m
 
"msg"
 
Create
 
commit
 
git
 
push
 
origin
 
branch
 
Push
 
to
 
remote
 
git
 
pull
 
origin
 
main
 
Fetch
 
and
 
merge
 
from
 
remote
 
git
 
checkout
 
-b
 
feature
 
Create
 
and
 
switch
 
to
 
branch
 
git
 
merge
 
feature
 
Merge
 
branch
 
into
 
current
 
git
 
rebase
 
main
 
Rebase
 
current
 
branch
 
onto
 
main
 
(linear
 
history)
 
git
 
stash
 
Save
 
uncommitted
 
changes
 
temporarily
 
git
 
stash
 
pop
 
Restore
 
stashed
 
changes
 
git
 
log
 
--oneline
 
--graph
 
Visual
 
commit
 
history
 
git
 
reset
 
--soft
 
HEAD~1
 
Undo
 
commit,
 
keep
 
changes
 
staged
 
git
 
reset
 
--mixed
 
HEAD~1
 
Undo
 
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
 
Undo
 
commit,
 
DELETE
 
changes
 
permanently
 
git
 
revert
 
<commit-id>
 
Create
 
new
 
commit
 
that
 
undoes
 
a
 
commit
 
(safe
 
for
 
shared
 
branches)
 
git
 
cherry-pick
 
<id>
 
Apply
 
specific
 
commit
 
from
 
another
 
branch
 
 
5.3
 
Merge
 
vs
 
Rebase
 
 
Merge
 
Rebase
 
History
 
Preserves
 
all
 
history
 
with
 
merge
 
commit
 
Creates
 
clean
 
linear
 
history
 
Use
 
for
 
Feature
 
branches
 
being
 
merged
 
to
 
main
 
Cleaning
 
up
 
local
 
commits
 
before
 
PR
 
Danger
 
Can
 
create
 
messy
 
history
 
NEVER
 
rebase
 
shared/public
 
branches

## Section / Page 19

5.4
 
PR
 
Workflow
 
(Your
 
Azure
 
DevOps
 
Setup)
 
Feature
 
branch
 
→
 
Push
 
→
 
Create
 
Pull
 
Request
 
→
 
Code
 
Review
 
→
 
Approve
 
→
 
Merge
 
to
 
main
 
→
 
Delete
 
branch
 
 
PR
 
Template
 
(.azuredevops/pull_request_template.md)
 
•
 
Folder
 
must
 
be
 
named
 
exactly:
 
.azuredevops
 
•
 
File
 
must
 
be
 
named
 
exactly:
 
pull_request_template.md
 
•
 
Must
 
be
 
merged
 
into
 
the
 
main
 
(default)
 
branch
 
to
 
auto-load
 
on
 
new
 
PRs
 
 
5.5
 
Branching
 
Strategies
 
•
 
GitFlow
 
—
 
main
 
+
 
develop
 
+
 
feature/*
 
+
 
release/*
 
+
 
hotfix/*
 
(complex,
 
for
 
large
 
teams)
 
•
 
GitHub
 
Flow
 
—
 
main
 
+
 
short-lived
 
feature
 
branches
 
(simple,
 
for
 
most
 
teams)
 
•
 
Trunk-based
 
—
 
everyone
 
commits
 
to
 
main
 
frequently
 
(advanced,
 
needs
 
strong
 
CI)

## Section / Page 20

SECTION
 
6:
 
LINUX
 
—
 
COMPLETE
 
GUIDE
 
 
6.1
 
File
 
System
 
Structure
 
Directory
 
Purpose
 
/etc
 
System
 
configuration
 
files
 
/var/log
 
Log
 
files
 
/home
 
User
 
home
 
directories
 
/tmp
 
Temporary
 
files
 
(cleared
 
on
 
reboot)
 
/opt
 
Optional/third-party
 
applications
 
(Tomcat,
 
etc.)
 
/usr/local/bin
 
Locally
 
installed
 
executables
 
/proc
 
Virtual
 
filesystem
 
—
 
running
 
process
 
info
 
 
6.2
 
File
 
Permissions
 
Permission
 
format:
 
rwx
 
=
 
r(4)
 
+
 
w(2)
 
+
 
x(1)
 
Permission
 
Number
 
Meaning
 
rwxr-xr-x
 
755
 
Owner:
 
full
 
access
 
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
 
access
 
|
 
Group+Others:
 
no
 
access
 
chmod
 
755
 
file
       
#
 
change
 
permissions
 
chown
 
user:group
 
file
 
#
 
change
 
owner
 
setfacl
 
-m
 
u:user:rwx
 
file
  
#
 
fine-grained
 
ACL
 
 
6.3
 
Key
 
Commands
 
Reference
 
Files
 
and
 
Navigation
 
ls
 
-la
 
|
 
pwd
 
|
 
cd
 
|
 
mkdir
 
-p
 
|
 
rm
 
-rf
 
cp
 
-r
 
|
 
mv
 
|
 
cat
 
|
 
tail
 
-f
 
|
 
head
 
-n
 
20
 
grep
 
-r
 
"pattern"
 
dir/
 
|
 
grep
 
-i
 
|
 
grep
 
-v
 
find
 
/
 
-name
 
"*.log"
 
|
 
find
 
.
 
-type
 
f
 
-mtime
 
-7
 
Process
 
Management
 
ps
 
aux
 
|
 
grep
 
process
 
top
 
/
 
htop
 
kill
 
-9
 
PID
 
|
 
pkill
 
name
 
|
 
pgrep
 
name
 
nohup
 
command
 
&
   
#
 
run
 
in
 
background,
 
survives
 
logout
 
Service
 
Management
 
systemctl
 
start/stop/restart/status
 
service
 
systemctl
 
enable
 
service
   
#
 
start
 
on
 
boot

## Section / Page 21

journalctl
 
-u
 
nginx
 
-f
     
#
 
follow
 
service
 
logs
 
Networking
 
ip
 
addr
 
|
 
ping
 
|
 
curl
 
|
 
ss
 
-tulpn
 
ufw
 
allow
 
22
 
|
 
ufw
 
enable
 
ssh
 
-i
 
key.pem
 
user@ip
 
|
 
scp
 
file
 
user@ip:/path
 
 
6.4
 
Piping
 
and
 
Redirection
 
cmd
 
>
 
file
           
#
 
overwrite
 
output
 
to
 
file
 
cmd
 
>>
 
file
          
#
 
append
 
output
 
to
 
file
 
cmd
 
2>&1
            
#
 
redirect
 
stderr
 
to
 
stdout
 
cmd1
 
|
 
cmd2
          
#
 
pipe
 
output
 
of
 
cmd1
 
to
 
cmd2
 
ps
 
aux
 
|
 
grep
 
java
 
|
 
wc
 
-l
  
#
 
chain
 
example
 
 
6.5
 
User
 
Management
 
useradd
 
-m
 
user
          
#
 
create
 
user
 
with
 
home
 
dir
 
userdel
 
-r
 
user
          
#
 
delete
 
user
 
and
 
home
 
dir
 
passwd
 
user
              
#
 
set
 
password
 
usermod
 
-aG
 
docker
 
user
  
#
 
add
 
user
 
to
 
group
 
groups
 
user
 
|
 
id
 
user
    
#
 
check
 
user
 
groups
 
 
6.6
 
Ulimit
 
Tuning
 
(Your
 
Project)
 
Ulimits
 
control
 
system
 
resource
 
limits
 
per
 
process.
 
You
 
tuned
 
these
 
in
 
your
 
Reverse
 
Proxy
 
project
 
to
 
handle
 
concurrent
 
Tomcat
 
+
 
Apache
 
+
 
PostgreSQL
 
load.
 
ulimit
 
-n
         
#
 
check
 
open
 
file
 
limit
 
ulimit
 
-n
 
65535
   
#
 
increase
 
open
 
files
 
#
 
Permanent:
 
edit
 
/etc/security/limits.conf

## Section / Page 22

SECTION
 
7:
 
TERRAFORM
 
—
 
COMPLETE
 
GUIDE
 
 
7.1
 
What
 
is
 
Terraform?
 
Terraform
 
is
 
an
 
Infrastructure
 
as
 
Code
 
(IaC)
 
tool
 
by
 
HashiCorp.
 
You
 
describe
 
your
 
desired
 
infrastructure
 
in
 
.tf
 
files,
 
and
 
Terraform
 
creates
 
it.
 
•
 
Declarative
 
—
 
you
 
say
 
WHAT
 
you
 
want,
 
Terraform
 
figures
 
out
 
HOW
 
•
 
Provider-agnostic
 
—
 
works
 
with
 
AWS,
 
Azure,
 
GCP,
 
and
 
1000+
 
others
 
•
 
Idempotent
 
—
 
running
 
same
 
config
 
multiple
 
times
 
=
 
same
 
result
 
 
7.2
 
Core
 
Workflow
 
init
 
→
 
plan
 
→
 
apply
 
→
 
destroy
 
Command
 
Action
 
terraform
 
init
 
Download
 
providers
 
and
 
modules,
 
initialize
 
backend
 
terraform
 
plan
 
Preview
 
changes
 
—
 
shows
 
what
 
will
 
be
 
created/modified/destroyed
 
terraform
 
apply
 
Execute
 
the
 
plan
 
and
 
create/update
 
infrastructure
 
terraform
 
destroy
 
Delete
 
all
 
infrastructure
 
managed
 
by
 
this
 
config
 
terraform
 
state
 
list
 
Show
 
all
 
resources
 
in
 
state
 
terraform
 
output
 
Show
 
output
 
values
 
terraform
 
workspace
 
new/select/list
 
Manage
 
workspaces
 
(dev/staging/prod)
 
terraform
 
import
 
Import
 
existing
 
infrastructure
 
into
 
state
 
 
7.3
 
Key
 
Files
 
File
 
Purpose
 
main.tf
 
Resource
 
definitions
 
variables.tf
 
Input
 
variable
 
declarations
 
outputs.tf
 
Output
 
value
 
definitions
 
terraform.tfvars
 
Variable
 
values
 
(not
 
committed
 
to
 
git
 
if
 
secrets)
 
terraform.tfstate
 
Current
 
state
 
of
 
infrastructure
 
—
 
DO
 
NOT
 
edit
 
manually
 
backend.tf
 
Remote
 
state
 
configuration
 
(S3
 
+
 
DynamoDB)
 
 
7.4
 
Resource
 
Block
 
Example
 
resource
 
"aws_instance"
 
"web"
 
{
 
  
ami
           
=
 
var.ami_id
 
  
instance_type
 
=
 
"t2.micro"
 
  
tags
 
=
 
{
 
    
Name
 
=
 
"WebServer"
 
  
}

## Section / Page 23

}
 
 
7.5
 
State
 
Management
 
terraform.tfstate
 
tracks
 
all
 
resources
 
Terraform
 
manages.
 
For
 
teams,
 
store
 
state
 
remotely:
 
#
 
backend.tf
 
—
 
store
 
state
 
in
 
S3
 
with
 
DynamoDB
 
locking
 
terraform
 
{
 
  
backend
 
"s3"
 
{
 
    
bucket
         
=
 
"my-terraform-state"
 
    
key
            
=
 
"prod/terraform.tfstate"
 
    
region
         
=
 
"us-east-1"
 
    
dynamodb_table
 
=
 
"terraform-locks"
 
  
}
 
}
 
 
7.6
 
Modules
 
Modules
 
are
 
reusable
 
blocks
 
of
 
Terraform
 
code
 
—
 
like
 
functions.
 
Write
 
once,
 
use
 
everywhere.
 
module
 
"vpc"
 
{
 
  
source
 
=
 
"./modules/vpc"
 
  
cidr
   
=
 
var.vpc_cidr
 
}

## Section / Page 24

SECTION
 
8:
 
AZURE
 
DEVOPS
 
—
 
COMPLETE
 
GUIDE
 
This
 
is
 
YOUR
 
territory!
 
You
 
built
 
actual
 
Azure
 
DevOps
 
projects.
 
Connect
 
everything
 
here
 
to
 
your
 
real
 
work.
 
This
 
is
 
where
 
you
 
should
 
be
 
most
 
confident.
 
 
8.1
 
Azure
 
DevOps
 
Overview
 
Azure
 
DevOps
 
is
 
Microsoft's
 
all-in-one
 
platform
 
for
 
DevOps.
 
Available
 
at
 
dev.azure.com.
 
Service
 
Purpose
 
You
 
Used
 
It?
 
Azure
 
Boards
 
Plan
 
work
 
—
 
Epics,
 
Features,
 
Tasks,
 
Kanban
 
boards
 
YES
 
Azure
 
Repos
 
Git
 
source
 
control
 
YES
 
Azure
 
Pipelines
 
CI/CD
 
automation
 
(YAML)
 
YES
 
Azure
 
Test
 
Plans
 
Manual
 
+
 
automated
 
testing
 
Theory
 
only
 
Azure
 
Artifacts
 
Package
 
registry
 
(npm,
 
NuGet)
 
Theory
 
only
 
 
8.2
 
Azure
 
Boards
 
—
 
Project
 
Management
 
Work
 
Item
 
Hierarchy
 
(Agile
 
Process)
 
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
 
Level
 
What
 
It
 
Is
 
Example
 
Epic
 
Large
 
business
 
objective
 
Build
 
CI/CD
 
Infrastructure
 
Feature
 
Functional
 
component
 
Automated
 
Tomcat
 
Deployment
 
User
 
Story
 
Requirement
 
from
 
user
 
perspective
 
As
 
a
 
dev,
 
I
 
want
 
auto-deploy
 
on
 
push
 
Task
 
Technical
 
implementation
 
work
 
Configure
 
azure-pipelines.yml
 
Bug
 
Defect
 
or
 
issue
 
Pipeline
 
fails
 
on
 
merge
 
to
 
main
 
 
Work
 
Item
 
States
 
New
 
→
 
Active
 
→
 
Resolved
 
→
 
Closed
 
Key
 
Features
 
•
 
Kanban
 
Board
 
—
 
drag-and-drop
 
workflow
 
visualization
 
•
 
Backlog
 
—
 
prioritized
 
list
 
of
 
all
 
work
 
•
 
Sprints
 
—
 
2-week
 
time-boxed
 
delivery
 
cycles
 
•
 
Queries
 
—
 
custom
 
filtered
 
views
 
(owner,
 
state,
 
priority,
 
tags)
 
•
 
Dashboards
 
—
 
sprint
 
burndown,
 
build
 
history,
 
velocity
 
widgets
 
Access
 
Levels
 
•
 
Stakeholder
 
(Free)
 
—
 
view
 
boards,
 
add
 
work
 
items.
 
No
 
code/pipeline
 
access.
 
•
 
Basic
 
(Free
 
for
 
5
 
users)
 
—
 
full
 
access
 
to
 
Boards,
 
Repos,
 
Pipelines.
 
•
 
Basic
 
+
 
Test
 
Plans
 
—
 
adds
 
Azure
 
Test
 
Plans.
 
Your
 
Project:
 
You
 
configured
 
Epics,
 
Features,
 
Tasks
 
hierarchy,
 
Query
 
Management
 
for
 
custom
 
views,
 
User
 
Roles/Permissions,
 
and
 
PR
 
Templates.

## Section / Page 25

8.3
 
Azure
 
Repos
 
—
 
Source
 
Control
 
Git
 
vs
 
TFVC
 
Feature
 
Git
 
TFVC
 
Local
 
copy
 
Full
 
history
 
Only
 
current
 
version
 
Offline
 
work
 
Yes
 
No
 
Popularity
 
Industry
 
standard
 
Legacy/enterprise
 
Use
 
Always
 
use
 
Git
 
Only
 
if
 
mandated
 
 
PR
 
Template
 
Setup
 
(Your
 
Project)
 
•
 
Create
 
folder:
 
.azuredevops/
 
at
 
repo
 
root
 
•
 
Create
 
file:
 
pull_request_template.md
 
inside
 
that
 
folder
 
•
 
Commit
 
to
 
main
 
branch
 
—
 
template
 
auto-loads
 
on
 
all
 
future
 
PRs
 
 
8.4
 
Azure
 
Pipelines
 
—
 
CI/CD
 
Pipeline
 
Hierarchy
 
Pipeline
 
→
 
Stage
 
→
 
Job
 
→
 
Step
 
→
 
Task
 
Level
 
Description
 
Pipeline
 
Full
 
automation
 
workflow
 
(azure-pipelines.yml)
 
Stage
 
Major
 
phase:
 
Build,
 
Test,
 
Deploy
 
Job
 
Unit
 
of
 
work
 
running
 
on
 
an
 
agent.
 
Max
 
256
 
jobs
 
per
 
stage.
 
Step
 
Individual
 
action
 
(script,
 
task)
 
Task
 
Pre-built
 
operations
 
(AzureCLI,
 
CopyFiles,
 
etc.)
 
 
Agent
 
Types
 
Type
 
Description
 
When
 
to
 
Use
 
Microsoft-hosted
 
Fresh
 
VM
 
for
 
each
 
run.
 
Auto-maintained.
 
General
 
purpose
 
builds
 
Self-hosted
 
Your
 
own
 
machine.
 
More
 
control
 
and
 
speed.
 
Custom
 
dependencies,
 
access
 
to
 
internal
 
networks
 
Your
 
Project:
 
You
 
set
 
up
 
a
 
self-hosted
 
agent
 
on
 
your
 
Azure
 
VM.
 
This
 
allows
 
the
 
pipeline
 
to
 
directly
 
deploy
 
to
 
Tomcat
 
on
 
the
 
same
 
machine
 
without
 
network
 
hops.
 
 
8.5
 
Self-Hosted
 
Agent
 
Setup
 
(Step
 
by
 
Step)
 
From
 
Organization
 
Settings
 
→
 
Agent
 
Pools
 
→
 
Default
 
→
 
New
 
Agent:
 
#
 
1.
 
Download
 
and
 
extract
 
agent
 
mkdir
 
~/myagent
 
&&
 
cd
 
~/myagent
 
tar
 
zxvf
 
vsts-agent-linux-x64-*.tar.gz

## Section / Page 26

#
 
2.
 
Configure
 
agent
 
./config.sh
 
  
Server
 
URL:
 
https://dev.azure.com/akhilbm13
 
  
Auth
 
type:
 
PAT
 
(Personal
 
Access
 
Token)
 
  
Agent
 
pool:
 
Default
 
  
Agent
 
name:
 
myagent
 
 
#
 
3.
 
Start
 
agent
 
./run.sh
 
#
 
Agent
 
shows:
 
Listening
 
for
 
Jobs
 
 
Common
 
Agent
 
Errors
 
Error
 
Cause
 
Fix
 
Agent
 
Offline
 
run.sh
 
not
 
running
 
Run
 
./run.sh
 
again
 
VS30063
 
Unauthorized
 
PAT
 
missing
 
permissions
 
Create
 
PAT
 
with
 
Agent
 
Pools:
 
Read
 
&
 
Manage
 
Pool
 
not
 
found
 
Used
 
agent
 
name
 
instead
 
of
 
pool
 
name
 
Use
 
pool:
 
name:
 
Default
 
Pipeline
 
uses
 
MS
 
agent
 
vmImage
 
still
 
in
 
YAML
 
Remove
 
vmImage,
 
use
 
pool:
 
name:
 
Default
 
 
8.6
 
YAML
 
Pipeline
 
—
 
Your
 
Project
 
Final
 
Working
 
Pipeline
 
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
 
 
stages:
 
-
 
stage:
 
Build
 
  
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
 
 
-
 
stage:
 
DeployTomcat1
 
  
dependsOn:
 
Build
 
  
condition:
 
succeeded()
 
  
jobs:
 
  
-
 
job:
 
Deploy1
 
    
steps:
 
    
-
 
script:
 
cp
 
target/*.war
 
/opt/tomcat1/webapps/

## Section / Page 27

-
 
stage:
 
DeployTomcat2
 
  
dependsOn:
 
DeployTomcat1
 
  
condition:
 
succeeded()
 
  
jobs:
 
  
-
 
job:
 
Deploy2
 
    
steps:
 
    
-
 
script:
 
cp
 
target/*.war
 
/opt/tomcat2/webapps/
 
 
YAML
 
Rules
 
(Critical)
 
•
 
Use
 
pool:
 
name:
 
Default
 
—
 
NOT
 
agent
 
name
 
•
 
Indentation
 
uses
 
spaces
 
only
 
—
 
never
 
tabs
 
•
 
Stage
 
names
 
must
 
be
 
alphanumeric
 
(hyphens
 
allowed,
 
no
 
spaces)
 
•
 
Every
 
stage
 
needs
 
at
 
least
 
one
 
job
 
•
 
dependsOn
 
+
 
condition:
 
succeeded()
 
—
 
chain
 
stages
 
safely
 
 
8.7
 
Variables
 
in
 
Pipelines
 
Type
 
Where
 
Defined
 
Use
 
Case
 
Inline
 
In
 
YAML
 
file
 
Non-sensitive
 
config
 
values
 
Pipeline
 
UI
 
Pipeline
 
settings
 
in
 
portal
 
Env-specific
 
values
 
Variable
 
Groups
 
(Library)
 
Shared
 
across
 
pipelines
 
Reusable
 
config
 
Key
 
Vault
 
Azure
 
Key
 
Vault
 
integration
 
Secrets:
 
passwords,
 
keys

## Section / Page 28

SECTION
 
9:
 
YOUR
 
PROJECTS
 
—
 
COMPLETE
 
DETAILS
 
Interview
 
Gold:
 
These
 
3
 
projects
 
ARE
 
your
 
biggest
 
strength.
 
Know
 
every
 
component,
 
every
 
decision,
 
every
 
trade-off.
 
This
 
section
 
covers
 
all
 
three
 
in
 
full
 
depth.
 
 
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
 
Architecture
 
Overview
 
Developer
 
pushes
 
code
 
to
 
Azure
 
Repo
 
(main
 
branch)
 
         
↓
 
Azure
 
DevOps
 
Pipeline
 
triggers
 
(self-hosted
 
agent
 
on
 
same
 
VM)
 
         
↓
 
Build
 
→
 
Test
 
→
 
Deploy
 
Tomcat1
 
→
 
Deploy
 
Tomcat2
 
 
Traffic
 
Flow:
 
User
 
hits:
 
http://your-vm-ip/project1
 
         
↓
 
Port
 
80
 
(Apache
 
Reverse
 
Proxy)
 
receives
 
request
 
         
↓
 
Apache
 
ProxyPass
 
config:
 
/project1
 
→
 
localhost:7789
 
         
↓
 
Tomcat
 
1
 
processes
 
and
 
responds
 
→
 
back
 
through
 
Apache
 
→
 
User
 
 
Components
 
Component
 
Details
 
Azure
 
DevOps
 
Boards
 
Epics,
 
Features,
 
Tasks,
 
Bug
 
tracking,
 
PR
 
templates
 
Azure
 
DevOps
 
Repos
 
Git
 
repository
 
with
 
branch
 
policies
 
Azure
 
DevOps
 
Pipelines
 
Multi-stage
 
YAML
 
CI/CD
 
pipeline
 
Self-hosted
 
Agent
 
Linux
 
VM
 
running
 
pipeline
 
jobs
 
(myagent)
 
Tomcat
 
1
 
Port
 
7789
 
—
 
isolated
 
Tomcat
 
instance
 
Tomcat
 
2
 
Port
 
8888
 
—
 
isolated
 
Tomcat
 
instance
 
Apache
 
HTTP
 
Server
 
Port
 
80
 
—
 
Reverse
 
Proxy
 
(public
 
entry
 
point)
 
PostgreSQL
 
Database
 
with
 
non-root
 
user,
 
encryption,
 
backups
 
UFW
 
/
 
Security
 
Groups
 
Only
 
Port
 
80
 
exposed;
 
7789/8888
 
internal
 
only
 
 
Tomcat
 
Setup
 
—
 
Key
 
Steps
 
•
 
Download
 
Tomcat
 
to
 
/opt/tomcat1
 
and
 
/opt/tomcat2
 
(physical
 
copies,
 
NOT
 
symlinks)
 
•
 
Assign
 
ownership:
 
sudo
 
chown
 
-R
 
azureuser:azureuser
 
/opt/tomcat1
 
/opt/tomcat2
 
•
 
server.xml:
 
Tomcat1
 
on
 
port
 
7789,
 
Tomcat2
 
on
 
port
 
8888
 
(change
 
shutdown
 
port
 
too
 
to
 
avoid
 
conflict)
 
•
 
Deploy
 
WAR
 
via
 
symbolic
 
links:
 
ln
 
-s
 
/opt/project1
 
/opt/tomcat1/webapps/project1
 
 
Apache
 
Reverse
 
Proxy
 
Configuration
 
sudo
 
a2enmod
 
proxy
 
proxy_http

## Section / Page 29

<VirtualHost
 
*:80>
 
    
ProxyPreserveHost
 
On
 
    
ProxyPass
 
/project1
 
http://127.0.0.1:7789/project1
 
    
ProxyPassReverse
 
/project1
 
http://127.0.0.1:7789/project1
 
    
ProxyPass
 
/project2
 
http://127.0.0.1:8888/project2
 
    
ProxyPassReverse
 
/project2
 
http://127.0.0.1:8888/project2
 
    
ErrorLog
 
${APACHE_LOG_DIR}/proxy-error.log
 
</VirtualHost>
 
 
Why
 
Separate
 
Tomcat
 
Instances?
 
(Key
 
Interview
 
Answer)
 
Context
 
paths
 
share
 
a
 
single
 
Java
 
process.
 
If
 
that
 
process
 
crashes,
 
ALL
 
apps
 
go
 
down.
 
Separate
 
instances
 
give:
 
•
 
✅
 
Fault
 
isolation
 
—
 
Tomcat
 
1
 
crash
 
does
 
not
 
affect
 
Tomcat
 
2
 
•
 
✅
 
Independent
 
resource
 
allocation
 
—
 
each
 
instance
 
gets
 
its
 
own
 
JVM
 
heap
 
•
 
✅
 
Independent
 
scaling
 
—
 
restart
 
or
 
scale
 
one
 
without
 
touching
 
the
 
other
 
•
 
✅
 
Better
 
security
 
—
 
one
 
app
 
cannot
 
access
 
another
 
app's
 
resources
 
 
LGTM
 
Monitoring
 
Stack
 
Log
 
Collection
 
Flow:
 
Apache/Tomcat
 
→
 
generate
 
logs
 
Promtail
 
→
 
reads
 
/var/log/apache2/*.log
 
and
 
/opt/tomcat*/logs/*.out
 
         
↓
 
sends
 
to
 
Loki
 
(port
 
3100)
 
Loki
 
→
 
stores
 
logs
 
with
 
labels
 
and
 
timestamps
 
         
↓
 
Grafana
 
(port
 
3000)
 
→
 
query
 
Loki
 
→
 
visualize
 
in
 
dashboards
 
 
Component
 
Role
 
Port
 
Grafana
 
Dashboard
 
UI
 
—
 
visualization,
 
alerts
 
3000
 
Loki
 
Log
 
storage
 
and
 
indexing
 
3100
 
Promtail
 
Log
 
collector
 
agent
 
(reads
 
log
 
files)
 
9080
 
Mimir
 
Metrics
 
storage
 
(optional
 
in
 
your
 
project)
 
-
 
Tempo
 
Distributed
 
traces
 
(optional
 
in
 
your
 
project)
 
-
 
 
LGTM
 
vs
 
CloudWatch
 
 
LGTM
 
(Loki)
 
CloudWatch
 
Cost
 
Free
 
and
 
open-source
 
Paid
 
service
 
Platform
 
Works
 
anywhere
 
(AWS,
 
Azure,
 
on-prem)
 
AWS-only
 
Control
 
Self-hosted,
 
full
 
control
 
Managed
 
by
 
AWS
 
Integration
 
Works
 
with
 
your
 
mixed
 
AWS+Azure
 
setup
 
Better
 
native
 
AWS
 
integration
 
 
Troubleshooting
 
Reference
 
(Project
 
1)

## Section / Page 30

Error
 
Cause
 
Fix
 
403
 
Access
 
Denied
 
Tomcat
 
RemoteAddrValve
 
blocks
 
external
 
IPs
 
Comment
 
out
 
the
 
Valve
 
in
 
context.xml,
 
restart
 
404
 
Not
 
Found
 
Page
 
does
 
not
 
exist
 
or
 
wrong
 
path
 
Verify
 
symlink
 
points
 
to
 
folder
 
with
 
index.html
 
Permission
 
Denied
 
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
 
Port
 
conflict
 
Both
 
Tomcats
 
on
 
same
 
shutdown
 
port
 
Change
 
shutdown
 
port
 
in
 
Tomcat2
 
server.xml
 
to
 
8006
 
Pipeline
 
not
 
triggering
 
Pushed
 
to
 
wrong
 
branch
 
(feature
 
not
 
main)
 
git
 
merge
 
feature
 
&&
 
git
 
push
 
origin
 
main
 
Git
 
auth
 
failed
 
Password
 
login
 
blocked
 
by
 
Azure
 
DevOps
 
Use
 
PAT
 
token
 
as
 
password
 
 
PROJECT
 
2:
 
Kubernetes
 
Cluster
 
on
 
AWS
 
via
 
kOps
 
Architecture
 
Overview
 
Setup
 
Flow:
 
1.
 
EC2
 
instance
 
(t2.medium)
 
with
 
IAM
 
permissions
 
→
 
install
 
kOps
 
2.
 
kops
 
create
 
cluster
 
→
 
kops
 
update
 
cluster
 
--yes
 
3.
 
Cluster:
 
1
 
Master
 
+
 
2
 
Worker
 
nodes
 
4.
 
Push
 
Docker
 
images
 
to
 
ECR
 
5.
 
kubectl
 
apply
 
-f
 
manifests/
 
→
 
Pods
 
running
 
 
Traffic
 
Flow:
 
User
 
→
 
AWS
 
LoadBalancer
 
→
 
Frontend
 
Service
 
→
 
Frontend
 
Pods
 
(3
 
replicas)
 
                                         
↓
 
                               
Backend
 
Service
 
(ClusterIP)
 
                                         
↓
 
K8s
 
internal
 
DNS
 
                               
Backend
 
Pods
 
(3
 
replicas)
 
                                         
↓
 
                               
Database
 
Service
 
(ClusterIP)
 
                                         
↓
 
                         
StatefulSet:
 
postgres-0,
 
postgres-1,
 
postgres-2
 
                         
(each
 
with
 
own
 
PVC
 
→
 
EBS
 
volume)
 
 
Kubernetes
 
Resources
 
You
 
Created
 
Resource
 
Type
 
Details
 
frontend-deployment
 
Deployment
 
3
 
replicas,
 
Apache
 
image,
 
LoadBalancer
 
service
 
backend-deployment
 
Deployment
 
3
 
replicas,
 
Node.js
 
image,
 
ClusterIP
 
service
 
database-statefulset
 
StatefulSet
 
3
 
replicas,
 
PostgreSQL,
 
ClusterIP
 
service,
 
PVC
 
per
 
pod
 
frontend-service
 
LoadBalancer
 
External
 
IP
 
from
 
AWS
 
ELB

## Section / Page 31

backend-service
 
ClusterIP
 
backend.default.svc.cluster.local:30
00
 
database-service
 
ClusterIP
 
postgres.default.svc.cluster.local:54
32
 
 
Key
 
Decisions
 
Explained
 
•
 
StatefulSet
 
for
 
PostgreSQL:
 
pods
 
get
 
stable
 
identity
 
(postgres-0,
 
postgres-1).
 
Each
 
reconnects
 
to
 
same
 
EBS
 
volume
 
after
 
restart.
 
Deployment
 
would
 
use
 
random
 
names
 
and
 
lose
 
data.
 
•
 
ClusterIP
 
for
 
backend:
 
backend
 
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
 
•
 
3
 
replicas:
 
ensures
 
high
 
availability.
 
If
 
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
 
pod.
 
 
Project
 
Limitations
 
(Know
 
These!)
 
•
 
❌
 
EBS
 
is
 
AZ-specific
 
—
 
if
 
the
 
AZ
 
fails,
 
your
 
database
 
becomes
 
inaccessible
 
•
 
❌
 
Single
 
master
 
node
 
—
 
if
 
master
 
goes
 
down,
 
cluster
 
stops
 
accepting
 
new
 
commands
 
•
 
❌
 
Manual
 
pod
 
scaling
 
—
 
no
 
Horizontal
 
Pod
 
Autoscaler
 
configured
 
•
 
❌
 
No
 
database
 
replication
 
—
 
StatefulSet
 
pods
 
don't
 
sync
 
data
 
between
 
them
 
 
Improvements
 
for
 
Production
 
•
 
✅
 
Replace
 
EBS
 
with
 
EFS
 
(Elastic
 
File
 
System)
 
for
 
multi-AZ
 
shared
 
storage
 
•
 
✅
 
3
 
master
 
nodes
 
for
 
High
 
Availability
 
control
 
plane
 
•
 
✅
 
Enable
 
Cluster
 
Autoscaler
 
for
 
automatic
 
node
 
scaling
 
•
 
✅
 
Configure
 
HPA
 
for
 
automatic
 
pod
 
scaling
 
based
 
on
 
CPU/memory
 
•
 
✅
 
Set
 
up
 
PostgreSQL
 
master-slave
 
replication
 
 
PROJECT
 
3:
 
LGTM
 
Monitoring
 
Stack
 
(Covered
 
under
 
Project
 
1
 
above.
 
The
 
LGTM
 
stack
 
was
 
part
 
of
 
Project
 
1
 
but
 
is
 
worth
 
knowing
 
as
 
a
 
standalone
 
topic.)
 
When
 
VM
 
Restarts
 
—
 
Recovery
 
Steps
 
sudo
 
systemctl
 
start
 
grafana-server
 
sudo
 
/opt/loki/loki-linux-amd64
 
-config.file=/etc/loki/loki-config.yaml
 
sudo
 
/usr/local/bin/promtail
 
-config.file=/etc/loki/promtail-config.yaml
 
 
Health
 
Check
 
curl
 
http://localhost:3100/ready
   
#
 
check
 
if
 
Loki
 
is
 
running
 
http://<VM-IP>:3000
               
#
 
Grafana
 
UI
 
—
 
admin/admin

## Section / Page 32

SECTION
 
10:
 
ANSIBLE
 
—
 
COMPLETE
 
GUIDE
 
 
10.1
 
What
 
is
 
Ansible?
 
Ansible
 
is
 
an
 
open-source
 
configuration
 
management
 
tool.
 
You
 
write
 
YAML
 
playbooks
 
once
 
and
 
apply
 
them
 
to
 
hundreds
 
of
 
servers
 
simultaneously.
 
•
 
Agentless
 
—
 
uses
 
SSH
 
only,
 
nothing
 
to
 
install
 
on
 
target
 
servers
 
•
 
Idempotent
 
—
 
running
 
the
 
same
 
playbook
 
twice
 
gives
 
the
 
same
 
result.
 
Safe
 
to
 
re-run.
 
•
 
Push-based
 
—
 
Ansible
 
controller
 
pushes
 
commands
 
to
 
servers
 
•
 
YAML-based
 
—
 
easy
 
to
 
read
 
and
 
write
 
 
10.2
 
Key
 
Components
 
Component
 
Description
 
Control
 
Node
 
Machine
 
where
 
Ansible
 
is
 
installed
 
and
 
commands
 
are
 
run
 
from
 
Managed
 
Nodes
 
Target
 
servers
 
being
 
configured.
 
No
 
Ansible
 
needed
 
on
 
them.
 
Inventory
 
File
 
listing
 
managed
 
nodes
 
(IP
 
addresses
 
or
 
hostnames)
 
Playbook
 
YAML
 
file
 
containing
 
automation
 
tasks
 
Task
 
Single
 
unit
 
of
 
work
 
(install
 
nginx,
 
copy
 
file,
 
restart
 
service)
 
Module
 
Pre-built
 
function
 
for
 
common
 
tasks
 
(apt,
 
yum,
 
copy,
 
service,
 
shell)
 
Handler
 
Task
 
that
 
runs
 
only
 
when
 
notified
 
(e.g.,
 
restart
 
nginx
 
after
 
config
 
change)
 
Role
 
Reusable,
 
organized
 
collection
 
of
 
tasks
 
Vault
 
Encrypted
 
storage
 
for
 
secrets
 
(passwords,
 
API
 
keys)
 
 
10.3
 
Ad-hoc
 
Commands
 
ansible
 
all
 
-m
 
ping
                                        
#
 
test
 
connectivity
 
ansible
 
webservers
 
-m
 
shell
 
-a
 
"uptime"
                   
#
 
run
 
command
 
ansible
 
all
 
-m
 
apt
 
-a
 
"name=nginx
 
state=present"
 
--become
 
#
 
install
 
package
 
 
10.4
 
Playbook
 
Structure
 
-
 
name:
 
Setup
 
Web
 
Server
 
  
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
 
  
tasks:
 
    
-
 
name:
 
Install
 
nginx
 
      
apt:

## Section / Page 33

name:
 
nginx
 
        
state:
 
present
 
      
notify:
 
Restart
 
nginx
 
 
    
-
 
name:
 
Copy
 
config
 
      
template:
 
        
src:
 
nginx.conf.j2
 
        
dest:
 
/etc/nginx/nginx.conf
 
      
notify:
 
Restart
 
nginx
 
 
  
handlers:
 
    
-
 
name:
 
Restart
 
nginx
 
      
service:
 
        
name:
 
nginx
 
        
state:
 
restarted
 
 
10.5
 
Ansible
 
vs
 
Chef
 
vs
 
Puppet
 
Feature
 
Ansible
 
Chef/Puppet
 
Architecture
 
Push
 
(controller
 
→
 
nodes)
 
Pull
 
(nodes
 
fetch
 
config)
 
Agent
 
No
 
agent
 
needed
 
—
 
SSH
 
only
 
Agent
 
required
 
on
 
each
 
node
 
Language
 
YAML
 
(easy)
 
Ruby
 
DSL
 
(harder)
 
Learning
 
curve
 
Easy
 
Steeper

## Section / Page 34

SECTION
 
11:
 
NETWORKING
 
FUNDAMENTALS
 
 
11.1
 
OSI
 
Model
 
(7
 
Layers)
 
Memory
 
trick:
 
"All
 
People
 
Seem
 
To
 
Need
 
Data
 
Processing"
 
(top
 
to
 
bottom)
 
Layer
 
Name
 
Protocol/Example
 
7
 
Application
 
HTTP,
 
HTTPS,
 
FTP,
 
SMTP,
 
DNS
 
6
 
Presentation
 
SSL/TLS,
 
encryption,
 
compression
 
5
 
Session
 
Session
 
establishment,
 
authentication
 
4
 
Transport
 
TCP
 
(reliable),
 
UDP
 
(fast)
 
3
 
Network
 
IP,
 
routing,
 
packets
 
2
 
Data
 
Link
 
Ethernet,
 
MAC
 
addresses,
 
frames
 
1
 
Physical
 
Cables,
 
fiber,
 
radio
 
signals,
 
bits
 
 
11.2
 
TCP
 
vs
 
UDP
 
Feature
 
TCP
 
UDP
 
Connection
 
Connection-oriented
 
(3-way
 
handshake)
 
Connectionless
 
Reliability
 
Guaranteed
 
delivery,
 
ordered
 
Best-effort,
 
no
 
guarantee
 
Speed
 
Slower
 
(overhead)
 
Faster
 
(no
 
overhead)
 
Use
 
cases
 
HTTP,
 
SSH,
 
FTP,
 
database
 
connections
 
DNS,
 
video
 
streaming,
 
gaming
 
TCP
 
3-Way
 
Handshake
 
SYN
 
→
 
SYN-ACK
 
→
 
ACK
 
(establishes
 
connection
 
before
 
data
 
transfer)
 
 
11.3
 
Key
 
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
 
HTTPS
 
443
 
-
 
FTP
 
21
 
-
 
DNS
 
53
 
-
 
SMTP
 
25
 
-
 
RDP
 
3389
 
Windows
 
EC2
 
MySQL
 
3306
 
-
 
PostgreSQL
 
5432
 
Your
 
database

## Section / Page 35

Tomcat
 
1
 
7789
 
Your
 
project
 
Tomcat
 
2
 
8888
 
Your
 
project
 
Grafana
 
3000
 
Your
 
project
 
Loki
 
3100
 
Your
 
project
 
 
11.4
 
DNS
 
DNS
 
(Domain
 
Name
 
System)
 
translates
 
domain
 
names
 
to
 
IP
 
addresses.
 
•
 
A
 
record
 
—
 
maps
 
domain
 
to
 
IPv4
 
address
 
•
 
CNAME
 
—
 
maps
 
domain
 
to
 
another
 
domain
 
name
 
(alias)
 
•
 
MX
 
record
 
—
 
mail
 
server
 
for
 
domain
 
•
 
TXT
 
record
 
—
 
verification
 
and
 
other
 
text
 
data
 
 
11.5
 
Other
 
Key
 
Concepts
 
Concept
 
Explanation
 
NAT
 
Maps
 
private
 
IPs
 
to
 
public
 
IP.
 
PAT
 
=
 
multiple
 
private
 
IPs
 
share
 
one
 
public
 
IP
 
using
 
ports.
 
DHCP
 
Auto-assigns
 
IP
 
to
 
devices.
 
DORA:
 
Discover
 
→
 
Offer
 
→
 
Request
 
→
 
Acknowledge
 
VPN
 
Encrypted
 
tunnel
 
over
 
public
 
internet
 
for
 
secure
 
private
 
communication
 
VLAN
 
Logical
 
network
 
segmentation
 
on
 
a
 
switch
 
—
 
reduces
 
broadcast,
 
improves
 
security
 
IPv4
 
vs
 
IPv6
 
IPv4:
 
32-bit,
 
4.3B
 
addresses
 
|
 
IPv6:
 
128-bit,
 
340
 
undecillion,
 
built-in
 
security
 
•
 
Private
 
IP
 
ranges:
 
10.x.x.x
 
|
 
172.16-31.x.x
 
|
 
192.168.x.x
 
•
 
Hub:
 
Layer
 
1
 
(broadcasts
 
all)
 
|
 
Switch:
 
Layer
 
2
 
(MAC-based)
 
|
 
Router:
 
Layer
 
3
 
(IP-based)

## Section / Page 36

SECTION
 
12:
 
INTERVIEW
 
PREPARATION
 
 
12.1
 
Your
 
Introduction
 
(Polished
 
—
 
90
 
Seconds)
 
Template:
 
"I
 
am
 
Akhil,
 
a
 
DevOps
 
and
 
Cloud
 
Engineer
 
from
 
Bengaluru.
 
I
 
have
 
hands-on
 
experience
 
building
 
multi-tier
 
cloud
 
architectures
 
on
 
AWS
 
and
 
Azure.
 
I
 
have
 
built
 
three
 
real
 
projects
 
—
 
a
 
Kubernetes
 
cluster
 
on
 
AWS
 
using
 
kOps
 
with
 
a
 
full-stack
 
Todo
 
application,
 
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
 
am
 
proficient
 
in
 
Docker,
 
Kubernetes,
 
Azure
 
DevOps,
 
Terraform,
 
and
 
Linux.
 
I
 
am
 
excited
 
about
 
the
 
opportunity
 
at
 
[company]
 
because
 
[reason]."
 
 
12.2
 
Project
 
Answers
 
(Practice
 
These
 
Aloud)
 
Walk
 
me
 
through
 
Project
 
1
 
(Azure
 
DevOps
 
+
 
Reverse
 
Proxy)
 
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
 
I
 
configured
 
Apache
 
HTTP
 
Server
 
as
 
a
 
reverse
 
proxy
 
on
 
port
 
80
 
to
 
route
 
traffic
 
—
 
/project1
 
goes
 
to
 
Tomcat
 
1
 
and
 
/project2
 
goes
 
to
 
Tomcat
 
2.
 
UFW
 
firewall
 
ensures
 
only
 
port
 
80
 
is
 
publicly
 
accessible.
 
I
 
automated
 
deployments
 
with
 
an
 
Azure
 
DevOps
 
multi-stage
 
YAML
 
pipeline
 
using
 
a
 
self-hosted
 
agent
 
on
 
the
 
same
 
VM.
 
PostgreSQL
 
serves
 
as
 
the
 
persistent
 
data
 
layer
 
with
 
a
 
non-root
 
user
 
and
 
encrypted
 
passwords.
 
The
 
LGTM
 
stack
 
—
 
Promtail,
 
Loki,
 
and
 
Grafana
 
—
 
provides
 
real-time
 
log
 
monitoring.
 
Walk
 
me
 
through
 
Project
 
2
 
(Kubernetes
 
on
 
AWS)
 
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
 
kOps,
 
which
 
automatically
 
created
 
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
 
load
 
balancers.
 
I
 
deployed
 
the
 
frontend
 
with
 
a
 
Deployment
 
(3
 
replicas)
 
exposed
 
via
 
a
 
LoadBalancer
 
service,
 
the
 
backend
 
via
 
ClusterIP,
 
and
 
PostgreSQL
 
via
 
a
 
StatefulSet
 
with
 
PersistentVolumeClaims
 
backed
 
by
 
EBS
 
volumes.
 
Services
 
communicate
 
using
 
Kubernetes
 
internal
 
DNS.
 
Why
 
StatefulSet
 
for
 
the
 
database?
 
StatefulSet
 
maintains
 
stable
 
pod
 
identities
 
—
 
postgres-0,
 
postgres-1,
 
postgres-2.
 
Each
 
pod
 
is
 
always
 
associated
 
with
 
the
 
same
 
PersistentVolume.
 
When
 
a
 
pod
 
restarts,
 
it
 
reconnects
 
to
 
the
 
same
 
EBS
 
volume,
 
so
 
data
 
is
 
preserved.
 
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
 
on
 
restart.
 
Why
 
did
 
you
 
choose
 
Loki
 
over
 
CloudWatch?
 
My
 
project
 
used
 
both
 
AWS
 
and
 
Azure,
 
so
 
CloudWatch
 
only
 
covered
 
the
 
AWS
 
side.
 
Loki
 
is
 
open-source,
 
free,
 
and
 
works
 
across
 
any
 
platform
 
—
 
AWS,
 
Azure,
 
or
 
on-premise.
 
For
 
a
 
mixed
 
environment
 
like
 
mine,
 
Loki
 
with
 
Grafana
 
gives
 
a
 
single
 
observability
 
interface
 
regardless
 
of
 
cloud
 
provider.
 
CloudWatch
 
would
 
have
 
been
 
more
 
appropriate
 
if
 
I
 
were
 
100%
 
on
 
AWS.
 
What
 
would
 
you
 
improve?
 
For
 
Project
 
1
 
—
 
add
 
health
 
checks
 
with
 
automatic
 
failover.
 
For
 
Project
 
2
 
—
 
replace
 
EBS
 
with
 
EFS
 
for
 
multi-AZ
 
resilient
 
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
 
and
 
implement
 
Horizontal
 
Pod
 
Autoscaler.
 
For
 
Project
 
3
 
—
 
add
 
Mimir
 
for
 
metrics
 
and
 
Tempo
 
for
 
distributed
 
tracing
 
to
 
complete
 
the
 
full
 
LGTM
 
stack.
 
 
12.3
 
Handling
 
Gaps
 
When
 
you
 
don't
 
know
 
something:
 
"I
 
haven't
 
worked
 
with
 
that
 
directly,
 
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
 
learn
 
it
 
by
 
[approach]."
 
 
12.4
 
Common
 
Interview
 
Questions
 
by
 
Topic

## Section / Page 37

DevOps
 
Culture
 
•
 
What
 
is
 
DevOps?
 
—
 
Culture
 
+
 
practices
 
uniting
 
Dev
 
and
 
Ops.
 
Collaborate.
 
Automate.
 
Deliver.
 
•
 
Difference
 
between
 
CI
 
and
 
CD?
 
—
 
CI:
 
auto-build/test
 
every
 
push.
 
CD:
 
auto-deploy
 
tested
 
build.
 
•
 
What
 
is
 
Infrastructure
 
as
 
Code?
 
—
 
Terraform,
 
Ansible
 
—
 
manage
 
infra
 
through
 
version-controlled
 
config
 
files.
 
Docker
 
Questions
 
•
 
Docker
 
image
 
vs
 
container?
 
—
 
Image
 
=
 
blueprint
 
(read-only).
 
Container
 
=
 
running
 
instance.
 
•
 
What
 
is
 
a
 
Dockerfile?
 
—
 
Instructions
 
to
 
build
 
an
 
image,
 
layer
 
by
 
layer.
 
•
 
What
 
is
 
Docker
 
Compose?
 
—
 
Multi-container
 
app
 
in
 
one
 
YAML
 
file.
 
docker-compose
 
up
 
-d.
 
Kubernetes
 
Questions
 
•
 
Pod
 
vs
 
Deployment?
 
—
 
Pod
 
=
 
smallest
 
unit.
 
Deployment
 
=
 
manages
 
ReplicaSets
 
which
 
manage
 
Pods.
 
•
 
How
 
does
 
K8s
 
handle
 
pod
 
failure?
 
—
 
kubelet
 
detects
 
crash,
 
Controller
 
Manager
 
schedules
 
new
 
pod,
 
self-healing.
 
•
 
What
 
is
 
a
 
Service
 
in
 
Kubernetes?
 
—
 
Stable
 
network
 
endpoint
 
for
 
pods
 
(ClusterIP/NodePort/LoadBalancer).
 
Git
 
Questions
 
•
 
Merge
 
vs
 
Rebase?
 
—
 
Merge
 
preserves
 
full
 
history.
 
Rebase
 
creates
 
clean
 
linear
 
history.
 
•
 
git
 
reset
 
--hard
 
vs
 
--soft?
 
—
 
hard:
 
deletes
 
changes.
 
soft:
 
keeps
 
changes
 
staged.
 
 
12.5
 
Technical
 
Terms
 
Glossary
 
Term
 
Definition
 
High
 
Availability
 
(HA)
 
System
 
keeps
 
running
 
even
 
if
 
components
 
fail
 
(multiple
 
replicas,
 
AZs)
 
Idempotency
 
Running
 
same
 
operation
 
multiple
 
times
 
=
 
same
 
result
 
(no
 
side
 
effects)
 
Declarative
 
You
 
describe
 
WHAT
 
you
 
want,
 
system
 
figures
 
out
 
HOW
 
Self-healing
 
System
 
automatically
 
restarts
 
failed
 
components
 
Load
 
Balancing
 
Distribute
 
requests
 
evenly
 
across
 
multiple
 
instances
 
Service
 
Discovery
 
Automatic
 
finding
 
of
 
services
 
via
 
DNS
 
(e.g.,
 
Kubernetes
 
internal
 
DNS)
 
Persistent
 
Storage
 
Data
 
survives
 
pod/container
 
restarts
 
(PV,
 
EBS)
 
Least
 
Privilege
 
Give
 
only
 
minimum
 
permissions
 
needed
 
for
 
a
 
task
 
Reverse
 
Proxy
 
Server
 
that
 
receives
 
requests
 
and
 
forwards
 
to
 
backend
 
(Apache,
 
Nginx)
 
Stateless
 
App
 
does
 
not
 
store
 
session
 
data
 
—
 
any
 
replica
 
can
 
handle
 
any
 
request
 
Stateful
 
App
 
stores
 
data
 
—
 
needs
 
stable
 
identity
 
and
 
persistent
 
storage

## Section / Page 38

SECTION
 
13:
 
HOW
 
TO
 
STUDY
 
THIS
 
DOCUMENT
 
 
Recommended
 
Study
 
Order
 
Day
 
1
 
—
 
Quick
 
Foundation
 
•
 
Read
 
PART
 
1
 
(Quick
 
Revision)
 
completely
 
—
 
20-30
 
minutes
 
•
 
Understand
 
Project
 
1
 
architecture
 
end
 
to
 
end
 
•
 
Understand
 
Project
 
2
 
architecture
 
end
 
to
 
end
 
Day
 
2
 
—
 
Core
 
Topics
 
•
 
Read
 
Section
 
1
 
(AWS)
 
fully
 
•
 
Read
 
Section
 
2
 
(Kubernetes)
 
fully
 
•
 
Practice
 
kubectl
 
commands
 
out
 
loud
 
Day
 
3
 
—
 
DevOps
 
Tools
 
•
 
Read
 
Section
 
3
 
(Docker)
 
+
 
Section
 
4
 
(Jenkins)
 
•
 
Read
 
Section
 
5
 
(Git)
 
•
 
Read
 
Section
 
8
 
(Azure
 
DevOps)
 
—
 
your
 
strongest
 
area
 
Day
 
4
 
—
 
Infrastructure
 
+
 
Project
 
Deep
 
Dive
 
•
 
Read
 
Section
 
7
 
(Terraform)
 
•
 
Read
 
Section
 
6
 
(Linux)
 
•
 
Read
 
Section
 
9
 
(Your
 
Projects)
 
—
 
memorize
 
the
 
architecture
 
flows
 
Day
 
5
 
—
 
Interview
 
Prep
 
•
 
Read
 
Section
 
10
 
(Ansible)
 
+
 
Section
 
11
 
(Networking)
 
•
 
Read
 
Section
 
12
 
(Interview
 
Preparation)
 
completely
 
•
 
Practice
 
all
 
project
 
answers
 
aloud
 
—
 
time
 
yourself
 
at
 
90
 
seconds
 
each
 
Before
 
Every
 
Interview
 
•
 
Re-read
 
PART
 
1
 
(Quick
 
Revision)
 
—
 
takes
 
only
 
20
 
minutes
 
•
 
Run
 
through
 
project
 
answers
 
once
 
aloud
 
 
Key
 
Things
 
to
 
Memorize
 
•
 
✅
 
Architecture
 
flows
 
for
 
all
 
3
 
projects
 
•
 
✅
 
Why
 
StatefulSet
 
for
 
database
 
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
 
Self-hosted
 
agent
 
setup
 
steps
 
and
 
common
 
errors
 
•
 
✅
 
kubectl
 
top
 
10
 
commands
 
•
 
✅
 
OSI
 
model
 
7
 
layers
 
•
 
✅
 
Key
 
ports
 
table
 
•
 
✅
 
Security
 
Group
 
vs
 
NACL
 
•
 
✅
 
Your
 
90-second
 
introduction
 
 
Interview
 
Day
 
Tips
 
•
 
Connect
 
every
 
concept
 
to
 
your
 
actual
 
projects
 
—
 
don't
 
just
 
define
 
terms

## Section / Page 39

•
 
If
 
you
 
don't
 
know:
 
say
 
"I
 
haven't
 
used
 
that
 
directly
 
but
 
based
 
on
 
[X]..."
 
•
 
Ask
 
clarifying
 
questions
 
before
 
answering
 
complex
 
scenarios
 
•
 
Mention
 
your
 
project
 
limitations
 
honestly
 
—
 
it
 
shows
 
maturity
 
•
 
End
 
answers
 
by
 
mentioning
 
what
 
you
 
would
 
improve
 
—
 
shows
 
growth
 
mindset
 
 
You've
 
Got
 
This!
 
You
 
have
 
built
 
3
 
real,
 
production-grade
 
projects.
 
Most
 
candidates
 
only
 
have
 
theory.
 
Own
 
your
 
experience
 
confidently.

