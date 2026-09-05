# TCP vs UDP Protocols (Transport Layer Deep Dive)

**Topic:** Transport Layer Protocols, TCP 3-Way Handshake, UDP Mechanisms & Cybersecurity Impact

---

## Overview

The **Transport Layer (Layer 4)** is responsible for end-to-end communication between applications running on different hosts.

Two of the most important Transport Layer protocols are:

* **TCP (Transmission Control Protocol)**
* **UDP (User Datagram Protocol)**

The choice between TCP and UDP depends on application requirements such as **reliability, ordering, latency, and overhead**.

> **Important:** TCP is not simply "slow" and UDP is not always "faster." UDP has lower protocol overhead and avoids connection establishment/retransmission mechanisms, which can reduce latency in suitable applications. Actual performance depends on the network and application.

---

# TCP (Transmission Control Protocol)

TCP is a **connection-oriented, reliable, byte-stream transport protocol**.

Before transferring application data, TCP establishes a connection between the client and server.

## Key Characteristics

### 1. Connection-Oriented

TCP establishes a connection before data transfer using the **TCP 3-Way Handshake**.

```text
Client                    Server
  |                         |
  | -------- SYN ---------> |
  | <----- SYN-ACK -------- |
  | -------- ACK ---------> |
  |                         |
  |   Connection Ready      |
```

---

### 2. Reliable Delivery

TCP provides mechanisms that allow data to be delivered reliably.

It uses:

* Sequence numbers
* Acknowledgements (ACKs)
* Retransmission
* Checksums
* Timers

If transmitted data is lost, TCP can retransmit the missing data.

---

### 3. Ordered Delivery

TCP uses **sequence numbers** to keep track of bytes in the data stream.

If segments arrive out of order, TCP can reorder the data before delivering the byte stream to the application.

---

### 4. Flow Control

TCP uses a **receive window** to prevent the sender from overwhelming the receiver.

The receiver can advertise how much additional data it is currently able to accept.

---

### 5. Congestion Control

TCP also implements congestion-control mechanisms to reduce the amount of traffic sent when network congestion is detected.

This helps TCP adapt to changing network conditions.

---

### 6. Header Size and Overhead

A TCP header has a minimum size of **20 bytes**, excluding optional fields.

TCP has more protocol overhead than UDP because it provides features such as:

* Connection management
* Sequence numbers
* Acknowledgements
* Retransmission
* Flow control
* Congestion control

---

## Common TCP Use Cases

TCP is commonly used when reliable and ordered delivery is important.

Examples include:

* **HTTP/HTTPS** — Web communication over TCP in HTTP/1.1 and HTTP/2
* **SSH** — Secure remote administration
* **SMTP** — Email transmission
* **IMAP** — Email retrieval
* **FTP** — File transfer
* **Database connections** — Many database protocols use TCP

> **Note:** HTTP/3 uses **QUIC over UDP** instead of TCP.

---

# UDP (User Datagram Protocol)

UDP is a **connectionless, datagram-oriented transport protocol**.

Unlike TCP, UDP does not establish a connection before sending data.

Each UDP datagram is sent independently.

## Key Characteristics

### 1. Connectionless

UDP does not perform a TCP-style handshake before sending data.

```text
Sender
   |
   | ------ UDP Datagram -----> Receiver
   |
   | ------ UDP Datagram -----> Receiver
   |
```

---

### 2. No Guaranteed Delivery

UDP does not guarantee that a datagram will reach the destination.

There is no built-in:

* Acknowledgement
* Retransmission
* Guaranteed delivery
* Guaranteed ordering

If an application requires reliability, it may implement its own reliability mechanisms on top of UDP.

---

### 3. No Guaranteed Ordering

UDP datagrams can arrive:

* In order
* Out of order
* Duplicated
* Not at all

UDP itself does not reorder them.

---

### 4. Low Overhead

The UDP header is only **8 bytes**.

Its basic header contains:

```text
Source Port
Destination Port
Length
Checksum
```

Because UDP provides fewer transport-level mechanisms than TCP, it is useful for applications where low overhead and low latency are important.

---

## Common UDP Use Cases

UDP is commonly used in applications where latency, simplicity, or application-controlled transport behavior is important.

Examples include:

* **DNS** — Commonly uses UDP for standard queries
* **DHCP** — Uses UDP
* **VoIP**
* **Real-time audio/video**
* **Online gaming**
* **QUIC / HTTP/3**

> UDP does not automatically make an application real-time or faster. The application must be designed to handle issues such as packet loss and reordering.

---

# TCP vs UDP Comparison

| Feature                 | TCP                                                    | UDP                            |
| ----------------------- | ------------------------------------------------------ | ------------------------------ |
| **Connection Type**     | Connection-oriented                                    | Connectionless                 |
| **Data Model**          | Byte stream                                            | Datagram                       |
| **Delivery Guarantee**  | Reliable delivery mechanisms                           | No delivery guarantee          |
| **Ordering**            | Ordered byte stream                                    | No ordering guarantee          |
| **Retransmission**      | Yes                                                    | No built-in retransmission     |
| **Acknowledgements**    | Yes                                                    | No built-in ACK                |
| **Flow Control**        | Yes                                                    | No built-in flow control       |
| **Congestion Control**  | Yes                                                    | No built-in congestion control |
| **Header Size**         | Minimum 20 bytes                                       | 8 bytes                        |
| **Overhead**            | Higher                                                 | Lower                          |
| **Latency**             | Can be higher due to connection/reliability mechanisms | Often lower overhead           |
| **Communication Style** | Stream-based                                           | Message/datagram-based         |
| **Examples**            | SSH, SMTP, FTP, HTTP/1.1, HTTP/2                       | DNS, DHCP, QUIC, VoIP, gaming  |

---

# TCP 3-Way Handshake

The **TCP 3-Way Handshake** is used to establish a TCP connection and synchronize initial sequence numbers between the client and server.

```text
Client                                  Server
  |                                      |
  | ----------- SYN -------------------> |
  |                                      |
  | <---------- SYN-ACK ---------------- |
  |                                      |
  | ----------- ACK -------------------> |
  |                                      |
  |       TCP Connection Established     |
```

## Step 1 — SYN

The client sends a **SYN (Synchronize)** segment to the server.

It essentially indicates:

> "I want to establish a TCP connection."

The SYN contains an initial sequence number.

---

## Step 2 — SYN-ACK

The server responds with:

**SYN + ACK**

This means the server:

* Received the client's SYN
* Acknowledged it
* Wants to establish the connection as well

---

## Step 3 — ACK

The client sends an **ACK (Acknowledgement)** back to the server.

The TCP connection is now established and application data can be exchanged.

---

# Why the TCP Handshake Matters in Cybersecurity

Understanding the TCP handshake helps security professionals understand:

* Port scanning
* Firewall behavior
* Network troubleshooting
* SYN flood attacks
* Connection states
* Packet analysis
* Intrusion detection

For example, a packet capture in Wireshark may show:

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
 ↓
Application Data
```

---

# Cybersecurity Context & Attack Vectors

## 1. TCP SYN Flood Attack

A **SYN flood** is a type of Denial-of-Service attack that abuses the TCP connection-establishment process.

A simplified attack pattern looks like:

```text
Attacker
   |
   | -------- SYN --------> Server
   |
   | <------ SYN-ACK ------ Server
   |
   X
   No final ACK
```

The server may maintain many **half-open connections** while waiting for the final ACK.

If the system receives enough malicious connection attempts, available connection-tracking resources can become exhausted, potentially preventing legitimate users from connecting.

### Defensive Measures

Common defenses include:

* SYN cookies
* Connection-rate limiting
* Firewall filtering
* Load balancing
* DDoS protection
* Increasing backlog capacity
* Network monitoring

---

# 2. UDP Reflection / Amplification Attacks

UDP can be abused in **reflection and amplification attacks**.

A simplified example:

```text
Attacker
   |
   | Spoofed request
   ↓
Open UDP Server
   |
   | Large response
   ↓
Victim
```

The attacker attempts to make third-party UDP servers send responses toward the victim.

If the response is significantly larger than the request, the attack can create **traffic amplification**.

Examples of historically abused services include:

* DNS
* NTP
* SSDP
* Memcached

### Important Concept

The key problem is not simply that UDP has "no source IP validation."

Rather, **IP spoofing can be used with UDP because the protocol itself does not establish a connection that inherently validates the sender's identity**. Network-level anti-spoofing controls such as BCP 38 can help reduce this abuse.

---

# 3. Port Scanning with Nmap

Port scanning is a common network reconnaissance technique used by security professionals.

> **Only scan systems and networks that you own or have explicit authorization to test.**

## TCP SYN Scan (`-sS`)

A TCP SYN scan sends a SYN packet and analyzes the response.

Simplified behavior:

```text
Scanner                 Target
   |                       |
   | ------ SYN ---------> |
   | <---- SYN-ACK ------- |  Open
   |                       |
```

The scanner normally does **not complete the full TCP connection** when it receives SYN-ACK. Instead, it can send a reset (RST) to terminate the attempt.

This is why it is often called a **half-open SYN scan**.

### Typical interpretation

```text
SYN → SYN-ACK
= Port likely open
```

```text
SYN → RST
= Port likely closed
```

Firewall filtering can produce different results, so scan results should be interpreted carefully.

---

# UDP Scan (`-sU`)

UDP scanning works differently because UDP has no TCP-style handshake.

Nmap may send UDP probes and analyze responses.

For example:

```text
UDP Probe
   ↓
Closed UDP Port
   ↓
ICMP Port Unreachable
```

An open UDP service may respond at the application layer, while an open/filtered port may produce little or no response.

Therefore, **UDP scanning is often slower and more difficult to interpret than TCP scanning**.

---

# TCP vs UDP from a Security Perspective

Understanding the differences between TCP and UDP helps security professionals identify attack surfaces.

## TCP Security Considerations

Important concepts include:

```text
TCP Handshake
TCP States
SYN Flood
Connection Exhaustion
RST Attacks
Port Scanning
Session Management
```

## UDP Security Considerations

Important concepts include:

```text
IP Spoofing
Reflection
Amplification
UDP Flooding
Stateless Communication
DNS Security
DHCP Security
```

---

# Packet Analysis with Wireshark

Wireshark can be used to inspect TCP and UDP traffic.

### TCP example

```text
SYN
↓
SYN-ACK
↓
ACK
↓
Application Data
↓
FIN/ACK
```

### UDP example

```text
UDP Datagram
↓
Application Data
```

There is no TCP-style connection handshake.

Useful Wireshark filters include:

```text
tcp
udp
tcp.flags.syn == 1
tcp.flags.ack == 1
udp.port == 53
tcp.port == 443
```

These filters can help analyze network traffic during authorized labs and troubleshooting.

---

# Real-World Example

Suppose you visit a website:

```text
Browser
   ↓
HTTP/HTTPS
   ↓
Transport Layer
   ↓
TCP (HTTP/1.1 or HTTP/2)
   ↓
IP
   ↓
Ethernet/Wi-Fi
   ↓
Network
```

For HTTP/3:

```text
Browser
   ↓
HTTP/3
   ↓
QUIC
   ↓
UDP
   ↓
IP
   ↓
Ethernet/Wi-Fi
```

This is an important modern networking concept:

> **HTTP does not always mean TCP. HTTP/3 uses QUIC, which runs over UDP.**

---

# Key Takeaways

1. **TCP is connection-oriented and provides reliable, ordered byte-stream delivery.**

2. **UDP is connectionless and provides best-effort datagram delivery without built-in retransmission or ordering.**

3. TCP has a minimum **20-byte header**, while UDP has an **8-byte header**.

4. TCP uses mechanisms such as:

   * Sequence numbers
   * ACKs
   * Retransmission
   * Flow control
   * Congestion control

5. UDP has lower transport-level overhead and is useful for applications that prioritize latency, simplicity, or application-controlled reliability.

6. The **TCP 3-Way Handshake** is:

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
```

7. **SYN floods** abuse TCP connection establishment.

8. **UDP reflection/amplification attacks** abuse UDP services and IP spoofing.

9. **TCP SYN scanning** uses TCP responses to infer port state.

10. **UDP scanning** is more difficult because UDP has no connection handshake and many services may not respond to unexpected probes.

11. Understanding TCP and UDP is essential for:

```text
Network Security
Penetration Testing
SOC Analysis
Incident Response
Wireshark
Nmap
Firewall Configuration
Threat Detection
```

---

# Quick Revision

```text
TCP
├── Connection-oriented
├── Reliable
├── Ordered
├── ACK
├── Retransmission
├── Flow Control
├── Congestion Control
├── 20+ byte header
└── SYN → SYN-ACK → ACK

UDP
├── Connectionless
├── Best-effort
├── No built-in ACK
├── No built-in retransmission
├── No ordering guarantee
├── 8 byte header
└── Low protocol overhead

Cybersecurity
├── TCP → SYN Flood
├── TCP → SYN Scanning
├── UDP → Reflection
├── UDP → Amplification
├── UDP → Flooding
└── Wireshark → Packet Analysis
```

## Final Concept

The most important thing to remember is:

> **TCP focuses on reliable, ordered delivery, while UDP provides a simpler datagram service with lower protocol overhead.**

Neither protocol is universally "better." The correct choice depends on the requirements of the application.
