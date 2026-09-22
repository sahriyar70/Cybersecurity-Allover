# Cybersecurity Scanning & Nmap — Complete Notes

## 1. What is Scanning?

**Scanning** is the process of collecting information about a target system, network, or host to identify:

* Active hosts
* Open ports
* Running services
* Service versions
* Operating systems
* Potential security weaknesses

Scanning is commonly used in:

* Network administration
* Cybersecurity
* Vulnerability assessment
* Penetration testing
* Network troubleshooting

---

## 2. What is Nmap?

**Nmap (Network Mapper)** is an open-source network scanning and security auditing tool.

It can be used to discover:

* Live hosts
* Open/closed/filtered ports
* Running services
* Service versions
* Operating systems
* Network information

### Basic Syntax

```bash
nmap [options] <target>
```

Example:

```bash
nmap 192.168.1.10
```

---

# 3. Basic Target Scanning

## Scan a Single Host

```bash
nmap 192.168.1.10
```

Scans the target host for commonly used TCP ports.

---

## Scan Multiple Hosts

```bash
nmap 192.168.1.10 192.168.1.20
```

---

## Scan an IP Range

```bash
nmap 192.168.1.1-50
```

Scans hosts from `192.168.1.1` to `192.168.1.50`.

---

## Scan an Entire Subnet

```bash
nmap 192.168.1.0/24
```

A `/24` network normally contains 256 IPv4 addresses.

---

# 4. Host Discovery

To discover which hosts are currently active:

```bash
nmap -sn 192.168.1.0/24
```

`-sn` performs **host discovery without a port scan**.

It helps identify live devices such as:

* PCs
* Servers
* Routers
* Phones
* IoT devices

---

# 5. Port Scanning

A port represents a communication endpoint used by network services.

Example:

```bash
nmap 192.168.1.10
```

Nmap checks commonly used ports and reports their states.

### Common Port States

| State    | Meaning                                                              |
| -------- | -------------------------------------------------------------------- |
| Open     | A service is listening on the port                                   |
| Closed   | The port is reachable but no service is listening                    |
| Filtered | A firewall or packet filter prevents Nmap from determining the state |

---

# 6. Scan Specific Ports

```bash
nmap -p 80 192.168.1.10
```

Scan multiple specific ports:

```bash
nmap -p 22,80,443 192.168.1.10
```

---

# 7. Scan a Port Range

```bash
nmap -p 1-1000 192.168.1.10
```

Scans ports from `1` to `1000`.

---

# 8. Scan All TCP Ports

```bash
nmap -p- 192.168.1.10
```

`-p-` means scan all TCP ports from `1` to `65535`.

---

# 9. Service and Version Detection

```bash
nmap -sV 192.168.1.10
```

`-sV` attempts to identify:

* Service name
* Service version
* Application information

Example:

```text
22/tcp   open   ssh      OpenSSH
80/tcp   open   http     Apache
443/tcp  open   https    nginx
```

---

# 10. Operating System Detection

```bash
nmap -O 192.168.1.10
```

`-O` attempts to identify the target's operating system.

Example:

```text
OS details: Linux
```

OS detection may require administrator/root privileges and may not always be accurate.

---

# 11. Aggressive Scan

```bash
nmap -A 192.168.1.10
```

`-A` enables several advanced detection features, including:

* OS detection
* Version detection
* Script scanning
* Traceroute

Use it carefully because it generates more traffic than a basic scan.

---

# 12. TCP SYN Scan

```bash
nmap -sS 192.168.1.10
```

`-sS` performs a **TCP SYN scan**.

It is commonly used for efficient TCP port discovery.

---

# 13. UDP Scan

```bash
nmap -sU 192.168.1.10
```

`-sU` scans UDP ports.

Common UDP services include:

* DNS — 53
* DHCP — 67/68
* SNMP — 161

UDP scanning is generally slower than TCP scanning.

---

# 14. Default Nmap Scripts

```bash
nmap -sC 192.168.1.10
```

`-sC` runs Nmap's default scripts.

These scripts can provide additional information about detected services.

---

# 15. Service Detection + Default Scripts

```bash
nmap -sC -sV 192.168.1.10
```

This is a common combination for service enumeration.

---

# 16. OS + Service Detection

```bash
nmap -O -sV 192.168.1.10
```

This attempts to identify both:

* Operating system
* Running services and versions

---

# 17. Output Results to a File

## Normal Output

```bash
nmap -oN scan.txt 192.168.1.10
```

Saves the scan in normal text format.

## XML Output

```bash
nmap -oX scan.xml 192.168.1.10
```

Useful for tools that process XML data.

## Grepable Output

```bash
nmap -oG scan.txt 192.168.1.10
```

Useful for text processing.

## Save in Multiple Formats

```bash
nmap -oA scan 192.168.1.10
```

Creates output files using the same base name.

---

# 18. Nmap Timing

Nmap provides timing templates from `T0` to `T5`.

| Option | General Purpose |
| ------ | --------------- |
| `-T0`  | Very slow       |
| `-T1`  | Slow            |
| `-T2`  | Polite          |
| `-T3`  | Normal          |
| `-T4`  | Faster          |
| `-T5`  | Very aggressive |

Example:

```bash
nmap -T4 192.168.1.10
```

---

# 19. Verbose Mode

```bash
nmap -v 192.168.1.10
```

Shows more information during the scan.

For even more details:

```bash
nmap -vv 192.168.1.10
```

---

# 20. Nmap Help

```bash
nmap -h
```

Displays Nmap's help information.

---

# 21. Check Nmap Version

```bash
nmap --version
```

Displays the installed Nmap version.

---

# 22. Common Nmap Cheat Sheet

| Purpose           | Command                  |
| ----------------- | ------------------------ |
| Basic scan        | `nmap <IP>`              |
| Host discovery    | `nmap -sn <network>`     |
| Specific port     | `nmap -p 80 <IP>`        |
| Multiple ports    | `nmap -p 22,80,443 <IP>` |
| Port range        | `nmap -p 1-1000 <IP>`    |
| All ports         | `nmap -p- <IP>`          |
| Service detection | `nmap -sV <IP>`          |
| OS detection      | `nmap -O <IP>`           |
| SYN scan          | `nmap -sS <IP>`          |
| UDP scan          | `nmap -sU <IP>`          |
| Default scripts   | `nmap -sC <IP>`          |
| Script + version  | `nmap -sC -sV <IP>`      |
| Aggressive scan   | `nmap -A <IP>`           |
| Verbose           | `nmap -v <IP>`           |
| Save output       | `nmap -oN scan.txt <IP>` |

---

# 23. Practical Scanning Workflow

A basic authorized security assessment can follow this general workflow:

```text
1. Discover live hosts
        ↓
2. Identify open ports
        ↓
3. Identify services
        ↓
4. Detect service versions
        ↓
5. Identify OS information
        ↓
6. Analyze the results
        ↓
7. Perform further authorized security testing
```

Example:

```bash
nmap -sn 192.168.1.0/24
```

Then scan an identified host:

```bash
nmap -sV 192.168.1.10
```

Then perform additional enumeration when appropriate:

```bash
nmap -sC -sV 192.168.1.10
```

---

# 24. Scanning vs Nmap

### Scanning

Scanning is the **general process** of collecting information from a network or system.

### Nmap

Nmap is a **tool used to perform network scanning and enumeration**.

Simple mental model:

```text
Scanning = Process
Nmap     = Tool
```

---

# 25. Why Nmap is Important in Cybersecurity

Nmap helps security professionals understand:

* Which devices are active
* Which ports are exposed
* Which services are running
* Which service versions are being used
* What operating systems may be present
* What network attack surface exists

This information can be used for:

* Security auditing
* Vulnerability assessment
* Network troubleshooting
* Asset discovery
* Penetration testing

---

# 26. Authorization and Safety

Nmap should only be used against systems that you:

* Own
* Have explicit permission to test
* Are authorized to assess
* Have set up as a cybersecurity lab

For learning, you can safely practice with:

* Your own computer
* Your own router/network
* Virtual machines
* Local cybersecurity labs
* Intentionally vulnerable systems designed for training

Avoid scanning systems on the Internet without permission.

---

# 27. Important Concepts to Remember

```text
Host Discovery
      ↓
Port Scanning
      ↓
Service Detection
      ↓
Version Detection
      ↓
OS Detection
      ↓
Enumeration
      ↓
Security Analysis
```

### Simple Mental Model

Think of a network like a building:

```text
IP Address  → Building Address
Port        → Door
Service     → Person/Service behind the door
Version     → Specific version of that service
Nmap        → Tool used to inspect the building
Scanning    → The inspection process
```

---

# Quick Summary

**Scanning** = Collecting information about a target.

**Nmap** = A network scanning and security auditing tool.

The most important commands to remember:

```bash
nmap <IP>
nmap -sn <network>
nmap -p- <IP>
nmap -sV <IP>
nmap -O <IP>
nmap -sS <IP>
nmap -sU <IP>
nmap -sC -sV <IP>
nmap -A <IP>
```

> **Always scan only systems and networks where you have authorization.**
