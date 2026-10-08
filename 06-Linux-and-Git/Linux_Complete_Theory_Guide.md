# The Complete Linux Guide (Beginner to DevOps-Ready)

This guide explains **how Linux actually works underneath**, not just which commands to type. If you understand the *why*, the commands become obvious. Written so that even someone who has never touched a terminal can follow along.

---

## PART 1: What Linux Actually Is

### The Big Picture
When your computer turns on, three layers work together:

1. **Kernel** — the core program that talks directly to your hardware (CPU, memory, disk, network card). It decides which program gets CPU time, manages memory, and controls devices. Nothing happens on the machine without going through the kernel.
2. **Shell** — a program that reads what you type, interprets it, and asks the kernel to do it. Bash is the most common shell. When you type `ls`, the shell is what figures out "oh, you want to list files" and asks the kernel to fetch that directory info.
3. **Terminal** — the window/application you're typing into. It's just a text box that sends your keystrokes to the shell and shows you the shell's response. The terminal itself does no "thinking" — it's just a display.

**Flow:** You type in the Terminal → Terminal sends it to the Shell → Shell interprets it and asks the Kernel → Kernel talks to hardware → result flows back up the same chain to your screen.

### Why This Matters
Every single thing you do in Linux — creating a file, killing a process, checking disk space — is really just "ask the shell to ask the kernel to do something with hardware or the filesystem." Once this clicks, Linux stops feeling like magic spells and starts feeling like logical cause-and-effect.

---

## PART 2: The Filesystem — Everything Is a File, Everything Has a Place

### The Tree Structure
Linux organizes everything as one giant tree starting at `/` (root — not to be confused with the root *user*). Every file and folder is a branch of this tree. There's no separate "C:\" or "D:\" like Windows — everything, including other disks, gets *mounted* somewhere inside this one tree.

Key locations you'll constantly interact with:
- `/` — the top of everything
- `/home/username` or `/root` — your personal space
- `/etc` — configuration files for almost everything on the system
- `/var/log` — where most logs live
- `/tmp` — temporary files, often cleared on reboot
- `/usr/bin`, `/usr/sbin` — where most installed programs actually live

### Navigating It
- `pwd` — "where am I right now" (print working directory)
- `cd` — change your current location
- `ls` — see what's in your current location

The shell always has a concept of "current directory" — a starting point every relative path is measured from. `cd ..` means "go up one level from wherever I am now." `cd ~` always jumps straight home regardless of where you are.

### Creating, Moving, Copying, Deleting
- `touch` creates an empty file (or updates its timestamp if it exists)
- `mkdir` creates a folder
- `cp` copies (needs `-r` for folders, since a folder isn't a single item — it's a tree of items)
- `mv` moves OR renames — Linux treats renaming as "moving to a new name in the same place," which is why one command does both
- `rm` deletes — deleting a folder needs `-r` (recursive, go through every file inside) and often `-f` (force, don't ask for confirmation on each one)

**Why `-r` matters:** A single `rm file.txt` deletes one item. But a folder isn't one item — it's a container possibly holding thousands of files and subfolders. Without `-r`, Linux refuses because it doesn't know if you meant to destroy everything inside.

### Reading File Content
- `cat` — dumps the whole file to screen at once (fine for small files)
- `head` / `tail` — show just the beginning or end (useful for huge files — you don't want to dump a million-line log)
- `tail -f` — "follow" mode, keeps watching the file and shows new lines as they get added, live. This is how you watch a log file in real time while something is happening.
- `less` — opens a file page by page, lets you scroll without loading the whole thing at once
- `>` — redirect output INTO a file, **overwriting** whatever was there
- `>>` — redirect output INTO a file, **appending** to the end, keeping existing content

**The core idea of redirection:** Normally, a command's output goes to your screen. `>` and `>>` reroute that output into a file instead. This is how you build log files, save command results, and construct config files from scripts.

---

## PART 3: Finding Things — `find` vs `grep`

These get confused constantly, so lock this in clearly:

- **`find` searches for FILES** — based on name, type, size, date. It answers "where is this file?"
- **`grep` searches INSIDE files** — for text/patterns. It answers "which files/lines contain this word?"

```
find . -name "*.yaml"        → finds files ending in .yaml
grep "ERROR" app.log          → finds lines containing the word ERROR inside app.log
grep -r "ERROR" .             → finds ERROR inside every file in every subfolder
```

**Why both exist:** In real troubleshooting, you often need both in sequence — first `find` to locate the right config/log files, then `grep` to search inside them for the specific problem.

Useful `grep` flags to remember by what they DO, not just letter:
- `-i` = ignore case (so ERROR/error/Error all match)
- `-n` = show line numbers (so you know exactly where to look)
- `-v` = invert — show everything that DOESN'T match
- `-c` = just count matches, don't show them
- `-r` = recursive, search every file in every subfolder

---

## PART 4: Permissions — Who Can Do What

### The Three Groups, Three Actions
Every file has an **owner**, a **group**, and everyone else (**others**). Each of those three can independently have:
- **r**ead
- **w**rite
- e**x**ecute

So a permission string like `rwxr-xr--` reads as: owner can do everything, group can read+execute, others can only read.

### Why Numbers (750, 644, etc.)
Instead of typing symbols, Linux lets you use numbers because each permission has a fixed value:
- read = 4
- write = 2
- execute = 1

Add them per group. `rwx` = 4+2+1 = **7**. `r-x` = 4+1 = **5**. `r--` = just **4**. `---` = **0**.

So `750` means: owner=7(rwx), group=5(r-x), others=0(nothing). This is faster to type than symbols once you internalize the math — you're not memorizing "750 means X," you're just adding numbers.

### Real Patterns You'll Actually Use
- `755` — scripts and programs (owner full control, everyone else can run it but not edit it)
- `644` — regular config/text files (owner can edit, everyone else can only read)
- `600` — secrets, private keys, passwords (ONLY the owner can even look at it)
- `777` — everyone can do everything — almost always a security mistake in production

**Why `chmod +x` alone works too:** `chmod +x file` just *adds* execute permission on top of whatever's already there, without touching read/write. It's a shortcut when you don't want to recalculate the whole numeric value.

### Ownership
Permissions only matter in relation to WHO you are. `chown` changes who owns a file. `chgrp` changes which group owns it. This is why a script can exist with `755` permissions but you *still* get "permission denied" — if you're not the owner and not in the right group, you fall into the "others" category, and maybe others only have `r--`.

---

## PART 5: Users, Groups, and the Permission System Behind Them

### How Linux Identifies "Who You Are"
Every user has a UID (user ID number) and belongs to at least one group (GID). This information lives in two files:
- `/etc/passwd` — identity: username, UID, GID, home directory, login shell
- `/etc/shadow` — the actual password hash, plus aging rules (when it expires, etc.)

The password is deliberately kept in a *separate* file (`shadow`) from the identity file (`passwd`) — `passwd` is world-readable (lots of programs need to check "does this username exist"), but the password hash itself must stay hidden, so it lives in a file only root can read.

### Creating Users, The Right Way
`useradd` is bare-bones by default — it does NOT automatically create a home directory or set a usable password. You explicitly ask for both:
```
useradd -m -G sudo ravi     → creates ravi, makes home dir, adds to sudo group
passwd ravi                  → sets an actual password (without this, login is blocked)
```

### The Most Dangerous Typo in Linux Administration
```
usermod -aG docker ravi     → APPENDS ravi to the docker group, keeps his other groups
usermod -G docker ravi      → REPLACES ALL of ravi's groups with just docker
```
One letter (`a`) is the entire difference between "add a new permission" and "silently strip away everything he already had." This single mistake has caused real production outages — someone loses sudo access because a well-meaning teammate ran the wrong version while trying to add them to an unrelated group.

### Switching Identity vs Just Moving
`cd /home/ravi` only changes your *location* — you're still logged in as yourself. `su - ravi` actually swaps your entire identity — new UID, new home, new environment, as if you logged in fresh as ravi. This is a common beginner confusion: standing inside someone's folder does not make you that person.

### Sudo — Controlled Superpowers
Being root means "no restrictions at all" — dangerous to use casually. Instead, regular users are granted the *ability to temporarily become root for specific commands* via `sudo`, controlled by:
- Group membership (being in the `sudo` group grants broad access)
- Specific rules in `/etc/sudoers` (granular, e.g., "this user can only restart this one service, no password needed")

`/etc/sudoers` should **never** be edited directly with a normal text editor — a single syntax mistake there can lock out `sudo` access for literally every user on the machine, including yourself. `visudo` exists specifically to check the file's syntax *before* saving, refusing to let you save something broken.

### Locking vs Deleting
When someone needs to be offboarded but you might need to reverse the decision or preserve records, you don't delete the account — you **lock** it (`passwd -l`), which just tampers with the stored password hash so nothing can match it anymore. The account, its data, and its history all stay intact. Deleting (`userdel -r`) is the final, irreversible step, done only once you're certain.

### Service Accounts
Not every account is for a human. Automated tools (backup scripts, monitoring agents, CI/CD bots) need their own account to own files and run scheduled tasks — but they should never be usable as an interactive login, because if their credentials ever leak, you don't want an attacker getting a real shell. This is done by setting their login shell to `/usr/sbin/nologin`, which immediately rejects any login attempt while still allowing the account to function for background purposes.

---

## PART 6: Processes — What's Actually Running

### What a Process Is
Every running program — your shell, a web server, a background script — is a *process*, identified by a PID (process ID). Processes can spawn other processes (their "children"), which is why you'll see a PPID (parent process ID) too.

### Watching What's Running
- `ps` alone only shows processes tied to *your* terminal session
- `ps aux` or `ps -ef` shows every process on the entire system
- `top` gives a live, constantly refreshing view — essential for watching CPU/memory usage change in real time during an incident

### Stopping a Process
`kill` doesn't literally "kill" by force by default — it sends a *signal*, and the default signal (SIGTERM) is a polite request: "please shut yourself down, clean up if you need to." The process can catch this signal and gracefully close files, finish writes, etc.

`kill -9` sends SIGKILL — this isn't a request, it's an order the kernel itself enforces immediately. The process gets **zero** chance to clean up. If it was mid-write to a file or database, that data can end up corrupted. This is why the correct habit is: always try a normal `kill` first, and only escalate to `-9` if the process is genuinely unresponsive.

### Priority
Every process has a "niceness" value from -20 (most CPU priority, most demanding) to +19 (most polite, steps aside for others). Regular users can only make their *own* processes nicer (raise the number) — never more aggressive — because letting any user hog CPU priority at will would let one user starve everyone else on a shared machine. Only root can assign negative (aggressive) priority.

---

## PART 7: Services — Long-Running Background Programs

### What a "Service" Is
A service is a program meant to run continuously in the background — a web server, a database, an SSH daemon — managed by `systemd`, the modern service manager almost all Linux distributions use.

### Two Completely Separate Questions
This is one of the most commonly misunderstood ideas in all of Linux administration:

- **"Is it running right now?"** → this is *active/inactive* status
- **"Will it start automatically the next time the server boots?"** → this is *enabled/disabled* status

These are **independent settings**. A service can be actively running today but disabled — meaning if the server reboots (a patch, a crash, anything), it will **not** come back on its own, even though it seemed perfectly fine yesterday. This exact scenario — "it was working yesterday, why is it down after the reboot" — is one of the most common real production incidents, and the fix is almost always checking `is-enabled`, not restarting blindly.

### The Commands, By Purpose
```
systemctl status nginx      → is it running? show recent activity
systemctl start/stop        → immediate action, right now
systemctl restart           → stop then start again (brief downtime, connections drop)
systemctl reload            → re-read its config file WITHOUT stopping (zero downtime)
systemctl enable/disable    → controls FUTURE boot behavior only
```

**Why check status before restarting:** Blindly restarting a broken service can mask the real underlying problem (a bad config file will just break again immediately) and wastes time compared to reading the actual error first.

---

## PART 8: Logs — The Record of Everything That Happened

### Two Systems That Coexist
Historically, every program just wrote its own plain text log file somewhere under `/var/log/`. When `systemd` (the modern init/service system) came along, it introduced `journalctl` — a unified, structured, searchable log store covering the kernel, every managed service, and boot events, all queryable from one place. Both systems still exist today because many tools still also write to their traditional flat files even on systemd-based systems.

### Reading the Journal Efficiently
```
journalctl -u nginx          → only nginx's logs, not the whole system's
journalctl -u nginx -f       → follow LIVE as new entries come in
journalctl --since "1 hour ago"   → time-window filtering, jump straight to when something broke
journalctl -p err             → only error-severity-and-above, cut the noise
```

### Kernel-Level vs Everything-Else
`dmesg` shows only kernel/hardware-level messages (boot process, driver issues, memory pressure events) — it's a much lower, more fundamental layer than application logs. If a process mysteriously dies with no application-level error, checking `dmesg` for an "Out of Memory: Killed process" line tells you the *kernel itself* killed it due to memory pressure, which is a completely different problem than an app crashing on its own.

---

## PART 9: Disk Space — Finding and Freeing It

### Two Different Questions, Two Different Tools
- **"Is my disk full?"** → `df -h` (filesystem-level, the big picture, shows overall usage per mounted drive)
- **"What's actually taking up all this space?"** → `du -sh` (directory-level, drills down into specific folders)

You almost always need both in sequence: `df` tells you *that* something's full, `du` tells you *what* is filling it. Combined with `sort` you can rank the worst offenders instantly:
```
du -sh /var/log/* | sort -rh | head -5
```

### The Physical Layer
`lsblk` shows you the actual disks and how they're divided into partitions, and where each partition is *mounted* (attached) into the filesystem tree. A disk isn't usable until it's mounted somewhere — mounting requires both a real device AND a real, existing target directory; missing either gives you a specific, different error message, which itself helps you diagnose what went wrong.

`fdisk -l` safely *lists* partition information. Running `fdisk` on a device *without* `-l` opens an interactive editor capable of destroying all data on that disk if used carelessly — this distinction (list vs. edit mode) matters enormously in production.

---

## PART 10: Networking — How Machines Talk to Each Other

### The Diagnostic Ladder
When something's "not working" over the network, the efficient approach is to check each layer in order, from most basic to most specific:

1. **Is the host reachable at all?** → `ping` (just checks basic connectivity, nothing about a specific service)
2. **Is the specific port/service actually listening?** → `ss -tuln` (a host can be "up" but the particular service on it might not be running)
3. **Does the domain name even resolve correctly?** → `dig` / `nslookup` (DNS translates names like google.com into IP addresses — if this fails, nothing downstream will work regardless of the server's actual health)
4. **Does an actual request succeed?** → `curl` (tests the real application layer, not just "is something listening")

Each layer failing tells you something completely different about *where* the problem is — which is why jumping straight to `curl` without checking the earlier layers can waste time chasing the wrong cause.

### Quick Reference
```
ip a                    → your own machine's network interfaces and IP addresses
ping -c 4 8.8.8.8        → basic reachability test (raw IP, skips DNS)
ss -tuln                 → what ports are listening on this machine
curl -I https://site.com → fetch just the HTTP headers, quick check
dig google.com            → detailed DNS resolution
traceroute google.com     → shows every network hop along the path to a destination
```

---

## PART 11: SSH — Secure Remote Access

### Why Keys Beat Passwords
A password is a secret you type — it can be guessed, phished, leaked, or reused across sites. An SSH key pair works differently: you have a **private key** (which never leaves your machine, ever) and a **public key** (which you can freely hand out). The server, holding only your public key, can verify that whoever's connecting truly possesses the matching private key — without the private key ever being transmitted or exposed anywhere.

### Which Key Goes Where
- **Private key** (`id_rsa`) — stays on YOUR machine only, forever
- **Public key** (`id_rsa.pub`) — copied into the target server's `authorized_keys` file, telling that server "this specific key is allowed to log in as this user"

### Why Permissions Matter Here Specifically
If your private key file were readable by other users on your own machine, anyone with access could steal it and impersonate you on every server that trusts that key. This is why SSH actively **refuses** to use a private key unless its permissions are locked down to `600` (owner read/write only, nobody else).

### Trust on First Connection
The very first time you connect to a new server, SSH shows you that server's fingerprint and asks you to confirm you trust it. Once confirmed, that fingerprint gets saved in `known_hosts`. Every future connection silently re-checks this — if the fingerprint ever suddenly changes (which could mean someone is impersonating that server), SSH refuses to connect quietly and warns you loudly instead.

---

## PART 12: Compression and Archiving

### Two Separate Concerns, Sometimes Combined
"Bundling many files into one" and "shrinking file size" are technically two different operations. `tar` originally only did the first (bundling, literally named after magnetic tape archives) — compression was added later as an optional flag (`-z` for gzip). `zip`, by contrast, was designed from day one to do both together, which is why it never needed a separate compression flag.

### Why `.tar.gz` Dominates in Linux/DevOps
Despite `zip` being more universally recognized (especially by Windows users), `.tar.gz` remains the standard for Linux backups and deployments because it far more reliably preserves Unix-specific file metadata — permissions, ownership, symbolic links — all of which matter enormously when restoring a system or deploying containers.

### Verifying Without Committing
`tar -tzvf archive.tar.gz` lists an archive's entire contents without actually extracting anything — critical for confirming a backup genuinely worked before you trust it enough to delete the original data it's supposed to be protecting.

---

## PART 13: Cron — Scheduling Automation

### What It Does
Cron runs commands automatically on a schedule you define, using five time fields: minute, hour, day-of-month, month, day-of-week. `*` means "any value" in that field.

### The Single Most Important Thing to Understand About Cron
Cron does **not** run your commands inside your normal interactive shell environment. It runs them in a stripped-down, minimal environment — meaning `.bashrc` and `.profile` are never sourced, and `$PATH` is often much shorter than what you're used to. This is the root cause of the single most common cron complaint in the industry: *"this script works perfectly when I run it myself, but silently fails when cron runs it."* The fix is either using absolute paths for everything inside the cron job, or explicitly setting the needed environment variables at the top of the crontab itself.

### Why Output Seems to Vanish
If a cron job produces errors and you never explicitly redirect that output somewhere, it typically gets silently discarded (historically it would be emailed to you, but most modern systems have no mail system configured at all). Always redirect explicitly: `>> /path/to/logfile 2>&1` so you actually capture what happened.

---

## PART 14: Environment Variables

### Shell Variable vs Environment Variable — The Critical Distinction
Setting `NAME=value` creates a variable that exists **only** inside your current shell session — it is invisible to any program or script you launch from that shell, because each of those runs as a completely separate process with its own memory space. `export NAME=value` promotes that variable into the *environment*, which genuinely gets copied down into every child process spawned afterward.

This is exactly why a variable set in your terminal doesn't automatically show up inside a script you run — unless it was exported first.

### Where Persistence Comes From
`export` by itself is entirely in-memory and temporary — closing the terminal wipes it out completely. To make something persist across every future session, you add the `export` line into a startup file that automatically runs every time a new shell begins: `.bashrc` for every new interactive terminal, `.profile` for login sessions specifically (like a fresh SSH connection).

### PATH — How the Shell Finds Commands
`$PATH` is a colon-separated list of directories the shell searches through whenever you type a command name, looking for a matching program. Adding your own tools requires **appending** to this list (`PATH=$PATH:/new/dir`) — never overwriting it entirely (`PATH=/new/dir`), because overwriting instantly breaks the shell's ability to find even basic built-in commands like `ls` or `cat`, whose directories would no longer be in the search list at all.

---

## PART 15: Bash Scripting — Automating Everything Above

### The Core Idea
A script is simply a text file containing a sequence of commands, run top to bottom, exactly as if you'd typed them one by one manually — but reusable, shareable, and automatable. The first line, `#!/bin/bash`, tells the operating system exactly which interpreter should execute the rest of the file.

### Why Execute Permission Is Required
Even a perfectly valid script won't run with `./script.sh` unless it has execute permission (`chmod +x`) — read permission alone lets you *view* the content, but Linux requires an explicit signal that a file is meant to be *run* as a program, not just read as text.

### Variables and the Silent Failure Trap
Bash does **not** throw an error for a mistyped or undefined variable name — it simply substitutes an empty string and continues running. This is one of the most dangerous behaviors in bash, because a typo like `$NAM` instead of `$NAME` produces no visible error at all, just quietly wrong output. Production scripts often add `set -u` at the top specifically to force bash to treat any unset variable as a hard error instead.

### Conditionals — Why Spacing and Quoting Matter
`[` inside an `if` statement isn't special syntax — it's actually a command in disguise (an alias for the `test` command), which is why it needs spaces around it like any other command with arguments: bash needs to see `[`, your condition, and `]` as separate distinct words to parse the line correctly.

Similarly, always quote variables inside conditionals (`[ "$VAR" -gt 5 ]`, not `[ $VAR -gt 5 ]`). If the variable happens to be empty, the unquoted version collapses into a malformed, incomplete condition and throws a syntax error — quoting guarantees it's always treated as one valid argument, even when empty.

### Loops — Choosing the Right One
- `for` loops iterate over a **known** list or range — you already know in advance exactly what you're going through (a fixed set of files, users, or numbers).
- `while` loops repeat based on a **condition** that might not have a predetermined end — useful for polling scenarios like "keep checking every few seconds until a service actually comes up," where you genuinely don't know in advance how many attempts it'll take.

### Exit Codes — How Scripts Communicate Success or Failure
Every command that finishes running produces an exit code: `0` always means success, and any non-zero value signals some kind of failure (the exact non-zero number can vary by command and sometimes carries specific meaning). This code is accessible immediately afterward via `$?`. This matters enormously in real automation — a script's caller (whether that's a human, another script, or a monitoring system) needs a reliable, structured way to know whether the previous step actually worked before deciding what to do next, rather than just assuming everything went fine.

---

## PART 16: How It All Connects — The Real-World Incident Pattern

Almost every production Linux problem eventually reduces to one of these root-cause families, and recognizing the pattern immediately is the difference between a 5-minute fix and a 2-hour investigation:

1. **Permission/ownership mismatch** — the user or process doesn't actually have the rights it needs (wrong owner, wrong group, wrong chmod value)
2. **Environment mismatch** — something works interactively but fails when automated, because cron/scripts run in a different, more minimal environment than your everyday terminal
3. **State assumption mismatch** — assuming something is "on" when it's actually just "on right now but not configured to survive a restart" (the active vs enabled trap)
4. **Silent failure** — bash doesn't error loudly on typos, unredirected output vanishes, exit codes get ignored — Linux often fails quietly unless you specifically ask it to tell you what happened
5. **Case sensitivity and single-character flag differences** — `-a` vs no `-a`, `-c` vs `-C`, `active` vs `Active` — Linux draws a hard, unforgiving line between characters that look almost identical to a human eye

Once you can categorize an incident into one of these five families quickly, you already know roughly where to look — which is exactly what separates confident troubleshooting from random guessing.

---
---

# DEEP DIVE SECTION — Filesystem, Logs, and Processes in Full Detail

The three areas below are the ones you'll touch most often as a DevOps engineer, so they get the fullest treatment: what they are, every important path, real scenarios, and worked examples.

---

## DEEP DIVE 1: The Filesystem — Full Detail

### What "the filesystem" actually means
It's not just "where files are stored." It's the entire organizational structure the kernel uses to track every file, folder, permission, and piece of metadata on every storage device attached to the machine — and Linux presents ALL of it, even multiple physical disks, as one single unified tree starting at `/`. This is fundamentally different from Windows' separate drive letters (C:, D:).

### The Complete Standard Directory Map

| Path | What lives here | Why you'd go there |
|---|---|---|
| `/` | Root of everything | Starting point of the whole tree |
| `/root` | Root user's home directory | Your files if logged in as root |
| `/home/username` | Regular user's home directory | Personal files for a normal user |
| `/etc` | System-wide configuration files | Almost every service's config lives under here (e.g. `/etc/ssh/sshd_config`, `/etc/nginx/nginx.conf`) |
| `/var` | Variable data — changes constantly during normal operation | Parent of logs, spool files, cache |
| `/var/log` | Almost all system and application logs | First place to check during any incident |
| `/var/spool/cron/crontabs` | Where each user's personal crontab actually lives on disk | Backing store for `crontab -e` |
| `/var/www` | Default web server document root (if using Apache/nginx defaults) | Where website files often live |
| `/tmp` | Temporary files, often wiped on reboot | Safe scratch space, never store anything important here |
| `/usr/bin`, `/usr/sbin` | Most installed programs/binaries live here | Where `which <command>` usually points |
| `/usr/local` | Manually installed software, not from the package manager | Custom tools you compiled/installed yourself |
| `/bin`, `/sbin` | Essential core system binaries | Critical low-level commands needed even in recovery mode |
| `/opt` | Optional/third-party software packages | Custom enterprise tools often get installed here |
| `/boot` | Kernel image and bootloader files | Rarely touched unless doing kernel/boot troubleshooting |
| `/dev` | Device files representing hardware | Every disk, terminal, USB device appears as a file here |
| `/proc` | Virtual filesystem representing running processes and kernel info | Not real files on disk — a live window into kernel state |
| `/mnt`, `/media` | Common conventional mount points for extra disks/USB drives | Where you'd typically attach an external filesystem |

### Real Scenario: "Where do I even start looking?"
A developer says "the app config isn't being picked up." Your mental path:
1. Check `/etc/<appname>/` or wherever that app's docs say its config lives
2. Check the app's actual working directory (sometimes apps load from their own install folder, not `/etc`)
3. Check environment variables that might override config file settings (ties to Part 14)

### File Types You'll Encounter
- Regular files (`-` at the start of `ls -l` output)
- Directories (`d`)
- Symbolic links (`l`) — a pointer/shortcut to another file elsewhere, similar to a Windows shortcut. You saw this yourself: `filesystem -> /` in your own home directory was a symlink pointing straight to root.
- Special device files (`b`, `c`) — represent hardware devices, live under `/dev`

### Absolute vs Relative Paths
- **Absolute path**: starts with `/`, always means the exact same location no matter where you currently are (e.g., `/var/log/syslog`)
- **Relative path**: doesn't start with `/`, means "relative to wherever I currently am" (e.g., `syslog` only works if you're already inside `/var/log`)

**Why this matters practically:** Scripts and cron jobs should almost always use absolute paths, because you can never be 100% sure what the "current directory" will be when they actually run — a relative path that works perfectly when you test it manually can silently break when triggered automatically from a different working directory.

### Worked Example: Full Investigation Flow
```
cd /var/log                    # go to the logs directory
ls -la                          # see everything, including hidden files
du -sh *                        # see size of everything in here
grep -r "ERROR" .               # search every file for ERROR
tail -f syslog                  # watch the main log live
```
This exact sequence — navigate, list, measure size, search content, watch live — is the standard investigation pattern used constantly in real troubleshooting, and it directly chains together L2 (navigation), L6 (find), L7 (grep), L14 (disk), and L5 (tail -f).

---

## DEEP DIVE 2: Logs — Full Detail

### The Two Logging Systems, and Exactly Why Both Still Exist
Before `systemd` became the standard init system, every Linux program independently wrote plain text log files, usually somewhere under `/var/log/`, in whatever format that program's author chose. There was no unified structure — you had to know each individual tool's log location and format.

`systemd` introduced `journalctl` as a centralized, structured, binary-indexed logging system that automatically captures kernel messages, boot events, and the stdout/stderr of every service it manages — all searchable through one consistent interface, with built-in filtering by time, service, and severity.

However, many tools (cron, SSH authentication, package managers) STILL also write to their traditional flat files for backward compatibility and because some workflows (like `grep`-ing a plain text file) are simpler than journal queries. This is why a real production system has BOTH systems actively logging in parallel.

### Complete Log Path Reference

| Path | Contains | Real scenario where you'd check this |
|---|---|---|
| `/var/log/syslog` | General system-wide activity (Debian/Ubuntu) | "Something happened on this server around 2pm, what was going on system-wide?" |
| `/var/log/auth.log` | Every login attempt, sudo usage, SSH authentication | "Did someone actually log in? Was there a failed brute-force attempt?" |
| `/var/log/kern.log` | Kernel-specific messages | "Is this a hardware/driver issue, not an application issue?" |
| `/var/log/dpkg.log` | Package install/remove/upgrade history | "Was a package just updated right before this broke?" |
| `/var/log/nginx/access.log` | Every HTTP request nginx received | "What requests is this endpoint actually getting? Is traffic even reaching it?" |
| `/var/log/nginx/error.log` | nginx's own internal errors | "Why did nginx itself fail to serve this request?" |
| `/var/log/cron.log` (some distros) | Cron job execution history | "Did my scheduled job even attempt to run?" |
| `/var/log/boot.log` | Boot-time startup messages | "Why did the server take so long to come up after a restart?" |
| `/var/log/journal/` | Binary backing store for journalctl (never read directly) | Never accessed by path — always go through the `journalctl` command |

### journalctl — Full Command Toolkit
```
journalctl                          # everything, oldest first
journalctl -r                       # everything, newest first (r = reverse)
journalctl -u nginx                 # only nginx's own logs
journalctl -u nginx -f              # follow nginx's logs live, like tail -f
journalctl --since "1 hour ago"     # time-window filter
journalctl --since "09:00" --until "09:30"   # narrow window between two exact times
journalctl -p err                   # only error-severity-and-above
journalctl -p warning               # warning-and-above (includes err too, since warning is a lower bar)
journalctl -b                       # only logs since the last boot
journalctl -k                       # kernel messages only, similar to dmesg but through journalctl
```

### dmesg — What Makes It Different
`dmesg` reads the **kernel ring buffer** — a fixed-size, in-memory log of kernel-level messages (hardware detection at boot, driver errors, memory pressure events). It is NOT a saved file — it resets when the machine reboots, and if too many new messages come in, the oldest ones simply get overwritten (it's a ring buffer, a fixed-size circular log).

**Real scenario where dmesg is essential and journalctl alone won't tell you:** A process mysteriously dies with no application-level error message at all. Checking `dmesg | grep -i "killed process"` reveals whether the **kernel's own OOM (Out-Of-Memory) killer** terminated it due to system-wide memory pressure — completely different root cause than an application bug, and only visible at this layer.

### Severity Levels, In Order (Most to Least Severe)
`emerg → alert → crit → err → warning → notice → info → debug`

When you filter with `-p err`, you get `err` and everything MORE severe than it (`crit`, `alert`, `emerg`) — not less severe. This is why fixing by priority means starting from the top of this list and working down, ignoring routine `info`/`debug` noise until the more serious categories are clear.

### Worked Example: Full Incident Investigation
A service crashed sometime in the last hour. Full investigation:
```
journalctl -u myservice --since "1 hour ago"   # see everything that service logged recently
journalctl -u myservice -p err --since "1 hour ago"   # narrow to just its errors
dmesg | grep -i "killed process"                # check if the KERNEL killed it (OOM)
grep myservice /var/log/syslog                  # cross-check against the flat-file log too
```
If `dmesg` shows an OOM-kill entry matching the timing, you know the root cause was memory pressure, not a bug in the service itself — a completely different fix (add memory, reduce memory usage, or adjust OOM-killer priority) versus debugging application code.

---

## DEEP DIVE 3: Processes — Full Detail

### What a Process Really Is
The moment any program starts running — whether it's your shell, a background daemon, or a one-off command — the kernel creates a **process** for it: a unique PID (process ID), an allocated chunk of memory, a set of open files it's using, and a record of which process started it (the parent, tracked via PPID).

Processes form a tree. The very first process (PID 1, historically `init`, now usually `systemd`) is the ancestor of every other process on the system. When a process's direct parent dies before it does, it becomes an "orphan" and gets automatically re-adopted by PID 1 — which is exactly why checking a suspicious process's PPID for the value `1` is a real technique for identifying an orphaned process during an incident.

### Full Command Toolkit

| Command | What it shows | When to use it |
|---|---|---|
| `ps` | Only YOUR terminal's own processes | Rarely useful alone |
| `ps aux` | Every process, system-wide, with %CPU/%MEM columns | "What's using the most resources right now, system-wide?" |
| `ps -ef` | Every process, system-wide, with PID/PPID columns | "What spawned this process? Is it an orphan?" |
| `top` | Live, auto-refreshing dashboard | Watching a runaway process in real time during an active incident |
| `htop` | Same as top, nicer colored UI | Same use case, more pleasant to read |
| `ps aux \| grep <name>` | Filter down to one specific process | "Is nginx even running? What's its PID?" |

### Signals — What Actually Happens When You "Kill" Something
`kill` doesn't inherently mean "force stop." It sends a **signal** — a message the kernel delivers to a process. Different signal numbers mean different things:

- **SIGTERM (signal 15, the default)** — "please terminate yourself." The process can catch this signal, run its own cleanup code (close files, finish a database write, release locks), and then exit gracefully.
- **SIGKILL (signal 9)** — not a request, an unconditional order enforced directly by the kernel itself. The target process gets ZERO opportunity to clean up — it's simply removed from memory immediately.

**Real scenario where this distinction matters enormously:** A database process is killed with `-9` while mid-write to its data files. Because it never got the chance to finish the write or roll back safely, the data file itself can end up in a corrupted, inconsistent state — a much worse outcome than the original problem that made you want to kill it in the first place. This is why the correct operational habit is always: try plain `kill` first, wait a reasonable amount of time, and only escalate to `-9` if the process is genuinely unresponsive to the polite request.

### Priority (Niceness) — Full Detail
Every process has a niceness value from **-20** (highest possible scheduling priority — most demanding, most aggressive about getting CPU time) to **+19** (lowest priority — most willing to step aside for other processes). The default for a normal process is **0**.

Regular (non-root) users can only ever move a process's niceness **upward** (make it nicer/lower priority) — never negative. This restriction exists because if any user could freely assign negative (aggressive) priority to their own processes, they could effectively starve every other user and process on a shared machine of CPU time. Only root has the authority to grant elevated (negative) priority.

```
nice -n 10 mycommand &          # START a new process at niceness 10 (lower priority)
renice 15 -p 1234                # CHANGE an ALREADY-RUNNING process's niceness to 15
ps -o pid,ni,cmd -p 1234         # check a specific process's current niceness value
```

### Worked Example: Diagnosing High CPU Usage
```
top                              # watch live, spot the process eating CPU (note its PID)
ps -o pid,ppid,ni,cmd -p <PID>   # check its PID, parent PID, and current niceness
kill <PID>                       # try the polite request first
sleep 5
ps aux | grep <PID>              # confirm whether it actually stopped
kill -9 <PID>                    # only if it's still alive after the polite request
```

### Worked Example: Finding an Orphaned Process
```
ps -ef | grep <process_name>     # find the process and note its PPID column
```
If the PPID shown is `1`, that process's original parent has already died, and it's now directly owned by the system's init process — a strong signal that whatever spawned it (a deploy script, a shell session) is long gone, but the process itself kept running unattended.

---

## DEEP DIVE 4: Networking — Full Detail

### What's Actually Happening When Two Machines "Talk"
Every network interaction involves layers stacking on top of each other: physical connectivity → routing → a specific port being open → the actual application responding correctly. When something "isn't working," the real skill is figuring out **which layer** is broken, because each layer failing looks similar from the outside ("it's not working") but has a completely different fix.

### Your Own Machine's Network Identity
```
ip a
```
Shows every network interface your machine has, and its IP address. Key things you'll see:
- `lo` — the loopback interface, always `127.0.0.1`, used for a machine talking to itself
- A real interface like `enp1s0` or `eth0` — your actual network connection, with a real IP like `172.30.1.2`
- Possibly a `docker0` bridge — a virtual internal network Docker creates for containers to talk to each other and the host

**Scenario:** A teammate asks "what's this server's IP?" — `ip a` is the direct answer, replacing the older, now-deprecated `ifconfig` command.

### The Diagnostic Ladder, In Full Detail

This is the single most valuable networking skill: checking layers in the correct order instead of jumping straight to the most complex tool.

**Layer 1 — Is the host reachable at all?**
```
ping -c 4 8.8.8.8          # raw IP, skips DNS entirely
ping -c 4 google.com        # domain name, DNS lookup happens first
```
`ping` sends small ICMP packets and waits for a reply. This tells you ONLY "can packets get from me to that machine and back" — nothing about whether any particular service on that machine is actually working. A server can respond to ping perfectly while its web server is completely down.

**Layer 2 — Is the specific service/port actually listening?**
```
ss -tuln
```
Breaking down the flags: `t`=TCP, `u`=UDP, `l`=listening sockets only, `n`=show numeric ports instead of resolving service names (faster, and works even if DNS is having issues).

**Scenario:** The host responds to ping just fine, but your app still can't connect on port 8080. Running `ss -tuln` and NOT seeing port 8080 in the list tells you immediately: nothing is even listening there — the application itself either isn't running or is bound to a different port/interface than expected. This narrows the problem from "network issue" to "application isn't up," a completely different team/fix.

**Layer 3 — Does the domain name even resolve to the right address?**
```
dig google.com
nslookup google.com
```
DNS translates human-readable names into IP addresses. If DNS resolution itself is broken or returning a stale/wrong IP, every layer after this will fail too, no matter how healthy the actual target server is. This is why DNS problems are notorious for causing confusing, seemingly-random failures — the symptom shows up somewhere completely different from the actual cause.

**Scenario:** An app suddenly can't reach its database, but the database server itself is fine. Running `dig` on the database's hostname reveals it's now resolving to the WRONG IP (maybe a DNS record changed, or a stale local DNS cache) — the fix is a DNS correction, not a database restart.

**Layer 4 — Does an actual request succeed at the application level?**
```
curl -I https://example.com      # headers only, fast check
curl https://example.com          # full response body
wget https://example.com          # download the response as a file
```
This is the final, most specific layer — actually sending a real HTTP request and seeing what comes back. A `curl -I` showing a proper HTTP status code (200, 301, etc.) confirms the full chain worked: reachable, port open, DNS correct, AND the application responded correctly.

### Full Path/Route Tracing
```
traceroute google.com
```
Shows every network "hop" (router) your traffic passes through on the way to a destination, with the time taken at each hop. Essential when something is technically reachable but **slow**, not fully down — you can pinpoint exactly which hop along the path is introducing delay, rather than treating the whole path as one black box.

### Port Reference — Common Services You'll See
| Port | Service |
|---|---|
| 22 | SSH |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 6379 | Redis |
| 8080 | Common alternate HTTP port for dev/internal services |

### Worked Example: Full "API Server Isn't Responding" Investigation
```
ping -c 4 api.internal.company.com        # Layer 1: reachable at all?
ss -tuln | grep <port>                     # Layer 2: is the port actually listening?
dig api.internal.company.com               # Layer 3: does the name resolve correctly?
curl -I https://api.internal.company.com   # Layer 4: does a real request succeed?
```
Whichever layer fails first tells you exactly where to focus — no guessing, no wasted effort chasing the wrong team or the wrong fix.

### Networking Files You Might Encounter
| Path | Purpose |
|---|---|
| `/etc/hosts` | Manual, local overrides for hostname-to-IP mapping — checked BEFORE real DNS lookups |
| `/etc/resolv.conf` | Which DNS servers this machine actually queries |
| `/etc/nsswitch.conf` | Controls the order Linux checks different sources (local files vs DNS) for name resolution |

**Scenario where `/etc/hosts` matters:** A developer swears "the DNS record is definitely updated" but their machine still resolves the old IP — often because a stale manual entry in their own local `/etc/hosts` file is silently overriding real DNS for that hostname, checked first before any actual DNS query even happens.

---

| Need | Command/Path |
|---|---|
| Find which directory is eating disk space | `du -sh /path/* \| sort -rh \| head -5` |
| Check if a service will survive a reboot | `systemctl is-enabled <service>` |
| See who logged in recently | `/var/log/auth.log` or `last` |
| Watch a log file update live | `tail -f /path/to/log` or `journalctl -u <service> -f` |
| Find every file of a certain type | `find /path -type f -name "*.ext"` |
| Search file contents for a keyword | `grep -rn "keyword" /path` |
| See exactly what's consuming CPU right now | `top` |
| Confirm a scheduled job actually ran | `grep CRON /var/log/syslog` or `journalctl -u cron` |
| Check if a process was killed by low memory | `dmesg \| grep -i "killed process"` |
| Verify a backup archive without extracting it | `tar -tzvf archive.tar.gz` |
| Check if a host is reachable at all | `ping -c 4 <host>` |
| Check if a specific port is open/listening | `ss -tuln \| grep <port>` |
| Check if a domain resolves to the right IP | `dig <domain>` or `nslookup <domain>` |
| Test if an actual web request succeeds | `curl -I https://<domain>` |
| See every hop between you and a destination | `traceroute <domain>` |
| Check local hostname overrides before DNS | `/etc/hosts` |
