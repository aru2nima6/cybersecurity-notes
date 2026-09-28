# Room 14 — Pyramid of Pain

**Path:** SOC Level 1 — Cyber Defense Frameworks 

**Platform:** TryHackMe

---

## Core Concept

The **Pyramid of Pain** is a concept used in cybersecurity to understand different types of indicators that defenders can detect.

It shows how much **"pain"** an attacker experiences when defenders detect different indicators.

The higher we move up the pyramid:

* Indicators become harder for attackers to change.
* Attackers need more time and resources to adapt.
* Detection becomes more focused on attacker behavior.

The Pyramid of Pain contains seven levels:

| Level | Indicator         | Difficulty for Attacker |
| ----- | ----------------- | ----------------------- |
| 1     | Hash Values       | Very Easy               |
| 2     | IP Addresses      | Easy                    |
| 3     | Domain Names      | Moderate                |
| 4     | Host Artifacts    | Difficult               |
| 5     | Network Artifacts | Difficult               |
| 6     | Tools             | Very Difficult          |
| 7     | TTPs              | Extremely Difficult     |

---

# 1. Hash Values

A **hash** is a fixed-length value generated from data using a hashing algorithm.

Security professionals use hashes to identify files, especially:

* Malware
* Suspicious files
* Ransomware samples
* Malicious executables

Common hashing algorithms include:

* **MD5**
* **SHA-1**
* **SHA-256**

> MD5 and SHA-1 are no longer considered secure for cryptographic purposes, but they can still be useful for identifying files.

---

## Why Hashes Are Low on the Pyramid

Hashes are easy for attackers to change.

Even changing a small part of a file can produce a completely different hash.

Example:

```powershell
Get-FileHash .\sample.exe -Algorithm MD5
```

If the file is modified:

```powershell
echo "Modified" >> .\sample.exe
```

The hash value will change.

Therefore, defenders cannot rely only on file hashes to detect malware.

---

## Hash Investigation

Security analysts can search suspicious hashes using threat intelligence platforms such as:

* VirusTotal
* MetaDefender
* MalwareBazaar

A hash can help identify:

* File name
* Malware family
* Previous detections
* Antivirus detections
* Related samples

---

# 2. IP Addresses

An **IP address** identifies a device or host on a network.

Attackers may use malicious IP addresses for:

* Command and Control (C2)
* Malware communication
* Hosting malicious files
* Phishing infrastructure

Defenders can block malicious IP addresses using:

* Firewalls
* IDS/IPS
* Network security controls

---

## Why IP Addresses Are Higher Than Hashes

Blocking a malicious IP address can stop communication with a known malicious host.

However, attackers can often obtain a new IP address.

This makes IP addresses relatively easy for attackers to change.

---

# Fast Flux

**Fast Flux** is a technique where multiple IP addresses are associated with a domain and changed frequently.

Attackers can use Fast Flux to make their infrastructure harder to:

* Detect
* Block
* Track
* Take down

### Simple Example

```text
malicious-domain.com
        |
   +----+----+----+
   |    |    |    |
  IP1  IP2  IP3  IP4
```

The IP addresses can constantly change while the domain remains the same.

---

## THM Investigation

In the provided Any.Run malware report:

**First IP address contacted:**

```text
50.87.136.52
```

**First domain contacted:**

```text
craftingalegacy.com
```

> Do not directly interact with suspicious IP addresses or malware infrastructure.

---

# 3. Domain Names

A **domain name** is a human-readable address used to access websites.

Example:

```text
tryhackme.com
```

A domain can contain:

```text
subdomain.domain.tld
```

Example:

```text
www.tryhackme.com
```

---

## Why Domain Names Cause More Pain

Changing a domain is more difficult than simply changing an IP address.

An attacker may need to:

1. Register a new domain
2. Configure DNS records
3. Set up infrastructure
4. Update malware or phishing links

Therefore, domain-based detection can create more problems for attackers.

---

# Punycode Attacks

**Punycode** is a way of representing Unicode characters using ASCII-compatible characters.

Attackers can abuse Unicode characters to create domains that visually resemble legitimate domains.

This is known as a **Punycode attack** or **IDN homograph attack**.

### Example

A malicious domain may use characters that look similar to letters in a legitimate domain.

The browser may display something that looks legitimate even though the underlying domain is different.

---

## Detecting Malicious Domains

Security analysts can investigate:

* DNS logs
* Proxy logs
* Web server logs
* Firewall logs
* SIEM alerts

Threat intelligence platforms can also provide information about suspicious domains.

---

# URL Shorteners

Attackers may hide malicious destinations behind URL-shortening services.

Examples include:

* bit.ly
* tinyurl.com
* ow.ly
* x.co

The shortened URL hides the real destination.

Analysts should investigate where the shortened URL redirects before determining whether it is malicious.

---

# Any.Run Networking

The **Networking** section of Any.Run can show different types of network activity generated by malware.

### HTTP Requests

Shows HTTP requests made by the malware.

Useful for identifying:

* Downloaded files
* Malicious URLs
* Web communication

### Connections

Shows communications between processes and hosts.

Useful for identifying:

* C2 communication
* FTP connections
* Data transfers

### DNS Requests

Shows DNS requests generated by the malware.

Malware may use DNS requests to:

* Locate C2 infrastructure
* Check internet connectivity
* Resolve malicious domains

---


# 4. Host Artifacts

**Host artifacts** are traces left by an attacker or malicious software on a system.

Examples include:

* Registry modifications
* Suspicious processes
* Dropped files
* Modified files
* Suspicious executables
* Malware execution patterns
* Persistence mechanisms

---

## Example

A malicious document might execute something like:

```text
Word Document
      ↓
Malicious Macro
      ↓
PowerShell
      ↓
Malware
```

The suspicious processes and files created during this activity can become useful detection artifacts.

---

## Why Host Artifacts Cause More Pain

Attackers may need to modify their malware or attack method if defenders detect specific host artifacts.

This requires more effort than simply changing:

* A hash
* An IP address
* A domain

---

## THM Investigation

A malicious process named:

```text
regidle.exe
```

made a POST request to an IP address on port:

```text
8080
```

### IP Address

```text
96.126.101.6
```

### Dropped Executable

```text
G_jugk.exe
```

These artifacts can be used as indicators during investigation and detection.

---

# 5. Network Artifacts

**Network artifacts** are suspicious patterns observed in network traffic.

Examples include:

* User-Agent strings
* URI patterns
* HTTP POST requests
* C2 communication patterns
* Suspicious DNS activity
* Unusual network protocols

---

# User-Agent

A **User-Agent** is information sent by a client in an HTTP request to identify the software making the request.

Example:

```text
Mozilla/5.0
```

Attackers and malware may use unusual or custom User-Agent strings.

These can become useful detection indicators.

---

## Detecting Network Artifacts

Network artifacts can be investigated using:

* Wireshark
* TShark
* Snort
* IDS/IPS
* SIEM

Example TShark command:

```bash
tshark --Y http.request -T fields -e http.host -e http.user_agent -r analysis_file.pcap
```

This extracts:

* HTTP host
* User-Agent

from a PCAP file.

---

# 6. Tools

At this level, defenders are detecting the actual tools used by attackers.

Examples include:

* Custom malware
* Backdoors
* Malicious macros
* Password crackers
* Custom executables
* Custom DLLs
* Payloads

---

## Why Tools Cause More Pain

If defenders can identify an attacker's specific tool, the attacker may need to:

* Modify the tool
* Build a new tool
* Find another tool
* Learn how to use another technique

This requires significantly more time and resources.

---

# Detection Methods

Security teams can use different techniques to identify malicious tools.

### Antivirus Signatures

Detect known malicious files.

### YARA Rules

Identify malware based on specific patterns.

### Detection Rules

Rules can identify known attack behaviors or artifacts.

### Fuzzy Hashing

Used to identify similarities between files even when they are not exactly identical.

---

# Fuzzy Hashing

Traditional hashes change completely when a file is modified.

**Fuzzy hashing** is different.

It allows security analysts to determine whether two files are similar even when they contain small differences.

This is useful when malware has been slightly modified to evade traditional hash-based detection.

---

# SSDeep

**SSDeep** is an example of a fuzzy hashing tool.

The alternative name for fuzzy hashes is:

```text
Context Triggered Piecewise Hashes
```

---

# 7. TTPs — The Apex

The highest level of the Pyramid of Pain is:

**TTPs**

TTP stands for:

**Tactics, Techniques and Procedures**

TTPs describe how an attacker operates.

They include the different actions an attacker performs throughout an attack.

---

## Example Attack

An attacker may perform:

```text
Phishing
   ↓
Initial Access
   ↓
Execution
   ↓
Persistence
   ↓
Privilege Escalation
   ↓
Credential Access
   ↓
Lateral Movement
   ↓
Data Exfiltration
```

These behaviors can be mapped to the **MITRE ATT&CK Framework**.

---

# Why TTPs Are at the Top

Attackers can relatively easily change:

```text
Hash → Easy
IP → Easy
Domain → Moderate
Host Artifact → Difficult
Network Artifact → Difficult
Tool → Very Difficult
TTP → Extremely Difficult
```

Changing an entire attack methodology requires significantly more effort.

For example, if defenders detect a specific **Pass-the-Hash** technique, the attacker may need to change their technique or attack strategy.

---

# MITRE ATT&CK and TTPs

MITRE ATT&CK provides a framework for documenting adversary:

* Tactics
* Techniques
* Procedures

Examples of tactics include:

* Initial Access
* Execution
* Persistence
* Privilege Escalation
* Defense Evasion
* Credential Access
* Discovery
* Lateral Movement
* Collection
* Command and Control
* Exfiltration
* Impact

Understanding TTPs helps SOC analysts detect attacker behavior instead of relying only on individual indicators.

---

# Pyramid of Pain — Simple View

```text
             TTPs
          ----------
            Tools
        ------------
      Network Artifacts
     ------------------
       Host Artifacts
    --------------------
       Domain Names
  ------------------------
       IP Addresses
----------------------------
       Hash Values
```

The higher we move up the pyramid:

* Indicators become harder for attackers to change.
* Attackers need more time and resources to adapt.
* Detection becomes more focused on attacker behavior.

---

# IOC vs TTP

| IOC / Indicator                 | TTP               |
| ------------------------------- | ----------------- |
| Specific evidence of compromise | Attacker behavior |
| Hash                            | Technique         |
| IP address                      | Tactic            |
| Domain                          | Procedure         |
| File                            | Attack method     |
| User-Agent                      | Example behavior  |

### Simple Example

Instead of only detecting:

```text
Malicious IP = 10.10.10.10
```

A SOC can also detect:

```text
Suspicious PowerShell execution
        +
Credential dumping
        +
Lateral movement
```

This focuses on **attacker behavior**, making detection less dependent on a single IOC.

---

# SOC Analyst Perspective

The Pyramid of Pain helps SOC analysts understand that not all indicators are equally useful for detection.

A good detection strategy can use multiple levels:

```text
Hash
 ↓
IP
 ↓
Domain
 ↓
Host Artifact
 ↓
Network Artifact
 ↓
Tool
 ↓
TTP
```

For example:

```text
SIEM Alert
    ↓
Suspicious IP
    ↓
Check Domain
    ↓
Check DNS Requests
    ↓
Check Host Processes
    ↓
Identify Malware
    ↓
Map Behavior to MITRE ATT&CK
```

This allows analysts to move from a single indicator toward understanding the overall attack behavior.

---

# Key Terms

| Term             | Definition                                                                      |
| ---------------- | ------------------------------------------------------------------------------- |
| Pyramid of Pain  | Concept showing how difficult different indicators are for attackers to change  |
| Hash             | Fixed-length value used to identify data                                        |
| IP Address       | Address identifying a host on a network                                         |
| Domain Name      | Human-readable address used to access websites                                  |
| Fast Flux        | Technique using frequently changing IP addresses for a domain                   |
| Punycode         | Encoding used to represent Unicode characters using ASCII-compatible characters |
| Host Artifact    | Evidence left on a host by an attacker or malware                               |
| Network Artifact | Suspicious pattern observed in network traffic                                  |
| User-Agent       | HTTP request header identifying the client software                             |
| Tool             | Software or utilities used by attackers                                         |
| TTP              | Tactics, Techniques and Procedures                                              |
| IOC              | Indicator of Compromise                                                         |
| C2               | Command and Control                                                             |
| Fuzzy Hashing    | Technique used to determine similarity between files                            |
| SSDeep           | Tool/algorithm used for fuzzy hashing                                           |
| MITRE ATT&CK     | Framework documenting adversary tactics and techniques                          |

---

# Personal Takeaways

* The **Pyramid of Pain** explains why different indicators have different levels of value during threat detection.
* Hashes are useful for identifying known malicious files but are easy for attackers to change.
* IP addresses and domains can be blocked, but attackers can change their infrastructure.
* Host and network artifacts provide more information about attacker activity.
* Fuzzy hashing can help identify modified versions of similar files.
* **TTP-based detection** focuses on attacker behavior rather than only individual IOCs.
* MITRE ATT&CK is useful for understanding and mapping attacker TTPs.
* As a SOC analyst, I should look beyond a single IOC and correlate multiple indicators and behaviors.

---

*Previous: Introduction to SOAR*
*Next: Cyber Kill Chain*

