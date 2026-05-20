# Day 04 – Linux Practice: Processes and Services

## Introduction

Today I practiced Linux process monitoring, service management, and log inspection commands.

The goal was to understand how Linux services and processes work in a real environment.

---

# Process Checks

## 1. Checking Running Processes

### Command

```bash
ps aux | head
```

### Output

```text
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.1 169252 12084 ?        Ss   May19   0:03 /sbin/init
root         512  0.0  0.2  82540 18400 ?        Ssl  May19   0:01 /usr/lib/systemd/systemd-journald
mysql       1023  0.3  4.5 1734560 365000 ?     Ssl  May19   1:22 mysqld
root        1250  0.0  0.1  45032  8200 ?       Ss   May19   0:00 cron
root        1300  0.1  0.3 1456780 28500 ?      Ssl  May19   0:45 dockerd
```

### What I Learned

- `ps aux` displays all running processes.
- It helps monitor CPU and memory usage.

---

## 2. Finding a Process using pgrep

### Command

```bash
pgrep mysql
```

### Output

```text
1023
```

### What I Learned

- `pgrep` quickly finds the process ID (PID) of a running application.
- It is useful for scripting and troubleshooting.

---

# Service Checks

## 3. Checking Docker Service Status

### Command

```bash
systemctl status docker
```

### Output

```text
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled)
     Active: active (running) since Tue 2026-05-19 09:30:15 IST; 1 day ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 1300 (dockerd)
      Tasks: 15
     Memory: 45.2M
        CPU: 1min 20.231s
```

### What I Learned

- Docker service is active and running successfully.
- `systemctl status` helps inspect service health and uptime.

---

## 4. Listing Running Services

### Command

```bash
systemctl list-units --type=service --state=running
```

### Output

```text
UNIT                     LOAD   ACTIVE SUB     DESCRIPTION
cron.service             loaded active running Regular background program processing daemon
docker.service           loaded active running Docker Application Container Engine
mysql.service            loaded active running MySQL Community Server
ssh.service              loaded active running OpenBSD Secure Shell server
systemd-journald.service loaded active running Journal Service
```

### What I Learned

- This command lists all currently running services.
- Useful during troubleshooting and server monitoring.

---

# Log Checks

## 5. Viewing Docker Logs

### Command

```bash
journalctl -u docker --no-pager | tail -n 10
```

### Output

```text
May 20 09:45:12 server dockerd[1300]: Docker daemon started
May 20 09:45:13 server dockerd[1300]: API listen on /run/docker.sock
May 20 09:46:10 server dockerd[1300]: Container started successfully
May 20 09:47:22 server dockerd[1300]: Network bridge initialized
```

### What I Learned

- `journalctl` displays logs for specific services.
- Helpful for debugging startup or runtime issues.

---

## 6. Checking System Logs

### Command

```bash
tail -n 20 /var/log/syslog
```

### Output

```text
May 20 10:01:22 server CRON[2210]: pam_unix(cron:session): session opened
May 20 10:01:22 server CRON[2210]: pam_unix(cron:session): session closed
May 20 10:02:15 server systemd[1]: Started Daily Cleanup Service.
May 20 10:03:11 server sshd[2401]: Accepted password for ubuntu
```

### What I Learned

- `tail` helps monitor the latest log entries quickly.
- Useful for checking recent activity and errors.

---

# Mini Troubleshooting Steps

## Issue

Docker containers were not starting properly.

---

## Step 1: Check Docker Service

### Command

```bash
systemctl status docker
```

### Result

- Docker service was running normally.

---

## Step 2: Inspect Docker Logs

### Command

```bash
journalctl -u docker --no-pager | tail -n 20
```

### Result

- Found a permission warning related to Docker socket access.

---

## Step 3: Restart Docker Service

### Command

```bash
sudo systemctl restart docker
```

### Result

- Docker containers started successfully after restart.

---

# Summary

Today I practiced:

- Process monitoring commands
- Service management commands
- Log inspection techniques
- Basic Linux troubleshooting workflow

This hands-on practice improved my confidence with Linux fundamentals and DevOps troubleshooting.
