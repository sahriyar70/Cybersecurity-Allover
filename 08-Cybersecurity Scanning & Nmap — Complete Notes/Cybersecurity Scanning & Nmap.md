# Cybersecurity Scanning & Nmap — Complete Notes

## 1. What is Scanning?

**Scanning** হলো কোনো network, host বা system সম্পর্কে technical information সংগ্রহ করার প্রক্রিয়া।

Scanning-এর মাধ্যমে জানা যেতে পারে:

* কোন host online আছে
* কোন port open আছে
* কোন service চলছে
* কোন operating system ব্যবহার হচ্ছে
* কোন network range active
* কোন service কোন version ব্যবহার করছে

### Simple Flow

```text
Target
   ↓
Discovery
   ↓
Port Scanning
   ↓
Service Detection
   ↓
OS Detection
   ↓
Security Assessment
```

> **Important:** শুধুমাত্র নিজের system, নিজের lab environment অথবা অনুমোদিত target-এ scanning করবে।

---

# 2. What is Nmap?

**Nmap (Network Mapper)** হলো একটি network scanning এবং security auditing tool।

Nmap ব্যবহার করে:

* Host discovery
* Port scanning
* Service detection
* Version detection
* OS detection
* Network mapping
* Basic security assessment

করা যায়।

---

# 3. Basic Nmap Syntax

```bash
nmap [options] <target>
```

Example:

```bash
nmap 192.168.1.1
```

এখানে:

```text
nmap
 ↓
Scanning tool

192.168.1.1
 ↓
Target IP
```

---

# 4. Scan a Single Host

```bash
nmap 192.168.1.10
```

### কাজ

একটি নির্দিষ্ট IP address-এর common ports scan করে।

---

# 5. Scan Multiple Hosts

```bash
nmap 192.168.1.10 192.168.1.20
```

### কাজ

একসাথে একাধিক host scan করে।

---

# 6. Scan an IP Range

```bash
nmap 192.168.1.1-20
```

### কাজ

`192.168.1.1` থেকে `192.168.1.20` পর্যন্ত host scan করে।

---

# 7. Scan an Entire Subnet

```bash
nmap 192.168.1.0/24
```

### কাজ

একটি `/24` network-এর hostগুলো scan করে।

Example:

```text
192.168.1.0/24
```

সাধারণভাবে এই range-এ:

```text
192.168.1.1
192.168.1.2
192.168.1.3
...
192.168.1.254
```

host address থাকে।

---

# 8. Host Discovery — Ping Scan

```bash
nmap -sn 192.168.1.0/24
```

### কাজ

Network-এর কোন hostগুলো discoverable/active তা খুঁজে বের করতে ব্যবহার করা হয়।

`-sn` মূলত host discovery করে এবং port scan না করে host availability যাচাই করে।

### Example

```text
nmap -sn 192.168.1.0/24
```

এর মাধ্যমে জানা যেতে পারে কোন কোন host network-এ পাওয়া যাচ্ছে।

---

# 9. Basic Port Scan

```bash
nmap 192.168.1.10
```

Nmap-এর basic scan common TCP ports সম্পর্কে information দিতে পারে।

Output সাধারণত এমন হতে পারে:

```text
PORT     STATE    SERVICE
22/tcp   open     ssh
80/tcp   open     http
443/tcp  open     https
```

---

# 10. Understanding Port States

Nmap-এর output-এ গুরুত্বপূর্ণ state:

### Open

```text
open
```

Port-এ কোনো application/service connection গ্রহণ করছে।

### Closed

```text
closed
```

Port reachable, কিন্তু সেখানে কোনো service listening করছে না।

### Filtered

```text
filtered
```

Firewall বা অন্য network filtering-এর কারণে Nmap port-এর state নিশ্চিতভাবে নির্ধারণ করতে পারছে না।

---

# 11. Scan Specific Ports

```bash
nmap -p 22 192.168.1.10
```

### কাজ

শুধু port `22` scan করে।

Multiple ports:

```bash
nmap -p 22,80,443 192.168.1.10
```

---

# 12. Scan a Port Range

```bash
nmap -p 1-1000 192.168.1.10
```

### কাজ

Port `1` থেকে `1000` পর্যন্ত scan করে।

---

# 13. Scan All TCP Ports

```bash
nmap -p- 192.168.1.10
```

### কাজ

Target-এর সমস্ত TCP port range scan করার জন্য ব্যবহৃত হয়।

`-p-` অর্থ পুরো TCP port range।

---

# 14. Service and Version Detection

```bash
nmap -sV 192.168.1.10
```

### কাজ

Open port-এ কোন service চলছে এবং সম্ভব হলে তার version শনাক্ত করার চেষ্টা করে।

Example:

```text
PORT    STATE   SERVICE   VERSION
22/tcp  open    ssh       OpenSSH ...
80/tcp  open    http      Apache ...
```

---

# 15. OS Detection

```bash
nmap -O 192.168.1.10
```

### কাজ

Target-এর operating system সম্পর্কে অনুমান করার চেষ্টা করে।

যেমন:

```text
Linux
Windows
```

ইত্যাদি।

OS detection সবসময় 100% accurate নাও হতে পারে।

---

# 16. Aggressive Scan

```bash
nmap -A 192.168.1.10
```

### কাজ

একাধিক detection technique একসাথে ব্যবহার করে।

সাধারণত এতে:

* OS detection
* Version detection
* Script scanning
* Traceroute

ইত্যাদি থাকতে পারে।

### Note

`-A` বেশি information সংগ্রহ করতে পারে, তাই lab বা authorized assessment-এ ব্যবহার করা উচিত।

---

# 17. TCP SYN Scan

```bash
nmap -sS 192.168.1.10
```

### কাজ

TCP SYN-based scanning ব্যবহার করে open ports শনাক্ত করার চেষ্টা করে।

এটি Nmap-এর বহুল ব্যবহৃত TCP scanning technique।

---

# 18. UDP Scan

```bash
nmap -sU 192.168.1.10
```

### কাজ

UDP ports scan করে।

উদাহরণ:

```text
53   → DNS
67   → DHCP Server
68   → DHCP Client
161  → SNMP
```

UDP scan TCP scan-এর তুলনায় ধীর হতে পারে।

---

# 19. Default Nmap Scripts

```bash
nmap -sC 192.168.1.10
```

### কাজ

Nmap-এর default NSE scripts ব্যবহার করে অতিরিক্ত information সংগ্রহ করার চেষ্টা করে।

---

# 20. Service + Default Scripts

```bash
nmap -sC -sV 192.168.1.10
```

এটি combine করে:

```text
-sC
 ↓
Default NSE scripts

-sV
 ↓
Service/version detection
```

---

# 21. Scan with OS + Service Detection

```bash
nmap -O -sV 192.168.1.10
```

### কাজ

একসাথে:

* OS detection
* Service detection
* Version detection

করার চেষ্টা করে।

---

# 22. Nmap Output to File

Normal output save:

```bash
nmap 192.168.1.10 -oN scan.txt
```

### কাজ

Nmap-এর normal output `scan.txt` file-এ save করে।

---

# 23. Useful Output Formats

### Normal

```bash
-oN scan.txt
```

### XML

```bash
-oX scan.xml
```

### Grepable

```bash
-oG scan.txt
```

### All major formats

```bash
-oA scan
```

---

# 24. Timing

Nmap-এর timing template:

```bash
-T0
-T1
-T2
-T3
-T4
-T5
```

সাধারণভাবে:

```text
T0 → Very slow
T1 → Slow
T2 → Polite
T3 → Normal
T4 → Fast
T5 → Very fast
```

Lab environment-এ প্রয়োজন অনুযায়ী timing ব্যবহার করা যায়।

---

# 25. Verbose Mode

```bash
nmap -v 192.168.1.10
```

### কাজ

Scan-এর সময় আরও বিস্তারিত progress/information দেখায়।

আরও verbose:

```bash
nmap -vv 192.168.1.10
```

---

# 26. Nmap Help

```bash
nmap -h
```

### কাজ

Nmap-এর command এবং option সম্পর্কে help information দেখায়।

---

# 27. Nmap Version

```bash
nmap --version
```

### কাজ

Installed Nmap-এর version দেখায়।

---

# 28. Common Nmap Commands Cheat Sheet

| Command                  | কাজ                       |
| ------------------------ | ------------------------- |
| `nmap <IP>`              | Basic scan                |
| `nmap -sn <network>`     | Host discovery            |
| `nmap -p 80 <IP>`        | Specific port scan        |
| `nmap -p 1-1000 <IP>`    | Port range scan           |
| `nmap -p- <IP>`          | All TCP ports             |
| `nmap -sS <IP>`          | TCP SYN scan              |
| `nmap -sU <IP>`          | UDP scan                  |
| `nmap -sV <IP>`          | Service/version detection |
| `nmap -O <IP>`           | OS detection              |
| `nmap -sC <IP>`          | Default NSE scripts       |
| `nmap -A <IP>`           | Aggressive detection      |
| `nmap -v <IP>`           | Verbose output            |
| `nmap -oN file.txt <IP>` | Save normal output        |
| `nmap -h`                | Help                      |
| `nmap --version`         | Show version              |

---

# 29. Practical Lab Example

নিজের lab network:

```text
Network:
192.168.1.0/24
```

## Step 1 — Find Active Hosts

```bash
nmap -sn 192.168.1.0/24
```

---

## Step 2 — Scan a Host

```bash
nmap 192.168.1.10
```

---

## Step 3 — Check Services

```bash
nmap -sV 192.168.1.10
```

---

## Step 4 — Check Specific Ports

```bash
nmap -p 22,80,443 192.168.1.10
```

---

## Step 5 — Save Result

```bash
nmap -sV 192.168.1.10 -oN scan.txt
```

---

# 30. Scanning Workflow

Cybersecurity assessment-এর basic workflow:

```text
Identify Target
      ↓
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
Analyze Results
      ↓
Security Assessment
```

---

# 31. Scanning vs Nmap

### Scanning

একটি **process/technique**।

### Nmap

Scanning করার জন্য ব্যবহৃত একটি **tool**।

সহজভাবে:

```text
Scanning = কাজ
Nmap     = কাজটি করার একটি Tool
```

---

# 32. Important Security Rule

Nmap বা অন্য scanning tools ব্যবহার করার আগে target-এর authorization থাকতে হবে।

### Safe Targets

```text
Your own PC
Your own router
Your own VM
Your own lab network
Authorized penetration-testing target
```

### Avoid

```text
Unknown public IP
Random websites
Other people's networks
Systems without permission
```

---

# Final Mental Model

```text
Nmap
 │
 ├── Host Discovery
 │      └── -sn
 │
 ├── Port Scanning
 │      ├── -p
 │      ├── -p-
 │      └── -sS
 │
 ├── Service Detection
 │      └── -sV
 │
 ├── OS Detection
 │      └── -O
 │
 ├── NSE Scripts
 │      └── -sC
 │
 ├── Advanced Detection
 │      └── -A
 │
 └── Save Results
        └── -oN / -oX / -oA
```

## Core Commands to Remember

```bash
nmap <IP>
nmap -sn <network>
nmap -p 80 <IP>
nmap -p- <IP>
nmap -sS <IP>
nmap -sV <IP>
nmap -O <IP>
nmap -sC <IP>
nmap -A <IP>
nmap -oN scan.txt <IP>
```

**Learning order:**
`Host Discovery → Port Scanning → Service Detection → Version Detection → OS Detection → NSE → Result Analysis`
