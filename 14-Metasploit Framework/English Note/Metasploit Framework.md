# Metasploit Framework – Complete Notes

Metasploit Framework is an open-source Penetration Testing Framework used for Vulnerability Assessment, Exploit Validation, Payload Testing, and Security Testing.

## 1. Metasploit Components

| Component | Purpose |
|---|---|
| MSFConsole | Main Command-Line Interface |
| MSFVenom | Payload Generation and Format Conversion |
| Exploits | Exploit System Vulnerabilities |
| Payloads | Actions performed after successful exploitation |
| Encoders | Payload Encoding |
| Auxiliary | Scanning, Enumeration, and Testing |
| NOPs | No Operation Instructions |
| Post | Post-Exploitation Security Assessment |
| Evasion | Security Detection Testing |
| Plugins | Extend Framework Functionality |
| Meterpreter | Advanced Payload Interface |
| Multi/Handler | Handles Incoming Payload Connections |
| Sessions | Manage Active Connections |
| Database | Store Hosts, Services, and Vulnerability Information |

---

## 2. MSFConsole

MSFConsole is the main command-line interface of Metasploit. It allows users to search, select, and configure modules.

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

An Exploit is a piece of code or module that takes advantage of a system vulnerability for security testing.

**Purpose:** To verify whether a vulnerability is exploitable.

### Commands

```bash
search type:exploit
search name:ms17_010
show exploits
info <exploit_name>
```

---

## 4. Payloads

A Payload is the action or code executed on a target system after a successful exploit.

### Payload Types

| Type | Purpose |
|---|---|
| Singles | Complete payload that works independently |
| Stagers | Small payload used to establish a connection |
| Stages | Larger payload delivered after the connection is established |

### Common Payload Names

```text
windows/x64/meterpreter/reverse_tcp
linux/x64/meterpreter/reverse_tcp
windows/x64/shell/reverse_tcp
generic/shell_reverse_tcp
```

### Reverse vs Bind Payload

- Reverse: The target initiates a connection to the testing machine.
- Bind: The target listens on a port and accepts an incoming connection.

---

## 5. MSFVenom

MSFVenom is a tool used to generate, encode, and export payloads into different file formats.

It replaced the older `msfpayload` and `msfencode` tools.

### Basic Commands

```bash
msfvenom --help
msfvenom -l payloads
msfvenom -l formats
msfvenom -l encoders
```

### Important Options

| Option | Purpose |
|---|---|
| `-p` | Select Payload |
| `-f` | Specify Output Format |
| `-o` | Specify Output File |
| `-a` | Specify Architecture |
| `-e` | Select Encoder |
| `-i` | Number of Encoding Iterations |
| `-l` | List Available Options |

### General Syntax

```bash
msfvenom -p <payload> -f <format> -o <output_file>
```

---

## 6. Encoders

An Encoder transforms payload data into a specific encoded format.

**Purpose:**

- Encode payload data.
- Meet character and format constraints.
- Test compatibility with legacy exploits.

### Commands

```bash
msfvenom -l encoders
```

```bash
info encoder/x86/shikata_ga_nai
```

**Note:** Encoding is not the same as encryption and does not guarantee bypassing antivirus detection.

---

## 7. Auxiliary Modules

Auxiliary Modules perform various security testing activities without directly exploiting vulnerabilities.

### Main Categories

| Module | Purpose |
|---|---|
| Scanner | Port and Service Scanning |
| Admin | Administration Testing |
| Gather | Information Gathering |
| Fuzzers | Input Handling Testing |
| DoS | Denial-of-Service Testing |
| Server | Server-Related Testing |

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

A Listener is a service that waits for incoming network connections.

`multi/handler` can handle connections from different types of payloads.

### Module

```bash
use exploit/multi/handler
show options
info
```

### Important Terms

| Term | Purpose |
|---|---|
| LHOST | Local Host IP Address |
| LPORT | Local Listening Port |
| RHOST | Remote Target IP Address |
| RPORT | Remote Service Port |

---

## 9. Meterpreter

Meterpreter is an advanced payload interface in Metasploit. It provides more functionality than a standard command shell.

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

| Command | Purpose |
|---|---|
| `sysinfo` | Display System Information |
| `getuid` | Display Current User |
| `pwd` | Show Current Directory |
| `ls` | List Directory Contents |
| `ps` | Show Running Processes |
| `ipconfig` | Display Network Information |
| `background` | Send Session to Background |
| `exit` | Exit the Session |

---

## 10. Post-Exploitation Modules

Post Modules are used to assess system security and configuration after exploitation.

**Purpose:**

- Collect System Information.
- Examine User and Group Information.
- Check Network Configuration.
- Perform Security Assessment.

### Commands

```bash
search type:post
show post
info post/multi/gather/env
```

---

## 11. NOPs (No Operation)

NOP stands for No Operation.

It is an instruction that performs no meaningful operation or changes to the system state.

**Purpose:**

- Construct Exploit Payload Layouts.
- Buffer Alignment.
- Exploit Compatibility Testing.

### Commands

```bash
search type:nop
show nops
```

---

## 12. Evasion Modules

Evasion Modules are used to test payload behavior against specific security detection mechanisms.

**Purpose:**

- Test Security Detection.
- Evaluate Defensive Tools.
- Perform Authorized Red Team Assessments.

### Commands

```bash
search type:evasion
```

**Note:** Encoders and Evasion Modules are not the same.

---

## 13. Plugins

Plugins extend Metasploit functionality by adding extra features and integrations.

### Commands

```bash
load <plugin_name>
```

---

## 14. Database & Workspace

The Metasploit Database stores scan results, hosts, services, and vulnerability information.

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

| Command | Purpose |
|---|---|
| `hosts` | Display Discovered Hosts |
| `services` | Display Discovered Services |
| `vulns` | Display Vulnerability Records |
| `creds` | Display Stored Credentials |

---

## 15. Sessions Management

A Session is an active connection established during penetration testing.

### Commands

```bash
sessions
sessions -l
sessions -i <session_id>
sessions -K
```

| Command | Purpose |
|---|---|
| `sessions` | Display Session Information |
| `sessions -l` | List Active Sessions |
| `sessions -i` | Interact with a Specific Session |
| `sessions -K` | Terminate All Sessions |

---

## 16. Important Metasploit Commands

| Command | Purpose |
|---|---|
| `msfconsole` | Start Metasploit |
| `msfvenom --help` | Display MSFVenom Help |
| `search` | Search Modules |
| `use` | Select a Module |
| `info` | Display Module Details |
| `show options` | Display Configuration Options |
| `show payloads` | List Available Payloads |
| `show exploits` | List Exploit Modules |
| `show auxiliary` | List Auxiliary Modules |
| `show post` | List Post Modules |
| `show nops` | List NOP Modules |
| `check` | Check Vulnerability on Supported Modules |
| `back` | Return from Current Module |
| `sessions -l` | List Active Sessions |
| `db_status` | Check Database Status |
| `workspace` | Display Workspaces |
| `hosts` | Display Host Information |
| `services` | Display Service Information |
| `vulns` | Display Vulnerability Information |
| `exit` | Exit Metasploit |

---

## 17. Metasploit Workflow

A general Penetration Testing Workflow:

1. **Information Gathering** – Collect information about the target.
2. **Scanning** – Identify open ports and running services.
3. **Enumeration** – Gather detailed service and version information.
4. **Vulnerability Assessment** – Identify security weaknesses.
5. **Exploit Validation** – Verify vulnerabilities in a lab environment.
6. **Payload Testing** – Test payload behavior.
7. **Session Management** – Manage authorized testing sessions.
8. **Post Assessment** – Evaluate the security impact on the system.
9. **Reporting** – Document vulnerabilities and remediation steps.

---

## 18. Important Terms

| Term | Meaning |
|---|---|
| Framework | Collection of Tools and Modules |
| Module | Component Designed for a Specific Task |
| Exploit | Code That Takes Advantage of a Vulnerability |
| Payload | Action Performed After Exploitation |
| Encoder | Payload Encoding Tool |
| Auxiliary | Scanning and Testing Module |
| Listener | Service That Accepts Connections |
| Meterpreter | Advanced Session Interface |
| Post | Post-Exploitation Testing |
| NOP | No Operation Instruction |
| Session | Active Connection |
| LHOST | Local Host Address |
| LPORT | Local Listening Port |
| RHOST | Remote Host Address |
| RPORT | Remote Service Port |

---

## 19. Important Notes

- Exploit and Payload are not the same.
- MSFConsole is the main interface of Metasploit.
- MSFVenom is a Payload Generation Tool.
- Auxiliary Modules perform testing without direct exploitation.
- Meterpreter provides more features than a standard shell.
- Encoding does not guarantee that a payload is safe or undetectable.
- Always perform testing in your own lab or on systems where you have explicit authorization.

**Main Goal of Metasploit:** Identify vulnerabilities, validate security weaknesses, and help improve system security.