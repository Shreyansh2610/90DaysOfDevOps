# Day 14 – Networking Fundamentals & Troubleshooting

## Task

Get comfortable with core networking concepts and the commands you'll actually run during troubleshooting.

### Objectives

* Map the OSI vs TCP/IP models in your own words.
* Run essential connectivity commands.
* Capture a mini network check for a target host/service.
* Keep it short, practical, and repeatable.

---

# Quick Concepts

## OSI Model vs TCP/IP Model

| OSI Layer              | TCP/IP Layer | Purpose                            |
| ---------------------- | ------------ | ---------------------------------- |
| Layer 7 – Application  | Application  | User-facing services and protocols |
| Layer 6 – Presentation | Application  | Data formatting and encryption     |
| Layer 5 – Session      | Application  | Session management                 |
| Layer 4 – Transport    | Transport    | End-to-end communication           |
| Layer 3 – Network      | Internet     | Routing and IP addressing          |
| Layer 2 – Data Link    | Link         | Local network communication        |
| Layer 1 – Physical     | Link         | Physical transmission media        |

### Protocol Locations

| Protocol     | Layer            |
| ------------ | ---------------- |
| HTTP / HTTPS | Application      |
| DNS          | Application      |
| SSH          | Application      |
| TCP          | Transport        |
| UDP          | Transport        |
| IP           | Internet/Network |

### Real Example

```text
curl https://example.com
```

Flow:

```text
Application (HTTPS)
       ↓
Transport (TCP)
       ↓
Internet (IP)
       ↓
Link (Ethernet/Wi-Fi)
```

This request starts at the Application Layer and travels down the stack before being transmitted across the network.

---

# Hands-On Networking Checks

## Target Host

```text
google.com
```

---

## 1. Identity Check

### Command

```bash
hostname -I
```

### Sample Output

```text
192.168.1.105
```

### Observation

The system is using a private IPv4 address assigned by the local network.

---

## 2. Reachability Test

### Command

```bash
ping -c 4 google.com
```

### Sample Output

```text
4 packets transmitted, 4 received, 0% packet loss
rtt min/avg/max = 18.3/22.1/28.5 ms
```

### Observation

The target is reachable with no packet loss and stable latency.

---

## 3. Route Path Analysis

### Command

```bash
traceroute google.com
```

### Sample Output

```text
1 192.168.1.1
2 ISP Gateway
3 Regional Router
4 Google Edge Network
```

### Observation

Traffic passes through multiple ISP routers before reaching Google's network.

---

## 4. Listening Ports

### Command

```bash
ss -tulpn
```

### Sample Output

```text
tcp LISTEN 0 128 0.0.0.0:22
```

### Observation

SSH service is listening on TCP port 22.

---

## 5. DNS Resolution

### Command

```bash
dig google.com +short
```

### Sample Output

```text
142.250.193.110
```

### Observation

DNS successfully resolved the domain name to an IP address.

---

## 6. HTTP Check

### Command

```bash
curl -I https://google.com
```

### Sample Output

```text
HTTP/2 301
```

### Observation

Google responds with a redirect to its preferred URL.

---

## 7. Connection Snapshot

### Command

```bash
netstat -an | head
```

### Sample Observation

```text
LISTEN      : 5
ESTABLISHED : 2
```

### Observation

The machine has several services listening and a few active network connections.

---

# Mini Task – Port Probe & Interpret

## Selected Service

SSH (Port 22)

### Command

```bash
nc -zv localhost 22
```

### Sample Output

```text
Connection to localhost 22 port [tcp/ssh] succeeded!
```

### Observation

The service is reachable locally and accepting connections.

### If It Was Not Reachable

Next troubleshooting steps:

```bash
systemctl status ssh
sudo ufw status
sudo iptables -L
```

Check service status and firewall rules.

---

# Reflection

## Which command gives the fastest signal when something is broken?

**ping**

It quickly confirms whether basic network connectivity exists and whether packet loss is occurring.

---

## What layer would you inspect next if DNS fails?

### OSI Model

* Layer 7 (Application)

### TCP/IP Model

* Application Layer

Focus on resolver configuration, DNS servers, and name resolution.

---

## What layer would you inspect if an HTTP 500 error appears?

### OSI Model

* Layer 7 (Application)

### TCP/IP Model

* Application Layer

The network path is functioning; the issue is usually with the web application or backend service.

---

## Two Follow-Up Checks During a Real Incident

### Check Logs

```bash
journalctl -xe
```

Review service and system logs for errors.

### Verify Listening Services

```bash
ss -tulpn
```

Confirm that required services are listening on expected ports.

---

# Key Learnings

* OSI and TCP/IP models help isolate networking problems by layer.
* Ping verifies connectivity.
* Traceroute reveals the path packets take through the network.
* Dig validates DNS resolution.
* Curl helps test HTTP/HTTPS endpoints.
* SS and Netstat reveal active and listening network connections.
* A structured troubleshooting approach significantly reduces diagnosis time.

---

## Commands Practiced

```bash
hostname -I
ping -c 4 google.com
traceroute google.com
ss -tulpn
dig google.com +short
curl -I https://google.com
netstat -an | head
nc -zv localhost 22
```
