# 📘 55 Core DevOps & Cloud Interview Questions

> *High-yield guide extracted from `Akhil_55QA_Interview_Guide.pdf` for mobile & web GitHub viewing.*

---

## Section / Page 1

AKHIL
 
B
 
M
 
DevOps
 
Intern
 
Interview
 
Prep
 
Solytics
 
Partners
 
—
 
55
 
Questions
 
&
 
Answers
 
Read
 
this
 
the
 
night
 
before.
 
You
 
are
 
ready.
 
💪
 
 
 
Projects
 
CI/CD
 
Docker
 
Kubernetes
 
AWS/Azure
 
Scenarios
 
 
 
Interview:
 
45
 
Minutes
 
Intro
 
(5)
 
|
 
Projects
 
(15)
 
|
 
Technical
 
(15)
 
|
 
Scenarios
 
(7)
 
|
 
Your
 
Q
 
(3)
 
Your
 
Biggest
 
Strength
 
3
 
REAL
 
projects!
 
Most
 
freshers
 
have
 
ZERO.

## Section / Page 2

📌
 
YOUR
 
INTRODUCTION
 
—
 
Memorize
 
This!
 
 
Good
 
morning,
 
my
 
name
 
is
 
Akhil
 
B
 
M.
 
I'm
 
from
 
Chitradurga,
 
Karnataka.
 
I
 
recently
 
completed
 
my
 
Bachelor
 
of
 
Engineering
 
in
 
Information
 
Science
 
and
 
Engineering
 
from
 
BMS
 
Institute
 
of
 
Technology,
 
Bangalore.
 
I
 
have
 
hands-on
 
experience
 
in
 
cloud
 
and
 
DevOps
 
through
 
my
 
training,
 
where
 
I
 
worked
 
with
 
AWS
 
services
 
like
 
EC2,
 
S3,
 
and
 
IAM,
 
along
 
with
 
Linux
 
system
 
administration
 
and
 
basic
 
scripting.
 
I
 
also
 
have
 
exposure
 
to
 
Azure
 
services
 
such
 
as
 
Virtual
 
Machines,
 
VNets,
 
and
 
Network
 
Security
 
Groups,
 
and
 
I
 
have
 
worked
 
on
 
CI/CD
 
pipelines
 
using
 
Azure
 
DevOps
 
and
 
Jenkins.
 
In
 
one
 
of
 
my
 
projects,
 
I
 
built
 
a
 
multi-tier
 
application
 
where
 
I
 
implemented
 
a
 
reverse
 
proxy
 
setup
 
and
 
handled
 
networking
 
and
 
security,
 
which
 
helped
 
me
 
understand
 
how
 
real-world
 
systems
 
are
 
deployed
 
and
 
managed.
 
I'm
 
a
 
quick
 
learner
 
and
 
very
 
interested
 
in
 
starting
 
my
 
career
 
in
 
cloud
 
operations,
 
especially
 
in
 
Azure,
 
where
 
I
 
can
 
contribute
 
and
 
continue
 
improving
 
my
 
skills.
 
 
⚡
 
DELIVERY
 
TIPS:
 
✅
 
Speak
 
slowly
 
and
 
clearly
   
✅
 
Make
 
eye
 
contact
 
(look
 
at
 
camera)
   
✅
 
Be
 
confident
 
—
 
you
 
have
 
REAL
 
projects!
 
✅
 
Do
 
NOT
 
read
 
—
 
speak
 
naturally
   
✅
 
Smile
 
while
 
speaking
   
✅
 
Total
 
time:
 
~90
 
seconds

## Section / Page 3

🏆
 
YOUR
 
PROJECTS
 
(Q1–Q10)
 
 
Q1.
 
Walk
 
me
 
through
 
Project
 
1
 
—
 
Azure
 
DevOps
 
Setup
 
&
 
Multi-Stage
 
Automation
 
PROBLEM:
 
Jenkins
 
needs
 
manual
 
setup
 
of
 
Docker,
 
Nexus,
 
SonarQube,
 
plugins
 
—
 
very
 
time
 
consuming.
 
Azure
 
DevOps
 
gives
 
everything
 
in
 
one
 
place:
 
Boards,
 
Repos,
 
Pipelines,
 
Artifacts.
 
 
AZURE
 
BOARDS:
 
Configured
 
Agile
 
process
 
—
 
Epic
 
→
 
Feature
 
→
 
User
 
Story
 
→
 
Task/Bug.
 
Used
 
Query
 
Management
 
for
 
custom
 
views
 
to
 
track
 
real-time
 
task
 
progress.
 
 
AZURE
 
REPOS:
 
Git
 
repository
 
+
 
branch
 
policies.
 
PR
 
Template
 
at:
 
.azuredevops/pull_request_template.md
 
(must
 
commit
 
to
 
main!)
 
Policies:
 
Minimum
 
1
 
reviewer
 
|
 
No
 
self-approval
 
|
 
Pipeline
 
must
 
pass
 
before
 
merge.
 
 
SELF
 
HOSTED
 
AGENT:
 
Set
 
up
 
on
 
Azure
 
VM
 
(myagent).
 
1.
 
Download
 
→
 
2.
 
Extract
 
→
 
3.
 
./config.sh
 
(URL,
 
PAT,
 
Pool:
 
Default)
 
→
 
4.
 
./run.sh
 
Why?
 
Same
 
VM
 
as
 
deployment
 
—
 
direct
 
file
 
access,
 
faster,
 
more
 
secure.
 
 
PIPELINE
 
(4
 
Stages):
 
Stage
 
1:
 
BUILD
 
→
 
mvn
 
clean
 
package
 
→
 
creates
 
WAR
 
file
 
Stage
 
2:
 
TEST
 
→
 
mvn
 
test
 
→
 
runs
 
unit
 
tests
 
Stage
 
3:
 
DEPLOY
 
NODE
 
1
 
→
 
copy
 
WAR
 
→
 
restart
 
Stage
 
4:
 
DEPLOY
 
NODE
 
2
 
→
 
copy
 
WAR
 
→
 
restart
 
Each
 
stage:
 
dependsOn
 
+
 
condition:
 
succeeded()
 
—
 
if
 
Build
 
fails,
 
nothing
 
else
 
runs!
 
 
LGTM:
 
Promtail
 
reads
 
logs
 
→
 
Loki
 
(3100)
 
stores
 
→
 
Grafana
 
(3000)
 
visualizes.
 
 
Q2.
 
Walk
 
me
 
through
 
Project
 
2
 
—
 
Reverse
 
Proxy
 
&
 
Secured
 
Stack
 
PROBLEM:
 
Multiple
 
Java
 
apps
 
need
 
different
 
ports.
 
Exposing
 
all
 
ports
 
publicly
 
=
 
security
 
risk.
 
 
WHAT
 
I
 
BUILT
 
on
 
Azure
 
VM:
 
├──
 
Apache
 
HTTP
 
Server
 
(Port
 
80)
 
→
 
PUBLIC
 
facing
 
├──
 
Tomcat
 
Instance
 
1
 
(Port
 
7789)
 
→
 
INTERNAL
 
only
 
├──
 
Tomcat
 
Instance
 
2
 
(Port
 
8888)
 
→
 
INTERNAL
 
only
 
└──
 
PostgreSQL
 
(Port
 
5432)
 
→
 
INTERNAL
 
only
 
 
TRAFFIC
 
FLOW:
 
User
 
→
 
Port
 
80
 
→
 
Apache
 
ProxyPass
 
→
 
localhost:7789
 
→
 
Tomcat
 
→
 
Response
 
 
APACHE
 
CONFIG:
 
ProxyPass
 
/project1
 
http://127.0.0.1:7789/project1
 
ProxyPass
 
/project2
 
http://127.0.0.1:8888/project2
 
 
POSTGRESQL
 
SECURITY:
 
Non-root
 
user
 
|
 
Encrypted
 
passwords
 
|
 
Roles
 
&
 
Privileges
 
|
 
Automated
 
backups
 
 
NETWORK
 
SECURITY
 
(UFW):
 
Port
 
80
 
→
 
OPEN
 
|
 
Port
 
22
 
→
 
OPEN
 
|
 
Port
 
7789/8888/5432
 
→
 
CLOSED
 
(internal
 
only)
 
 
LINUX
 
TUNING:
 
Ulimit
 
adjustments
 
to
 
handle
 
concurrent
 
load
 
of
 
all
 
services
 
on
 
one
 
VM.
 
 
Q3.
 
Walk
 
me
 
through
 
Project
 
3
 
—
 
Kubernetes
 
Todo
 
App
 
on
 
AWS
 
via
 
kOps

## Section / Page 4

PROBLEM:
 
Docker
 
Compose
 
lacks
 
auto-healing,
 
auto-scaling,
 
load
 
balancing
 
for
 
production.
 
Migrated
 
Todo
 
app
 
to
 
Kubernetes
 
on
 
AWS.
 
 
APPLICATION:
 
Frontend
 
(Apache)
 
+
 
Backend
 
(Node.js
 
+
 
Express)
 
+
 
Database
 
(PostgreSQL)
 
 
CLUSTER
 
SETUP:
 
1.
 
EC2
 
t2.medium
 
with
 
IAM
 
permissions
 
→
 
install
 
kOps
 
+
 
kubectl
 
2.
 
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
 
config
 
4.
 
kops
 
update
 
cluster
 
--yes
 
→
 
creates
 
VPC,
 
Subnets,
 
SGs,
 
1
 
Master
 
+
 
2
 
Workers,
 
ELB
 
5.
 
kops
 
validate
 
cluster
 
→
 
verify
 
healthy
 
 
KUBERNETES
 
RESOURCES:
 
Frontend
 
→
 
Deployment
 
(3
 
replicas)
 
+
 
LoadBalancer
 
Service
 
(creates
 
AWS
 
ELB)
 
Backend
 
→
 
Deployment
 
(3
 
replicas)
 
+
 
ClusterIP
 
(internal:
 
backend-service.default.svc.cluster.local:3000)
 
Database
 
→
 
StatefulSet
 
(3
 
replicas)
 
+
 
ClusterIP
 
(postgres.default.svc.cluster.local:5432)
 
         
→
 
Each
 
pod
 
gets
 
OWN
 
PVC
 
→
 
EBS
 
volume
 
→
 
data
 
survives
 
restarts!
 
 
TRAFFIC:
 
User
 
→
 
AWS
 
ELB
 
→
 
Frontend
 
Pods
 
→
 
K8s
 
DNS
 
→
 
Backend
 
Pods
 
→
 
DB
 
Pods
 
 
Q4.
 
Why
 
2
 
separate
 
Tomcat
 
instances
 
instead
 
of
 
context
 
paths?
 
Context
 
paths
 
share
 
ONE
 
JVM
 
process.
 
If
 
it
 
crashes
 
→
 
ALL
 
apps
 
go
 
down.
 
 
❌
 
Single
 
Point
 
of
 
Failure:
 
Tomcat
 
crash
 
→
 
both
 
apps
 
down
 
✅
 
Separate:
 
only
 
affected
 
app
 
goes
 
down,
 
other
 
keeps
 
running
 
 
❌
 
Resource
 
Sharing:
 
both
 
apps
 
compete
 
for
 
same
 
JVM
 
heap
 
memory
 
✅
 
Separate:
 
dedicated
 
resources
 
for
 
each
 
(Tomcat1:
 
512MB,
 
Tomcat2:
 
2GB)
 
 
❌
 
No
 
Independent
 
Restart:
 
context
 
paths
 
→
 
both
 
apps
 
restart
 
together
 
✅
 
Separate:
 
restart
 
one,
 
other
 
keeps
 
serving
 
users
 
 
❌
 
Security
 
Risk:
 
vulnerability
 
in
 
one
 
can
 
affect
 
the
 
other
 
✅
 
Separate:
 
proper
 
isolation
 
between
 
applications
 
 
Industry
 
standard
 
is
 
separate
 
instances
 
for
 
production-grade
 
deployments.
 
 
Q5.
 
Why
 
StatefulSet
 
for
 
the
 
database
 
and
 
not
 
Deployment?
 
Deployment
 
gives
 
RANDOM
 
pod
 
names
 
(postgres-abc123).
 
If
 
pod
 
restarts
 
→
 
new
 
random
 
name
 
→
 
loses
 
PVC
 
connection
 
→
 
DATA
 
LOST!
 
❌
 
 
StatefulSet
 
gives
 
STABLE
 
pod
 
names:
 
postgres-0,
 
postgres-1,
 
postgres-2
 
Each
 
pod
 
gets
 
its
 
OWN
 
PersistentVolumeClaim
 
(PVC).
 
When
 
pod
 
restarts
 
→
 
reconnects
 
to
 
SAME
 
EBS
 
volume
 
→
 
data
 
is
 
always
 
safe!
 
✅
 
 
That
 
is
 
why
 
databases
 
ALWAYS
 
use
 
StatefulSet,
 
not
 
Deployment.
 
 
Q6.
 
Why
 
did
 
you
 
choose
 
Loki
 
over
 
CloudWatch
 
for
 
monitoring?
 
CloudWatch:
 
AWS-only
 
❌
 
|
 
Paid
 
service
 
❌
 
|
 
Limited
 
to
 
AWS
 
resources
 
❌

## Section / Page 5

Loki:
 
Free
 
&
 
open
 
source
 
✅
 
|
 
Works
 
across
 
AWS
 
AND
 
Azure
 
✅
 
|
 
Self-hosted
 
full
 
control
 
✅
 
 
My
 
project
 
used
 
BOTH
 
AWS
 
and
 
Azure.
 
CloudWatch
 
would
 
only
 
cover
 
the
 
AWS
 
side.
 
Loki
 
+
 
Grafana
 
gives
 
ONE
 
dashboard
 
monitoring
 
both
 
Azure
 
VM
 
and
 
AWS
 
K8s
 
cluster.
 
That
 
is
 
why
 
Loki
 
was
 
the
 
right
 
choice
 
for
 
my
 
mixed-cloud
 
environment.
 
 
Q7.
 
Why
 
did
 
you
 
use
 
a
 
self-hosted
 
agent
 
instead
 
of
 
Microsoft-hosted?
 
Microsoft
 
hosted
 
agent
 
runs
 
on
 
a
 
DIFFERENT
 
VM.
 
Cannot
 
access
 
my
 
Tomcat
 
folders
 
directly.
 
Would
 
need
 
SSH
 
setup
 
→
 
complex
 
and
 
less
 
secure.
 
 
Self-hosted
 
agent
 
runs
 
on
 
SAME
 
VM
 
as
 
Tomcat.
 
Pipeline
 
directly
 
copies
 
WAR
 
files:
 
cp
 
target/*.war
 
/opt/tomcat1/webapps/
 
 
✅
 
Same
 
VM
 
→
 
direct
 
file
 
access
 
✅
 
Faster
 
deployment
 
—
 
no
 
network
 
hops
 
✅
 
More
 
secure
 
—
 
no
 
external
 
access
 
needed
 
 
Q8.
 
What
 
are
 
the
 
limitations
 
of
 
your
 
projects?
 
Project
 
1
 
(Azure
 
DevOps
 
+
 
Reverse
 
Proxy):
 
❌
 
No
 
health
 
checks
 
or
 
auto
 
failover
 
❌
 
No
 
HTTPS
 
(HTTP
 
only)
 
❌
 
Single
 
VM
 
→
 
no
 
high
 
availability
 
❌
 
Only
 
implemented
 
LG
 
of
 
LGTM
 
(no
 
Mimir/Tempo)
 
 
Project
 
2
 
(Kubernetes):
 
❌
 
EBS
 
is
 
AZ
 
specific
 
→
 
if
 
AZ
 
fails,
 
database
 
goes
 
down
 
❌
 
Single
 
master
 
node
 
→
 
not
 
HA
 
❌
 
No
 
auto
 
scaling
 
(HPA
 
not
 
configured)
 
❌
 
No
 
database
 
replication
 
between
 
pods
 
 
I
 
am
 
honest
 
about
 
these
 
because
 
knowing
 
limitations
 
drives
 
improvement.
 
 
Q9.
 
What
 
would
 
you
 
improve
 
in
 
your
 
projects?
 
Project
 
1:
 
✅
 
Add
 
health
 
checks
 
with
 
automatic
 
failover
 
✅
 
Implement
 
HTTPS
 
with
 
SSL
 
certificate
 
(Let's
 
Encrypt)
 
✅
 
Add
 
Mimir
 
for
 
metrics
 
and
 
Tempo
 
for
 
traces
 
(complete
 
LGTM)
 
✅
 
Containerize
 
applications
 
with
 
Docker
 
 
Project
 
2
 
(Kubernetes):
 
✅
 
Replace
 
EBS
 
with
 
EFS
 
for
 
multi-AZ
 
persistent
 
storage
 
✅
 
3
 
master
 
nodes
 
for
 
HA
 
control
 
plane
 
✅
 
Enable
 
HPA
 
for
 
automatic
 
pod
 
scaling
 
based
 
on
 
CPU/memory
 
✅
 
Set
 
up
 
PostgreSQL
 
master-slave
 
replication
 
✅
 
Add
 
Ingress
 
controller
 
instead
 
of
 
LoadBalancer
 
per
 
service

## Section / Page 6

Q10.
 
Walk
 
me
 
through
 
pipeline
 
end
 
to
 
end
 
Developer
 
writes
 
code
 
on
 
feature
 
branch
 
→
 
git
 
push
 
origin
 
feature
 
→
 
Creates
 
Pull
 
Request
 
→
 
PR
 
template
 
loads
 
automatically
 
→
 
Reviewer
 
reviews,
 
approves,
 
links
 
to
 
Azure
 
Boards
 
work
 
item
 
→
 
Merge
 
to
 
main
 
branch
 
→
 
Pipeline
 
triggers
 
automatically
 
(trigger:
 
main)
 
→
 
Self-hosted
 
agent
 
(myagent)
 
picks
 
up
 
job
 
→
 
Stage
 
1:
 
mvn
 
clean
 
package
 
(builds
 
WAR)
 
→
 
Stage
 
2:
 
mvn
 
test
 
(runs
 
unit
 
tests)
 
→
 
Stage
 
3:
 
Deploy
 
to
 
Tomcat
 
1
 
(port
 
7789)
 
→
 
Stage
 
4:
 
Deploy
 
to
 
Tomcat
 
2
 
(port
 
8888)
 
→
 
LGTM
 
monitors
 
logs
 
in
 
real
 
time
 
→
 
User
 
accesses
 
via
 
Apache
 
port
 
80
 
→
 
routes
 
to
 
correct
 
Tomcat

## Section / Page 7

🔄
 
CI/CD
 
(Q11–Q18)
 
 
Q11.
 
What
 
is
 
CI/CD?
 
CI
 
=
 
Continuous
 
Integration
 
Automatically
 
build
 
and
 
test
 
code
 
on
 
every
 
push
 
to
 
repository.
 
Catches
 
bugs
 
early
 
before
 
they
 
reach
 
production!
 
✅
 
 
CD
 
=
 
Continuous
 
Delivery
 
Auto
 
deploy
 
to
 
staging.
 
Human
 
approves
 
before
 
production.
 
 
CD
 
=
 
Continuous
 
Deployment
 
Fully
 
automated
 
all
 
the
 
way
 
to
 
production.
 
No
 
human
 
approval.
 
 
In
 
my
 
project:
 
CI
 
→
 
Push
 
to
 
main
 
→
 
Build
 
→
 
Test
 
CD
 
→
 
Deploy
 
to
 
Tomcat
 
1
 
and
 
Tomcat
 
2
 
automatically
 
 
Q12.
 
What
 
is
 
GitHub
 
Actions?
 
GitHub
 
Actions
 
is
 
CI/CD
 
automation
 
built
 
DIRECTLY
 
inside
 
GitHub.
 
You
 
create
 
a
 
YAML
 
workflow
 
file
 
at:
 
.github/workflows/main.yml
 
 
Triggered
 
by
 
GitHub
 
events:
 
push,
 
pull
 
request,
 
scheduled
 
cron.
 
 
Key
 
concepts:
 
├──
 
Workflow
 
→
 
full
 
automation
 
file
 
(.yml)
 
├──
 
Event
 
→
 
what
 
triggers
 
it
 
(push,
 
PR)
 
├──
 
Job
 
→
 
unit
 
of
 
work
 
├──
 
Step
 
→
 
individual
 
action
 
└──
 
Runner
 
→
 
machine
 
that
 
runs
 
jobs
 
(GitHub-hosted
 
or
 
self-hosted)
 
 
Very
 
similar
 
to
 
Azure
 
DevOps
 
—
 
both
 
YAML-based,
 
both
 
support
 
self-hosted
 
runners.
 
 
Q13.
 
Jenkins
 
vs
 
Azure
 
DevOps?
 
Jenkins:
 
-
 
Open
 
source,
 
self-hosted
 
(you
 
manage
 
the
 
server)
 
-
 
1800+
 
plugins,
 
Jenkinsfile
 
(Groovy)
 
-
 
Need
 
separate
 
tools
 
for
 
repos,
 
project
 
tracking
 
-
 
Used
 
in
 
my
 
INTERNSHIP
 
 
Azure
 
DevOps:
 
-
 
Microsoft
 
managed
 
platform
 
-
 
Boards
 
+
 
Repos
 
+
 
Pipelines
 
+
 
Artifacts
 
ALL
 
in
 
one
 
place
 
-
 
YAML
 
pipeline,
 
no
 
server
 
management
 
-
 
Used
 
in
 
my
 
MAIN
 
PROJECTS
 
 
I
 
chose
 
Azure
 
DevOps
 
because
 
my
 
infrastructure
 
was
 
on
 
Azure
 
—
 
native
 
integration.
 
 
Q14.
 
What
 
happens
 
if
 
one
 
stage
 
fails
 
in
 
your
 
pipeline?

## Section / Page 8

Each
 
stage
 
uses:
 
dependsOn
 
+
 
condition:
 
succeeded()
 
 
If
 
Build
 
fails:
 
→
 
Test
 
stage
 
will
 
NOT
 
run
 
→
 
Deploy
 
stages
 
will
 
NOT
 
run
 
→
 
Pipeline
 
stops
 
immediately
 
→
 
Developer
 
gets
 
notified
 
 
This
 
prevents:
 
❌
 
Deploying
 
broken
 
code
 
to
 
servers
 
❌
 
Running
 
tests
 
on
 
a
 
failed
 
build
 
❌
 
Wasting
 
time
 
and
 
resources
 
 
It
 
is
 
a
 
safety
 
net
 
for
 
the
 
entire
 
pipeline!
 
✅
 
 
Q15.
 
What
 
is
 
a
 
self-hosted
 
agent
 
and
 
how
 
did
 
you
 
set
 
it
 
up?
 
A
 
self-hosted
 
agent
 
is
 
YOUR
 
OWN
 
machine
 
registered
 
to
 
run
 
Azure
 
DevOps
 
pipeline
 
jobs.
 
 
SETUP
 
STEPS:
 
1.
 
Download
 
from:
 
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
 
Extract:
 
tar
 
zxvf
 
vsts-agent-linux-x64-*.tar.gz
 
3.
 
Configure:
 
./config.sh
 
   
-
 
Server
 
URL:
 
https://dev.azure.com/akhilbm13
 
   
-
 
Auth:
 
PAT
 
token
 
   
-
 
Pool:
 
Default
 
(NOT
 
agent
 
name!)
 
   
-
 
Agent
 
name:
 
myagent
 
4.
 
Start:
 
./run.sh
 
→
 
Shows:
 
Listening
 
for
 
Jobs
 
✅
 
5.
 
Verify:
 
Azure
 
DevOps
 
→
 
Agent
 
Pools
 
→
 
Default
 
→
 
myagent
 
ONLINE
 
(green)
 
 
Common
 
errors:
 
VS30063
 
Unauthorized
 
→
 
Wrong
 
PAT
 
permissions
 
(need
 
Agent
 
Pools:
 
Read
 
&
 
Manage)
 
Pool
 
not
 
found
 
→
 
Used
 
agent
 
name
 
instead
 
of
 
pool
 
name
 
Agent
 
offline
 
→
 
run.sh
 
not
 
running
 
 
Q16.
 
What
 
is
 
a
 
PR
 
template
 
and
 
where
 
do
 
you
 
store
 
it?
 
PR
 
template
 
is
 
a
 
markdown
 
file
 
that
 
automatically
 
loads
 
when
 
anyone
 
creates
 
a
 
PR.
 
 
Location
 
(MUST
 
be
 
exact):
 
.azuredevops/pull_request_template.md
 
 
MUST
 
be
 
committed
 
to
 
the
 
MAIN
 
branch
 
to
 
auto-load!
 
 
Template
 
includes:
 
-
 
Type
 
of
 
PR
 
(Feature/Bugfix/Enhancement)
 
-
 
Description
 
of
 
changes
 
-
 
Related
 
work
 
item
 
link
 
-
 
Testing
 
done
 
-
 
Post
 
deployment
 
tasks
 
 
✅
 
Standardizes
 
code
 
reviews
 
✅
 
Every
 
PR
 
links
 
to
 
work
 
item

## Section / Page 9

✅
 
Reviewers
 
quickly
 
understand
 
changes
 
 
Q17.
 
What
 
are
 
branch
 
policies?
 
Branch
 
policies
 
enforce
 
standards
 
before
 
code
 
can
 
be
 
merged
 
to
 
main.
 
 
Policies
 
I
 
configured:
 
✅
 
Minimum
 
1
 
reviewer
 
required
 
✅
 
No
 
self-approval
 
allowed
 
✅
 
Must
 
link
 
work
 
item
 
(Task/Bug)
 
✅
 
Pipeline
 
must
 
pass
 
before
 
merge
 
 
Benefits:
 
-
 
No
 
broken
 
code
 
can
 
be
 
merged
 
-
 
Every
 
change
 
is
 
reviewed
 
by
 
another
 
person
 
-
 
Full
 
traceability
 
to
 
work
 
items
 
-
 
Consistent
 
quality
 
standards
 
across
 
team
 
 
Q18.
 
What
 
is
 
a
 
PAT
 
token
 
and
 
what
 
did
 
you
 
use
 
it
 
for?
 
PAT
 
=
 
Personal
 
Access
 
Token
 
 
It
 
is
 
a
 
secure
 
alternative
 
to
 
password
 
for
 
Azure
 
DevOps
 
authentication.
 
 
I
 
used
 
PAT
 
for:
 
1.
 
Self-hosted
 
agent
 
registration
 
(config.sh
 
authentication)
 
2.
 
Git
 
authentication
 
when
 
pushing
 
code
 
(Azure
 
DevOps
 
blocks
 
password
 
login)
 
 
PAT
 
has
 
scopes
 
—
 
you
 
give
 
ONLY
 
the
 
permissions
 
needed:
 
-
 
Agent
 
Pools:
 
Read
 
&
 
Manage
 
(for
 
agent
 
setup)
 
-
 
Code:
 
Read
 
&
 
Write
 
(for
 
git
 
operations)
 
 
Key
 
principle:
 
Least
 
privilege
 
—
 
give
 
minimum
 
permissions
 
needed!
 
✅

## Section / Page 10

🐳
 
DOCKER
 
(Q19–Q25)
 
 
Q19.
 
What
 
is
 
Docker
 
and
 
what
 
problem
 
does
 
it
 
solve?
 
Docker
 
is
 
a
 
containerization
 
platform
 
that
 
packages
 
your
 
application,
 
dependencies,
 
and
 
runtime
 
into
 
a
 
container.
 
 
Container
 
runs
 
the
 
SAME
 
everywhere:
 
laptop,
 
staging,
 
production.
 
Solves
 
the
 
famous
 
"Works
 
on
 
my
 
machine"
 
problem!
 
✅
 
 
Key
 
components:
 
├──
 
Dockerfile
 
→
 
text
 
file
 
with
 
instructions
 
to
 
build
 
image
 
├──
 
Image
 
→
 
read-only
 
blueprint
 
(built
 
from
 
Dockerfile)
 
├──
 
Container
 
→
 
running
 
instance
 
of
 
an
 
image
 
└──
 
Registry
 
→
 
stores
 
images
 
(Docker
 
Hub,
 
ECR,
 
ACR)
 
 
Flow:
 
Dockerfile
 
→
 
docker
 
build
 
→
 
Image
 
→
 
docker
 
run
 
→
 
Container
 
 
Q20.
 
VM
 
vs
 
Container
 
—
 
what
 
is
 
the
 
difference?
 
VM:
 
├──
 
Full
 
OS
 
per
 
instance
 
(GBs
 
in
 
size)
 
├──
 
Minutes
 
to
 
start
 
├──
 
Heavy
 
overhead
 
└──
 
Full
 
hardware
 
isolation
 
 
Container:
 
├──
 
Shares
 
host
 
OS
 
kernel
 
(MBs
 
in
 
size)
 
├──
 
Seconds
 
to
 
start
 
├──
 
Near
 
native
 
performance
 
└──
 
Process-level
 
isolation
 
 
For
 
microservices
 
and
 
CI/CD
 
→
 
containers
 
are
 
preferred.
 
VMs
 
are
 
for
 
full
 
OS
 
isolation
 
requirements.
 
 
Q21.
 
What
 
is
 
a
 
Dockerfile
 
and
 
key
 
instructions?
 
Dockerfile
 
is
 
a
 
text
 
file
 
with
 
instructions
 
to
 
build
 
a
 
Docker
 
image.
 
 
FROM
 
→
 
base
 
image
 
(e.g.,
 
FROM
 
node:18-alpine)
 
WORKDIR
 
→
 
set
 
working
 
directory
 
(e.g.,
 
WORKDIR
 
/app)
 
COPY
 
→
 
copy
 
files
 
from
 
host
 
to
 
image
 
ADD
 
→
 
like
 
COPY
 
but
 
also
 
extracts
 
tar
 
and
 
downloads
 
URLs
 
RUN
 
→
 
execute
 
command
 
at
 
BUILD
 
time
 
(install
 
packages)
 
EXPOSE
 
→
 
document
 
port
 
(does
 
NOT
 
actually
 
publish)
 
ENV
 
→
 
set
 
environment
 
variables
 
ARG
 
→
 
build-time
 
variables
 
(not
 
in
 
final
 
image)
 
CMD
 
→
 
default
 
start
 
command
 
(CAN
 
be
 
overridden)
 
ENTRYPOINT
 
→
 
fixed
 
main
 
command
 
(cannot
 
easily
 
override)
 
USER
 
→
 
run
 
as
 
non-root
 
user
 
(security
 
best
 
practice)
 
 
RUN
 
=
 
build
 
time
 
|
 
CMD
 
=
 
runtime
 
default
 
|
 
ENTRYPOINT
 
=
 
runtime
 
fixed

## Section / Page 11

Q22.
 
What
 
is
 
a
 
multi-stage
 
build
 
and
 
why
 
do
 
we
 
use
 
it?
 
Multi-stage
 
build
 
uses
 
multiple
 
FROM
 
statements
 
in
 
one
 
Dockerfile.
 
Build
 
in
 
large
 
stage
 
→
 
copy
 
ONLY
 
final
 
artifact
 
to
 
small
 
runtime
 
image.
 
 
#
 
Stage
 
1
 
—
 
Build
 
(large,
 
has
 
all
 
build
 
tools)
 
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
 
RUN
 
mvn
 
clean
 
package
 
-DskipTests
 
 
#
 
Stage
 
2
 
—
 
Runtime
 
(small,
 
just
 
JRE)
 
FROM
 
eclipse-temurin:17-jre-alpine
 
WORKDIR
 
/app
 
COPY
 
--from=builder
 
/app/target/myapp.jar
 
.
 
USER
 
nobody
 
EXPOSE
 
8080
 
CMD
 
["java",
 
"-jar",
 
"myapp.jar"]
 
 
Result:
 
800MB
 
→
 
180MB
 
(80%
 
reduction!)
 
🔥
 
Also
 
more
 
secure
 
—
 
source
 
code
 
NOT
 
in
 
final
 
image.
 
 
Q23.
 
What
 
is
 
Docker
 
Compose?
 
Docker
 
Compose
 
runs
 
MULTIPLE
 
containers
 
together
 
with
 
one
 
YAML
 
file.
 
 
Commands:
 
docker-compose
 
up
 
-d
     
→
 
start
 
all
 
services
 
in
 
background
 
docker-compose
 
down
      
→
 
stop
 
and
 
remove
 
all
 
containers
 
docker-compose
 
logs
 
-f
   
→
 
follow
 
all
 
service
 
logs
 
docker-compose
 
ps
        
→
 
list
 
running
 
services
 
docker-compose
 
restart
 
backend
 
→
 
restart
 
specific
 
service
 
 
Use
 
case:
 
Run
 
frontend
 
+
 
backend
 
+
 
database
 
with
 
ONE
 
command!
 
 
Docker
 
Compose
 
vs
 
Kubernetes:
 
Compose
 
→
 
local
 
development,
 
simple,
 
no
 
auto-healing
 
Kubernetes
 
→
 
production,
 
auto-healing,
 
auto-scaling
 
 
Q24.
 
How
 
do
 
you
 
view
 
Docker
 
container
 
logs?
 
docker
 
logs
 
mycontainer
              
→
 
basic
 
logs
 
docker
 
logs
 
-f
 
mycontainer
           
→
 
follow
 
real
 
time
 
docker
 
logs
 
--tail
 
100
 
mycontainer
   
→
 
last
 
100
 
lines
 
docker
 
logs
 
-t
 
mycontainer
           
→
 
with
 
timestamps
 
docker
 
logs
 
--since
 
1h
 
mycontainer
   
→
 
last
 
1
 
hour
 
 
For
 
Docker
 
Compose:
 
docker-compose
 
logs
 
-f
               
→
 
all
 
services
 
docker-compose
 
logs
 
-f
 
backend
       
→
 
specific
 
service

## Section / Page 12

Limit
 
log
 
size
 
(prevent
 
disk
 
full):
 
docker
 
run
 
--log-opt
 
max-size=10m
 
--log-opt
 
max-file=3
 
myapp
 
 
Q25.
 
What
 
is
 
Alpine
 
and
 
why
 
do
 
we
 
use
 
alpine
 
images?
 
Alpine
 
is
 
a
 
minimal
 
Linux
 
distribution
 
with
 
only
 
~5MB
 
base
 
size.
 
 
node:18
         
→
 
900MB
 
❌
 
node:18-alpine
  
→
 
150MB
 
✅
 
 
Benefits:
 
✅
 
Much
 
smaller
 
image
 
size
 
✅
 
Faster
 
to
 
pull
 
from
 
registry
 
✅
 
Smaller
 
attack
 
surface
 
(fewer
 
packages
 
=
 
less
 
vulnerability)
 
 
Note:
 
Sometimes
 
Alpine
 
causes
 
compatibility
 
issues
 
with
 
some
 
Java
 
apps.
 
In
 
that
 
case
 
use
 
-slim
 
variants
 
instead.

## Section / Page 13

☸
 
KUBERNETES
 
(Q26–Q33)
 
 
Q26.
 
What
 
is
 
Kubernetes
 
and
 
why
 
do
 
we
 
need
 
it?
 
Kubernetes
 
is
 
an
 
open-source
 
container
 
orchestration
 
platform
 
that
 
automates
 
deployment,
 
scaling,
 
and
 
management
 
of
 
containerized
 
applications.
 
 
Docker
 
standalone
 
problems
 
→
 
Kubernetes
 
solutions:
 
❌
 
Container
 
crashes
 
→
 
stays
 
dead
 
|
 
✅
 
Auto-healing:
 
restarts
 
automatically
 
❌
 
Cannot
 
scale
 
on
 
demand
 
|
 
✅
 
HPA:
 
scales
 
based
 
on
 
CPU/memory
 
❌
 
No
 
traffic
 
distribution
 
|
 
✅
 
Load
 
balancing
 
across
 
pod
 
replicas
 
❌
 
Single
 
host
 
only
 
|
 
✅
 
Multi-node
 
cluster
 
across
 
many
 
machines
 
❌
 
No
 
rolling
 
updates
 
|
 
✅
 
Zero
 
downtime
 
deployments
 
 
Key
 
features:
 
Auto-healing
 
|
 
Auto-scaling
 
|
 
Load
 
balancing
 
|
 
Rolling
 
updates
 
|
 
Service
 
discovery
 
|
 
Storage
 
management
 
 
Q27.
 
What
 
is
 
a
 
Pod?
 
Pod
 
is
 
the
 
SMALLEST
 
deployable
 
unit
 
in
 
Kubernetes.
 
A
 
Pod
 
wraps
 
one
 
or
 
more
 
containers.
 
 
Containers
 
in
 
a
 
Pod
 
SHARE:
 
-
 
Same
 
IP
 
address
 
-
 
Same
 
storage
 
volumes
 
-
 
Same
 
network
 
namespace
 
 
Mostly
 
ONE
 
container
 
per
 
Pod
 
(best
 
practice).
 
Multi-container
 
Pod
 
used
 
for
 
sidecar
 
patterns
 
(logging
 
agents,
 
proxies).
 
 
Pods
 
are
 
managed
 
by
 
Deployments
 
or
 
StatefulSets
 
—
 
not
 
created
 
directly.
 
 
Q28.
 
Deployment
 
vs
 
StatefulSet
 
—
 
what
 
is
 
the
 
difference?
 
Deployment:
 
├──
 
For
 
STATELESS
 
applications
 
├──
 
Random
 
pod
 
names
 
(nginx-abc123,
 
nginx-xyz789)
 
├──
 
Pods
 
created
 
on
 
any
 
available
 
node
 
├──
 
No
 
stable
 
identity
 
needed
 
└──
 
Used
 
for:
 
Frontend,
 
Backend
 
APIs,
 
Microservices
 
 
StatefulSet:
 
├──
 
For
 
STATEFUL
 
applications
 
├──
 
Stable
 
pod
 
names
 
(postgres-0,
 
postgres-1,
 
postgres-2)
 
├──
 
Each
 
pod
 
gets
 
its
 
OWN
 
PVC
 
(data
 
survives
 
restarts)
 
├──
 
Ordered
 
deployment
 
and
 
deletion
 
└──
 
Used
 
for:
 
Databases,
 
Kafka,
 
Zookeeper
 
 
My
 
project:
 
Frontend
 
+
 
Backend
 
→
 
Deployment
 
|
 
PostgreSQL
 
→
 
StatefulSet
 
 
Q29.
 
What
 
are
 
the
 
3
 
Service
 
types
 
in
 
Kubernetes?

## Section / Page 14

1.
 
ClusterIP
 
(DEFAULT):
 
   
Internal
 
only
 
—
 
no
 
external
 
access.
 
   
Pod-to-Pod
 
communication
 
inside
 
cluster.
 
   
DNS:
 
service-name.namespace.svc.cluster.local
 
   
→
 
Used
 
for:
 
Backend,
 
Database
 
(my
 
project)
 
 
2.
 
NodePort:
 
   
External
 
via
 
NodeIP:30000-32767.
 
   
Dev/test
 
only
 
—
 
not
 
for
 
production.
 
 
3.
 
LoadBalancer:
 
   
External
 
via
 
cloud
 
Load
 
Balancer.
 
   
Creates
 
AWS
 
ELB
 
automatically.
 
   
Production
 
public
 
access.
 
   
→
 
Used
 
for:
 
Frontend
 
(my
 
project)
 
 
Q30.
 
How
 
does
 
Kubernetes
 
internal
 
DNS
 
work?
 
Every
 
Service
 
in
 
Kubernetes
 
gets
 
a
 
DNS
 
name
 
automatically.
 
 
Format:
 
<service-name>.<namespace>.svc.cluster.local
 
 
My
 
project:
 
Backend
 
DNS:
 
backend-service.default.svc.cluster.local:3000
 
Database
 
DNS:
 
postgres.default.svc.cluster.local:5432
 
 
Frontend
 
calls
 
backend
 
using
 
this
 
DNS.
 
Backend
 
calls
 
database
 
using
 
this
 
DNS.
 
 
No
 
hardcoded
 
IP
 
addresses
 
needed!
 
Even
 
if
 
pod
 
restarts
 
→
 
same
 
DNS
 
always
 
works
 
✅
 
 
Q31.
 
What
 
is
 
kOps
 
and
 
what
 
does
 
it
 
create?
 
kOps
 
=
 
Kubernetes
 
Operations
 
Tool
 
to
 
provision
 
and
 
manage
 
Kubernetes
 
clusters
 
on
 
AWS.
 
 
Steps:
 
1.
 
kops
 
create
 
cluster
 
→
 
defines
 
cluster
 
config
 
(does
 
NOT
 
create
 
yet)
 
2.
 
kops
 
update
 
cluster
 
--yes
 
→
 
actually
 
creates
 
AWS
 
resources
 
3.
 
kops
 
validate
 
cluster
 
→
 
verify
 
cluster
 
is
 
healthy
 
4.
 
kops
 
delete
 
cluster
 
→
 
delete
 
everything
 
 
kOps
 
automatically
 
creates:
 
├──
 
VPC
 
and
 
Subnets
 
├──
 
Security
 
Groups
 
├──
 
EC2
 
instances
 
(1
 
master
 
+
 
2
 
workers)
 
├──
 
IAM
 
Roles
 
for
 
master
 
and
 
workers
 
├──
 
ELB
 
for
 
Kubernetes
 
API
 
server
 
└──
 
Auto
 
Scaling
 
Groups
 
for
 
workers
 
 
Why
 
kOps
 
over
 
EKS?
 
Full
 
control
 
+
 
learn
 
K8s
 
internals.
 
EKS
 
abstracts
 
the
 
control
 
plane
 
—
 
less
 
learning.

## Section / Page 15

Q32.
 
What
 
is
 
auto-healing
 
in
 
Kubernetes?
 
Auto-healing
 
=
 
Kubernetes
 
automatically
 
restarts
 
failed
 
pods.
 
 
How
 
it
 
works:
 
1.
 
kubelet
 
on
 
worker
 
node
 
detects
 
pod
 
crash
 
2.
 
Reports
 
to
 
API
 
Server
 
→
 
Controller
 
Manager
 
3.
 
Controller
 
Manager:
 
ReplicaSet
 
has
 
fewer
 
pods
 
than
 
desired
 
4.
 
Schedules
 
new
 
pod
 
on
 
available
 
worker
 
node
 
5.
 
New
 
pod
 
starts
 
automatically
 
—
 
usually
 
in
 
10-30
 
seconds
 
 
No
 
manual
 
intervention
 
needed!
 
✅
 
 
If
 
pod
 
keeps
 
crashing:
 
→
 
Enters
 
CrashLoopBackOff
 
state
 
→
 
K8s
 
retries
 
with
 
exponential
 
backoff
 
(10s,
 
20s,
 
40s...
 
max
 
5min)
 
 
Q33.
 
What
 
are
 
Kubernetes
 
Master
 
Node
 
components?
 
API
 
Server:
 
Front
 
door
 
of
 
K8s.
 
All
 
kubectl
 
commands
 
go
 
here.
 
 
etcd:
 
Distributed
 
key-value
 
database.
 
      
Stores
 
ALL
 
cluster
 
state.
 
The
 
source
 
of
 
truth.
 
 
Scheduler:
 
Watches
 
for
 
unscheduled
 
pods.
 
           
Decides
 
WHICH
 
node
 
to
 
place
 
pod
 
on.
 
 
Controller
 
Manager:
 
Maintains
 
desired
 
state.
 
                    
If
 
3
 
pods
 
needed
 
→
 
ensures
 
3
 
always
 
running.
 
 
Worker
 
Node
 
components:
 
kubelet:
 
Node
 
agent.
 
Creates
 
and
 
manages
 
pods
 
on
 
that
 
node.
 
kube-proxy:
 
Manages
 
network
 
rules.
 
Handles
 
service
 
routing.
 
Container
 
Runtime:
 
Actually
 
runs
 
containers
 
(containerd).

## Section / Page 16

☁
 
AWS
 
&
 
AZURE
 
(Q34–Q40)
 
 
Q34.
 
What
 
is
 
VPC?
 
VPC
 
=
 
Virtual
 
Private
 
Cloud
 
Your
 
own
 
isolated
 
private
 
network
 
in
 
AWS.
 
 
You
 
control:
 
├──
 
Subnets
 
(public
 
and
 
private)
 
├──
 
Route
 
tables
 
├──
 
Internet
 
Gateway
 
├──
 
Security
 
Groups
 
and
 
NACLs
 
└──
 
All
 
traffic
 
flow
 
between
 
resources
 
 
In
 
my
 
project:
 
kOps
 
automatically
 
created
 
a
 
VPC
 
for
 
the
 
K8s
 
cluster.
 
 
Q35.
 
Public
 
Subnet
 
vs
 
Private
 
Subnet?
 
Public
 
Subnet:
 
├──
 
Has
 
Internet
 
Gateway
 
→
 
direct
 
internet
 
(inbound
 
+
 
outbound)
 
├──
 
Instances
 
can
 
have
 
public
 
IPs
 
└──
 
Used
 
for:
 
Load
 
balancers,
 
Bastion
 
hosts
 
 
Private
 
Subnet:
 
├──
 
NO
 
Internet
 
Gateway
 
├──
 
Internet
 
via
 
NAT
 
Gateway
 
(OUTBOUND
 
only
 
—
 
no
 
inbound!)
 
├──
 
No
 
public
 
IPs
 
└──
 
Used
 
for:
 
Databases,
 
App
 
servers,
 
K8s
 
nodes
 
 
Internet
 
CANNOT
 
initiate
 
connection
 
to
 
private
 
subnet
 
—
 
one
 
way
 
only!
 
🔒
 
 
Q36.
 
What
 
is
 
IAM?
 
IAM
 
=
 
Identity
 
and
 
Access
 
Management
 
Controls
 
WHO
 
can
 
access
 
WHAT
 
in
 
AWS.
 
 
4
 
Components:
 
├──
 
Users
 
→
 
permanent
 
identity
 
for
 
humans
 
(username
 
+
 
password
 
+
 
access
 
keys)
 
├──
 
Groups
 
→
 
collection
 
of
 
users
 
with
 
shared
 
permissions
 
├──
 
Roles
 
→
 
temporary
 
identity
 
for
 
AWS
 
services
 
(no
 
credentials!)
 
└──
 
Policies
 
→
 
JSON
 
documents
 
defining
 
permissions
 
 
Key
 
principle:
 
LEAST
 
PRIVILEGE
 
—
 
give
 
minimum
 
permissions
 
needed.
 
Never
 
use
 
wildcards
 
(*)
 
in
 
production
 
policies.
 
 
Best
 
practice:
 
Use
 
ROLES
 
for
 
services
 
(EC2,
 
Lambda)
 
—
 
never
 
store
 
access
 
keys!
 
 
Q37.
 
IAM
 
User
 
vs
 
IAM
 
Role?
 
IAM
 
User:
 
├──
 
Permanent
 
identity
 
├──
 
For
 
HUMANS

## Section / Page 17

├──
 
Username
 
+
 
password
 
+
 
access
 
keys
 
└──
 
Long-term
 
credentials
 
 
IAM
 
Role:
 
├──
 
Temporary
 
identity
 
├──
 
For
 
AWS
 
SERVICES
 
(EC2,
 
Lambda)
 
├──
 
No
 
username
 
or
 
password
 
└──
 
Temporary
 
tokens
 
(auto-rotate,
 
auto-expire)
 
 
Best
 
practice:
 
Use
 
roles
 
for
 
services!
 
Never
 
store
 
access
 
keys
 
on
 
EC2
 
—
 
security
 
risk
 
if
 
instance
 
is
 
compromised.
 
 
In
 
my
 
project:
 
kOps
 
created
 
IAM
 
roles
 
for
 
master
 
and
 
worker
 
nodes.
 
 
Q38.
 
What
 
is
 
S3?
 
S3
 
=
 
Simple
 
Storage
 
Service
 
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
 
 
├──
 
Global
 
(not
 
AZ
 
specific)
 
├──
 
Bucket
 
→
 
container
 
for
 
objects
 
├──
 
Object
 
→
 
actual
 
file
 
├──
 
Max
 
5TB
 
per
 
object
 
└──
 
Globally
 
unique
 
bucket
 
names
 
 
Storage
 
classes:
 
Standard
 
→
 
Standard-IA
 
→
 
Glacier
 
→
 
Glacier
 
Deep
 
Archive
 
(cheapest)
 
 
In
 
my
 
project:
 
kOps
 
state
 
store
 
→
 
s3://akhil-kops-state-store
 
 
Q39.
 
EBS
 
vs
 
EFS
 
—
 
what
 
is
 
the
 
difference?
 
EBS
 
(Elastic
 
Block
 
Store):
 
├──
 
Block
 
storage
 
(like
 
hard
 
drive
 
attached
 
to
 
EC2)
 
├──
 
AZ
 
specific
 
❌
 
(if
 
AZ
 
fails,
 
volume
 
inaccessible)
 
├──
 
One
 
EC2
 
at
 
a
 
time
 
├──
 
Fast
 
read/write
 
└──
 
Used
 
for:
 
databases,
 
OS
 
volumes
 
 
EFS
 
(Elastic
 
File
 
System):
 
├──
 
File
 
storage
 
(shared
 
network
 
drive)
 
├──
 
Multi
 
AZ
 
✅
 
├──
 
Multiple
 
EC2
 
simultaneously
 
├──
 
Slightly
 
slower
 
than
 
EBS
 
└──
 
Used
 
for:
 
shared
 
content
 
between
 
multiple
 
servers
 
 
My
 
project:
 
EBS
 
for
 
PostgreSQL.
 
Limitation:
 
AZ
 
specific.
 
Production
 
improvement:
 
Replace
 
with
 
EFS.
 
 
Q40.
 
AWS
 
vs
 
Azure
 
—
 
key
 
differences?
 
AWS
              
→
 
Azure
 
EC2
              
→
 
Azure
 
VM

## Section / Page 18

VPC
              
→
 
VNet
 
(Virtual
 
Network)
 
Security
 
Group
   
→
 
NSG
 
(Network
 
Security
 
Group)
 
S3
               
→
 
Azure
 
Blob
 
Storage
 
EBS
              
→
 
Azure
 
Managed
 
Disks
 
EFS
              
→
 
Azure
 
Files
 
RDS
              
→
 
Azure
 
SQL
 
Database
 
DynamoDB
         
→
 
CosmosDB
 
IAM
              
→
 
Azure
 
Active
 
Directory
 
CloudWatch
       
→
 
Azure
 
Monitor
 
Lambda
           
→
 
Azure
 
Functions
 
EKS
              
→
 
AKS
 
 
Azure
 
specific:
 
Resource
 
Groups
 
—
 
everything
 
must
 
belong
 
to
 
one
 
(no
 
AWS
 
equivalent).
 
 
My
 
experience:
 
AWS
 
→
 
Project
 
2
 
(K8s)
 
|
 
Azure
 
→
 
Project
 
1
 
(DevOps
 
+
 
Reverse
 
Proxy)

## Section / Page 19

🔥
 
SCENARIO
 
BASED
 
(Q41–Q45)
 
 
Q41.
 
Production
 
is
 
down
 
at
 
2AM
 
—
 
what
 
do
 
you
 
do
 
step
 
by
 
step?
 
STEP
 
1:
 
Stay
 
calm.
 
Inform
 
manager
 
you
 
are
 
investigating.
 
 
STEP
 
2:
 
Check
 
what
 
error
 
user
 
sees:
 
  
502
 
Bad
 
Gateway
 
→
 
Apache
 
cannot
 
reach
 
Tomcat
 
  
403
 
Forbidden
 
→
 
Permission
 
issue
 
  
404
 
Not
 
Found
 
→
 
Wrong
 
URL
 
or
 
not
 
deployed
 
  
Timeout
 
→
 
Network
 
issue
 
or
 
server
 
overload
 
 
STEP
 
3:
 
Check
 
Grafana
 
dashboard
 
(http://VM-IP:3000)
 
  
Any
 
ERROR
 
spikes?
 
When
 
did
 
errors
 
start?
 
 
STEP
 
4:
 
SSH
 
into
 
server
 
  
ssh
 
-i
 
key.pem
 
azureuser@VM-IP
 
 
STEP
 
5:
 
Check
 
all
 
service
 
statuses
 
  
sudo
 
systemctl
 
status
 
apache2
 
  
ps
 
aux
 
|
 
grep
 
tomcat
 
  
sudo
 
systemctl
 
status
 
postgresql
 
  
ss
 
-tulpn
 
|
 
grep
 
-E
 
"80|7789|8888"
 
 
STEP
 
6:
 
Check
 
logs
 
  
tail
 
-f
 
/var/log/apache2/error.log
 
  
tail
 
-f
 
/opt/tomcat1/logs/catalina.out
 
  
Look
 
for:
 
OutOfMemoryError,
 
Exception,
 
Connection
 
refused
 
 
STEP
 
7:
 
Check
 
system
 
resources
 
  
top
 
→
 
CPU
 
|
 
free
 
-h
 
→
 
RAM/Swap
 
|
 
df
 
-h
 
→
 
disk
 
space
 
 
STEP
 
8:
 
Fix
 
based
 
on
 
findings
 
  
Apache
 
down
 
→
 
sudo
 
systemctl
 
restart
 
apache2
 
  
Tomcat
 
down
 
→
 
/opt/tomcat1/bin/startup.sh
 
  
Disk
 
full
 
→
 
rm
 
old
 
log
 
files
 
  
Memory
 
→
 
restart
 
Tomcat
 
 
STEP
 
9:
 
Verify
 
→
 
curl
 
-I
 
http://localhost:80
 
 
STEP
 
10:
 
Document
 
→
 
what
 
happened,
 
how
 
fixed,
 
how
 
to
 
prevent.
 
 
Q42.
 
CI/CD
 
pipeline
 
is
 
not
 
triggering
 
—
 
how
 
do
 
you
 
debug?
 
STEP
 
1:
 
Check
 
which
 
branch
 
was
 
pushed
 
to
 
  
git
 
branch
 
|
 
git
 
log
 
--oneline
 
  
MOST
 
COMMON:
 
pushed
 
to
 
feature
 
branch
 
not
 
main!
 
  
Fix:
 
git
 
checkout
 
main
 
→
 
git
 
merge
 
feature
 
→
 
git
 
push
 
origin
 
main
 
 
STEP
 
2:
 
Check
 
trigger
 
in
 
YAML
 
  
trigger:
 
  
-
 
main
   
←
 
must
 
match
 
your
 
actual
 
branch
 
name

## Section / Page 20

STEP
 
3:
 
Check
 
agent
 
status
 
  
Azure
 
DevOps
 
→
 
Organization
 
Settings
 
→
 
Agent
 
Pools
 
→
 
Default
 
  
Is
 
myagent
 
ONLINE?
 
If
 
offline
 
→
 
cd
 
~/myagent
 
&&
 
./run.sh
 
 
STEP
 
4:
 
Check
 
YAML
 
file
 
  
Is
 
azure-pipelines.yml
 
committed
 
to
 
repo?
 
  
Is
 
it
 
in
 
the
 
ROOT
 
of
 
the
 
repository?
 
  
Any
 
indentation/syntax
 
errors?
 
 
STEP
 
5:
 
Try
 
manual
 
trigger
 
  
Azure
 
DevOps
 
→
 
Pipelines
 
→
 
Run
 
Pipeline
 
  
If
 
manual
 
works
 
→
 
trigger
 
config
 
issue
 
  
If
 
manual
 
fails
 
→
 
pipeline/agent
 
issue
 
 
I
 
faced
 
this
 
exact
 
issue!
 
Pushed
 
to
 
feature
 
branch
 
not
 
main.
 
Fix:
 
merged
 
feature
 
to
 
main
 
→
 
pipeline
 
triggered
 
immediately!
 
✅
 
 
Q43.
 
Pod
 
is
 
in
 
CrashLoopBackOff
 
—
 
what
 
do
 
you
 
do?
 
CrashLoopBackOff
 
means:
 
container
 
starts
 
→
 
crashes
 
→
 
K8s
 
restarts
 
→
 
crashes
 
again.
 
Kubernetes
 
retries
 
with
 
exponential
 
backoff
 
(10s,
 
20s,
 
40s...).
 
 
STEP
 
1:
 
Check
 
pod
 
status
 
  
kubectl
 
get
 
pods
 
→
 
identify
 
which
 
pod
 
is
 
crashing
 
 
STEP
 
2:
 
Check
 
crash
 
logs
 
(MOST
 
IMPORTANT)
 
  
kubectl
 
logs
 
<pod>
 
--previous
 
  
Look
 
for:
 
Exception,
 
Error,
 
OOMKilled
 
 
STEP
 
3:
 
Describe
 
pod
 
  
kubectl
 
describe
 
pod
 
<pod>
 
  
Check
 
Events
 
section
 
at
 
the
 
bottom
 
 
STEP
 
4:
 
Common
 
causes
 
and
 
fixes:
 
  
❌
 
Application
 
bug
 
→
 
fix
 
code,
 
rebuild
 
image,
 
redeploy
 
  
❌
 
Wrong
 
env
 
variables
 
→
 
check
 
ConfigMap
 
and
 
Secrets
 
  
❌
 
Wrong
 
image
 
name/tag
 
→
 
check
 
kubectl
 
describe
 
output
 
  
❌
 
OOMKilled
 
(out
 
of
 
memory)
 
→
 
increase
 
memory
 
limits
 
in
 
spec
 
  
❌
 
Missing
 
dependencies
 
→
 
fix
 
Dockerfile,
 
rebuild
 
 
STEP
 
5:
 
Fix
 
and
 
redeploy
 
  
kubectl
 
set
 
image
 
deployment/app
 
app=myrepo/app:fixed
 
  
kubectl
 
rollout
 
status
 
deployment/app
 
 
STEP
 
6:
 
If
 
still
 
broken
 
→
 
rollback
 
  
kubectl
 
rollout
 
undo
 
deployment/app
 
 
Q44.
 
Disk
 
is
 
full
 
at
 
2AM
 
—
 
what
 
steps
 
do
 
you
 
take?
 
STEP
 
1:
 
Confirm
 
disk
 
is
 
full
 
  
df
 
-h
 
→
 
see
 
which
 
partition
 
is
 
at
 
100%
 
 
STEP
 
2:
 
Find
 
which
 
folder
 
is
 
biggest

## Section / Page 21

du
 
-sh
 
/var/log/*
 
  
du
 
-sh
 
/opt/tomcat1/logs/*
 
  
du
 
-sh
 
/opt/tomcat2/logs/*
 
 
STEP
 
3:
 
Check
 
specific
 
log
 
files
 
  
ls
 
-lh
 
/opt/tomcat1/logs/
 
 
STEP
 
4:
 
Delete
 
old
 
log
 
files
 
  
rm
 
-rf
 
/opt/tomcat1/logs/catalina.out.*
 
  
rm
 
-rf
 
/var/log/apache2/*.gz
 
 
STEP
 
5:
 
Confirm
 
disk
 
freed
 
  
df
 
-h
 
→
 
verify
 
space
 
is
 
available
 
now
 
 
STEP
 
6:
 
Restart
 
services
 
if
 
needed
 
(they
 
may
 
have
 
stopped
 
due
 
to
 
disk
 
full)
 
 
STEP
 
7:
 
Next
 
day
 
→
 
configure
 
logrotate
 
for
 
automatic
 
log
 
cleanup.
 
  
Prevents
 
the
 
same
 
issue
 
from
 
happening
 
again!
 
 
Q45.
 
Server
 
CPU
 
is
 
at
 
95%
 
—
 
how
 
do
 
you
 
find
 
and
 
fix
 
it?
 
STEP
 
1:
 
Check
 
overall
 
CPU
 
  
top
 
→
 
see
 
overall
 
CPU
 
percentage
 
 
STEP
 
2:
 
Find
 
highest
 
CPU
 
consumer
 
  
ps
 
aux
 
--sort=-%cpu
 
|
 
head
 
-10
 
  
Shows
 
top
 
10
 
CPU
 
consuming
 
processes
 
 
STEP
 
3:
 
Identify
 
process
 
from
 
COMMAND
 
column
 
  
java
 
→
 
Tomcat
 
is
 
consuming
 
  
httpd
 
→
 
Apache
 
is
 
consuming
 
  
postgres
 
→
 
PostgreSQL
 
is
 
consuming
 
 
STEP
 
4:
 
Check
 
application
 
logs
 
  
tail
 
-f
 
/opt/tomcat1/logs/catalina.out
 
  
Look
 
for:
 
infinite
 
loops,
 
heavy
 
queries,
 
exception
 
storms
 
 
STEP
 
5:
 
Fix
 
based
 
on
 
cause
 
  
Memory
 
leak
 
→
 
restart
 
Tomcat
 
  
Heavy
 
DB
 
query
 
→
 
optimize
 
the
 
query
 
  
Too
 
much
 
traffic
 
→
 
scale
 
up
 
/
 
add
 
capacity
 
  
Infinite
 
loop
 
in
 
code
 
→
 
fix
 
the
 
bug
 
 
STEP
 
6:
 
Monitor
 
after
 
fix
 
  
top
 
→
 
verify
 
CPU
 
returns
 
to
 
normal

## Section / Page 22

📊
 
MONITORING
 
—
 
LGTM
 
(Q46–Q50)
 
 
Q46.
 
What
 
is
 
the
 
LGTM
 
stack?
 
LGTM
 
is
 
a
 
complete
 
observability
 
stack:
 
 
L
 
=
 
Loki
 
→
 
Log
 
storage
 
and
 
indexing
 
G
 
=
 
Grafana
 
→
 
Visualization
 
dashboard
 
and
 
alerting
 
T
 
=
 
Tempo
 
→
 
Distributed
 
tracing
 
(request
 
journey
 
across
 
services)
 
M
 
=
 
Mimir
 
→
 
Metrics
 
storage
 
(CPU%,
 
memory%,
 
request
 
count)
 
 
Observability
 
answers
 
3
 
questions:
 
1.
 
What
 
happened?
 
→
 
Logs
 
(Loki)
 
2.
 
How
 
is
 
system
 
performing?
 
→
 
Metrics
 
(Mimir)
 
3.
 
How
 
did
 
request
 
travel?
 
→
 
Traces
 
(Tempo)
 
 
In
 
my
 
project
 
I
 
implemented
 
LG:
 
Promtail
 
(collector)
 
+
 
Loki
 
(storage)
 
+
 
Grafana
 
(visualization)
 
 
Q47.
 
What
 
is
 
Promtail?
 
Promtail
 
is
 
a
 
log
 
COLLECTOR
 
agent.
 
Installed
 
on
 
the
 
same
 
VM
 
as
 
your
 
applications.
 
 
It:
 
├──
 
Reads
 
log
 
files
 
from
 
disk
 
continuously
 
├──
 
Adds
 
labels
 
(job=apache,
 
job=tomcat)
 
└──
 
Pushes
 
logs
 
to
 
Loki
 
 
Config
 
I
 
used:
 
scrape_configs:
 
-
 
job_name:
 
apache
 
  
__path__:
 
/var/log/apache2/*.log
 
-
 
job_name:
 
tomcat
 
  
__path__:
 
/opt/tomcat*/logs/*.out
 
 
Port:
 
9080
 
 
Q48.
 
What
 
is
 
Loki
 
and
 
how
 
is
 
it
 
different
 
from
 
Elasticsearch?
 
Loki
 
is
 
a
 
log
 
STORAGE
 
and
 
indexing
 
system.
 
Receives
 
logs
 
from
 
Promtail,
 
stores
 
with
 
timestamps
 
and
 
labels.
 
 
Port:
 
3100
 
 
Health
 
check:
 
curl
 
http://localhost:3100/ready
 
 
Loki
 
vs
 
Elasticsearch:
 
Loki
 
→
 
indexes
 
only
 
LABELS
 
(lightweight,
 
cheap)
 
Elasticsearch
 
→
 
indexes
 
FULL
 
log
 
content
 
(heavy,
 
expensive)
 
 
For
 
most
 
use
 
cases,
 
Loki
 
is
 
sufficient
 
and
 
much
 
simpler
 
to
 
run.

## Section / Page 23

Q49.
 
What
 
is
 
Grafana?
 
Grafana
 
is
 
a
 
visualization
 
and
 
dashboarding
 
tool.
 
Queries
 
Loki
 
for
 
logs,
 
displays
 
in
 
real-time
 
dashboards,
 
creates
 
alerts.
 
 
Port:
 
3000
 
|
 
Default
 
login:
 
admin/admin
 
 
How
 
I
 
set
 
it
 
up:
 
1.
 
Connections
 
→
 
Data
 
Sources
 
→
 
Loki
 
2.
 
URL:
 
http://localhost:3100
 
3.
 
Save
 
&
 
Test
 
4.
 
Explore
 
→
 
Select
 
Loki
 
→
 
Label
 
Browser
 
→
 
job
 
→
 
apache
 
or
 
tomcat
 
5.
 
See
 
real-time
 
logs
 
in
 
dashboard
 
✅
 
 
After
 
VM
 
reboot
 
—
 
restart
 
services:
 
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
 
 
Q50.
 
Why
 
LGTM
 
over
 
CloudWatch?
 
CloudWatch:
 
❌
 
AWS
 
only
 
—
 
cannot
 
monitor
 
Azure
 
services
 
❌
 
Paid
 
service
 
(costs
 
money)
 
❌
 
Limited
 
to
 
AWS
 
resources
 
only
 
 
LGTM
 
(Loki
 
+
 
Grafana):
 
✅
 
Free
 
and
 
open
 
source
 
✅
 
Works
 
across
 
AWS
 
AND
 
Azure
 
✅
 
Self-hosted
 
—
 
full
 
control
 
✅
 
Lightweight
 
and
 
easy
 
to
 
run
 
 
My
 
project
 
used
 
BOTH
 
AWS
 
(K8s)
 
and
 
Azure
 
(VM).
 
CloudWatch
 
would
 
only
 
cover
 
the
 
AWS
 
side.
 
LGTM
 
gives
 
ONE
 
unified
 
dashboard
 
for
 
both
 
clouds.
 
 
That
 
is
 
why
 
LGTM
 
was
 
the
 
right
 
choice
 
for
 
my
 
setup.

## Section / Page 24

💼
 
HR
 
QUESTIONS
 
(Q51–Q55)
 
 
Q51.
 
Why
 
Solytics
 
Partners?
 
I
 
am
 
excited
 
about
 
Solytics
 
Partners
 
for
 
three
 
specific
 
reasons:
 
 
FIRST:
 
You
 
work
 
with
 
cutting-edge
 
technologies
 
like
 
AI,
 
ML,
 
and
 
Generative
 
AI.
 
DevOps
 
for
 
AI/ML
 
workloads
 
is
 
the
 
future
 
and
 
I
 
want
 
to
 
be
 
part
 
of
 
that
 
journey.
 
 
SECOND:
 
This
 
role
 
directly
 
matches
 
my
 
hands-on
 
experience
 
with
 
CI/CD
 
pipelines,
 
Docker,
 
Kubernetes,
 
AWS
 
and
 
Azure
 
—
 
all
 
built
 
through
 
real
 
projects.
 
 
THIRD:
 
Solytics
 
is
 
a
 
recognized
 
global
 
analytics
 
firm
 
with
 
multiple
 
industry
 
awards.
 
Working
 
with
 
experienced
 
engineers
 
here
 
will
 
accelerate
 
my
 
growth
 
significantly.
 
 
I
 
am
 
confident
 
I
 
can
 
contribute
 
to
 
your
 
DevOps
 
infrastructure
 
from
 
day
 
one.
 
 
Q52.
 
Where
 
do
 
you
 
see
 
yourself
 
in
 
2
 
years?
 
In
 
2
 
years
 
I
 
see
 
myself
 
as
 
a
 
confident
 
DevOps
 
Engineer
 
who
 
can:
 
 
├──
 
Design
 
and
 
build
 
complete
 
cloud
 
infrastructure
 
from
 
scratch
 
├──
 
Lead
 
CI/CD
 
pipeline
 
implementations
 
for
 
teams
 
├──
 
Handle
 
production
 
incidents
 
independently
 
└──
 
Work
 
with
 
AI/ML
 
deployment
 
pipelines
 
(MLOps)
 
 
I
 
want
 
to
 
deepen
 
my
 
expertise
 
in:
 
├──
 
Kubernetes
 
advanced
 
topics
 
(RBAC,
 
Ingress,
 
HPA)
 
├──
 
Terraform
 
for
 
Infrastructure
 
as
 
Code
 
├──
 
Security
 
and
 
compliance
 
in
 
cloud
 
└──
 
MLOps
 
for
 
AI/ML
 
model
 
deployments
 
 
Solytics
 
is
 
the
 
perfect
 
place
 
because
 
of
 
your
 
focus
 
on
 
AI
 
and
 
analytics.
 
 
Q53.
 
What
 
are
 
your
 
strengths?
 
My
 
top
 
3
 
strengths:
 
 
1.
 
HANDS-ON
 
BUILDER:
 
   
I
 
don't
 
just
 
study
 
theory
 
—
 
I
 
build
 
real
 
projects.
 
   
3
 
production-grade
 
projects
 
prove
 
this.
 
 
2.
 
PROBLEM
 
SOLVER:
 
   
When
 
I
 
faced
 
issues
 
(permission
 
errors,
 
port
 
conflicts,
 
pipeline
 
failures)
 
   
I
 
debugged
 
and
 
fixed
 
them
 
systematically.
 
I
 
never
 
give
 
up.
 
 
3.
 
QUICK
 
LEARNER:
 
   
I
 
learned
 
Azure
 
DevOps,
 
Kubernetes,
 
LGTM
 
stack
 
from
 
scratch
 
   
and
 
built
 
complete
 
working
 
projects.
 
   
I
 
pick
 
up
 
new
 
technologies
 
fast
 
and
 
am
 
always
 
curious.
 
 
Q54.
 
What
 
are
 
your
 
weaknesses?

## Section / Page 25

My
 
main
 
weakness:
 
I
 
sometimes
 
spend
 
too
 
much
 
time
 
solving
 
problems
 
on
 
my
 
own
 
before
 
asking
 
for
 
help.
 
 
I
 
am
 
actively
 
working
 
on
 
this
 
by:
 
├──
 
Setting
 
a
 
30-minute
 
time
 
limit
 
before
 
seeking
 
help
 
├──
 
Consulting
 
documentation
 
and
 
team
 
proactively
 
└──
 
Collaborating
 
more
 
openly
 
with
 
peers
 
 
Another
 
area
 
I
 
want
 
to
 
improve:
 
I
 
have
 
basic
 
knowledge
 
of
 
Terraform
 
and
 
want
 
hands-on
 
production
 
experience.
 
I
 
see
 
Solytics
 
as
 
the
 
perfect
 
place
 
to
 
develop
 
this
 
skill.
 
 
Q55.
 
Do
 
you
 
have
 
any
 
questions
 
for
 
us?
 
1.
 
What
 
does
 
the
 
DevOps
 
infrastructure
 
currently
 
look
 
like
 
at
 
Solytics?
 
   
What
 
tools
 
and
 
cloud
 
platforms
 
do
 
you
 
primarily
 
use?
 
 
2.
 
What
 
would
 
my
 
first
 
30
 
days
 
look
 
like
 
in
 
this
 
role?
 
   
What
 
projects
 
would
 
I
 
be
 
contributing
 
to?
 
 
3.
 
How
 
does
 
the
 
DevOps
 
team
 
collaborate
 
with
 
AI/ML
 
and
 
development
 
teams?
 
 
4.
 
What
 
does
 
the
 
learning
 
and
 
growth
 
path
 
look
 
like
 
for
 
DevOps
 
engineers
 
here?
 
 
5.
 
What
 
are
 
the
 
biggest
 
DevOps
 
challenges
 
the
 
team
 
is
 
currently
 
facing?
 
   
I
 
would
 
love
 
to
 
understand
 
where
 
I
 
can
 
contribute
 
most.

## Section / Page 26

🔥
 
YOU
 
ARE
 
READY,
 
AKHIL!
 
🔥
 
You
 
have
 
3
 
REAL
 
projects.
 
Most
 
freshers
 
have
 
ZERO.
 
Walk
 
in
 
confident.
 
You
 
earned
 
this.
 
💪
 
 
 
Connect
 
every
 
answer
 
to
 
your
 
REAL
 
projects
 
Mention
 
limitations
 
shows
 
engineering
 
maturity
 
Ask
 
smart
 
questions
 
at
 
the
 
end
 
of
 
interview

