# Linux Commands Cheat Sheet

## Process Management

| Command | Usage |
|---------|--------|
| `ps aux` | Show all running processes |
| `top` | Monitor live system processes |
| `htop` | Interactive process viewer |
| `kill PID` | Kill a process by PID |
| `kill -9 PID` | Force kill a process |
| `pkill nginx` | Kill process by name |
| `pgrep mysql` | Find process ID by name |
| `jobs` | Show background jobs |
| `bg` | Resume job in background |
| `fg` | Bring background job to foreground |
| `systemctl status nginx` | Check service status |
| `systemctl restart nginx` | Restart a service |

---

## File System Commands

| Command | Usage |
|---------|--------|
| `pwd` | Show current directory |
| `ls -la` | List files with details |
| `cd /path` | Change directory |
| `mkdir project` | Create new directory |
| `rm -rf folder` | Remove directory recursively |
| `cp file1 file2` | Copy files |
| `mv old new` | Move or rename files |
| `find / -name file.txt` | Search file by name |
| `du -sh *` | Show directory sizes |
| `df -h` | Check disk usage |
| `chmod 755 file.sh` | Change file permissions |
| `chown user:user file` | Change file ownership |
| `cat file.txt` | Display file content |
| `tail -f /var/log/syslog` | Monitor logs in real time |
| `grep "error" app.log` | Search text inside files |

---

## Networking Troubleshooting

| Command | Usage |
|---------|--------|
| `ping google.com` | Check network connectivity |
| `ip addr` | Show IP addresses |
| `curl https://example.com` | Test HTTP response |
| `dig google.com` | Check DNS records |
| `netstat -tulnp` | Show listening ports |
| `ss -tulnp` | Display socket statistics |
| `traceroute google.com` | Trace network route |
| `nslookup google.com` | Query DNS information |
| `wget URL` | Download files from internet |
| `ssh user@server` | Connect to remote server |

---

## Useful Log Commands

| Command | Usage |
|---------|--------|
| `journalctl -xe` | View systemd logs |
| `journalctl -u nginx` | View logs for a service |
| `dmesg` | Show kernel logs |
| `tail -100 logfile.log` | View last 100 log lines |

---

## System Information

| Command | Usage |
|---------|--------|
| `uname -a` | Show system information |
| `uptime` | Check system uptime |
| `free -h` | Display memory usage |
| `whoami` | Show current user |
| `hostname` | Display system hostname |
