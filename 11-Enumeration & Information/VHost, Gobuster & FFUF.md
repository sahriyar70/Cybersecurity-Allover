# Web Enumeration: VHost, Gobuster & FFUF

## 1. VHost Enumeration

**VHost (Virtual Host)** হলো একই সার্ভারে একাধিক ডোমেইন বা ওয়েবসাইট হোস্ট করার ব্যবস্থা।

**VHost Enumeration** দিয়ে সার্ভারে কনফিগার করা অতিরিক্ত Virtual Host বা ওয়েবসাইট খুঁজে বের করার চেষ্টা করা হয়।

### Using Gobuster

```bash
gobuster vhost -u http://example.com -w subdomains.txt
```

**Important Flags:**
- `vhost` — Virtual Host Enumeration মোড।
- `-u` — টার্গেট URL।
- `-w` — Wordlist ফাইল।

### Using FFUF

```bash
ffuf -u http://example.com -H "Host: FUZZ.example.com" -w subdomains.txt
```

**Important Flags:**
- `-u` — টার্গেট URL।
- `-H` — HTTP Header নির্ধারণ করে।
- `FUZZ` — Wordlist-এর প্রতিটি শব্দ দিয়ে প্রতিস্থাপিত হয়।
- `-w` — Wordlist নির্ধারণ করে।

---

## 2. Gobuster

**Gobuster** হলো Go ভাষায় তৈরি একটি Enumeration টুল। এটি Directory, File, DNS Subdomain এবং Virtual Host খুঁজে বের করতে ব্যবহৃত হয়।

### Installation

```bash
sudo apt update
sudo apt install gobuster
```

### A. Directory & File Enumeration

```bash
gobuster dir -u https://example.com -w /path/to/wordlist.txt
```

**Important Flags:**
- `dir` — Directory/File Enumeration মোড।
- `-u` — টার্গেট URL।
- `-w` — Wordlist ফাইল।
- `-x` — নির্দিষ্ট File Extension পরীক্ষা করে।
- `-o` — ফলাফল ফাইলে সংরক্ষণ করে।
- `-t` — Concurrent Threads নির্ধারণ করে।

**Example:**

```bash
gobuster dir -u https://example.com -w wordlist.txt -x php,txt -o results.txt
```

### B. DNS Subdomain Enumeration

```bash
gobuster dns -d example.com -w subdomains.txt
```

**Important Flags:**
- `dns` — DNS Enumeration মোড।
- `-d` — টার্গেট ডোমেইন।
- `-w` — Subdomain Wordlist।

### C. Virtual Host Enumeration

```bash
gobuster vhost -u http://example.com -w subdomains.txt
```

---

## 3. FFUF (Fuzz Faster U Fool)

**FFUF** হলো একটি দ্রুত Web Fuzzing টুল। এটি Directory, File, Virtual Host, GET/POST Parameter এবং অন্যান্য ইনপুট পরীক্ষা করতে ব্যবহৃত হয়।

### Installation

```bash
sudo apt update
sudo apt install ffuf
```

### A. Directory Enumeration

```bash
ffuf -u https://example.com/FUZZ -w wordlist.txt
```

### B. File Extension Discovery

```bash
ffuf -u https://example.com/FUZZ -w wordlist.txt -e .php,.txt,.html
```

**Important Flags:**
- `-u` — টার্গেট URL।
- `FUZZ` — Wordlist-এর শব্দ বসানোর জায়গা।
- `-w` — Wordlist নির্ধারণ করে।
- `-e` — অতিরিক্ত File Extension পরীক্ষা করে।
- `-mc` — নির্দিষ্ট HTTP Status Code দেখায়।
- `-fc` — নির্দিষ্ট HTTP Status Code বাদ দেয়।
- `-fs` — নির্দিষ্ট Response Size বাদ দেয়।
- `-o` — ফলাফল সংরক্ষণ করে।

### C. GET Parameter Fuzzing

```bash
ffuf -u "https://example.com/page?FUZZ=test" -w parameters.txt
```

### D. POST Parameter Fuzzing

```bash
ffuf -X POST -u https://example.com/login \
-d "username=FUZZ&password=test" \
-H "Content-Type: application/x-www-form-urlencoded" \
-w usernames.txt
```

**নোট:** POST Fuzzing কেবল অনুমোদিত টেস্টিং পরিবেশে করবে। বাস্তব লগইন সিস্টেমে অনুমতি ছাড়া পরীক্ষা করবে না।

---

## 4. Gobuster vs FFUF

| বৈশিষ্ট্য | Gobuster | FFUF |
|---|---|---|
| Directory Enumeration | হ্যাঁ | হ্যাঁ |
| DNS Subdomain Enumeration | হ্যাঁ | কাস্টমভাবে সম্ভব |
| VHost Enumeration | হ্যাঁ | হ্যাঁ |
| Parameter Fuzzing | সীমিত | প্রধান ব্যবহারগুলোর একটি |
| File Extension Testing | `-x` | `-e` |
| প্রধান সুবিধা | সহজ ও নির্দিষ্ট Enumeration | নমনীয় ও দ্রুত Fuzzing |

## 5. গুরুত্বপূর্ণ ধারণা

- **VHost Enumeration:** একই সার্ভারে থাকা অতিরিক্ত Virtual Host খোঁজা।
- **Directory Enumeration:** ওয়েব সার্ভারের সম্ভাব্য Directory ও File খোঁজা।
- **DNS Enumeration:** ডোমেইনের DNS রেকর্ড ও Subdomain সম্পর্কে তথ্য সংগ্রহ।
- **Fuzzing:** বিভিন্ন ইনপুট দিয়ে অ্যাপ্লিকেশনের প্রতিক্রিয়া পরীক্ষা করা।
- **Wordlist:** পরীক্ষার জন্য ব্যবহৃত সম্ভাব্য নাম, পাথ বা প্যারামিটারের তালিকা।

**Security Note:** নিজের Lab, অনুমোদিত Target অথবা ইচ্ছাকৃতভাবে তৈরি Practice Environment-এ এসব টুল ব্যবহার করবেন।
