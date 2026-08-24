# IP Addressing, CIDR, Ports & Protocols — Cybersecurity Focus

**Topics:** IPv4 vs IPv6, Public vs Private IP, CIDR Subnetting, Network Ports & Wireshark Concepts

---

## Overview

Understanding **IP addressing, subnetting, CIDR, ports, and protocols** is essential for network security and ethical hacking.

These concepts are directly used in:

* Network traffic analysis
* Packet tracing
* Network discovery
* Port scanning
* Nmap
* Wireshark
* Firewall configuration
* Network segmentation
* Threat analysis

---

# IPv4 vs IPv6 Addressing

| Feature                  | IPv4                    | IPv6                                            |
| ------------------------ | ----------------------- | ----------------------------------------------- |
| **Address Size**         | 32-bit                  | 128-bit                                         |
| **Number of Addresses**  | ~4.3 billion (`2^32`)   | ~`3.4 × 10^38` (`2^128`)                        |
| **Format**               | Dotted decimal          | Hexadecimal                                     |
| **Example**              | `192.168.1.1`           | `2001:db8::ff00:42`                             |
| **Configuration**        | Manual / DHCP           | SLAAC / DHCPv6 / Manual                         |
| **Address Availability** | Limited                 | Extremely large address space                   |
| **NAT**                  | Commonly used with IPv4 | Generally not required for address conservation |

### IPv4 Example

```text
192.168.1.10
```

IPv4 contains four 8-bit octets:

```text
192     .     168     .     1     .     10
 ↓            ↓             ↓          ↓
8 bits       8 bits        8 bits     8 bits
```

Total:

```text
8 + 8 + 8 + 8 = 32 bits
```

### IPv6 Example

```text
2001:db8:85a3::8a2e:370:7334
```

IPv6 uses 128-bit addresses represented using hexadecimal notation.

> **Security Note:** IPv6 has a much larger address space, but simply using IPv6 does not automatically make a network more secure. Proper configuration and security controls are still required.

---

# Public IP vs Private IP Address

## 1. Public IP Address

A **Public IP address** is globally routable on the Internet.

It can be used to identify a network interface or service from the public Internet.

### Characteristics

* Globally routable
* Assigned by an ISP or organization
* Can be reachable from the Internet when routing and firewall rules allow it
* Used for Internet-facing services

Example:

```text
8.8.8.8
```

---

# 2. Private IP Address

A **Private IP address** is intended for use inside private networks and is not directly routed across the public Internet.

RFC 1918 defines three major IPv4 private address ranges:

### Private IPv4 Ranges

| Range                           | CIDR             | Typical Use                    |
| ------------------------------- | ---------------- | ------------------------------ |
| `10.0.0.0 – 10.255.255.255`     | `10.0.0.0/8`     | Large enterprise networks      |
| `172.16.0.0 – 172.31.255.255`   | `172.16.0.0/12`  | Medium/large private networks  |
| `192.168.0.0 – 192.168.255.255` | `192.168.0.0/16` | Home and small office networks |

Example:

```text
Laptop
192.168.1.10
     │
     ▼
Router / NAT
     │
     ▼
Public Internet
```

Private addresses normally require a mechanism such as **NAT/PAT** to communicate with the public IPv4 Internet.

> **Security Note:** A private IP address is not automatically secure. Internal systems can still be attacked by compromised devices, insiders, or other hosts on the same network.

---

# CIDR Notation & Subnetting

**CIDR (Classless Inter-Domain Routing)** is a method of representing IP networks using a prefix length.

Example:

```text
192.168.1.0/24
```

The `/24` represents the number of bits used for the network prefix.

### IPv4 Structure

An IPv4 address contains:

```text
32 bits
```

For:

```text
192.168.1.0/24
```

we have:

```text
Network bits = 24
Host bits    = 32 - 24 = 8
```

Therefore:

```text
2^8 = 256 total addresses
```

For a traditional IPv4 subnet:

```text
256 - 2 = 254 usable host addresses
```

The two excluded addresses are:

* Network address
* Broadcast address

### Example

```text
Network:
192.168.1.0/24

First usable:
192.168.1.1

Last usable:
192.168.1.254

Broadcast:
192.168.1.255
```

> Modern networking also includes special cases such as `/31` point-to-point links and `/32` host routes, so the traditional "subtract 2" rule does not apply to every CIDR prefix.

---

# Common CIDR Prefixes

| CIDR Prefix | Subnet Mask       | Traditional Usable IPv4 Hosts | Common Use                  |
| ----------- | ----------------- | ----------------------------: | --------------------------- |
| **/32**     | `255.255.255.255` |                             1 | Single host / host route    |
| **/30**     | `255.255.255.252` |                             2 | Small point-to-point subnet |
| **/24**     | `255.255.255.0`   |                           254 | Common LAN                  |
| **/16**     | `255.255.0.0`     |                        65,534 | Large private network       |
| **/8**      | `255.0.0.0`       |                    16,777,214 | Very large network          |

---

# CIDR and Security

CIDR is important when creating:

* Firewall rules
* Network ACLs
* Security groups
* Routing rules
* Network segmentation policies
* Access control policies

### Example

Blocking:

```text
192.168.1.0/24
```

can apply a rule to the entire `/24` network.

Blocking:

```text
192.168.1.50/32
```

targets a single IPv4 address.

```text
192.168.1.0/24
        ↓
Entire subnet

192.168.1.50/32
        ↓
Single host
```

This is why understanding CIDR is important when designing precise security policies.

---

# Network Ports

An **IP address** identifies a network interface or destination, while a **port number** identifies a logical service endpoint associated with a transport-layer protocol such as TCP or UDP.

A useful analogy:

```text
IP Address = Building Address
Port       = Apartment / Service Number
```

For example:

```text
192.168.1.10:443
```

means:

```text
IP Address → 192.168.1.10
Port       → 443
Protocol   → TCP (commonly for HTTPS)
```

IPv4 and IPv6 each use a **16-bit port number**, giving:

```text
0 – 65,535
```

---

# Port Categories

## 1. Well-Known Ports

```text
0 – 1023
```

These ports are associated with commonly used services and protocols.

Examples:

* `22` → SSH
* `53` → DNS
* `80` → HTTP
* `443` → HTTPS

---

## 2. Registered Ports

```text
1024 – 49151
```

These ports are commonly associated with applications and services registered with IANA.

Example:

```text
3306 → MySQL
```

---

## 3. Dynamic / Ephemeral Ports

```text
49152 – 65535
```

These are commonly used as temporary source ports for client-side connections.

Example:

```text
Client:
192.168.1.10:52341

        ↓

Server:
93.184.216.34:443
```

Here:

```text
52341 → Ephemeral client port
443   → Server service port
```

> Operating systems may use different ephemeral port ranges depending on the OS and configuration.

---

# Important Ports for Cybersecurity

|      Port | Protocol / Service | Description                  | Security Consideration                                       |
| --------: | ------------------ | ---------------------------- | ------------------------------------------------------------ |
| **20/21** | FTP                | File Transfer Protocol       | Traditional FTP is plaintext                                 |
|    **22** | SSH                | Secure remote access         | Protect with strong authentication and secure configuration  |
|    **23** | Telnet             | Remote access                | Plaintext and generally insecure                             |
|    **25** | SMTP               | Email transfer               | Requires secure configuration and anti-abuse controls        |
|    **53** | DNS                | Domain Name System           | Can be targeted by DNS-based attacks                         |
|    **80** | HTTP               | Web traffic                  | Normally unencrypted                                         |
|   **110** | POP3               | Email retrieval              | Traditional POP3 is plaintext                                |
|   **143** | IMAP               | Email access                 | Use TLS-protected configurations                             |
|   **443** | HTTPS              | HTTP over TLS                | Encrypted in transit                                         |
|   **445** | SMB                | Windows file/printer sharing | Important attack surface when exposed or misconfigured       |
|  **3306** | MySQL              | Database service             | Should generally not be publicly exposed                     |
|  **3389** | RDP                | Windows Remote Desktop       | Protect with strong access controls and network restrictions |

> A port number alone does not determine whether a service is secure. Security depends on the service, configuration, authentication, exposure, software version, and applied security controls.

---

# Localhost / Loopback

The **Loopback address** refers to the local system itself.

### IPv4

```text
127.0.0.1
```

### IPv6

```text
::1
```

Common hostname:

```text
localhost
```

### Example

If a web server is running locally:

```text
http://127.0.0.1:8080
```

the request is being sent to a service running on the same machine.

### Security Use

Loopback addresses are commonly used for:

* Local development
* Testing applications
* Local APIs
* Internal services
* Security testing

---

# APIPA

**APIPA (Automatic Private IP Addressing)** is a mechanism used by systems such as Windows to automatically assign an IPv4 address when DHCP configuration is unsuccessful.

The typical APIPA range is:

```text
169.254.0.0/16
```

Example:

```text
169.254.25.10
```

If a device unexpectedly receives a `169.254.x.x` address, it may indicate a problem communicating with the DHCP server or network configuration.

> APIPA is not the same thing as an RFC 1918 private address range.

---

# Special IPv4 Addresses

## 0.0.0.0

```text
0.0.0.0
```

The meaning depends on context.

For example:

```text
0.0.0.0/0
```

represents all IPv4 addresses and is commonly used in routing or firewall rules to mean "any IPv4 destination."

A server binding to:

```text
0.0.0.0
```

usually means it is listening on all available IPv4 interfaces.

---

# Broadcast Address

An IPv4 broadcast address is used to communicate with all hosts within a broadcast domain/subnet.

Example:

```text
Network:
192.168.1.0/24

Broadcast:
192.168.1.255
```

A packet sent to the subnet's broadcast address is intended for all hosts on that local broadcast domain.

---

# Network Address

The **Network Address** identifies the subnet itself.

Example:

```text
192.168.1.0/24
```

Here:

```text
Network Address → 192.168.1.0
```

The network address is not normally assigned to an individual host in a traditional IPv4 subnet.

---

# Nmap and IP Discovery

Network discovery is an important concept in security assessment.

A security professional may identify active hosts within an authorized network range.

Example:

```text
192.168.1.0/24
```

This represents a subnet containing 256 IPv4 addresses.

A discovery process may determine:

```text
192.168.1.1   → Active
192.168.1.10  → Active
192.168.1.20  → Active
192.168.1.50  → Active
```

Nmap can be used for authorized network discovery and security testing.

> Only scan systems and networks that you own or have explicit permission to test.

---

# Port Scanning

After identifying hosts, security professionals may determine which TCP or UDP ports are reachable.

Conceptually:

```text
Target Host
     │
     ├── 22  → Open
     ├── 80  → Open
     ├── 443 → Open
     ├── 3306 → Closed/Filtered
     └── 8080 → Open
```

Open ports may reveal which services are exposed.

### Security Importance

Port scanning can help identify:

* Exposed services
* Unnecessary services
* Attack surface
* Network filtering
* Potential misconfigurations

---

# Wireshark Concepts

**Wireshark** is a network protocol analyzer used to capture and inspect network traffic.

A simplified packet structure:

```text
┌──────────────────────────┐
│ Ethernet Frame           │
├──────────────────────────┤
│ IP Packet                │
├──────────────────────────┤
│ TCP / UDP Segment        │
├──────────────────────────┤
│ Application Data         │
└──────────────────────────┘
```

For an HTTPS connection, you may see:

```text
Ethernet
   ↓
IP
   ↓
TCP
   ↓
TLS
   ↓
Encrypted Application Data
```

---

# Useful Wireshark Fields

When analyzing packets, common fields include:

### Ethernet

* Source MAC
* Destination MAC
* EtherType

### IP

* Source IP
* Destination IP
* TTL
* Protocol

### TCP

* Source Port
* Destination Port
* Sequence Number
* Acknowledgment Number
* Flags

### UDP

* Source Port
* Destination Port
* Length

### Application Protocols

* HTTP
* DNS
* TLS
* DHCP
* ICMP
* SSH

---

# Network Communication Example

Suppose a user visits:

```text
https://example.com
```

A simplified flow is:

```text
Browser
   ↓
DNS
   ↓
IP Address
   ↓
TCP Connection
   ↓
TLS Handshake
   ↓
HTTPS Request
   ↓
Server Response
```

At the network level:

```text
Application
    ↓
TLS
    ↓
TCP
    ↓
IP
    ↓
Ethernet / Wi-Fi
    ↓
Physical Network
```

---

# Cybersecurity Attack Surface

IP addresses and ports are important because they help define what is exposed to a network.

Example:

```text
Internet
    │
    ▼
Public IP
203.0.113.10
    │
    ├── 22  → SSH
    ├── 80  → HTTP
    └── 443 → HTTPS
```

Each exposed service represents a potential part of the network's attack surface.

Security teams can reduce unnecessary exposure by:

* Closing unused ports
* Removing unnecessary services
* Restricting source IPs
* Using firewalls
* Applying network segmentation
* Using secure authentication
* Monitoring network traffic
* Keeping services patched

---

# Key Security Takeaways

1. **IPv4** uses 32-bit addresses, while **IPv6** uses 128-bit addresses.
2. **Public IPs** are globally routable, while **RFC 1918 private IPs** are intended for private networks.
3. **CIDR notation** defines the network prefix and is essential for subnetting and security policies.
4. `192.168.1.0/24` represents an IPv4 subnet with **256 total addresses** and traditionally **254 usable host addresses**.
5. **Ports** identify logical service endpoints associated with TCP or UDP.
6. Ports range from **0 to 65,535**.
7. **Well-known ports** range from `0–1023`.
8. **Registered ports** range from `1024–49151`.
9. **Dynamic/Ephemeral ports** commonly range from `49152–65535`.
10. **127.0.0.1** and **::1** represent IPv4 and IPv6 loopback addresses.
11. **169.254.0.0/16** is the IPv4 APIPA range commonly assigned when DHCP configuration fails.
12. **Nmap** can be used for authorized host discovery and port scanning.
13. **Wireshark** can capture and analyze network packets.
14. Open ports and exposed services contribute to an organization's **attack surface**.
15. Firewall rules, CIDR ranges, segmentation, and port restrictions are important tools for controlling network exposure.
16. Always perform network scanning and security testing only on systems you own or have explicit authorization to test.

---

# Quick Revision

```text
IP ADDRESSING
│
├── IPv4
│   └── 32-bit
│
├── IPv6
│   └── 128-bit
│
├── Public IP
│   └── Globally Routable
│
└── Private IP
    ├── 10.0.0.0/8
    ├── 172.16.0.0/12
    └── 192.168.0.0/16


CIDR
│
├── /32 → Single Host
├── /30 → Small Point-to-Point Subnet
├── /24 → 254 Traditional Usable Hosts
├── /16 → 65,534 Traditional Usable Hosts
└── /8  → 16,777,214 Traditional Usable Hosts


PORTS
│
├── 0–1023       → Well-Known
├── 1024–49151   → Registered
└── 49152–65535  → Dynamic / Ephemeral


IMPORTANT
│
├── 22   → SSH
├── 53   → DNS
├── 80   → HTTP
├── 443  → HTTPS
├── 445  → SMB
├── 3306 → MySQL
└── 3389 → RDP


SECURITY TOOLS
│
├── Nmap
│   ├── Host Discovery
│   └── Port Scanning
│
└── Wireshark
    ├── Packet Capture
    ├── Protocol Analysis
    └── Traffic Investigation
```
