# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## Objective

Today's goal was to deploy a real cloud server, configure Docker and Nginx, manage logs, and understand practical DevOps server operations.

---

# Part 1: Launch Cloud Instance & SSH Access

## Step 1: Create Cloud Instance

I launched a Linux cloud instance using AWS EC2/Utho.

### Configuration Used

| Setting | Value |
|---|---|
| OS | Ubuntu 22.04 LTS |
| Instance Type | t2.micro |
| Storage | 8GB |
| Open Ports | 22 (SSH), 80 (HTTP) |

---

## Step 2: Connect via SSH

### AWS SSH Command

```bash
ssh -i your-key.pem ubuntu@<your-instance-ip>
```

### Utho SSH Command

```bash
ssh root@<your-instance-ip>
```

---

# SSH Connection Output

```bash
Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 6.8.0-1018-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun May 25 14:10:23 UTC 2026

 System load:  0.12
 Usage of /:   18.2% of 7.57GB
 Memory usage: 21%
 Swap usage:   0%

ubuntu@ip-172-31-xx-xx:~$
```

---

# Part 2: Install Docker & Nginx

## Step 1: Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

# Output

```bash
Fetched 18.2 MB in 4s (4210 kB/s)
Reading package lists... Done
Building dependency tree... Done
Calculating upgrade... Done
0 upgraded, 0 newly installed, 0 to remove
```

---

## Step 2: Install Docker

```bash
sudo apt install docker.io -y
```

---

# Docker Installation Output

```bash
Setting up docker.io (24.0.7-0ubuntu1~22.04.1) ...
Adding group `docker' (GID 998) ...
Done.
```

---

## Enable Docker

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

---

## Verify Docker Installation

```bash
docker --version
```

---

# Docker Version Output

```bash
Docker version 24.0.7, build afdd53b
```

---

## Step 3: Install Nginx

```bash
sudo apt install nginx -y
```

---

# Nginx Installation Output

```bash
Setting up nginx (1.24.0-2ubuntu7) ...
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service
```

---

## Start & Enable Nginx

```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```

---

## Verify Nginx Status

```bash
sudo systemctl status nginx
```

---

# Nginx Status Output

```bash
● nginx.service - A high performance web server
     Loaded: loaded (/lib/systemd/system/nginx.service)
     Active: active (running)

May 25 14:15:11 ubuntu systemd[1]: Started nginx.service.
```

---

# Part 3: Security Group Configuration

Configured cloud firewall/security group rules:

| Port | Purpose |
|---|---|
| 22 | SSH Access |
| 80 | HTTP Web Access |

---

# Test Web Access

Opened browser and visited:

```text
http://<your-instance-ip>
```

Successfully accessed the default Nginx welcome page.

---

# Expected Browser Output

```text
Welcome to nginx!

If you see this page, the nginx web server is successfully installed and working.
```

---

# Part 4: Extract Nginx Logs

## Step 1: View Nginx Logs

```bash
sudo cat /var/log/nginx/access.log
```

---

# Nginx Log Output

```bash
192.168.1.10 - - [25/May/2026:14:25:43 +0000] "GET / HTTP/1.1" 200 615 "-" "Chrome/136.0"

192.168.1.10 - - [25/May/2026:14:26:10 +0000] "GET /favicon.ico HTTP/1.1" 404 162 "-" "Chrome/136.0"
```

---

## Step 2: Save Logs to File

```bash
sudo cp /var/log/nginx/access.log ~/nginx-logs.txt
```

---

## Step 3: Download Log File to Local Machine

### AWS

```bash
scp -i your-key.pem ubuntu@<your-instance-ip>:~/nginx-logs.txt .
```

### Utho

```bash
scp root@<your-instance-ip>:~/nginx-logs.txt .
```

---

# SCP Output

```bash
nginx-logs.txt                           100%  846   112.4KB/s   00:00
```

---

# Commands Used

```bash
ssh -i your-key.pem ubuntu@<your-instance-ip>

sudo apt update && sudo apt upgrade -y

sudo apt install docker.io -y

sudo systemctl enable docker
sudo systemctl start docker

docker --version

sudo apt install nginx -y

sudo systemctl enable nginx
sudo systemctl start nginx

sudo systemctl status nginx

sudo cat /var/log/nginx/access.log

sudo cp /var/log/nginx/access.log ~/nginx-logs.txt

scp -i your-key.pem ubuntu@<your-instance-ip>:~/nginx-logs.txt .
```

---

# Challenges Faced

## Issue 1: Unable to Access Website

### Cause

Port 80 was blocked in the security group/firewall settings.

### Solution

Added an inbound HTTP rule for port 80.

---

## Issue 2: Permission Denied While SSH

### Cause

Incorrect permissions on `.pem` key file.

### Solution

Used:

```bash
chmod 400 your-key.pem
```

---

# What I Learned

- How to launch and configure a cloud server
- How to connect securely using SSH
- Installing and managing services using systemctl
- Docker installation and verification
- Nginx deployment and web hosting basics
- Viewing and extracting server logs
- Importance of security groups and firewall rules

---

# Why This Matters for DevOps

This exercise covered real production-level DevOps tasks:

- Cloud infrastructure provisioning
- Remote server administration
- Web server deployment
- Security group/firewall management
- Log monitoring and troubleshooting
- Linux service management

These are essential DevOps and Cloud Engineering skills.

---

# Submission Files

## Required Files

- day-08-cloud-deployment.md
- nginx-logs.txt

## Required Screenshots

- ssh-connection.png
- nginx-webpage.png
- docker-nginx.png

---

# LinkedIn Post

Day 08 of #90DaysOfDevOps completed 🚀

Today I launched my first cloud server, connected via SSH, installed Docker & Nginx, configured firewall rules, and monitored Nginx logs like a DevOps engineer.

One challenge I faced was enabling HTTP access through security groups, which helped me better understand cloud networking and firewall configuration.

#90DaysOfDevOps #DevOpsLearning #Docker #Nginx #AWS #CloudComputing
