# Room 06 — SOC L1 Alert Reporting

**Path:** SOC Level 1 — SOC Team Internals

**Platform:** TryHackMe  
 
---
 
## Core Concept
 
Classifying an alert as True or False Positive isn't the end of 
the job. Real threats need to be **reported** clearly and 
**escalated** to L2 — and sometimes L1 needs to **communicate** with 
other departments to get the context needed to make a verdict.
 
---
 
## The Alert's Journey
 
L1 receives alerts in a SIEM/EDR/ticketing platform → most are 
closed as False Positives or handled at L1 → complex/threatening 
ones are escalated to L2, who handle most remediation.
 
Three concepts drive that handoff:
- **Reporting** — documenting the investigation
- **Escalation** — passing a confirmed threat to L2
- **Communication** — looping in other teams when needed
---
 
## Why L1 Reports Matter
 
| Purpose | Explanation |
|---|---|
| Context for escalation | Saves L2 time — they don't start from scratch |
| Long-term record | Raw logs expire in 3–12 months, but alerts (with your report) are kept indefinitely |
| Skill building | Writing a clear report forces you to actually understand the alert |
 
---
 
## Report Format — The 5 Ws
 
A good report should answer:
 
- **Who** — user/account involved
- **What** — exact action or event sequence
- **When** — start and end of the suspicious activity
- **Where** — device, IP, or site involved
- **Why** — the reasoning behind your final verdict (the most important one)
---
 
## When to Escalate to L2
 
Escalate if:
1. It looks like a major attack needing deeper investigation/DFIR
2. Remediation is needed (malware removal, host isolation, password reset)
3. Other parties need to be looped in (customers, management, law enforcement)
4. You're unsure and need senior input
---
 
## Escalation Steps
 
1. Move alert to **In Progress**, do the analysis
2. Write the report, set a verdict (e.g. True Positive)
3. Reassign to the L2 on shift if escalation is needed
4. L2 reviews your report, may ask questions, then validates, 
   communicates further if needed, and starts formal Incident 
   Response for major cases
Asking L2 for help when unsure is normal and expected — better than 
closing an alert you don't fully understand.
 
---
 
## Communication Cases to Know
 
| Situation | What to do |
|---|---|
| Critical alert, L2 unresponsive for 30 min | Escalate up the chain — L2 → L3 → manager |
| Suspected compromised Slack/Teams account | Verify with the user via a separate channel, not the compromised one |
| Sudden flood of alerts, some critical | Prioritise per normal workflow, but flag the situation to L2 |
| Realise a past alert was misclassified | Report it to L2 immediately — attackers can stay dormant before acting |
| Logs not parsing/searchable in the SIEM | Don't skip the alert — investigate what's possible, flag to L2/SOC engineer |
 
---
 
## Key Terms
 
| Term | Definition |
|---|---|
| Alert report | Documented investigation and reasoning behind a verdict |
| Escalation | Passing a confirmed/uncertain alert to L2 for deeper action |
| 5 Ws | Who, What, When, Where, Why — structure for a good report |
| DFIR | Digital Forensics and Incident Response |
| Crisis Communication procedure | Predefined team process for handling urgent/unclear situations |
 
---
 
## Personal Takeaways
 
- A report is really written for your future self and for L2 — 
  "why" is the part that actually carries weight, not just the verdict
- Escalation isn't a failure to solve it yourself — it's part of the 
  process, and asking early is better than closing something wrong
- Communication during a compromise needs to assume the compromised 
  channel itself isn't trustworthy (e.g. don't verify a hacked 
  Slack account over Slack)
- Even messy situations (broken logs, alert floods, missed alerts) 
  have a "don't just stay silent" answer — report the issue upward
---
*Previous: SOC L1 Alert Triage*  
*Next: SOC Workbooks and Lookups*
 
