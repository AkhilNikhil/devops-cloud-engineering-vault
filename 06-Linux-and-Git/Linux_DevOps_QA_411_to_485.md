# Linux & DevOps Interview Prep — Q411 to Q485

> User Management · File Management · File Permissions · Process Management · Metrics & Monitoring · Log Management · Networking · Scripting · Scenario Questions

---

## Table of Contents

1. [User Management](#user-management) (Q411–Q422)
2. [File Management](#file-management) (Q423–Q432)
3. [File Permissions](#file-permissions) (Q433–Q439)
4. [Process Management](#process-management) (Q440–Q449)
5. [Metrics & Monitoring](#metrics--monitoring) (Q450–Q455)
6. [Log Management](#log-management) (Q456–Q463)
7. [Networking](#networking) (Q464–Q470)
8. [Scripting](#scripting) (Q471–Q478)
9. [Scenario Questions](#linux-scenario-questions) (Q479–Q485)

---

## User Management

### Q411. What are the 3 types of users in Linux?

**1. Root User**
- Superuser — complete control of the system
- UID = `0`
- Can read/write/execute any file, install software, manage users, change system settings
- Username: `root` · Home: `/root`
- ⚠️ Dangerous — one wrong command can destroy the system

**2. System Users**
- Created automatically by software/services
- UID range: `1–999`
- Never log in interactively; run services (nginx, mysql, www-data, jenkins)
- No home directory (or `/dev/null`)
- Security principle: services run as these users, **not root**

**3. Regular Users**
- Human users who log in and work
- UID range: `1000+`
- Have a home directory: `/home/username`
- Limited privileges; need `sudo` for admin commands

**Check your UID:**
```bash
id
# uid=1001(akhil) gid=1001(akhil) groups=1001(akhil),27(sudo)
```

| UID range | Meaning |
|---|---|
| `0` | root (always) |
| `1–999` | system users |
| `1000+` | regular users |

**See all users:**
```bash
cat /etc/passwd
# username:x:UID:GID:description:home:shell
```

---

### Q412. What is UID and GID?

**UID (User ID)** — a unique number per user, used internally by Linux instead of usernames.
- `0` = root
- `1–999` = system users
- `1000+` = regular users

**GID (Group ID)** — a unique number per group. Every user has a **primary group** (usually same name as the user).

```bash
id akhil
# uid=1001(akhil) gid=1001(akhil) groups=1001(akhil),27(sudo),998(docker)

id             # current user's info
id -u akhil    # just the UID
id -g akhil    # just the primary GID
```

**Why UIDs matter:** files are owned by UID *numbers*, not names.
```bash
ls -la
# -rw-r--r-- 1 1001 1001 100 app.js
```
If user `akhil` (UID 1001) is deleted, the file still shows `1001` — a number, not a name. This is why a Docker container running as UID 1001 might map to a *different* user on the host.

---

### Q413. What files store user and group information?

**`/etc/passwd`** — account info for all users
```
akhil:x:1001:1001:Akhil BM:/home/akhil:/bin/bash
│     │  │    │    │         │            └─ shell
│     │  │    │    │         └─ home directory
│     │  │    │    └─ GECOS (comment/full name)
│     │  │    └─ primary GID
│     │  └─ UID
│     └─ password placeholder (x → real hash in /etc/shadow)
└─ username
```
Readable by everyone.

**`/etc/shadow`** — encrypted passwords, root-only
```
akhil:$6$salt$hash...:19000:0:99999:7:::
```
```bash
sudo cat /etc/shadow    # works for root only
```

**`/etc/group`** — groups and their members
```
sudo:x:27:akhil,ravi
docker:x:998:akhil
developers:x:1002:akhil,priya,ravi
```

**`/etc/gshadow`** — encrypted group passwords (rarely used)

---

### Q414. How do you create a user with a home directory?

```bash
useradd -m devops
```
- `-m` → create home directory (`/home/devops`) — **without it, no home dir is created**

**Full specification:**
```bash
useradd \
  -m \                        # create home directory
  -s /bin/bash \              # set shell
  -G docker,sudo \            # add to these groups
  -c "DevOps Engineer" \      # comment/description
  devops
```

**Set password after creation:**
```bash
passwd devops
```

**Verify:**
```bash
id devops
ls -la /home/devops
grep devops /etc/passwd
```

**`adduser` vs `useradd`:**

| | `adduser` (Debian/Ubuntu) | `useradd` (scripted) |
|---|---|---|
| Interaction | Interactive prompts | Non-interactive |
| Home dir | Created by default | Needs `-m` |
| Use case | Manual, easy | Scripts/automation |

---

### Q415. How do you set a password for a user?

```bash
passwd devops          # interactive prompt
sudo passwd devops     # root setting another user's password
passwd                 # change your own (no username)
```

**Non-interactive (scripts):**
```bash
echo "devops:mypassword" | chpasswd     # works on Ubuntu & RHEL
echo "devops:$(openssl rand -base64 16)" | chpasswd   # secure random password
```

**Password policy:**
```bash
passwd -x 90 devops     # expire after 90 days
passwd -n 1 devops      # min 1 day between changes
passwd -w 7 devops      # warn 7 days before expiry
passwd -l devops        # lock account
passwd -u devops        # unlock account
passwd -S devops        # check status → P (set) / L (locked) / NP (none)
```

---

### Q416. How do you add a user to a group?

```bash
usermod -aG groupname username
usermod -aG sudo devops
usermod -aG sudo,docker,developers devops   # multiple at once
```
- `-a` = **append** (don't remove existing groups)
- `-G` = specify group(s)

```bash
groupadd mygroup             # create group if it doesn't exist
usermod -aG mygroup devops
```

⚠️ **Group changes require re-login** (or `newgrp groupname` for the current shell).

**Verify:**
```bash
groups devops
id devops
```

**Create + add to groups in one step:**
```bash
useradd -m -s /bin/bash -G sudo,docker devops
```

---

### Q417. What is the difference between `-aG` and `-G` in usermod?

⚠️ **Critical** — the wrong flag can wipe out all group memberships.

| Command | Result |
|---|---|
| `usermod -aG docker devops` | ✅ **Appends** docker → keeps existing groups |
| `usermod -G docker devops` | ❌ **Replaces** all groups with only `docker` |

**Example danger:**
```bash
usermod -G docker akhil
# If akhil was in "sudo" → sudo access is now GONE!
```

**Memory trick:** `-a` = append = **add** = safe. No `-a` = replace = **remove existing** = dangerous.

**Always use:**
```bash
usermod -aG docker akhil
```

---

### Q418. `sudo` group (Ubuntu) vs `wheel` group (RHEL)

Both grant admin/sudo privileges — just different names by distro convention.

| Distro | Admin group |
|---|---|
| Ubuntu / Debian | `sudo` |
| RHEL / CentOS / Amazon Linux / Fedora | `wheel` |

```bash
usermod -aG sudo akhil      # Ubuntu
usermod -aG wheel ec2-user  # RHEL / Amazon Linux
```

**Check which applies:**
```bash
grep -E "^%sudo|^%wheel" /etc/sudoers
cat /etc/os-release | grep NAME
```

> **Interview line:** "Ubuntu uses the `sudo` group, while RHEL-based systems like CentOS and Amazon Linux use `wheel`. Same functionality, different naming convention."

---

### Q419. Why do group changes require re-login?

Group memberships are **read at login time** (via PAM) and cached in the session — they don't auto-refresh.

```bash
usermod -aG docker akhil
# /etc/group updated immediately, but akhil's CURRENT session still has old data

groups akhil     # reads /etc/group → shows docker ✅
groups           # shows session's cached groups → may NOT show docker
```

**Fixes:**
```bash
exit          # then SSH back in — full re-login
newgrp docker # new shell with docker group active (current shell only)
su - akhil    # login-like session refresh
```

> Classic symptom: "I added the user to the docker group but still get permission denied" → they need to re-login.

---

### Q420. How do you delete a user along with their home directory?

```bash
userdel -r devops
```
- `-r` = also remove home directory + mail spool

**Without `-r`:** account is deleted but `/home/devops` remains orphaned (files show a UID number, not a username).

**What `-r` removes:** `/etc/passwd` entry, `/etc/shadow` entry, `/etc/group` entries, home dir, mail spool.
**What it does NOT remove:** files owned by the user *outside* their home dir, cron jobs, running processes.

**Safe deletion procedure:**
```bash
ps aux | grep devops           # check running processes
kill -9 $(pgrep -u devops)     # kill them
userdel -r devops              # then delete
find / -nouser 2>/dev/null     # find orphaned files afterward
```

---

### Q421. How do you check which groups a user belongs to?

```bash
groups devops
# devops : devops sudo docker developers

id devops
# uid=1001(devops) gid=1001(devops) groups=1001(devops),27(sudo),998(docker)
```

| Command | Shows |
|---|---|
| `groups devops` | which groups devops belongs to |
| `id devops` | same, plus UID/GID numbers |

> `groups` (no username) may show **stale/cached** data from login time; `groups devops` reads `/etc/group` live.

---

### Q422. How do you check who is inside a group?

```bash
getent group sudo
# sudo:x:27:devops,akhil,ravi

grep "^sudo:" /etc/group
```

**Why `getent` over `cat /etc/group`:** `getent` queries NSS (Name Service Switch) — covers local files **and** LDAP/NIS. `cat /etc/group` only reads the local file.

```bash
getent group docker      # from the group's perspective
groups devops            # from the user's perspective
```

---

## File Management

### Q423. Absolute vs relative path

**Absolute path** — starts from root (`/`), works from anywhere.
```bash
/home/akhil/projects/app.js
/etc/nginx/nginx.conf
```

**Relative path** — starts from the current directory.
```bash
projects/app.js     # only resolves correctly from /home/akhil
../etc/nginx.conf
./start.sh
```

**Use absolute in scripts** (unknown execution location); **relative interactively** (you know where you are).

> Common mistake: absolute path starts from **root** `/`, not the home directory.

---

### Q424. What do `/`, `~`, `.`, `..`, `-` mean in paths?

| Symbol | Meaning | Example |
|---|---|---|
| `/` | Root directory | `cd /` |
| `~` | Home directory | `cd ~` → `/home/akhil` |
| `.` | Current directory | `./app.sh`, `cp app.js .` |
| `..` | Parent directory | `cd ..`, `cd ../..` |
| `-` | Previous directory | `cd -` toggles between last two dirs |

```bash
pwd     # /home/akhil/projects
cd ..   # /home/akhil
cd -    # /home/akhil/projects (back!)
```

---

### Q425. List all files including hidden ones, with sizes

```bash
ls -lah
```
- `-l` long format · `-a` all (incl. hidden) · `-h` human-readable sizes

```bash
ls -la       # long + all (raw byte sizes)
ls -lah      # long + all + human-readable ✅ best default
ls -lt       # newest first
ls -ltr      # oldest first
ls -lS       # largest first
ls -R        # recursive
```

---

### Q426. Create nested directories in one command

```bash
mkdir -p /opt/tomcat/webapps/myapp
```
`-p` (parents) creates every missing parent directory — and won't error if they already exist.

**Brace expansion for multiple dirs at once:**
```bash
mkdir -p /opt/tomcat{1,2}/webapps
mkdir -p project/{src,tests,docs,config}
```

---

### Q427. `cp` vs `mv`

| | `cp` (copy) | `mv` (move/rename) |
|---|---|---|
| Original | Stays at source | Removed from source |
| Result | Two copies exist | Only one location exists |
| Use for | Duplicating | Relocating or renaming |

```bash
cp -r /opt/tomcat1 /opt/tomcat2   # copy directory
mv oldname.js newname.js          # rename
mv /opt/tomcat1/config /opt/tomcat2/config
```

Useful flags: `cp -p` (preserve timestamps/perms), `cp -i` / `mv -i` (confirm before overwrite).

---

### Q428. `rm` vs `rm -rf`

```bash
rm filename.txt          # single file only — errors on directories
rm -r dirname            # recursive, prompts per file
rm -f filename           # force, no prompts
rm -rf dirname           # recursive + force = delete everything, no confirmation
```

⚠️ **Linux has no recycle bin** — `rm -rf` is permanent and unrecoverable.

**Safer approach:**
```bash
ls -la /path/to/delete   # always review first
rm -ri dirname           # -i asks per file
```

---

### Q429. Why is `rm -rf` dangerous?

1. **No recycle bin** — deleted instantly, permanently
2. **No confirmation** (`-f` skips all prompts)
3. **Recursive** — destroys entire subdirectory trees
4. **Typos are catastrophic** — `rm -rf /opt /tomcat` (space) deletes two top-level dirs instead of one path
5. **As root**, it can destroy the entire OS: `rm -rf /`

**Mitigations:**
```bash
alias rm='rm -i'     # always confirm
# or use trash-cli for a soft-delete workflow
```

---

### Q430. View the last 100 lines of a file and follow it live

```bash
tail -fn 100 /opt/tomcat1/logs/catalina.out
```
- `-f` follow (watch for new lines) · `-n 100` show last 100 lines first

**Combine with grep to filter:**
```bash
tail -f catalina.out | grep -i "exception\|error"
```
`Ctrl+C` stops following.

---

### Q431. `cat` vs `head` vs `tail` vs `less`

| Command | Purpose | Best for |
|---|---|---|
| `cat file` | Print entire file | Small files |
| `head -n 20 file` | First N lines | Checking file format |
| `tail -n 100 file` | Last N lines | Recent log entries |
| `tail -f file` | Follow live | Watching logs in real time |
| `less file` | Interactive pager | Large files, searchable |

**`less` navigation:** `Space`/`PgDn` next page · `b` previous page · `/pattern` search forward · `n` next match · `q` quit.

---

### Q432. Hidden files — what and how to view them

Hidden files start with a dot: `.bashrc`, `.bash_history`, `.gitignore`, `.env`, `.ssh/`, `.config/`.

```bash
ls -a      # show all, including hidden
ls -lah    # long + all + human-readable ✅
```

⚠️ `.env` files often contain secrets — always add them to `.gitignore`.

---

## File Permissions

### Q433. What does `rwx` mean?

| Letter | Meaning (file) | Meaning (directory) | Value |
|---|---|---|---|
| `r` | read content | list contents | 4 |
| `w` | modify content | create/delete/rename entries | 2 |
| `x` | run as program | enter (`cd`) | 1 |

**Permission string:**
```
-rwxr-xr-x
│ │   │   └─ others
│ │   └─ group
│ └─ owner
└─ type (- file, d directory, l symlink)
```

**Numeric equivalents:** `rwx`=7, `rw-`=6, `r-x`=5, `r--`=4, `---`=0

---

### Q434. What is `chmod` and how do you use it?

**Numeric (octal):**
```bash
chmod 755 filename
chmod 600 ~/.ssh/id_rsa    # private key: owner rw only
```

**Symbolic:**
```bash
chmod u+x script.sh    # add execute for owner
chmod g+w file.txt     # add write for group
chmod o-r secret.txt   # remove read for others
chmod a+x script.sh    # add for everyone
```

`u`=user, `g`=group, `o`=others, `a`=all · `+`/`-`/`=` add/remove/set

**Recursive:**
```bash
chmod -R 755 /opt/tomcat/
```

| Mode | Typical use |
|---|---|
| `755` | executables, directories |
| `644` | regular files, config |
| `600` | private files |
| `400` | read-only private keys |
| `777` | ⚠️ avoid — everyone gets everything |

---

### Q435. What does `chmod 755` mean?

`7` owner=`rwx` · `5` group=`r-x` · `5` others=`r-x` → `-rwxr-xr-x`

Use for: shell scripts, binaries, directories (need `x` to `cd` into them).
```bash
chmod 755 startup.sh
chmod 755 /opt/tomcat/
```

---

### Q436. What does `chmod 644` mean?

`6` owner=`rw-` · `4` group=`r--` · `4` others=`r--` → `-rw-r--r--`

Use for: text files, configs (`nginx.conf`), HTML/CSS/JS, logs, documentation. **Not** for executables or private keys.

| Mode | Use case |
|---|---|
| `644` | regular files (read all, write owner) |
| `755` | executables (run all, write owner) |
| `600` | private (owner rw only) |
| `400` | read-only private keys |

---

### Q437. What is `chown` and how do you use it?

```bash
chown akhil app.js                       # change owner
chown akhil:developers app.js            # change owner + group
chown :docker /var/run/docker.sock       # change group only
chown -R tomcat:tomcat /opt/tomcat1/     # recursive
```

**Verify:**
```bash
ls -la app.js
# -rw-r--r-- 1 akhil developers 100 app.js
```

**Common fix** after creating files as root:
```bash
sudo chown -R $USER:$USER /opt/myapp/
```

---

### Q438. What is `setfacl` and when do you use it?

ACLs give **fine-grained permissions** beyond owner/group/others — e.g. one specific extra user needs read access without joining the group.

```bash
setfacl -m u:john:r-- /opt/myapp/config.txt   # john gets read
setfacl -m g:devteam:rwx /opt/myapp/          # devteam group gets rwx
setfacl -x u:john /opt/myapp/config.txt       # remove john's ACL
setfacl -b /opt/myapp/config.txt              # remove ALL ACLs
setfacl -R -m u:john:r-x /opt/myapp/          # recursive
```

**View ACLs:**
```bash
getfacl filename.txt
# user:john:r--   ← john specifically!
```

**Use when:** a single user needs different access than group membership allows, without loosening permissions for the whole group.

---

### Q439. Owner vs group vs others

```
-rwxr-x---
 rwx│r-x│---
 owner group others
```

- **Owner** — usually whoever created the file
- **Group** — members of the file's group get the middle permission set
- **Others** — everyone else gets the last set

```bash
ls -la filename       # see owner and group
chown akhil file.txt        # change owner
chown :developers file.txt  # change group
chown akhil:developers file.txt   # change both
```

---

## Process Management

### Q440. View all running processes

```bash
ps aux          # all processes on the system
ps aux | grep tomcat
top             # live view
htop            # enhanced live view
pstree          # parent-child tree
```

**Key `ps aux` columns:** `PID`, `%CPU`, `%MEM`, `STAT` (S=sleeping, R=running, Z=zombie, D=disk wait), `TIME`, `COMMAND`

---

### Q441. `top` vs `htop`

| | `top` | `htop` |
|---|---|---|
| Availability | Built-in, always there | `apt install htop` |
| Colors | Minimal | Rich |
| Mouse support | No | Yes |
| Kill process | Enter PID | Click + `F9` |
| Visual bars | No | Yes (CPU/mem) |

**`top` shortcuts:** `q` quit · `P` sort CPU · `M` sort memory · `k` kill · `1` all cores
**`htop` shortcuts:** `F3` search · `F4` filter · `F5` tree view · `F9` kill

---

### Q442. Find the process using the most CPU

```bash
ps aux --sort=-%cpu | head -10
top            # already sorted by CPU
htop           # visual, sorted by CPU
```

---

### Q443. Find the process using the most memory

```bash
ps aux --sort=-%mem | head -10
top            # press M
htop           # press F6 → MEM%
pmap -x 1234   # detailed memory map for PID 1234
smem -s rss -r # better memory reporting (install required)
```

---

### Q444. `kill` vs `kill -9`

| | `kill` (SIGTERM, 15) | `kill -9` (SIGKILL) |
|---|---|---|
| Behavior | Process can clean up & exit gracefully | Immediate, forced termination |
| Catchable | Yes | No — cannot be caught/ignored |
| Risk | Low | Data loss / corruption possible |

**Best practice — try graceful first:**
```bash
kill 1234
sleep 5
if ps -p 1234 > /dev/null 2>&1; then
  kill -9 1234    # force only if still running
fi
```

---

### Q445. SIGTERM vs SIGKILL

| Signal | Number | Catchable | Behavior |
|---|---|---|---|
| SIGHUP | 1 | Yes | Hangup (often: reload config) |
| SIGINT | 2 | Yes | Interrupt (Ctrl+C) |
| SIGTERM | 15 | Yes | Graceful terminate |
| SIGKILL | 9 | **No** | Immediate kill, uncatchable |

Typical shutdown sequence: SIGTERM → wait 30s → SIGKILL if unresponsive (this is what `docker stop` and `systemctl stop` do internally).

---

### Q446. Kill a process by name

```bash
pkill java              # pattern match — "tom" matches tomcat, tomee, etc.
pkill -9 java
killall java            # exact name match only
pgrep java              # list matching PIDs
kill $(pgrep java)      # kill all matches
```

---

### Q447. Check if a service is running

```bash
systemctl status nginx
systemctl is-active nginx     # quick: "active" or "inactive"
ps aux | grep nginx | grep -v grep
pgrep nginx
ss -tulpn | grep :80          # indirect check via port
```

---

### Q448. Start, stop, restart a service

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx    # stop + start (brief downtime)
sudo systemctl reload nginx     # apply config, zero downtime
```

**Reload vs restart:** use `reload` for config changes with no downtime; `restart` after major changes or when unresponsive.

---

### Q449. Enable a service to start on boot

```bash
sudo systemctl enable nginx
sudo systemctl enable --now nginx    # enable + start immediately
sudo systemctl is-enabled nginx
sudo systemctl disable nginx
```

---

## Metrics & Monitoring

### Q450. Check RAM and Swap usage

```bash
free -h
```
```
              total    used    free   shared  buff/cache  available
Mem:           7.7G    3.2G    1.5G    100M       3.0G       4.2G
Swap:          2.0G    0.5G    1.5G
```

> ⚠️ Look at **`available`**, not `free` — Linux uses spare RAM for cache. `available` = free + reclaimable cache.

```bash
watch -n 2 free -h    # monitor continuously
```

---

### Q451. What is Swap and when does Linux use it?

Swap = disk space used as overflow RAM. **Analogy:** RAM is your desk, Swap is the drawer next to it.

When RAM fills up, Linux moves inactive memory pages to Swap to free space — but disk is **10–300x slower** than RAM, so heavy swapping causes severe slowdowns ("swap storms").

```bash
free -h    # check Swap usage — high "used" swap = problem
```
**Fixes:** kill memory hogs, add RAM, reduce app memory footprint.

---

### Q452. Check disk space usage

```bash
df -h
```
| Column | Meaning |
|---|---|
| Size | total partition size |
| Used | space used |
| Avail | space remaining |
| Use% | percentage used |

**Warning levels:** 80% monitor · 90% urgent · 100% critical (apps may crash)

```bash
df -h /opt          # specific mount
df -i               # inode usage
watch -n 10 df -h   # continuous monitoring
```

---

### Q453. Find which folder is using the most disk space

```bash
du -sh /var/log/*           # summary per item, human-readable
du -sh /* | sort -hr         # largest first
du -ah / | sort -rh | head -20   # top 20 largest files/dirs
```

**`df` vs `du`:** `df` = space per filesystem/partition; `du` = space per folder/file.

**Disk-full workflow:**
```bash
df -h                 # confirm it's full
du -sh /*             # find the big top-level dir
du -sh /var/*         # drill down
du -sh /var/log/*     # drill down further
```

---

### Q454. Check disk I/O

```bash
iostat -x 2      # extended stats, updates every 2s
sudo iotop       # top-style view for disk I/O per process
```

**Key columns:** `await` (wait time, high = bottleneck) · `%util` (near 100% = disk saturated)

```bash
apt install sysstat     # provides iostat on Ubuntu/Debian
```

---

### Q455. `df -h` vs `du -sh`

| Question | Command |
|---|---|
| How full is my disk overall? | `df -h` |
| Which folder is eating space? | `du -sh /path/*` |

**Typical drill-down:**
```bash
df -h                              # "root at 90%!"
du -sh /*                          # "/var is biggest"
du -sh /var/*                      # "/var/log is 5GB"
du -sh /var/log/*                  # "apache logs are 4GB"
rm -rf /var/log/apache2/*.gz       # clean up
```

---

## Log Management

### Q456. System log locations — Ubuntu

| Log | Purpose |
|---|---|
| `/var/log/syslog` | General system log — most important |
| `/var/log/auth.log` | Logins, sudo usage, SSH attempts |
| `/var/log/kern.log` | Kernel/hardware messages |
| `/var/log/dpkg.log` | Package install/remove history |
| `/var/log/apt/history.log` | apt command history |
| `/var/log/apache2/` | `access.log`, `error.log` |
| `/opt/tomcat/logs/` | `catalina.out` |

```bash
journalctl              # systemd logs
journalctl -u nginx -f  # follow a specific service's logs
```

---

### Q457. System log locations — RHEL

| Log | Purpose |
|---|---|
| `/var/log/messages` | General system log (= Ubuntu's `syslog`) |
| `/var/log/secure` | Auth/security events (= Ubuntu's `auth.log`) |
| `/var/log/cron` | Cron execution log |
| `/var/log/maillog` | Mail server logs |
| `/var/log/yum.log` / `dnf.log` | Package install history |
| `/var/log/cloud-init.log` | EC2 startup logs |

`journalctl -u nginx -f` works identically on both distro families.

---

### Q458. `access.log` vs `error.log` (Apache)

**`access.log`** — every incoming HTTP request:
```
192.168.1.100 - - [20/Apr/2026:10:30:45] "GET /project1 HTTP/1.1" 200 1234
```
Tells you: who visited, what URL, when, status code, bytes served.

**`error.log`** — Apache errors and problems, e.g.:
```
[error] File does not exist: /var/www/html/favicon.ico
[error] [proxy] AH01114: failed to make connection to backend: localhost:7789
```

> A `502` in `error.log` pointing at `localhost:7789` typically means the backend (Tomcat) is down.

---

### Q459. Search for "error" across all log files recursively

```bash
grep -ri "error" /var/log/
```
`-r` recursive · `-i` case-insensitive

```bash
grep -rl "error" /var/log/                 # filenames only
grep -rn "error" /var/log/                 # with line numbers
grep -ri "error\|warning\|critical" /var/log/
grep -ri "error" /var/log/ --exclude="*.gz"
grep -ri -A 3 "error" /var/log/            # 3 lines of context after
```

---

### Q460. Count how many ERROR lines are in a log file

```bash
grep -c "ERROR" filename.log
grep -ci "error" catalina.out      # case-insensitive
grep -rc "ERROR" /var/log/         # per-file counts, recursive
grep "ERROR" file.log | wc -l      # equivalent alternative
```

---

### Q461. Watch logs live, filtered to errors only

```bash
tail -f /opt/tomcat1/logs/catalina.out | grep -i "error\|exception\|fatal"
tail -f /var/log/apache2/access.log | grep " 500 "
tail -fn 100 catalina.out | grep -i error   # last 100 first, then follow
```

**Watch multiple files at once:**
```bash
tail -f /opt/tomcat1/logs/catalina.out \
     -f /opt/tomcat2/logs/catalina.out \
     -f /var/log/apache2/error.log | grep -i error
```

---

### Q462. HTTP status codes — 200, 403, 404, 500, 502

| Code | Meaning |
|---|---|
| `200 OK` | Success |
| `301 / 302` | Redirect (permanent / temporary) |
| `401 Unauthorized` | Not authenticated |
| `403 Forbidden` | Authenticated but not authorized |
| `404 Not Found` | Resource doesn't exist |
| `500 Internal Server Error` | Generic server-side crash/exception |
| `502 Bad Gateway` | Proxy couldn't get a response from upstream |
| `503 Service Unavailable` | Overloaded or under maintenance |

---

### Q463. What does a 502 mean in a Tomcat + Apache setup?

**502 = Apache (proxy) can't reach Tomcat (backend).**

```
User → Apache (port 80) → Tomcat 1 (7789) / Tomcat 2 (8888)
```

**Debugging workflow:**
```bash
ps aux | grep tomcat                          # 1. is Tomcat running?
curl http://localhost:7789/project1           # 2. test Tomcat directly
tail -f /var/log/apache2/error.log            # 3. check Apache errors
tail -f /opt/tomcat1/logs/catalina.out        # 4. check Tomcat errors
/opt/tomcat1/bin/shutdown.sh                  # 5. restart
/opt/tomcat1/bin/startup.sh
```

**Common causes:** Tomcat stopped/crashed, wrong port in `server.xml`, wrong Apache `ProxyPass` config.

---

## Networking

### Q464. Check the IP address of a Linux server

```bash
ip addr             # modern
ip a show eth0       # specific interface
ifconfig             # older/deprecated

hostname -I                       # quick list of IPs
curl ifconfig.me                  # public/external IP
ip link show                      # list interfaces (eth0, lo, ens3...)
```

---

### Q465. Test connectivity to a host

```bash
ping -c 4 google.com              # ICMP test, 4 packets
nc -zv 192.168.1.5 22             # test a specific TCP port
curl -I http://example.com        # HTTP headers only
telnet 192.168.1.5 22             # test TCP connection
traceroute google.com             # show network path
mtr google.com                    # real-time traceroute
```

---

### Q466. Check which ports are open and listening

```bash
ss -tulpn
```
`-t` TCP · `-u` UDP · `-l` listening only · `-p` process · `-n` numeric

```bash
ss -tulpn | grep :80        # who's on port 80?
netstat -tulpn              # older equivalent
nmap -p 22,80,443 192.168.1.5   # scan remote host's ports
```

> `0.0.0.0:80` = listening on all interfaces (external access). `127.0.0.1:7789` = localhost only (internal).

---

### Q467. How do you SSH into a server?

```bash
ssh -i ~/Downloads/mykey.pem ec2-user@54.23.45.67
chmod 400 mykey.pem              # required permission for key files
```

| Distro | Default AWS username |
|---|---|
| Amazon Linux | `ec2-user` |
| Ubuntu | `ubuntu` |
| CentOS / RHEL | `centos` / `ec2-user` |
| Debian | `admin` |

**Jump through a bastion:**
```bash
ssh -J ec2-user@bastion-ip ec2-user@private-ip
```

**SSH config shortcut** (`~/.ssh/config`):
```
Host myserver
  HostName 54.23.45.67
  User ec2-user
  IdentityFile ~/.ssh/mykey.pem
```
Then just `ssh myserver`.

**Common errors:** "Permission denied (publickey)" → wrong user/key; "Connection refused" → SSH down or port blocked; "Connection timed out" → firewall/wrong IP.

---

### Q468. Copy files securely between servers

```bash
scp -i key.pem app.war ec2-user@54.23.45.67:/opt/tomcat/webapps/    # local → remote
scp -i key.pem ec2-user@54.23.45.67:/var/log/app.log ./              # remote → local
scp -r ./mydir user@remote:/destination/                             # recursive
rsync -av --progress ./project ec2-user@server:/opt/                 # better for dirs, resumable
```

**`scp` vs `rsync`:** scp is simple for single files; rsync is better for directories (resumes, syncs, `-z` compresses).

**SFTP (interactive):**
```bash
sftp user@hostname
# ls, get file.txt, put local.txt, exit
```

---

### Q469. Allow a port through UFW firewall

```bash
sudo ufw enable
sudo ufw allow 22              # SSH
sudo ufw allow 80/tcp          # HTTP, TCP only
sudo ufw allow from 192.168.1.100 to any port 22   # restrict by source IP
sudo ufw deny 8080             # block a port
sudo ufw delete allow 7789     # remove a rule
```

**Typical setup:**
```bash
sudo ufw allow 22    # SSH admin access
sudo ufw allow 80    # public Apache
sudo ufw deny 7789   # Tomcat 1 — internal only
sudo ufw deny 8888   # Tomcat 2 — internal only
sudo ufw deny 5432   # PostgreSQL — internal only
```

---

### Q470. Check firewall rules

```bash
sudo ufw status verbose
sudo ufw status numbered        # for deleting specific rules

sudo iptables -L -v             # underlying firewall, verbose
sudo firewall-cmd --list-all    # RHEL/CentOS (firewalld)

nc -zv server-ip 7789           # is a port reachable externally?
nmap -p 7789 server-ip          # port scan
```

---

## Scripting

### Q471. What is a shell script?

A text file containing a sequence of Linux commands executed automatically, instead of typing them manually each time.

```bash
#!/bin/bash
apt update
apt install -y nginx
systemctl start nginx
systemctl enable nginx
echo "nginx installed!"
```

**Why:** automation, consistency, scheduling (cron), error handling, logging.

---

### Q472. How do you make a shell script executable?

```bash
chmod +x deploy.sh
./deploy.sh
```

**Full workflow:**
```bash
nano deploy.sh          # 1. create
chmod +x deploy.sh      # 2. make executable
./deploy.sh             # 3. run
```

**Alternative without chmod:**
```bash
bash deploy.sh          # explicitly invoke the interpreter
```

---

### Q473. What is a shebang line?

The first line of a script (`#!/bin/bash`) telling the OS which interpreter to use.

| Shebang | Interpreter |
|---|---|
| `#!/bin/bash` | Bash — most common, full features |
| `#!/bin/sh` | POSIX shell — more portable, fewer features |
| `#!/usr/bin/env python3` | Python 3 |
| `#!/usr/bin/env node` | Node.js |

Without a shebang the system has to guess the interpreter, which may pick wrong — always include one.

---

### Q474. How do you define a variable in a shell script?

```bash
NAME="Akhil"           # NO spaces around =
PORT=7789
echo "Port is: $PORT"
echo "${NAME}'s port"  # {} needed when followed directly by text
```

⚠️ `NAME = "Akhil"` (with spaces) is a syntax error.

```bash
TODAY=$(date)                 # command substitution
readonly MAX_RETRIES=5        # read-only variable
export DB_HOST="localhost"    # environment variable (available to child processes)
```

---

### Q475. How do you write an if-else in a shell script?

```bash
FILE="/opt/tomcat1/webapps/myapp.war"

if [ -f "$FILE" ]; then
  echo "WAR file exists! Deploying..."
else
  echo "ERROR: WAR file not found!"
  exit 1
fi
```

**Comparison operators:**

| Category | Operators |
|---|---|
| String | `==` `!=` `-z` (empty) `-n` (not empty) |
| Numbers | `-eq` `-ne` `-gt` `-lt` `-ge` `-le` |
| Files | `-f` (exists, file) `-d` (exists, dir) `-e` (exists) `-r`/`-w`/`-x` (readable/writable/executable) |

**Example — service check:**
```bash
if systemctl is-active nginx > /dev/null 2>&1; then
  echo "nginx is running"
else
  systemctl start nginx
fi
```

---

### Q476. How do you write a for loop in a shell script?

```bash
for item in item1 item2 item3; do echo "$item"; done
for i in 1 2 3 4 5; do echo "$i"; done
for ((i=1; i<=5; i++)); do echo "$i"; done       # C-style
for file in /opt/tomcat1/logs/*.log; do echo "$file"; done
```

**Deploy to multiple Tomcats:**
```bash
#!/bin/bash
TOMCAT_HOMES=("/opt/tomcat1" "/opt/tomcat2")
WAR_FILE="target/myapp.war"

for TOMCAT in "${TOMCAT_HOMES[@]}"; do
  cp $WAR_FILE $TOMCAT/webapps/
  $TOMCAT/bin/shutdown.sh
  sleep 3
  $TOMCAT/bin/startup.sh
  echo "Deployed to $TOMCAT ✅"
done
```

---

### Q477. What is a cron job and how do you schedule one?

A cron job runs a script automatically at a scheduled time, managed by the cron daemon.

```bash
crontab -e       # edit current user's crontab
crontab -l       # list
crontab -r       # remove
```

```bash
0 2 * * * /scripts/backup.sh >> /var/log/backup.log 2>&1   # daily at 2 AM, log output
*/5 * * * * /scripts/monitor.sh                              # every 5 minutes
0 9 * * 1 /scripts/weekly_report.sh                          # every Monday 9 AM
```

**System-wide locations:** `/etc/crontab`, `/etc/cron.d/`, `/etc/cron.{daily,weekly,monthly}/`

---

### Q478. Cron syntax — each field explained

```
MINUTE  HOUR  DAY  MONTH  DAYOFWEEK  command
 0-59   0-23  1-31  1-12    0-7        
```

- `*` = every value · `*/n` = every n · `n,m` = specific values · `n-m` = range
- Day of week: `0` or `7` = Sunday, `1` = Monday, ... `5` = Friday

| Expression | Meaning |
|---|---|
| `0 2 * * *` | Every day at 2:00 AM |
| `30 6 * * 1-5` | Weekdays at 6:30 AM |
| `0 0 1 * *` | First of every month, midnight |
| `*/15 * * * *` | Every 15 minutes |
| `0 9,17 * * 1-5` | Weekdays at 9 AM and 5 PM |

> Tool: **crontab.guru** — paste an expression, get a plain-English explanation.

---

## Linux Scenario Questions

### Q479. Disk is at 95% — walk through fixing it

```bash
# 1. Confirm
df -h

# 2. Find the biggest offender (drill down)
du -sh /* 2>/dev/null | sort -rh | head -10
du -sh /var/* | sort -rh | head -10
du -sh /var/log/* | sort -rh | head -10

# 3. Inspect
ls -lh /var/log/apache2/

# 4. Clean up
rm -rf /var/log/apache2/*.gz          # old compressed logs
rm -rf /var/log/apache2/*.1           # rotated logs
> /var/log/apache2/access.log         # truncate an ACTIVE log (don't rm it!)
docker system prune -a                # unused docker data
apt clean                             # package cache

# 5. Verify
df -h
```

**Prevent recurrence:** configure `logrotate`, set a disk-usage alarm (e.g. CloudWatch), schedule a weekly cleanup cron job.

---

### Q480. A service is not starting — how do you debug it?

```bash
sudo systemctl status nginx           # 1. status + exit code
sudo journalctl -u nginx -n 50        # 2. detailed systemd logs
tail -f /var/log/nginx/error.log      # 3. service-specific log
nginx -t                              # 4. test config syntax
sudo nginx -g "daemon off;"           # 5. run in foreground to see errors directly
ss -tulpn | grep :80                  # 6a. port conflict?
ls -la /var/run/nginx/                # 6b. permission issue?
```

Fix the root cause, then:
```bash
sudo systemctl start nginx
sudo systemctl status nginx      # confirm running
```

---

### Q481. Application using too much CPU — find and fix

```bash
top                                     # 1. confirm high CPU
ps aux --sort=-%cpu | head -10          # 2. find the process
ps -p 1234 -o pid,ppid,%cpu,%mem,cmd    # 3. inspect it
lsof -p 1234 | head -20                 # check open files (I/O clues)
tail -f catalina.out | grep -i "error\|exception\|loop"   # 4. app logs
```

**Fix based on cause:**
- Infinite loop / bug → restart service, flag for a code fix
- Too much traffic → scale out / add a load balancer
- Slow query → check DB slow-query logs
- Runaway background job → `kill -9`, then fix the job

```bash
/opt/tomcat1/bin/shutdown.sh
sleep 5
/opt/tomcat1/bin/startup.sh
```

---

### Q482. Cannot SSH into a server — what do you check?

```bash
ping google.com                    # 1. is it YOUR internet/VPN?
ping server-ip                     # 2. is the server reachable at all?
nc -zv server-ip 22                # 3. is port 22 open?
```

- "Connection refused" → SSH service not running
- "Connection timed out" → firewall blocking the port

```bash
systemctl status sshd              # 4. (via console access) is sshd running?
sudo ufw status                    # 5a. local firewall allows 22?
# 5b. Cloud security group inbound rules allow port 22 from your IP?
ls -la mykey.pem                   # 6. key perms must be 400/600
chmod 400 mykey.pem
ssh -vvv -i mykey.pem ec2-user@ip  # 7. verbose output for exact failure point
```

**Most common causes:** missing security-group rule, wrong key/permissions, wrong username, sshd not running, source IP changed.

---

### Q483. A user cannot run sudo commands — what do you check?

```bash
groups akhil                       # 1. is user in sudo/wheel group?
sudo usermod -aG sudo akhil        # 2. Ubuntu — add if missing
sudo usermod -aG wheel akhil       #    RHEL — add if missing
```

⚠️ User must **log out and back in** — or use `su - akhil` for an immediate refresh.

```bash
groups                             # 3. verify after re-login
sudo whoami                        # should return "root"
sudo visudo                        # 4. check sudoers has %sudo or %wheel entry
grep -E "^%sudo|^%wheel" /etc/sudoers
```

> Adding a user to `wheel` on an Ubuntu box does nothing — check which group the distro actually expects.

---

### Q484. Server is slow — first thing to check?

```bash
top     # or htop — instant overview of everything
```

| Look at | Meaning |
|---|---|
| Load average | if higher than CPU core count → overloaded |
| `%Cpu(s)` | near 100% → CPU-bound issue |
| Memory | near-zero free/available → RAM pressure, possible swapping |
| Top process | usually points straight at the culprit |

**Follow-up checks based on what you find:**
```bash
ps aux --sort=-%cpu | head -5    # high CPU
free -h                          # memory/swap
iostat -x 2                      # disk I/O
ss -tulpn                        # unusual connections
```

---

### Q485. Find all log files modified in the last 7 days

```bash
find /var/log -name "*.log" -mtime -7
```
- `-mtime -7` = modified less than 7 days ago
- `-mtime +7` = modified more than 7 days ago

```bash
find /var/log -name "*.log" -mtime -1                 # last 24 hours
find /var/log -name "*.log" -mmin -60                  # last 60 minutes
find /var/log -name "*.log" -mtime +30 -delete         # delete logs older than 30 days
find /var/log -name "*.log" -mtime +7 -exec gzip {} \; # compress older logs
find /var/log -name "*.log" -mtime -7 -ls | sort -k7 -rn | head -10   # sort by size
```

---

*End of Q411–Q485*
