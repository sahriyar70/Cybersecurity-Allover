# Tor Network, Tails OS, Whonix & Proxy Guide

This guide covers the basic concepts and essential commands of Tor Network, Tails OS, Whonix, and Proxy for privacy, anonymity, and secure browsing.

---

## 1. Tor Network

**Tor (The Onion Router)** is a network that routes internet traffic through multiple relays to help hide the user's IP address.

### How Tor Works

1. **Entry Guard:** The user's traffic enters the Tor Network.
2. **Middle Relay:** Traffic passes through one or more intermediate relays.
3. **Exit Relay:** Traffic reaches the destination website.

Tor encryption is often compared to layers of an onion.

### Install Tor (Kali Linux / Debian)

```bash
sudo apt update
sudo apt install tor
```

### Tor Service Commands

```bash
sudo systemctl start tor
```
Starts the Tor service.

```bash
sudo systemctl stop tor
```
Stops the Tor service.

```bash
sudo systemctl status tor
```
Displays the current status of the Tor service.

```bash
sudo systemctl enable tor
```
Enables Tor to start automatically during system boot.

### Test Tor Connection

```bash
curl --socks5-hostname 127.0.0.1:9050 https://check.torproject.org/api/ip
```

Tests the connection using the Tor SOCKS5 proxy.

**Note:** The default SOCKS proxy port for the Tor service is usually `9050`. Tor Browser may use its own Tor connection.

---

## 2. Tails OS

**Tails (The Amnesic Incognito Live System)** is a privacy-focused Linux operating system that can be booted from a USB drive.

### Key Features

- Routes internet traffic through the Tor Network.
- Does not normally save user activity after shutdown.
- Provides an amnesic environment to reduce digital traces.
- Designed for privacy and secure communication.

### Verify Tor Connection

After starting Tails and establishing a Tor connection:

```bash
curl https://check.torproject.org/api/ip
```

Checks whether the Tor connection is working.

### Persistent Storage

Tails provides Persistent Storage to save selected files and settings across sessions.

**Note:** Tails is designed to improve privacy, but it does not provide complete protection against all tracking or malware.

---

## 3. Whonix

**Whonix** is a privacy-focused operating system designed to run inside virtual machines.

### Architecture

Whonix has two main components:

| Component | Function |
|---|---|
| Whonix-Gateway | Routes network traffic through Tor |
| Whonix-Workstation | Runs user applications |

### How It Works

```text
User Application
       |
Whonix-Workstation
       |
Whonix-Gateway
       |
   Tor Network
       |
   Internet
```

Whonix-Workstation does not connect directly to the Internet. Its network traffic passes through the Gateway.

### Verify Tor Connection

From Whonix-Workstation:

```bash
curl https://check.torproject.org/api/ip
```

Checks whether the connection is using the Tor Network.

**Note:** Whonix improves security by separating the Gateway and Workstation through network isolation.

---

## 4. Proxy Server

A **Proxy Server** acts as an intermediary between a user and the Internet, forwarding network requests on behalf of the user.

### Types of Proxy

| Proxy | Description |
|---|---|
| HTTP Proxy | Forwards HTTP traffic |
| HTTPS Proxy | Supports HTTPS connections |
| SOCKS5 Proxy | Forwards different types of network traffic |
| Transparent Proxy | Forwards traffic without requiring separate client configuration |

### Proxy Configuration (Linux)

```bash
export http_proxy="http://127.0.0.1:8080"
```

Sets the HTTP proxy.

```bash
export https_proxy="http://127.0.0.1:8080"
```

Sets the HTTPS proxy.

```bash
export all_proxy="socks5h://127.0.0.1:9050"
```

Sets a SOCKS5 proxy and directs DNS resolution through the proxy.

### Check Proxy Configuration

```bash
env | grep -i proxy
```

Displays the current proxy environment variables.

### Remove Proxy

```bash
unset http_proxy
unset https_proxy
unset all_proxy
```

Removes the proxy environment variables.

---

## 5. Tor vs Proxy vs VPN

| Feature | Tor | Proxy | VPN |
|---|---|---|---|
| Hides IP Address | Yes | Yes | Yes |
| Traffic Encryption | Within Tor Network | Depends on proxy type | Within VPN tunnel |
| Multiple Relays | Yes | Usually No | Usually No |
| Speed | Relatively slow | Depends on proxy | Usually faster |
| Main Purpose | Anonymity | Traffic forwarding | Secure connection |

---

## Important Security Notes

- Tor does not guarantee complete anonymity.
- Logging into personal accounts may reveal your identity.
- HTTPS encrypts communication between the browser and the destination website, including when using a Tor exit relay.
- Unknown proxy servers may introduce privacy and security risks.
- Tails and Whonix cannot protect against every threat; safe user behavior remains important.
- Always follow local laws and conduct security testing only on authorized systems.

---

## Summary

- **Tor:** An anonymity-focused network that routes traffic through multiple relays.
- **Tails:** A privacy-focused live operating system that can run from a USB drive.
- **Whonix:** Uses separate Gateway and Workstation environments to route traffic through Tor.
- **Proxy:** Forwards requests between a client and the Internet.


