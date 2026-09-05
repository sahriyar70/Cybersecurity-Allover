# Common Network Protocols, Ports & Cybersecurity Reference Guide

**Topic:** Network Protocols, Default Port Numbers, Functions & Security Considerations

---

## Overview

Understanding **network protocols, their commonly used ports, and their functions** is fundamental for:

* Networking
* Cybersecurity
* Security auditing
* Firewall configuration
* Network troubleshooting
* Penetration testing
* Port scanning
* Reconnaissance
* Incident response

Knowing which service commonly uses which port helps security professionals identify the **attack surface** of a network and understand what services may be exposed.

---

# Complete Protocols & Ports Master Table

| Protocol   | Full Form                             | Common Port(s) | Transport | Main Purpose                                       |
| ---------- | ------------------------------------- | -------------: | --------- | -------------------------------------------------- |
| **FTP**    | File Transfer Protocol                |        20 / 21 | TCP       | File transfer                                      |
| **SSH**    | Secure Shell                          |             22 | TCP       | Secure remote access and administration            |
| **Telnet** | Teletype Network                      |             23 | TCP       | Remote terminal access without built-in encryption |
| **SMTP**   | Simple Mail Transfer Protocol         |             25 | TCP       | Email transmission between mail servers            |
| **DNS**    | Domain Name System                    |             53 | UDP / TCP | Domain-name resolution and DNS services            |
| **DHCP**   | Dynamic Host Configuration Protocol   |        67 / 68 | UDP       | Automatic IP configuration                         |
| **HTTP**   | Hypertext Transfer Protocol           |             80 | TCP       | Web communication without TLS                      |
| **POP3**   | Post Office Protocol Version 3        |            110 | TCP       | Email retrieval                                    |
| **NTP**    | Network Time Protocol                 |            123 | UDP       | Time synchronization                               |
| **IMAP**   | Internet Message Access Protocol      |            143 | TCP       | Server-based email access and synchronization      |
| **SNMP**   | Simple Network Management Protocol    |      161 / 162 | UDP       | Network monitoring and management                  |
| **LDAP**   | Lightweight Directory Access Protocol |            389 | TCP / UDP | Directory services and queries                     |
| **HTTPS**  | HTTP Secure                           |            443 | TCP / UDP | HTTP protected by TLS                              |
| **SMB**    | Server Message Block                  |            445 | TCP       | File, printer, and resource sharing                |
| **LDAPS**  | LDAP over TLS                         |            636 | TCP       | LDAP communication protected with TLS              |
| **IMAPS**  | IMAP over TLS                         |            993 | TCP       | Secure email access                                |
| **POP3S**  | POP3 over TLS                         |            995 | TCP       | Secure email retrieval                             |
| **RDP**    | Remote Desktop Protocol               |           3389 | TCP / UDP | Windows remote desktop access                      |

> **Important:** Port numbers are conventions, not absolute guarantees. A service can sometimes be configured to run on a different port.

---

# 1. FTP — File Transfer Protocol

**Port:** 20 / 21
**Transport:** TCP

FTP is used to transfer files between a client and a server.

### Common Ports

```text
TCP 21 → FTP Control Connection
TCP 20 → FTP Data Connection in traditional Active Mode
```

FTP does **not provide encryption by itself**.

Therefore, usernames, passwords, and transferred data can potentially be exposed to network sniffing.

### Security Concerns

* Plaintext credentials
* Credential sniffing
* Brute-force attacks
* Misconfigured anonymous access
* Data interception

### Secure Alternatives

* **SFTP** — File transfer over SSH
* **FTPS** — FTP secured using TLS

> **Important:** SFTP and FTPS are different protocols. SFTP is not "FTP + SSL/TLS"; it operates over SSH.

---

# 2. SSH — Secure Shell

**Port:** 22
**Transport:** TCP

SSH provides secure remote access to systems.

It encrypts the communication channel and can be used for:

* Remote administration
* Secure shell access
* File transfer through SCP/SFTP
* Secure tunneling
* Port forwarding

### Security Concerns

SSH is secure when properly configured, but it can still be targeted by:

* Brute-force attacks
* Credential attacks
* Stolen private keys
* Vulnerable SSH implementations
* Misconfiguration

### Best Practices

```text
Use strong authentication
Use SSH keys where appropriate
Disable unnecessary password authentication
Disable direct root login where appropriate
Restrict source IPs
Use MFA where supported
Keep SSH software updated
```

---

# 3. Telnet

**Port:** 23
**Transport:** TCP

Telnet provides remote terminal access but does not provide encryption by default.

Example:

```text
Client
  |
  | Plaintext communication
  ↓
Telnet Server
```

An attacker capable of observing the traffic may be able to capture credentials and commands.

### Security Recommendation

Avoid Telnet for sensitive administration.

Use:

```text
Telnet 
   ↓
SSH 
```

---

# 4. SMTP — Simple Mail Transfer Protocol

**Port:** 25
**Transport:** TCP

SMTP is primarily used for **sending and relaying email**.

Commonly:

```text
Mail Client
    ↓
Mail Server
    ↓
SMTP
    ↓
Recipient Mail Server
```

Modern email systems may also use submission ports such as:

```text
587 → Message Submission
465 → SMTP over TLS (commonly used)
```

### Security Concerns

* Open relay configuration
* Email spoofing
* Credential attacks
* Phishing
* Misconfigured authentication
* TLS misconfiguration

---

# 5. DNS — Domain Name System

**Port:** 53
**Transport:** UDP / TCP

DNS translates domain names into IP addresses and provides other DNS-related information.

Example:

```text
example.com
     ↓
DNS
     ↓
93.184.216.34
```

### UDP vs TCP

DNS commonly uses:

```text
UDP 53 → Normal DNS queries
TCP 53 → Zone transfers and other cases requiring TCP
```

DNS can also use modern encrypted transports such as:

```text
DoH → DNS over HTTPS
DoT → DNS over TLS
```

### Security Concerns

* DNS spoofing
* DNS cache poisoning
* DNS tunneling
* DNS amplification
* Malicious domain resolution
* Zone transfer misconfiguration

---

# 6. DHCP — Dynamic Host Configuration Protocol

**Ports:** 67 / 68
**Transport:** UDP

DHCP automatically provides network configuration to clients.

It can provide:

* IP address
* Subnet mask
* Default gateway
* DNS server
* Lease information

### Basic DHCP Process

```text
Client
  ↓
DHCP Discover
  ↓
DHCP Offer
  ↓
DHCP Request
  ↓
DHCP ACK
```

### Security Concerns

* Rogue DHCP server
* DHCP spoofing
* Network configuration manipulation
* Denial of DHCP service

---

# 7. HTTP — Hypertext Transfer Protocol

**Port:** 80
**Transport:** Traditionally TCP

HTTP is used for communication between web clients and web servers.

Example:

```text
Browser
   ↓
HTTP Request
   ↓
Web Server
   ↓
HTTP Response
   ↓
Browser
```

HTTP itself does not encrypt application data.

Therefore, sensitive information sent over plain HTTP can potentially be observed or modified by an attacker positioned on the network.

### Security Concerns

* Traffic sniffing
* Credential exposure
* Man-in-the-Middle attacks
* Session theft
* Content manipulation

For sensitive web communication, HTTPS should be used.

---

# 8. HTTPS — HTTP Secure

**Port:** 443
**Transport:** TCP or UDP depending on the HTTP version

HTTPS means HTTP protected using **TLS (Transport Layer Security)**.

For example:

```text
Browser
   ↓
HTTPS
   ↓
TLS
   ↓
Transport
   ↓
Network
```

HTTPS provides protections such as:

* Confidentiality
* Integrity
* Server authentication

### Modern Important Detail

HTTP/1.1 and HTTP/2 commonly use:

```text
HTTPS
  ↓
TLS
  ↓
TCP
```

HTTP/3 uses:

```text
HTTP/3
  ↓
QUIC
  ↓
UDP
```

So **port 443 can be used with both TCP and UDP**.

---

# 9. POP3 — Post Office Protocol Version 3

**Port:** 110
**Transport:** TCP

POP3 is used to retrieve email from a mail server.

Traditionally, POP3 is designed around downloading messages to a client, but exact server/client behavior—such as whether messages are deleted from the server—depends on configuration.

### Secure Version

```text
POP3  → TCP 110
POP3S → TCP 995
```

POP3S uses TLS to protect the connection.

---

# 10. IMAP — Internet Message Access Protocol

**Port:** 143
**Transport:** TCP

IMAP allows users to access and synchronize email while keeping messages managed on the mail server.

This makes it suitable for using the same mailbox across:

```text
Phone
Laptop
Desktop
Tablet
```

### Secure Version

```text
IMAP   → TCP 143
IMAPS  → TCP 993
```

IMAPS uses TLS to protect the connection.

---

# 11. NTP — Network Time Protocol

**Port:** 123
**Transport:** UDP

NTP synchronizes clocks across networked systems.

Accurate time is extremely important for cybersecurity because timestamps are used in:

* Logs
* Incident investigation
* Authentication systems
* Certificates
* Event correlation
* SIEM systems

### Security Concerns

* NTP amplification attacks
* Time manipulation
* Malicious or untrusted time sources
* Misconfigured NTP servers

---

# 12. SNMP — Simple Network Management Protocol

**Ports:** 161 / 162
**Transport:** UDP

SNMP is commonly used to monitor and manage network devices.

Examples:

```text
Routers
Switches
Servers
Firewalls
Printers
Network appliances
```

### Common Ports

```text
UDP 161 → SNMP queries/management
UDP 162 → SNMP traps/notifications
```

### SNMP Versions

```text
SNMPv1
SNMPv2c
SNMPv3
```

SNMPv1 and SNMPv2c use community strings and do not provide the same security protections as SNMPv3.

**SNMPv3** supports security features such as authentication and privacy (encryption), depending on the configured security level.

---

# 13. LDAP — Lightweight Directory Access Protocol

**Port:** 389
**Transport:** TCP / UDP

LDAP is used to access and query directory services.

It can be used for:

* User directories
* Authentication-related workflows
* Organizational information
* Group information
* Directory searches

Microsoft Active Directory commonly uses LDAP-related services.

### Security Concerns

Plain LDAP can expose sensitive information if not protected appropriately.

Secure alternatives include:

```text
LDAP + StartTLS
LDAP over TLS (commonly called LDAPS)
```

---

# 14. LDAPS

**Port:** 636
**Transport:** TCP

LDAPS refers to LDAP communication protected using TLS.

```text
LDAP
  ↓
TLS
  ↓
Encrypted Directory Communication
```

It can help protect:

* Credentials
* Directory queries
* Directory responses

---

# 15. SMB — Server Message Block

**Port:** 445
**Transport:** TCP

SMB is widely used in Windows environments for:

* File sharing
* Folder sharing
* Printer sharing
* Network resources
* Windows administrative operations

Example:

```text
Windows Client
      ↓
     SMB
      ↓
Windows File Server
```

### Major Security Concerns

SMB has historically been targeted by attackers because vulnerable or exposed SMB services can provide significant access to Windows environments.

A famous example is **EternalBlue**, which exploited a vulnerability in older SMBv1 implementations and was associated with the spread of the WannaCry ransomware outbreak.

### Best Practices

```text
Disable SMBv1
Keep systems patched
Restrict TCP 445
Use network segmentation
Avoid exposing SMB directly to the Internet
Monitor SMB activity
```

---

# 16. RDP — Remote Desktop Protocol

**Port:** 3389
**Transport:** TCP / UDP

RDP provides graphical remote access to Windows systems.

Example:

```text
Administrator
      ↓
    RDP
      ↓
Windows Server
      ↓
Desktop Environment
```

### Security Concerns

RDP is frequently targeted because it provides remote access to Windows systems.

Potential threats include:

* Brute-force attacks
* Credential stuffing
* Stolen credentials
* Vulnerable RDP services
* Remote exploitation

**BlueKeep**, for example, was a critical vulnerability affecting certain older Windows Remote Desktop Services implementations.

### Best Practices

Avoid exposing RDP directly to the public Internet whenever possible.

Prefer:

```text
Internet
   ↓
VPN / Zero Trust Access
   ↓
Firewall
   ↓
RDP
   ↓
Windows System
```

Also use:

* Network Level Authentication (NLA)
* Strong authentication
* MFA where supported
* IP restrictions
* Account lockout/rate limiting
* Regular patching

---

# Remote Access Protocols: SSH vs Telnet vs RDP

| Feature                 | SSH                             | Telnet                     | RDP                                                         |
| ----------------------- | ------------------------------- | -------------------------- | ----------------------------------------------------------- |
| **Default Port**        | 22                              | 23                         | 3389                                                        |
| **Primary Use**         | Secure remote administration    | Remote terminal            | Windows GUI remote access                                   |
| **Encryption**          | Yes                             | No built-in encryption     | Security features available; typically used with encryption |
| **Typical Environment** | Linux/Unix, network devices     | Legacy systems             | Windows                                                     |
| **Security Level**      | Strong when configured properly | Insecure for sensitive use | Strong when properly secured                                |
| **Common Attacks**      | Credential attacks, key theft   | Credential sniffing        | Brute force, credential attacks, exploitation               |

---

# Web Protocols: HTTP vs HTTPS

| Feature                            | HTTP                        | HTTPS                                    |
| ---------------------------------- | --------------------------- | ---------------------------------------- |
| **Port**                           | 80                          | 443                                      |
| **Encryption**                     | No TLS                      | TLS                                      |
| **Confidentiality**                | Not provided by HTTP itself | Provided by TLS                          |
| **Integrity Protection**           | Not provided by HTTP itself | Provided by TLS                          |
| **Server Authentication**          | No TLS authentication       | TLS certificates authenticate the server |
| **Recommended for Sensitive Data** |  No                        |  Yes                                    |

---

# Email Protocols

| Protocol        | Port | Purpose                                  | Security                   |
| --------------- | ---: | ---------------------------------------- | -------------------------- |
| SMTP            |   25 | Mail server-to-server transmission/relay | TLS can be used            |
| SMTP Submission |  587 | Client mail submission                   | Usually protected with TLS |
| POP3            |  110 | Email retrieval                          | No TLS by default          |
| POP3S           |  995 | Secure POP3                              | TLS                        |
| IMAP            |  143 | Email access/synchronization             | No TLS by default          |
| IMAPS           |  993 | Secure IMAP                              | TLS                        |

---

# Common Plaintext / Unencrypted Protocols

The following protocols **do not provide encryption by default**:

```text
Telnet
FTP
HTTP
POP3
IMAP
LDAP
```

This does **not** mean every deployment is necessarily sending everything in plaintext—some protocols can be protected using additional mechanisms such as TLS.

For example:

```text
HTTP
  ↓
TLS
  ↓
HTTPS
```

```text
IMAP
  ↓
TLS
  ↓
IMAPS
```

```text
POP3
  ↓
TLS
  ↓
POP3S
```

```text
LDAP
  ↓
TLS / StartTLS
  ↓
Protected LDAP
```

---

# Important Security Distinction

Do not confuse these protocols:

### SFTP

```text
SFTP
 ↓
SSH
 ↓
Encrypted connection
```

### FTPS

```text
FTPS
 ↓
FTP
 ↓
TLS
```

They are different technologies.

---

# Attack Surface Perspective

From a cybersecurity perspective, an open port means that **a service is reachable**. It does not automatically mean the service is vulnerable.

For example:

```text
TCP 22 Open
     ↓
SSH Service
     ↓
Check:
├── Version
├── Configuration
├── Authentication
├── Exposure
└── Known vulnerabilities
```

Therefore:

> **Open port ≠ Vulnerability**

The security risk depends on the service, configuration, software version, authentication, exposure, and other environmental factors.

---

# Security Assessment Workflow

When performing an **authorized** security assessment:

```text
1. Discover Hosts
       ↓
2. Identify Open Ports
       ↓
3. Identify Services
       ↓
4. Determine Versions
       ↓
5. Review Configuration
       ↓
6. Identify Vulnerabilities
       ↓
7. Validate Safely
       ↓
8. Report Findings
       ↓
9. Remediate
       ↓
10. Re-test
```

Tools commonly used in authorized environments include:

```text
Nmap
Wireshark
Burp Suite
Netcat
curl
tcpdump
```

---

# Firewall Best Practices

## 1. Minimize Exposed Ports

Only expose services that are actually required.

```text
Required Service → Allow
Unused Service   → Block
```

---

## 2. Restrict Management Services

Management services such as:

```text
SSH  → 22
RDP  → 3389
SMB  → 445
```

should generally not be exposed directly to the public Internet unless there is a strong, well-designed reason and appropriate protections.

Prefer:

```text
Internet
   ↓
VPN / Zero Trust Access
   ↓
Firewall
   ↓
Internal Service
```

---

## 3. Use Encryption

Prefer secure alternatives where appropriate:

```text
Telnet  → SSH
FTP     → SFTP / FTPS
HTTP    → HTTPS
IMAP    → IMAPS / TLS
POP3    → POP3S / TLS
LDAP    → TLS / LDAPS
```

---

## 4. Keep Services Updated

Regularly patch:

* Operating systems
* Web servers
* SSH servers
* RDP services
* SMB
* DNS servers
* Email servers
* Network appliances

---

## 5. Monitor Network Activity

Monitor important services for:

```text
Unusual connections
Repeated authentication failures
Unexpected geographic sources
Port scanning
Brute-force attempts
Large traffic spikes
Suspicious protocols
```

---

# Quick Reference

```text
FTP      → 20/21  → File Transfer
SSH      → 22     → Secure Remote Access
Telnet   → 23     → Insecure Remote Access
SMTP     → 25     → Email Transmission
DNS      → 53     → Name Resolution
DHCP     → 67/68  → IP Configuration
HTTP     → 80     → Web Traffic
POP3     → 110    → Email Retrieval
NTP      → 123    → Time Synchronization
IMAP     → 143    → Email Access
SNMP     → 161    → Network Management
SNMP     → 162    → Traps/Notifications
LDAP     → 389    → Directory Services
HTTPS    → 443    → Secure Web Traffic
SMB      → 445    → Windows File Sharing
LDAPS    → 636    → LDAP over TLS
IMAPS    → 993    → Secure IMAP
POP3S    → 995    → Secure POP3
RDP      → 3389   → Windows Remote Desktop
```

---

# Cybersecurity Cheat Sheet

```text
SSH
├── Port: 22
├── Secure remote access
└── Protect against credential attacks

Telnet
├── Port: 23
├── No built-in encryption
└── Replace with SSH

FTP
├── Port: 20/21
├── No encryption by default
└── Prefer SFTP or FTPS

HTTP
├── Port: 80
├── No TLS
└── Prefer HTTPS

HTTPS
├── Port: 443
├── TLS protected
└── Common for secure web communication

DNS
├── Port: 53
├── UDP/TCP
└── Watch for spoofing, tunneling and amplification

SMB
├── Port: 445
├── Windows file sharing
└── Restrict exposure and disable SMBv1

RDP
├── Port: 3389
├── Windows remote desktop
└── Restrict exposure and use strong authentication

SNMP
├── Port: 161/162
├── Network monitoring
└── Prefer SNMPv3

LDAP
├── Port: 389
├── Directory services
└── Protect with TLS where appropriate

LDAPS
├── Port: 636
└── LDAP over TLS
```

---

# Final Key Takeaways

1. **Knowing protocols and ports is fundamental to network security.**

2. A port number identifies a transport-layer endpoint commonly associated with a service, but it does **not guarantee** which service is actually running there.

3. **Open ports are not automatically vulnerabilities.**

4. Plaintext protocols such as Telnet and traditional FTP should generally be avoided for sensitive communication.

5. **SFTP uses SSH**, while **FTPS uses TLS**. They are not the same protocol.

6. **HTTPS uses TLS** and commonly runs over TCP for HTTP/1.1 and HTTP/2, while HTTP/3 uses QUIC over UDP.

7. **SMB (445)** should generally not be exposed directly to the public Internet.

8. **RDP (3389)** should be strongly protected and preferably accessed through controlled remote-access mechanisms such as VPN or Zero Trust solutions.

9. **SNMPv3** provides stronger security capabilities than SNMPv1/v2c.

10. Firewall configuration should follow the principle of **least exposure**:

```text
Allow what is required
Block what is unnecessary
Restrict management access
Encrypt sensitive communication
Monitor exposed services
Patch regularly
```

> **Core Cybersecurity Principle:**
> **Know the service → Understand the protocol → Identify the exposure → Assess the risk → Apply appropriate controls.**
