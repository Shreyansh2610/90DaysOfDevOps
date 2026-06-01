# Day 15 – Networking Concepts (DNS, IP Addressing, CIDR & Ports)

## Objective

Build a strong understanding of core networking concepts used daily in DevOps:

* DNS Resolution
* IPv4 Addressing
* Public vs Private Networks
* CIDR & Subnetting
* Network Ports

---

# Task 1: DNS – How Names Become IPs

## What happens when you type google.com in a browser?

When a user enters `google.com` into a browser, the system first checks local DNS cache. If the IP address is not cached, a DNS query is sent to a DNS resolver. The resolver contacts DNS servers to find the IP address associated with the domain. Once the IP is returned, the browser establishes a connection to that server and loads the website.

---

## Common DNS Record Types

### A Record

Maps a domain name to an IPv4 address.

### AAAA Record

Maps a domain name to an IPv6 address.

### CNAME Record

Creates an alias from one domain name to another.

### MX Record

Specifies mail servers responsible for receiving email.

### NS Record

Identifies the authoritative name servers for a domain.

---

## Command

```bash
dig google.com
```

### Sample Output

```text
;; ANSWER SECTION:
google.com.      300     IN      A       142.250.193.14
```

### Findings

| Item     | Value          |
| -------- | -------------- |
| A Record | 142.250.193.14 |
| TTL      | 300 seconds    |

---

# Task 2: IP Addressing

## What is an IPv4 Address?

An IPv4 address is a 32-bit numeric identifier assigned to devices on a network. It consists of four octets separated by dots.

Example:

```text
192.168.1.10
```

Each octet ranges from 0–255.

---

## Public vs Private IP

### Public IP

Accessible over the internet and globally unique.

Example:

```text
8.8.8.8
```

### Private IP

Used inside local networks and not routable on the public internet.

Example:

```text
192.168.1.100
```

---

## Private IP Ranges

```text
10.0.0.0 – 10.255.255.255

172.16.0.0 – 172.31.255.255

192.168.0.0 – 192.168.255.255
```

---

## Command

```bash
ip addr show
```

### Sample Output

```text
2: eth0:
    inet 192.168.1.50/24
```

### Findings

Private IP detected:

```text
192.168.1.50
```

Reason:

It belongs to the 192.168.x.x private address range.

---

# Task 3: CIDR & Subnetting

## What does /24 mean?

A `/24` means the first 24 bits are reserved for the network portion and the remaining 8 bits are available for host addresses.

Example:

```text
192.168.1.0/24
```

Subnet Mask:

```text
255.255.255.0
```

---

## Usable Hosts

### /24

```text
256 total IPs
254 usable hosts
```

### /16

```text
65,536 total IPs
65,534 usable hosts
```

### /28

```text
16 total IPs
14 usable hosts
```

---

## Why Do We Subnet?

Subnetting divides large networks into smaller logical networks. This improves network organization, security, performance, and efficient IP address utilization.

---

## CIDR Table

| CIDR | Subnet Mask     | Total IPs | Usable Hosts |
| ---- | --------------- | --------- | ------------ |
| /24  | 255.255.255.0   | 256       | 254          |
| /16  | 255.255.0.0     | 65,536    | 65,534       |
| /28  | 255.255.255.240 | 16        | 14           |

---

# Task 4: Ports – The Doors to Services

## What is a Port?

A port is a logical communication endpoint used by applications and services. Ports allow multiple services to operate simultaneously on a single IP address.

---

## Common Ports

| Port  | Service |
| ----- | ------- |
| 22    | SSH     |
| 80    | HTTP    |
| 443   | HTTPS   |
| 53    | DNS     |
| 3306  | MySQL   |
| 6379  | Redis   |
| 27017 | MongoDB |

---

## Command

```bash
ss -tulpn
```

### Sample Output

```text
tcp LISTEN 0 128 0.0.0.0:22
tcp LISTEN 0 128 127.0.0.1:3306
```

### Findings

| Port | Service        |
| ---- | -------------- |
| 22   | SSH Server     |
| 3306 | MySQL Database |

---

# Task 5: Putting It Together

## Scenario 1

### You run:

```bash
curl http://myapp.com:8080
```

### Networking Concepts Involved

1. DNS resolves `myapp.com` into an IP address.
2. TCP establishes a connection to port `8080`.
3. HTTP request is sent to the application running on that port.
4. Routing and IP networking deliver packets between client and server.

---

## Scenario 2

### Your application cannot reach:

```text
10.0.1.50:3306
```

### What would you check first?

1. Verify network connectivity using `ping` or `telnet`.
2. Confirm MySQL is listening on port `3306`.
3. Check firewall/security group rules.
4. Verify the database server IP address and subnet routing.
5. Ensure the database service is running.

---

# Key Learnings

### 1. DNS Translates Human-Friendly Names into IP Addresses

Without DNS, users would need to remember IP addresses instead of domain names.

### 2. CIDR Helps Efficiently Manage Networks

CIDR notation defines network size and determines available host addresses.

### 3. Ports Identify Services Running on a Host

Multiple applications can share the same IP because they use different ports.

---

# Commands Executed

```bash
dig google.com

ip addr show

ss -tulpn
```

---

# Conclusion

Today I learned how DNS converts domain names into IP addresses, how IPv4 addressing and private networks work, how CIDR notation determines network size, and how ports enable communication with different services. These concepts form the foundation of troubleshooting and designing infrastructure in DevOps.
