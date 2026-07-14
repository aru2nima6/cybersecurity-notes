# Room 07 — SOC Workbooks and Lookups

**Path:** SOC Level 1 — SOC Team Internals

**Platform:** TryHackMe  


---

## Core Concept

Alert triage often needs more than the alert itself — you need 
context about the user, the host, and the network involved. This 
room covers **identity inventory**, **asset inventory**, **network 
diagrams**, and **workbooks** as the tools that provide that context 
and standardise the investigation.

---

## The Problem

An alert like "G.Baker logged into HQ-FINFS-02 and downloaded a 
financial file, then shared it with R.Lund" raises questions that 
the alert alone can't answer:

- Who is G.Baker — role, working hours?
- What is HQ-FINFS-02, and who's allowed to access it?
- Why would R.Lund need that file?

Answering these needs lookups into identity data, asset data, and 
sometimes the network layout.

---

## Identity Inventory

A catalogue of employees and service accounts, with details like 
role, privileges, and contact info. Helps confirm whether a user's 
activity matches their normal role.

| Source | Examples | Notes |
|---|---|---|
| Active Directory | On-prem AD, Entra ID | Common identity database for SOC use |
| SSO Providers | Okta, Google Workspace | Cloud alternative to AD |
| HR Systems | BambooHR, SAP, HiBob | Employee-only, but full profile data |
| Custom Solution | CSV/Excel sheets | Common for smaller IT/security teams |

---

## Asset Inventory

A list of computing resources (servers, workstations) in the 
environment — helps confirm what a given host is for and who should 
be accessing it.

| Source | Examples | Notes |
|---|---|---|
| Active Directory | On-prem AD, Entra ID | Also works as an asset database |
| SIEM/EDR | Elastic, CrowdStrike | Agents often collect host info |
| MDM Solution | MS Intune, Jamf | Purpose-built for asset management |
| Custom Solution | CSV/Excel sheets | Same as identity inventory |

---

## Network Diagrams

A visual map of subnets, locations, and how they connect. Useful 
when triaging alerts involving IPs, especially firewall/network 
logs, to understand *why* a connection between two points is or 
isn't expected.

**Example reconstruction using a diagram:**
1. External IP repeatedly hits the firewall on a VPN port → brute force attempt
2. Successful login → attacker gets an internal IP from the VPN subnet
3. Attacker scans the Database subnet → blocked by firewall rules
4. Attacker pivots to scan the Office subnet → looking for a weaker target

Without the diagram, the IPs and subnets are just numbers — with it, 
the attack path makes sense.

---

## SOC Workbooks

Also called **playbooks**, **runbooks**, or **workflows** — a 
structured, step-by-step guide for investigating a specific type of 
alert. Written by senior analysts to keep L1 triage consistent and 
reduce mistakes, since L1s aren't expected to know every scenario 
from experience alone.

**Typical workbook structure (e.g. "Unusual Login Location"):**

1. **Enrichment** — pull context from threat intel and identity inventory
2. **Investigation** — check SIEM logs, decide if the login is expected
3. **Escalation** — escalate to L2 or contact the user directly if needed

---

## Key Terms

| Term | Definition |
|---|---|
| Identity inventory | Catalogue of user/service accounts and their details |
| Asset inventory | Catalogue of servers/workstations in the environment |
| Network diagram | Visual map of subnets and how they connect |
| Workbook/Playbook/Runbook | Standardised step-by-step alert investigation guide |
| Enrichment | Gathering supporting context before making a verdict |

---

## Personal Takeaways

- Most triage delays come from not having quick access to identity/asset 
  context — inventories exist to remove that bottleneck
- Network diagrams turn a list of IPs into an actual story — without 
  one, lateral movement between subnets is easy to miss
- Workbooks are what make L1 triage consistent across a whole team, 
  not just dependent on one analyst's experience
- Enrichment → Investigation → Escalation is a clean mental model 
  that applies beyond just login alerts

---
*Previous: SOC L1 Alert Reporting*  
*Next: SOC Metrics and Objectives*
