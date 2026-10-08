# 🐧 Linux Systems Administration & Networking: The Definitive Master Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Linux Kernel Architecture, Filesystem Hierarchy Standard (FHS), User & Privilege Management, POSIX Permissions & Special Bits (SUID, SGID, Sticky), Process Management (`systemd`), Disk & Memory Diagnostics, Text Processing (`grep`, `awk`, `sed`), OSI & TCP/IP Stack, TCP 3-Way Handshake, DNS Resolution, and Network Troubleshooting Toolchains.

---

## 📑 Table of Contents
- [1. Linux Kernel Architecture & Filesystem Hierarchy (FHS)](#1-linux-kernel-architecture--filesystem-hierarchy-fhs)
- [2. User, Group, & Sudoers Administration](#2-user-group--sudoers-administration)
- [3. File Permissions, Ownership, & Special Bits](#3-file-permissions-ownership--special-bits)
- [4. Process Lifecycle, Signals, & `systemd` Services](#4-process-lifecycle-signals--systemd-services)
- [5. System Resource Diagnostics (CPU, Memory, Disk, I/O)](#5-system-resource-diagnostics-cpu-memory-disk-io)
- [6. DevOps Text Processing Power Tools (`grep`, `awk`, `sed`, `find`)](#6-devops-text-processing-power-tools-grep-awk-sed-find)
- [7. OSI 7-Layer vs TCP/IP 4-Layer Architecture](#7-osi-7-layer-vs-tcpip-4-layer-architecture)
- [8. TCP vs UDP Protocol Comparison](#8-tcp-vs-udp-protocol-comparison)
- [9. TCP 3-Way Handshake & Connection Teardown](#9-tcp-3-way-handshake--connection-teardown)
- [10. DNS Resolution Lifecycle & IP Subnetting (CIDR)](#10-dns-resolution-lifecycle--ip-subnetting-cidr)
- [11. Network Troubleshooting CLI Toolchain (`ss`, `curl`, `dig`, `tcpdump`)](#11-network-troubleshooting-cli-toolchain-ss-curl-dig-tcpdump)
- [12. Senior DevOps Interview Q&A](#12-senior-devops-interview-qa)

---

## 1. Linux Kernel Architecture & Filesystem Hierarchy (FHS)

### Linux Architectural Layers
```text
┌─────────────────────────────────────────────────────────────┐
│                 User Space Applications                     │
│         (Shell, Web Servers, Docker Daemon, Python)         │
└──────────────────────────────┬──────────────────────────────┘
                               │ System Calls (syscalls: open, read, fork)
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                       Linux Kernel                          │
│   • Process Scheduling      • Memory Management (Virtual)   │
│   • VFS (Filesystems)       • Device Drivers                │
│   • Network Stack (Netfilter)• Namespaces & cgroups         │
└──────────────────────────────┬──────────────────────────────┘
                               │ Hardware Instructions
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                   Physical Hardware                         │
│                    (CPU, RAM, Disks, NIC)                   │
└─────────────────────────────────────────────────────────────┘
```

### Filesystem Hierarchy Standard (FHS) Quick Reference
* `/` — Root of the entire filesystem tree.
* `/bin` & `/usr/bin` — Essential user command binaries (`bash`, `ls`, `grep`, `curl`).
* `/sbin` & `/usr/sbin` — Administrative system binaries (`iptables`, `fdisk`, `useradd`).
* `/etc` — System-wide configuration files (`/etc/passwd`, `/etc/hosts`, `/etc/ssh/sshd_config`).
* `/var` — Variable dynamic data (`/var/log` for system logs, `/var/lib/docker` for container layers).
* `/proc` — Virtual pseudo-filesystem exposing real-time kernel and process memory state (e.g., `/proc/cpuinfo`, `/proc/meminfo`).
* `/sys` — Virtual pseudo-filesystem exposing hardware device parameters and kernel tuning variables.
* `/tmp` — Ephemeral temporary files; flushed on reboot.
* `/dev` — Hardware and pseudo-device nodes (`/dev/sda`, `/dev/null`, `/dev/random`).

---

## 2. User, Group, & Sudoers Administration

### User & Group Management CLI
```bash
# Create a dedicated system user with home directory and bash shell
sudo useradd -m -s /bin/bash -g devops -G docker,sudo devops_user

# Modify existing user: add to supplementary group without removing existing groups
sudo usermod -aG docker devops_user

# Lock / unlock user account
sudo passwd -l devops_user   # Lock
sudo passwd -u devops_user   # Unlock

# Delete user and wipe home directory
sudo userdel -r old_user

# Inspect user ID, primary group, and supplementary group memberships
id devops_user
```

### Sudoers Security (`/etc/sudoers`)
* Always edit using `sudo visudo` to prevent syntax corruption that locks out root access.
* **Passwordless Sudo for CI/CD Automation Agents**:
```text
jenkins ALL=(ALL) NOPASSWD: ALL
```

---

## 3. File Permissions, Ownership, & Special Bits

### POSIX Permission Triplet (`rwxr-xr--`)
* **3 User Classes**: Owner (`u`), Group (`g`), Others (`o`).
* **Numeric Values**: Read (`r` = 4), Write (`w` = 2), Execute (`x` = 1).

### Permission Calculation Matrix
| Symbolic | Numeric | Meaning |
| :--- | :--- | :--- |
| `rwx------` | `700` | Owner has full read/write/execute; Group and Others have zero access (Private keys: `chmod 600`) |
| `rwxr-xr-x` | `755` | Owner can edit; Group and Others can read and execute (Standard executable scripts) |
| `rw-r--r--` | `644` | Owner can edit; Group and Others can read only (Standard config files) |

### Special Permission Bits
* **SUID (SetUID - `4000`)**: Executes file with the privileges of the **file owner** rather than the running user (e.g., `/usr/bin/passwd`).
* **SGID (SetGID - `2000`)**: New files created in directory automatically inherit the **group ownership** of the parent directory (Essential for shared engineering directories).
* **Sticky Bit (`1000`)**: Files in directory can only be deleted or renamed by the file owner or root (e.g., `/tmp` has permissions `1777`).

```bash
# Set SGID on a shared directory
sudo chmod 2775 /var/shared_project

# Change file owner and group recursively
sudo chown -R devops:devops /var/www/html
```

---

## 4. Process Lifecycle, Signals, & `systemd` Services

### Common Linux Process Signals
* **`SIGTERM` (Signal 15)**: Graceful termination request. Application intercepts signal, closes active connections, flushes buffers, and exits cleanly.
* **`SIGKILL` (Signal 9)**: Forceful, unconditional termination by kernel. Cannot be trapped or ignored by the process.
* **`SIGHUP` (Signal 1)**: Hangup signal; typically instructs daemons (Nginx, Prometheus) to reload configuration without dropping connections.

### Process Inspection CLI
```bash
# List all running processes with user, CPU %, and memory %
ps aux | grep node

# Search processes by name
pgrep -l nginx

# Graceful termination vs Force kill
kill -15 <PID>
kill -9 <PID>

# Interactive dynamic process monitor
top
htop
```

### Managing Daemons with `systemd`
```bash
# Start, stop, restart services
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx       # Hot-reload configuration without dropping traffic

# Enable / disable service to boot on startup
sudo systemctl enable nginx
sudo systemctl status nginx

# Inspect real-time logs of a systemd unit
journalctl -u nginx -f --tail=100
```

---

## 5. System Resource Diagnostics (CPU, Memory, Disk, I/O)

### The Production Diagnostic Toolkit
* **CPU & Load Average**:
  * `uptime` — Displays system running time and Load Averages (1m, 5m, 15m).
  * *Rule of Thumb*: Load Average should not exceed the total number of physical/virtual CPU cores.
* **Memory Utilization**:
  * `free -h` — Inspect total, used, free, and available RAM and Swap.
  * *Focus*: Always evaluate **`available`** memory, as Linux aggressively uses unused RAM for filesystem cache.
* **Disk Capacity & Inode Exhaustion**:
  * `df -h` — Inspect disk partition capacity.
  * `df -i` — Inspect **Inode usage**. (A disk can run out of inodes even with 50% free space if thousands of micro-files/logs exist!)
  * `du -sh /var/log/* | sort -hr | head -n 10` — Find the largest 10 space-consuming directories.
* **Disk I/O Bottlenecks**:
  * `iostat -xz 1 5` — Measure disk saturation, awaiting time (`await`), and utilization % (`%util`).
* **Network & Open Files**:
  * `lsof -i :8080` — Identify which process is holding a specific port open.

---

## 6. DevOps Text Processing Power Tools (`grep`, `awk`, `sed`, `find`)

```bash
# 1. GREP — Pattern Matching
grep -E "ERROR|FATAL" /var/log/app.log          # Match multiple regex patterns
grep -rn "API_KEY" /etc/                       # Recursive search with line numbers
grep -v "^#" config.conf                       # Invert match: strip commented lines

# 2. AWK — Column & Field Processing
# Extract IP address and HTTP status code from Nginx access log:
awk '{print $1, $9}' /var/log/nginx/access.log

# Sum total memory used by all nginx worker processes:
ps aux | grep nginx | awk '{sum += $6} END {print sum/1024, "MB"}'

# 3. SED — Stream Editing & Replacement
# Replace 'staging' with 'production' in place:
sed -i 's/staging/production/g' config.env

# Delete blank lines:
sed -i '/^$/d' file.txt

# 4. FIND — Filesystem Search & Batch Execution
# Find and delete log files older than 30 days:
find /var/log/app -name "*.log" -mtime +30 -exec rm -f {} \;

# Find files with dangerous world-writable permissions:
find / -perm -002 -type f 2>/dev/null
```

---

## 7. OSI 7-Layer vs TCP/IP 4-Layer Architecture

### Architecture Comparison

| Layer # | OSI 7-Layer Model | TCP/IP 4-Layer Model | Common Protocols & Protocols |
| :--- | :--- | :--- | :--- |
| **7** | Application | **Application Layer** | HTTP, HTTPS, DNS, SSH, SMTP, gRPC |
| **6** | Presentation | ^ | TLS/SSL, JSON, gzip compression |
| **5** | Session | ^ | Sockets, RPC sessions |
| **4** | Transport | **Transport Layer** | TCP (Reliable), UDP (Fast, Datagram) |
| **3** | Network | **Internet Layer** | IPv4, IPv6, ICMP, IPsec, BGP |
| **2** | Data Link | **Network Access Layer** | Ethernet, MAC Addressing, VLANs (802.1Q) |
| **1** | Physical | ^ | Fiber optic, Cat6 copper, Wi-Fi |

---

## 8. TCP vs UDP Protocol Comparison

### Technical Comparison Matrix

| Attribute | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :--- | :--- | :--- |
| **Connection Model** | **Connection-Oriented** (3-Way Handshake) | **Connectionless** (Fire-and-forget) |
| **Reliability** | Guaranteed delivery (Acknowledgments & Retransmissions)| Best-effort (Packets can drop or arrive out-of-order) |
| **Ordering** | Guarantees ordered byte-stream delivery | No sequence ordering guaranteed |
| **Flow & Congestion Control**| Yes (Sliding window, Slow start algorithms) | Zero flow or congestion control |
| **Overhead** | Heavier header (20-60 bytes) | Minimal header (8 bytes) |
| **DevOps Use Cases** | Web APIs (HTTP/HTTPS), SSH, Git, Database connections | Real-time audio/video, DNS queries, Syslog, SNMP |

---

## 9. TCP 3-Way Handshake & Connection Teardown

### Handshake Sequence (Connection Establishment)
```text
Client                                Server
  │                                     │
  │─── 1. SYN (Seq = X) ───────────────►│  Client initiates connection
  │                                     │
  │◄── 2. SYN-ACK (Seq = Y, Ack = X+1) ─│  Server acknowledges & synchronizes
  │                                     │
  │─── 3. ACK (Ack = Y+1) ─────────────►│  Client acknowledges
  │                                     │
[ESTABLISHED]                      [ESTABLISHED]
  │                                     │
  │◄════ Data Transfer (Bidirectional) ═►│
```

### 4-Way Handshake (Connection Teardown)
* **Step 1: FIN**: Client initiates closure when work completes.
* **Step 2: ACK**: Server acknowledges receipt of FIN.
* **Step 3: FIN**: Server completes final tasks and sends its own FIN to client.
* **Step 4: ACK**: Client acknowledges; enters `TIME_WAIT` state (2 * MSL) to ensure server received ACK before socket closes completely.

---

## 10. DNS Resolution Lifecycle & IP Subnetting (CIDR)

### The 8-Step Recursive DNS Resolution Workflow
```text
Browser ──► Local /etc/hosts ──► DNS Resolver (ISP / 8.8.8.8)
                                        │
             ┌──────────────────────────┼─────────────────────────┐
             ▼                          ▼                         ▼
      1. Root Server (.)         2. TLD Server (.com)     3. Authoritative Nameserver
      ("Ask .com TLD")           ("Ask Route53 NS")       ("api.vault.com = 54.12.34.56")
```

### CIDR Subnetting Reference

| CIDR Mask | Subnet Mask | Total IPs | Usable IPs (AWS VPC) | Common Use Case |
| :--- | :--- | :--- | :--- | :--- |
| `/16` | `255.255.0.0` | 65,536 | 65,531 | Standard VPC network boundary |
| `/20` | `255.255.240.0`| 4,096 | 4,091 | Large production subnet |
| `/24` | `255.255.255.0`| 256 | 251 | Standard application tier subnet |
| `/28` | `255.255.255.240`| 16 | 11 | Private database / internal proxy subnet |
| `/32` | `255.255.255.255`| 1 | 1 | Single specific host IP |

* *AWS Reserved IPs*: In every AWS subnet, **5 IP addresses** are automatically reserved by AWS (Network address `.0`, VPC Router `.1`, DNS Server `.2`, Future use `.3`, Broadcast `.255`).

---

## 11. Network Troubleshooting CLI Toolchain (`ss`, `curl`, `dig`, `tcpdump`)

```bash
# 1. Socket & Port Inspection (Modern replacement for netstat)
ss -tulnp                     # Show listening TCP & UDP ports with process names
ss -tuna                      # Show all established and active socket connections

# 2. HTTP & API Diagnostics
curl -Iv https://api.vault.com                 # Inspect TLS handshake, certificates, and HTTP headers
curl -w "@curl-format.txt" -o /dev/null -s ... # Measure DNS lookup, TCP connect, and TTFB latency

# 3. DNS Lookup & Querying
dig +trace api.vault.com                       # Full recursive trace from Root server to Authoritative NS
nslookup api.vault.com 8.8.8.8                 # Query specific public DNS server directly

# 4. Routing & Connectivity
ping -c 4 8.8.8.8                             # Test ICMP echo packet loss
traceroute -T -p 443 api.vault.com             # Trace network path using TCP SYN on port 443

# 5. Packet Capture
sudo tcpdump -i eth0 -n "port 80 or port 443" -c 50  # Capture 50 web packets on eth0 interface
```

---

## 12. Senior DevOps Interview Q&A

### Q1: What happens when you type `https://www.google.com` in your browser and press Enter?
* **DNS Resolution**: Browser checks local cache, OS cache, `/etc/hosts`, then queries recursive resolver to resolve IP address.
* **TCP Handshake**: Client initiates TCP 3-way handshake (SYN, SYN-ACK, ACK) on port 443.
* **TLS Handshake**: Client and server negotiate cipher suites, authenticate server X.509 certificate, exchange key material (Diffie-Hellman), and establish encrypted symmetric session.
* **HTTP Request**: Browser transmits `GET / HTTP/2` request.
* **Server Processing**: Reverse proxy (Nginx/ALB) terminates TLS, load balances request to backend microservice, which fetches data and returns HTTP 200 payload.
* **Browser Rendering**: Browser receives HTML/CSS/JS, constructs DOM and CSSOM trees, and paints the webpage.

### Q2: What causes high load average when CPU usage is near 0%?
* Load average counts processes that are in **Runnable state (`R`)** OR in **Uninterruptible Sleep (`D`)**.
* If CPU % is low but load average is high, processes are stuck in **Uninterruptible Sleep (`D`)**, almost always waiting on **disk I/O bottlenecks**, hanging NFS network mounts, or dead hardware storage.
* *Fix*: Run `iostat -xz 1` or `vmstat 1` to confirm I/O wait (`wa`), and `ps aux | awk '$8 ~ /D/'` to identify the stuck processes.

### Q3: How do you identify which process is consuming port 80?
* Execute `sudo ss -tulnp | grep :80` or `sudo lsof -i :80`.
* The output reveals the exact Process Name and Process ID (`PID`).
