# Day 12 – Breather & Revision (Days 01–11)

## Goal
Take a one-day pause to consolidate everything from Days 01–11 so you don’t forget the fundamentals you just built.

---

# Task

## What to Review

### 1. Mindset & Plan
- Revisit Day 01 learning plan
- Check whether goals are still correct
- Identify improvements needed

### 2. Processes & Services
Practice commands from Day 04/05:
- `ps`
- `systemctl status`
- `journalctl`

### 3. File Skills
Practice operations from Days 06–11:
- `echo >>`
- `chmod`
- `chown`
- `ls -l`
- `cp`
- `mkdir`

### 4. Cheat Sheet Refresh
Review Day 03 commands and identify:
- Top 5 commands useful during incidents

### 5. User & Group Sanity
Recreate a small scenario:
- Create user
- Change ownership
- Verify with `id` and `ls -l`

---

# Mini Self-Check Questions

1. Which 3 commands save you the most time right now, and why?

2. How do you check if a service is healthy?

3. How do you safely change ownership and permissions?

4. What will you focus on improving in the next 3 days?

---

# Suggested Flow

| Time | Activity |
|---|---|
| 10 min | Skim notes from previous days |
| 15–20 min | Hands-on revision practice |
| 5–10 min | Write self-check answers |

---

# Output / Practice

# 1. Mindset & Learning Plan Review

## Current Goal
- Build strong Linux fundamentals
- Improve troubleshooting skills
- Move toward DevOps Engineer role

## Areas to Improve
- Linux permissions
- Service logs analysis
- Faster command recall

---

# 2. Processes & Services Practice

## Check Running Processes

```bash
ps aux | head
```

### Output

```bash
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 169280 11520 ?        Ss   10:00   0:01 /sbin/init
root       625  0.0  0.2  72240 15432 ?        Ss   10:01   0:00 sshd
ubuntu    1200  0.0  0.1  11232  5120 pts/0    S+   10:15   0:00 bash
```

---

## Check Nginx Service Status

```bash
systemctl status nginx
```

### Output

```bash
● nginx.service - A high performance web server
     Loaded: loaded (/lib/systemd/system/nginx.service)
     Active: active (running)
```

---

## View Service Logs

```bash
journalctl -u nginx --since "1 hour ago"
```

### Output

```bash
May 25 10:20:11 server nginx[1020]: Starting nginx service
May 25 10:20:12 server systemd[1]: Started nginx.service
```

---

# 3. File Skills Practice

## Append Text to File

```bash
echo "Linux Revision" >> notes.txt
```

## Verify

```bash
cat notes.txt
```

### Output

```bash
Linux Revision
```

---

## Change File Permission

```bash
chmod 755 script.sh
```

## Verify

```bash
ls -l script.sh
```

### Output

```bash
-rwxr-xr-x 1 ubuntu ubuntu 120 May 25 10:30 script.sh
```

---

## Change Ownership

```bash
sudo chown ubuntu:developers project.txt
```

## Verify

```bash
ls -l project.txt
```

### Output

```bash
-rw-r--r-- 1 ubuntu developers 0 May 25 10:35 project.txt
```

---

# 4. Cheat Sheet Refresh

## Top 5 Commands for Troubleshooting

| Command | Purpose |
|---|---|
| `top` | Monitor CPU and memory |
| `ps aux` | View running processes |
| `systemctl status` | Check service health |
| `journalctl -xe` | View logs and errors |
| `df -h` | Check disk usage |

---

# 5. User & Group Practice

## Create User

```bash
sudo useradd devuser
```

---

## Set Password

```bash
sudo passwd devuser
```

---

## Verify User

```bash
id devuser
```

### Output

```bash
uid=1002(devuser) gid=1002(devuser) groups=1002(devuser)
```

---

## Change Ownership

```bash
sudo chown devuser:devuser testfile.txt
```

## Verify

```bash
ls -l testfile.txt
```

### Output

```bash
-rw-r--r-- 1 devuser devuser 0 May 25 10:40 testfile.txt
```

---

# Mini Self-Check Answers

## 1. Which 3 commands save you the most time right now?

### `ls -l`
Quickly checks permissions and ownership.

### `systemctl status`
Checks whether services are running correctly.

### `journalctl`
Helps troubleshoot service failures and logs.

---

## 2. How do you check if a service is healthy?

### Commands

```bash
systemctl status nginx
```

```bash
ps aux | grep nginx
```

```bash
journalctl -u nginx -n 20
```

---

## 3. How do you safely change ownership and permissions?

### Example

```bash
sudo chown -R ubuntu:developers project/
```

```bash
chmod -R 755 project/
```

### Best Practices
- Verify with `ls -l`
- Avoid using `777`
- Use recursive commands carefully

---

## 4. What will you focus on improving in the next 3 days?

- Shell scripting basics
- Linux networking
- Faster troubleshooting
- Log analysis practice

---

# Key Takeaways

- Repetition improves Linux command memory
- Service logs are essential for troubleshooting
- Permissions and ownership must be handled carefully
- Daily hands-on practice builds confidence

---

# Learn in Public

Today was focused on revising Linux and DevOps fundamentals from Days 01–11.

Reinforced:
- Process management
- Service monitoring
- File permissions
- User and ownership management

One command I now remember confidently:

```bash
systemctl status <service>
```

---

# Hashtags

#90DaysOfDevOps  
#DevOpsLearning
