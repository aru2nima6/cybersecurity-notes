
# Room 03 — Humans as Attack Vectors
**Path:** SOC Level 1
**Platform:** TryHackMe  
**Date completed:** 11/06/2026

---

## Core Concept — Humans as the Weakest Link

Instead of breaking through the door (technical attack), attackers 
manipulate the gatekeeper (human) into opening it willingly.

---

## Threat Actors

Anyone who intentionally causes harm to systems or data.
- Some have a clear goal, some breach first and decide later
- Types: script kiddies, hacktivists, cybercriminals, insiders, 
  nation-state actors, APT groups

---

## Social Engineering

Manipulating human psychology to gain access or information.

Exploits: **authority, urgency, fear, trust, curiosity**

---

## Phishing

Fraudulent messages tricking victims into revealing credentials 
or downloading malware.

| Type | Method |
|---|---|
| Email phishing | Fake emails — most common |
| Spear phishing | Targeted at a specific person |
| Whaling | Targets executives specifically |
| Smishing | Via SMS |
| Vishing | Via voice call |

---

## Malware Downloads

Phishing emails deliver malware through attachments or links.  
Common payloads: ransomware, keyloggers, RATs, stealers.

---

## SEO Poisoning - Search Engine Optimization Poisoning

Attackers push fake malicious websites to the top of search results.  
Victim searches for legitimate software → downloads malware instead.

---

## Deepfakes

AI-generated fake audio/video used to impersonate real people.

**Real example:** Finance employee transferred **$25 million** after 
receiving a fake video call that looked exactly like their boss.

**Defence:** Always verify large requests through a second 
independent channel — never trust face or voice alone.

---

## Impersonation

Pretending to be IT support, an executive, a vendor, or a new 
employee to manipulate someone into giving access or money.

**Red flags:** unexpected urgency, unusual request, pressure 
not to verify.

---

## Mitigation

- Security awareness training and phishing simulations
- Multi-factor authentication (MFA)
- Email authentication — SPF, DKIM, DMARC
- Verification procedures for financial requests
- Principle of least privilege
- Safe incident reporting culture

---

## Detection (SOC perspective)

| Indicator | Possible meaning |
|---|---|
| Login from unusual IP/location | Stolen credentials |
| New email forwarding rule | Attacker maintaining access |
| Large unexpected file transfer | Data exfiltration |
| Malware alert after email opened | Successful phishing |
| Unusual financial transaction | BEC / deepfake fraud |

---

## Key Terms

| Term | Definition |
|---|---|
| Social engineering | Psychological manipulation to gain access |
| Phishing | Fake messages to steal credentials or deliver malware |
| SEO poisoning | Fake sites ranked high in search results |
| Deepfake | AI-generated fake video/audio |
| BEC | Business Email Compromise — executive impersonation fraud |
| MFA | Second layer of login verification |
| Least privilege | Users only access what they need |

---

## Personal Takeaways
- Technical defences fail if a human opens the door
- SEO poisoning — be careful where you download software from
- Deepfakes make even face verification unreliable
- After a human attack succeeds, SOC detects the aftermath — 
  unusual logins, transfers, mail rules

## Questions to research later
- [ ] How do SPF, DKIM, DMARC actually work?
- [ ] What does a BEC investigation look like in a SIEM?
- [ ] What deepfake detection tools exist?

---
*Previous: SOC Role in the Blue Team*  
*Next: Systems as Attack Vectors*
