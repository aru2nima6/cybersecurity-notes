# Room 05 — SOC L1 Alert Triage
**Path:** SOC Level 1 — SOC Team Internals
**Platform:** TryHackMe  

---

## Core Concept

A SOC does not have the time or manpower to investigate every alert 
in full depth. **Triage** is the process of quickly sorting incoming 
alerts by severity and likelihood so analysts spend their limited 
time on the alerts that actually matter — without missing a real 
attack buried in the noise.

---

## Why Triage Matters

- A busy SOC can receive **thousands of alerts per day**
- Most alerts are false positives or low-risk noise
- Analysts have limited time — triage decides **what gets looked 
  at first, and what gets looked at at all**
- Poor triage leads to either alert fatigue (missing real attacks) 
  or wasted effort (chasing noise)

---

## The Triage Process

A systematic approach to handling an alert as it comes in:

1. **Initial review** — read the alert, understand what triggered it
2. **Categorize** — what type of alert is this (malware, login 
   anomaly, network scan, etc.)?
3. **Assess severity/priority** — how dangerous or urgent is this, 
   based on asset criticality and potential impact?
4. **Gather context** — pull in supporting data (logs, asset info, 
   user info, threat intel) to judge if it's real
5. **Decide** — close as false positive, escalate for deeper 
   investigation, or declare an incident

---

## Key Factors in Prioritization

| Factor | Why it matters |
|---|---|
| Asset criticality | An alert on a domain controller matters more than one on a test machine |
| Alert severity/confidence | How confident is the detection rule that this is malicious? |
| Potential impact | Data loss, downtime, financial/reputational damage if real |
| Threat intelligence match | Does this match a known IOC, campaign, or TTP? |
| Frequency/pattern | Is this a one-off, or part of a recurring/escalating pattern? |

---

## False Positives vs True Positives

| Term | Meaning |
|---|---|
| False Positive (FP) | Alert fired but there was no actual malicious activity |
| True Positive (TP) | Alert fired and it correctly identified malicious activity |
| False Negative (FN) | Malicious activity occurred but no alert fired |
| True Negative (TN) | No malicious activity, and correctly no alert fired |

**Goal of tuning detections:** reduce false positives without 
increasing false negatives — a hard balance to strike.

---

## The 5 Ws (Triage Questions)

When triaging, an analyst should be able to answer:

- **Who** — who/what is involved (user, host, IP)?
- **What** — what happened / what triggered the alert?
- **When** — what is the timeline of events?
- **Where** — where in the environment did this occur?
- **Why** — why did this trigger — is it explainable/benign, or 
  suspicious?

---

## Key Terms

| Term | Definition |
|---|---|
| Triage | Process of sorting and prioritizing alerts by severity/urgency |
| False positive | An alert that fired without real malicious activity |
| True positive | An alert that correctly identified malicious activity |
| Alert fatigue | Analyst desensitization caused by too many low-value alerts |
| IOC | Indicator of Compromise — evidence suggesting a system was breached |
| TTP | Tactics, Techniques, and Procedures used by an attacker |

---

## Personal Takeaways

- Triage is really about **time management under pressure** — not 
  every alert deserves the same attention
- Asset criticality changes everything — the same alert type can be 
  a non-issue on one host and a critical incident on another
- Answering the 5 Ws quickly is a good mental checklist to avoid 
  jumping to conclusions too early
- Alert fatigue is a real risk — tuning out noise carefully matters 
  as much as catching the real threats

---
*Previous: Systems as Attack Vectors*  
*Next: SOC L1 Alert Reporting*
