# 🐧 Linux Systems Administration & Networking: The Definitive Master Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Linux Kernel Architecture, Filesystem Hierarchy Standard (FHS), User & Privilege Management, POSIX Permissions & Special Bits (SUID, SGID, Sticky), Process Lifecycle & Signals, `systemd` Administration (`enable` vs `start`), Memory & Disk Diagnostics, Text Processing (`grep`, `awk`, `sed`), OSI & TCP/IP Protocols, and Network Troubleshooting Toolchains (`ss`, `curl`, `dig`, `tcpdump`).

---

## 📑 Table of Contents
- [1. Linux Kernel Architecture & Filesystem Hierarchy (FHS)](#1-linux-kernel-architecture--filesystem-hierarchy-fhs)
- [2. User, Group, & Sudoers Administration](#2-user-group--sudoers-administration)
- [3. File Permissions, Ownership, & Special Bits](#3-file-permissions-ownership--special-bits)
- [4. Process Lifecycle, Signals, & `systemd` Services](#4-process-lifecycle-signals--systemd-services)
- [5. System Resource Diagnostics (CPU, Memory, Disk, I/O)](#5-system-resource-diagnostics-cpu-memory-disk-io)
- [6. File Location Utilities: `which` vs `whereis` vs `locate` vs `find`](#6-file-location-utilities-which-vs-whereis-vs-locate-vs-find)
- [7. DevOps Text Processing Power Tools (`grep`, `awk`, `sed`)](#7-devops-text-processing-power-tools-grep-awk-sed)
- [8. OSI 7-Layer vs TCP/IP 4-Layer Architecture](#8-osi-7-layer-vs-tcpip-4-layer-architecture)
- [9. TCP 3-Way Handshake & Connection Teardown](#9-tcp-3-way-handshake--connection-teardown)
- [10. Network Troubleshooting CLI Toolchain (`ss`, `curl`, `dig`, `tcpdump`)](#10-network-troubleshooting-cli-toolchain-ss-curl-dig-tcpdump)
- [11. Senior DevOps Interview Q&A](#11-senior-devops-interview-qa)

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
* `/etc` — System-wide configuration files (`/etc/passwd`, `/etc/hosts`, `/etc/ssh/sshd_config`, `/etc/fstab`).
* `/var` — Variable dynamic data (`/var/log` for system logs, `/var/lib/docker` for container layers).
* `/proc` — Virtual pseudo-filesystem exposing real-time kernel and process memory state (e.g., `/proc/cpuinfo`, `/proc/meminfo`).
* `/sys` — Virtual pseudo-filesystem exposing hardware device parameters and kernel tuning variables.
* `/tmp` — Ephemeral temporary files; flushed on reboot.
* `/dev` — Hardware and pseudo-device nodes (`/dev/sda`, `/dev/null`, `/dev/random`).

---

## 2. User, Group, & Sudoers Administration

* **User Management Commands**:
  * `useradd -m -s /bin/bash appuser` — Create user with home directory and default bash shell.
  * `usermod -aG docker,sudo appuser` — Append user to `docker` and `sudo` groups without dropping existing groups (`-a` is critical).
  * `userdel -r appuser` — Delete user and purge home directory.
* **The `/etc/sudoers` Configuration**:
  * Always edit safely using `visudo` to prevent syntax lockouts.
  * Grant passwordless execution for automated deployment users:
    ```text
    jenkins ALL=(ALL) NOPASSWD: ALL
    ```

---

## 3. File Permissions, Ownership, & Special Bits

### Standard POSIX Permissions
Permissions are divided into three tiers: **Owner (User)**, **Group**, and **Others**.

```text
-  rwx  r-x  r--
│  ───  ───  ───
│   │    │    └── Others: Read (4)
│   │    └─────── Group: Read (4) + Execute (1) = 5
│   └──────────── Owner: Read (4) + Write (2) + Execute (1) = 7
└──────────────── File type: '-' (regular file), 'd' (directory)
```

* **Numeric Translation**: `chmod 754 script.sh`.
* **Recursive Ownership**: `chown -R appuser:appgroup /var/www/app`.

### Special Permission Bits
* **SUID (Set User ID - Numeric 4000)**:
  * Executes binary with the permissions of the file owner rather than the calling user (e.g., `/usr/bin/passwd`).
  * Syntax: `chmod u+s /path/to/binary`.
* **SGID (Set Group ID - Numeric 2000)**:
  * On directories, any newly created files inherit the parent directory's group ownership rather than the creator's group.
  * Syntax: `chmod g+s /shared/directory`.
* **Sticky Bit (Numeric 1000)**:
  * Prevents users from deleting or renaming files owned by others within shared writable directories (e.g., `/tmp`).
  * Syntax: `chmod +t /tmp`.

---

## 4. Process Lifecycle, Signals, & `systemd` Services

### `systemctl enable` vs `systemctl start` (Critical Difference)
Understanding the difference between enabling and starting services is essential for system reliability:

* **`systemctl start <service>`**:
  * **Immediate Execution**: Spawns and launches the daemon process into memory **right now** for the current session.
  * **No Boot Persistence**: If the server or EC2 instance is rebooted, the service **WILL NOT auto-start**!
* **`systemctl enable <service>`**:
  * **Boot Persistence**: Creates symbolic links inside `/etc/systemd/system/multi-user.target.wants/` pointing to the service unit file.
  * **Guarantees Auto-Start**: Ensures the service launches automatically every time the OS reboots.
  * **Does NOT Launch Immediately**: It does not start the running process right now!
* **Production Recommended Pattern**:
  ```bash
  # Enable auto-start on boot AND start process immediately in one command:
  sudo systemctl enable --now nginx.service
  ```

### Linux Process Termination Signals
* **`SIGHUP (1)`**: Hangup signal. Tells daemon to reload its configuration file without terminating active worker connections.
* **`SIGTERM (15)`**: Graceful termination request. Allows application process to flush buffers, finish in-flight HTTP requests, close database sockets, and exit cleanly.
* **`SIGKILL (9)`**: Forcible uncatchable kernel kill. Kernel terminates process immediately without buffer cleanup. Use only when process is unresponsive to `SIGTERM`.

### Custom `systemd` Unit Blueprint (`/etc/systemd/system/taskflow.service`)
```ini
[Unit]
Description=TaskFlow Production API Service
After=network.target postgresql.service

[Service]
Type=simple
User=appuser
Group=appuser
WorkingDirectory=/var/www/taskflow/backend
ExecStart=/usr/bin/node dist/index.js
Restart=always
RestartSec=5s
Environment=NODE_ENV=production PORT=5000
LimitNOFILE=65536

[Install]
WantedBy=multi-user.target
```

---

## 5. System Resource Diagnostics (CPU, Memory, Disk, I/O)

* **`uptime`**: View system running time and Load Average over 1, 5, and 15 minutes.
* **`top` / `htop`**: Real-time process and CPU core monitoring.
* **`free -h`**: Human-readable memory usage (Total, Used, Free, Buffers/Cache).
* **`df -h`**: Disk partition usage and mount points.
* **`du -sh * | sort -hr | head -n 10`**: Find top 10 largest directories eating storage.
* **`vmstat 1 5`**: Virtual memory, process paging, CPU context switches.
* **`iostat -xz 1 5`**: Deep disk I/O diagnostics; shows `%util` (storage bottleneck).

---

## 6. File Location Utilities: `which` vs `whereis` vs `locate` vs `find`

| Command | How It Works | Speed | Best Use Case |
| :--- | :--- | :--- | :--- |
| **`which`** | Searches directories in `$PATH` environment variable | Instant | Locating the active executable binary (e.g., `which python3`) |
| **`whereis`** | Searches standard system binary, source, and manpage directories | Instant | Finding binary, source, and documentation paths (e.g., `whereis maven`) |
| **`locate`** | Queries a pre-built local database index (`/var/lib/mlocate/mlocate.db`) | Very Fast | Fast file lookup; database updated via `updatedb` |
| **`find`** | Real-time recursive filesystem walk | Slowest | Dynamic complex queries by name, modification time, size, or permissions |

```bash
# Production find examples
find /var/log -type f -name "*.log" -mtime +30 -delete # Delete logs older than 30 days
find / -perm -4000 -type f 2>/dev/null                # Audit all SUID binaries on system
```

---

## 7. DevOps Text Processing Power Tools (`grep`, `awk`, `sed`)

### 1. `grep` (Search Pattern Filtering)
* `grep -ri "error" /var/log/` — Case-insensitive recursive search.
* `grep -v "^#" /etc/nginx/nginx.conf` — Invert match (strip comments).
* `grep -E "50[0-4]" access.log` — Extended regex for HTTP 500-504 errors.

### 2. `awk` (Column Extraction & Aggregation)
* `awk '{print $1, $9}' access.log` — Extract IP address ($1) and HTTP status code ($9).
* `awk '{sum += $10} END {print sum/1024/1024 " MB"}' access.log` — Calculate total bandwidth.
* Top 10 client IP addresses hitting server:
  ```bash
  awk '{print $1}' access.log | sort | uniq -c | sort -nr | head -n 10
  ```

### 3. `sed` (Stream Editor & In-Place Replacement)
* `sed -i 's/DEBUG=True/DEBUG=False/g' config.env` — Replace text in-place.
* `sed -i '/^#/d' /etc/hosts` — Delete all comment lines starting with `#`.

---

## 8. OSI 7-Layer vs TCP/IP 4-Layer Architecture

```text
┌──────────────────────┬──────────────────────┬─────────────────────────────────────┐
│ OSI 7-Layer Model    │ TCP/IP 4-Layer Model │ Common Protocols & Hardware         │
├──────────────────────┼──────────────────────┼─────────────────────────────────────┤
│ 7. Application       │                      │ HTTP, HTTPS, DNS, SSH, SMTP         │
│ 6. Presentation      │ Application Layer    │ SSL/TLS, JSON, Base64               │
│ 5. Session           │                      │ Sockets, RPC, Sessions              │
├──────────────────────┼──────────────────────┼─────────────────────────────────────┤
│ 4. Transport         │ Transport Layer      │ TCP, UDP (Ports)                    │
├──────────────────────┼──────────────────────┼─────────────────────────────────────┤
│ 3. Network           │ Internet Layer       │ IP (IPv4/IPv6), ICMP, Routers       │
├──────────────────────┼──────────────────────┼─────────────────────────────────────┤
│ 2. Data Link         │                      │ Ethernet, MAC Addresses, Switches   │
│ 1. Physical          │ Network Access Layer │ Fiber, Copper Cables, NICs          │
└──────────────────────┴──────────────────────┴─────────────────────────────────────┘
```

---

## 9. TCP 3-Way Handshake & Connection Teardown

### Connection Establishment (3-Way Handshake)
```text
Client                                  Server
  │                 SYN                   │
  ├──────────────────────────────────────►│ Client sends initial sequence number
  │                                       │
  │               SYN-ACK                 │
  │◄──────────────────────────────────────┤ Server acknowledges and sends its SEQ
  │                                       │
  │                 ACK                   │
  ├──────────────────────────────────────►│ Connection ESTABLISHED; data flows
```

### Connection Teardown (4-Way Handshake)
* Initiating side sends `FIN` $	o$ Receiver sends `ACK`.
* Receiver sends its own `FIN` $	o$ Initiator sends `ACK` and enters `TIME_WAIT` state (typically 60 seconds) to ensure final ACK delivery before socket closure.

---

## 10. Network Troubleshooting CLI Toolchain (`ss`, `curl`, `dig`, `tcpdump`)

* **`ss -tulpn`**: Inspect all listening TCP/UDP ports and associated process names (modern replacement for `netstat`).
* **`curl -Iv https://app.example.com`**: Inspect HTTP status codes, headers, and SSL certificates with verbose debug output.
* **`dig +trace api.example.com`**: Trace complete recursive DNS resolution from root servers down to authoritative nameservers.
* **`tcpdump -i eth0 port 80 -nn -s0 -w capture.pcap`**: Capture raw network packet traces for Wireshark inspection.

---

## 11. Senior DevOps Interview Q&A

### Q1: What is the difference between `systemctl enable` and `systemctl start`?
* `systemctl start` launches the process immediately into memory, but will NOT start it after a system reboot.
* `systemctl enable` creates systemd symlinks to guarantee the service auto-starts on every system boot, but does not launch the service immediately.
* Best practice is `systemctl enable --now <service>` to do both at once.

### Q2: How do you identify which process is listening on port 8080?
* Execute `sudo ss -tulpn | grep :8080` or `sudo lsof -i :8080`.
* Both commands return the process name, PID, and user executing the daemon.
