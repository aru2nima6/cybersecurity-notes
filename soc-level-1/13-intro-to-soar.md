# Room 12 — Introduction to SOAR

**Path:** SOC Level 1 — Security Solutions

**Platform:** TryHackMe

---

## Core Concept

**SOAR (Security Orchestration, Automation, and Response)** helps SOC teams automate repetitive security tasks, connect multiple security tools, and streamline incident response using predefined workflows called **playbooks**.

Unlike SIEM, which mainly detects threats, SOAR focuses on **coordinating tools, automating investigations, and responding to incidents**.

---

# Traditional SOC Workflow

A Security Operations Center (SOC) protects an organization's digital assets through continuous monitoring, detection, and incident response.

### Core Responsibilities

| Capability | Purpose |
|------------|---------|
| Monitoring & Detection | Detect suspicious activity using SIEM and security tools |
| Recovery & Remediation | Isolate hosts, terminate processes, block IPs, remove malware |
| Threat Intelligence | Validate IOCs such as malicious IPs, hashes, and domains |
| Communication | Coordinate with IT teams and management through tickets and reports |

---

## Challenges Faced by Traditional SOCs

| Challenge | Problem |
|-----------|---------|
| Alert Fatigue | Large number of alerts overwhelm analysts |
| Disconnected Tools | Analysts constantly switch between SIEM, EDR, Firewalls, TI platforms, etc. |
| Manual Processes | Investigations rely on repetitive manual steps |
| Talent Shortage | Limited analysts handling increasing security incidents |

---

# What is SOAR?

**SOAR (Security Orchestration, Automation, and Response)** is a platform that integrates multiple security solutions into a single interface and automates repetitive security workflows.

Instead of manually switching between different tools, analysts can investigate and respond from one centralized platform.

SOAR also provides:

- Case management
- Ticketing
- Incident tracking
- Automated workflows
- Response automation

---

# Three Pillars of SOAR

| Pillar | Purpose |
|---------|---------|
| Orchestration | Connects multiple security tools into one workflow |
| Automation | Executes repetitive investigation steps automatically |
| Response | Performs containment actions such as blocking IPs or disabling users |

---

## 1. Orchestration

Orchestration integrates different security tools and defines **Playbooks** that describe how investigations should proceed.

Example tools involved:

- SIEM
- EDR
- Threat Intelligence platforms
- IAM
- Firewall
- Ticketing systems

Example VPN brute-force playbook:

1. Receive SIEM alert
2. Check user's historical logins
3. Check IP reputation
4. Verify successful logins
5. Escalate if malicious

---

## 2. Automation

Automation allows SOAR to execute playbooks automatically without analyst intervention.

Example:

- Receive SIEM alert
- Query historical logins
- Check IP reputation
- Disable compromised account
- Open investigation ticket

Benefits:

- Faster investigations
- Reduced manual work
- Lower analyst workload
- Consistent incident handling

---

## 3. Response

SOAR can automatically or manually execute response actions across integrated tools.

Common response actions include:

- Block IP address
- Disable user account
- Isolate endpoint
- Open incident ticket
- Notify security team

---

# Do SOAR Tools Replace SOC Analysts?

**No.**

SOAR automates repetitive work but **does not replace analysts**.

SOC analysts are still responsible for:

- Investigating complex incidents
- Making business-aware decisions
- Validating true positives
- Creating and improving playbooks
- Handling situations requiring human judgment

SOAR assists analysts—it does not replace them.

---

# What are Playbooks?

A **Playbook** is a predefined workflow that tells SOAR how to investigate and respond to a specific type of alert.

Think of it as a **step-by-step decision tree** for incident handling.

---

# Phishing Playbook

Example workflow:

1. Suspicious email received
2. Create investigation ticket
3. Check for URLs or attachments
4. Scan URLs/files using Threat Intelligence
5. Determine if email is malicious
6. Remove malicious email
7. Notify affected users
8. Escalate if necessary

Most repetitive tasks are automated, while analysts validate important decisions.

---

# CVE Patching Playbook

A **CVE (Common Vulnerabilities and Exposures)** is a publicly disclosed security vulnerability assigned a unique CVE ID.

Typical SOAR workflow:

1. Monitor newly released CVEs
2. Assess vulnerability severity
3. Check if vulnerable systems exist
4. Create remediation ticket
5. Test security patch
6. Deploy patch to production
7. Verify successful remediation

This reduces manual effort in vulnerability management.

---

# SOAR Benefits

- Centralizes multiple security tools
- Automates repetitive investigations
- Reduces alert fatigue
- Speeds up incident response
- Standardizes investigation workflows
- Improves analyst productivity
- Provides integrated case management

---

# SIEM vs EDR vs SOAR

| Solution | Primary Function |
|----------|------------------|
| SIEM | Collects, correlates, and detects threats from logs |
| EDR | Monitors endpoints, detects endpoint threats, and performs response actions |
| SOAR | Automates investigations and orchestrates multiple security tools |

---

# Key Terms

| Term | Definition |
|------|------------|
| SOAR | Security Orchestration, Automation, and Response |
| Orchestration | Coordinating multiple security tools through workflows |
| Automation | Automatically executing repetitive investigation tasks |
| Response | Taking containment actions against threats |
| Playbook | Predefined workflow used to investigate and respond to alerts |
| IOC | Indicator of Compromise (IP, domain, hash, URL, etc.) |
| TI | Threat Intelligence |
| IAM | Identity and Access Management |
| CVE | Common Vulnerabilities and Exposures |

---

# Personal Takeaways

- SOAR complements SIEM and EDR by automating repetitive SOC workflows.
- Playbooks standardize investigations, making responses faster and more consistent.
- Automation reduces analyst workload but still requires human oversight for critical decisions.
- Understanding how SIEM, EDR, and SOAR work together is essential for SOC analysts.
- Effective SOAR implementations improve response time while allowing analysts to focus on higher-value investigations.

---

*Previous: Elastic Stack (ELK)*  
*Next: Pyramid of Pain*
