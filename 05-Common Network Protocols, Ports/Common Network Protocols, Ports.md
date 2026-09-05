# Common Network Protocols, Ports & Cybersecurity Reference Guide
 
**বিষয়:** Network Protocols, Default Port Numbers, Functions & Security Vulnerabilities

---

## Overview
নেটওয়ার্কিং, সিকিউরিটি অডিটিং, ফায়ারওয়াল রুল সেটআপ এবং এথিক্যাল হ্যাকিংয়ের (Port Scanning / Reconnaissance) জন্য কোন প্রোটোকল কোন পোর্টে কাজ করে এবং এর কাজ কী—তা জানা অত্যন্ত মৌলিক একটি বিষয়। এই নোটে পরিচিত প্রোটোকল, তাদের পোর্ট নম্বর, কাজের উদ্দেশ্য এবং সিকিউরিটি পয়েন্টগুলো চমৎকারভাবে সাজানো হয়েছে।

---

## Complete Protocols & Ports Master Table

| Protocol Name | Full Form (পূর্ণরূপ) | Default Port | Transport Protocol | Main Purpose (মূল কাজ) |
| :--- | :--- | :--- | :--- | :--- |
| **FTP** | File Transfer Protocol | 20 / 21 | TCP | ফাইল আপলোড ও ডাউনলোড করার জন্য |
| **SSH** | Secure Shell | 22 | TCP | সিকিউর এনক্রিপ্টেড রিমোট সার্ভার অ্যাক্সেস |
| **Telnet** | Teletype Network | 23 | TCP | প্লেনটেক্সট বা এনক্রিপশন ছাড়া রিমোট অ্যাক্সেস |
| **SMTP** | Simple Mail Transfer Protocol | 25 | TCP | ইমেইল এক সার্ভার থেকে অন্য সার্ভারে পাঠানো (Sending) |
| **DNS** | Domain Name System | 53 | TCP / UDP | ডোমেইন নেমকে (Domain Name) IP Address-এ রূপান্তর |
| **DHCP** | Dynamic Host Configuration Protocol | 67 / 68 | UDP | নেটওয়ার্কে স্বয়ংক্রিয়ভাবে IP অ্যাড্রেস বিতরণ করা |
| **HTTP** | Hypertext Transfer Protocol | 80 | TCP | অনিরাপদ ও এনক্রিপশন ছাড়া ওয়েব ব্রাউজিং |
| **POP3** | Post Office Protocol version 3 | 110 | TCP | ইমেইল সার্ভার থেকে লোকাল পিসিতে ইমেইল ডাউনলোড করা |
| **NTP** | Network Time Protocol | 123 | UDP | নেটওয়ার্কের সব ডিভাইসের ঘড়ি ও সময় সিঙ্ক করা |
| **IMAP** | Internet Message Access Protocol | 143 | TCP | সার্ভারে রেখে একাধিক ডিভাইস থেকে ইমেইল সিঙ্ক করে পড়া |
| **SNMP** | Simple Network Management Protocol | 161 / 162 | UDP | রাউটার, সুইচ বা সার্ভার মনিটরিং ও অ্যালার্ট গ্রহণ |
| **LDAP** | Lightweight Directory Access Protocol | 389 | TCP / UDP | ডিরেক্টরি সার্ভিস (যেমন: Active Directory) সার্চ করা |
| **HTTPS** | Hypertext Transfer Protocol Secure | 443 | TCP | SSL/TLS দিয়ে এনক্রিপ্টেড ও সিকিউর ওয়েব ব্রাউজিং |
| **SMB** | Server Message Block | 445 | TCP | উইন্ডোজ নেটওয়ার্কে ফাইল, ফোল্ডার ও প্রিন্টার শেয়ারিং |
| **LDAPS** | Lightweight Directory Access Protocol Secure | 636 | TCP | TLS এনক্রিপশনসহ সিকিউর ডিরেক্টরি সার্ভিস |
| **IMAPS** | Internet Message Access Protocol Secure | 993 | TCP | SSL/TLS এনক্রিপশনসহ সিকিউর IMAP ইমেইল অ্যাক্সেস |
| **POP3S** | Post Office Protocol 3 Secure | 995 | TCP | SSL/TLS এনক্রিপশনসহ সিকিউর POP3 ইমেইল অ্যাক্সেস |
| **RDP** | Remote Desktop Protocol | 3389 | TCP / UDP | উইন্ডোজের গ্রাফিক্যাল রিমোট ডেস্কটপ এক্সেস |

---

## Short Security Takeaways

1. **FTP, Telnet, HTTP, POP3, IMAP, LDAP:** এগুলো সব পুরানো প্রোটোকল যার ডেটা **Plaintext** আকারে যায়।
2. **SFTP/SSH, HTTPS, POP3S, IMAPS, LDAPS:** এগুলোতে SSL/TLS ব্যবহার করে **Encryption** যুক্ত করা হয়েছে যাতে হ্যাকাররা নেটওয়ার্ক স্নাইফ করে তথ্য বা পাসওয়ার্ড না চুরি করতে পারে।

## Detailed Breakdown & Cybersecurity Context

### 1. Remote Access Protocols
* **SSH (Port 22) vs Telnet (Port 23):**
  * **Telnet:** পুরোনো প্রোটোকল। এতে ব্যবহৃত পাসওয়ার্ড এবং কমান্ড সব প্লেনটেক্সট (Plaintext) আকারে নেটওয়ার্কে পরিভ্রমণ করে, যা খুব সহজে Sniffing/Wireshark দিয়ে চুরি করা যায়।
  * **SSH:** সব ধরনের কমিউনিকেশন এনক্রিপ্ট করে পাঠায়। রিমোট সার্ভার ম্যানেজমেন্টের জন্য সবসময় Telnet-এর বদলে SSH ব্যবহার করা উচিত।
* **RDP (Port 3389):**
  * উইন্ডোজ সার্ভার বা পিসিতে গ্রাফিক্যাল ইন্টারফেস (GUI) দিয়ে রিমোটলি কাজ করার সুযোগ দেয়।
  * **Security Concern:** Brute-force আক্রমণ এবং BlueKeep-এর মতো জনপ্রিয় ভ্যালনারেবিলিটির প্রধান টার্গেট। এটি ফায়ারওয়ালের মাধ্যমে কেবল সীমিত নির্দিষ্ট আইপির জন্য খোলা রাখা উচিত।

---

### 2. Web & Directory Protocols
* **HTTP (Port 80) vs HTTPS (Port 443):**
  * **HTTP:** কোনো এনক্রিপশন থাকে না (Man-in-the-Middle Attack সম্ভব)।
  * **HTTPS:** SSL/TLS সার্টিফিকেট ব্যবহার করে তথ্য এনক্রিপ্ট করে, যা ক্রেডিট কার্ড তথ্য, পাসওয়ার্ড সুরক্ষিত রাখে।
* **LDAP (Port 389) vs LDAPS (Port 636):**
  * Active Directory বা ইউজার ডেটাবেজ সার্চ করার জন্য ব্যবহৃত হয়। LDAPS সার্ভিসটি TLS ব্যবহার করে এনক্রিপ্টেড উপায়ে ক্রেডেনশিয়াল আদান-প্রদান করে।

---

### 3. Email Protocols
* **SMTP (Port 25):** মূলত এক মেইল সার্ভার থেকে অন্য মেইল সার্ভারে ইমেইল ট্রান্সমিশনের (Sending) জন্য ব্যবহৃত হয়।
* **POP3 (Port 110) vs IMAP (Port 143):**
  * **POP3:** ইমেইল সার্ভার থেকে মেসেজ লোকাল কম্পিউটারে ডাউনলোড করে নিয়ে আসে (সার্ভারে সাধারণত ইমেইল কপি থাকে না)।
  * **IMAP:** ইমেইল সার্ভারেই মেসেজ রেখে সিঙ্ক করে (ফোন ও পিসি দুই জায়গা থেকেই পড়া যায়)।
* **Encrypted Versions (IMAPS - 993, POP3S - 995):** নিরাপত্তাহীনতায় আক্রান্ত হওয়া ঠেকাতে এনক্রিপ্টেড ভার্সন ব্যবহার করা বাধ্যতামূলক।

---

### 4. File Sharing & Network Infrastructure Protocols
* **SMB (Port 445):**
  * উইন্ডোজ নেটওয়ার্কে ফাইল, ফোল্ডার এবং প্রিন্টার শেয়ার করতে ব্যবহৃত হয়।
  * **Security Threat:** ইতিহাসের অন্যতম বিপজ্জনক র‍্যানসামওয়্যার **WannaCry** এবং **EternalBlue** এই SMBv1-এর দুর্বলতাকে কাজে লাগিয়ে বিশ্বজুড়ে ছড়িয়ে পড়েছিল। কখনো এই পোর্টটি ইন্টারনেটের মুখে খোলা রাখা উচিত নয়।
* **DNS (Port 53):**
  * মানুষের বোধগম্য ডোমেইন নামকে আইপি ঠিকানায় রূপান্তর করে। এটি সাম্পাদক কাজের জন্য UDP এবং বড় জোন ট্রান্সফারের (Zone Transfer) জন্য TCP ব্যবহার করে।
* **SNMP (Port 161/162):**
  * রাউটার, সুইচ এবং সার্ভারের পারফরম্যান্স মনিটর করতে এটি ব্যবহৃত হয়। SNMPv1 এবং SNMPv2c-তে Community String প্লেনটেক্সটে যায়, তাই নিরাপদে ব্যবহারের জন্য **SNMPv3** এনক্রিপশন ব্যবহার করা জরুরি।

---

## Cybersecurity Assessment Rules of Thumb (Best Practices)

1. **Disable Plaintext Protocols:** আপনার নেটওয়ার্কে Telnet (23), HTTP (80), FTP (21) বন্ধ রেখে সেগুলোর সিকিউর এনক্রিপ্টেড বিকল্প (SSH, HTTPS, SFTP) ব্যবহার নিশ্চিত করুন।
2. **Restrict Critical Management Ports:** RDP (3389), SSH (22), SMB (445), এবং Database পোর্টগুলো কখনো সরাসরি পাবলিক ইন্টারনেটে ওপেন রাখবেন না। এগুলো অ্যাক্সেসের জন্য **VPN** ব্যবহার বাধ্যতামূলক করুন।
3. **Minimize Attack Surface:** ফায়ারওয়াল রুলসের সাহায্যে যেসব পোর্ট ব্যবহার হচ্ছে না, সেগুলো বন্ধ রাখা (Default Deny Policy) নিশ্চিত করুন।