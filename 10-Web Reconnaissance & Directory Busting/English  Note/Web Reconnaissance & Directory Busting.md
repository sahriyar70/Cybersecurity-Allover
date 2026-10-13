# Web Reconnaissance & Directory Busting

## 1. Web Reconnaissance

Web Reconnaissance is the process of collecting information about a website or web application to identify its structure, technologies, and potential security weaknesses.

**Common Tools:**

* **HTTrack:** Downloads a website for offline browsing.
* **CeWL:** Generates custom wordlists by collecting words from website content.
* **Gobuster:** Discovers hidden directories, files, and subdomains.
* **FFUF:** Fuzzes web requests to discover directories, files, parameters, and virtual hosts.

## 2. HTTrack

**Purpose:** Creates a local copy of a website for offline analysis.

**Use Cases:**

* Website structure analysis
* Offline browsing
* Reviewing publicly accessible pages

**Note:** HTTrack does not copy every server-side function or database.

## 3. CeWL (Custom Word List Generator)

**Purpose:** Creates wordlists from words found on a target website.

**Command:**

```bash
cewl https://example.com -w wordlist.txt
```

* `-w`: Saves the wordlist to a file.
* Useful for authorized password-auditing and security assessments.

## 4. Directory Busting

Directory busting is the process of discovering hidden directories and files on a web server using wordlists.

**Common Tools:**

* Gobuster
* FFUF
* Dirsearch
* Feroxbuster

**Common Targets:**

* `/admin`
* `/backup`
* `/uploads`
* `/robots.txt`

## 5. Gobuster

**Purpose:** Discovers directories and files using wordlists.

**Command:**

```bash
gobuster dir -u https://example.com -w wordlist.txt
```

* `dir`: Directory/file discovery mode.
* `-u`: Target URL.
* `-w`: Wordlist path.

## 6. FFUF (Fuzz Faster U Fool)

**Purpose:** A web fuzzer used to discover hidden paths, files, parameters, and virtual hosts.

**Directory Discovery:**

```bash
ffuf -u https://example.com/FUZZ -w wordlist.txt
```

* `FUZZ`: Placeholder replaced by each wordlist entry.
* `-u`: Target URL.
* `-w`: Wordlist path.

**Parameter Discovery Example:**

```bash
ffuf -u "https://example.com/?FUZZ=test" -w params.txt
```

## 7. Key Differences

| Tool     | Main Purpose                 |
| -------- | ---------------------------- |
| HTTrack  | Website mirroring            |
| CeWL     | Custom wordlist generation   |
| Gobuster | Directory and file discovery |
| FFUF     | Flexible web fuzzing         |

**Important:** Use these tools only on systems you own or have explicit permission to test. Start with low request rates to avoid overloading the target.
