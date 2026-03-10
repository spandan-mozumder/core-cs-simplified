# 🐧 Linux — Interview Questions & Answers

> Top Linux interview questions with answers and command examples.
> Source: [Intellipaat — Linux Interview Questions](https://intellipaat.com/blog/interview-question/linux-interview-questions/)

---

### Q1. What is Linux?

**Linux** is a free, open-source, Unix-like operating system kernel created by **Linus Torvalds** in 1991. Distributions (distros) like Ubuntu, CentOS, and Fedora build complete OS platforms around it.

---

### Q2. Components of the Linux System

| Component            | Function                                   |
| -------------------- | ------------------------------------------ |
| **Kernel**           | Core — manages hardware, memory, processes |
| **Shell**            | Command interpreter (Bash, Zsh, Fish)      |
| **File System**      | Organizes data (ext4, XFS, Btrfs)          |
| **System Libraries** | Functions for applications (glibc)         |
| **System Utilities** | Commands (ls, cp, grep)                    |

---

### Q3. Linux File Permissions

```bash
# Format: rwxrwxrwx (owner/group/others)
ls -la
# -rw-r--r-- 1 user group 4096 Jan 1 file.txt

# Change permissions
chmod 755 script.sh    # rwxr-xr-x
chmod u+x file.sh      # Add execute for owner
chmod go-w file.txt     # Remove write for group & others

# Change ownership
chown user:group file.txt
chown -R user:group /directory/

# Permission numbers: r=4, w=2, x=1
# 755 = rwx(7) r-x(5) r-x(5)
# 644 = rw-(6) r--(4) r--(4)
```

---

### Q4. Essential Linux Commands

```bash
# File operations
ls -la              # List all files with details
cp source dest      # Copy
mv old new          # Move/rename
rm -rf directory    # Remove recursively
mkdir -p a/b/c      # Create nested directories
find / -name "*.log" -mtime -7  # Find files modified in last 7 days

# Text processing
grep -rn "pattern" /path/    # Search recursively with line numbers
grep -i "error" log.txt      # Case-insensitive search
cat file.txt | sort | uniq   # Sort and remove duplicates
awk '{print $1, $3}' file    # Print columns 1 and 3
sed 's/old/new/g' file.txt   # Replace text
wc -l file.txt               # Count lines
tail -f /var/log/syslog      # Follow log in real-time
head -n 20 file.txt          # First 20 lines

# Process management
ps aux                       # List all processes
top / htop                   # Interactive process viewer
kill -9 <PID>                # Force kill
killall nginx                # Kill all nginx processes
nohup command &              # Run in background, survive logout

# Disk & memory
df -h                        # Disk space usage
du -sh /var/log               # Directory size
free -m                      # Memory usage
```

---

### Q5. Hard Link vs Soft Link

```bash
# Hard link — same inode, same data
ln original.txt hardlink.txt
# Deleting original doesn't affect hard link

# Soft link (symbolic) — pointer to file
ln -s /path/to/original.txt symlink.txt
# Deleting original breaks the soft link
```

| Feature          | Hard Link   | Soft Link |
| ---------------- | ----------- | --------- |
| Inode            | Same        | Different |
| Cross filesystem | ❌          | ✅        |
| Directories      | ❌          | ✅        |
| Original deleted | Still works | Breaks    |

---

### Q6. Shell Scripting

```bash
#!/bin/bash

# Variables
NAME="Alice"
echo "Hello, $NAME"

# Conditional
if [ -f "/etc/passwd" ]; then
    echo "File exists"
elif [ -d "/tmp" ]; then
    echo "Directory exists"
else
    echo "Not found"
fi

# Loops
for i in {1..5}; do
    echo "Number: $i"
done

# While loop
count=0
while [ $count -lt 5 ]; do
    echo "Count: $count"
    ((count++))
done

# Functions
greet() {
    echo "Hello, $1! You are $2 years old."
}
greet "Bob" 25

# Arrays
fruits=("apple" "banana" "cherry")
echo ${fruits[0]}       # apple
echo ${#fruits[@]}      # 3 (length)

# Command substitution
current_date=$(date +%Y-%m-%d)
echo "Today: $current_date"
```

---

### Q7. Networking Commands

```bash
# Network info
ifconfig / ip addr show      # Show IP addresses
hostname -I                  # Show all IP addresses
netstat -tlnp               # Show listening ports
ss -tlnp                     # Modern alternative to netstat

# DNS
nslookup google.com
dig google.com

# Connectivity
ping -c 4 google.com
traceroute google.com
curl -I https://google.com   # HTTP headers
wget https://example.com/file.zip

# Firewall (iptables / ufw)
sudo ufw enable
sudo ufw allow 80/tcp
sudo ufw deny 22
sudo ufw status
```

---

### Q8. Cron Jobs

```bash
# Edit crontab
crontab -e

# Format: minute hour day month weekday command
# ┌───── minute (0-59)
# │ ┌──── hour (0-23)
# │ │ ┌─── day of month (1-31)
# │ │ │ ┌── month (1-12)
# │ │ │ │ ┌─ day of week (0-7, 0=Sun)
# * * * * * command

# Every day at 2 AM
0 2 * * * /scripts/backup.sh

# Every 5 minutes
*/5 * * * * /scripts/health_check.sh

# Every Monday at 9 AM
0 9 * * 1 /scripts/weekly_report.sh

# List cron jobs
crontab -l
```

---

### Q9. User & Group Management

```bash
# Create user
sudo useradd -m -s /bin/bash username
sudo passwd username

# Create group & add user
sudo groupadd developers
sudo usermod -aG developers username

# Check groups
groups username
id username

# Switch user
su - username
sudo -u username command

# Delete user
sudo userdel -r username
```

---

### Q10. Process Signals

| Signal    | Number | Description                    |
| --------- | ------ | ------------------------------ |
| `SIGHUP`  | 1      | Hangup — reload config         |
| `SIGINT`  | 2      | Interrupt (Ctrl+C)             |
| `SIGKILL` | 9      | Force kill (cannot be caught)  |
| `SIGTERM` | 15     | Graceful termination (default) |
| `SIGSTOP` | 19     | Pause process (Ctrl+Z)         |

```bash
kill -15 <PID>    # Graceful stop
kill -9 <PID>     # Force kill
kill -1 <PID>     # Reload configuration
```

---

### Q11. SSH & Remote Access

```bash
# Connect to remote server
ssh user@192.168.1.100

# SSH with key-based auth
ssh-keygen -t ed25519           # Generate key pair
ssh-copy-id user@server         # Copy public key to server

# SCP — secure file copy
scp file.txt user@server:/path/
scp -r folder/ user@server:/path/

# SSH tunnel (port forwarding)
ssh -L 8080:localhost:80 user@server   # Local port forwarding
```

---

### Q12. System Logs

```bash
# View system logs
journalctl                    # Systemd journal
journalctl -u nginx -f        # Follow nginx logs
cat /var/log/syslog           # General system log
cat /var/log/auth.log         # Authentication log
cat /var/log/kern.log         # Kernel log
dmesg                        # Boot/kernel messages

# Log analysis
grep "ERROR" /var/log/syslog | tail -20
awk '/Failed password/ {print $11}' /var/log/auth.log | sort | uniq -c | sort -rn
```

---

### Q13. Package Management

```bash
# Debian/Ubuntu (APT)
sudo apt update
sudo apt install nginx
sudo apt remove nginx
sudo apt upgrade

# RedHat/CentOS (YUM/DNF)
sudo yum install httpd
sudo dnf install httpd
sudo yum remove httpd
```

---

### Q14. LVM (Logical Volume Management)

```bash
# Create physical volume
sudo pvcreate /dev/sdb1

# Create volume group
sudo vgcreate my_vg /dev/sdb1

# Create logical volume
sudo lvcreate -L 10G -n my_lv my_vg

# Extend logical volume
sudo lvextend -L +5G /dev/my_vg/my_lv
sudo resize2fs /dev/my_vg/my_lv
```

---

### Q15. Three Standard Streams

| Stream | File Descriptor | Symbol | Purpose |
| ------ | --------------- | ------ | ------- |
| stdin  | 0               | `<`    | Input   |
| stdout | 1               | `>`    | Output  |
| stderr | 2               | `2>`   | Errors  |

```bash
# Redirect stdout to file
command > output.txt

# Redirect stderr to file
command 2> errors.txt

# Redirect both
command > output.txt 2>&1
command &> combined.txt

# Pipe stdout to next command
cat file.txt | grep "error" | wc -l
```

---
