# Linux Command Reference Guide

## 1. System Information Commands

### 1.1 Kernel and System Details

#### `uname -a`
**Description**: Prints detailed system information
**Example**:
```bash
$ uname -a
Linux hostname 5.4.0-146-generic #163-Ubuntu SMP Fri Mar 17 22:41:43 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
```
**Breakdown**:
- Linux: Operating system
- hostname: Machine name
- 5.4.0-146-generic: Kernel version
- x86_64: System architecture

#### `cat /etc/os-release`
**Description**: Display distribution-specific information
**Example**:
```bash
$ cat /etc/os-release
NAME="Ubuntu"
VERSION="20.04.4 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
```

### 1.2 System Uptime and Load

#### `uptime`
**Description**: Shows how long the system has been running, number of users, and load averages
**Example**:
```bash
$ uptime
 09:45:23 up 7 days,  2:33,  3 users,  load average: 0.08, 0.03, 0.01
```
**Explanation**:
- `09:45:23`: Current time
- `up 7 days, 2:33`: System uptime
- `3 users`: Number of logged-in users
- `load average`: System load for past 1, 5, and 15 minutes

### 1.3 Date and Time

#### `date`
**Description**: Display or set system date and time
**Examples**:
```bash
# Display current date and time
$ date
Mon Apr 10 09:45:30 UTC 2023

# Custom format
$ date "+%Y-%m-%d %H:%M:%S"
2023-04-10 09:45:30

# Set date (requires root)
$ sudo date -s "2023-04-10 10:00:00"
```

### 1.4 System Hostname

#### `hostname`
**Description**: Show or set the system's hostname
**Examples**:
```bash
# Display hostname
$ hostname
mycomputer

# Set hostname temporarily
$ sudo hostname newname

# Permanently set hostname
$ sudo hostnamectl set-hostname newname
```

## 2. Hardware Information Commands

### 2.1 CPU Information

#### `lscpu`
**Description**: Detailed CPU information
**Example**:
```bash
$ lscpu
Architecture:        x86_64
CPU(s):              8
Thread(s) per core:  2
Core(s) per socket:  4
Socket(s):           1
```

#### `cat /proc/cpuinfo`
**Description**: Raw CPU information from kernel
**Tip**: Use `grep` to filter specific information
```bash
$ cat /proc/cpuinfo | grep "model name"
model name	: Intel(R) Core(TM) i7-9750H CPU @ 2.60GHz
```

### 2.2 Memory Information

#### `free -h`
**Description**: Display memory usage in human-readable format
**Example**:
```bash
$ free -h
              total        used        free      shared  buff/cache   available
Mem:           15Gi       5.3Gi       2.7Gi       652Mi        7.3Gi        9.1Gi
Swap:          2.0Gi       256Mi       1.7Gi
```

### 2.3 Disk Information

#### `lsblk`
**Description**: List block devices
**Example**:
```bash
$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 465.8G  0 disk 
├─sda1   8:1    0   450G  0 part /
├─sda2   8:2    0    15G  0 part [SWAP]
```

## 3. Performance Monitoring

### 3.1 Process Monitoring

#### `top` and `htop`
**Description**: Real-time process viewer
**Key Interactions in htop**:
- F5: Tree view
- F6: Sort processes
- F9: Send signals to processes

### 3.2 System Load

#### `mpstat`
**Description**: Multiprocessor statistics
**Example**:
```bash
$ mpstat 1 5
Average:  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
Average:  all   10.25    0.00    3.50    0.75    0.00    0.25    0.00    0.00    0.00   85.25
```

### 3.3 Network Monitoring

#### `tcpdump`
**Description**: Packet analyzer
**Examples**:
```bash
# Capture all packets on eth0
$ sudo tcpdump -i eth0

# Capture HTTP traffic
$ sudo tcpdump -i eth0 port 80
```

## 4. User and Permission Management

### 4.1 User Information

#### `id`
**Description**: Print user and group information
**Example**:
```bash
$ id
uid=1000(john) gid=1000(john) groups=1000(john),27(sudo)
```

### 4.2 Creating Users

#### `useradd`
**Description**: Create a new user
**Examples**:
```bash
# Create user with home directory
$ sudo useradd -m username

# Create user with specific shell
$ sudo useradd -m -s /bin/bash username

# Create user with comment
$ sudo useradd -c "John Doe" -m john
```

### 4.3 File Permissions

#### `chmod` Permission Codes
- 4 (r): Read
- 2 (w): Write
- 1 (x): Execute

**Examples**:
```bash
# Full permissions for owner, read/execute for group and others
$ chmod 755 script.sh

# Read/write for owner, read-only for group and others
$ chmod 644 document.txt
```

## 5. File and Directory Operations

### 5.1 Advanced File Searching

#### `find`
**Description**: Search for files with complex criteria
**Examples**:
```bash
# Find files larger than 100MB
$ find / -type f -size +100M

# Find files modified in last 7 days
$ find /home -mtime -7

# Find and execute command on found files
$ find . -name "*.txt" -exec grep "pattern" {} \;
```

### 5.2 File Compression

#### `tar`
**Description**: Archive utility
**Examples**:
```bash
# Create compressed tarball
$ tar -czvf archive.tar.gz /path/to/directory

# Extract tarball
$ tar -xzvf archive.tar.gz
```

## 6. Networking Commands

### 6.1 Network Diagnostics

#### `ping`
**Description**: Test network connectivity
**Example**:
```bash
$ ping google.com
PING google.com (172.217.16.142): 56 data bytes
64 bytes from 172.217.16.142: icmp_seq=0 ttl=117 time=10.966 ms
```

#### `traceroute`
**Description**: Trace network path to destination
**Example**:
```bash
$ traceroute google.com
1  router.local (192.168.1.1)  0.331 ms
2  isp.gateway (10.0.0.1)  15.432 ms
3  ...
```

## Pro Tips
1. Always use `man` command to get detailed information about any command
2. Use `sudo` carefully and only when necessary
3. Keep your system updated
4. Learn to use command-line text editors like `vim` or `nano`
5. Understand file permissions and security

## Recommended Learning Resources
- Linux Documentation Project
- Linux Man Pages
- Online Linux training platforms
- GitHub Linux tutorials
