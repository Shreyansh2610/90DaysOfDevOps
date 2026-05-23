# Day 07 – Linux File System Hierarchy & Scenario-Based Practice

## Objective

Today's goal is to understand:

- Linux File System Hierarchy
- Real-world troubleshooting scenarios
- How DevOps engineers investigate production issues

---

# Part 1: Linux File System Hierarchy

---

# 1. Root Directory `/`

## Purpose

The root directory `/` is the starting point of the entire Linux file system. Every file and folder exists under this directory.

## Command

```bash
ls -l /
```

## Sample Output

```bash
drwxr-xr-x   2 root root 4096 bin
drwxr-xr-x   5 root root 4096 boot
drwxr-xr-x  20 root root 4096 etc
drwxr-xr-x   3 root root 4096 home
drwxr-xr-x  10 root root 4096 usr
drwxrwxrwt   8 root root 4096 tmp
```

## Important Directories Seen

- `home`
- `etc`
- `usr`
- `tmp`

## I would use this when...

I need to navigate the full Linux system or troubleshoot system-level issues.

---

# 2. `/home`

## Purpose

Contains personal directories for normal users.

## Command

```bash
ls -l /home
```

## Sample Output

```bash
drwxr-x--- 5 ubuntu ubuntu 4096 ubuntu
drwxr-x--- 3 developer developer 4096 developer
```

## Important Folders Seen

- `ubuntu`
- `developer`

## I would use this when...

I need to access user files, downloads, scripts, or SSH keys.

---

# 3. `/root`

## Purpose

Home directory of the root user (administrator).

## Command

```bash
ls -l /root
```

## Sample Output

```bash
-rw------- 1 root root  220 .bash_logout
-rw------- 1 root root 3771 .bashrc
drwxr-xr-x 2 root root 4096 scripts
```

## Important Files/Folders Seen

- `.bashrc`
- `scripts`

## I would use this when...

I perform administrative or server-management tasks.

---

# 4. `/etc`

## Purpose

Contains system-wide configuration files.

## Command

```bash
ls -l /etc
```

## Sample Output

```bash
-rw-r--r-- 1 root root   12 hostname
drwxr-xr-x 3 root root 4096 ssh
drwxr-xr-x 2 root root 4096 systemd
```

## Important Files/Folders Seen

- `hostname`
- `ssh`
- `systemd`

## I would use this when...

I need to configure services, networking, or system settings.

---

# 5. `/var/log`

## Purpose

Stores system logs and application logs.

Very important for DevOps troubleshooting.

## Command

```bash
ls -l /var/log
```

## Sample Output

```bash
-rw-r----- 1 syslog adm  24576 syslog
-rw-r----- 1 root   adm   8192 auth.log
drwxr-xr-x 2 root   root  4096 nginx
```

## Important Files/Folders Seen

- `syslog`
- `auth.log`
- `nginx`

## I would use this when...

I investigate application failures, login problems, or server errors.

---

# 6. `/tmp`

## Purpose

Stores temporary files created by applications and users.

## Command

```bash
ls -l /tmp
```

## Sample Output

```bash
drwx------ 2 root root 4096 systemd-private
-rw-r--r-- 1 user user    0 temp.txt
```

## Important Files/Folders Seen

- `systemd-private`
- `temp.txt`

## I would use this when...

Applications require temporary storage during execution.

---

# Additional Directories

---

# 7. `/bin`

## Purpose

Contains essential Linux command binaries required for system operation.

## Command

```bash
ls -l /bin
```

## Sample Output

```bash
-rwxr-xr-x 1 root root 14632 ls
-rwxr-xr-x 1 root root 35664 cat
```

## Important Commands Seen

- `ls`
- `cat`

## I would use this when...

I need access to essential Linux commands.

---

# 8. `/usr/bin`

## Purpose

Contains user command binaries and installed applications.

## Command

```bash
ls -l /usr/bin
```

## Sample Output

```bash
-rwxr-xr-x 1 root root 54232 python3
-rwxr-xr-x 1 root root 87320 git
```

## Important Applications Seen

- `python3`
- `git`

## I would use this when...

I run installed applications and development tools.

---

# 9. `/opt`

## Purpose

Used for optional or third-party software installations.

## Command

```bash
ls -l /opt
```

## Sample Output

```bash
drwxr-xr-x 3 root root 4096 google
drwxr-xr-x 2 root root 4096 custom-app
```

## Important Folders Seen

- `google`
- `custom-app`

## I would use this when...

I install third-party software manually.

---

# Hands-On Tasks

---

# Find the Largest Log Files

## Command

```bash
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```

## Sample Output

```bash
4.0M /var/log/auth.log
8.0M /var/log/kern.log
12M  /var/log/syslog
20M  /var/log/nginx
50M  /var/log/journal
```

## What I Learned

This helps identify log files consuming large disk space.

---

# Look at a Config File in `/etc`

## Command

```bash
cat /etc/hostname
```

## Sample Output

```bash
devops-server
```

## What I Learned

The hostname file stores the server name.

---

# Check Home Directory

## Command

```bash
ls -la ~
```

## Sample Output

```bash
drwxr-xr-x 5 ubuntu ubuntu 4096 .
drwxr-xr-x 3 root   root   4096 ..
-rw-r--r-- 1 ubuntu ubuntu  220 .bash_logout
-rw-r--r-- 1 ubuntu ubuntu 3771 .bashrc
drwxr-xr-x 2 ubuntu ubuntu 4096 scripts
```

## What I Learned

Hidden files like `.bashrc` store user shell configurations.

---

# Part 2: Scenario-Based Practice

---

# SOLVED EXAMPLE

## Scenario: Check if nginx service is running

### Step 1: Check Service Status

```bash
systemctl status nginx
```

### Why

Shows whether the service is active, stopped, or failed.

---

### Step 2: List Services

```bash
systemctl list-units --type=service
```

### Why

Shows all available services in the system.

---

### Step 3: Check Boot Status

```bash
systemctl is-enabled nginx
```

### Why

Checks whether nginx starts automatically after reboot.

---

## What I Learned

Always check service status first before deeper troubleshooting.

---

# Scenario 1: Service Not Starting

## Problem

A web application service called `myapp` failed after reboot.

---

## Step 1: Check Service Status

### Command

```bash
systemctl status myapp
```

### Sample Output

```bash
● myapp.service - My Application
   Loaded: loaded
   Active: failed
```

### Why

Checks whether the service is failed or inactive.

---

## Step 2: Check Logs

### Command

```bash
journalctl -u myapp -n 50
```

### Sample Output

```bash
Error: Database connection failed
Service exited with code 1
```

### Why

Shows recent logs for troubleshooting.

---

## Step 3: Check Boot Enablement

### Command

```bash
systemctl is-enabled myapp
```

### Sample Output

```bash
enabled
```

### Why

Verifies whether the service starts automatically during boot.

---

## Step 4: View System Logs

### Command

```bash
journalctl -xe
```

### Sample Output

```bash
Failed to start myapp.service
Dependency failed for myapp.service
```

### Why

Displays detailed system-level errors.

---

## What I Learned

The troubleshooting flow should be:
- Check status
- Read logs
- Verify boot configuration
- Investigate dependencies

---

# Scenario 2: High CPU Usage

## Problem

The application server is slow.

---

## Step 1: Monitor Live CPU Usage

### Command

```bash
top
```

### Sample Output

```bash
PID USER   PR NI VIRT  RES SHR S %CPU %MEM COMMAND
2456 root  20  0 500m 120m  12m R 85.0  5.0 java
```

### Why

Shows live CPU and memory usage.

---

## Step 2: Show Top CPU Processes

### Command

```bash
ps aux --sort=-%cpu | head -10
```

### Sample Output

```bash
root   2456 85.0  5.0 java
mysql  1320 25.0 10.0 mysqld
```

### Why

Identifies processes consuming high CPU.

---

## Step 3: Inspect Process Details

### Command

```bash
ps -fp 2456
```

### Sample Output

```bash
UID   PID  PPID CMD
root 2456     1 java -jar app.jar
```

### Why

Shows detailed information about the process.

---

## Step 4: Interactive Monitoring

### Command

```bash
htop
```

### Sample Output

```bash
Interactive process viewer opens
```

### Why

Provides better visualization of CPU and memory usage.

---

## What I Learned

Start with monitoring tools, identify the PID, and investigate the process.

---

# Scenario 3: Finding Service Logs

## Problem

A developer asks:
"Where are Docker service logs?"

---

## Step 1: Check Docker Service Status

### Command

```bash
systemctl status docker
```

### Sample Output

```bash
● docker.service - Docker Application Container Engine
   Active: active (running)
```

### Why

Confirms whether Docker is running correctly.

---

## Step 2: View Last 50 Logs

### Command

```bash
journalctl -u docker -n 50
```

### Sample Output

```bash
Docker daemon started
Container created successfully
```

### Why

Displays recent Docker logs.

---

## Step 3: Follow Logs in Real Time

### Command

```bash
journalctl -u docker -f
```

### Sample Output

```bash
New container started
Network bridge created
```

### Why

Streams live logs continuously.

---

## Step 4: Search for Errors

### Command

```bash
journalctl -u docker | grep -i error
```

### Sample Output

```bash
Error initializing network controller
```

### Why

Filters logs to show only errors.

---

## What I Learned

Systemd-managed services store logs in journald and are accessed using `journalctl`.

---

# Scenario 4: File Permission Issue

## Problem

A script `/home/user/backup.sh` shows:

```bash
Permission denied
```

---

## Step 1: Check File Permissions

### Command

```bash
ls -l /home/user/backup.sh
```

### Sample Output

```bash
-rw-r--r-- 1 user user 120 backup.sh
```

### Why

Checks whether execute permission exists.

---

## Step 2: Add Execute Permission

### Command

```bash
chmod +x /home/user/backup.sh
```

### Sample Output

```bash
(no output)
```

### Why

Adds execute permission.

---

## Step 3: Verify Permissions Again

### Command

```bash
ls -l /home/user/backup.sh
```

### Sample Output

```bash
-rwxr-xr-x 1 user user 120 backup.sh
```

### Why

Confirms that execute permission was added.

---

## Step 4: Run the Script

### Command

```bash
./backup.sh
```

### Sample Output

```bash
Backup completed successfully
```

### Why

Tests whether the issue is resolved.

---

## What I Learned

Linux scripts require execute (`x`) permission before they can run.

---

# Why This Matters for DevOps

Understanding Linux file systems and troubleshooting helps DevOps engineers:

- Find logs quickly
- Manage configuration files
- Troubleshoot production incidents
- Debug permissions issues
- Investigate CPU and service problems
- Write reliable automation scripts

Scenario-based learning improves:
- Real-world troubleshooting
- DevOps interview preparation
- On-call debugging confidence

---

# Final Summary

Today I learned:

- Linux file system hierarchy
- Important directories and their purpose
- How to investigate service failures
- How to analyze high CPU usage
- How to access service logs
- How Linux permissions affect script execution

---
