# Day 09 Challenge

## Users & Groups Created

### Users
- tokyo
- berlin
- professor
- nairobi

### Groups
- developers
- admins
- project-team

---

## Group Assignments

| User | Groups |
|------|---------|
| tokyo | developers, project-team |
| berlin | developers, admins |
| professor | admins |
| nairobi | project-team |

---

## Directories Created

| Directory | Group Owner | Permissions |
|-----------|-------------|-------------|
| /opt/dev-project | developers | 775 |
| /opt/team-workspace | project-team | 775 |

---

## Commands Used

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor
sudo useradd -m nairobi

sudo passwd tokyo
sudo passwd berlin
sudo passwd professor
sudo passwd nairobi

sudo groupadd developers
sudo groupadd admins
sudo groupadd project-team

sudo usermod -aG developers tokyo
sudo usermod -aG developers berlin
sudo usermod -aG admins berlin
sudo usermod -aG admins professor
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo

sudo mkdir -p /opt/dev-project
sudo mkdir -p /opt/team-workspace

sudo chgrp developers /opt/dev-project
sudo chgrp project-team /opt/team-workspace

sudo chmod 775 /opt/dev-project
sudo chmod 775 /opt/team-workspace

sudo -u tokyo touch /opt/dev-project/tokyo.txt
sudo -u berlin touch /opt/dev-project/berlin.txt
sudo -u nairobi touch /opt/team-workspace/nairobi.txt
```

---

## Verification Commands

```bash
cat /etc/passwd
cat /etc/group

groups tokyo
groups berlin
groups professor
groups nairobi

ls -ld /opt/dev-project
ls -ld /opt/team-workspace

ls -l /opt/dev-project
ls -l /opt/team-workspace
```

---

## What I Learned

1. How Linux users and groups work together for permission management.
2. How to assign multiple groups to users using `usermod -aG`.
3. How directory permissions and group ownership control shared access in DevOps environments.

---

## Troubleshooting

### Permission denied
Use sudo:

```bash
sudo command
```

### User cannot access directory

Check group membership:

```bash
groups username
```

Check permissions:

```bash
ls -ld /path
```
