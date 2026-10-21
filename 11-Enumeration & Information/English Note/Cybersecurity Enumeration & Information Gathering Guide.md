# Cybersecurity Enumeration & Information Gathering Guide

## 1. What is Enumeration?

Enumeration is the process of gathering detailed information about a target system, domain, website, or network during security reconnaissance.

**Common information collected:**
- Domain and DNS records
- IP addresses and subdomains
- Open ports and services
- Web Application Firewall (WAF)
- Publicly available certificates and directories

> **Note:** Perform enumeration only on systems you own or have permission to test.

---

## 2. Package Installation (`apt`)

`apt` is a package manager used in Debian-based Linux distributions, such as Kali Linux and Ubuntu.

```bash
sudo apt update
sudo apt install <tool_name>
```

---

## 3. Enumeration Tools & Commands

### A. WHOIS

**Purpose:** Retrieves publicly available domain registration information.

```bash
whois example.com
```

**Information:** Registrar, registration dates, name servers, and available registrant details.

### B. Host

**Purpose:** Performs DNS lookups and reverse DNS queries.

```bash
host example.com
host 93.184.216.34
```

### C. DNSrecon

**Purpose:** Discovers DNS records, subdomains, and potential DNS misconfigurations.

**Installation:**
```bash
sudo apt install dnsrecon
```

**Commands:**
```bash
dnsrecon -d example.com
dnsrecon -d example.com -t std
dnsrecon -d example.com -t axfr
```

**Important flags:**
- `-d` — Specify the target domain.
- `-t` — Specify the enumeration type.
- `-r` — Specify an IP range for reverse lookup.

**Note:** Zone transfer testing should only be performed with authorization.

### D. WAFW00F

**Purpose:** Identifies Web Application Firewalls (WAFs) protecting a website.

**Installation:**
```bash
sudo apt install wafw00f
```

**Commands:**
```bash
wafw00f https://example.com
wafw00f -a https://example.com
```

**Important flags:**
- `-a` — Check for all detectable WAFs.
- `-v` — Display verbose output.
- `-l` — List supported WAFs.

### E. Sublist3r

**Purpose:** Collects subdomains from supported public sources.

**Installation:**
```bash
sudo apt install sublist3r
```

**Commands:**
```bash
sublist3r -d example.com
sublist3r -d example.com -o subdomains.txt
sublist3r -d example.com -b
```

**Important flags:**
- `-d` — Specify the domain.
- `-b` — Enable brute-force discovery, if supported.
- `-p` — Specify ports to check, if supported.
- `-o` — Save results to a file.

### F. Certificate Transparency — crt.sh

**Purpose:** Finds publicly logged SSL/TLS certificates that may reveal subdomains.

Website: https://crt.sh

Search for a domain, such as `example.com`, and review matching certificate entries.

### G. Web Check

**Purpose:** Provides website information, including DNS records, HTTP security headers, TLS details, and other technical observations.

Website: https://web-check.xyz

Enter a website URL and review the available results. Some checks may be limited or unavailable.

### H. HTTrack

**Purpose:** Downloads website resources for offline browsing and authorized analysis.

**Installation:**
```bash
sudo apt install httrack
```

**Command:**
```bash
httrack https://example.com -O ./website-copy
```

**Important flag:**
- `-O` — Specify the output directory.

**Note:** HTTrack creates a local copy of accessible website resources; it does not necessarily retrieve the original server-side source code.

---

## 4. Wordlists

A **wordlist** is a text file containing candidate words, usernames, passwords, directory names, or subdomains. Each entry is usually stored on a separate line.

### A. Create a Custom Wordlist

```bash
nano custom_list.txt
```

Example contents:

```text
admin
login
test
dashboard
```

Save in Nano:
- `Ctrl + O` — Save
- `Enter` — Confirm filename
- `Ctrl + X` — Exit

### B. Common Wordlist Location

```bash
ls /usr/share/wordlists/
```

Some Kali Linux installations include `rockyou.txt`, which may require extraction before use.

### C. Generate Wordlists with Crunch

**Installation:**
```bash
sudo apt install crunch
```

**Syntax:**
```bash
crunch <min_length> <max_length> <characters> -o output.txt
```

**Example:**
```bash
crunch 4 6 abc123 -o mylist.txt
```

This generates combinations of 4–6 characters using `a`, `b`, `c`, `1`, `2`, and `3`.

**Warning:** Generated wordlists can consume substantial disk space. Use appropriate length and character limits.

---

## 5. Quick Reference

| Tool | Main Purpose |
|---|---|
| `whois` | Domain registration information |
| `host` | DNS and reverse DNS lookup |
| `dnsrecon` | DNS enumeration |
| `wafw00f` | WAF detection |
| `sublist3r` | Subdomain discovery |
| `crt.sh` | Certificate transparency search |
| `Web Check` | Website information gathering |
| `HTTrack` | Website mirroring |
| `Crunch` | Wordlist generation |

## 6. Best Practices

- Start with passive reconnaissance where possible.
- Verify discovered information before drawing conclusions.
- Avoid testing third-party systems without permission.
- Keep collected data secure and respect privacy.
- Use wordlists responsibly and avoid unauthorized password attacks.


