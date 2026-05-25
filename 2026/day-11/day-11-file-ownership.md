# Day 11 – File Ownership Challenge

## Objective
Learn Linux file ownership management using:

- `chown`
- `chgrp`
- Recursive ownership changes
- User and group management

---

# Task 1 – Understanding Ownership

## Task

Run `ls -l` in your home directory and identify:

- Owner column
- Group column
- File permissions format

## Commands

```bash
ls -l
```

## Output

```bash
-rw-r--r-- 1 shreyansh shreyansh    0 May 25 10:00 notes.txt
drwxr-xr-x 2 shreyansh shreyansh 4096 May 25 10:02 projects
```

## Format Explanation

```text
-rw-r--r-- 1 owner group size date filename
```

## Difference Between Owner and Group

| Type | Description |
|------|-------------|
| Owner | Primary user controlling the file |
| Group | Multiple users sharing access permissions |

---

# Task 2 – Basic chown Operations

## Task

Create a file and change its ownership between users.

## Commands

### Create File

```bash
touch devops-file.txt
```

### Check Current Owner

```bash
ls -l devops-file.txt
```

## Output

```bash
-rw-r--r-- 1 shreyansh shreyansh 0 May 25 10:10 devops-file.txt
```

### Create Users

```bash
sudo useradd tokyo
sudo useradd berlin
```

### Change Owner to tokyo

```bash
sudo chown tokyo devops-file.txt
```

### Verify

```bash
ls -l devops-file.txt
```

## Output

```bash
-rw-r--r-- 1 tokyo shreyansh 0 May 25 10:10 devops-file.txt
```

### Change Owner to berlin

```bash
sudo chown berlin devops-file.txt
```

### Verify Again

```bash
ls -l devops-file.txt
```

## Output

```bash
-rw-r--r-- 1 berlin shreyansh 0 May 25 10:10 devops-file.txt
```

---

# Task 3 – Basic chgrp Operations

## Task

Create a group and assign it to a file.

## Commands

### Create File

```bash
touch team-notes.txt
```

### Check Current Group

```bash
ls -l team-notes.txt
```

## Output

```bash
-rw-r--r-- 1 shreyansh shreyansh 0 May 25 10:20 team-notes.txt
```

### Create Group

```bash
sudo groupadd heist-team
```

### Change Group

```bash
sudo chgrp heist-team team-notes.txt
```

### Verify

```bash
ls -l team-notes.txt
```

## Output

```bash
-rw-r--r-- 1 shreyansh heist-team 0 May 25 10:20 team-notes.txt
```

---

# Task 4 – Combined Owner & Group Change

## Task

Change owner and group together using one command.

## Commands

### Create User

```bash
sudo useradd professor
```

### Create File

```bash
touch project-config.yaml
```

### Change Owner and Group

```bash
sudo chown professor:heist-team project-config.yaml
```

### Verify

```bash
ls -l project-config.yaml
```

## Output

```bash
-rw-r--r-- 1 professor heist-team 0 May 25 10:30 project-config.yaml
```

---

## Directory Ownership Change

### Create Directory

```bash
mkdir app-logs
```

### Change Owner and Group

```bash
sudo chown berlin:heist-team app-logs
```

### Verify

```bash
ls -ld app-logs
```

## Output

```bash
drwxr-xr-x 2 berlin heist-team 4096 May 25 10:35 app-logs
```

---

# Task 5 – Recursive Ownership

## Task

Apply ownership recursively on directories and files.

## Commands

### Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

### Create Group

```bash
sudo groupadd planners
```

### Apply Recursive Ownership

```bash
sudo chown -R professor:planners heist-project/
```

### Verify

```bash
ls -lR heist-project/
```

## Output

```bash
heist-project:
total 8
drwxr-xr-x 2 professor planners 4096 May 25 10:40 plans
drwxr-xr-x 2 professor planners 4096 May 25 10:40 vault

heist-project/plans:
total 0
-rw-r--r-- 1 professor planners 0 May 25 10:40 strategy.conf

heist-project/vault:
total 0
-rw-r--r-- 1 professor planners 0 May 25 10:40 gold.txt
```

---

# Task 6 – Practice Challenge

## Task

Create multiple users, groups, files, and assign different ownership.

## Commands

### Create Users

```bash
sudo useradd tokyo
sudo useradd berlin
sudo useradd nairobi
```

### Create Groups

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

### Create Directory

```bash
mkdir bank-heist
```

### Create Files

```bash
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

### Set Ownership

#### access-codes.txt

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
```

#### blueprints.pdf

```bash
sudo chown berlin:tech-team bank-heist/blueprints.pdf
```

#### escape-plan.txt

```bash
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

### Verify

```bash
ls -l bank-heist/
```

## Output

```bash
-rw-r--r-- 1 tokyo   vault-team 0 May 25 10:50 access-codes.txt
-rw-r--r-- 1 berlin  tech-team  0 May 25 10:50 blueprints.pdf
-rw-r--r-- 1 nairobi vault-team 0 May 25 10:50 escape-plan.txt
```

---

# Key Commands Reference

## View Ownership

```bash
ls -l filename
```

## Change Owner

```bash
sudo chown newowner filename
```

## Change Group

```bash
sudo chgrp newgroup filename
```

## Change Owner & Group

```bash
sudo chown owner:group filename
```

## Recursive Ownership Change

```bash
sudo chown -R owner:group directory/
```

## Change Only Group Using chown

```bash
sudo chown :groupname filename
```

---

# Files & Directories Created

## Files

- devops-file.txt
- team-notes.txt
- project-config.yaml
- heist-project/vault/gold.txt
- heist-project/plans/strategy.conf
- bank-heist/access-codes.txt
- bank-heist/blueprints.pdf
- bank-heist/escape-plan.txt

## Directories

- app-logs/
- heist-project/
- heist-project/vault/
- heist-project/plans/
- bank-heist/

---

# Ownership Summary

| File/Directory | Ownership |
|---|---|
| devops-file.txt | berlin:shreyansh |
| team-notes.txt | shreyansh:heist-team |
| project-config.yaml | professor:heist-team |
| app-logs/ | berlin:heist-team |
| heist-project/ | professor:planners |
| access-codes.txt | tokyo:vault-team |
| blueprints.pdf | berlin:tech-team |
| escape-plan.txt | nairobi:vault-team |

---

# What I Learned

1. Every Linux file has an owner and a group.
2. `chown` changes ownership while `chgrp` changes group ownership.
3. Recursive ownership with `-R` is useful for project directories and deployments.

---

# Why File Ownership Matters in DevOps

File ownership is important for:

- Application deployments
- Shared directories
- CI/CD pipelines
- Docker containers
- Server security
- Log management

---

# Submission Commands

```bash
cd 2026/day-11/
git add day-11-file-ownership.md
git commit -m "Completed Day 11 File Ownership Challenge"
git push origin main
```

---

# LinkedIn Hashtags

```text
#90DaysOfDevOps
#DevOpsLearning
#Linux
#DevOps
#SystemAdministration
```
