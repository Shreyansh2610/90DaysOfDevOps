# Day 13 – Linux Volume Management (LVM)

## Task
Learn LVM to manage storage flexibly – create, extend, and mount volumes.

---

# Before You Start

## Switch to Root User

```bash
sudo -i
```

OR

```bash
sudo su
```

---

# Create Virtual Disk (If No Spare Disk Available)

## Command

```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
```

## Output

```bash
1024+0 records in
1024+0 records out
1073741824 bytes (1.1 GB) copied
```

---

## Attach Loop Device

```bash
losetup -fP /tmp/disk1.img
```

## Verify Loop Device

```bash
losetup -a
```

## Output

```bash
/dev/loop0: []: (/tmp/disk1.img)
```

---

# Task 1 – Check Current Storage

## Commands

```bash
lsblk
pvs
vgs
lvs
df -h
```

## Output

### lsblk

```bash
NAME        MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sda           8:0    0  20G  0 disk
├─sda1        8:1    0  19G  0 part /
└─sda2        8:2    0   1G  0 part [SWAP]
loop0         7:0    0   1G  0 loop
```

### pvs

```bash
No physical volume found
```

### vgs

```bash
No volume groups found
```

### lvs

```bash
No logical volumes found
```

### df -h

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        19G  5.0G   13G  30% /
```

---

# Task 2 – Create Physical Volume

## Command

```bash
pvcreate /dev/loop0
```

## Output

```bash
Physical volume "/dev/loop0" successfully created.
```

## Verify Physical Volume

```bash
pvs
```

## Output

```bash
PV           VG   Fmt  Attr PSize PFree
/dev/loop0        lvm2 ---  1.00g 1.00g
```

---

# Task 3 – Create Volume Group

## Command

```bash
vgcreate devops-vg /dev/loop0
```

## Output

```bash
Volume group "devops-vg" successfully created
```

## Verify Volume Group

```bash
vgs
```

## Output

```bash
VG         #PV #LV #SN Attr   VSize VFree
devops-vg    1   0   0 wz--n- 1.00g 1.00g
```

---

# Task 4 – Create Logical Volume

## Command

```bash
lvcreate -L 500M -n app-data devops-vg
```

## Output

```bash
Logical volume "app-data" created.
```

## Verify Logical Volume

```bash
lvs
```

## Output

```bash
LV        VG         Attr       LSize
app-data  devops-vg -wi-a----- 500.00m
```

---

# Task 5 – Format and Mount Logical Volume

## Format Volume

```bash
mkfs.ext4 /dev/devops-vg/app-data
```

## Output

```bash
Creating filesystem with 512000 1k blocks
Filesystem UUID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
Superblock backups stored on blocks:
```

---

## Create Mount Directory

```bash
mkdir -p /mnt/app-data
```

---

## Mount Logical Volume

```bash
mount /dev/devops-vg/app-data /mnt/app-data
```

---

## Verify Mounted Storage

```bash
df -h /mnt/app-data
```

## Output

```bash
Filesystem                       Size  Used Avail Use% Mounted on
/dev/mapper/devops--vg-app--data 487M   24K  451M   1% /mnt/app-data
```

---

# Task 6 – Extend the Volume

## Extend Logical Volume

```bash
lvextend -L +200M /dev/devops-vg/app-data
```

## Output

```bash
Size of logical volume devops-vg/app-data changed
from 500.00 MiB to 700.00 MiB
```

---

## Resize Filesystem

```bash
resize2fs /dev/devops-vg/app-data
```

## Output

```bash
Filesystem resized successfully
```

---

## Verify Extended Storage

```bash
df -h /mnt/app-data
```

## Output

```bash
Filesystem                       Size  Used Avail Use% Mounted on
/dev/mapper/devops--vg-app--data 682M   25K  650M   1% /mnt/app-data
```

---

# Important LVM Commands

| Command | Description |
|----------|-------------|
| `pvcreate` | Create Physical Volume |
| `vgcreate` | Create Volume Group |
| `lvcreate` | Create Logical Volume |
| `lvextend` | Extend Logical Volume |
| `resize2fs` | Resize EXT4 Filesystem |
| `pvs` | Show Physical Volumes |
| `vgs` | Show Volume Groups |
| `lvs` | Show Logical Volumes |

---

# What I Learned

1. LVM provides flexible storage management in Linux.
2. Logical Volumes can be resized dynamically without repartitioning.
3. Physical Volumes, Volume Groups, and Logical Volumes work together in layered storage architecture.

---

# Submission Steps

## Create Directory

```bash
mkdir -p 2026/day-13
```

## Create Markdown File

```bash
nano 2026/day-13/day-13-lvm.md
```

## Git Commands

```bash
git add .
git commit -m "Added Day 13 Linux LVM challenge"
git push origin main
```

---

# LinkedIn Learning Summary

Completed Day 13 of #90DaysOfDevOps 🚀

Today I learned:

✅ Physical Volumes (PV)  
✅ Volume Groups (VG)  
✅ Logical Volumes (LV)  
✅ Mounting Storage  
✅ Extending Storage Dynamically  

Linux LVM makes storage management scalable and flexible for real-world DevOps environments.

#DevOps #Linux #LVM #CloudComputing #SystemAdministration
