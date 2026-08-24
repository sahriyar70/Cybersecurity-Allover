# কম্পিউটার নেটওয়ার্কিং ফান্ডামেন্টালস (Cybersecurity Perspective)

**বিষয়:** Computer Networks, Devices, IP/MAC, Architecture & Protocols

---

## Overview
সাইবার সিকিউরিটির ভিত্তি হলো নেটওয়ার্কিং। নেটওয়ার্ক কীভাবে কাজ করে, ডেটা কীভাবে এক জায়গা থেকে অন্য জায়গায় ভ্রমণ করে এবং কী কী প্রোটোকল ব্যবহৃত হয়—তা না জানলে নেটওয়ার্ক অ্যাটাক শনাক্ত করা বা ডিফেন্ড করা অসম্ভব। এই নোটে সাইবার সিকিউরিটি ফোকাসড নেটওয়ার্কিং বিষয়াবলি বিস্তারিত আলোচনা করা হলো।

---

## What is Networking?
একাধিক ডিজিটাল ডিভাইস (যেমন: কম্পিউটার, সার্ভার, রাউটার) যখন ডেটা ও রিসোর্স শেয়ার করার উদ্দেশ্যে তারের মাধ্যমে (Wired) বা তারহীন উপায়ে (Wireless) সংযুক্ত হয়, তখন তাকে **কম্পিউটার নেটওয়ার্ক** বলে।

---

## Hardware & Networking Devices

1. **NIC (Network Interface Card):** ডিভাইসের ফিজিক্যাল কার্ড যা তাকে নেটওয়ার্কে যুক্ত হতে সাহায্য করে। এতে ইউনিক MAC অ্যাড্রেস থাকে।
2. **Switch (Layer 2 Device):** লোকাল নেটওয়ার্কে (LAN) ডিভাইসগুলোকে যুক্ত করে। এটি **MAC Address Table** মেইনটেইন করে নির্দিষ্ট ডিভাইসে ডেটা ফ্রেম পাঠায়।
3. **Router (Layer 3 Device):** বিভিন্ন নেটওয়ার্ককে (যেমন: LAN ও WAN) যুক্ত করে। এটি **IP Address** এবং Routing Table ব্যবহার করে সেরা পাথ দিয়ে ডেটা প্যাকেট পাঠায়।
4. **Firewall:** নেটওয়ার্কের ট্রাফিক মনিটর ও ফিল্টার করার প্রধান সুরক্ষাবলয়। এটি প্রি-ডিফাইন্ড সিকিউরিটি রুলসের ওপর ভিত্তি করে ট্রাফিক Allow বা Block করে।
5. **Access Point (AP):** তারযুক্ত নেটওয়ার্ককে ওয়্যারলেস (Wi-Fi) নেটওয়ার্কে রূপান্তর করে।

---

## MAC Address vs IP Address

| বিষয় | MAC Address | IP Address |
| :--- | :--- | :--- |
| **পূর্ণরূপ** | Media Access Control | Internet Protocol |
| **সংজ্ঞা** | ডিভাইসের স্থায়ী ফিজিক্যাল বা হার্ডওয়্যার ঠিকানা। | নেটওয়ার্কে ডিভাইসের পরিবর্তনযোগ্য লজিক্যাল ঠিকানা। |
| **ওএসআই লেয়ার** | Data Link Layer (Layer 2) | Network Layer (Layer 3) |
| **ফরম্যাট** | 48-bit (যেমন: `00:1A:2B:3C:4D:5E`) | IPv4 (32-bit: `192.168.1.1`) / IPv6 (128-bit) |
| **সাইবার গুরুত্ব** | MAC Spoofing শনাক্তকরণ ও Port Security | Firewall Rules, IP Tracking, Threat Analysis |

---

## Network Types: LAN, WAN, WLAN

* **LAN (Local Area Network):** ছোট ভৌগোলিক সীমানায় (যেমন: বাসা বা অফিস) থাকা নিজস্ব নেটওয়ার্ক। হাই-স্পিড ও কম লাটেন্সিযুক্ত।
* **WLAN (Wireless LAN):** ওয়াই-ফাই (Wi-Fi) প্রযুক্তির সাহায্যে গঠিত তারহীন লোকাল নেটওয়ার্ক (IEEE 802.11 স্ট্যান্ডার্ড)।
* **WAN (Wide Area Network):** বিশাল ভৌগোলিক এলাকা (যেমন: দুটি শহর বা দেশ) জুড়ে গঠিত নেটওয়ার্ক। সবচেয়ে বড় WAN-এর উদাহরণ হলো **ইন্টারনেট**।

---

## NAT vs PAT (Network Address Translation)

পাবলিক আইপি (IPv4) বাঁচানো এবং ইন্টারনাল নেটওয়ার্ককে সুরক্ষিত রাখার জন্য NAT ব্যবহৃত হয়।

* **NAT (Static/Dynamic NAT):** প্রাইভেট আইপিকে পাবলিক আইপিতে রূপান্তর করে। সাধারণত ১টি প্রাইভেট আইপির জন্য ১টি পাবলিক আইপি ম্যাপ করা হয়।
* **PAT (Port Address Translation / NAT Overload):** একাধিক প্রাইভেট আইপিকে **একটি মাত্র পাবলিক আইপি** এবং **আলাদা আলাদা সোর্স পোর্ট** ব্যবহার করে ইন্টারনেটে অ্যাক্সেস দেয়।
* **সিকিউরিটি গুরুত্ব:** বাইরের ইন্টারনেট থেকে কেউ সরাসরি অভ্যন্তরীণ (Private) আইপিতে আক্রমণ করতে পারে না, ফলে এটি নিরাপত্তার প্রাথমিক ঢাল হিসেবে কাজ করে।

---

## OSI vs TCP/IP Model (Cybersecurity Core)

নেটওয়ার্ক বোঝার জন্য ওএসআই Model সবচেয়ে গুরুত্বপূর্ণ। প্রতিটি লেয়ারে আলাদা অ্যাটাক ও সিকিউরিটি মেকানিজম থাকে:

OSI Layer           Security Focus & Attacks
┌──────────────┐   ┌─────────────────────────────────────────┐
│ Application  │ ──│ HTTP, DNS | SQLi, XSS, Phishing         │
│ Presentation │ ──│ SSL/TLS Encryption, Data Encoding       │
│ Session      │ ──│ Session Hijacking, Token Management     │
│ Transport    │ ──│ TCP/UDP | Port Scanning, SYN Flood     │
│ Network      │ ──│ IP, Router | IP Spoofing, ICMP Flood   │
│ Data Link    │ ──│ MAC, Switch | ARP Spoofing, MAC Flooding│
│ Physical     │ ──│ Cables | Wiretapping, Physical Damage   │
└──────────────┘   └─────────────────────────────────────────┘

## Important Protocols & Port Numbers (Must-Know)

সাইবার সিকিউরিটিতে কোন পোর্টে কোন প্রোটোকল কাজ করে তা জানা অত্যন্ত জরুরি:

| Port | Protocol | বিবরণ ও সিকিউরিটি নোট |
| :--- | :--- | :--- |
| **21** | FTP | ফাইল ট্রান্সফার (Plaintext - অনিরাপদ) |
| **22** | SSH | সিকিউর রিমোট লগইন (Encrypted) |
| **23** | Telnet | রিমোট লগইন (Unencrypted - সহজে প্যাকট স্নাইফ করা যায়) |
| **53** | DNS | ডোমেন নেম থেকে IP রেজোলিউশন (DNS Spoofing Target) |
| **80** | HTTP | এনক্রিপশন ছাড়া ওয়েবসাইটের ডেটা আদান-প্রদান |
| **443** | HTTPS | TLS/SSL এনক্রিপশনসহ সিকিউর ওয়েব ট্রাফিক |
| **67/68** | DHCP | স্বয়ংক্রিয়ভাবে IP বিতরণ (DHCP Starvation Attack Target) |

---

## Key Security Networking Concepts

### ১. ARP (Address Resolution Protocol) & ARP Spoofing
* **কাজ:** IP Address থেকে MAC Address বের করা।
* **আক্রমণ:** হ্যাকার ভুয়া ARP বার্তা পাঠিয়ে ক্লায়েন্ট ও রাউটারের মাঝে নিজেকে বসিয়ে দেয় (Man-in-the-Middle / MITM Attack)।

### ২. DNS (Domain Name System) Security
* **কাজ:** Domain Name (যেমন: `google.com`) কে IP Address-এ রূপান্তর করা।
* **ঝুঁকি:** DNS Poisoning বা Hijacking-এর মাধ্যমে আসল সাইটের বদলে ভুয়া ফিশিং সাইটে ট্রাফিক রিডাইরেক্ট করা হয়।

### ৩. TCP 3-Way Handshake
কানেকশন তৈরির প্রক্রিয়া: `SYN` ➔ `SYN-ACK` ➔ `ACK`
* **আক্রমণ (SYN Flood):** হ্যাকার প্রচুর পরিমাণে `SYN` প্যাকেট পাঠিয়ে কিন্তু `ACK` না দিয়ে সার্ভারের কানেকশন মেমোরি ফুল করে ফেলে (DDoS Attack)।

### ৪. Network Segmentation & VLAN
নেটওয়ার্ককে ছোট ছোট অংশে ভাগ করা যেন কোনো একটি ডিভাইস হ্যাক হলেও পুরো অফিসে আক্রমণ ছড়িয়ে না পড়তে পারে (Blast Radius কমানো)।

---

## Key Takeaways
1. Layer 2-এ থাকে **MAC Address** এবং Layer 3-এ থাকে **IP Address**।
2. **PAT** একটি পাবলিক আইপি দিয়ে একটি পুরো অফিসের ইন্টারনেট অ্যাক্সেস দেয়।
3. সিকিউরিটির জন্য সবসময় Plaintext প্রোটোকলের (HTTP, Telnet) পরিবর্তে Encrypted ভার্সন (HTTPS, SSH) ব্যবহার করতে হবে।
4. **Network Segmentation** এবং **Firewall Control Rules** সাইবার আক্রমণের বিস্তার রোধ করে।