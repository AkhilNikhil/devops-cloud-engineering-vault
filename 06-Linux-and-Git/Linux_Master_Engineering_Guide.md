# 🐧 Linux Systems & Networking: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers OS Kernel Architecture, Process Hierarchy, File Permissions, Modern Networking (`ss`/`ip`), Computer Networking Fundamentals (OSI, TCP/IP, DNS), Bash Strict Mode, and Performance Triage.

---

## 📑 Table of Contents
- [Linux Operating System Architecture](#linux-architecture)
- [File System Hierarchy & Permissions (Octal 755/644, SUID/SGID)](#file-system--permissions)
- [Process Management & Lifecycle (Zombies vs Orphans, Signals)](#process-management)
- [System Performance Diagnosis (CPU Load, Available RAM, Disk I/O)](#system-performance)
- [Modern System Administration & systemd Services](#systemd-services)
- [Computer Networking Fundamentals (OSI 7 Layers, TCP 3-Way Handshake, DNS)](#networking-fundamentals)
- [Modern Networking Command Cheat Sheet (`ss` vs `netstat`)](#networking-commands)
- [Production Bash Shell Scripting Blueprint](#bash-scripting)
- [Troubleshooting Playbook & Senior Interview Q&A](#troubleshooting-playbook)

---

# PART 1: LINUX SYSTEMS ADMINISTRATION

SECTION 6: LINUX — COMPLETE GUIDE
Flow: Introduction → Distributions → Structure → Shell → File System → Commands → Users & Groups →
Permissions → Compression → Filters → Networking → Advanced
1. What is Linux?
Definition:
Linux is a free, open-source Unix-like operating system kernel created by Linus Torvalds in 1991. It is the
foundation of most servers, cloud infrastructure, containers, and DevOps tooling in the world.
Key Features:
Open Source — source code is freely available, anyone can modify and distribute
Multi-user — multiple users can log in and work simultaneously
Multi-tasking — runs multiple processes at the same time
Secure — strong permission model, less vulnerable to viruses
Stable — servers run for years without rebooting
Portable — runs on almost any hardware
Shell/CLI — powerful command-line interface for automation
Free — no licensing cost (huge for DevOps at scale)
Why DevOps uses Linux:
Most cloud servers (AWS EC2, Azure VMs) run Linux
Docker containers use Linux kernel
Most DevOps tools (Jenkins, Kubernetes, Terraform) run natively on Linux
Shell scripting enables powerful automation




2. Linux Distributions (Distros)
A Linux distribution = Linux kernel + package manager + default software + UI
Distribution Package Manager Used For
Ubuntu apt Most popular, DevOps, beginners
RHEL (Red Hat) yum / dnf Enterprise production servers
CentOS yum / dnf Free RHEL alternative (deprecated)
Amazon Linux yum / dnf AWS EC2 instances
Debian apt Stable servers
Alpine apk Docker base images (tiny, ~5MB)
Kali Linux apt Security/penetration testing
Fedora dnf Cutting edge features
For your resume: You used Ubuntu and RHEL — mention both in interviews.
3. Linux Architecture / Structure
Hardware (CPU, RAM, Disk, Network)
         ↑
       Kernel  (core of OS — manages hardware, memory, processes)
         ↑
   System Libraries (glibc, etc.)
         ↑
      Shell  (command interpreter — bash, sh, zsh)
         ↑
   Applications / User Programs
         ↑
       User
Components explained:




Kernel — the brain of Linux. Manages CPU, memory, I/O, processes, networking. You never interact with it
directly.
Shell — the interface between you and the kernel. You type commands → shell interprets → kernel
executes.
System Libraries — pre-written functions that programs use to talk to the kernel.
User Space — where all applications run (your programs, services, tools).
4. Linux Shell
What is a Shell?
A shell is a command-line interpreter. You type commands, it passes them to the kernel for execution.
Types of Shells:
Shell Description
bash Bourne Again Shell — most common, default on Ubuntu/RHEL
sh Original Bourne Shell
zsh Extended bash with better features, popular on Mac
fish User-friendly shell with autocomplete
ksh Korn Shell — used in some enterprise environments
Check your shell:
echo $SHELL          # shows current shell path
echo $0              # shows current shell name
cat /etc/shells      # list all installed shells
chsh -s /bin/zsh     # change default shell
Shell Prompt:
devops@server:~$
  │      │    │ └── $ = normal user, # = root user
  │      │    └──── ~ = home directory
  │      └───────── hostname
  └──────────────── username




5. Linux File System Structure
Everything in Linux is a file. The filesystem starts from root / .
/                    ← Root — top of entire filesystem
├── bin/             ← Essential binaries (ls, cp, mv, cat)
├── sbin/            ← System binaries (only root uses: fdisk, mount)
├── etc/             ← Configuration files (nginx.conf, passwd, hosts)
├── home/            ← User home directories (/home/devops)
├── root/            ← Root user's home directory
├── var/             ← Variable data (logs, databases, mail)
│   └── log/         ← System and application logs
├── tmp/             ← Temporary files (cleared on reboot)
├── usr/             ← User programs and utilities
│   ├── bin/         ← Most user commands
│   └── local/       ← Locally installed software
├── opt/             ← Optional/third-party software
├── dev/             ← Device files (disks, terminals)
├── proc/            ← Virtual filesystem — running processes info
├── sys/             ← Virtual filesystem — kernel/hardware info
├── mnt/             ← Temporary mount points
├── media/           ← Removable media (USB, CD)
├── boot/            ← Boot loader files (kernel, grub)
└── lib/             ← Shared libraries
Key directories to remember:
/etc  — ALL config files live here
/var/log  — ALL logs live here
/home  — user files
/tmp  — temporary, cleared on reboot
/proc  — real-time system info (not real files)
6. Types of File Systems
File System Description Used On
ext4 Most common Linux filesystem, journaling Ubuntu, Debian EC2




xfs High performance, large files RHEL, Amazon Linux EC2
btrfs Modern, snapshots, RAID support Advanced Linux
NTFS Windows filesystem Windows (readable on Linux)
FAT32 Universal, USB drives USB drives
tmpfs In-memory filesystem /tmp on modern Linux
NFS Network File System — share files over network Shared storage
EFS AWS Elastic File System (NFS-based) AWS shared storage
7. Absolute Path vs Relative Path
Absolute Path:
Always starts from root /
Full path regardless of where you are
Example: /home/devops/projects/app.js
Relative Path:
Starts from your current location
Uses .  (current dir) and ..  (parent dir)
Example: ./projects/app.js  or ../etc/nginx.conf
# You are in /home/devops/
cd /etc/nginx          # absolute — goes from root
cd ../etc/nginx        # relative — goes up one level then to etc/nginx
cd ./projects          # relative — goes into projects in current dir
# Special symbols
.     # current directory
..    # parent directory
~     # home directory of current user
-     # previous directory
/     # root directory
# Examples
cd ~                   # go to home directory




cd -                   # go to previous directory
cd ../..               # go up two levels
8. File System Commands
Navigation
pwd                          # print working directory (where am I?)
ls                           # list files
ls -l                        # long format (permissions, owner, size, date)
ls -a                        # show hidden files (starting with .)
ls -la                       # long format + hidden files
ls -lh                       # human readable file sizes
ls -lt                       # sort by modification time
ls -R                        # list recursively
Create Files and Directories
touch filename.txt           # create empty file or update timestamp
touch file1 file2 file3      # create multiple files
mkdir dirname                # create directory
mkdir -p a/b/c               # create nested directories (parents)
mkdir -p project/{src,tests,docs}  # create multiple subdirs at once
Copy — cp
cp file1 file2               # copy file1 to file2
cp file1 /path/to/dir/       # copy file to directory
cp -r dir1 dir2              # copy directory recursively
cp -p file1 file2            # copy and preserve permissions/timestamps
cp -i file1 file2            # interactive — ask before overwrite
cp -v file1 file2            # verbose — show what's being copied
cp *.txt /backup/            # copy all txt files to backup
Move / Rename — mv




mv file1 file2               # rename file1 to file2
mv file1 /path/to/dir/       # move file to directory
mv dir1 dir2                 # rename directory
mv -i file1 file2            # ask before overwrite
mv -v file1 file2            # verbose
mv *.log /var/log/archive/   # move all log files
Delete — rm
rm filename                  # delete file
rm -i filename               # ask before delete
rm -f filename               # force delete, no prompt
rm -r dirname                # delete directory recursively
rm -rf dirname               # force delete directory (DANGEROUS — no undo)
rm *.tmp                     # delete all .tmp files
View File Content
cat filename                 # print entire file
cat -n filename              # with line numbers
less filename                # scroll through file (q to quit)
more filename                # page through file
head filename                # first 10 lines
head -n 20 filename          # first 20 lines
tail filename                # last 10 lines
tail -n 20 filename          # last 20 lines
tail -f /var/log/syslog      # follow log in real time (VERY useful for DevOps)
File Information
file filename                # what type of file is it?
stat filename                # detailed file info (size, permissions, timestamps)
wc filename                  # count lines, words, characters
wc -l filename               # count lines only
du -sh dirname               # disk usage of directory (human readable)
du -sh *                     # disk usage of all items in current dir
df -h                        # disk space of all mounted filesystems
Links




 
ln file1 hardlink            # create hard link (same inode)
ln -s file1 symlink          # create symbolic (soft) link (like a shortcut)
ls -l                        # symlinks shown with ->
readlink symlink             # show where symlink points
9. How to Add a Volume to an EC2 Instance
This is a common DevOps task — adding extra storage to your EC2 instance.
Step 1 — Create and Attach EBS Volume (AWS Console or CLI)
# Using AWS CLI:
aws ec2 create-volume --size 20 --availability-zone us-east-1a --volume-type gp3
aws ec2 attach-volume --volume-id vol-xxxxxxxx --instance-id i-xxxxxxxx --device /dev/
Step 2 — SSH into your EC2 instance and verify disk is attached
lsblk                        # list all block devices — you should see xvdf
fdisk -l                     # detailed disk info
Step 3 — Format the Volume with a File System
mkfs.ext4 /dev/xvdf          # format with ext4
# OR
mkfs.xfs /dev/xvdf           # format with xfs (for RHEL/Amazon Linux)
Step 4 — Create a Mount Point and Mount
mkdir /data                  # create directory to mount to
mount /dev/xvdf /data        # mount volume to /data
df -h                        # verify it's mounted
Step 5 — Make it Persistent (survive reboots)




# Get UUID of the volume
blkid /dev/xvdf
# Output: /dev/xvdf: UUID="abc123..." TYPE="ext4"
# Add to /etc/fstab for auto-mount on reboot
echo "UUID=abc123...  /data  ext4  defaults,nofs  0  2" >> /etc/fstab
# Test fstab entry
mount -a                     # mount all entries in fstab
df -h                        # verify
Unmount
umount /data                 # unmount volume
umount -l /data              # lazy unmount (if busy)
10. System Commands
System Information
uname -a                     # all system info (kernel, hostname, arch)
uname -r                     # kernel version only
hostname                     # show hostname
hostnamectl                  # detailed hostname and OS info
hostnamectl set-hostname newname   # change hostname permanently
cat /etc/os-release          # OS details (name, version)
lscpu                        # CPU info
free -h                      # RAM usage (human readable)
uptime                       # how long system has been running
whoami                       # current logged in user
id                           # user ID, group ID, groups
w                            # who is logged in and what they're doing
last                         # login history
Date and Time — timedatectl
date                         # current date and time
date "+%Y-%m-%d %H:%M:%S"   # formatted date




 
timedatectl                  # detailed time info including timezone
timedatectl list-timezones   # list all timezones
timedatectl set-timezone Asia/Kolkata   # set timezone (for India)
timedatectl set-ntp true     # enable NTP time sync
hwclock                      # hardware clock time
Process Management
ps                           # processes of current terminal
ps aux                       # all running processes (a=all, u=user, x=no terminal)
ps aux | grep nginx          # find specific process
top                          # live process monitor (q to quit)
htop                         # better live monitor (install separately)
kill PID                     # send SIGTERM (graceful stop) to process
kill -9 PID                  # send SIGKILL (force stop) — cannot be ignored
kill -15 PID                 # send SIGTERM explicitly
killall nginx                # kill all processes named nginx
pkill nginx                  # kill by name pattern
pgrep nginx                  # find PID of process by name
nohup command &              # run command that survives logout
jobs                         # list background jobs
bg %1                        # put job 1 in background
fg %1                        # bring job 1 to foreground
Service Management — systemctl
systemctl start nginx        # start service
systemctl stop nginx         # stop service
systemctl restart nginx      # restart service
systemctl reload nginx       # reload config without restart
systemctl status nginx       # check service status
systemctl enable nginx       # start on boot
systemctl disable nginx      # don't start on boot
systemctl is-active nginx    # is it running?
systemctl is-enabled nginx   # is it enabled on boot?
systemctl list-units --type=service   # list all services
journalctl -u nginx          # view logs for specific service
journalctl -u nginx -f       # follow logs for service
journalctl -n 50             # last 50 log lines
Package Management




# Ubuntu/Debian (apt)
apt update                   # update package list
apt upgrade                  # upgrade all packages
apt install nginx            # install package
apt remove nginx             # remove package
apt purge nginx              # remove package + config files
apt search nginx             # search for package
dpkg -l                      # list installed packages
# RHEL/CentOS/Amazon Linux (yum/dnf)
yum update                   # update all packages
yum install nginx            # install package
yum remove nginx             # remove package
yum search nginx             # search package
yum list installed           # list installed packages
dnf install nginx            # same but newer (dnf replaces yum)
11. User Management Commands
Linux has three types of users:
Root — superuser, UID 0, full access
System users — created by services (nginx, mysql), UID 1-999
Regular users — human users, UID 1000+
# User info files
cat /etc/passwd              # list of all users (username:x:UID:GID:info:home:shell)
cat /etc/shadow              # encrypted passwords (root only)
# Create user
useradd devops                          # create user (no home dir by default on some d
useradd -m devops                       # create user WITH home directory
useradd -m -s /bin/bash devops          # with home dir and bash shell
useradd -m -u 1500 devops              # with specific UID
useradd -m -g devops devops            # with primary group
useradd -m -G docker,sudo devops       # with supplementary groups
# Set/change password
passwd devops                           # set password for user
passwd                                 # change your own password
passwd -l devops                        # lock user account
passwd -u devops                        # unlock user account
passwd -e devops                        # force password change on next login




 
# Modify user
usermod -s /bin/zsh devops             # change shell
usermod -d /home/newdir devops         # change home directory
usermod -aG docker devops              # add user to docker group (a = append, G = grou
usermod -aG sudo devops                # give user sudo access
usermod -L devops                      # lock user
# Delete user
userdel devops                          # delete user (keeps home dir)
userdel -r devops                       # delete user AND home directory
# Switch user
su devops                               # switch to devops (need devops's password)
su -                                   # switch to root
sudo command                           # run single command as root
sudo su                                # become root using your password
sudo -u devops command                  # run command as another user
# View who is logged in
who                                    # logged in users
w                                      # logged in users + what they're doing
id devops                               # show UID, GID, groups of user
finger devops                           # user info (if installed)
12. Group Management Commands
Groups allow you to manage permissions for multiple users at once.
# Group info file
cat /etc/group               # list all groups (groupname:x:GID:members)
# Create group
groupadd devops              # create group
groupadd -g 2000 devops      # create group with specific GID
# Modify group
groupmod -n newname devops   # rename group
groupmod -g 2001 devops      # change GID
# Delete group
groupdel devops              # delete group
# Add/remove user from group




usermod -aG devops devops     # add devops to devops group
gpasswd -a devops devops      # add devops to devops group
gpasswd -d devops devops      # remove devops from devops group
# View groups
groups                       # groups current user belongs to
groups devops                 # groups a specific user belongs to
id devops                     # UID, GID, all groups
# Primary vs Secondary groups
# Primary group: default group assigned when user creates files
# Secondary groups: additional groups for extra permissions
13. File Permissions
Every file has three permission sets:
-rwxrwxrwx  1  devops  devops  4096  Jan 1  file.txt
│└──┘└──┘└──┘
│  │   │   └── others (everyone else)
│  │   └─────── group
│  └─────────── owner (user)
└────────────── file type (- = file, d = directory, l = symlink)
Permission types:
Symbol Number Meaning On File On Directory
r 4 read view content list files
w 2 write modify content create/delete files
x 1 execute run as program enter directory (cd)
- 0 no permission — —
Numeric (Octal) representation:
rwx = 4+2+1 = 7
rw- = 4+2+0 = 6
r-x = 4+0+1 = 5
r-- = 4+0+0 = 4




 
--- = 0+0+0 = 0
# Examples:
755 = rwxr-xr-x  (owner: all, group: read+execute, others: read+execute)
644 = rw-r--r--  (owner: read+write, group: read, others: read)
600 = rw-------  (owner: read+write, nobody else)
777 = rwxrwxrwx  (everyone full access — DANGEROUS, avoid in production)
chmod — Change Permissions
# Numeric mode
chmod 755 script.sh          # rwxr-xr-x
chmod 644 config.txt         # rw-r--r--
chmod 600 private.key        # rw------- (SSH keys must be 600)
chmod 777 file               # AVOID in production
chmod -R 755 /var/www/       # recursive — apply to all files in directory
# Symbolic mode
chmod u+x script.sh          # add execute for owner (u=user, g=group, o=others, a=all
chmod g+w file.txt           # add write for group
chmod o-r file.txt           # remove read for others
chmod a+r file.txt           # add read for everyone
chmod u=rwx,g=rx,o=r file   # set exact permissions
chown — Change Owner
chown devops file.txt             # change owner to devops
chown devops:devops file.txt      # change owner AND group
chown :devops file.txt           # change group only
chown -R devops:devops /var/www/  # recursive change
chgrp — Change Group
chgrp devops file.txt            # change group of file
chgrp -R devops /project/        # recursive
umask — Default Permission Mask




umask                            # show current umask (usually 022)
umask 022                        # set umask
# umask 022 means new files get 644, new directories get 755
# 666 (file default) - 022 = 644
# 777 (dir default)  - 022 = 755
Special Permissions
# SUID (Set User ID) — run file as owner, not as executor
chmod u+s script.sh          # sets SUID
chmod 4755 script.sh         # numeric
# SGID (Set Group ID) — files inherit group of directory
chmod g+s /shared/           # sets SGID on directory
chmod 2755 /shared/          # numeric
# Sticky Bit — only owner can delete their files in shared dir (like /tmp)
chmod +t /shared/            # sets sticky bit
chmod 1777 /tmp              # numeric (t shown as T if no execute)
# View special permissions
ls -l                        # s in execute position = SUID/SGID, t = sticky
14. ACL — setfacl and getfacl
What is ACL?
Standard Linux permissions only allow one owner and one group per file. ACL (Access Control List) gives you
fine-grained control — set different permissions for multiple users and groups on the same file.
# Install ACL if needed
apt install acl              # Ubuntu
yum install acl              # RHEL
# Check if ACL is supported
mount | grep acl             # look for 'acl' in mount options
# getfacl — view ACL of a file
getfacl filename.txt
# Output:
# file: filename.txt




# owner: devops
# group: devops
# user::rw-
# group::r--
# other::r--
# setfacl — set ACL
setfacl -m u:john:rwx file.txt       # give john rwx on file
setfacl -m u:jane:r-- file.txt       # give jane read only
setfacl -m g:qa:rx /testdir/         # give qa group rx on directory
setfacl -R -m u:john:rwx /project/  # recursive ACL
setfacl -x u:john file.txt           # remove ACL for john
setfacl -b file.txt                  # remove ALL ACLs from file
# Default ACL (inherited by new files in directory)
setfacl -d -m u:john:rwx /shared/   # any new file in /shared gets john's ACL
# Mask — limits effective permissions
setfacl -m m:rx file.txt            # set mask to rx (limits group + named users)
15. File Compression and Archiving
tar — Tape Archive (most common in Linux)
# Create archive
tar -cvf archive.tar files/          # create tar (c=create, v=verbose, f=file)
tar -czvf archive.tar.gz files/      # create compressed tar.gz (z=gzip)
tar -cjvf archive.tar.bz2 files/     # create compressed tar.bz2 (j=bzip2)
tar -cJvf archive.tar.xz files/      # create compressed tar.xz (J=xz)
# Extract archive
tar -xvf archive.tar                 # extract tar
tar -xzvf archive.tar.gz             # extract tar.gz
tar -xzvf archive.tar.gz -C /path/  # extract to specific directory
# View contents without extracting
tar -tvf archive.tar                 # list contents
# Add to existing archive
tar -rvf archive.tar newfile.txt
# Memory trick: c=create, x=extract, t=list, v=verbose, f=filename, z=gzip




 
gzip / gunzip
gzip file.txt                        # compress — creates file.txt.gz, removes origina
gzip -k file.txt                     # compress, keep original
gzip -d file.txt.gz                  # decompress
gunzip file.txt.gz                   # decompress (same as gzip -d)
gzip -l file.txt.gz                  # show compression stats
gzip -9 file.txt                     # maximum compression
zip / unzip
zip archive.zip file1 file2         # zip files
zip -r archive.zip folder/          # zip directory recursively
unzip archive.zip                   # extract zip
unzip archive.zip -d /path/         # extract to specific directory
unzip -l archive.zip                # list contents
Other compression
bzip2 file.txt                      # compress with bzip2 (better ratio, slower)
bunzip2 file.txt.bz2                # decompress
xz file.txt                         # compress with xz (best ratio, slowest)
unxz file.txt.xz                    # decompress
16. Filter Commands and Regular Expressions
grep — Search Text
grep "pattern" file.txt              # search for pattern in file
grep -i "pattern" file.txt           # case insensitive
grep -r "pattern" /var/log/          # recursive search in directory
grep -n "pattern" file.txt           # show line numbers
grep -v "pattern" file.txt           # invert — show lines that DON'T match
grep -c "pattern" file.txt           # count matching lines
grep -l "pattern" *.txt              # list files that contain pattern
grep -w "word" file.txt              # match whole word only
grep -A 3 "pattern" file.txt         # show 3 lines After match




grep -B 3 "pattern" file.txt         # show 3 lines Before match
grep -E "pattern1|pattern2" file     # extended regex (OR)
grep "^start" file.txt               # lines starting with "start"
grep "end$" file.txt                 # lines ending with "end"
grep "^$" file.txt                   # empty lines
# Real DevOps examples:
grep "ERROR" /var/log/app.log              # find errors in log
grep -i "failed" /var/log/syslog           # find failures
ps aux | grep nginx                         # find nginx process
cat /etc/passwd | grep "/bin/bash"          # users with bash shell
Regular Expressions (Regex) Quick Reference
.       any single character
*       zero or more of previous
+       one or more of previous (use with -E)
?       zero or one of previous (use with -E)
^       start of line
$       end of line
[]      character class [abc] = a, b, or c
[^]     negated class [^abc] = not a, b, or c
|       OR (use with -E)
\       escape special character
{n}     exactly n times
{n,m}   between n and m times
# Examples:
grep "^[0-9]" file           # lines starting with digit
grep "[0-9]\{3\}" file       # exactly 3 digits
grep -E "error|fail" file    # lines with error OR fail
grep "\." file               # literal dot
awk — Pattern Scanning and Processing
awk '{print $1}' file.txt           # print first column
awk '{print $1, $3}' file.txt       # print columns 1 and 3
awk -F: '{print $1}' /etc/passwd    # use : as delimiter, print first field
awk 'NR==5' file.txt                # print line 5
awk 'NR>=5 && NR<=10' file.txt      # print lines 5 to 10
awk '/pattern/ {print}' file        # print lines matching pattern
awk '{print NR, $0}' file           # print with line numbers
awk '{sum+=$1} END {print sum}' f   # sum first column
df -h | awk '{print $1, $5}'        # print disk name and usage %




# Real example — get usernames from /etc/passwd
awk -F: '{print $1}' /etc/passwd
sed — Stream Editor
sed 's/old/new/' file.txt            # replace first occurrence per line
sed 's/old/new/g' file.txt           # replace ALL occurrences
sed 's/old/new/gi' file.txt          # replace all, case insensitive
sed -i 's/old/new/g' file.txt        # edit file IN PLACE (modifies actual file)
sed -i.bak 's/old/new/g' file.txt    # in place with backup (.bak)
sed '5d' file.txt                    # delete line 5
sed '/pattern/d' file.txt            # delete lines matching pattern
sed -n '5,10p' file.txt              # print lines 5 to 10 only
sed '5i\new line' file.txt           # insert line before line 5
sed '5a\new line' file.txt           # append line after line 5
sed 's/^/prefix/' file.txt           # add prefix to every line
sed 's/$/ suffix/' file.txt          # add suffix to every line
# Real DevOps example — update config file
sed -i 's/port=8080/port=80/' /etc/app.conf
cut — Cut Columns from Text
cut -d: -f1 /etc/passwd             # cut field 1 using : as delimiter
cut -d, -f2,4 data.csv              # cut fields 2 and 4 from CSV
cut -c1-10 file.txt                 # cut first 10 characters
cut -d' ' -f1 file.txt              # cut first word
sort — Sort Lines
sort file.txt                       # alphabetical sort
sort -r file.txt                    # reverse sort
sort -n file.txt                    # numerical sort
sort -u file.txt                    # sort and remove duplicates
sort -k2 file.txt                   # sort by second column
sort -t: -k3 -n /etc/passwd         # sort passwd by UID (field 3, numeric)
uniq — Remove Duplicates




uniq file.txt                       # remove consecutive duplicates
uniq -c file.txt                    # count occurrences
uniq -d file.txt                    # show only duplicates
sort file.txt | uniq                # sort first, then remove all duplicates
sort file.txt | uniq -c | sort -rn  # count and sort by frequency
tr — Translate Characters
tr 'a-z' 'A-Z' < file.txt          # lowercase to uppercase
tr -d '\n' < file.txt              # remove newlines
tr -s ' ' < file.txt               # squeeze multiple spaces into one
echo "hello" | tr 'a-z' 'A-Z'     # HELLO
wc — Word Count
wc file.txt                        # lines, words, characters
wc -l file.txt                     # count lines only
wc -w file.txt                     # count words only
wc -c file.txt                     # count bytes
ls | wc -l                         # count files in directory
17. Find and Locate Commands
find — Search Files in Real Time
# Basic find
find /path -name "filename"          # find by exact name
find /path -name "*.log"             # find by pattern
find /path -iname "*.Log"            # case insensitive name
find . -name "*.txt"                 # find in current directory
# Find by type
find /path -type f                   # files only
find /path -type d                   # directories only
find /path -type l                   # symbolic links only
# Find by size
find / -size +100M                   # files larger than 100MB




 
 
find / -size -1k                     # files smaller than 1KB
find / -size 50M                     # files exactly 50MB
# Find by time
find / -mtime -7                     # modified in last 7 days
find / -mtime +30                    # modified more than 30 days ago
find / -atime -1                     # accessed in last 24 hours
find / -newer file.txt               # files newer than file.txt
# Find by permissions
find / -perm 777                     # files with exactly 777
find / -perm /u+s                    # files with SUID set
# Find by owner
find /home -user devops               # files owned by devops
find /home -group devops             # files owned by devops group
# Find and execute action
find /tmp -name "*.tmp" -delete      # find and delete
find /var/log -name "*.log" -exec ls -lh {} \;   # find and run ls
find . -name "*.txt" -exec grep "error" {} \;    # find txt files and grep inside them
# Real DevOps examples:
find / -name "nginx.conf" 2>/dev/null          # find nginx config
find /var/log -name "*.log" -mtime +7 -delete  # delete logs older than 7 days
find / -perm /u+s -type f 2>/dev/null          # find all SUID files (security check)
locate — Fast File Search (uses database)
locate filename                      # fast search using pre-built database
locate "*.conf"                      # search by pattern
locate -i filename                   # case insensitive
locate -c filename                   # count results only
locate -n 10 filename                # show only 10 results
updatedb — Update locate Database
updatedb                             # update the locate database (run as root)
# locate uses a database built by updatedb — run this before locate if files are new
# updatedb runs automatically as a cron job daily




18. Piping and Redirection
Piping — | (pass output of one command to another)
# Pipe takes stdout of left command and feeds it as stdin to right command
ls -l | grep ".txt"                  # list files, filter for .txt
ps aux | grep nginx                  # find nginx processes
cat /etc/passwd | grep "/bin/bash"   # users with bash shell
df -h | grep "/dev/xvda"            # find specific disk
cat access.log | grep "ERROR" | wc -l   # count errors in log
cat /etc/passwd | cut -d: -f1 | sort    # sorted list of usernames
ps aux | sort -k3 -rn | head -5     # top 5 CPU-consuming processes
Redirection
# Output redirection
command > file.txt              # redirect stdout to file (OVERWRITES)
command >> file.txt             # redirect stdout to file (APPENDS)
command 2> error.txt            # redirect stderr to file
command 2>> error.txt           # append stderr to file
command > output.txt 2>&1       # redirect both stdout and stderr to file
command &> file.txt             # redirect both (shorthand)
command > /dev/null             # discard output (send to null)
command > /dev/null 2>&1        # discard all output
# Input redirection
command < file.txt              # use file as input
mysql -u root -p dbname < dump.sql   # import SQL dump
# Here document
cat << EOF > file.txt
This is line 1
This is line 2
EOF
# Pipe and redirection combined
grep "ERROR" /var/log/app.log | tail -100 > errors.txt   # save last 100 errors
ps aux | grep nginx | awk '{print $2}' | xargs kill      # kill nginx processes
19. Networking Commands




# Interface and IP info
ip addr                              # show all network interfaces and IPs
ip addr show eth0                    # show specific interface
ifconfig                             # older command (may need net-tools)
ip link                              # show link layer info
ip link set eth0 up                  # bring interface up
ip link set eth0 down                # bring interface down
# Routing
ip route                             # show routing table
ip route show                        # same
route -n                             # show routing table (older)
ip route add 192.168.1.0/24 via 10.0.0.1   # add static route
ip route del 192.168.1.0/24          # delete route
# DNS
nslookup google.com                  # DNS lookup
dig google.com                       # detailed DNS lookup
dig google.com A                     # lookup A record
dig google.com MX                    # lookup mail records
cat /etc/resolv.conf                 # DNS server config
cat /etc/hosts                       # local hostname resolution
# Connectivity
ping google.com                      # test connectivity (sends ICMP)
ping -c 4 google.com                 # ping 4 times then stop
ping -i 0.5 google.com               # ping every 0.5 seconds
traceroute google.com                # trace path to destination
mtr google.com                       # continuous traceroute
# Ports and Connections
netstat -tulpn                       # listening ports (t=tcp, u=udp, l=listening, p=p
ss -tulpn                            # same but faster (modern replacement for netstat
ss -s                                # socket statistics summary
lsof -i :80                          # what process is using port 80
lsof -i :8080                        # check specific port
netstat -an | grep ESTABLISHED       # active connections
# HTTP Requests
curl http://example.com              # basic HTTP GET
curl -I http://example.com           # headers only
curl -X POST -d '{"key":"val"}' -H "Content-Type: application/json" http://api
curl -o file.zip http://example.com/file.zip   # download file
curl -L http://example.com           # follow redirects
curl -u username:password http://api # basic auth
wget http://example.com/file.zip     # download file
wget -r http://example.com           # recursive download




# Firewall — UFW (Ubuntu)
ufw status                           # check firewall status
ufw enable                           # enable firewall
ufw disable                          # disable firewall
ufw allow 22                         # allow SSH
ufw allow 80/tcp                     # allow HTTP
ufw allow 443/tcp                    # allow HTTPS
ufw deny 8080                        # deny port 8080
ufw delete allow 8080               # remove rule
ufw allow from 192.168.1.0/24       # allow from subnet
# Firewall — iptables (lower level)
iptables -L                          # list all rules
iptables -A INPUT -p tcp --dport 80 -j ACCEPT    # allow port 80 in
iptables -A INPUT -p tcp --dport 22 -j ACCEPT    # allow SSH
iptables -A INPUT -j DROP            # drop everything else
iptables -F                          # flush (delete) all rules
# SSH
ssh devops@192.168.1.10               # SSH to server
ssh -i key.pem ec2-user@ip           # SSH with key (AWS EC2)
ssh -p 2222 user@host                # SSH on custom port
scp file.txt user@host:/path/        # copy file to remote server
scp user@host:/path/file.txt .       # copy file from remote server
scp -r folder/ user@host:/path/      # copy directory to remote
ssh-keygen -t rsa -b 4096            # generate SSH key pair
ssh-copy-id user@host                # copy public key to remote server
# Network performance
iperf3 -s                            # start iperf server
iperf3 -c server-ip                  # test bandwidth to server
nload                                # real-time network traffic monitor
nethogs                              # network usage per process
20. Environment Variables
# View variables
env                                  # show all environment variables
printenv                             # same
printenv PATH                        # show specific variable
echo $HOME                           # print variable value
echo $PATH                           # print PATH
# Set variables




 
export MYVAR="hello"                 # set and export variable (available to child pro
MYVAR="hello"                        # set but NOT exported (only in current shell)
export PATH=$PATH:/new/path          # add to PATH
# Permanent variables — add to ~/.bashrc or /etc/environment
echo 'export MYVAR="hello"' >> ~/.bashrc
source ~/.bashrc                     # reload bashrc
# Common environment variables
$HOME    # user's home directory
$PATH    # directories to search for commands
$USER    # current username
$SHELL   # current shell
$PWD     # current working directory
$EDITOR  # default text editor
$LANG    # system language
21. Text Editors
# vim (most important for DevOps)
vim filename                 # open file in vim
# vim modes:
# Normal mode  — default, navigate and run commands
# Insert mode  — press 'i' to enter, type text
# Command mode — press ':' to enter commands
# Essential vim commands:
i          # enter insert mode
Esc        # go back to normal mode
:w         # save file
:q         # quit (fails if unsaved changes)
:wq        # save and quit
:q!        # quit without saving (force)
:wq!       # save and quit (force)
dd         # delete current line
yy         # copy (yank) current line
p          # paste
u          # undo
Ctrl+r     # redo
/pattern   # search forward
n          # next search result
:%s/old/new/g  # replace all occurrences in file
gg         # go to top of file




G          # go to bottom of file
:set nu    # show line numbers
# nano (simpler editor)
nano filename                # open file
Ctrl+O                       # save
Ctrl+X                       # exit
Ctrl+W                       # search
Ctrl+K                       # cut line
Ctrl+U                       # paste
22. Log Management
# Important log files
/var/log/syslog              # general system logs (Ubuntu)
/var/log/messages            # general system logs (RHEL)
/var/log/auth.log            # authentication logs (Ubuntu)
/var/log/secure              # authentication logs (RHEL)
/var/log/kern.log            # kernel logs
/var/log/dmesg               # boot messages
/var/log/nginx/access.log    # nginx access log
/var/log/nginx/error.log     # nginx error log
/var/log/apache2/            # apache logs
# View logs
tail -f /var/log/syslog                  # follow live log
tail -100 /var/log/nginx/error.log       # last 100 lines
grep "ERROR" /var/log/app.log            # filter errors
grep "ERROR" /var/log/app.log | wc -l   # count errors
journalctl -f                            # follow systemd journal
journalctl -u nginx --since "1 hour ago" # nginx logs from last hour
journalctl --since "2024-01-01" --until "2024-01-02"  # date range
23. Shell Scripting Basics
#!/bin/bash                  # shebang — tells system to use bash
# Variables
NAME="DevOpsEngineer"




echo "Hello, $NAME"
# Input
read -p "Enter name: " NAME
# Conditions
if [ $NAME == "DevOpsEngineer" ]; then
    echo "Welcome DevOpsEngineer"
elif [ $NAME == "John" ]; then
    echo "Welcome John"
else
    echo "Unknown user"
fi
# Loops
for i in 1 2 3 4 5; do
    echo "Number: $i"
done
for file in *.txt; do
    echo "Processing: $file"
done
while [ condition ]; do
    # commands
done
# Functions
greet() {
    echo "Hello, $1"    # $1 = first argument
}
greet "DevOpsEngineer"
# Exit codes
echo $?          # 0 = success, non-zero = failure
exit 0           # exit script with success
exit 1           # exit script with failure
# Make script executable and run
chmod +x script.sh
./script.sh
bash script.sh
24. Quick Reference — Most Used Linux Commands




# NAVIGATION
pwd           cd           ls -la        cd ~
# FILE OPERATIONS
touch         mkdir -p     cp -r         mv           rm -rf
cat           less         head -n       tail -f      file
# PERMISSIONS
chmod 755     chown user:group    setfacl -m u:user:rwx    getfacl
# USER MANAGEMENT
useradd -m    passwd        usermod -aG    userdel -r
groupadd      gpasswd -a    groups         id
# PROCESSES
ps aux        top           kill -9       systemctl status
systemctl start/stop/restart/enable
# NETWORKING
ip addr       ping          curl          ss -tulpn
ufw allow     ssh           scp           dig
# SEARCH
grep -r       find / -name  locate        grep -i -n
awk           sed -i        cut           sort | uniq
# COMPRESSION
tar -czvf     tar -xzvf     zip -r        unzip        gzip
# DISK
df -h         du -sh        lsblk         mount        umount
mkfs.ext4     blkid
# LOGS
tail -f       journalctl -u    grep "ERROR"    /var/log/
TOPICS TO ADD NEXT
[ ] Terraform — complete guide
[ ] Azure DevOps — complete guide




[ ] Ansible — complete guide
[ ] AWS Scenario-based questions
[ ] Networking deep dive
Prepared for: DevOps & Cloud Engineer | DevOps & Cloud Engineer
Keep going — you're doing great!


---

# PART 2: COMPUTER NETWORKING FUNDAMENTALS

SECTION 10: NETWORKING FUNDAMENTALS —
COMPLETE GUIDE
Essential networking knowledge for DevOps interviews. Covers OSI, TCP/IP, DNS, DHCP, IP addressing, and
more.
1. Why Networking Matters for DevOps
As a DevOps engineer you deal with networking every day — configuring VPCs, setting up load balancers,
troubleshooting why services can't communicate, configuring security groups. Understanding networking
fundamentals makes you a much stronger engineer.
2. OSI Model — 7 Layers
OSI (Open Systems Interconnection) — a conceptual framework that breaks network communication into 7
layers, each with a specific function.
Layer 7 — Application    → HTTP, FTP, SMTP, Telnet       → Data
Layer 6 — Presentation   → JPEG, GIF, MPEG, ASCII        → Data
Layer 5 — Session        → Session setup/teardown         → Data
Layer 4 — Transport      → TCP, UDP                       → Segment
Layer 3 — Network        → IP, ICMP, ARP, OSPF, RIP       → Packet
Layer 2 — Data Link      → Ethernet, PPP, MAC addresses   → Frame
Layer 1 — Physical       → Cables, fiber, hubs            → Bit
Easy memory trick (top to bottom): All People Seem To Need Data Processing
Layer Name Purpose Key Protocols
7 Application Interface for apps to access network HTTP, FTP, SMTP, Telnet
6 Presentation Data formatting, encryption, compression JPEG, GIF, MPEG, ASCII
5 Session Establish, manage, terminate sessions NetBIOS, RPC
4 Transport Reliable/unreliable delivery, segmentation TCP, UDP




3 Network Logical addressing, routing packets IP, ICMP, ARP, OSPF
2 Data Link Node-to-node transfer, MAC addressing Ethernet, PPP
1 Physical Physical transmission of bits Cables, fiber, hubs
DevOps relevance:
Layer 4 — Load Balancers (ALB = Layer 7, NLB = Layer 4)
Layer 3 — Routing tables, VPC routing
Layer 7 — HTTP/HTTPS, application-level firewalls
3. TCP/IP Model — 4 Layers
A simplified, practical model used in real networking. Maps to OSI layers.
TCP/IP Layer          OSI Layers              Data Name
Application    =  Application + Presentation + Session   → Data
Transport      =  Transport                               → Segment
Internet       =  Network                                 → Packet
Network Access =  Data Link + Physical                    → Frame / Bit
TCP/IP Layer Key Protocols Function
Application HTTP, FTP, DNS, SMTP User-facing services
Transport TCP, UDP End-to-end delivery
Internet IP, ARP, ICMP Routing, logical addressing
Network Access Ethernet, MAC Physical transmission
4. TCP vs UDP
Both operate at Layer 4 (Transport Layer). Think of data as cars carrying packages — the difference is HOW
they ensure delivery.
Feature TCP UDP




Connection Connection-oriented (establishes connection
first)
Connectionless (no setup needed)
Reliability Reliable — guarantees delivery in order Unreliable — no guarantee
Acknowledgement Yes — confirms data received No
Speed Slower (overhead for reliability) Faster (no overhead)
Protocol number 6 17
Use case HTTP, FTP, SMTP, SSH DNS, DHCP, video streaming,
gaming
Why TCP is Reliable:
1. Acknowledgement — receiver confirms data received
2. Sequencing — data divided into numbered segments, receiver detects missing segments
3. Checksum — detects corruption during transmission
Why UDP is Unreliable but Fast:
No connection setup
No acknowledgements
No retransmission
Perfect for real-time streaming, gaming, DNS where speed > accuracy
5. TCP Three-Way Handshake
Process to establish a connection between client and server BEFORE data is sent.
Client                          Server
  │                               │
  │──── SYN ───────────────────── ▶ │  Step 1: Client says "I want to connect"
  │                               │
  │ ◀ ─── SYN-ACK ──────────────────│  Step 2: Server says "OK, I'm ready"
  │                               │
  │──── ACK ───────────────────── ▶ │  Step 3: Client confirms "Let's go"
  │                               │
  │ ←──── DATA FLOWS ──────────── ▶ │  Connection established!
SYN — Synchronize — client requests connection
SYN-ACK — Synchronize-Acknowledge — server acknowledges and signals readiness




 
ACK — Acknowledge — client confirms, connection established
6. DNS — Domain Name System
What is DNS?
DNS translates human-readable domain names (like google.com) into IP addresses (like 142.250.64.46) that
computers use to communicate.
You type: google.com
DNS resolves: 142.250.64.46
Browser connects to that IP
DNS Resolution Flow:
Browser → Local Cache → Hosts file → DNS Resolver → Root Server → TLD Server → Authori
Key DNS Commands:
nslookup google.com          # DNS lookup
dig google.com               # detailed DNS lookup
dig google.com A             # lookup A record (IPv4)
dig google.com MX            # lookup mail records
cat /etc/resolv.conf         # DNS server config
cat /etc/hosts               # local hostname resolution
7. ARP — Address Resolution Protocol
What is ARP?
ARP maps a device's IP address (Layer 3) to its MAC address (Layer 2). When a device wants to communicate
on the same local network, it uses ARP to find the recipient's MAC address.
Device A wants to talk to 192.168.1.10
ARP broadcast: "Who has 192.168.1.10?"




Device B replies: "I do! My MAC is AA:BB:CC:DD:EE:FF"
Device A sends data to that MAC
8. PING
PING uses ICMP (Internet Control Message Protocol) to test reachability of a host.
Sends echo request → waits for echo reply
Measures round trip time (RTT)
Tests connectivity and latency
ping google.com              # test connectivity
ping -c 4 google.com         # ping 4 times only
ping -i 0.5 google.com       # ping every 0.5 seconds
9. DHCP — Dynamic Host Configuration Protocol
What is DHCP?
DHCP automatically assigns IP addresses and network configuration (subnet mask, gateway, DNS) to devices.
Eliminates manual configuration.
DORA Process (how DHCP works):
Client                              DHCP Server
  │                                     │
  │── DISCOVER (broadcast) ──────────── ▶ │  "I need an IP address!"
  │                                     │
  │ ◀ ── OFFER (unicast) ─────────────────│  "How about 192.168.1.100?"
  │                                     │
  │── REQUEST (broadcast) ───────────── ▶ │  "Yes, I'll take that IP"
  │                                     │
  │ ◀ ── ACK (unicast) ───────────────────│  "It's yours! Here's your config"
  │                                     │
  │  IP assigned!  192.168.1.100        │
DORA = Discover → Offer → Request → Acknowledge
Why DHCP?




Automation — no manual IP assignment
Error Prevention — no duplicate IPs
Central Management — manage all IPs from one place
10. Network Performance Metrics
Metric Definition
Bandwidth Maximum rate data can transfer (bits per second). Capacity of the connection.
Latency Time for data to travel from source to destination. Lower = faster.
RTT (Round Trip Time) Time for packet to go to destination AND come back.
MTU (Max Transmission Unit) Largest packet size that can be transmitted (typically 1500 bytes on Ethernet).
Throughput Actual data transferred in a given time (vs bandwidth which is maximum).
Jitter Variation in latency over time. High jitter causes choppy audio/video.
11. IPv4 vs IPv6
IPv4 — 32-bit addresses, ~4.3 billion addresses. Running out!
IPv6 — 128-bit addresses, ~340 undecillion addresses. The future.
Feature IPv4 IPv6
Address Length 32 bits (4 octets) 128 bits (8 octets)
Format Decimal dots (192.168.0.1) Hex colons (2001:0db8::7334)
Total Addresses ~4.3 billion ~340 undecillion (2^128)
NAT Required Yes (to extend address space) No (enough addresses for all)
Security No built-in (needs IPsec) Built-in IPsec support
Configuration Manual or DHCP Auto-config (SLAAC) or DHCPv6
Broadcast Supported No broadcast (uses Multicast/Anycast)




 
Header Complex Simplified (faster processing)
12. IP Address Classes
Class A: 1.0.0.0    – 126.0.0.0    Mask: 255.0.0.0     Networks: 126      Hosts: 16,77
Class B: 128.0.0.0  – 191.0.0.0    Mask: 255.255.0.0   Networks: 16,384   Hosts: 65,53
Class C: 192.0.0.0  – 223.0.0.0    Mask: 255.255.255.0 Networks: 2,097,152 Hosts: 254
Special:
127.0.0.1        = Loopback (localhost)
255.255.255.255  = Broadcast
Private IP Ranges (not routable on internet):
Class A: 10.0.0.0    – 10.255.255.255
Class B: 172.16.0.0  – 172.31.255.255
Class C: 192.168.0.0 – 192.168.255.255
APIPA (Automatic Private IP Addressing):
If a device fails to get an IP from DHCP, it assigns itself an address in the 169.254.0.0/16 range. This allows
local communication but NOT internet access.
13. Common Ports and Protocols
Port Protocol Service
22 TCP SSH — secure remote access
23 TCP Telnet — insecure remote access
25 TCP SMTP — email sending
53 TCP/UDP DNS — domain name resolution
67/68 UDP DHCP — IP address assignment
80 TCP HTTP — web traffic
443 TCP HTTPS — secure web traffic




3306 TCP MySQL database
5432 TCP PostgreSQL database
6443 TCP Kubernetes API server
2379/2380 TCP etcd
10250 TCP kubelet API
8080 TCP HTTP alternate (Tomcat, Jenkins)
SSH vs Telnet:
SSH Telnet
Port 22 23
Encryption Yes No (plain text)
Security Secure Insecure
Use today Always preferred Never in production
14. Network Devices
Device OSI Layer How it works
Hub Layer 1 (Physical) Broadcasts all data to ALL ports. Dumb, no intelligence.
Switch Layer 2 (Data Link) Forwards data to SPECIFIC device using MAC address. Intelligent.
Router Layer 3 (Network) Routes packets between DIFFERENT networks using IP addresses.
Firewall Layer 3-7 Filters traffic based on rules. Permits or denies based on policies.
Hub vs Switch vs Router:
Hub:     A shouts → everyone hears (broadcast to all)
Switch:  A shouts → only B hears (targeted by MAC)
Router:  A sends to different city → router finds the path (routing by IP)
Can you replace a Router with a Switch?




No. They serve different purposes. Router = between networks (Layer 3). Switch = within a network (Layer 2).
Some Layer 3 switches can do limited routing but don't replace a full router.
15. NAT — Network Address Translation
What is NAT?
Converts private IP addresses to public IP addresses for internet access. Conserves public IPs and adds security
by hiding internal addresses.
Types of NAT:
Type How it works
Static NAT One private IP → one public IP (1:1 mapping)
Dynamic NAT Multiple private IPs → pool of public IPs
PAT (Port Address
Translation)
Multiple private IPs → ONE public IP using different ports. Also called NAT
overload. Most common.
AWS NAT Gateway works exactly like PAT — allows private subnet instances to access internet while blocking
inbound connections.
16. VLAN — Virtual Local Area Network
What is VLAN?
Logically segments a physical network into multiple virtual networks. Devices in different VLANs can't
communicate directly without routing.
Why use VLANs?
Security — isolate sensitive devices (HR network separate from Dev network)
Performance — reduce broadcast traffic by limiting to specific VLANs
Organization — logically structure network regardless of physical location
VLAN reduces broadcast traffic by dividing network into smaller broadcast domains. Traffic in VLAN 10
doesn't reach VLAN 20.
Access Port vs Trunk Port:




Access Port Trunk Port
VLANs Carries ONE VLAN Carries MULTIPLE VLANs
Use Connect end devices (PCs) Connect switches to switches/routers
VLAN tagging Removed before sending to device Maintains VLAN tags
17. VPN — Virtual Private Network
What is VPN?
Extends a private network over a public network (internet) using an encrypted tunnel. Allows secure
communication over untrusted networks.
VPN uses:
Encryption — protects data in transit
Authentication — verifies identities
Tunneling protocols — securely transport data
VPN vs VLAN:
VPN VLAN
Purpose Secure tunnel over internet Logical network segmentation
Location Between sites/users over public internet Within local network
Security Encryption + authentication Traffic isolation
Cost Low (uses existing internet) Low (configured on switch)
18. Firewall
What is a Firewall?
A network security device that filters traffic between trusted (internal) and untrusted (external) networks.
Permits or denies traffic based on predefined rules.
Firewall functions:
1. Traffic Filtering — allow only legitimate traffic




2. Network Segmentation — isolate parts of network
3. Protection — shield internal network from threats
In AWS:
Security Groups = instance-level firewall (stateful)
Network ACLs = subnet-level firewall (stateless)
19. Network Topologies
Topology Structure Pros Cons Use Case
Bus All nodes on single
cable
Simple, cheap One failure = all
down
Small/temporary
networks
Star All devices connect
to central
hub/switch
Easy troubleshoot, one
link failure doesn't affect
others
Central hub
failure = all down
Homes, offices
Ring Each node connects
to exactly two others
Simple data flow Single node
failure breaks
ring
Token ring
networks
Mesh Every node connects
to multiple others
Highly redundant,
multiple paths
Expensive,
complex
Military, data
centers
Tree Star networks
connected via
central bus
Scalable, hierarchical Main bus failure
= all segments
down
Schools,
universities
Hybrid Combination of
topologies
Flexible, customizable Complex and
expensive
Large corporate
networks
20. Networking Quick Reference for DevOps Interviews
OSI Model (7 layers, top to bottom):
Application → Presentation → Session → Transport → Network → Data Link → Physical
Data names by layer:
Application/Presentation/Session = Data
Transport = Segment




Network = Packet
Data Link = Frame
Physical = Bit
TCP = reliable, connection-oriented, port 6
UDP = unreliable, connectionless, port 17
Three-way handshake = SYN → SYN-ACK → ACK
DNS = domain → IP translation (port 53)
DHCP = auto IP assignment → DORA process
ARP = IP → MAC address mapping
PING = ICMP echo request/reply
IPv4 = 32-bit, 4.3B addresses
IPv6 = 128-bit, 340 undecillion addresses
Private ranges: 10.x, 172.16-31.x, 192.168.x
Loopback: 127.0.0.1
APIPA: 169.254.x.x (no DHCP available)
NAT = private IP → public IP (PAT = most common)
VLAN = logical network segmentation
VPN = encrypted tunnel over internet
Firewall = traffic filter by rules
Hub = Layer 1, broadcasts all
Switch = Layer 2, forwards by MAC
Router = Layer 3, routes by IP
SSH (port 22) = secure, encrypted
Telnet (port 23) = insecure, plain text

