# Metasploit Framework – Complete Notes

Metasploit Framework হলো একটি Penetration Testing Framework। এটি দিয়ে Vulnerability Assessment, Exploit Validation, Payload Testing এবং Security Testing করা হয়।

## 1. Metasploit Components

| Component | কাজ |
|---|---|
| MSFConsole | Main Command-Line Interface |
| MSFVenom | Payload তৈরি ও Format পরিবর্তন |
| Exploits | Vulnerability কাজে লাগানো |
| Payloads | Exploit সফল হলে Action সম্পাদন |
| Encoders | Payload Encoding |
| Auxiliary | Scanning, Enumeration ও Testing |
| NOPs | No Operation Instruction |
| Post | Exploitation-এর পর Security Assessment |
| Evasion | Detection Mechanism Testing |
| Plugins | Framework-এর Functionality বাড়ানো |
| Meterpreter | Advanced Payload Interface |
| Multi/Handler | Incoming Payload Connection গ্রহণ |
| Sessions | Active Connection পরিচালনা |
| Database | Hosts, Services ও Vulnerability সংরক্ষণ |

---

## 2. MSFConsole

MSFConsole হলো Metasploit-এর Main Interface। এখান থেকে Module Search, Select এবং Configure করা হয়।

### Start Metasploit

```bash
msfconsole
```

### Basic Commands

```bash
help
version
banner
search <name>
info <module>
use <module>
show options
show payloads
show targets
back
exit
```

### Example

```bash
search type:auxiliary
info auxiliary/scanner/portscan/tcp
use auxiliary/scanner/portscan/tcp
show options
```

---

## 3. Exploits

Exploit হলো এমন একটি Code বা Module, যা কোনো System-এর Vulnerability কাজে লাগিয়ে Security Testing করে।

**উদ্দেশ্য:** কোনো Vulnerability বাস্তবে Exploitable কি না যাচাই করা।

### Commands

```bash
search type:exploit
search name:ms17_010
show exploits
info <exploit_name>
```

---

## 4. Payloads

Payload হলো Exploit সফল হওয়ার পর Target System-এ যে Action সম্পাদন করা হয়।

### Payload Types

| Type | কাজ |
|---|---|
| Singles | সম্পূর্ণ Payload একসঙ্গে কাজ করে |
| Stagers | ছোট Payload দিয়ে Connection তৈরি করে |
| Stages | Connection-এর পর বড় Payload পাঠায় |

### Common Payload Names

```text
windows/x64/meterpreter/reverse_tcp
linux/x64/meterpreter/reverse_tcp
windows/x64/shell/reverse_tcp
generic/shell_reverse_tcp
```

### Reverse vs Bind Payload

- Reverse: Target থেকে Testing Machine-এর দিকে Connection আসে।
- Bind: Target-এর Listening Port-এ Connection গ্রহণ করা হয়।

---

## 5. MSFVenom

MSFVenom হলো Payload তৈরি, Encode এবং বিভিন্ন File Format-এ Export করার Tool।

এটি পুরোনো `msfpayload` ও `msfencode` Tool-এর বিকল্প।

### Basic Commands

```bash
msfvenom --help
msfvenom -l payloads
msfvenom -l formats
msfvenom -l encoders
```

### Important Options

| Option | কাজ |
|---|---|
| `-p` | Payload নির্বাচন |
| `-f` | Output Format |
| `-o` | Output File |
| `-a` | Architecture |
| `-e` | Encoder নির্বাচন |
| `-i` | Encoding Iterations |
| `-l` | Available List |

### General Syntax

```bash
msfvenom -p <payload> -f <format> -o <output_file>
```

---

## 6. Encoders

Encoder Payload-এর Data একটি নির্দিষ্ট Encoding Format-এ পরিবর্তন করে।

**উদ্দেশ্য:**
- Payload Encoding।
- Character ও Format Constraint পূরণ।
- Legacy Exploit Compatibility Testing।

### Commands

```bash
msfvenom -l encoders
```

```bash
info encoder/x86/shikata_ga_nai
```

**Note:** Encoding মানেই Encryption নয় এবং এটি Antivirus Detection এড়ানোর নিশ্চয়তা দেয় না।

---

## 7. Auxiliary Modules

Auxiliary Module দিয়ে Exploitation ছাড়াই বিভিন্ন Security Testing করা যায়।

### Main Categories

| Module | কাজ |
|---|---|
| Scanner | Port ও Service Scanning |
| Admin | Administration Testing |
| Gather | Information Gathering |
| Fuzzers | Input Handling Testing |
| Dos | Denial-of-Service Testing |
| Server | Server-related Testing |

### Commands

```bash
search type:auxiliary
show auxiliary
```

### Port Scanner Module

```bash
search type:auxiliary portscan
info auxiliary/scanner/portscan/tcp
```

---

## 8. Listeners & Multi/Handler

Listener হলো এমন একটি Service, যা নির্দিষ্ট Network Connection গ্রহণ করার জন্য অপেক্ষা করে।

`multi/handler` বিভিন্ন ধরনের Payload Connection Handle করতে পারে।

### Module

```bash
use exploit/multi/handler
show options
info
```

### Important Terms

| Term | কাজ |
|---|---|
| LHOST | Local Host IP |
| LPORT | Local Listening Port |
| RHOST | Remote Target IP |
| RPORT | Remote Service Port |

---

## 9. Meterpreter

Meterpreter হলো Metasploit-এর Advanced Payload Interface। এটি সাধারণ Shell-এর তুলনায় বেশি Functionality প্রদান করে।

### Important Commands

```bash
help
sysinfo
getuid
pwd
ls
ps
ipconfig
ifconfig
background
exit
```

| Command | কাজ |
|---|---|
| `sysinfo` | System Information |
| `getuid` | Current User |
| `pwd` | Current Directory |
| `ls` | Directory Contents |
| `ps` | Running Processes |
| `ipconfig` | Network Information |
| `background` | Session Background |
| `exit` | Session থেকে বের হওয়া |

---

## 10. Post Exploitation Modules

Post Module Exploitation-এর পর System-এর Security Condition ও Configuration পরীক্ষা করতে ব্যবহৃত হয়।

**উদ্দেশ্য:**
- System Information সংগ্রহ।
- User ও Group Information পরীক্ষা।
- Network Configuration পরীক্ষা।
- Security Assessment।

### Commands

```bash
search type:post
show post
info post/multi/gather/env
```

---

## 11. NOPs (No Operation)

NOP-এর পূর্ণরূপ No Operation।

এটি এমন Instruction, যা কার্যকরভাবে কোনো পরিবর্তন করে না।

**উদ্দেশ্য:**
- Exploit-এর Payload Layout তৈরি।
- Buffer Alignment।
- Exploit Compatibility Testing।

### Commands

```bash
search type:nop
show nops
```

---

## 12. Evasion Modules

Evasion Module নির্দিষ্ট Security Detection Mechanism-এর বিরুদ্ধে Payload Testing-এর জন্য ব্যবহৃত হয়।

**উদ্দেশ্য:**
- Security Detection পরীক্ষা।
- Defensive Tool-এর কার্যকারিতা যাচাই।
- Authorized Red Team Assessment।

### Commands

```bash
search type:evasion
```

**Note:** Encoder এবং Evasion এক জিনিস নয়।

---

## 13. Plugins

Plugin Metasploit-এর Functionality বাড়ায় এবং অতিরিক্ত Feature যুক্ত করে।

### Commands

```bash
load <plugin_name>
```

---

## 14. Database & Workspace

Database Scan Results, Hosts, Services এবং Vulnerability Information সংরক্ষণ করে।

### Database Status

```bash
db_status
```

### Workspace Management

```bash
workspace
workspace -a Lab
workspace Lab
workspace -d Lab
```

### Database Commands

```bash
hosts
services
vulns
creds
```

| Command | কাজ |
|---|---|
| `hosts` | Discovered Hosts |
| `services` | Discovered Services |
| `vulns` | Vulnerability Records |
| `creds` | Stored Credentials |

---

## 15. Sessions Management

Session হলো Testing-এর সময় তৈরি হওয়া Active Connection।

### Commands

```bash
sessions
sessions -l
sessions -i <session_id>
sessions -K
```

| Command | কাজ |
|---|---|
| `sessions` | Session Information |
| `sessions -l` | Active Session List |
| `sessions -i` | নির্দিষ্ট Session-এ প্রবেশ |
| `sessions -K` | সব Session বন্ধ |

---

## 16. Important Metasploit Commands

| Command | কাজ |
|---|---|
| `msfconsole` | Metasploit চালু |
| `msfvenom --help` | MSFVenom Help |
| `search` | Module Search |
| `use` | Module Select |
| `info` | Module Details |
| `show options` | Configuration Options |
| `show payloads` | Payload List |
| `show exploits` | Exploit List |
| `show auxiliary` | Auxiliary List |
| `show post` | Post Modules |
| `show nops` | NOP Modules |
| `check` | Supported Module-এ Vulnerability Check |
| `back` | Module থেকে ফিরে আসা |
| `sessions -l` | Active Sessions |
| `db_status` | Database Status |
| `workspace` | Workspace List |
| `hosts` | Host Information |
| `services` | Service Information |
| `vulns` | Vulnerability Information |
| `exit` | Exit |

---

## 17. Metasploit Workflow

সাধারণ Penetration Testing Workflow:

1. **Information Gathering** – Target সম্পর্কে তথ্য সংগ্রহ।
2. **Scanning** – Open Ports ও Running Services শনাক্ত।
3. **Enumeration** – Service ও Version সম্পর্কে বিস্তারিত তথ্য।
4. **Vulnerability Assessment** – Security Weakness শনাক্ত।
5. **Exploit Validation** – Lab-এ Vulnerability যাচাই।
6. **Payload Testing** – Payload Behaviour পরীক্ষা।
7. **Session Management** – অনুমোদিত Session পরিচালনা।
8. **Post Assessment** – System Security Impact পরীক্ষা।
9. **Reporting** – Vulnerability ও Remediation Report তৈরি।

---

## 18. Important Terms

| Term | সহজ অর্থ |
|---|---|
| Framework | বিভিন্ন Tool ও Module-এর সমন্বয় |
| Module | নির্দিষ্ট কাজের Component |
| Exploit | Vulnerability কাজে লাগানোর Code |
| Payload | Exploit-এর পরের Action |
| Encoder | Payload Encoding Tool |
| Auxiliary | Scanning ও Testing Module |
| Listener | Connection গ্রহণকারী Service |
| Meterpreter | Advanced Session Interface |
| Post | Exploitation-এর পরের Testing |
| NOP | No Operation Instruction |
| Session | Active Connection |
| LHOST | Local Host Address |
| LPORT | Local Listening Port |
| RHOST | Remote Host Address |
| RPORT | Remote Service Port |

---

## 19. Important Notes

- Exploit এবং Payload এক জিনিস নয়।
- MSFConsole হলো Metasploit-এর Main Interface।
- MSFVenom হলো Payload Generation Tool।
- Auxiliary Module দিয়ে Exploitation ছাড়াই Testing করা যায়।
- Meterpreter সাধারণ Shell-এর চেয়ে বেশি Feature দেয়।
- Encoder মানেই Payload নিরাপদ বা Undetectable নয়।
- সবসময় নিজের Lab অথবা অনুমোদিত System-এ Testing করবে।

**Metasploit-এর মূল উদ্দেশ্য:** Vulnerability খুঁজে বের করা, Security Weakness যাচাই করা এবং System-এর Security উন্নত করতে সাহায্য করা।