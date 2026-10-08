# 📖 aws handbook 
> *Converted from `aws handbook .pdf` for high-readability on GitHub.*

---
## Page 1

What
 
is
 
AWS?
 
Think
 
of
 
AWS
 
as
 
a
 
giant
 
toolbox
 
of
 
IT
 
services
 
on
 
the
 
internet
.
 
 
Instead
 
of
 
buying
 
expensive
 
computers,
 
storage,
 
or
 
networking
 
equipment,
 
you
 
can
 
rent
 
them
 
from
 
AWS
 
whenever
 
you
 
need
 
and
 
pay
 
only
 
for
 
what
 
you
 
use.
 
AWS
 
is
 
a
 
cloud
 
computing
 
platform
 
that
 
provides
 
on-demand
 
Infrastructure-as-a-Service
 
(IaaS)
,
 
Platform-as-a-Service
 
(PaaS)
,
 
and
 
Software-as-a-Service
 
(SaaS)
.
 
 
It
 
operates
 
from
 
global
 
data
 
centers
 
(Regions
 
&
 
Availability
 
Zones)
 
and
 
offers
 
services
 
across
 
compute,
 
storage,
 
networking,
 
databases,
 
AI/ML,
 
analytics,
 
security,
 
DevOps,
 
and
 
more
.
 
Example:
 
●
 
Instead
 
of
 
buying
 
a
 
generator,
 
you
 
get
 
electricity
 
from
 
the
 
power
 
grid.
 
 
●
 
Similarly,
 
instead
 
of
 
owning
 
servers,
 
you
 
use
 
AWS’s
 
servers.
 
 
AWS
 
Global
 
Infrastructure
 
AWS
 
has
 
data
 
centers
 
spread
 
across
 
the
 
world.
 
●
 
Regions
:
 
~35+
 
(example:
 
ap-south-1
 
=
 
Mumbai).
 
●
 
Availability
 
Zones
 
(AZs)
:
 
Each
 
region
 
has
 
2–6
 
AZs
 
for
 
redundancy.
 
●
 
Edge
 
Locations
:
 
Used
 
by
 
CloudFront
 
(CDN)
 
to
 
deliver
 
content
 
closer
 
to
 
users.
 
●
 
Local
 
Zones
 
&
 
Outposts
:
 
Extend
 
AWS
 
services
 
closer
 
to
 
customers.
 
 
AWS
 
Core
 
Services
 
1.
 
Compute
 
Services
 
Think
 
of
 
Compute
 
services
 
as
 
brains/machines
 
that
 
run
 
applications.
 
Instead
 
of
 
buying
 
a
 
physical
 
computer,
 
you
 
“rent”
 
it
 
on-demand
 
from
 
AWS.
 
●
 
Amazon
 
EC2
 
(Elastic
 
Compute
 
Cloud):
 
 
○
 
Virtual
 
servers
 
(instances)
 
with
 
customizable
 
CPU,
 
RAM,
 
storage,
 
and
 
networking.

## Page 2

○
 
Types:
 
General
 
Purpose,
 
Compute
 
Optimized,
 
Memory
 
Optimized,
 
Storage
 
Optimized,
 
Accelerated
 
Computing.
 
 
○
 
Features:
 
Auto
 
Scaling,
 
Placement
 
Groups,
 
Spot
 
Instances,
 
Elastic
 
IPs.
 
Amazon
 
EC2
 
(Elastic
 
Compute
 
Cloud)
 
Think
 
of
 
Amazon
 
EC2
 
like
 
renting
 
a
 
computer
 
in
 
the
 
cloud.
 
Instead
 
of
 
buying
 
a
 
physical
 
computer
 
(server)
 
and
 
keeping
 
it
 
in
 
your
 
office,
 
you
 
can
 
rent
 
a
 
virtual
 
computer
 
from
 
AWS
 
whenever
 
you
 
need
 
it
.
 
Amazon
 
EC2
 
is
 
a
 
scalable
 
Infrastructure-as-a-Service
 
(IaaS)
 
offering
 
that
 
provides
 
resizable
 
virtual
 
machines
 
(instances)
 
in
 
the
 
AWS
 
cloud.
 
It
 
allows
 
customers
 
to
 
provision
 
compute
 
resources
 
with
 
control
 
over:
 
●
 
Operating
 
system
 
(Linux,
 
Windows,
 
etc.)
 
 
●
 
Instance
 
type
 
(CPU,
 
memory,
 
GPU,
 
storage)
 
 
●
 
Networking
 
(VPC,
 
security
 
groups,
 
elastic
 
IPs)
 
 
●
 
Storage
 
(EBS
 
volumes,
 
instance
 
store,
 
EFS,
 
FSx)
 
 
●
 
You
 
can
 
choose
 
how
 
powerful
 
the
 
computer
 
should
 
be
 
(CPU,
 
memory,
 
storage,
 
operating
 
system).
 
 
●
 
You
 
only
 
pay
 
for
 
how
 
long
 
you
 
use
 
it
 
—
 
like
 
paying
 
electricity
 
bills
 
based
 
on
 
usage.
 
 
●
 
If
 
you
 
need
 
10
 
computers
 
today
 
and
 
just
 
2
 
tomorrow
,
 
you
 
can
 
easily
 
scale
 
up
 
or
 
down
 
without
 
worrying
 
about
 
hardware.
 
 
●
 
Businesses
 
use
 
EC2
 
to
 
run
 
websites,
 
apps,
 
databases,
 
or
 
even
 
machine
 
learning
 
workloads.
 
 
👉
 
In
 
short:
 
EC2
 
=
 
Virtual
 
Computer
 
on
 
the
 
Internet
 
provided
 
by
 
AWS.
 
Core
 
Components
 
of
 
Amazon
 
EC2

## Page 3

Think
 
of
 
EC2
 
as
 
renting
 
virtual
 
computers
 
(servers)
 
in
 
the
 
cloud
.
 
To
 
use
 
these
 
computers,
 
you
 
need
 
certain
 
parts,
 
just
 
like
 
when
 
setting
 
up
 
a
 
physical
 
computer
 
in
 
real
 
life.
 
The
 
core
 
components
 
of
 
EC2
 
are:
 
Amazon
 
Machine
 
Image
 
(AMI)
 
Think
 
of
 
an
 
AMI
 
as
 
the
 
blueprint
 
or
 
pre-installed
 
operating
 
system
 
+
 
software
 
for
 
your
 
virtual
 
server.
 
It
 
decides
 
what
 
your
 
server
 
looks
 
like
 
when
 
it
 
starts.
 
 
○
 
AMI
 
=
 
Template
 
for
 
an
 
instance.
 
 
○
 
Contains:
 
 
■
 
OS
 
(Linux,
 
Windows,
 
etc.)
 
 
■
 
Application
 
server
 
(Apache,
 
Nginx,
 
IIS,
 
etc.)
 
 
■
 
Applications
 
(databases,
 
custom
 
apps,
 
etc.)
 
 
○
 
You
 
can
 
use
 
AWS
 
pre-built
 
AMIs
 
(e.g.,
 
Amazon
 
Linux
 
2,
 
Ubuntu,
 
Windows
 
Server)
 
or
 
create
 
custom
 
AMIs
 
with
 
your
 
own
 
configurations.
 
Instance
 
Types
 
 
Like
 
buying
 
a
 
laptop
 
–
 
you
 
pick
 
one
 
based
 
on
 
how
 
much
 
CPU
 
power,
 
RAM,
 
and
 
storage
 
you
 
need.
 
 
○
 
Defines
 
hardware
 
configuration
 
of
 
an
 
EC2
 
instance.
 
 
○
 
Categories:
 
 
■
 
General
 
Purpose
 
–
 
Balanced
 
CPU/memory
 
(e.g.,
 
t3,
 
m5).
 
 
■
 
Compute
 
Optimized
 
–
 
High-performance
 
CPU
 
(e.g.,
 
c5,
 
c6g).
 
 
■
 
Memory
 
Optimized
 
–
 
Large
 
RAM
 
for
 
big
 
data,
 
caching
 
(e.g.,
 
r5,
 
x1e).
 
 
■
 
Storage
 
Optimized
 
–
 
High
 
IOPS
 
and
 
throughput
 
(e.g.,
 
i3,
 
d2).

## Page 4

■
 
Accelerated
 
Computing
 
–
 
GPUs
 
or
 
FPGAs
 
(e.g.,
 
p4,
 
g5,
 
f1).
 
 
○
 
Each
 
instance
 
type
 
family
 
comes
 
in
 
sizes
 
(small
 
→
 
large
 
→
 
xlarge).
 
 
Instance
 
Storage
 
Think
 
of
 
it
 
as
 
the
 
hard
 
drive
 
for
 
your
 
server.
 
Some
 
drives
 
are
 
temporary
 
(deleted
 
when
 
server
 
stops),
 
while
 
others
 
are
 
permanent.
 
 
○
 
Amazon
 
EBS
 
(Elastic
 
Block
 
Store):
 
 
Imagine
 
you
 
buy
 
a
 
computer
 
💻
.
 
You
 
need
 
a
 
hard
 
drive
 
(storage)
 
to
 
save
 
your
 
files,
 
apps,
 
and
 
system
 
data.
 
Without
 
storage,
 
your
 
computer
 
can’t
 
really
 
function.
 
In
 
AWS:
 
●
 
EC2
 
=
 
Computer
 
(CPU
 
+
 
Memory)
 
 
●
 
EBS
 
=
 
Hard
 
Drive
 
(Storage)
 
 
EBS
 
provides
 
durable,
 
high-performance,
 
resizable
 
storage
 
that
 
attaches
 
to
 
your
 
EC2
 
instances.
 
Unlike
 
the
 
temporary
 
storage
 
that
 
vanishes
 
when
 
you
 
shut
 
down
 
a
 
computer,
 
EBS
 
persists
 
data
 
even
 
after
 
you
 
stop
 
or
 
terminate
 
EC2
 
instances
 
(like
 
an
 
external
 
hard
 
drive).
 
Amazon
 
EBS
 
(Elastic
 
Block
 
Store)
 
is
 
a
 
block
 
storage
 
service
 
designed
 
for
 
use
 
with
 
Amazon
 
EC2.
 
It
 
provides
 
low-latency,
 
persistent
 
storage
 
volumes
 
that
 
can
 
be:
 
●
 
Attached
 
to
 
EC2
 
instances
 
 
●
 
Detached
 
and
 
re-attached
 
to
 
other
 
instances
 
 
●
 
Used
 
as
 
boot
 
volumes
 
or
 
data
 
volumes
 
You
 
can
 
think
 
of
 
EBS
 
like:
 
●
 
C:
 
Drive
 
/
 
D:
 
Drive
 
on
 
Windows
 
 
●
 
/dev/sda1,
 
/dev/xvdf
 
on
 
Linux

## Page 5

👉
 
It
 
gives
 
you
 
block-level
 
storage
,
 
meaning
 
data
 
is
 
stored
 
in
 
chunks
 
(blocks),
 
similar
 
to
 
how
 
physical
 
SSDs/HDDs
 
store
 
data.
 
This
 
is
 
different
 
from
 
Amazon
 
S3,
 
which
 
stores
 
data
 
as
 
objects
 
(files)
.
 
✅
 
Core
 
Features
 
of
 
EBS:
 
1.
 
Persistence
:
 
Data
 
remains
 
available
 
even
 
if
 
the
 
EC2
 
instance
 
is
 
stopped/terminated
 
(unless
 
explicitly
 
deleted).
 
 
2.
 
Block-Level
 
Storage
:
 
Functions
 
like
 
raw
 
unformatted
 
disks.
 
You
 
can
 
partition,
 
format,
 
and
 
mount
 
it
 
like
 
local
 
storage.
 
 
3.
 
High
 
Durability
:
 
Each
 
EBS
 
volume
 
is
 
automatically
 
replicated
 
within
 
its
 
Availability
 
Zone
 
(AZ)
 
to
 
protect
 
against
 
hardware
 
failures.
 
 
4.
 
Performance
 
Options
:
 
Multiple
 
volume
 
types
 
optimized
 
for
 
IOPS
 
(Input/Output
 
per
 
second)
 
or
 
Throughput
.
 
 
5.
 
Scalability
:
 
Volumes
 
can
 
be
 
resized
 
without
 
downtime.
 
 
6.
 
Backups
 
&
 
Snapshots
:
 
Integrated
 
with
 
Amazon
 
S3
 
to
 
create
 
point-in-time
 
snapshots.
 
 
 
EBS
 
Volume
 
Types
 
(Storage
 
Classes)
 
EBS
 
offers
 
multiple
 
volume
 
types
 
to
 
match
 
performance
 
vs
 
cost
 
needs
:
 
Volume
 
Type
 
Storage
 
Medium
 
Use
 
Case
 
Performance
 
gp3
 
(General
 
Purpose
 
SSD)
 
SSD
 
General
 
workloads,
 
system
 
boot
 
volumes
 
Balanced
 
price/performance
 
gp2
 
(General
 
Purpose
 
SSD)
 
SSD
 
(older)
 
Legacy
 
general
 
workloads
 
Performance
 
scales
 
with
 
size

## Page 6

io2
 
/
 
io1
 
(Provisioned
 
IOPS
 
SSD)
 
SSD
 
High-performance
 
apps,
 
databases
 
(Oracle,
 
SQL,
 
SAP)
 
Consistent
 
IOPS,
 
very
 
low
 
latency
 
st1
 
(Throughput
 
Optimized
 
HDD)
 
Magnetic
 
HDD
 
Big
 
data,
 
data
 
warehouses,
 
log
 
processing
 
High
 
throughput,
 
low
 
cost
 
sc1
 
(Cold
 
HDD)
 
Magnetic
 
HDD
 
Infrequent
 
access,
 
archival
 
storage
 
Cheapest,
 
lowest
 
performance
 
 
○
 
Instance
 
Store:
 
What
 
is
 
Instance
 
Store?
 
Think
 
of
 
Instance
 
Store
 
as
 
a
 
temporary
 
hard
 
drive
 
that
 
comes
 
built-in
 
with
 
the
 
physical
 
server
 
hosting
 
your
 
EC2
 
instance.
 
●
 
An
 
ephemeral
 
block-level
 
storage
 
physically
 
attached
 
to
 
the
 
host
 
machine
 
where
 
your
 
EC2
 
instance
 
runs.
 
 
●
 
Lifecycle:
 
Tied
 
to
 
the
 
lifetime
 
of
 
the
 
instance
.
 
Data
 
is
 
lost
 
when:
 
 
○
 
The
 
instance
 
is
 
stopped.
 
 
○
 
The
 
instance
 
is
 
terminated.
 
 
○
 
The
 
hardware
 
hosting
 
the
 
instance
 
fails.
 
 
●
 
Persistence:
 
Data
 
persists
 
only
 
during
 
reboots
 
of
 
the
 
same
 
instance
 
(but
 
not
 
stop/start).
 
 
 
●
 
It’s
 
fast
 
(since
 
it’s
 
directly
 
attached
 
to
 
the
 
physical
 
hardware).

## Page 7

●
 
But
 
it’s
 
temporary
 
–
 
meaning
 
if
 
you
 
stop,
 
terminate,
 
or
 
your
 
instance
 
crashes,
 
all
 
the
 
data
 
in
 
Instance
 
Store
 
is
 
gone.
 
 
●
 
Best
 
use
 
case:
 
caching,
 
temporary
 
storage,
 
or
 
buffers
 
where
 
speed
 
matters
 
but
 
you
 
don’t
 
need
 
permanent
 
storage.
 
 
👉
 
Example:
 
Imagine
 
you’re
 
cooking
 
in
 
a
 
rented
 
kitchen.
 
The
 
kitchen
 
counter
 
(Instance
 
Store)
 
is
 
very
 
close
 
and
 
fast
 
to
 
use,
 
but
 
when
 
you
 
leave,
 
you
 
must
 
clean
 
it
 
up
 
–
 
nothing
 
stays.
 
If
 
you
 
want
 
to
 
save
 
your
 
recipe
 
for
 
later,
 
you’d
 
write
 
it
 
in
 
a
 
notebook
 
(Amazon
 
EBS).
 
Characteristics
 
of
 
Instance
 
Store
 
●
 
High
 
Performance:
 
Very
 
low
 
latency
 
since
 
it’s
 
on
 
the
 
same
 
physical
 
machine.
 
 
●
 
Temporary:
 
Cannot
 
be
 
used
 
for
 
persistent
 
storage.
 
 
●
 
Cost:
 
Free
 
with
 
the
 
instance
 
–
 
included
 
in
 
the
 
price.
 
 
●
 
Size
 
&
 
Type:
 
Depends
 
on
 
the
 
instance
 
type
 
(e.g.,
 
some
 
have
 
SSD-based
 
instance
 
stores
 
for
 
high
 
IOPS
 
workloads).
 
 
●
 
Access:
 
Appears
 
as
 
a
 
block
 
device
 
(like
 
/dev/sd*
 
or
 
/dev/nvme*
).
 
 
Use
 
Cases
 
of
 
Instance
 
Store
 
●
 
High-speed
 
temporary
 
data:
 
 
○
 
Caching
 
layers
 
(e.g.,
 
web
 
server
 
cache).
 
 
○
 
Temporary
 
storage
 
for
 
batch
 
processing.
 
 
●
 
Buffer
 
or
 
scratch
 
space:
 
 
○
 
Data
 
that
 
can
 
be
 
recomputed
 
or
 
regenerated.
 
 
○
 
Temporary
 
storage
 
for
 
logs
 
before
 
pushing
 
to
 
S3.
 
 
●
 
Big
 
data
 
/
 
analytics:
 
 
○
 
Store
 
intermediate
 
results
 
of
 
Hadoop/Spark
 
workloads.

## Page 8

Difference:
 
Instance
 
Store
 
vs
 
EBS
 
Feature
 
Instance
 
Store
 
Amazon
 
EBS
 
Storage
 
Type
 
Local
 
(attached
 
to
 
host)
 
Network-attached
 
block
 
storage
 
Persistence
 
Lost
 
on
 
stop/terminate
 
Persists
 
independently
 
Performance
 
Very
 
high
 
(low
 
latency)
 
High
 
but
 
slightly
 
slower
 
Cost
 
Included
 
in
 
instance
 
Paid
 
separately
 
(per
 
GB)
 
Use
 
Case
 
Temporary
 
/
 
cache
 
/
 
buffer
 
Long-term
 
persistent
 
storage
 
Durability
 
Not
 
durable
 
Highly
 
durable
 
(replicated
 
across
 
AZs)
 
 
○
 
EFS
 
(Elastic
 
File
 
System):
 
 
■
 
Shared
 
file
 
storage
 
across
 
multiple
 
EC2s.
 
 
○
 
S3:
 
 
■
 
Object
 
storage,
 
often
 
used
 
for
 
backups
 
&
 
data
 
lakes.
 
 
 
Networking
 
(VPC,
 
Security
 
Groups,
 
ENIs)

## Page 9

1)Networking
 
fundamentals
 
(quick
 
but
 
precise)
 
These
 
are
 
the
 
concepts
 
you
 
must
 
own
 
before
 
designing
 
anything.
 
IP
 
&
 
subnetting
 
●
 
IPv4
 
addresses
 
are
 
32
 
bits.
 
A
 
prefix
 
/N
 
leaves
 
32−N
 
host
 
bits.
 
 
Example:
 
/24
 
→
 
32−24
 
=
 
8
 
host
 
bits
 
→
 
2^8
 
=
 
256
 
addresses.
 
Usable
 
hosts
 
usually
 
=
 
256
 
−
 
2
 
=
 
254
 
(network
 
+
 
broadcast).
 
 
(Calculation:
 
2^(32-24)
 
=
 
2^8
 
=
 
256
 
→
 
256
 
−
 
2
 
=
 
254
.)
 
 
MAC
 
/
 
ARP
 
●
 
Ethernet
 
uses
 
MAC
 
addresses;
 
ARP
 
maps
 
IPv4
 
→
 
MAC
 
inside
 
a
 
broadcast
 
domain
 
(subnet).

## Page 10

Routing
 
●
 
Routers
 
forward
 
packets
 
between
 
subnets/IP
 
ranges
 
using
 
route
 
tables.
 
Default
 
route
 
(
0.0.0.0/0
)
 
sends
 
traffic
 
to
 
the
 
internet
 
gateway
 
or
 
to
 
a
 
NAT.
 
 
TCP
 
vs
 
UDP
 
●
 
TCP:
 
reliable,
 
ordered,
 
congestion
 
control
 
(3-way
 
handshake).
 
 
●
 
UDP:
 
connectionless,
 
low
 
overhead
 
(good
 
for
 
DNS,
 
RTP,
 
telemetry).
 
 
Ports
 
&
 
Services
 
●
 
Ports
 
(0–65535)
 
identify
 
services.
 
Open
 
only
 
the
 
ports
 
your
 
app
 
needs.
 
 
NAT
 
&
 
PAT
 
●
 
NAT
 
translates
 
private
 
→
 
public
 
IPs
 
for
 
egress.
 
PAT
 
(port
 
address
 
translation)
 
lets
 
many
 
private
 
hosts
 
share
 
one
 
public
 
IP.
 
 
MTU
 
&
 
fragmentation
 
●
 
Maximum
 
Transmission
 
Unit
 
(e.g.,
 
1500
 
bytes)
 
—
 
oversized
 
packets
 
are
 
fragmented
 
or
 
dropped.
 
Keep
 
MTU
 
consistent
 
end-to-end
 
where
 
possible.
 
 
VPC
 
(Virtual
 
Private
 
Cloud)
 
1.
 
What
 
is
 
a
 
VPC?
 
●
 
Imagine
 
you
 
are
 
building
 
a
 
new
 
house:
 
●
 
Amazon
 
VPC
 
(Virtual
 
Private
 
Cloud)
 
is
 
a
 
logically
 
isolated
 
virtual
 
network
 
in
 
AWS.
 
●
 
It
 
allows
 
you
 
to
 
control
 
networking
:
 
IP
 
addresses,
 
routing,
 
firewalls,
 
and
 
connectivity
 
between
 
AWS
 
resources
 
and
 
external
 
networks.
 
●
 
Every
 
AWS
 
account
 
gets
 
a
 
default
 
VPC
,
 
but
 
you
 
can
 
(and
 
often
 
should)
 
create
 
custom
 
VPCs
 
for
 
better
 
control.
 
●
 
You
 
need
 
a
 
piece
 
of
 
land
 
→
 
this
 
is
 
your
 
VPC
 
(your
 
private
 
area
 
inside
 
AWS).
 
●
 
You
 
decide
 
where
 
to
 
place
 
rooms
 
→
 
these
 
are
 
your
 
subnets
 
(smaller
 
sections
 
inside
 
your
 
land).
 
●
 
You
 
install
 
walls
 
and
 
gates
 
→
 
these
 
are
 
your
 
security
 
groups
 
and
 
network
 
ACLs
 
(deciding
 
who
 
can
 
enter
 
or
 
exit).

## Page 11

●
 
You
 
connect
 
the
 
house
 
to
 
the
 
internet
 
with
 
a
 
Wi-Fi
 
router
 
→
 
this
 
is
 
the
 
Internet
 
Gateway
 
(IGW)
.
 
●
 
For
 
private
 
areas
 
(like
 
a
 
storeroom
 
not
 
connected
 
to
 
the
 
internet),
 
you
 
only
 
allow
 
access
 
from
 
inside
 
→
 
these
 
are
 
private
 
subnets
.
 
●
 
You
 
may
 
also
 
hire
 
a
 
watchman
 
→
 
this
 
is
 
like
 
a
 
Network
 
Firewall
 
or
 
NAT
 
Gateway
.
 
 
👉
 
In
 
short:
 
A
 
VPC
 
is
 
your
 
own
 
private
 
network
 
inside
 
AWS
,
 
where
 
you
 
decide
 
how
 
systems
 
connect,
 
communicate,
 
and
 
stay
 
secure.
 
2.
 
Core
 
Components
 
of
 
VPC
 
Let’s
 
break
 
down
 
the
 
building
 
blocks:
 
🟣
 
a)
 
CIDR
 
Block
 
(IP
 
Range)
 
●
 
Defines
 
the
 
IP
 
address
 
space
 
of
 
your
 
VPC.
 
 
●
 
Example:
 
10.0.0.0/16
 
→
 
gives
 
you
 
65,536
 
IPs.
 
 
●
 
You
 
divide
 
this
 
into
 
subnets
.
 
 
●
 
IPv4
 
and
 
IPv6
 
supported
.
 
 
🟣
 
b)
 
Subnets
 
●
 
Subdivisions
 
of
 
your
 
VPC’s
 
IP
 
range.
 
 
●
 
Types
:
 
 
○
 
Public
 
Subnet
 
→
 
connected
 
to
 
Internet
 
Gateway
.
 
Resources
 
here
 
can
 
access/receive
 
internet
 
traffic.
 
 
○
 
Private
 
Subnet
 
→
 
no
 
direct
 
internet
 
access.
 
Used
 
for
 
databases,
 
backend
 
servers,
 
etc.
 
 
○
 
Isolated
 
Subnet
 
→
 
completely
 
internal,
 
with
 
no
 
external
 
access
 
at
 
all.
 
 
●
 
Each
 
subnet
 
belongs
 
to
 
one
 
Availability
 
Zone
 
(AZ)
.
 
 
🟣
 
c)
 
Route
 
Tables

## Page 12

●
 
Define
 
traffic
 
routing
 
rules
 
for
 
subnets.
 
 
●
 
Example:
 
 
○
 
Default
 
route
 
(
0.0.0.0/0
 
→
 
IGW
)
 
→
 
sends
 
traffic
 
to
 
the
 
internet.
 
 
○
 
Internal
 
route
 
(
10.0.1.0/24
 
→
 
local
)
 
→
 
stays
 
within
 
VPC.
 
 
🟣
 
d)
 
Internet
 
Gateway
 
(IGW)
 
●
 
A
 
horizontally
 
scaled,
 
highly
 
available
 
gateway
 
to
 
connect
 
VPC
 
↔
 
Internet
.
 
 
●
 
Must
 
be
 
attached
 
to
 
a
 
VPC
 
to
 
allow
 
internet
 
communication.
 
 
🟣
 
e)
 
NAT
 
Gateway
 
(Network
 
Address
 
Translation)
 
●
 
Allows
 
private
 
subnet
 
instances
 
to
 
access
 
the
 
internet
 
(for
 
updates,
 
patches,
 
downloads)
 
without
 
exposing
 
them
 
to
 
incoming
 
internet
 
traffic.
 
 
●
 
Example:
 
Database
 
server
 
in
 
a
 
private
 
subnet
 
needs
 
to
 
download
 
security
 
patches
 
→
 
uses
 
NAT.
 
🟣
 
f)
 
Security
 
Controls
 
●
 
Security
 
Groups
 
(SGs):
 
 
○
 
Act
 
as
 
firewalls
 
for
 
EC2
 
instances
.
 
 
○
 
Stateful
 
→
 
If
 
you
 
allow
 
inbound,
 
outbound
 
is
 
automatically
 
allowed.
 
 
○
 
Example:
 
Allow
 
inbound
 
port
 
22
 
(SSH)
 
from
 
office
 
IP.
 
 
●
 
Network
 
ACLs
 
(NACLs):
 
 
○
 
Act
 
as
 
firewalls
 
for
 
subnets
.
 
 
○
 
Stateless
 
→
 
Must
 
define
 
both
 
inbound
 
and
 
outbound
 
rules.
 
 
○
 
Example:
 
Block
 
all
 
inbound
 
traffic
 
from
 
0.0.0.0/0
 
on
 
port
 
23
 
(Telnet)
.
 
 
🟣
 
g)
 
Elastic
 
IPs
 
&
 
ENIs

## Page 13

●
 
Elastic
 
IP
 
(EIP):
 
Static
 
IPv4
 
address
 
for
 
dynamic
 
cloud
 
resources.
 
 
●
 
ENI
 
(Elastic
 
Network
 
Interface):
 
Virtual
 
network
 
card
 
attached
 
to
 
an
 
EC2.
 
You
 
can
 
attach/detach
 
ENIs
 
for
 
redundancy.
 
 
🟣
 
h)
 
VPC
 
Peering
 
●
 
Connects
 
two
 
VPCs
 
(even
 
across
 
accounts/regions).
 
 
●
 
Traffic
 
flows
 
as
 
if
 
they’re
 
in
 
the
 
same
 
network
,
 
but
 
no
 
transitive
 
routing
 
(VPC
 
A
 
↔
 
B
 
↔
 
C
 
is
 
not
 
allowed
 
directly).
 
 
🟣
 
i)
 
Transit
 
Gateway
 
●
 
A
 
hub-and-spoke
 
model
 
to
 
connect
 
multiple
 
VPCs
 
+
 
On-premises
 
networks
 
at
 
scale.
 
 
●
 
Simplifies
 
routing
 
vs.
 
multiple
 
VPC
 
Peering
 
connections.
 
 
🟣
 
j)
 
VPC
 
Endpoints
 
●
 
Private
 
connections
 
between
 
VPC
 
↔
 
AWS
 
services
 
(like
 
S3,
 
DynamoDB).
 
 
●
 
Avoids
 
using
 
the
 
internet
 
(more
 
secure
 
and
 
cost-efficient).
 
 
●
 
Types:
 
 
○
 
Gateway
 
Endpoint
 
(S3,
 
DynamoDB)
 
 
○
 
Interface
 
Endpoint
 
(PrivateLink)
 
→
 
ENI
 
powered
 
 
🟣
 
k)
 
VPN
 
&
 
Direct
 
Connect
 
●
 
Site-to-Site
 
VPN:
 
Secure
 
IPSec
 
tunnel
 
between
 
VPC
 
↔
 
On-premises
 
data
 
center.
 
 
●
 
AWS
 
Direct
 
Connect:
 
Dedicated
 
physical
 
fiber
 
link
 
between
 
your
 
premises
 
↔
 
AWS.
 
Lower
 
latency,
 
higher
 
bandwidth.
 
3.
 
Default
 
VPC
 
vs.
 
Custom
 
VPC
 
●
 
Default
 
VPC
 
→
 
Automatically
 
created,
 
ready-to-use,
 
all
 
subnets
 
public
 
by
 
default.

## Page 14

●
 
Custom
 
VPC
 
→
 
You
 
define
 
CIDR,
 
subnets,
 
route
 
tables,
 
and
 
gateways.
 
Used
 
in
 
production
 
for
 
security
 
&
 
flexibility
.
 
 
4.
 
Best
 
Practices
 
●
 
Use
 
private
 
subnets
 
for
 
databases
,
 
public
 
for
 
web
 
servers
.
 
 
●
 
Enable
 
Flow
 
Logs
 
to
 
capture
 
traffic
 
metadata
 
(security
 
monitoring).
 
 
●
 
Use
 
NAT
 
Gateway
 
instead
 
of
 
public
 
IPs
 
for
 
backend
 
resources.
 
 
●
 
Apply
 
least
 
privilege
 
rules
 
in
 
Security
 
Groups
 
&
 
NACLs.
 
 
●
 
Use
 
Transit
 
Gateway
 
for
 
multi-VPC
 
connectivity
 
at
 
scale.
 
🔑
 
Key
 
Pairs
 
(SSH/RDP
 
Access)
 
1.
 
What
 
is
 
a
 
Key
 
Pair?
 
When
 
you
 
launch
 
an
 
EC2
 
instance
 
(a
 
virtual
 
server
 
in
 
AWS),
 
you
 
need
 
a
 
way
 
to
 
log
 
into
 
it
 
securely
.
 
AWS
 
uses
 
something
 
called
 
Key
 
Pairs
 
to
 
do
 
this.
 
A
 
Key
 
Pair
 
is
 
a
 
cryptographic
 
mechanism
 
based
 
on
 
Public
 
Key
 
Infrastructure
 
(PKI)
.
 
It
 
consists
 
of:
 
●
 
Public
 
Key
 
–
 
stored
 
by
 
AWS
 
on
 
your
 
instance
 
(in
 
the
 
~/.ssh/authorized_keys
 
file
 
for
 
Linux).
 
 
●
 
Private
 
Key
 
(.pem
 
file)
 
–
 
downloaded
 
once
 
by
 
you
 
when
 
you
 
create
 
the
 
Key
 
Pair.
 
 
Together,
 
they
 
enable
 
asymmetric
 
encryption
 
for
 
secure
 
authentication.
 
●
 
Think
 
of
 
a
 
key
 
pair
 
like
 
a
 
lock
 
and
 
key
 
for
 
your
 
server.
 
 
●
 
AWS
 
installs
 
the
 
lock
 
(public
 
key)
 
on
 
your
 
EC2
 
instance.
 
 
●
 
You
 
keep
 
the
 
key
 
(private
 
key)
 
with
 
you
 
on
 
your
 
computer.
 
 
●
 
When
 
you
 
try
 
to
 
connect
 
to
 
the
 
server
 
(using
 
SSH
 
for
 
Linux
 
or
 
RDP
 
for
 
Windows),
 
the
 
server
 
checks
 
if
 
your
 
private
 
key
 
matches
 
the
 
lock
 
(public
 
key).

## Page 15

●
 
If
 
they
 
match
 
→
 
✅
 
You’re
 
allowed
 
in.
 
If
 
not
 
→
 
❌
 
Access
 
is
 
denied.
 
 
This
 
way,
 
you
 
don’t
 
need
 
to
 
use
 
insecure
 
passwords.
 
It’s
 
like
 
having
 
a
 
digital
 
key
 
to
 
your
 
cloud
 
house.
 
2.
 
How
 
Key
 
Pairs
 
Work
 
in
 
EC2
 
●
 
When
 
you
 
create
 
a
 
new
 
EC2
 
instance,
 
you
 
must
 
choose
 
or
 
create
 
a
 
Key
 
Pair
.
 
 
●
 
AWS
 
injects
 
the
 
public
 
key
 
into
 
the
 
instance
 
metadata
 
during
 
boot.
 
 
●
 
For
 
Linux
 
instances
:
 
 
○
 
The
 
public
 
key
 
is
 
stored
 
in
 
the
 
~/.ssh/authorized_keys
 
file
 
for
 
the
 
default
 
user
 
(e.g.,
 
ec2-user
,
 
ubuntu
,
 
centos
).
 
 
○
 
You
 
use
 
your
 
private
 
key
 
with
 
an
 
SSH
 
client
 
to
 
log
 
in.
 
 
Example:
 
 
 
ssh
 
-i
 
mykey.pem
 
ec2-user@<public-ip>
 
○
 
 
●
 
For
 
Windows
 
instances
:
 
 
○
 
The
 
Key
 
Pair
 
is
 
used
 
to
 
decrypt
 
the
 
randomly
 
generated
 
Administrator
 
password
.
 
 
○
 
You
 
use
 
RDP
 
(Remote
 
Desktop
 
Protocol)
 
to
 
connect
 
after
 
retrieving
 
the
 
password.
 
 
3.
 
Key
 
Pair
 
File
 
Formats
 
●
 
PEM
 
(.pem)
:
 
Default
 
format
 
provided
 
by
 
AWS
 
(used
 
in
 
Linux/macOS).
 
 
●
 
PPK
 
(.ppk)
:
 
PuTTY
 
format
 
(used
 
in
 
Windows
 
with
 
PuTTY).
 
 
●
 
AWS
 
can
 
convert
 
.pem
 
→
 
.ppk
 
using
 
PuTTYgen
 
if
 
needed.
 
 
4.
 
Important
 
Security
 
Considerations

## Page 16

●
 
AWS
 
never
 
stores
 
your
 
private
 
key
 
–
 
you
 
must
 
download
 
it
 
once
 
at
 
creation.
 
If
 
lost,
 
you
 
cannot
 
download
 
it
 
again
.
 
 
●
 
If
 
you
 
lose
 
your
 
private
 
key,
 
you
 
cannot
 
log
 
in.
 
You’d
 
need
 
to:
 
 
○
 
Use
 
Systems
 
Manager
 
Session
 
Manager
 
(if
 
enabled).
 
 
○
 
Or
 
detach
 
the
 
root
 
EBS
 
volume,
 
mount
 
it
 
to
 
another
 
instance,
 
and
 
add
 
a
 
new
 
key.
 
 
●
 
Protect
 
the
 
private
 
key
 
file
 
(
chmod
 
400
 
mykey.pem
 
on
 
Linux).
 
 
●
 
Use
 
different
 
Key
 
Pairs
 
for
 
different
 
environments
 
(dev/test/prod).
 
 
5.
 
Best
 
Practices
 
●
 
🔐
 
Use
 
SSH
 
key
 
rotation
 
policies
 
→
 
change
 
keys
 
periodically.
 
 
●
 
󰰁
 
Use
 
IAM
 
users
 
with
 
AWS
 
Systems
 
Manager
 
Session
 
Manager
 
→
 
avoids
 
key
 
distribution.
 
 
●
 
📁
 
Store
 
private
 
keys
 
securely
 
(encrypted
 
vaults
 
like
 
AWS
 
Secrets
 
Manager,
 
HashiCorp
 
Vault,
 
or
 
password
 
managers).
 
 
●
 
🚫
 
Never
 
hardcode
 
or
 
share
 
private
 
keys
 
in
 
GitHub,
 
Slack,
 
or
 
email.
 
 
6.
 
Integration
 
with
 
AWS
 
Services
 
●
 
CloudFormation
 
/
 
Terraform
 
→
 
Key
 
Pairs
 
can
 
be
 
specified
 
when
 
deploying
 
EC2.
 
 
●
 
AWS
 
Systems
 
Manager
 
(Session
 
Manager)
 
→
 
provides
 
keyless
 
access
 
(no
 
SSH/RDP
 
needed).
 
 
●
 
EKS/EMR
 
Clusters
 
→
 
rely
 
on
 
Key
 
Pairs
 
for
 
initial
 
cluster
 
node
 
login.
 
Amazon
 
EC2
 
User
 
Data
 
and
 
Instance
 
Metadata
 
(IMDS)
 
1.
 
EC2
 
User
 
Data

## Page 17

When
 
you
 
launch
 
a
 
computer
 
(EC2
 
instance)
 
in
 
AWS,
 
sometimes
 
you
 
want
 
it
 
to
 
do
 
something
 
automatically
 
the
 
first
 
time
 
it
 
starts.
 
For
 
example:
 
●
 
Install
 
software
 
 
●
 
Download
 
updates
 
 
●
 
Set
 
up
 
your
 
application
 
 
This
 
is
 
where
 
User
 
Data
 
comes
 
in.
 
Think
 
of
 
it
 
like
 
a
 
"note
 
to
 
the
 
computer"
 
that
 
says:
 
“When
 
you
 
wake
 
up
 
for
 
the
 
first
 
time,
 
do
 
these
 
tasks
 
automatically.”
 
●
 
User
 
Data
 
is
 
data
 
passed
 
to
 
an
 
instance
 
at
 
launch
 
time.
 
It
 
is
 
typically
 
used
 
for
 
bootstrapping
 
(automating
 
the
 
initial
 
setup).
 
 
●
 
Execution:
 
 
○
 
By
 
default,
 
User
 
Data
 
scripts
 
run
 
only
 
at
 
the
 
first
 
boot
.
 
 
○
 
You
 
can
 
configure
 
them
 
to
 
run
 
at
 
every
 
restart
 
by
 
modifying
 
cloud-init
 
(Linux)
 
or
 
EC2Launch
 
(Windows).
 
 
On
 
the
 
other
 
hand,
 
sometimes
 
your
 
running
 
computer
 
needs
 
to
 
know
 
more
 
about
 
itself
.
 
For
 
example:
 
●
 
What
 
is
 
my
 
public
 
IP
 
address?
 
 
●
 
What
 
is
 
my
 
instance
 
ID?
 
 
●
 
What
 
region
 
am
 
I
 
in?
 
 
This
 
is
 
where
 
Instance
 
Metadata
 
comes
 
in.
 
Think
 
of
 
it
 
like
 
the
 
computer
 
asking
 
AWS
 
about
 
itself
:
 
“Hey
 
AWS,
 
who
 
am
 
I
 
and
 
what’s
 
around
 
me?”
 
So:
 
●
 
User
 
Data
 
=
 
instructions
 
you
 
give
 
at
 
startup.
 
 
●
 
Metadata
 
=
 
information
 
the
 
instance
 
can
 
fetch
 
about
 
itself.
 
 
●
 
Format:

## Page 18

○
 
User
 
Data
 
can
 
be:
 
 
■
 
Shell
 
scripts
 
(Linux)
 
 
■
 
PowerShell
 
scripts
 
(Windows)
 
 
■
 
Cloud-init
 
directives
 
(YAML)
 
 
●
 
Storage:
 
 
○
 
AWS
 
stores
 
User
 
Data
 
securely
 
with
 
the
 
instance.
 
 
○
 
Maximum
 
size:
 
16
 
KB
.
 
 
●
 
Use
 
Cases:
 
 
○
 
Install
 
Apache/Nginx
 
on
 
first
 
boot.
 
 
○
 
Fetch
 
and
 
deploy
 
application
 
code
 
from
 
S3.
 
 
○
 
Run
 
updates
 
and
 
security
 
patches.
 
 
○
 
Configure
 
logging
 
and
 
monitoring
 
agents.
 
 
👉
 
(Linux
 
User
 
Data
 
script):
 
#!/bin/bash
 
yum
 
update
 
-y
 
yum
 
install
 
-y
 
httpd
 
systemctl
 
start
 
httpd
 
systemctl
 
enable
 
httpd
 
echo
 
"Hello
 
from
 
EC2"
 
>
 
/var/www/html/index.html
 
 
This
 
script
 
updates
 
the
 
server,
 
installs
 
Apache,
 
starts
 
it,
 
and
 
puts
 
a
 
message
 
on
 
the
 
website.
 
2.
 
Instance
 
Metadata
 
(IMDS)

## Page 19

●
 
Metadata
 
service
 
provides
 
information
 
about
 
the
 
instance
.
 
 
●
 
Access:
 
 
Available
 
from
 
inside
 
the
 
instance
 
at:
 
 
 
http://169.254.169.254/latest/meta-data/
 
○
 
 
○
 
It
 
does
 
not
 
require
 
internet
 
access.
 
 
●
 
Types
 
of
 
Metadata:
 
 
○
 
Meta-Data:
 
Instance
 
ID,
 
AMI
 
ID,
 
private/public
 
IPs,
 
security
 
groups,
 
region,
 
availability
 
zone,
 
etc.
 
 
○
 
Dynamic
 
Data:
 
Info
 
that
 
changes
 
over
 
time,
 
e.g.,
 
boot
 
status.
 
 
○
 
User
 
Data:
 
You
 
can
 
also
 
retrieve
 
the
 
User
 
Data
 
script
 
via
 
metadata
 
endpoint.
 
 
○
 
IAM
 
Role
 
credentials:
 
Temporary
 
credentials
 
if
 
an
 
IAM
 
role
 
is
 
attached.
 
 
👉
 
Commands:
 
#
 
Get
 
instance
 
ID
 
curl
 
http://169.254.169.254/latest/meta-data/instance-id
 
 
#
 
Get
 
public
 
IP
 
curl
 
http://169.254.169.254/latest/meta-data/public-ipv4
 
 
#
 
Get
 
availability
 
zone
 
curl
 
http://169.254.169.254/latest/meta-data/placement/availability-zone
 
3.
 
IMDS
 
Versions

## Page 20

●
 
IMDSv1
 
(older):
 
Uses
 
HTTP
 
GET
 
requests
 
with
 
no
 
session
 
protection.
 
Vulnerable
 
to
 
SSRF
 
attacks
 
(Server-Side
 
Request
 
Forgery).
 
 
●
 
IMDSv2
 
(recommended):
 
Uses
 
a
 
session-based
 
token
.
 
 
○
 
Steps:
 
 
1.
 
Request
 
a
 
token
 
with
 
an
 
HTTP
 
PUT
 
request.
 
 
2.
 
Use
 
the
 
token
 
to
 
fetch
 
metadata.
 
 
○
 
This
 
prevents
 
attackers
 
from
 
easily
 
stealing
 
IAM
 
credentials.
 
 
👉
 
(IMDSv2):
 
#
 
Get
 
token
 
TOKEN=`curl
 
-X
 
PUT
 
"http://169.254.169.254/latest/api/token"
 
\
 
  
-H
 
"X-aws-ec2-metadata-token-ttl-seconds:
 
21600"`
 
 
#
 
Use
 
token
 
to
 
fetch
 
metadata
 
curl
 
-H
 
"X-aws-ec2-metadata-token:
 
$TOKEN"
 
\
 
  
http://169.254.169.254/latest/meta-data/instance-id
 
🏗
 
Key
 
Differences
 
Feature
 
User
 
Data
 
Instance
 
Metadata
 
(IMDS)
 
Purpose
 
Bootstrapping
 
automation
 
(setup
 
at
 
launch)
 
Retrieve
 
information
 
about
 
the
 
instance
 
Execution
 
Runs
 
at
 
startup
 
(default:
 
first
 
boot
 
only)
 
Queried
 
anytime
 
during
 
runtime

## Page 21

Accessed
 
By
 
AWS
 
→
 
Instance
 
(one-way
 
instruction)
 
Instance
 
→
 
AWS
 
(self-query)
 
Examples
 
Install
 
software,
 
configure
 
apps
 
Get
 
IP,
 
Instance
 
ID,
 
IAM
 
role
 
credentials
 
Security
 
Concern
 
Can
 
contain
 
sensitive
 
scripts
 
(stored)
 
IMDSv1
 
vulnerable
 
→
 
Use
 
IMDSv2
 
Amazon
 
EC2
 
Placement
 
Groups
 
(Optional
 
for
 
Performance)
 
Placement
 
Groups
 
are
 
an
 
advanced
 
feature
 
in
 
EC2
 
that
 
control
 
how
 
AWS
 
places
 
your
 
instances
 
on
 
the
 
underlying
 
hardware
 
inside
 
an
 
Availability
 
Zone
 
(AZ)
.
 
 
They
 
help
 
you
 
optimize
 
networking
 
performance,
 
fault
 
tolerance,
 
or
 
both
 
depending
 
on
 
your
 
workload.
 
Think
 
of
 
them
 
as
 
strategic
 
grouping
 
policies
 
for
 
your
 
EC2
 
instances
 
inside
 
AWS
 
data
 
centers.
 
Imagine
 
you’re
 
arranging
 
computers
 
in
 
a
 
room:
 
●
 
If
 
you
 
put
 
them
 
next
 
to
 
each
 
other
,
 
they
 
can
 
talk
 
faster
 
(low
 
latency,
 
high
 
bandwidth).
 
 
●
 
If
 
you
 
spread
 
them
 
across
 
the
 
room
,
 
one
 
fire
 
won’t
 
destroy
 
all,
 
but
 
they
 
take
 
longer
 
to
 
communicate.
 
 
●
 
If
 
you
 
place
 
them
 
on
 
different
 
floors
,
 
you
 
get
 
both
 
safety
 
and
 
performance
 
balance.
 
 
Placement
 
Groups
 
are
 
just
 
AWS’s
 
way
 
of
 
letting
 
you
 
control
 
where
 
your
 
EC2
 
machines
 
"sit"
 
inside
 
the
 
giant
 
AWS
 
building.
 
AWS
 
offers
 
three
 
types
 
of
 
Placement
 
Groups
,
 
each
 
with
 
different
 
goals:
 
1.
 
Cluster
 
Placement
 
Group

## Page 22

●
 
Goal:
 
Maximum
 
performance
 
(low
 
latency
 
+
 
high
 
bandwidth).
 
 
●
 
How
 
it
 
works:
 
 
All
 
instances
 
are
 
placed
 
close
 
together
 
on
 
the
 
same
 
rack
 
or
 
within
 
a
 
single
 
AZ
.
 
 
●
 
Use
 
Cases:
 
 
○
 
High-performance
 
computing
 
(HPC)
 
 
○
 
Big
 
data
 
analytics
 
 
○
 
Machine
 
learning
 
training
 
 
●
 
Limitations:
 
 
○
 
Only
 
within
 
a
 
single
 
AZ
.
 
 
○
 
Works
 
best
 
with
 
specific
 
instance
 
types
 
that
 
support
 
enhanced
 
networking
 
(like
 
C5n,
 
P4d,
 
etc.).
 
2.
 
Spread
 
Placement
 
Group
 
●
 
Goal:
 
High
 
fault
 
tolerance.
 
 
●
 
How
 
it
 
works:
 
 
Instances
 
are
 
spread
 
across
 
different
 
racks
 
(each
 
rack
 
has
 
its
 
own
 
power
 
and
 
network).
 
 
→
 
If
 
one
 
rack
 
fails,
 
only
 
one
 
instance
 
is
 
affected.
 
 
●
 
Use
 
Cases:
 
 
○
 
Critical
 
workloads
 
requiring
 
high
 
availability
.
 
 
○
 
Small
 
numbers
 
of
 
important
 
servers
 
(like
 
5–7
 
instances
 
for
 
HA
 
systems).
 
 
●
 
Limitations:
 
 
○
 
Max
 
7
 
instances
 
per
 
AZ
.
 
 
○
 
Higher
 
network
 
latency
 
compared
 
to
 
Cluster.
 
3.
 
Partition
 
Placement
 
Group

## Page 23

●
 
Goal:
 
Balance
 
between
 
performance
 
and
 
fault
 
tolerance
 
for
 
large
 
distributed
 
workloads
.
 
 
●
 
How
 
it
 
works:
 
 
Instances
 
are
 
divided
 
into
 
logical
 
partitions
.
 
 
Each
 
partition
 
is
 
isolated
 
at
 
the
 
hardware
 
level
 
(different
 
racks).
 
 
→
 
Multiple
 
instances
 
can
 
run
 
in
 
each
 
partition,
 
but
 
partitions
 
don’t
 
share
 
racks
.
 
 
●
 
Use
 
Cases:
 
 
○
 
Big
 
data
 
frameworks
 
like
 
Hadoop,
 
HDFS,
 
Cassandra.
 
 
○
 
Distributed
 
databases.
 
 
●
 
Limitations:
 
 
○
 
Supports
 
hundreds
 
of
 
instances
.
 
 
○
 
Designed
 
for
 
large-scale
 
distributed
 
clusters
.
 
 
⚙
 
How
 
Placement
 
Groups
 
Work
 
(Internals)
 
●
 
AWS’s
 
underlying
 
hypervisor
 
decides
 
where
 
to
 
place
 
instances.
 
 
●
 
Normally,
 
you
 
don’t
 
control
 
physical
 
placement.
 
Placement
 
Groups
 
give
 
you
 
hints
 
to
 
AWS
:
 
 
○
 
Cluster
 
→
 
“Put
 
them
 
all
 
together.”
 
 
○
 
Spread
 
→
 
“Put
 
them
 
far
 
apart.”
 
 
○
 
Partition
 
→
 
“Put
 
them
 
in
 
grouped
 
isolation.”
 
 
●
 
Requires
 
homogeneous
 
instance
 
types
 
for
 
best
 
performance.
 
 
●
 
Some
 
operations
 
(like
 
moving
 
an
 
instance
 
from
 
one
 
PG
 
to
 
another)
 
may
 
require
 
stopping/relaunching
 
instances.
 
 
🛠
 
CLI
 
/
 
AWS
 
Console
 
 
Create
 
a
 
Placement
 
Group
 
(Cluster)

## Page 24

aws
 
ec2
 
create-placement-group
 
\
 
    
--group-name
 
my-cluster-pg
 
\
 
    
--strategy
 
cluster
 
 
Launch
 
Instances
 
into
 
it
 
aws
 
ec2
 
run-instances
 
\
 
    
--image-id
 
ami-12345678
 
\
 
    
--count
 
4
 
\
 
    
--instance-type
 
c5n.9xlarge
 
\
 
    
--key-name
 
MyKeyPair
 
\
 
    
--placement
 
GroupName=my-cluster-pg
 
📊
 
Comparison
 
Table
 
Placement
 
Group
 
Optimized
 
for
 
Availabilit
y
 
Latenc
y
 
Instance
 
Limit
 
Example
 
Use
 
Case
 
Cluster
 
Performance
 
Low
 
Very
 
low
 
Hundreds
 
(same
 
AZ)
 
HPC,
 
ML,
 
Analytics
 
Spread
 
Fault
 
Tolerance
 
High
 
Higher
 
7
 
per
 
AZ
 
Small
 
HA
 
systems
 
Partition
 
Balance
 
(large
 
scale)
 
Medium
 
Medium
 
100s
 
(multi-partition)
 
Hadoop,
 
Cassandra
 
✅
 
Summary:
 
 
Placement
 
Groups
 
are
 
optional
 
but
 
powerful
 
for
 
workloads
 
where
 
performance
 
or
 
high
 
availability
 
is
 
critical
.

## Page 25

●
 
Cluster
 
=
 
Speed
 
🚀
 
 
●
 
Spread
 
=
 
Safety
 
🛡
 
 
●
 
Partition
 
=
 
Big
 
Data
 
📊
 
 
Monitoring
 
&
 
Management
 
in
 
EC2
 
Think
 
of
 
EC2
 
Monitoring
 
&
 
Management
 
as
 
keeping
 
an
 
eye
 
on
 
your
 
servers
 
and
 
controlling
 
their
 
behavior
.
 
●
 
Just
 
like
 
in
 
a
 
factory,
 
you
 
install
 
sensors
 
to
 
check
 
temperature,
 
energy
 
use,
 
and
 
machine
 
speed
,
 
in
 
EC2
 
you
 
use
 
monitoring
 
tools
 
to
 
track
 
CPU
 
usage,
 
memory,
 
disk,
 
and
 
network
 
activity.
 
 
●
 
If
 
something
 
goes
 
wrong,
 
like
 
a
 
machine
 
overheating,
 
an
 
alarm
 
system
 
alerts
 
the
 
manager
.
 
In
 
EC2,
 
CloudWatch
 
sends
 
alerts
 
when
 
your
 
instance
 
is
 
overloaded.
 
 
●
 
Management
 
tools
 
let
 
you
 
start,
 
stop,
 
restart,
 
or
 
even
 
automatically
 
replace
 
faulty
 
machines
—just
 
like
 
a
 
factory
 
manager
 
who
 
can
 
pause
 
or
 
replace
 
a
 
machine
 
when
 
it
 
fails.
 
 
In
 
short:
 
Monitoring
 
ensures
 
visibility,
 
Management
 
ensures
 
control.
 
1.
 
Amazon
 
CloudWatch
 
(Monitoring
 
Service)
 
●
 
Purpose:
 
Collects
 
metrics,
 
logs,
 
and
 
events
 
from
 
EC2
 
instances.
 
 
●
 
Default
 
Metrics
 
(Basic
 
Monitoring):
 
Provided
 
automatically
 
every
 
5
 
minutes.
 
Includes:
 
 
○
 
CPU
 
Utilization
 
(%)
 
 
○
 
Network
 
In/Out
 
(bytes)
 
 
○
 
Disk
 
Reads/Writes
 
(bytes)
 
 
○
 
Status
 
Checks
 
(instance
 
reachability
 
&
 
system
 
health)
 
 
●
 
Detailed
 
Monitoring:
 
Provides
 
1-minute
 
metrics
 
for
 
fine-grained
 
visibility.

## Page 26

📌
 
Use
 
Case:
 
If
 
CPU
 
>
 
80%
 
for
 
5
 
minutes,
 
trigger
 
an
 
Auto
 
Scaling
 
policy
 
to
 
launch
 
new
 
instances.
 
2.
 
CloudWatch
 
Alarms
 
●
 
Purpose:
 
Define
 
thresholds
 
and
 
take
 
actions.
 
 
●
 
Example:
 
 
○
 
Alarm
 
if
 
CPU
 
>
 
70%
 
for
 
10
 
minutes.
 
 
○
 
Actions:
 
send
 
SNS
 
notification
 
(email/SMS)
 
or
 
Auto
 
Scaling
 
action
.
 
 
3.
 
CloudWatch
 
Logs
 
●
 
EC2
 
instances
 
can
 
push
 
application/system
 
logs
 
to
 
CloudWatch
 
Logs.
 
 
●
 
Helps
 
in
 
debugging
 
by
 
centralizing
 
log
 
storage
 
and
 
analysis.
 
 
4.
 
CloudTrail
 
(Audit
 
&
 
Management
 
Logging)
 
●
 
Tracks
 
who
 
did
 
what
 
in
 
your
 
AWS
 
account.
 
 
●
 
Example:
 
Records
 
actions
 
like:
 
 
○
 
StartInstances
 
 
○
 
StopInstances
 
 
○
 
Security
 
Group
 
changes
 
 
●
 
Useful
 
for
 
compliance
 
&
 
security
 
audits
.
 
 
5.
 
AWS
 
Systems
 
Manager
 
(SSM)
 
●
 
A
 
management
 
tool
 
for
 
automating
 
administrative
 
tasks.

## Page 27

●
 
Key
 
Features:
 
 
○
 
Session
 
Manager
 
→
 
Secure
 
shell
 
(SSH-like)
 
access
 
without
 
opening
 
port
 
22.
 
 
○
 
Run
 
Command
 
→
 
Execute
 
scripts/commands
 
on
 
EC2
 
instances.
 
 
○
 
Patch
 
Manager
 
→
 
Apply
 
OS
 
and
 
software
 
updates
 
automatically.
 
 
○
 
Inventory
 
→
 
Collect
 
instance
 
configuration
 
details.
 
 
6.
 
Auto
 
Scaling
 
(Self-Management
 
for
 
Performance
 
&
 
Cost)
 
●
 
Purpose:
 
Automatically
 
adjusts
 
the
 
number
 
of
 
EC2
 
instances
 
based
 
on
 
demand.
 
 
●
 
Types:
 
 
○
 
Dynamic
 
Scaling:
 
Scale
 
up/down
 
based
 
on
 
metrics
 
(CPU,
 
memory).
 
 
○
 
Scheduled
 
Scaling:
 
Scale
 
at
 
fixed
 
times
 
(e.g.,
 
add
 
instances
 
every
 
morning
 
at
 
9
 
AM).
 
 
○
 
Predictive
 
Scaling:
 
Uses
 
ML
 
to
 
anticipate
 
demand.
 
 
7.
 
Elastic
 
Load
 
Balancing
 
(ELB)
 
●
 
Works
 
with
 
EC2
 
to
 
distribute
 
traffic
 
across
 
multiple
 
instances.
 
 
●
 
Integrated
 
with
 
CloudWatch
 
for
 
monitoring
 
traffic
 
patterns
 
and
 
health
 
checks.
 
 
8.
 
Trusted
 
Advisor
 
(Best
 
Practices
 
Check)
 
●
 
Provides
 
recommendations
 
for
 
cost
 
optimization,
 
performance,
 
security,
 
and
 
fault
 
tolerance.
 
 
●
 
Example:
 
Identifies
 
underutilized
 
EC2
 
instances
 
and
 
suggests
 
downsizing.

## Page 28

⚙
 
Workflow
 
Example:
 
How
 
Monitoring
 
&
 
Management
 
Work
 
Together
 
1.
 
CloudWatch
 
monitors
 
EC2
 
→
 
detects
 
CPU
 
utilization
 
at
 
95%.
 
 
2.
 
CloudWatch
 
Alarm
 
triggers
 
an
 
action
 
→
 
notifies
 
via
 
SNS
 
and
 
scales
 
out
 
using
 
Auto
 
Scaling
.
 
 
3.
 
Auto
 
Scaling
 
launches
 
2
 
new
 
EC2
 
instances.
 
 
4.
 
Load
 
Balancer
 
distributes
 
traffic
 
across
 
old
 
+
 
new
 
instances.
 
 
5.
 
CloudTrail
 
logs
 
the
 
action
 
for
 
auditing.
 
 
6.
 
Systems
 
Manager
 
patches
 
and
 
configures
 
the
 
new
 
instances
 
automatically.
 
 
 
🏆
 
Key
 
Benefits
 
✅
 
Visibility:
 
Track
 
instance
 
health
 
and
 
performance.
 
 
✅
 
Automation:
 
Reduce
 
manual
 
management
 
through
 
scaling,
 
patching,
 
and
 
healing.
 
 
✅
 
Security:
 
Audit
 
actions
 
and
 
restrict
 
access.
 
 
✅
 
Reliability:
 
Ensure
 
apps
 
stay
 
online
 
even
 
if
 
some
 
EC2s
 
fail.
 
🎯
 
Summary
 
The
 
core
 
components
 
of
 
an
 
EC2
 
instance
 
are:
 
 
✅
 
AMI
 
(blueprint)
 
 
✅
 
Instance
 
Types
 
(hardware
 
config)
 
 
✅
 
Instance
 
Storage
 
(EBS,
 
Instance
 
Store,
 
EFS,
 
S3)
 
 
✅
 
Networking
 
(VPC,
 
IPs,
 
Security
 
Groups,
 
ENIs)
 
 
✅
 
Key
 
Pairs
 
(authentication)
 
 
✅
 
User
 
Data
 
&
 
Metadata
 
(automation
 
&
 
instance
 
info)
 
 
✅
 
Placement
 
Groups
 
(performance
 
optimization)
 
 
✅
 
Monitoring
 
&
 
Management
 
(CloudWatch,
 
SSM)

