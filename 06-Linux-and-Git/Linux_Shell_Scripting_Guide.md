# 📖 Linux Shell Scripting Guide
> *Converted from `Linux Shell Scripting Guide.pdf` for high-readability on GitHub.*

---
## Page 1

Complete Linux & Shell Scripting Interview Guide
1. Linux Basics
Q1. What is Linux? - Open-source, Unix-like OS used in servers, cloud, and embedded systems.
Q2. Components of Linux: - Kernel, Shell, File system, Utilities & applications.
Q3. Difference between Linux and Unix:  | Feature | Linux | Unix | |---------|-------|------| | Source | Open-
source | Usually proprietary | | Cost | Free | Paid | | Platforms | PC/Servers | High-end servers |
Q4. What is a shell? - Command-line interpreter (bash, sh, zsh) that interacts with the kernel.
Q5. Linux processes: - Running instances of programs. Each has a PID, owner , and state.
Q6. Foreground vs Background Process:  | Type | Description | |------|-------------| | Foreground | Runs
interactively, blocks terminal | | Background | Runs asynchronously, frees terminal |
Q7. Symbolic vs Hard Link:  - Symlink: pointer to another file/directory - Hard link: another name for a file
pointing to the inode
Q8. Check disk usage:
df -h
du -sh foldername
Q9. File permissions: - Format: -rwxr-xr-- (owner , group, others)
2. File Permissions & Ownership
Change file permissions:
chmod 755 file.txt
chmod u+x file.txt
chmod g-w file.txt
chmod o=r file.txt
Check permissions:
1

## Page 2

ls -l file.txt
stat file.txt
Change ownership:
chown user:group file.txt
chown user file.txt
chgrp group file.txt
3. User & Group Management
Create user:
sudo useradd username
sudo passwd username
Delete user:
sudo userdel username
sudo userdel -r username
Create group & add user:
sudo groupadd groupname
sudo usermod -aG groupname username
List users and groups:
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
10. Shell Scripting Basics
Q1. What is Shell Scripting? - Program written for shell to automate tasks.
Q2. Types of shells: - Bash, sh, csh, ksh, zsh
Q3. Create & execute a script:
#!/bin/bash
echo "Hello World"
chmod +x script.sh
./script.sh
Q4. Variables:
5

## Page 6

name="Akhil"
echo $name
read -p "Enter name: " user
Special variables: $0, $1, $#, $@, $?, $$
11. Conditional Statements
if [ condition ]; then
# commands
elif [ condition ]; then
# commands
else
# commands
fi
Example:
read -p "Enter number: " num
if [ $num -gt 0 ]; then
echo "Positive"
elif [ $num -lt 0 ]; then
echo "Negative"
else
echo "Zero"
fi
12. Loops
For loop:
for i in 1 2 3 4 5; do
echo $i
done
While loop:
6

## Page 7

count=1
while [ $count -le 5 ]; do
echo $count
((count++))
done
Until loop:
count=1
until [ $count -gt 5 ]; do
echo $count
((count++))
done
13. Functions
greet() {
echo "Hello $1"
}
greet "Akhil"
14. Case Statement
read -p "Enter 1-3: " num
case $num in
1) echo "One" ;;
2) echo "Two" ;;
3) echo "Three" ;;
*) echo "Invalid" ;;
esac
15. File & String Operations
Check file/dir existence:
7

## Page 8

[ -f file.txt ] && echo "File exists"
[ -d /path ] && echo "Directory exists"
String comparison:
str1="hello"
str2="world"
[ "$str1" == "$str2" ] && echo "Same" || echo "Different"
16. Basic Shell Scripts Examples
Hello World:
echo "Hello World"
Sum of Two Numbers:
read a
read b
sum=$((a+b))
echo $sum
Factorial:
fact=1
for ((i=1;i<=num;i++)); do
fact=$((fact*i))
done
echo $fact
Reverse String:
rev=""
for ((i=${#str}-1;i>=0;i--)); do
rev="$rev${str:$i:1}"
8

## Page 9

done
echo $rev
Prime Number Check:
isPrime=1
for ((i=2;i<=n/2;i++)); do
if [ $((n%i)) -eq 0 ]; then
isPrime=0
break
fi
done
[ $isPrime -eq 1 ] && echo "Prime" || echo "Not Prime"
17. Miscellaneous Shell Commands
Command Use
echo Print output
read Take input
expr Evaluate expressions
$(( )) Arithmetic operations
test / [ ] Conditional expressions
sleep Pause execution
exit Exit script with status
date Current date/time
ls, cat, grep File operations
This  combined  guide  covers  Linux  fundamentals,  commands,  user/group  management,  file
permissions, compression, filter commands, and shell scripting  including basic programs for interview
preparation.
9

