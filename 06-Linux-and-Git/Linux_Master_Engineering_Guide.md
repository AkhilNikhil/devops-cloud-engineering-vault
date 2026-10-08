# 🐧 Linux Systems Administration: The Definitive Master Engineering Guide

> **Authoritative Production Reference & Senior Technical Interview Playbook**  
> Covers OS Kernel Architecture, Process Hierarchy, File Permissions, Modern Networking (`ss`/`ip`), systemd Service Governance, Production Shell Scripting (`set -euo pipefail`), and System Triage.

---

## 📑 Table of Contents
1. [Linux Operating System Architecture](#1-linux-operating-system-architecture)
2. [Process Management & Lifecycle States](#2-process-management--lifecycle-states)
3. [File Hierarchy, Permissions & Special Bits](#3-file-hierarchy-permissions--special-bits)
4. [Modern System Administration & systemd](#4-modern-system-administration--systemd)
5. [Modern Networking & Diagnostic Tooling](#5-modern-networking--diagnostic-tooling)
6. [System Performance Diagnosis (CPU, RAM, Disk I/O)](#6-system-performance-diagnosis-cpu-ram-disk-io)
7. [Production Bash Shell Scripting Blueprint](#7-production-bash-shell-scripting-blueprint)
8. [Production Troubleshooting Playbook](#8-production-troubleshooting-playbook)
9. [Senior Linux Systems Interview Q&A](#9-senior-linux-systems-interview-qa)

---

## 1. Linux Operating System Architecture

The Linux architecture operates in two CPU privilege rings:
* **Kernel Space (Ring 0):** Unrestricted access to hardware, CPU registers, and physical RAM. Manages device drivers, virtual memory management, interrupt handling, and process scheduling.
* **User Space (Ring 3):** Isolated application space (Nginx, PostgreSQL, Python, Bash). Can only interact with hardware via **System Calls (`syscalls`)** such as `fork()`, `execve()`, `read()`, `write()`, `open()`.

---

## 2. Process Management & Lifecycle States

### 2.1 Process Creation Mechanism
1. **`fork()`:** Clones the parent process, creating a child process with an identical memory space (leveraging Copy-on-Write).
2. **`exec()` / `execve()`:** Overwrites the child process address space with a new program executable.

### 2.2 Zombie vs. Orphan Processes
* **Zombie Process (`<defunct>` / State `Z`):**
  * A process that has finished execution (called `exit()`), but its parent process has not yet read its exit status via `wait()` or `waitpid()`.
  * *Resource Impact:* Consumes **zero CPU and zero RAM**, but occupies an entry in the system **Process Table (`PID`)**.
  * *Remediation:* You cannot `kill -9` a zombie (it is already dead). You must restart or terminate the parent process.
* **Orphan Process:**
  * A running child process whose parent process died or terminated before it.
  * *Resolution:* Automatically adopted by `PID 1` (`systemd`), which regularly reaps orphaned child processes when they terminate.

### 2.3 Process Signals
* **`SIGTERM` (Signal 15 - Graceful Shutdown):** Polite request to terminate. Allows the process to close database connections, write buffers to disk, and clean up temporary lockfiles.
* **`SIGKILL` (Signal 9 - Unconditional Kill):** Handled directly by the Linux kernel. The process cannot catch, block, or ignore it; terminated instantly.
* **`SIGHUP` (Signal 1 - Hangup):** Instructs daemons (Nginx, Apache) to reload configuration files without dropping active connections.

---

## 3. File Hierarchy, Permissions & Special Bits

### 3.1 Standard Octal Permissions
Every file and directory has 3 permission categories: **Owner (User)**, **Group**, and **Others**:
* `r` (Read) = 4
* `w` (Write) = 2
* `x` (Execute) = 1

| Octal | Meaning | Common Usage |
| :--- | :--- | :--- |
| **`755`** | `rwxr-xr-x` (Owner full; Group/Others read+execute) | Executable binaries (`/usr/bin`), web public directories |
| **`644`** | `rw-r--r--` (Owner read+write; Group/Others read) | Standard files, config files |
| **`600`** | `rw-------` (Owner read+write; Group/Others none) | Private SSH keys (`~/.ssh/id_rsa`), database secrets |
| **`700`** | `rwx------` (Owner full; Group/Others none) | `~/.ssh` directory, root home directory |

### 3.2 Special Permission Bits
1. **SUID (Set User ID - Octal `4000`):** File executes with the permissions of the file owner rather than the user running it (e.g. `/usr/bin/passwd`).
2. **SGID (Set Group ID - Octal `2000`):** New files created in directory automatically inherit the directory's group ownership.
3. **Sticky Bit (Octal `1000`):** In shared directories (`/tmp`), users can only delete files that they personally own.

---

## 4. Modern System Administration & systemd

`systemd` is the init system (`PID 1`) on all modern distributions (Ubuntu, RHEL, Debian):
```bash
# Service Control
systemctl start <service>
systemctl enable --now <service>   # Enable on system boot and start immediately
systemctl status <service>
systemctl restart <service>

# Log Inspection via journalctl
journalctl -u <service> -f         # Stream live logs for a specific service
journalctl -u <service> -n 100     # View last 100 log lines
journalctl --vacuum-time=7d        # Purge journal logs older than 7 days
```

---

## 5. Modern Networking & Diagnostic Tooling

*Note: Legacy tools (`netstat`, `ifconfig`, `arp`) are officially deprecated. Use the modern **iproute2** suite:*

| Task | Modern Command (Industry Standard) | Deprecated Legacy Command |
| :--- | :--- | :--- |
| **Inspect Open Ports & Sockets** | `ss -tulnp` | `netstat -tulnp` |
| **View Network Interfaces & IPs** | `ip addr show` (or `ip a`) | `ifconfig` |
| **View Routing Table** | `ip route show` (or `ip r`) | `route -n` or `netstat -r` |
| **Trace Network Route** | `traceroute` or `mtr -rw <ip>` | `traceroute` |
| **Test Port Reachability** | `nc -zv <host> <port>` or `curl -Iv telnet://...` | `telnet <host> <port>` |
| **DNS Resolution Query** | `dig <domain> +short` or `nslookup` | `host` |

---

## 6. System Performance Diagnosis (CPU, RAM, Disk I/O)

When triaging production performance degradation, follow the **USE Method (Utilization, Saturation, Errors)**:

### 6.1 CPU & Load Average
```bash
uptime
# Output: load average: 4.10, 2.50, 1.20 (1-min, 5-min, 15-min)
```
* **Rule of Thumb:** A load average equal to your number of CPU cores indicates 100% capacity. If load average > core count, processes are queueing up waiting for CPU time.

### 6.2 Memory Analysis
```bash
free -h
# Look at the 'available' column, NOT the 'free' column!
# Linux aggressively uses unused RAM for file page caches ('buff/cache').
# Available memory represents RAM that can immediately be claimed by applications.
```

### 6.3 Disk I/O Bottlenecks
```bash
iostat -xz 1 5
# Look at '%util': If %util > 90%, the disk hardware is saturated and causing application I/O wait latency.
df -h          # Check disk space usage per filesystem
df -i          # Check INODE usage (a disk can be 100% full due to running out of inodes even with free disk space!)
```

---

## 7. Production Bash Shell Scripting Blueprint

Production shell scripts must enforce **Bash Strict Mode**:

```bash
#!/usr/bin/env bash
# ==============================================================================
# BASH STRICT MODE:
# -e: Exit immediately if any command returns a non-zero status
# -u: Treat unset variables as an error and exit immediately
# -o pipefail: Pipeline fails if ANY sub-command fails (not just the last one)
# ==============================================================================
set -euo pipefail

readonly SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
readonly LOG_FILE="/var/log/app_deploy.log"

log() {
    local -r message="$1"
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] ${message}" | tee -a "${LOG_FILE}"
}

cleanup() {
    log "Performing cleanup tasks..."
    rm -rf /tmp/scratch_data_* 2>/dev/null || true
}

# Trap unexpected errors and script exits
trap cleanup EXIT
trap 'log "ERROR: Script failed at line ${LINENO} exiting."; exit 1' ERR

main() {
    log "Starting automated system health validation..."
    
    local -r DISK_USAGE=$(df / | awk 'NR==2 {print $5}' | tr -d '%')
    if [[ "${DISK_USAGE}" -gt 90 ]]; then
        log "CRITICAL: Root disk usage is above 90% (${DISK_USAGE}%)"
        exit 1
    fi
    
    log "System health verification passed."
}

main "$@"
```

---

## 8. Production Troubleshooting Playbook

### Scenario 1: Disk is 100% Full (`No space left on device`), but `du` doesn't show large files
* **Root Cause:** A deleted log file is still being held open by a running process (e.g. Nginx or Java). The directory entry is removed, but disk blocks are not freed until the process closes the file handle.
* **Resolution:**
  ```bash
  # Identify processes holding deleted files
  lsof +L1
  # Restart the holding service or truncate via /proc/<PID>/fd/<FD>
  systemctl restart <holding_service>
  ```

### Scenario 2: High CPU Wait (`%wa` in `top`)
* **Root Cause:** CPU is idling because it is waiting for slow disk read/writes or network storage (NFS/EBS) to return data.
* **Resolution:** Run `iotop -o` to pinpoint the specific process causing excessive disk operations.

---

## 9. Senior Linux Systems Interview Q&A

### Q1. What happens when you type `ls -l` in a terminal?
1. **Shell parsing:** Shell reads the line, parses tokens, and checks for aliases.
2. **Path lookup:** Searches the `$PATH` directories to find `/bin/ls`.
3. **System call execution:** Shell calls `fork()` to create a child process, then `execve("/bin/ls", ["ls", "-l"], ...)`.
4. **Filesystem reading:** `ls` issues `opendir()` and `readdir()` syscalls to read directory entries and inodes.
5. **Metadata fetching:** Calls `stat()` on each file to retrieve size, permissions, owner, and modification timestamps.
6. **Output rendering:** Formats and outputs text to stdout via `write()` syscall, which terminal renders.
