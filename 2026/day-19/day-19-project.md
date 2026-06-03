# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## Overview

This project demonstrates practical shell scripting skills by automating:

* Log rotation and cleanup
* Server backup creation and retention
* Cron job scheduling
* Centralized maintenance automation

---

# Task 1: Log Rotation Script

## log_rotate.sh

```bash
#!/bin/bash

set -euo pipefail

LOG_DIR="${1:-}"

if [[ -z "$LOG_DIR" ]]; then
    echo "Usage: $0 <log_directory>"
    exit 1
fi

if [[ ! -d "$LOG_DIR" ]]; then
    echo "Error: Directory does not exist."
    exit 1
fi

compressed_count=0
deleted_count=0

while IFS= read -r file; do
    gzip "$file"
    ((compressed_count++))
done < <(find "$LOG_DIR" -type f -name "*.log" -mtime +7)

while IFS= read -r file; do
    rm -f "$file"
    ((deleted_count++))
done < <(find "$LOG_DIR" -type f -name "*.gz" -mtime +30)

echo "Compressed files: $compressed_count"
echo "Deleted files: $deleted_count"
```

### Example

```bash
./log_rotate.sh /var/log/myapp
```

### Sample Output

```text
Compressed files: 12
Deleted files: 5
```

---

# Task 2: Server Backup Script

## backup.sh

```bash
#!/bin/bash

set -euo pipefail

SOURCE_DIR="${1:-}"
BACKUP_DIR="${2:-}"

if [[ -z "$SOURCE_DIR" || -z "$BACKUP_DIR" ]]; then
    echo "Usage: $0 <source_directory> <backup_directory>"
    exit 1
fi

if [[ ! -d "$SOURCE_DIR" ]]; then
    echo "Error: Source directory does not exist."
    exit 1
fi

mkdir -p "$BACKUP_DIR"

TIMESTAMP=$(date +%Y-%m-%d_%H-%M-%S)
ARCHIVE_NAME="backup-${TIMESTAMP}.tar.gz"
ARCHIVE_PATH="${BACKUP_DIR}/${ARCHIVE_NAME}"

tar -czf "$ARCHIVE_PATH" "$SOURCE_DIR"

if [[ ! -f "$ARCHIVE_PATH" ]]; then
    echo "Backup creation failed."
    exit 1
fi

SIZE=$(du -h "$ARCHIVE_PATH" | cut -f1)

echo "Backup created successfully"
echo "Archive: $ARCHIVE_NAME"
echo "Size: $SIZE"

find "$BACKUP_DIR" -type f -name "backup-*.tar.gz" -mtime +14 -delete
```

### Example

```bash
./backup.sh /var/www/html /backups
```

### Sample Output

```text
Backup created successfully
Archive: backup-2026-06-03_20-30-00.tar.gz
Size: 150M
```

---

# Task 3: Crontab

## View Existing Cron Jobs

```bash
crontab -l
```

## Cron Syntax

```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

## Cron Entries

### Run log rotation every day at 2 AM

```cron
0 2 * * * /home/user/scripts/log_rotate.sh /var/log/myapp
```

### Run backup every Sunday at 3 AM

```cron
0 3 * * 0 /home/user/scripts/backup.sh /var/www/html /backups
```

### Run health check every 5 minutes

```cron
*/5 * * * * /home/user/scripts/health_check.sh
```

---

# Task 4: Scheduled Maintenance Script

## maintenance.sh

```bash
#!/bin/bash

set -euo pipefail

LOGFILE="/var/log/maintenance.log"

log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> "$LOGFILE"
}

run_log_rotation() {
    /home/user/scripts/log_rotate.sh /var/log/myapp >> "$LOGFILE" 2>&1
}

run_backup() {
    /home/user/scripts/backup.sh /var/www/html /backups >> "$LOGFILE" 2>&1
}

log_message "Maintenance started"

run_log_rotation
run_backup

log_message "Maintenance completed"
```

### Cron Entry

Run daily at 1 AM:

```cron
0 1 * * * /home/user/scripts/maintenance.sh
```

---

# Sample Maintenance Log

```text
2026-06-03 01:00:00 - Maintenance started
Compressed files: 10
Deleted files: 3
Backup created successfully
Archive: backup-2026-06-03_01-00-01.tar.gz
Size: 120M
2026-06-03 01:00:05 - Maintenance completed
```

---

# What I Learned

1. Shell scripts become more maintainable when functions and strict mode (`set -euo pipefail`) are used.
2. Cron jobs allow reliable automation of repetitive server administration tasks.
3. Log rotation and backup retention policies help manage disk space and improve system reliability.

---

# Submission

```bash
mkdir -p 2026/day-19

cp log_rotate.sh 2026/day-19/
cp backup.sh 2026/day-19/
cp maintenance.sh 2026/day-19/
cp day-19-project.md 2026/day-19/

git add .
git commit -m "Day 19 - Shell scripting project: log rotation, backup and cron jobs"
git push origin main
```
