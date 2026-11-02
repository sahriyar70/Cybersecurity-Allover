# Cybersecurity Privacy & Anonymity Guide

এই নোটে Anonymity, Tor Network, Tails OS, Whonix, Proxy Chaining এবং GhostSwitch-এর মূল ধারণা ও গুরুত্বপূর্ণ কমান্ড আলোচনা করা হয়েছে।

---

## ১. Anonymity (পরিচয় গোপন রাখা)

**Anonymity** হলো ইন্টারনেটে নিজের প্রকৃত পরিচয় ও ব্যক্তিগত তথ্য প্রকাশ না করে কার্যক্রম পরিচালনা করা।

### গুরুত্বপূর্ণ ধারণা

| Term | কাজ |
|---|---|
| Privacy | ব্যক্তিগত তথ্য সুরক্ষিত রাখা |
| Anonymity | নিজের পরিচয় গোপন রাখা |
| IP Masking | প্রকৃত IP Address আড়াল করা |
| Encryption | তথ্যকে এনক্রিপ্ট করে সুরক্ষিত রাখা |
| Fingerprinting | Browser ও Device-এর বৈশিষ্ট্য দিয়ে ব্যবহারকারী শনাক্ত করা |

**মনে রাখবে:** IP Address লুকালেই সম্পূর্ণ Anonymity নিশ্চিত হয় না। Login, Cookies ও Browser Fingerprinting থেকেও পরিচয় প্রকাশ হতে পারে।

---

## ২. Tor Network

**Tor (The Onion Router)** হলো একটি Privacy Network, যা একাধিক Relay-এর মাধ্যমে Internet Traffic পাঠিয়ে ব্যবহারকারীর IP Address আড়াল করতে সাহায্য করে।

### How Tor Works

```text
User
  |
Entry Guard
  |
Middle Relay
  |
Exit Relay
  |
Website
```

প্রতিটি Relay Tor-এর Encryption Layer-এর একটি অংশ সরিয়ে পরবর্তী Relay-এর কাছে Traffic পাঠায়।

### Tor Installation (Kali Linux)

```bash
sudo apt update
sudo apt install tor
```

### Tor Service Commands

```bash
sudo systemctl start tor
sudo systemctl stop tor
sudo systemctl status tor
```

যথাক্রমে Tor চালু, বন্ধ ও Status পরীক্ষা করে।

### Tor Connection Test

```bash
curl --socks5-hostname 127.0.0.1:9050 \
https://check.torproject.org/api/ip
```

Tor SOCKS5 Proxy-এর মাধ্যমে Connection পরীক্ষা করে।

**Note:** Tor Browser সাধারণত নিজস্ব Tor Connection ব্যবহার করে। System Tor Service-এর Port সাধারণত `9050`।

---

## ৩. Tails OS

**Tails (The Amnesic Incognito Live System)** হলো একটি Privacy-focused Linux OS, যা USB Drive থেকে চালানো যায়।

### প্রধান কাজ

- Internet Traffic Tor Network-এর মাধ্যমে পাঠায়।
- Shutdown-এর পর সাধারণত Session-এর তথ্য সংরক্ষণ করে না।
- Persistent Storage দিয়ে নির্বাচিত ফাইল সংরক্ষণ করা যায়।
- Privacy ও Secure Communication-এর জন্য ব্যবহৃত হয়।

### Network Test

```bash
curl https://check.torproject.org/api/ip
```

Tor Connection পরীক্ষা করে।

### গুরুত্বপূর্ণ Commands

```bash
ip addr
```

Network Interface ও IP Address দেখায়।

```bash
ip route
```

Routing Table দেখায়।

**Note:** Tails ব্যবহার করলেও ব্যক্তিগত Account-এ Login করলে পরিচয় প্রকাশ হতে পারে।

---

## ৪. Whonix

**Whonix** হলো একটি Privacy-focused Operating System, যা Virtual Machine-এর মাধ্যমে ব্যবহার করা হয়।

### Whonix Architecture

```text
Whonix-Workstation
        |
Whonix-Gateway
        |
    Tor Network
        |
     Internet
```

| Component | কাজ |
|---|---|
| Whonix-Gateway | Tor-এর মাধ্যমে Traffic পাঠায় |
| Whonix-Workstation | User Applications চালায় |

### প্রধান সুবিধা

- Network Isolation
- Tor-এর মাধ্যমে Traffic Routing
- Workstation থেকে সরাসরি Internet Access বন্ধ রাখা

### Verification

```bash
curl https://check.torproject.org/api/ip
```

Tor Connection পরীক্ষা করে।

---

## ৫. Proxy & Proxy Chaining

**Proxy Server** হলো Client ও Internet-এর মধ্যে একটি মধ্যবর্তী Server, যা Network Request Forward করে।

### Proxy Types

| Type | কাজ |
|---|---|
| HTTP Proxy | HTTP Traffic Forward করে |
| SOCKS5 Proxy | বিভিন্ন Network Traffic Forward করে |
| Transparent Proxy | Client-এর আলাদা Configuration ছাড়া Traffic Forward করে |

### Proxy Configuration

```bash
export http_proxy="http://127.0.0.1:8080"
export https_proxy="http://127.0.0.1:8080"
```

HTTP ও HTTPS Proxy সেট করে।

### Proxy Chaining

**Proxy Chaining** হলো একাধিক Proxy Server-এর মধ্য দিয়ে Traffic পাঠানোর প্রক্রিয়া।

```text
User
 |
Proxy 1
 |
Proxy 2
 |
Proxy 3
 |
Internet
```

### ProxyChains Installation

```bash
sudo apt update
sudo apt install proxychains4
```

### Configuration File

```bash
sudo nano /etc/proxychains4.conf
```

ফাইলের নিচে Proxy Server যোগ করা যায়:

```text
[ProxyList]
socks5 127.0.0.1 9050
```

### ProxyChains Commands

```bash
proxychains4 curl https://check.torproject.org/api/ip
```

Tor SOCKS5 Proxy-এর মাধ্যমে Request পাঠায়।

```bash
proxychains4 firefox
```

ProxyChains-এর মাধ্যমে Firefox চালানোর চেষ্টা করে।

### Chain Modes

| Mode | কাজ |
|---|---|
| strict_chain | সব Proxy নির্দিষ্ট ক্রমে ব্যবহার করে |
| dynamic_chain | সচল Proxy ব্যবহার করে নির্দিষ্ট ক্রম বজায় রাখে |
| random_chain | তালিকা থেকে Proxy এলোমেলোভাবে নির্বাচন করে |

**Note:** ProxyChains সব Application-এর Traffic নিয়ন্ত্রণ করতে পারে না। এটি মূলত নির্দিষ্ট Linux Application-এর Connection Redirect করে।

---

## ৬. GhostSwitch

**GhostSwitch** নামটি বিভিন্ন Tool বা Project-এর জন্য ব্যবহৃত হতে পারে। এখানে এটিকে Privacy Tool-এর একটি সাধারণ ধারণা হিসেবে ব্যাখ্যা করা হয়েছে—যেখানে একটি Switch দিয়ে Proxy বা Tor Connection চালু ও বন্ধ করা হয়।

### সাধারণ কাজ

- Proxy Connection চালু বা বন্ধ করা
- Network Traffic-এর Routing পরিবর্তন করা
- Privacy Connection-এর Status পরীক্ষা করা

### Linux Proxy Toggle

Proxy চালু:

```bash
export all_proxy="socks5h://127.0.0.1:9050"
```

Proxy বন্ধ:

```bash
unset all_proxy
```

বর্তমান Proxy পরীক্ষা:

```bash
env | grep -i proxy
```

**Note:** এটি Linux-এর সাধারণ Proxy Toggle, নির্দিষ্ট GhostSwitch Software-এর Command নয়। নির্দিষ্ট GhostSwitch Tool-এর Repository বা Link পেলে তার সঠিক Command যোগ করা যাবে।

---

## ৭. Important Security Commands

| Command | কাজ |
|---|---|
| `ip addr` | IP Address দেখায় |
| `ip route` | Routing Table দেখায় |
| `curl ifconfig.me` | Public IP দেখায় |
| `env \| grep -i proxy` | Proxy Settings দেখায় |
| `sudo systemctl status tor` | Tor Service Status দেখায় |
| `ss -tuln` | Listening Ports দেখায় |
| `ping <IP>` | Network Connectivity পরীক্ষা করে |
| `traceroute <IP>` | Network Path পরীক্ষা করে |

---

## ৮. Security Best Practices

- Tor Browser শুধুমাত্র Official Website থেকে Download করবে।
- Unknown Proxy Server ব্যবহার করা থেকে বিরত থাকবে।
- ব্যক্তিগত Account-এ Login করলে Anonymity কমে যেতে পারে।
- HTTPS Website ব্যবহার করবে।
- Browser Extension কম ব্যবহার করবে।
- Tails ও Whonix-এর Security Update নিয়মিত করবে।
- Security Testing শুধুমাত্র অনুমোদিত System-এ করবে।

---

## Summary

- **Anonymity:** নিজের পরিচয় গোপন রাখা।
- **Tor:** একাধিক Relay-এর মাধ্যমে Traffic পাঠায়।
- **Tails OS:** USB থেকে চালানো Privacy-focused Live OS।
- **Whonix:** Gateway ও Workstation আলাদা করে Tor Traffic পরিচালনা করে।
- **Proxy:** Client ও Internet-এর মধ্যে Request Forward করে।
- **Proxy Chaining:** একাধিক Proxy-এর মধ্য দিয়ে Traffic পাঠায়।
- **GhostSwitch:** সাধারণ ধারণায় Proxy বা Privacy Connection Toggle করার Tool।

### References

- [Tor Project](https://www.torproject.org/)
- [Tails OS](https://tails.net/)
- [Whonix](https://www.whonix.org/)
- [ProxyChains-ng](https://github.com/rofl0r/proxychains-ng)
- [GOST Proxy & Tunnel](https://gost.run/en/)

