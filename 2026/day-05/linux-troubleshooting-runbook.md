# Day 05 – Linux Troubleshooting Runbook

## Target Service / Process
Service Chosen: Docker

Purpose:
Investigate overall system health and verify whether Docker service is running correctly.

---

# Environment Basics

## 1. Kernel & System Information

### Command
```bash
uname -a
```

### Observation
System is running Ubuntu Linux with a stable kernel version.

---

## 2. Distribution Information

### Command
```bash
lsb_release -a
```

### Observation
Ubuntu 24.04 LTS detected. Stable production-ready environment.

---

# Filesystem Sanity Checks

## 3. Create Temporary Troubleshooting Directory

### Command
```bash
mkdir -p /tmp/runbook-demo
```

### Observation
Temporary troubleshooting directory created successfully.

---

## 4. Copy & Verify File Operations

### Command
```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

### Observation
Filesystem write and copy operations are working correctly.

---

# CPU & Memory Snapshot

## 5. Process Resource Usage

### Command
```bash
ps -o pid,pcpu,pmem,comm -C dockerd
```

### Observation
Docker daemon is using minimal CPU and memory resources.

---

## 6. Memory Availability

### Command
```bash
free -h
```

### Observation
Sufficient free memory available. Swap usage is normal.

---

# Disk & IO Snapshot

## 7. Disk Space Usage

### Command
```bash
df -h
```

### Observation
Disk usage is within acceptable limits with enough free storage.

---

## 8. Log Directory Size

### Command
```bash
du -sh /var/log
```

### Observation
Log directory size is manageable and not causing disk pressure.

---

# Network Snapshot

## 9. Listening Services

### Command
```bash
ss -tulpn
```

### Observation
Docker and system services are listening on expected ports.

---

## 10. Service Connectivity Check

### Command
```bash
curl -I http://localhost
```

### Observation
Local service endpoint is reachable and returning HTTP 200 response.

---

# Logs Reviewed

## 11. Docker Service Logs

### Command
```bash
journalctl -u docker -n 50
```

### Observation
No recent critical Docker errors detected in logs.

---

## 12. System Log Monitoring

### Command
```bash
tail -n 50 /var/log/syslog
```

### Observation
No kernel panic, OOM kill, or major warnings observed.

---

# Quick Findings

- Docker service is healthy
- CPU and memory usage are normal
- Disk space is sufficient
- Network connectivity is functioning properly
- No critical issues found in logs

---

# If This Worsens (Next Steps)

## 1. Restart Docker Service

```bash
sudo systemctl restart docker
sudo systemctl status docker
```

Purpose:
Restart the service if it becomes unresponsive.

---

## 2. Monitor Live Logs

```bash
journalctl -u docker -f
```

Purpose:
Track real-time Docker logs for recurring issues.

---

## 3. Capture Deep Diagnostics

```bash
strace -p <PID>
```

Purpose:
Trace system calls if the process hangs or behaves abnormally.

---

# Resources

- man top
- man ps
- man journalctl
- man ss
- Docker Documentation
- Ubuntu Server Documentation
