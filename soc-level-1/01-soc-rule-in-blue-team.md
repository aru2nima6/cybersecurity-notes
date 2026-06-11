# Room 02 — SOC Role in the Blue Team
**Path:** SOC Level 1  
**Platform:** TryHackMe  
**Date completed:** 09/06/2026

---

## What I learned in this room

This room gave me a clear picture of how cybersecurity teams are 
structured — who does what, how teams differ, and where the SOC 
fits inside the bigger security picture.

---

## The Three Major Cybersecurity Teams

| Team | Nickname | What they do |
|---|---|---|
| Blue Team | Defenders | Protect, monitor, detect, and respond to attacks |
| Red Team | Attackers | Simulate real attacks to find weaknesses before real attackers do |
| GRC Team | Governance | Handle compliance, risk, audits, and security policies |

### Simple analogy:
- Red team tries to break into the house
- Blue team defends the house and catches intruders
- GRC team writes the rules about how the house should be secured 
  and checks that those rules are being followed

---

## Blue Team — Defenders

The blue team is responsible for **defending the organization** 
from cyber attacks.

### What blue team does:
- Monitor networks and systems for suspicious activity
- Detect and investigate security alerts
- Respond to incidents and contain damage
- Build detection rules and improve defenses over time
- Analyze attacker behavior to improve future defenses

**The SOC is the core of the blue team.**

---

## Red Team — Attackers (Ethical)

The red team **simulates real attacks** on the organization — with 
permission — to find vulnerabilities before real attackers do.

### What red team does:
- Penetration testing (breaking into systems legally)
- Social engineering simulations (phishing tests)
- Physical security testing
- Report findings to the blue team so they can fix weaknesses

**Key point:** Red teamers think like attackers so the blue team 
can build better defenses.

---

## GRC Team — Governance, Risk and Compliance

GRC stands for **Governance, Risk, and Compliance**.

This team is less technical and more process/policy focused.

### What GRC does:
- Write and enforce security policies
- Conduct audits — check that security rules are actually being followed
- Manage risk assessments — identify what could go wrong and how bad it would be
- Ensure the company meets legal and regulatory requirements 
  (like ISO 27001, GDPR, PCI-DSS)

**GRC analysts don't investigate attacks — they make sure the 
organization is doing security correctly from a rules and compliance 
perspective.**

---

## SOC Team — Functions and Roles

The SOC (Security Operations Center) is the blue team's operational 
hub. Every role has a specific function.

---

### SOC L1 Analyst — Junior Security Analyst

**The entry-level role. First eyes on every alert.**

| | |
|---|---|
| Main job | Monitor SIEM dashboard, triage alerts, initial investigation |
| Reports to | SOC L2 / Senior Analyst |
| Acts alone? | No — escalates all confirmed or complex threats |
| Key skills | Alert triage, IP reputation checks, log reading, ticket documentation |

**Day in the life example:**
> An alert fires at 2am showing an internal laptop connecting to a 
> known malware IP. The L1 analyst checks the IP on AbuseIPDB, 
> confirms it is malicious, documents findings in the ticket, and 
> escalates to L2 with a clear summary.

---

### SOC L2 Analyst — Senior Analyst

**Handles complex cases escalated from L1. More experience, deeper 
investigation capability.**

| | |
|---|---|
| Main job | Deep-dive investigation, confirm or dismiss L1 escalations |
| Reports to | SOC Manager |
| Acts alone? | Can take containment actions; escalates major incidents to L3/IR |
| Key skills | Malware analysis basics, threat hunting, forensics, mentoring L1 |

**Day in the life example:**
> L1 escalates a suspicious alert. L2 pulls the full event timeline 
> from the SIEM, checks if the device made any other suspicious 
> connections, and determines this is an active malware infection. 
> They isolate the device and loop in the incident responder.

---

### SOC L3 Analyst — Threat Hunter

**The most experienced analyst. Proactively hunts for threats that 
automated tools haven't detected yet.**

| | |
|---|---|
| Main job | Proactive threat hunting, complex incident handling |
| Reports to | SOC Manager |
| Unique aspect | Does not wait for alerts — actively searches for hidden threats |
| Key skills | Advanced forensics, threat intelligence, attacker TTPs |

**Day in the life example:**
> No alert has fired, but L3 notices unusual DNS query patterns 
> in the logs over the past week. They investigate manually and 
> discover a slow, low-and-slow data exfiltration that automated 
> rules missed completely.

---

### SOC Engineer

**Builds and maintains the tools that analysts use.**

| | |
|---|---|
| Main job | Configure SIEM, EDR, firewall rules, and detection logic |
| Reports to | SOC Manager |
| Does shifts? | No — not an alert reviewer |
| Key skills | SIEM administration, scripting, tool integration |

**Day in the life example:**
> Analysts keep getting false positive alerts for a specific internal 
> scanning tool. The SOC engineer updates the SIEM rule to exclude 
> that tool's traffic so analysts stop wasting time on it.

---

### Detection Engineer

**Writes the rules that make alerts fire in the first place.**

| | |
|---|---|
| Main job | Create and tune detection rules based on known attack patterns |
| Works with | SOC engineers, threat researchers, L2/L3 analysts |
| Key skills | SIEM query language (Splunk SPL, KQL), knowledge of attacker TTPs |

**Day in the life example:**
> A new ransomware technique is published. The detection engineer 
> writes a SIEM rule that fires an alert if any device shows that 
> specific behavior pattern.

---

### SOC Manager

**Keeps the whole operation running.**

| | |
|---|---|
| Main job | Oversee SOC operations, report to senior management, manage team |
| Technical? | Yes, but more strategic than hands-on |
| Key skills | Leadership, reporting, SLA management, incident coordination |

**Day in the life example:**
> A major incident is ongoing. The SOC manager coordinates between 
> the L2 analyst, incident responder, IT team, and legal team — 
> making sure everyone knows their role and communication flows 
> correctly.

---

### Penetration Tester (Red Team)

**Simulates attacks on the company — legally and with permission.**

| | |
|---|---|
| Main job | Find vulnerabilities by actually exploiting them in a controlled way|
| Team | Red team — not part of SOC |
| Key skills | Nmap, Burp Suite, Metasploit, social engineering, report writing |

**Day in the life example:**
> Hired to test the company's web application. Uses Burp Suite to 
> find an SQL injection vulnerability, exploits it to access a test 
> database, documents the full attack path, and writes a report with 
> remediation steps.

---

### GRC Auditor

**Checks that security policies are actually being followed.**

| | |
|---|---|
| Main job | Conduct internal audits, assess compliance, write risk reports |
| Team | GRC — separate from SOC |
| Key skills | Knowledge of frameworks (ISO 27001, NIST, PCI-DSS), interviewing, documentation |

**Day in the life example:**
> Conducts a quarterly audit. Reviews whether all employees completed 
> security awareness training, checks if access controls match the 
> policy, and flags three gaps in a formal report to management.

---

### Threat Researcher

**Studies attackers — their tools, techniques, and motivations.**

| | |
|---|---|
| Main job | Research new malware, attacker groups, and emerging threats |
| Output | Threat intelligence reports used by analysts and detection engineers |
| Key skills | Malware analysis, dark web monitoring, OSINT, writing |

**Day in the life example:**
> Discovers a new ransomware group targeting Indian financial companies. 
> Writes an intelligence report detailing their attack methods, 
> indicators of compromise (IOCs), and recommended detections — 
> shared with the SOC team to improve their defenses.

---

### CERT Lead — Computer Emergency Response Team Lead

**Takes charge during major incidents.**

| | |
|---|---|
| Main job | Lead the response to serious security incidents |
| Called when | Major breach, ransomware, critical system compromise |
| Key skills | Incident response, forensics, coordination, communication under pressure |

**Day in the life example:**
> Ransomware hits 30 company machines overnight. The CERT lead 
> coordinates containment (isolating affected machines), evidence 
> preservation (taking forensic images), recovery (restoring backups), 
> and post-incident review (how did this happen and how do we prevent it).

---

## Internal SOC vs MSSP

Two ways a company can run its security operations:

| | Internal SOC | MSSP |
|---|---|---|
| Full name | In-house Security Operations Center | Managed Security Service Provider |
| Who runs it | Company's own employees | External third-party security company |
| Cost | High — salaries, tools, infrastructure | Lower — shared cost across many clients |
| Best for | Large companies with complex needs | Smaller companies that can't afford a full SOC |
| Control | Full control over tools and processes | Less control — depends on the provider |
| Example | A bank runs its own 24/7 SOC team | A small startup pays CrowdStrike to monitor their alerts |

**Key point:** Many entry-level SOC analyst jobs in India are at 
MSSPs — companies like Tata Communications, Wipro, HCL, and Infosys 
run MSSPs and hire L1 analysts regularly.

---

## Cyber Security Incident Response Team (CSIRT / CERT)

A **CSIRT** (Computer Security Incident Response Team) is a specialized 
group activated during serious security incidents.

### Their process:
1. **Identify** — confirm a real incident is happening
2. **Contain** — stop the spread (isolate affected systems)
3. **Eradicate** — remove the threat completely
4. **Recover** — restore systems to normal operation
5. **Post-incident review** — understand what happened and improve

**Difference from SOC:**
- SOC monitors and detects threats daily
- CSIRT/CERT responds to confirmed major incidents
- In many companies the same people do both

---

## Specialized Defensive Roles Summary

| Role | Team | Focus |
|---|---|---|
| SOC L1 Analyst | Blue / SOC | Alert triage, first response |
| SOC L2 Analyst | Blue / SOC | Deep investigation, mentoring L1 |
| SOC L3 / Threat Hunter | Blue / SOC | Proactive hunting, complex cases |
| SOC Engineer | Blue / SOC | Tool configuration and maintenance |
| Detection Engineer | Blue / SOC | Writing and tuning detection rules |
| SOC Manager | Blue / SOC | Team leadership and reporting |
| CERT Lead | Blue / IR | Major incident coordination |
| Threat Researcher | Blue / Intel | Attacker research and intelligence |
| Penetration Tester | Red | Simulated attacks, finding weaknesses |
| GRC Auditor | GRC | Compliance, audits, risk management |

---

## Key Terms from this Room

| Term | Definition |
|---|---|
| Blue team | Defensive security team — detect, protect, respond |
| Red team | Offensive security team — simulate attacks ethically |
| GRC | Governance, Risk, Compliance — policy and audit focused |
| MSSP | Managed Security Service Provider — outsourced SOC |
| CERT / CSIRT | Incident response team activated during major incidents |
| Threat hunting | Proactively searching for hidden threats without waiting for alerts |
| TTP | Tactics, Techniques and Procedures — how attackers operate |
| IOC | Indicator of Compromise — evidence an attack occurred |
| Alert triage | Prioritizing and assessing incoming alerts quickly |
| Escalation | Passing a case to a higher-level analyst |

---

## My Personal Takeaways

- The SOC is just one part of a bigger security structure — red team 
  and GRC exist alongside it
- L1 is where everyone starts — the path to L2, L3, engineer or 
  manager all begin here
- MSSPs are a realistic entry point for fresher SOC analyst jobs in India
- Incident response is a separate specialized function — not every 
  analyst does it
- Understanding where your role fits in the bigger picture helps you 
  explain it clearly in interviews

---

## Questions I want to research further

- [ ] What does a real MSSP work environment look like compared to internal SOC?
- [ ] What certifications do L2 analysts typically have?
- [ ] What is the difference between CSIRT and CERT exactly?
- [ ] How does threat hunting work practically — what tools are used?

---

*Previous room: Junior Security Analyst Intro*  
*Next room: Humans as Attacks vectors*  
*Path: SOC Level 1 — TryHackMe*
