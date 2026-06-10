# Room 01 — Junior Security Analyst Intro
**Path:** SOC Level 1  
**Platform:** TryHackMe  
**Date completed:**04-06-2026   
**Status:** Completed
---

## What I learned in this room

This room introduced the role of a Junior SOC Analyst and gave me 
a practical simulation of investigating a malicious IP — from detection 
to blocking it on the firewall.

---

## SOC — Security Operations Center

A SOC is a team that protects a company's systems 24/7 by monitoring, 
detecting, and responding to security threats.

**Main focus of a SOC:**
- **Detection** — find threats before they cause damage
- **Response** — take action when a threat is confirmed

---

## Three Pillars of a SOC

| Pillar | What it means |
|---|---|
| People | The analysts, engineers, and managers who run the SOC |
| Process | The playbooks and procedures followed during incidents |
| Technology | The tools used to detect and respond (SIEM, EDR, firewall) |

---

## SOC Team Hierarchy

From top to bottom:
CISO (Chief Information Security Officer)
└── SOC Manager
├── Detection Engineer
├── Security Engineer
├── SOC Analyst L3 (most experienced)
├── SOC Analyst L2 (Senior Analyst)
└── SOC Analyst L1 (Junior Analyst) ← this is the entry role

**Key point:** L1 analysts are the first to see alerts. They do initial 
investigation and escalate to L2 if needed. They never act alone on 
major decisions.

---

## Role: Junior SOC Analyst (L1)

Also called: **Junior Security Analyst**

### What an L1 analyst does daily:
- Monitor the SIEM dashboard for incoming alerts
- Investigate and triage security tickets
- Perform IP reputation checks on suspicious IPs
- Escalate confirmed threats to the Senior Analyst (L2)
- Document findings clearly in every ticket

---

## What are Tickets?

A **ticket** is a logged record of a security alert that needs 
investigation. When the SIEM detects something suspicious, it 
automatically creates a ticket assigned to an analyst.

As an L1 analyst, your job for every ticket:
1. Open the ticket and read what triggered it
2. Investigate — is this real or a false alarm?
3. Document what you found
4. Escalate or close with clear notes

---

## What is Alert Triage?

**Triage** means quickly assessing incoming alerts to decide:
- Is this a **true positive** (real threat) or **false positive** (false alarm)?
- How urgent is it?
- What action needs to be taken?

In a busy SOC, dozens of alerts come in per shift. Triage helps 
analysts prioritize which ones need immediate attention.

---

## What is Data Exfiltration?

Data exfiltration is when an attacker **steals data from inside a 
network and sends it outside** — to a server they control.

Example: malware on a company laptop quietly sending customer 
records to an attacker's server every night.

This is one of the most serious things an L1 analyst watches for 
in traffic logs and SIEM alerts.

---

## Technology Used in a SOC

| Tool | Full name | What it does |
|---|---|---|
| SIEM | Security Information and Event Management | Collects all logs, shows alerts in one dashboard |
| EDR | Endpoint Detection and Response | Monitors individual devices (laptops, servers) for threats |
| Firewall | — | Controls what traffic is allowed in and out of the network |

---

## What is a SIEM?

A SIEM collects logs from every system in the company — firewalls, 
servers, endpoints, applications — and brings them into one place.

As an analyst, you use the SIEM to:
- Search logs for suspicious activity
- View real-time alerts
- Investigate what happened before and after an incident

**Important:** The SIEM detects and alerts — it does not automatically 
stop attacks. That's the analyst's job.

---

## IP Reputation Check

When a suspicious IP appears in an alert, an analyst checks whether 
that IP is known to be malicious.

### Tools used:
- **VirusTotal** — virustotal.com — check if IP is flagged by security vendors
- **AbuseIPDB** — abuseipdb.com — community-reported malicious IPs with confidence score

### How to do it:
1. Copy the suspicious IP from the alert
2. Paste it into AbuseIPDB → check confidence score and abuse reports
3. Paste it into VirusTotal → check vendor detections
4. Document your findings in the ticket

---

## Practical Lab — Malicious IP Investigation

This is what I actually did in the room simulation:

### Step 1 — Alert received
A security alert appeared on the dashboard flagging a suspicious IP 
communicating with the network.

### Step 2 — IP reputation check
Looked up the IP on AbuseIPDB.  
Result: IP was flagged as malicious — confirmed bad actor.

### Step 3 — Escalate and report
Reported findings to the SOC Team Lead with:
- The malicious IP
- Evidence from AbuseIPDB
- What the IP was doing on the network

### Step 4 — Got permission to block
Received authorization from the SOC Team Lead to block the IP 
on the firewall.

**Key point:** L1 analysts do not block IPs on their own authority. 
They always get permission first.

### Step 5 — Blocked the IP
- Pasted the IP into the firewall block list
- Wrote a comment explaining why it was blocked
- Confirmed the block was applied

**Result:** Attack slowed down / stopped before further damage.

---

## Port Scan Activity

Also did a practical where a port scan was detected on the network.

- Identified the scan in the dashboard
- Confirmed it was intentional/suspicious activity
- Investigated the source

**What a port scan means:** An attacker (or tool) is probing the 
network to find open ports and running services — this is typically 
the **reconnaissance phase** before an actual attack.

---

## Key Terms from this Room

| Term | Definition |
|---|---|
| SOC | Team that monitors and protects company security 24/7 |
| L1 Analyst | Entry-level analyst — first to review alerts |
| Ticket | A logged alert or task requiring analyst investigation |
| Alert triage | Quickly prioritizing and assessing incoming alerts |
| True positive | Alert is real — actual threat confirmed |
| False positive | Alert is a false alarm — no real threat |
| IP reputation check | Looking up an IP to see if it is known to be malicious |
| Data exfiltration | Attacker stealing data and sending it outside the network |
| SIEM | Tool that collects all logs and displays alerts centrally |
| EDR | Tool that monitors individual devices for threats |
| Escalation | Passing a confirmed threat to a higher-level analyst |
| Firewall block | Preventing a specific IP from communicating with the network |

---

## My Personal Takeaways

- L1 analysts never act alone — always escalate and get permission
- IP reputation checks use multiple tools, not just one
- The SIEM shows alerts but the analyst decides what they mean
- Port scans are a warning sign — someone is mapping your network
- Documenting every step in the ticket is as important as the investigation itself

---

## Questions I want to research further

- [ ] What does a real SIEM alert look like in Splunk?
- [ ] How does a firewall decide what to block automatically vs manually?
- [ ] What happens after you block an IP — does the attacker just use another one?
- [ ] What is the difference between EDR and antivirus?

---

*Next room: SOC Role in the Blue Team*  
*Path: SOC Level 1 — TryHackMe*
