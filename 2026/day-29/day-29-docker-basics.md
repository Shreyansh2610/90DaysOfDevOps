# Day 29 – Introduction to Docker

## Objective

Learn the fundamentals of Docker, understand containers, and run your first Docker containers.

---

# Task 1: What is Docker?

## What is a Container and Why Do We Need Them?

A container is a lightweight, portable package that contains an application along with all its dependencies, libraries, and configuration files needed to run.

### Why Containers?

Before containers:

* Applications worked on one machine but failed on another.
* Dependency conflicts were common.
* Deployments were inconsistent.

Containers solve these problems by ensuring the application runs the same way everywhere.

### Benefits

* Lightweight
* Fast startup
* Portable
* Consistent environments
* Easy scaling
* Better resource utilization

---

## Containers vs Virtual Machines

| Feature        | Containers  | Virtual Machines |
| -------------- | ----------- | ---------------- |
| Virtualization | OS-Level    | Hardware-Level   |
| Startup Time   | Seconds     | Minutes          |
| Size           | MBs         | GBs              |
| Resource Usage | Low         | High             |
| Performance    | Near Native | Slight Overhead  |
| OS Included    | No          | Yes              |

### Virtual Machine Architecture

```text
Hardware
│
Hypervisor
│
├── VM 1 (Guest OS + App)
├── VM 2 (Guest OS + App)
└── VM 3 (Guest OS + App)
```

### Container Architecture

```text
Hardware
│
Host OS
│
Docker Engine
│
├── Container 1
├── Container 2
└── Container 3
```

Containers share the host OS kernel, making them much more efficient than VMs.

---

## Docker Architecture

Docker consists of four major components:

### 1. Docker Client

The command-line interface (CLI) used by users.

Example:

```bash
docker run nginx
```

---

### 2. Docker Daemon

The background service responsible for:

* Building images
* Running containers
* Managing networks
* Managing storage

---

### 3. Docker Images

Read-only templates used to create containers.

Examples:

* nginx
* ubuntu
* mysql
* redis

---

### 4. Docker Containers

Running instances of Docker images.

Example:

```bash
docker run nginx
```

creates a container from the nginx image.

---

### 5. Docker Registry

Stores Docker images.

Examples:

* Docker Hub
* Private Registry

Docker Hub is the default public registry.

---

## Docker Architecture Diagram

```text
                Docker Hub
                     │
                     ▼
              Docker Registry
                     │
                     ▼
+----------------------------------+
|         Docker Daemon            |
|                                  |
|  Images     Containers           |
|                                  |
+----------------------------------+
                     ▲
                     │
             Docker Client
          (docker commands)
```

### Explanation

1. User runs a Docker command.
2. Docker Client sends request to Docker Daemon.
3. Docker Daemon pulls image from Docker Hub if needed.
4. Docker Daemon creates and runs containers.

---

# Task 2: Install Docker

## Verify Installation

```bash
docker --version
```

Example Output:

```bash
Docker version 28.x.x
```

---

## Run Hello World Container

```bash
docker run hello-world
```

### What Happened?

1. Docker searched for the image locally.
2. Image was not found.
3. Docker downloaded it from Docker Hub.
4. Container started.
5. Container displayed a welcome message.
6. Container exited successfully.

---

# Task 3: Run Real Containers

## Run Nginx Container

```bash
docker run -d -p 8080:80 --name my-nginx nginx
```

### Verify

```bash
docker ps
```

Open browser:

```text
http://localhost:8080
```

You should see the Nginx welcome page.

---

## Run Ubuntu Container

```bash
docker run -it ubuntu bash
```

### Explore

```bash
ls
pwd
whoami
cat /etc/os-release
```

Exit:

```bash
exit
```

---

## List Running Containers

```bash
docker ps
```

---

## List All Containers

```bash
docker ps -a
```

---

## Stop a Container

```bash
docker stop my-nginx
```

---

## Remove a Container

```bash
docker rm my-nginx
```

---

# Task 4: Explore Docker Features

## Detached Mode

Run container in background:

```bash
docker run -d nginx
```

### Difference

* Terminal remains free.
* Container runs in background.

---

## Custom Container Name

```bash
docker run -d --name webserver nginx
```

---

## Port Mapping

```bash
docker run -d -p 8080:80 nginx
```

Meaning:

```text
Host Port 8080 → Container Port 80
```

---

## View Container Logs

```bash
docker logs webserver
```

---

## Execute Commands Inside Running Container

```bash
docker exec -it webserver bash
```

Example:

```bash
ls /usr/share/nginx/html
```

Exit:

```bash
exit
```

---

# Commands Learned Today

```bash
docker --version

docker run hello-world

docker run nginx

docker run -d nginx

docker run -it ubuntu bash

docker run -d -p 8080:80 nginx

docker run -d --name webserver nginx

docker ps

docker ps -a

docker stop webserver

docker rm webserver

docker logs webserver

docker exec -it webserver bash
```

---

# Key Learnings

* Docker packages applications into containers.
* Containers are lightweight compared to virtual machines.
* Docker uses Images to create Containers.
* Docker Hub stores public images.
* Containers can run in interactive or detached mode.
* Port mapping exposes container services to the host.
* Docker logs and exec commands help with troubleshooting.

---

# Conclusion

Today I learned the fundamentals of Docker and successfully ran my first containers. I explored Docker architecture, understood the difference between containers and virtual machines, worked with Nginx and Ubuntu containers, managed container lifecycles, viewed logs, and executed commands inside running containers. Docker is a foundational technology for modern DevOps, CI/CD pipelines, and container orchestration platforms like Kubernetes.
