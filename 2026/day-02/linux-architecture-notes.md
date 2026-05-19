# Linux Architecture, Processes, and systemd

## 1. Core Components of Linux

### Kernel
- Core part of Linux OS
- Manages:
  - CPU
  - Memory
  - Devices
  - Filesystems
  - Processes
- Acts as bridge between hardware and software

### User Space
- Area where user applications run
- Examples:
  - Bash
  - Nginx
  - Docker
  - VS Code
- Users interact with Linux through commands and applications

### Init / systemd
- First process started by kernel
- PID = 1
- Responsible for:
  - Starting services
  - Managing background processes
  - Handling system boot

---

## 2. Process Management

### What is a Process?
- A running instance of a program
- Each process has:
  - PID (Process ID)
  - Parent Process
  - Memory usage
  - CPU usage

### Process Creation
- Linux creates processes using:
  - `fork()` → creates copy of process
  - `exec()` → loads new program into process

### Common Process States
| State | Meaning |
|------|------|
| Running | Process is using CPU |
| Sleeping | Waiting for resource/input |
| Stopped | Paused process |
| Zombie | Process finished but parent didn't clean it |
| Orphan | Parent process terminated |

---

## 3. systemd Overview

### What is systemd?
- Modern Linux init system
- Manages services and boot process

### Why systemd Matters
- Faster boot process
- Automatic service restart
- Centralized logging with `journalctl`
- Dependency management between services

### Useful systemd Commands
```bash
systemctl status nginx
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
journalctl -u nginx
