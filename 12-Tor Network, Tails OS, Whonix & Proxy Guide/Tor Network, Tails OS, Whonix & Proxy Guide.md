# Tor Network, Tails OS, Whonix & Proxy Guide

এই নোটে Privacy, Anonymity এবং Secure Browsing-এর জন্য ব্যবহৃত Tor Network, Tails OS, Whonix ও Proxy-এর মূল ধারণা এবং গুরুত্বপূর্ণ কমান্ড আলোচনা করা হয়েছে।

---

## 1. Tor Network

**Tor (The Onion Router)** হলো একটি নেটওয়ার্ক, যা একাধিক Relay-এর মাধ্যমে ইন্টারনেট ট্রাফিক পাঠিয়ে ব্যবহারকারীর IP Address আড়াল করতে সাহায্য করে।

### How Tor Works
1. **Entry Guard:** ব্যবহারকারীর ট্রাফিক Tor Network-এ প্রবেশ করে।
2. **Middle Relay:** ট্রাফিক একাধিক Relay-এর মধ্য দিয়ে যায়।
3. **Exit Relay:** ট্রাফিক গন্তব্য ওয়েবসাইটে পৌঁছায়।

Tor Encryption-কে Onion-এর স্তরের সঙ্গে তুলনা করা হয়।

### Tor Installation (Kali Linux / Debian)

```bash
sudo apt update
sudo apt install tor
```

### Tor Service Commands

```bash
sudo systemctl start tor
```
Tor Service চালু করে।

```bash
sudo systemctl stop tor
```
Tor Service বন্ধ করে।

```bash
sudo systemctl status tor
```
Tor Service-এর বর্তমান অবস্থা দেখায়।

```bash
sudo systemctl enable tor
```
System Boot-এর সময় Tor Service স্বয়ংক্রিয়ভাবে চালু করে।

### Tor Connection Test

```bash
curl --socks5-hostname 127.0.0.1:9050 https://check.torproject.org/api/ip
```

Tor SOCKS5 Proxy ব্যবহার করে সংযোগ পরীক্ষা করে।

**Note:** সাধারণত Tor Service-এর SOCKS Proxy Port হলো `9050`। Tor Browser নিজস্ব Tor Connection ব্যবহার করতে পারে।

---

## 2. Tails OS

**Tails (The Amnesic Incognito Live System)** হলো একটি Privacy-focused Linux Operating System, যা USB থেকে চালানো যায়।

### Key Features
- Tor Network-এর মাধ্যমে ইন্টারনেট ট্রাফিক পাঠায়।
- Default অবস্থায় Shutdown-এর পর ব্যবহারকারীর কার্যক্রম সংরক্ষণ করে না।
- Amnesic System: ব্যবহারকারীর ডিজিটাল চিহ্ন কমিয়ে রাখে।
- Secure Communication ও Privacy-এর জন্য উপযোগী।

### Verify Tor Connection

Tails চালু করে Tor Connection স্থাপন হওয়ার পর:

```bash
curl https://check.torproject.org/api/ip
```

Tor Connection সঠিকভাবে কাজ করছে কি না পরীক্ষা করতে পারে।

### Persistent Storage
Tails-এর Persistent Storage ব্যবহার করে নির্বাচিত ফাইল ও সেটিংস সংরক্ষণ করা যায়।

**Note:** Tails-এর উদ্দেশ্য হলো Live System-এর মাধ্যমে Privacy বজায় রাখা। তবে এটি সব ধরনের Tracking বা Malware থেকে সম্পূর্ণ সুরক্ষা দেয় না।

---

## 3. Whonix

**Whonix** হলো একটি Privacy-focused Operating System, যা সাধারণত Virtual Machine-এর মাধ্যমে ব্যবহার করা হয়।

### Architecture

Whonix-এর দুটি প্রধান অংশ:

| Component | Function |
|---|---|
| Whonix-Gateway | Tor-এর মাধ্যমে Network Traffic পাঠায় |
| Whonix-Workstation | ব্যবহারকারীর Application চালায় |

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

Whonix-Workstation সরাসরি Internet-এর সঙ্গে সংযুক্ত হয় না। এর Network Traffic Gateway-এর মাধ্যমে যায়।

### Verify Tor Connection

Whonix-Workstation থেকে:

```bash
curl https://check.torproject.org/api/ip
```

Tor Network-এর মাধ্যমে সংযোগ হচ্ছে কি না পরীক্ষা করে।

**Note:** Whonix-এর মূল সুবিধা হলো Gateway ও Workstation আলাদা রাখার মাধ্যমে Network Isolation নিশ্চিত করা।

---

## 4. Proxy Server

**Proxy Server** হলো ব্যবহারকারী ও Internet-এর মধ্যে একটি মধ্যবর্তী Server, যা ব্যবহারকারীর Network Request Forward করে।

### Types of Proxy

| Proxy | Description |
|---|---|
| HTTP Proxy | HTTP Traffic Forward করে |
| HTTPS Proxy | HTTPS Connection-এর জন্য ব্যবহৃত হয় |
| SOCKS5 Proxy | বিভিন্ন ধরনের Network Traffic Forward করতে পারে |
| Transparent Proxy | ব্যবহারকারীর আলাদা Configuration ছাড়াই Traffic Forward করতে পারে |

### Proxy Configuration (Linux)

```bash
export http_proxy="http://127.0.0.1:8080"
```

HTTP Proxy সেট করে।

```bash
export https_proxy="http://127.0.0.1:8080"
```

HTTPS Proxy সেট করে।

```bash
export all_proxy="socks5h://127.0.0.1:9050"
```

SOCKS5 Proxy সেট করে এবং DNS Resolution Proxy-এর মাধ্যমে করার নির্দেশ দেয়।

### Check Proxy Configuration

```bash
env | grep -i proxy
```

বর্তমান Proxy Environment Variables দেখায়।

### Remove Proxy

```bash
unset http_proxy
unset https_proxy
unset all_proxy
```

Proxy Environment Variables সরিয়ে দেয়।

---

## 5. Tor vs Proxy vs VPN

| Feature | Tor | Proxy | VPN |
|---|---|---|---|
| IP Address Hide | Yes | Yes | Yes |
| Traffic Encryption | Tor Network-এর মধ্যে | Proxy-এর ধরন অনুযায়ী | VPN Tunnel-এর মধ্যে |
| Multiple Relays | Yes | Usually No | Usually No |
| Speed | তুলনামূলক ধীর | Proxy অনুযায়ী | সাধারণত দ্রুত |
| Main Purpose | Anonymity | Traffic Forwarding | Secure Connection |

---

## Important Security Notes

- Tor ব্যবহার করলেই সম্পূর্ণ Anonymity নিশ্চিত হয় না।
- Personal Account-এ Login করলে পরিচয় প্রকাশ পেতে পারে।
- HTTPS ব্যবহার করলে Exit Relay থেকে Website-এর সঙ্গে যোগাযোগ এনক্রিপ্টেড থাকে।
- Unknown Proxy ব্যবহার করলে Privacy ও Security ঝুঁকিতে পড়তে পারে।
- Tails ও Whonix সঠিকভাবে ব্যবহার করলেও নিরাপত্তার জন্য User Behavior গুরুত্বপূর্ণ।
- Tor Network ব্যবহার করার সময় স্থানীয় আইন ও অনুমোদিত Security Testing-এর নিয়ম মেনে চলতে হবে।

---

## Summary

- **Tor:** একাধিক Relay-এর মাধ্যমে Anonymity প্রদানকারী Network।
- **Tails:** USB থেকে চালানো যায় এমন Privacy-focused Live OS।
- **Whonix:** Gateway ও Workstation আলাদা করে Tor Traffic পরিচালনা করে।
- **Proxy:** Client ও Internet-এর মধ্যে Request Forward করে।

