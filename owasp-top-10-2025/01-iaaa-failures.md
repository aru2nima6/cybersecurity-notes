# OWASP Top 10 2025 — IAAA Failures

**Module:** OWASP Top 10 2025

**Platform:** TryHackMe

---

## Core Concept

The **OWASP Top 10** is a list of the most important security risk categories affecting web applications.

It is published by the **Open Worldwide Application Security Project (OWASP)** to help developers, security professionals, and organizations understand common web application security risks and build more secure applications.

The OWASP Top 10 does not list individual vulnerabilities. Instead, it groups similar vulnerabilities and weaknesses into broad security risk categories.

**Simple Example:**

`IDOR Vulnerability → Broken Access Control Category`

`SQL Injection Vulnerability → Injection Category`

`Weak Login Mechanism → Authentication Failures Category`

---

## Why OWASP Top 10 Matters

Security professionals use the OWASP Top 10 for:

- Understanding common web application security risks
- Web application security assessments
- Penetration testing
- Secure application development
- Vulnerability management
- Security awareness and training

For SOC analysts, OWASP knowledge helps with:

- Recognizing common web application attacks
- Understanding WAF, IDS/IPS, and SIEM alerts
- Investigating suspicious web requests
- Analyzing authentication-related activity
- Understanding the impact of web vulnerabilities
- Communicating with penetration testers and developers

---

## OWASP Top 10 2025 Categories

| Category | Security Risk |
|---|---|
| A01 | Broken Access Control |
| A02 | Security Misconfiguration |
| A03 | Software Supply Chain Failures |
| A04 | Cryptographic Failures |
| A05 | Injection |
| A06 | Insecure Design |
| A07 | Authentication Failures |
| A08 | Software or Data Integrity Failures |
| A09 | Logging & Alerting Failures |
| A10 | Mishandling of Exceptional Conditions |

---

## Categories Covered in This Room

This room focuses on three OWASP Top 10 2025 categories related to failures in **Identity, Authentication, Authorisation, and Accountability (IAAA)**:

- **A01: Broken Access Control**
- **A07: Authentication Failures**
- **A09: Logging & Alerting Failures**

Weaknesses in these areas can allow attackers to access unauthorized data, compromise accounts, gain additional privileges, or perform malicious activity without being detected.

---

## IAAA Overview

**IAAA** stands for:

**Identity → Authentication → Authorisation → Accountability**

These concepts describe how applications identify users, verify them, control their permissions, and record their actions.

| Concept | Purpose |
|---|---|
| Identity | Identifies who the user or service is |
| Authentication | Verifies the claimed identity |
| Authorisation | Determines what the user is allowed to access |
| Accountability | Records and monitors user actions |

**Simple Flow:**

`Who are you? → Prove it → What can you access? → What did you do?`

Each stage depends on the previous one being correctly implemented.

---

# A01 — Broken Access Control

## Core Concept

Broken Access Control occurs when an application fails to properly enforce what authenticated users are allowed to access or modify.

The server should verify the user's permissions every time a protected resource is requested.

If the application trusts user-controlled parameters without checking authorization, attackers may access other users' data or privileged functionality.

---

## Insecure Direct Object Reference (IDOR)

**IDOR (Insecure Direct Object Reference)** is a common example of Broken Access Control.

Consider the following URL:

```text
/account?id=7
```

The user changes the ID:

```text
/account?id=6
```

If the server returns another user's account information without checking whether the logged-in user is authorized to access it, the application is vulnerable.

**Attack Flow:**

`Login as Normal User → Change Object ID → Access Another User's Data`

Changing an ID itself is not the vulnerability.

The vulnerability exists because the server fails to verify whether the user is authorized to access the requested resource.

---

## Privilege Escalation

Broken Access Control can result in two types of privilege escalation.

### Horizontal Privilege Escalation

A user accesses another user's resources while remaining at the same privilege level.

**Example:**

`User A → Changes Account ID → Accesses User B's Account`

### Vertical Privilege Escalation

A normal user gains access to functionality intended for higher-privileged users.

**Example:**

`Normal User → Accesses Admin Functionality`

---

## Preventing Broken Access Control

- Enforce authorization checks on the server side
- Verify permissions for every protected request
- Deny access by default
- Do not trust user-controlled parameters
- Implement Role-Based Access Control (RBAC)
- Prevent users from accessing unauthorized objects
- Log and monitor access control failures

---

# A07 — Authentication Failures

## Core Concept

Authentication Failures occur when an application cannot securely verify a user's identity or properly manage authenticated sessions.

Successful exploitation may allow attackers to access another user's account.

---

## Common Authentication Weaknesses

Examples include:

- Username enumeration
- Weak or guessable passwords
- Missing rate limiting
- Missing account lockout
- Login logic flaws
- Registration logic flaws
- Insecure session management
- Insecure cookie handling

---

## Authentication Logic Flaw Example

The room demonstrated a vulnerability involving inconsistent username handling.

Existing account:

```text
admin
```

Attacker registers:

```text
aDmiN
```

If the application treats usernames differently during registration and authentication, an attacker may exploit this logic flaw to gain unauthorized access.

Applications should convert usernames into a consistent **canonical form** before comparing or storing them.

**Simple Concept:**

`admin ≠ aDmiN during registration`

`admin = aDmiN during authentication`

`Inconsistent Validation → Authentication Bypass`

---

## Preventing Authentication Failures

- Enforce strong password policies
- Implement Multi-Factor Authentication (MFA)
- Apply rate limiting to login attempts
- Temporarily restrict accounts after repeated failures
- Prevent username enumeration
- Validate login and registration logic
- Securely manage sessions and cookies
- Rotate session identifiers after login
- Rotate sessions after password or privilege changes
- Enforce consistent username handling

---

# A09 — Logging & Alerting Failures

## Core Concept

Logging & Alerting Failures occur when applications do not properly record, monitor, or alert on security-related activities.

Without sufficient logging, security teams may be unable to detect attacks or reconstruct incidents.

**Simple Concept:**

`Attack Happens → No Logs → No Alert → SOC Cannot Investigate`

Logging supports **Accountability** because it allows security teams to determine who performed an action, what happened, when it happened, and where the activity originated.

---

## Security Events That Should Be Logged

Applications should record important security events such as:

- Successful login attempts
- Failed login attempts
- Password changes
- MFA changes
- Role and privilege changes
- Administrative actions
- Access control failures
- Suspicious authentication activity

Good security logs should help answer:

`Who → Did What → When → From Where`

---

## Common Logging & Alerting Failures

Examples include:

- Authentication events are not logged
- Logs contain insufficient investigation context
- No alerts for repeated failed login attempts
- No alerts for privilege changes
- Logs are stored only on the application server
- Attackers can modify or delete logs
- Logs are deleted too quickly
- No centralized log monitoring
- Security teams are not alerted about suspicious activity

---

## Preventing Logging & Alerting Failures

- Log the complete authentication lifecycle
- Record administrative actions
- Record privilege and role changes
- Centralize logs away from application servers
- Protect logs from unauthorized modification
- Define appropriate log retention periods
- Continuously monitor security logs
- Create alerts for suspicious behavior

**Example Alerts:**

`Multiple Failed Logins → Possible Brute Force Attack`

`Successful Login After Multiple Failures → Possible Account Compromise`

`Unexpected Privilege Change → Possible Privilege Escalation`

`Repeated Access Control Failures → Possible Unauthorized Access Attempt`

---

## How the Three Categories Connect

These vulnerabilities can appear together during an attack.

```text
Authentication Failure
        ↓
Attacker Gains Account Access
        ↓
Broken Access Control
        ↓
Attacker Accesses Unauthorized Resources
        ↓
Logging & Alerting Failure
        ↓
Attack Remains Undetected
```

This demonstrates why Identity, Authentication, Authorisation, and Accountability must work together.

---

## SOC Analyst Investigation Perspective

Understanding OWASP vulnerabilities helps SOC analysts know what suspicious activity to search for in logs and SIEM alerts.

### Broken Access Control Indicators

Look for:

- Users accessing unusual resources
- Repeated requests using different object IDs
- Normal users accessing administrative endpoints
- Large numbers of authorization failures
- Access to resources outside a user's normal permissions

### Authentication Failure Indicators

Look for:

- Multiple failed login attempts
- Successful login after repeated failures
- Logins from unusual IP addresses
- Logins from unusual geographic locations
- Unexpected session activity
- Multiple accounts accessed from the same suspicious IP
- Account takeover indicators

### Logging & Alerting Failure Indicators

Check whether:

- Important security events are recorded
- Logs contain sufficient investigation context
- Logs are centrally collected
- Logs are protected from modification
- Appropriate alerts are configured
- Logs are retained long enough for investigations

---

## Example SOC Investigation Flow

Suppose the SIEM generates an alert for repeated failed login attempts.

The investigation may follow:

```text
Alert Triggered
      ↓
Identify User and Source IP
      ↓
Review Failed Login Attempts
      ↓
Check for Successful Login
      ↓
Review Resources Accessed
      ↓
Check for Privilege Changes
      ↓
Search for Related Activity
      ↓
Determine True Positive or False Positive
      ↓
Escalate or Close Alert
```

Understanding authentication failures and access control vulnerabilities helps the analyst understand the possible impact of the activity.

---

## Key Terms

| Term | Definition |
|---|---|
| OWASP | Open Worldwide Application Security Project |
| OWASP Top 10 | List of major web application security risk categories |
| IAAA | Identity, Authentication, Authorisation, and Accountability |
| Identity | Unique account representing a user or service |
| Authentication | Process of verifying identity |
| Authorisation | Determining what an authenticated user can access |
| Accountability | Recording and monitoring user actions |
| Broken Access Control | Failure to properly restrict access to resources |
| IDOR | Accessing unauthorized objects by manipulating identifiers |
| Horizontal Privilege Escalation | Accessing another user's resources |
| Vertical Privilege Escalation | Gaining higher-level permissions |
| Authentication Failure | Weakness that allows authentication or session controls to be bypassed |
| Logging & Alerting Failure | Failure to properly record, monitor, or alert on security events |
| RBAC | Role-Based Access Control |
| MFA | Multi-Factor Authentication |
| Canonical Form | Standardized representation of input used for consistent comparison |

---

## Personal Takeaways

- The OWASP Top 10 groups common web application vulnerabilities into major security risk categories.
- Understanding OWASP vulnerabilities is useful for SOC analysts because web attacks generate evidence in application logs, authentication logs, web server logs, WAF alerts, and SIEM systems.
- Identity determines who the user is, authentication verifies the identity, authorisation controls what the user can access, and accountability records what the user does.
- Broken Access Control occurs when the server fails to properly enforce authorization checks.
- IDOR demonstrates why changing an identifier should never allow a user to access another user's resources without server-side permission checks.
- Authentication Failures can involve weak passwords, missing rate limits, insecure sessions, and flaws in login or registration logic.
- Proper logging and alerting are essential for detecting attacks and reconstructing incidents.
- From a SOC perspective, understanding the connection between authentication, access control, and logging helps analysts investigate alerts and determine the potential impact of suspicious activity.

---

*Module: OWASP Top 10 2025*

*Room Topics: Broken Access Control | Authentication Failures | Logging & Alerting Failures*
