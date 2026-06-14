
# Room 04 — Systems as Attack Vectors
**Path:** SOC Level 1
**Platform:** TryHackMe  
**Date completed:** 13/06/2026

---

## Core Concept

Even a security-aware human cannot protect a system with weak 
technical defences. If the lock is fragile, the attacker 
sneaks in while no one is watching — no human interaction needed.

---

## Website Defacement

An attack where an attacker gains unauthorized access to a website 
and **visibly alters its content** — replacing it with their own 
message, images, or propaganda.

---

## Supply Chain Attacks

Instead of attacking a target directly, the attacker **compromises 
a trusted third-party vendor or software** that the target uses.

The target installs or trusts the compromised product — and 
unknowingly lets the attacker in.

### Why supply chain attacks are dangerous:
- The malicious software comes from a trusted, legitimate source
- Victims have no reason to suspect it
- One successful attack can compromise thousands of organizations 
  simultaneously

---

### Real Example 1 — SolarWinds (2020)

**What happened:**
- SolarWinds makes Orion — a widely used IT monitoring software
- Attackers (Russian state-sponsored group) compromised SolarWinds' 
  build process and inserted malware into a legitimate software update
- Around 18,000 organizations downloaded and installed the update — 
  including US government agencies and Fortune 500 companies
- Attackers had silent access for months before discovery

**Key lesson:**  
Even installing a legitimate, signed update from a trusted vendor 
can compromise your entire organization.

---

### Real Example 2 — 3CX (2023)

**What happened:**
- 3CX is a popular business phone software used by 600,000+ companies
- Attackers compromised 3CX's own software installer
- Companies that downloaded the official 3CX desktop app installed 
  malware without knowing
- The attack was itself caused by a prior supply chain attack — 
  a compromised financial software (Trading Technologies) had 
  infected a 3CX employee's machine first

**Key lesson:**  
Supply chain attacks can chain together — one compromised vendor 
leads to another, spreading further than any direct attack could.

---

## Vulnerabilities

A **vulnerability** is a weakness in a system, application, or 
network that can be exploited by an attacker.

### Types:

| Type | Description |
|---|---|
| Software vulnerability | Bug or flaw in code that can be exploited |
| Unpatched systems | Known vulnerability exists but fix has not been applied |
| Zero-day | Vulnerability unknown to the vendor — no patch exists yet |
| Weak credentials | Default or easily guessable passwords on systems |
| Open ports | Unnecessary services exposed to the internet |

### How to deal with vulnerabilities:

- **Patch management** — apply security updates regularly and promptly
- **Vulnerability scanning** — tools like Nessus, OpenVAS scan systems 
  for known weaknesses
- **Penetration testing** — ethical hackers attempt to exploit 
  vulnerabilities before real attackers do
- **CVE monitoring** — track Common Vulnerabilities and Exposures 
  database for newly disclosed flaws affecting your software
- **Attack surface reduction** — disable unnecessary services, 
  close unused ports, remove unused software

---

## Misconfigurations

A **misconfiguration** is when a system is set up incorrectly — 
not a bug in the software itself, but a human error in how 
it was configured.

### Common misconfigurations:

| Misconfiguration | Example |
|---|---|
| Default credentials | Admin panel still using username: admin / password: admin |
| Excessive permissions | Employee has admin rights they do not need |
| Open cloud storage | S3 bucket or Azure blob set to public — anyone can read it |
| Exposed admin panels | Login portals accessible directly from the internet |
| Unnecessary open ports | Services running and exposed that should be disabled |
| Missing encryption | Sensitive data stored or transmitted without encryption |
| Overly permissive firewall rules | Firewall allows all inbound traffic instead of specific ports |

### How to deal with misconfigurations:

- **Security hardening** — follow benchmarks like CIS Controls to 
  configure systems securely from the start
- **Regular audits** — periodically review configurations against 
  security baselines
- **Automated scanning** — tools that continuously check for 
  common misconfigurations
- **Principle of least privilege** — give users and systems only 
  the minimum access they need
- **Change management** — track and review every configuration 
  change made to systems

---

## Key Terms

| Term | Definition |
|---|---|
| Website defacement | Unauthorized alteration of a website's visible content |
| Supply chain attack | Compromising a trusted vendor to reach the actual target |
| Vulnerability | A weakness in a system that can be exploited |
| Zero-day | Vulnerability with no available patch yet |
| Misconfiguration | Insecure system setup due to human error in configuration |
| Patch management | Process of regularly applying security updates |
| CIS Controls | Security configuration benchmarks for hardening systems |
| CVE | Common Vulnerabilities and Exposures — public database of known flaws |
| Attack surface | All possible points where an attacker could try to gain access |

---

## Personal Takeaways

- A security-aware user is useless if the underlying system is weak — 
  both human and technical defences are needed together
- SolarWinds showed that even government agencies can be compromised 
  through a trusted software update — scale of supply chain attacks 
  is terrifying
- 3CX showed supply chain attacks can chain — one breach triggers another
- Misconfigurations are often more common than actual software 
  vulnerabilities — human error in setup is a massive attack surface
- As a SOC analyst, seeing an admin panel exposed to the internet 
  or default credentials in use should immediately raise a flag


---
*Previous: Humans as Attack Vectors*  
*Next: SOC L1 Alert Triage*
