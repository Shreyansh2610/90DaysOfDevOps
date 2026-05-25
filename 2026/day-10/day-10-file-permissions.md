# Day 10 – File Permissions & File Operations Challenge

## Task
Master file permissions and basic file operations in Linux.

Topics covered:
- Create and read files using `touch`, `cat`, `vim`
- Understand and modify permissions using `chmod`

---

# Task 1: Create Files

## Create Empty File

### Command
```bash
touch devops.txt
```

### Output
```bash
ls -l devops.txt
-rw-rw-r-- 1 user user 0 May 25 10:00 devops.txt
```

---

## Create notes.txt with Content

### Command
```bash
echo "Linux permissions are important for security." > notes.txt
```

### Verify Content
```bash
cat notes.txt
```

### Output
```bash
Linux permissions are important for security.
```

---

## Create script.sh using vim

### Command
```bash
vim script.sh
```

### Add Content
```bash
echo "Hello DevOps"
```

### Verify
```bash
cat script.sh
```

### Output
```bash
echo "Hello DevOps"
```

---

## Verify All Files

### Command
```bash
ls -l
```

### Output
```bash
-rw-rw-r-- 1 user user  0 May 25 10:00 devops.txt
-rw-rw-r-- 1 user user 45 May 25 10:01 notes.txt
-rw-rw-r-- 1 user user 21 May 25 10:02 script.sh
```

---

# Task 2: Read Files

## Read notes.txt

### Command
```bash
cat notes.txt
```

### Output
```bash
Linux permissions are important for security.
```

---

## View script.sh in Read-Only Mode

### Command
```bash
vim -R script.sh
```

### Output
```bash
"script.sh" [readonly]
```

---

## Display First 5 Lines of /etc/passwd

### Command
```bash
head -n 5 /etc/passwd
```

### Output
```bash
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```

---

## Display Last 5 Lines of /etc/passwd

### Command
```bash
tail -n 5 /etc/passwd
```

### Output
```bash
systemd-timesync:x:997:997:systemd Time Synchronization:/:/usr/sbin/nologin
messagebus:x:100:102::/nonexistent:/usr/sbin/nologin
pollinate:x:998:998::/var/cache/pollinate:/bin/false
sshd:x:101:65534::/run/sshd:/usr/sbin/nologin
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
```

---

# Task 3: Understand Permissions

## Permission Format

```text
rwxrwxrwx
│ │ │
│ │ └── Others
│ └──── Group
└────── Owner
```

| Permission | Meaning | Value |
|------------|----------|-------|
| r | Read | 4 |
| w | Write | 2 |
| x | Execute | 1 |

---

## Check File Permissions

### Command
```bash
ls -l devops.txt notes.txt script.sh
```

### Output
```bash
-rw-rw-r-- 1 user user  0 May 25 10:00 devops.txt
-rw-rw-r-- 1 user user 45 May 25 10:01 notes.txt
-rw-rw-r-- 1 user user 21 May 25 10:02 script.sh
```

---

## Current Permissions Analysis

### devops.txt
- Owner: Read + Write
- Group: Read + Write
- Others: Read only

### notes.txt
- Owner: Read + Write
- Group: Read + Write
- Others: Read only

### script.sh
- Owner: Read + Write
- Group: Read + Write
- Others: Read only
- Execute permission not enabled

---

# Task 4: Modify Permissions

## Make script.sh Executable

### Command
```bash
chmod +x script.sh
```

### Verify
```bash
ls -l script.sh
```

### Output
```bash
-rwxrwxr-x 1 user user 21 May 25 10:02 script.sh
```

---

## Run script.sh

### Command
```bash
./script.sh
```

### Output
```bash
Hello DevOps
```

---

## Set devops.txt to Read-Only

### Command
```bash
chmod a-w devops.txt
```

### Verify
```bash
ls -l devops.txt
```

### Output
```bash
-r--r--r-- 1 user user 0 May 25 10:00 devops.txt
```

---

## Set notes.txt Permission to 640

### Command
```bash
chmod 640 notes.txt
```

### Verify
```bash
ls -l notes.txt
```

### Output
```bash
-rw-r----- 1 user user 45 May 25 10:01 notes.txt
```

### Meaning
- Owner: Read + Write
- Group: Read only
- Others: No permission

---

## Create project Directory with Permission 755

### Commands
```bash
mkdir project
chmod 755 project
```

### Verify
```bash
ls -ld project
```

### Output
```bash
drwxr-xr-x 2 user user 4096 May 25 10:10 project
```

### Meaning
- Owner: Full access
- Group: Read + Execute
- Others: Read + Execute

---

# Task 5: Test Permissions

## Try Writing to Read-Only File

### Command
```bash
echo "Testing" >> devops.txt
```

### Output
```bash
bash: devops.txt: Permission denied
```

---

## Remove Execute Permission from script.sh

### Command
```bash
chmod -x script.sh
```

### Verify
```bash
ls -l script.sh
```

### Output
```bash
-rw-rw-r-- 1 user user 21 May 25 10:02 script.sh
```

---

## Try Executing Without Execute Permission

### Command
```bash
./script.sh
```

### Output
```bash
bash: ./script.sh: Permission denied
```

---

# Commands Used

```bash
touch devops.txt
echo "Linux permissions are important for security." > notes.txt
vim script.sh
ls -l
cat notes.txt
vim -R script.sh
head -n 5 /etc/passwd
tail -n 5 /etc/passwd
chmod +x script.sh
./script.sh
chmod a-w devops.txt
chmod 640 notes.txt
mkdir project
chmod 755 project
ls -ld project
chmod -x script.sh
```

---

# What I Learned

1. Linux permissions control who can read, write, and execute files.
2. `chmod` is used to change file and directory permissions.
3. Shell scripts require execute permission to run.

---

# Screenshots to Include

- File creation commands
- `ls -l` outputs before and after permission changes
- Running executable script
- Permission denied errors
- Directory permission verification

---

# Submission Steps

```bash
cd 2026/day-10/
git add day-10-file-permissions.md
git commit -m "Completed Day 10 File Permissions Challenge"
git push
```

---

# LinkedIn Hashtags

```text
#90DaysOfDevOps
#DevOpsLearning
#Linux
#LinuxCommands
#SystemAdministration
```
