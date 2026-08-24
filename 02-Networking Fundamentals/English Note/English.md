# Computer Networking Fundamentals — Cybersecurity Perspective

**Topics:** Computer Networks, Devices, IP/MAC, Architecture & Protocols

---

## Overview

Networking is one of the fundamental foundations of cybersecurity.

Understanding how networks work, how data travels from one system to another, and which protocols are used is essential for detecting, analyzing, and defending against network-based attacks.

This guide covers cybersecurity-focused networking fundamentals, including networking devices, IP and MAC addresses, network types, NAT/PAT, the OSI and TCP/IP models, important protocols and ports, and common network security concepts.

---

# What is Networking?

A **computer network** is a collection of interconnected digital devices that communicate with each other to exchange data and share resources.

Devices can be connected through:

* Wired connections
* Wireless connections

Examples of networked devices include:

* Computers
* Servers
* Routers
* Switches
* Smartphones
* IoT devices
* Network appliances

---

# Hardware & Networking Devices

## 1. NIC — Network Interface Card

A **Network Interface Card (NIC)** is a hardware component that allows a device to connect to a network.

A NIC can provide:

* Wired Ethernet connectivity
* Wireless connectivity
* A MAC address

### Example

```text
Computer
   │
   ▼
  NIC
   │
   ▼
Network
```

---

## 2. Switch

A **Switch** is primarily a **Layer 2 (Data Link Layer)** networking device used to connect devices within a Local Area Network (LAN).

A switch maintains a **MAC Address Table** and uses MAC addresses to forward Ethernet frames to the appropriate destination port.

### Example

```text
PC 1 ───┐
PC 2 ───┤
PC 3 ───┤── Switch
PC 4 ───┘
```

### Security Concepts

* MAC Address Table
* Port Security
* VLAN
* MAC flooding
* Network segmentation

---

## 3. Router

A **Router** is primarily a **Layer 3 (Network Layer)** device that connects different networks.

Routers use:

* IP addresses
* Routing tables
* Routing protocols

to determine where packets should be forwarded.

### Example

```text
LAN
 │
 ▼
Router
 │
 ▼
Internet / WAN
```

### Security Concepts

* Routing
* ACLs
* Firewall integration
* IP filtering
* Network segmentation

---

## 4. Firewall

A **Firewall** is a security control that monitors and filters network traffic based on predefined security rules.

A firewall can:

* Allow traffic
* Block traffic
* Restrict ports
* Restrict IP addresses
* Filter protocols
* Control inbound and outbound connections

### Example

```text
Internet
    │
    ▼
[ Firewall ]
    │
    ▼
Internal Network
```

---

## 5. Access Point (AP)

An **Access Point (AP)** allows wireless devices to connect to a wired network using Wi-Fi.

### Example

```text
Wired Network
      │
      ▼
 Access Point
   /   |   \
  /    |    \
Laptop Phone Tablet
```

Access points commonly use the **IEEE 802.11** family of standards for Wi-Fi communication.

---

# MAC Address vs IP Address

| Feature                | MAC Address                                           | IP Address                                           |
| ---------------------- | ----------------------------------------------------- | ---------------------------------------------------- |
| **Full Form**          | Media Access Control                                  | Internet Protocol                                    |
| **Purpose**            | Identifies a network interface at the Data Link layer | Provides logical addressing and routing              |
| **OSI Layer**          | Layer 2 — Data Link                                   | Layer 3 — Network                                    |
| **IPv4 Size**          | 48-bit                                                | 32-bit                                               |
| **IPv6 Size**          | 48-bit MAC                                            | 128-bit                                              |
| **Example**            | `00:1A:2B:3C:4D:5E`                                   | `192.168.1.10`                                       |
| **Security Relevance** | MAC spoofing, port security                           | Firewall rules, traffic analysis, IP-based filtering |

> A MAC address is not necessarily permanently tied to a device. Modern operating systems can use randomized or changed MAC addresses, especially on Wi-Fi networks.

---

# Network Types

## LAN — Local Area Network

A **LAN** is a network covering a relatively small geographical area.

Examples:

* Home network
* Office network
* School network
* Small business network

Characteristics:

* High speed
* Low latency
* Limited geographical area

---

## WLAN — Wireless Local Area Network

A **WLAN** is a LAN that uses wireless communication, typically Wi-Fi.

WLANs commonly use the **IEEE 802.11** family of standards.

Example:

```text
Internet
   │
Router / AP
   │
 ┌─┼──────────────┐
 │ │              │
PC Phone         Laptop
```

---

## WAN — Wide Area Network

A **WAN** connects networks across large geographical areas.

Examples:

* Multiple offices across different cities
* International corporate networks
* ISP networks

The **Internet** is the world's largest interconnected network and can be considered a global network of networks.

---

# NAT vs PAT

## NAT — Network Address Translation

**Network Address Translation (NAT)** translates IP addresses between different addressing domains, commonly between private and public IPv4 addresses.

NAT can be implemented in different ways, including:

* Static NAT
* Dynamic NAT

### Static NAT

A specific private IP address is mapped to a specific public IP address.

```text
Private IP
192.168.1.10
      │
      ▼
Public IP
203.0.113.10
```

---

## PAT — Port Address Translation

**Port Address Translation (PAT)**, commonly called **NAT Overload**, allows many private hosts to share a single public IPv4 address by using different source port numbers.

```text
192.168.1.10:50001 ─┐
192.168.1.11:50002 ─┼──► Public IP:Port
192.168.1.12:50003 ─┘
```

### Why is PAT Important?

PAT helps:

* Conserve public IPv4 addresses
* Allow multiple internal devices to access the Internet
* Keep internal addressing private from direct Internet visibility

> NAT/PAT can provide some exposure reduction, but NAT itself should not be considered a complete security control or firewall.

---

# OSI Model

The **OSI (Open Systems Interconnection) Model** is a conceptual model that divides network communication into seven layers.

Understanding these layers is extremely important for cybersecurity because different attacks and security controls operate at different layers.

```text
┌──────────────────────────────────────────────────────────┐
│ Layer 7 — Application   │ HTTP, DNS | SQLi, XSS         │
├──────────────────────────────────────────────────────────┤
│ Layer 6 — Presentation  │ TLS, Encoding, Compression    │
├──────────────────────────────────────────────────────────┤
│ Layer 5 — Session       │ Session Management, Tokens     │
├──────────────────────────────────────────────────────────┤
│ Layer 4 — Transport     │ TCP, UDP | Port Scanning      │
├──────────────────────────────────────────────────────────┤
│ Layer 3 — Network       │ IP, ICMP | IP Spoofing         │
├──────────────────────────────────────────────────────────┤
│ Layer 2 — Data Link     │ MAC, Ethernet | ARP Spoofing   │
├──────────────────────────────────────────────────────────┤
│ Layer 1 — Physical      │ Cables, Signals | Wiretapping  │
└──────────────────────────────────────────────────────────┘
```

## Layer 7 — Application

Examples:

* HTTP
* HTTPS
* DNS
* FTP
* SMTP
* SSH

Security concepts:

* SQL Injection
* XSS
* Authentication attacks
* Phishing
* API security

---

## Layer 6 — Presentation

Responsible for data representation, encoding, encryption, and compression.

Examples:

* TLS-related functions
* Data encoding
* Encryption
* Compression
* Serialization

---

## Layer 5 — Session

Responsible for establishing, managing, and terminating communication sessions.

Security concepts:

* Session management
* Session tokens
* Session hijacking
* Authentication sessions

> In modern TCP/IP networking, Session and Presentation layer responsibilities are often handled within application protocols and libraries rather than existing as clearly separate layers.

---

## Layer 4 — Transport

Provides end-to-end communication between applications.

Main protocols:

* TCP
* UDP

Security concepts:

* Port scanning
* SYN floods
* Connection management
* Port-based filtering

---

## Layer 3 — Network

Responsible for logical addressing and routing.

Examples:

* IPv4
* IPv6
* ICMP
* IPsec

Security concepts:

* IP spoofing
* Routing attacks
* ICMP attacks
* Packet filtering

---

## Layer 2 — Data Link

Responsible for communication within a local network.

Examples:

* Ethernet
* Wi-Fi
* MAC addresses
* ARP
* VLAN

Security concepts:

* ARP spoofing
* MAC flooding
* VLAN attacks
* Switch security

---

## Layer 1 — Physical

Responsible for transmitting raw bits through physical media.

Examples:

* Ethernet cables
* Fiber-optic cables
* Radio signals
* Electrical signals
* Network connectors

Security concepts:

* Wiretapping
* Hardware tampering
* Physical theft
* Cable damage

---

# TCP/IP Model

The **TCP/IP model** is the practical networking model used by modern Internet networks.

A simplified mapping is:

```text
TCP/IP Model          OSI Model

Application     →     Application
                  →   Presentation
                  →   Session

Transport       →     Transport

Internet        →     Network

Network Access  →     Data Link
                  →   Physical
```

---

# Important Protocols & Port Numbers

Knowing common protocols and their default ports is important for cybersecurity, network monitoring, troubleshooting, and security assessments.

|      Port | Protocol | Description                  | Security Notes                                                     |
| --------: | -------- | ---------------------------- | ------------------------------------------------------------------ |
|    **21** | FTP      | File Transfer Protocol       | Traditionally plaintext; use secure alternatives where appropriate |
|    **22** | SSH      | Secure remote administration | Encrypted; protect with strong authentication                      |
|    **23** | Telnet   | Remote login                 | Unencrypted; generally insecure                                    |
|    **53** | DNS      | Domain Name System           | Can be targeted by spoofing, poisoning, and other attacks          |
|    **80** | HTTP     | Web traffic                  | Typically unencrypted; use HTTPS for sensitive traffic             |
|   **443** | HTTPS    | HTTP over TLS                | Provides encrypted web communication                               |
| **67/68** | DHCP     | Automatic IP configuration   | Can be targeted by DHCP starvation and rogue DHCP attacks          |

> Port numbers identify services at the transport layer. A port being open does not automatically mean that the service is vulnerable.

---

# Key Security Networking Concepts

## 1. ARP — Address Resolution Protocol

**ARP** is used in IPv4 local networks to discover the MAC address associated with an IPv4 address.

Example:

```text
Who has 192.168.1.1?

192.168.1.1 → AA:BB:CC:DD:EE:FF
```

### ARP Spoofing

In an **ARP spoofing** attack, an attacker sends forged ARP messages to associate their MAC address with another device's IP address.

This can potentially enable:

* Man-in-the-Middle (MITM) attacks
* Traffic interception
* Traffic manipulation

### Security Measures

* Dynamic ARP Inspection (DAI)
* Network segmentation
* Static ARP entries where appropriate
* Secure switch configuration
* Network monitoring

---

# 2. DNS — Domain Name System

DNS translates human-readable domain names into IP addresses.

Example:

```text
example.com
     ↓
DNS
     ↓
93.184.216.34
```

### Security Risks

DNS can be targeted by:

* DNS spoofing
* DNS cache poisoning
* DNS hijacking
* DNS tunneling
* DNS amplification attacks

### Security Measures

* DNSSEC
* Secure DNS resolvers
* Monitoring
* Proper DNS configuration
* Network filtering

---

# 3. TCP Three-Way Handshake

TCP establishes a connection using a three-way handshake.

```text
Client                    Server

  │                         │
  │────── SYN ─────────────►│
  │                         │
  │◄──── SYN-ACK ───────────│
  │                         │
  │────── ACK ─────────────►│
  │                         │
  │     Connection Ready    │
```

### Steps

1. **SYN** — Client requests a connection.
2. **SYN-ACK** — Server acknowledges the request and responds.
3. **ACK** — Client acknowledges the server.

---

## SYN Flood

A **SYN Flood** is a denial-of-service technique in which an attacker sends a large number of TCP SYN requests without completing the expected handshake.

This can consume server resources and potentially make the service unavailable.

### Defensive Measures

* SYN cookies
* Rate limiting
* Firewall filtering
* Load balancing
* DDoS protection
* Traffic monitoring

---

# 4. Network Segmentation & VLAN

**Network segmentation** divides a network into smaller security zones.

The primary goal is to limit unnecessary communication and reduce the **blast radius** of a compromise.

### Example

```text
                    Router / Firewall
                           │
             ┌─────────────┼─────────────┐
             │             │             │
          VLAN 10       VLAN 20       VLAN 30
             │             │             │
           Users        Servers         IoT
```

If an attacker compromises a device in one segment, proper segmentation and access controls can make it harder to move laterally into other segments.

### Benefits

* Limits lateral movement
* Reduces attack surface
* Improves traffic control
* Separates sensitive systems
* Improves monitoring

---

# HTTP vs HTTPS

## HTTP

HTTP normally transfers web traffic without encryption.

```text
Client
  │
  │ HTTP
  ▼
Server
```

Traffic can potentially be observed or modified by an attacker who can successfully intercept the communication.

---

## HTTPS

HTTPS is **HTTP over TLS**.

```text
Client
  │
  │ HTTPS
  │ TLS Encryption
  ▼
Server
```

HTTPS provides:

* Confidentiality
* Integrity
* Server authentication through certificates

> HTTPS protects data in transit, but it does not automatically make the underlying application secure. Application vulnerabilities such as SQL injection or broken access control can still exist over HTTPS.

---

# Network Communication Flow

A simplified web communication flow looks like this:

```text
User
  │
  ▼
Browser
  │
  ▼
HTTP / HTTPS
  │
  ▼
TCP / UDP
  │
  ▼
IP
  │
  ▼
Ethernet / Wi-Fi
  │
  ▼
Physical Network
```

For a typical HTTPS connection:

```text
HTTPS
  ↓
TLS
  ↓
TCP
  ↓
IP
  ↓
Ethernet / Wi-Fi
  ↓
Physical Transmission
```

---

# Key Takeaways

1. **Networking is a fundamental foundation of cybersecurity.**
2. **MAC addresses** operate primarily at Layer 2, while **IP addresses** operate at Layer 3.
3. **Switches** primarily forward Ethernet frames using MAC addresses.
4. **Routers** forward packets between networks using IP addresses and routing information.
5. **Firewalls** filter network traffic according to security policies.
6. **NAT** translates IP addresses, while **PAT** allows multiple private hosts to share a public IPv4 address using different ports.
7. The **OSI Model** provides seven conceptual layers for understanding network communication.
8. **HTTP operates at the Application Layer**; HTTPS is HTTP protected by TLS.
9. **TCP** provides reliable connection-oriented communication, while **UDP** provides connectionless communication.
10. **ARP** maps IPv4 addresses to MAC addresses on local networks.
11. **DNS** translates domain names into IP addresses.
12. **Network segmentation and VLANs** can reduce lateral movement and limit the blast radius of a compromise.
13. Plaintext protocols such as **HTTP and Telnet** should generally be replaced with secure alternatives such as **HTTPS and SSH** where appropriate.
14. Knowing common **protocols, ports, and network layers** is essential for network monitoring, troubleshooting, threat detection, and security analysis.

---

# Quick Revision

```text
NETWORKING
│
├── Devices
│   ├── NIC
│   ├── Switch
│   ├── Router
│   ├── Firewall
│   └── Access Point
│
├── Addressing
│   ├── MAC Address
│   ├── IPv4
│   └── IPv6
│
├── Network Types
│   ├── LAN
│   ├── WLAN
│   └── WAN
│
├── Translation
│   ├── NAT
│   └── PAT
│
├── OSI Model
│   ├── Layer 7 → Application
│   ├── Layer 6 → Presentation
│   ├── Layer 5 → Session
│   ├── Layer 4 → Transport
│   ├── Layer 3 → Network
│   ├── Layer 2 → Data Link
│   └── Layer 1 → Physical
│
├── Important Protocols
│   ├── HTTP / HTTPS
│   ├── DNS
│   ├── SSH
│   ├── FTP
│   ├── DHCP
│   ├── TCP
│   └── UDP
│
└── Security Concepts
    ├── ARP Spoofing
    ├── DNS Attacks
    ├── SYN Flood
    ├── Port Scanning
    ├── Network Segmentation
    ├── VLAN
    └── Firewall
```
