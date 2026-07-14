# Room 05 — SOC L1 Alert Triage

**Path:** SOC Level 1 — SOC Team Internals

**Platform:** TryHackMe  
 
---
 
## Core Concept
 
A SOC can't manually review millions of raw logs a day. **Alerts** 
exist to filter that noise down to a manageable number of 
suspicious events — turning millions of logs into dozens of alerts 
an analyst can actually triage.
 
---
 
## From Events to Alerts
 
1. An **event** happens (login, process launch, file download, etc.)
2. The system generating it (OS, firewall, cloud provider) **logs** it
3. Logs are shipped to a security solution (**SIEM/EDR**)
4. If the logs match a detection rule, an **alert** is generated
---
 
## Alert Management Platforms
 
| Solution | Examples | Use |
|---|---|---|
| SIEM | Splunk ES, Elastic | Core alert management for most SOC teams |
| EDR/NDR | MS Defender, CrowdStrike | Own alert dashboards, but usually feeds SIEM/SOAR |
| SOAR | Splunk SOAR, Cortex SOAR | Centralises alerts from multiple sources (larger teams) |
| ITSM | Jira, TheHive | Ticket-based alert/case tracking |
 
---
 
## Who's Involved in Triage
 
- **L1 analyst** — reviews alerts, sorts real threats from noise, escalates to L2
- **L2 analyst** — receives escalations, does deeper investigation and remediation
- **SOC engineer** — makes sure alerts carry enough info to triage efficiently
- **SOC manager** — tracks triage speed/quality so real attacks aren't missed
---
 
## Key Alert Properties
 
| Property | What it tells you |
|---|---|
| Alert Time | When the alert fired (slightly after the actual event) |
| Alert Name | Summary of what happened, from the detection rule name |
| Severity | Urgency — Low / Medium / High / Critical |
| Status | New, In Progress, Closed, etc. |
| Verdict | True Positive (real threat) or False Positive (noise) |
| Assignee | Analyst who owns the alert |
| Description | Rule logic, why it matters, how to investigate |
| Alert Fields | Supporting data — hostname, command line, etc. |
 
---
 
## Alert Prioritisation
 
When picking an alert from the queue:
 
1. **Filter** — only take new/unassigned alerts, skip ones already being worked
2. **Sort by severity** — Critical → High → Medium → Low
3. **Sort by time** — oldest first (an older breach likely has more attacker progress)
---
 
## The Triage Flow
 
**1. Initial Actions**
Assign the alert to yourself, move it to *In Progress*, and read through 
the name, description, and key fields.
 
**2. Investigation**
The core step — apply technical judgement in the SIEM/EDR:
- Identify who/what is affected (user, host, network, cloud)
- Understand the specific action described in the alert
- Review surrounding events for suspicious activity nearby
- Cross-check with threat intel where useful
Some teams provide **workbooks/playbooks/runbooks** to standardise this 
step for common alert types.
 
**3. Final Actions**
Decide **True Positive** or **False Positive**, write a comment 
explaining the reasoning, and close the alert.
 
---
 
## Key Terms
 
| Term | Definition |
|---|---|
| Event | A single occurrence logged by a system (login, process, etc.) |
| Alert | A notification generated when logs match a detection rule |
| Alert triage | Process of reviewing, investigating, and closing an alert |
| True Positive | Alert correctly identifies real malicious activity |
| False Positive | Alert fires but there is no real threat |
| Workbook/Playbook | Standardised investigation instructions for an alert type |
 
---
 
## Personal Takeaways
 
- Alerts exist purely to make an impossible volume of logs manageable — 
  triage is the human filter after the automated one
- Severity and age of an alert are both good proxies for urgency — 
  older alerts mean the attacker has had more time inside
- Workbooks matter a lot for L1 consistency — without them, triage 
  quality depends heavily on individual analyst experience
- A closed alert is only as good as the comment behind it — the 
  reasoning matters as much as the verdict
---
*Previous: Systems as Attack Vectors*  
*Next: SOC L1 Alert Reporting*
