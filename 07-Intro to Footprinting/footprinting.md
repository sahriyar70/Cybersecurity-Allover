#  Cybersecurity Footprinting & Reconnaissance Guide

ফুটপ্রিন্টিং (Footprinting) বা রিকনেসান্স (Reconnaissance) হলো কোনোটার্গেট (Target System/Organization) সম্পর্কে আক্রমণ চালানোর আগে বা সিকিউরিটি অডিট করার আগে প্রয়োজনীয় তথ্য সংগ্রহ করার প্রক্রিয়া।

---

##  ১. Operating System (OS Footprinting)

টার্গেটের অপারেটিং সিস্টেম শনাক্ত করার মাধ্যমে সেই OS-এর পরিচিত ত্রুটি (Vulnerabilities) খুঁজে বের করা যায়।

* **Nmap OS Detection:**  
  `nmap -O <target-ip>`  
  *(টার্গেটের কার্নেল সংস্করণ ও OS টাইপ শনাক্ত করে)*
* **TTL (Time to Live) Analysis:**  
  `ping <target-ip>`  
  *(TTL ভ্যালু দেখে OS অনুমানের সাধারণ নিয়ম: Linux ≈ 64, Windows ≈ 128, Router/Cisco ≈ 255)*
* **WhatWeb Tool:**  
  `whatweb <url>`  
  *(ওয়েব সার্ভারের OS ও ব্যাকএন্ড টেকনোলজি প্রকাশ করে)*

---

##  ২. Firewall Footprinting

ফায়ারওয়ালের উপস্থিতি এবং ফায়ারওয়াল বাইপাসের উপায় বা ফিল্টারিং রুল পরীক্ষা করা।

* **WAF (Web Application Firewall) Detection:**  
  `wafw00f https://example.com`  
  *(Cloudflare, ModSecurity বা অন্যান্য WAF শনাক্ত করে)*
* **Nmap ACK Scan (Firewall Filtering Test):**  
  `nmap -sA <target-ip>`  
  *(পোর্ট ফিল্টার করা নাকি আনফিল্টারড তা নির্ধারণ করে)*
* **Nmap Firewall Bypass Techniques:**  
  `nmap -f <target-ip>` *(ফ্রেগমেন্টেড প্যাকেট পাঠায়)*  
  `nmap -D RND:10 <target-ip>` *(ডিকয় বা ফেক IP ব্যবহার করে নাম গোপন রাখে)*

---

##  ৩. IP Address Reconnaissance

টার্গেটের পাবলিক IP, IP Range এবং Subnet তথ্য সংগ্রহ।

* **nslookup / host:**  
  `nslookup example.com`  
  `host example.com`  
  *(ডোমেইনের সাথে সম্পর্কিত IP Address দেখায়)*
* **WHOIS Lookup:**  
  `whois <target-ip>`  
  *(IP এর মালিকানা, অর্গানাইজেশন এবং NetRange সংক্রান্ত তথ্য দেয়)*
* **Reverse IP Lookup:**  
  *(একটি নির্দিষ্ট IP-তে কতগুলো ওয়েবসাইট হোস্ট করা আছে তা খুঁজে বের করা)*

---

##  ৪. Network Mapping & Topology

নেটওয়ার্কের স্ট্রাকচার, রাউটিং পাথ এবং হোস্টসমূহ ম্যাপ করা।

* **Nmap Host Discovery (Ping Sweep):**  
  `nmap -sn 192.168.1.0/24`  
  *(নেটওয়ার্কে চালু থাকা সব ডিভাইসের তালিকা দেখায়)*
* **Traceroute / MTR:**  
  `traceroute example.com`  
  *(টার্গেট সার্ভারে পৌঁছানোর সমস্ত রাউটার ও নেটওয়ার্ক হপ দেখায়)*
* **Network Topology Mapping (Zenmap / Maltego):**  
  *(ভিজ্যুয়াল ম্যাপ ও গ্রাফ তৈরির মাধ্যমে টপোলজি বিশ্লেষণ)*

---

##  🥷 ৫. Security Configuration & Banner Grabbing

সার্ভারের ওপেন সার্ভিস ও সেগুলোর কনফিগারেশন সংক্রান্ত দুর্বলতা বের করা।

* **Banner Grabbing (Netcat / Telnet):**  
  `nc -vv <target-ip> 80`  
  `curl -I https://example.com`  
  *(সার্ভার কোন সফটওয়্যার ভার্সন রান করছে তা প্রকাশ করে, যেমন: Apache/2.4.41)*
* **Nmap Aggressive & Vulnerability Scan:**  
  `nmap -A -sV <target-ip>`  
  `nmap --script vuln <target-ip>`  
  *(ওপেন পোর্ট, সার্ভিস ভার্সন ও সিকিউরিটি ফাকঁতাল খোঁজ করে)*

---

##  ৬. Email ID & Password Leak Check (OSINT)

সামাজিক মাধ্যম ও ডাটা ব্রিচ (Data Breach) থেকে মেইল এবং পাসওয়ার্ড সংক্রান্ত তথ্য ফাঁস হওয়া পরীক্ষা।

* **TheHarvester:**  
  `theHarvester -d example.com -b google,linkedin`  
  *(সার্চ ইঞ্জিন থেকে টার্গেট ডোমেইনের ইমেইল ঠিকানা ও সাবডোমেইন কালেক্ট করে)*
* **HaveIBeenPwned API / OSINT Tools:**  
  *(পূর্বে ফাঁস হওয়া ডাটাবেজ বা ডার্কওয়েবে ইমেইল/পাসওয়ার্ডের উপস্থিতি যাচাই)*
* **Hunter.io / Phonebook.cz:**  
  *(অর্গানাইজেশনের কর্মচারীদের ইমেইল প্যাটার্ন খুঁজে বের করে)*

---

##  ৭. Server Configuration & Header Analysis

সার্ভার কনফিগারেশন মিসটেক বা ভুল সেটিংস পরীক্ষা করা।

* **HTTP Security Headers Inspection:**  
  `curl -sI https://example.com`  
  *(X-Frame-Options, CSP, HSTS ইত্যাদি সিকিউরিটি হেডার আছে কিনা তা দেখায়)*
* **Directory Enumeration (Gobuster / Dirb):**  
  `gobuster dir -u https://example.com -w /path/to/wordlist.txt`  
  *(গোপন ফোল্ডার ও কনফিগারেশন ফাইল খুঁজে বের করে)*
* **DNS Zone Transfer Test:**  
  `dig axfr @ns1.example.com example.com`  
  *(ডিএনএস কনফিগারেশন ভুলের কারণে পুরো সাবডোমেইন লিস্ট লিক হয় কিনা দেখে)*

---

##  ৮. URL & Subdomain Enumeration

টার্গেটের সমস্ত সাবডোমেইন ও হিডেন URL বের করা।

* **Sublist3r:**  
  `sublist3r -d example.com`  
  *(বিভিন্ন সার্চ ইঞ্জিন থেকে সাবডোমেইন খুঁজে আনে)*
* **Amass:**  
  `amass enum -d example.com`  
  *(অত্যন্ত শক্তিশালী ইন-ডেপথ ডিএনএস ও সাবডোমেইন এনুমারেশন টুল)*
* **Google Dorking for URLs:**  
  `site:example.com filetype:pdf`  
  `site:example.com inurl:admin`  
  *(গুগল সার্চ ট্রিকস দিয়ে সংবেদনশীল URL খুঁজে বের করা)*

---

##  ৯. VPN & Proxy Detection

টার্গেট কোনো ভিপিএন, প্রক্সি বা টর (Tor) নেটওয়ার্ক ব্যবহার করছে কিনা বা তাদের নিজস্ব VPN ইনফ্রাস্ট্রাকচার খুঁজে বের করা।

* **VPN Gateway Recon:**  
  `nmap -sU -p 500,4500 <target-ip>`  
  *(IPsec/IKE VPN সার্ভিস রানিং আছে কিনা চেক করে)*
* **Shodan Query for VPNs:**  
  `shodan search "port:1194" / "OpenVPN"`  
  *(ওপেন ভিপিএন ও প্রক্সি এনভায়রনমেন্ট শনাক্ত করে)*
* **IP Reputation Check:**  
  *(প্রক্সি/ভিপিএন ব্লকলিস্ট ডাটাবেজের সাহায্যে প্রক্সি শনাক্তকরণ)*

---

## ➕ ১০. অতিরিক্ত অন্যান্য গুরুত্বপূর্ণ ফুটপ্রিন্টিং টেকনিক (Bonus Categories)

###  Metadata Analysis (ExifTool)
ডকুমেন্ট ও ইমেজ থেকে সংবেদনশীল মেটাডেটা (ইউজারনেম, সফটওয়্যার ভার্সন, জিপিএস লোকেশন) বের করা।
```bash
exiftool sample.pdf