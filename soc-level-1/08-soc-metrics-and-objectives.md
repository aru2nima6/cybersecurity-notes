# Room 08 — SOC Metrics and Objectives

**Path:** SOC Level 1 — SOC Team Internals

**Platform:** TryHackMe  


---

## Core Concept

The SOC's job is to protect confidentiality, integrity, and 
availability of digital assets — but how well it does that needs to 
be measurable. This room covers the core metrics (Alerts Count, FPR, 
AER, TDR, MTTD, MTTA, MTTR) used to evaluate SOC and L1 performance, 
and how to improve them.

---

## Alert-Level Metrics

| Metric | Formula | Measures |
|---|---|---|
| Alerts Count (AC) | Total alerts received | Overall analyst workload |
| False Positive Rate (FPR) | False Positives / Total Alerts | Noise level in alerts |
| Alert Escalation Rate (AER) | Escalated Alerts / Total Alerts | L1 experience/independence |
| Threat Detection Rate (TDR) | Detected Threats / Total Threats | Reliability of the SOC team |

### Alerts Count
Too many alerts (e.g. 80 unresolved) risks missing real threats in 
the noise. Too few can mean a visibility gap in the SIEM itself. A 
healthy range is roughly **5–30 alerts per day per L1 analyst**, 
depending on company size.

### False Positive Rate
High FPR (e.g. 94%) breeds complacency — analysts start treating 
everything as noise. 0% isn't realistic, but **80%+ is a serious 
problem**, usually fixed through detection rule tuning ("False 
Positive Remediation").

### Alert Escalation Rate
Measures how often L1 escalates instead of resolving independently. 
Target is generally **below 50%, ideally below 20%** — too high 
suggests inexperience or unclear workbooks.

### Threat Detection Rate
The share of real attacks actually detected and stopped. Unlike the 
others, **TDR should aim for 100%** — every missed threat is a 
potential major incident (e.g. ransomware, data exfiltration).

---

## Time-Based Metrics (SLA)

These sit under a **Service Level Agreement (SLA)** — a formal 
commitment between the SOC and the business (or an MSSP and its 
customers) on how fast threats get handled.

| Metric | Common SLA | Description |
|---|---|---|
| SOC Team Availability | 24/7 | SOC working schedule (8/5 vs 24/7) |
| Mean Time to Detect (MTTD) | 5 min | Time from attack to detection by tooling |
| Mean Time to Acknowledge (MTTA) | 10 min | Time for L1 to start triaging a new alert |
| Mean Time to Respond (MTTR) | 60 min | Time to actually contain/stop the breach |

**Timeline order:** attack → **MTTD** → alert created → **MTTA** → 
triage starts → **MTTR** → breach contained.

---

## Why Metrics Matter to L1

- They make the SOC more effective at stopping real attacks
- They're used to evaluate individual performance — directly tied to 
  career growth toward L2

---

## Improving the Metrics

| Issue | Recommendations |
|---|---|
| FPR over 80% | Exclude trusted/expected activity from detection rules; automate common alert triage via SOAR/scripts |
| MTTD over 30 min | Push SOC engineers to tune detection rule speed/frequency; verify logs are ingested in real-time |
| MTTA over 30 min | Ensure real-time analyst notifications; distribute the alert queue evenly across the shift |
| MTTR over 4 hours | Escalate confirmed threats to L2 quickly; keep documented playbooks for common attack scenarios |

---

## Key Terms

| Term | Definition |
|---|---|
| SLA | Service Level Agreement — formal target times for detection/response |
| MTTD | Mean Time to Detect |
| MTTA | Mean Time to Acknowledge |
| MTTR | Mean Time to Respond |
| FPR | False Positive Rate |
| AER | Alert Escalation Rate |
| TDR | Threat Detection Rate |

---

## Personal Takeaways

- Metrics aren't just management overhead — a high FPR or slow MTTA 
  is exactly the kind of thing an L1 would be first to notice day to day
- TDR is the one metric with no acceptable "good enough" below 
  100% — every other metric has a healthy range, this one doesn't
- Escalation rate cuts both ways — too high suggests inexperience, 
  but escalating when genuinely unsure is still the right call
- Improving these metrics is often about workflow/tooling fixes 
  (automation, real-time notifications, tuning), not just "try harder"

---
*Previous: SOC Workbooks and Lookups*  
*Next: Introduction to EDR*
