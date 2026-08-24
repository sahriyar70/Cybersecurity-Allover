# Cybersecurity Fundamentals Guide

**Topics:** Cybersecurity Concepts, Threat Modeling, Risk Assessment & Security Architecture

---

## Overview

Cybersecurity is the overall practice of protecting digital assets, systems, networks, applications, and data from cyberattacks, unauthorized access, disruption, modification, or destruction.

This guide covers the fundamental principles of cybersecurity, including the CIA Triad, threats and vulnerabilities, risk assessment, attack surfaces, security controls, defense strategies, access control, Zero Trust, and continuous security practices.

---

## What is Cybersecurity?

Cybersecurity is the practice of protecting:

* Networks
* Devices
* Applications
* Systems
* Digital infrastructure
* Data

from unauthorized access, cyberattacks, disruption, damage, or theft.

The primary objectives of cybersecurity are to:

1. Keep systems and services available.
2. Protect sensitive and confidential information.
3. Maintain the integrity and accuracy of data.
4. Prevent unauthorized access.
5. Detect and respond to security incidents.
6. Recover systems and data after an incident.

---

# The CIA Triad

The **CIA Triad** represents three fundamental principles of information security:

* **Confidentiality**
* **Integrity**
* **Availability**

These three principles form the foundation of many security architectures and security policies.

### 1. Confidentiality

**Definition:** Ensuring that sensitive information can only be accessed by authorized individuals, systems, or processes.

**Goal:**

> Prevent unauthorized disclosure of information.

**Examples of security mechanisms:**

* Encryption
* Multi-Factor Authentication (MFA)
* Access Control Lists (ACLs)
* Role-Based Access Control (RBAC)
* Data classification

**Example:**

Only authorized employees should be able to access a company's confidential customer database.

---

### 2. Integrity

**Definition:** Ensuring that data remains accurate, complete, and protected from unauthorized modification or deletion.

**Goal:**

> Prevent unauthorized alteration or destruction of information.

**Examples of security mechanisms:**

* Hashing
* SHA-256
* Digital signatures
* File integrity monitoring
* Version control
* Database controls

**Example:**

If an attacker modifies a financial transaction from `$100` to `$10,000`, the integrity of the data has been compromised.

---

### 3. Availability

**Definition:** Ensuring that authorized users can access systems, services, and data when they are needed.

**Goal:**

> Keep systems and services operational and accessible.

**Examples of security mechanisms:**

* Load balancers
* Redundant infrastructure
* High-availability systems
* DDoS mitigation
* Backups
* Disaster recovery
* Failover systems

**Example:**

An online banking service should remain available to customers even if one server fails.

---

# Threat, Vulnerability, Risk, Exploit & Impact

These terms are closely related but represent different concepts in cybersecurity.

A simplified relationship can be represented as:

```text
Threat
   ↓
Targets
   ↓
Vulnerability
   ↓
Exploit
   ↓
Potential Impact
   ↓
Risk
```

---

## Threat

A **Threat** is anything that has the potential to cause harm to a system, network, application, organization, or data.

Examples:

* Cybercriminals
* Malware
* Attackers
* Insider threats
* Natural disasters
* Hardware failures
* Nation-state actors

---

## Vulnerability

A **Vulnerability** is a weakness or flaw in a system, application, network, configuration, process, or security policy that could potentially be exploited.

Examples:

* Unpatched software
* Weak passwords
* Misconfigured servers
* Insecure APIs
* Outdated operating systems
* Improper access controls
* Software bugs

---

## Exploit

An **Exploit** is a technique, procedure, code, or tool used to take advantage of a vulnerability.

For example:

```text
Vulnerability:
Outdated software with a known security flaw

        ↓

Exploit:
A technique that abuses the vulnerability

        ↓

Result:
Unauthorized access or other security impact
```

---

## Risk

**Risk** represents the possibility that a threat will successfully exploit a vulnerability and cause a harmful impact.

A simplified conceptual formula is:

```text
Risk ≈ Likelihood × Impact
```

Risk assessment may consider several factors, including:

* Threat likelihood
* Vulnerability severity
* Exposure
* Asset value
* Potential business impact
* Existing security controls

> Note: `Threat × Vulnerability × Impact` can be useful as a simplified learning model, but there is no single universal mathematical formula for cybersecurity risk.

---

## Impact

**Impact** is the level of damage or consequence resulting from a successful security incident.

Impact may include:

* Financial loss
* Data loss
* Service disruption
* Legal consequences
* Regulatory penalties
* Reputation damage
* Customer trust loss
* Operational disruption

---

# Attack Surface

An **Attack Surface** is the collection of possible entry points, interfaces, systems, or pathways that an attacker could potentially use to interact with or compromise an environment.

The larger the attack surface, the more opportunities an attacker may have.

## Types of Attack Surface

### 1. Digital Attack Surface

Examples:

* Open ports
* Public IP addresses
* Web applications
* APIs
* Login portals
* Cloud infrastructure
* Exposed databases
* Remote access services

### 2. Physical Attack Surface

Examples:

* Server rooms
* Data centers
* Unlocked computers
* USB devices
* Network equipment
* Physical access points

### 3. Human / Social Attack Surface

Examples:

* Employees
* Customers
* Phishing targets
* Social engineering targets
* Users with weak security awareness

### Security Goal

Security teams generally try to **reduce unnecessary attack surface** by:

* Closing unused ports
* Removing unnecessary services
* Restricting network access
* Removing unused accounts
* Applying secure configurations
* Reducing unnecessary privileges
* Securing public-facing applications

---

# Security Controls

**Security Controls** are safeguards, technologies, processes, policies, or procedures designed to reduce security risks.

## Types of Security Controls

| Control Type     | Purpose                                                                       | Examples                                  |
| ---------------- | ----------------------------------------------------------------------------- | ----------------------------------------- |
| **Preventive**   | Prevent security incidents before they occur                                  | Firewall, MFA, IPS                        |
| **Detective**    | Detect attacks or suspicious activity                                         | IDS, SIEM, log monitoring                 |
| **Corrective**   | Correct problems and restore normal operation                                 | Backup restoration, system recovery       |
| **Deterrent**    | Discourage attackers from attempting attacks                                  | Warning banners, CCTV, legal consequences |
| **Compensating** | Provide alternative protection when the primary control cannot be implemented | WAF protecting a legacy application       |

---

# Defense in Depth

**Defense in Depth** is a security strategy that uses multiple layers of protection instead of relying on a single security mechanism.

The core idea is:

> If one security layer fails, another layer should still provide protection.

A simplified model:

```text
[ Physical Security ]
          ↓
[ Perimeter Security ]
          ↓
[ Network Security ]
          ↓
[ Endpoint Security ]
          ↓
[ Application Security ]
          ↓
[ Data Security ]
```

## Example Layers

### 1. Physical Security

Examples:

* Access cards
* Biometrics
* Security guards
* CCTV
* Locked server rooms

### 2. Perimeter Security

Examples:

* Firewalls
* Network gateways
* DDoS protection
* Intrusion prevention systems

### 3. Network Security

Examples:

* Network segmentation
* VLANs
* Access control
* IDS/IPS
* Network monitoring

### 4. Endpoint Security

Examples:

* Antivirus
* EDR
* Host-based firewalls
* Endpoint monitoring
* Device encryption

### 5. Application Security

Examples:

* Input validation
* Secure authentication
* Authorization
* Secure coding
* Web Application Firewall (WAF)

### 6. Data Security

Examples:

* Encryption at rest
* Encryption in transit
* Data access controls
* Backups
* Data loss prevention

---

# Principle of Least Privilege (PoLP)

The **Principle of Least Privilege** states that a user, application, service, or system should receive only the minimum permissions required to perform its intended task.

In simple terms:

> Give users and systems only the access they actually need.

## Why is Least Privilege Important?

If an account is compromised, excessive permissions can allow an attacker to access a much larger portion of the environment.

Least privilege helps reduce the:

**Blast Radius**

of a compromised account or system.

## Example

A content writer may need permission to:

```text
Create posts
Edit posts
Publish posts
```

But they may not need:

```text
Database administrator access
Server administrator access
User account management
Infrastructure management
```

Giving unnecessary privileges increases security risk.

---

# Authentication vs Authorization

Authentication and authorization are related but different concepts.

|                  | Authentication (AuthN)         | Authorization (AuthZ)                |
| ---------------- | ------------------------------ | ------------------------------------ |
| **Question**     | "Who are you?"                 | "What are you allowed to do?"        |
| **Purpose**      | Verify identity                | Determine permissions                |
| **When**         | Usually happens first          | Usually happens after authentication |
| **Examples**     | Password, OTP, Biometrics, SSO | RBAC, ABAC, OAuth scopes             |
| **HTTP Example** | `401 Unauthorized`             | `403 Forbidden`                      |

### Authentication Example

A user enters:

```text
Username
Password
MFA Code
```

The system verifies that the user is really who they claim to be.

### Authorization Example

After authentication, the system checks:

```text
Can this user access /admin?
```

If the user does not have permission, access should be denied.

---

# Security is Continuous

Cybersecurity is not a one-time project or configuration.

It is a **continuous process**.

New vulnerabilities, threats, attack techniques, technologies, and business requirements constantly emerge.

## Why is Security Continuous?

Because:

* New vulnerabilities are discovered.
* New attack techniques are developed.
* Systems and applications change.
* New devices are introduced.
* New users join organizations.
* Threat actors change their tactics.
* Software requires continuous patching.
* Security configurations can become outdated.

## Continuous Security Lifecycle

```text
Identify
   ↓
Protect
   ↓
Detect
   ↓
Respond
   ↓
Recover
   ↓
Improve
   ↓
Identify
```

## Important Activities

Organizations should regularly perform:

* Patch management
* Vulnerability assessment
* Security monitoring
* Security audits
* Penetration testing
* Configuration reviews
* Incident response exercises
* Backup testing
* Access reviews

---

# Zero Trust Architecture (ZTA)

**Zero Trust** is a security approach based on the principle:

> **Never Trust, Always Verify.**

Traditional security models often relied heavily on the idea of a trusted internal network.

Zero Trust assumes that **no user, device, application, or network location should automatically be trusted**.

Every access request should be evaluated based on relevant security signals.

## Key Zero Trust Principles

* Verify explicitly
* Apply least privilege
* Assume breach
* Continuously monitor
* Validate identity
* Validate device security
* Limit access
* Reduce lateral movement

A simplified model:

```text
User / Device
      ↓
Identity Verification
      ↓
Device Verification
      ↓
Policy Evaluation
      ↓
Least-Privilege Access
      ↓
Continuous Monitoring
```

---

# Non-Repudiation

**Non-Repudiation** is the ability to provide evidence that a specific action, transaction, or communication was performed by a particular entity, making it difficult for that entity to later deny the action.

Common mechanisms include:

* Digital signatures
* Audit logs
* Transaction records
* Cryptographic evidence
* Trusted timestamps

## Example

If a user digitally signs a document using a valid digital signature, the signature can provide evidence that the document was signed by that user and that the content was not altered after signing.

---

# Social Engineering & Phishing

**Social Engineering** is the manipulation of people into performing actions or revealing information that could compromise security.

Instead of directly attacking a technical vulnerability, an attacker may exploit human behavior.

## Common Examples

* Phishing
* Spear phishing
* Smishing
* Vishing
* Pretexting
* Baiting
* Impersonation

### Phishing Example

An attacker may send a fake email pretending to be from a legitimate organization and attempt to convince the victim to:

* Click a malicious link
* Reveal credentials
* Download a malicious file
* Transfer money
* Provide sensitive information

### Security Awareness

Users should learn to identify:

* Suspicious links
* Unexpected attachments
* Urgent requests
* Fake login pages
* Unusual sender addresses
* Requests for passwords or MFA codes

---

# Threat Modeling

**Threat Modeling** is a structured process used to identify potential threats, vulnerabilities, attack paths, and security requirements before or during the design of a system.

A simplified threat modeling process:

```text
Identify Assets
      ↓
Understand Architecture
      ↓
Identify Threats
      ↓
Identify Vulnerabilities
      ↓
Assess Risk
      ↓
Design Security Controls
      ↓
Validate & Review
```

## Important Questions

When analyzing a system, ask:

1. What are we protecting?
2. Who are we protecting it from?
3. What could go wrong?
4. How could an attacker reach the asset?
5. What would be the impact?
6. What security controls can reduce the risk?

---

# Risk Assessment

**Risk Assessment** is the process of identifying, analyzing, and evaluating security risks.

A basic process:

```text
Identify Assets
      ↓
Identify Threats
      ↓
Identify Vulnerabilities
      ↓
Estimate Likelihood
      ↓
Estimate Impact
      ↓
Determine Risk
      ↓
Prioritize
      ↓
Apply Controls
```

## Example

Suppose an organization has an internet-facing server running outdated software.

```text
Asset:
Web Server

Threat:
External Attacker

Vulnerability:
Outdated Software

Likelihood:
High

Potential Impact:
High

Risk:
High
```

The organization may then prioritize:

* Patching the software
* Restricting unnecessary access
* Monitoring the server
* Reviewing logs
* Applying additional security controls

---

# Key Security Principles

Several important principles appear repeatedly throughout cybersecurity.

### Least Privilege

Provide only the permissions that are required.

### Defense in Depth

Use multiple security layers.

### Zero Trust

Never automatically trust users, devices, or networks.

### Secure by Design

Security should be considered during system design rather than added only after deployment.

### Fail Securely

When something fails, the system should fail in a secure state whenever practical.

### Minimize Attack Surface

Reduce unnecessary services, interfaces, permissions, and exposure.

### Assume Breach

Design systems with the assumption that a compromise may eventually occur.

### Continuous Monitoring

Continuously monitor systems for suspicious or abnormal activity.

---

# Key Takeaways

1. **The CIA Triad**—Confidentiality, Integrity, and Availability—is one of the fundamental foundations of information security.
2. A **Threat** is a potential source of harm, while a **Vulnerability** is a weakness that can potentially be exploited.
3. An **Exploit** is a method or technique used to take advantage of a vulnerability.
4. **Risk** considers both the likelihood of an adverse event and its potential impact.
5. Keep the **Attack Surface** as small as reasonably possible.
6. Use **Defense in Depth** instead of relying on a single security control.
7. Apply the **Principle of Least Privilege** to minimize unnecessary access.
8. **Authentication** verifies identity, while **Authorization** determines permissions.
9. **Zero Trust** follows the principle of "Never Trust, Always Verify."
10. **Threat Modeling** helps identify security problems before they become incidents.
11. Security is a **continuous process**, not a one-time implementation.
12. **Security controls** should prevent, detect, respond to, and recover from security incidents.
13. Human behavior is an important part of the security landscape, making **Social Engineering and Phishing** major security concerns.
14. Effective cybersecurity requires a combination of **people, processes, and technology**.

---

# Quick Revision

```text
CIA Triad
├── Confidentiality → Prevent unauthorized disclosure
├── Integrity       → Prevent unauthorized modification
└── Availability    → Keep systems accessible

Threat        → Potential source of harm
Vulnerability → Weakness
Exploit       → Method of exploiting a weakness
Risk          → Likelihood + Impact
Impact        → Consequence of an incident

Attack Surface
├── Digital
├── Physical
└── Human

Security Controls
├── Preventive
├── Detective
├── Corrective
├── Deterrent
└── Compensating

Core Principles
├── Least Privilege
├── Defense in Depth
├── Zero Trust
├── Secure by Design
├── Minimize Attack Surface
└── Assume Breach
```

---

## Recommended Next Topics

After completing these fundamentals, useful next areas to study include:

1. Networking Fundamentals
2. Linux Fundamentals
3. Windows Fundamentals
4. Operating System Security
5. Cryptography
6. Web Security
7. Authentication & Access Control
8. Vulnerability Management
9. Penetration Testing
10. Security Operations (SOC)
11. Digital Forensics
12. Incident Response
13. Malware Analysis
14. Cloud Security
15. Active Directory Security
16. CTF & Security Labs
