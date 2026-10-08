# 📖 Linux Interview Guide
> *Converted from `Linux Interview Guide.pdf` for high-readability on GitHub.*

---
## Page 1

Linux Interview Questions, Answers, and Commands
1. Linux Basics
Q1. What is Linux? - Open-source, Unix-like OS used in servers, cloud, and embedded systems.
Q2. Components of Linux: - Kernel, Shell, File system, Utilities & applications.
Q3. Difference between Linux and Unix:  | Feature | Linux | Unix | |---------|-------|------| | Source | Open-
source | Usually proprietary | | Cost | Free | Paid | | Platforms | PC/Servers | High-end servers |
Q4. What is a shell? - Command-line interpreter (bash, sh, zsh) that interacts with the kernel.
Q5. What are Linux processes? - Running instances of programs. Each has a PID, owner , and state.
Q6. Foreground vs Background Process:  | Type | Description | |------|-------------| | Foreground | Runs
interactively, blocks terminal | | Background | Runs asynchronously, frees terminal |
Q7. Symbolic vs Hard Link:  - Symlink: pointer to another file/directory - Hard link: another name for a file
pointing to the inode
Q8. How to check disk usage:
df -h
du -sh foldername
Q9. File permissions: - Format: -rwxr-xr-- (owner , group, others)
2. File Permissions & Ownership
Q10. Change file permissions:
chmod 755 file.txt
chmod u+x file.txt
chmod g-w file.txt
chmod o=r file.txt
Q11. Check permissions:
1

## Page 2

ls -l file.txt
stat file.txt
Q12. Change ownership:
chown user:group file.txt
chown user file.txt
chgrp group file.txt
3. User & Group Management
Q13. Create user:
sudo useradd username
sudo passwd username
Q14. Delete user:
sudo userdel username
sudo userdel -r username
Q15. Create group & add user:
sudo groupadd groupname
sudo usermod -aG groupname username
Q16. List users and groups:
cat /etc/passwd
cat /etc/group
2

## Page 3

4. File Compression
Command Description
tar -czvf file.tar .gz folder Compress folder into tar .gz
tar -xzvf file.tar .gz Extract tar .gz
gzip file.txt Compress file
gunzip file.txt.gz Decompress gzip
zip file.zip folder Compress folder into zip
unzip file.zip Extract zip
5. Filter Commands
grep
grep "pattern" file.txt
grep -i "pattern" file.txt
grep -r "pattern" /path
awk
awk '{print $1}' file.txt
awk '/pattern/ {print $2}' file.txt
sed
sed 's/old/new/g' file.txt
sed -n '1,5p' file.txt
sort & uniq
sort file.txt
sort -n file.txt
uniq file.txt
sort file.txt | uniq
3

## Page 4

head & tail
head -n 10 file.txt
tail -n 10 file.txt
tail -f file.log
wc
wc -l file.txt
wc -w file.txt
wc -c file.txt
6. Process Management
ps aux
top
htop
kill <PID>
kill -9 <PID>
jobs
fg %1
bg %1
7. Disk and Memory Management
df -h
du -sh folder
free -h
vmstat
8. Networking Commands
ifconfig / ip a
ping google.com
4

## Page 5

netstat -tulnp
curl url
scp file user@host:/path
ssh user@host
9. File and Directory Commands
pwd
ls
ls -l
cd /path
mkdir folder
rmdir folder
rm file
rm -rf folder
cp src dest
mv src dest
touch file
cat file
less file
more file
10. Additional Linux Commands
uname -a # Kernel & OS info
uptime # System uptime
whoami # Current user
history # Command history
alias ll='ls -l' # Create alias
unalias ll # Remove alias
This  guide  combines  all  Linux  interview  topics:  file  permissions,  user  &  group  management,  file
compression, filter commands, process management, networking, and common Linux commands.
You can now convert this into a PDF for offline reference and interview prep.
5

