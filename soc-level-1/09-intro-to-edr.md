# Room 09 — Introduction to EDR

**Path:** SOC Level 1 — Core SOC Solutions

**Platform:** TryHackMe

---

## Core Concept

Endpoint Detection and Response (EDR) is a security solution that continuously monitors endpoints, detects advanced threats, and allows SOC analysts to investigate and respond to malicious activity.

The three main pillars of EDR are:

**Visibility → Detection → Response**

---

## Why EDR is Needed

Traditional antivirus mainly detects known threats using signatures. EDR provides deeper endpoint monitoring and can detect advanced threats based on suspicious behavior.

EDR continuously protects endpoints such as laptops, workstations, and servers, even when they are outside the corporate network.

---

## Three Pillars of EDR

| Pillar | Purpose |
|---|---|
| Visibility | Collect detailed endpoint activity |
| Detection | Identify known and advanced threats |
| Response | Contain and remediate detected threats |

### Visibility

EDR collects detailed endpoint activity such as:

- Process executions and process trees
- Network connections
- File and folder modifications
- Registry changes
- User activities

This helps analysts reconstruct attack timelines and investigate the complete chain of events.

### Detection

EDR uses multiple detection techniques:

- Signature-based detection
- Behavioral detection
- Anomaly detection
- IOC matching
- MITRE ATT&CK mapping
- Machine learning

### Response

Analysts can respond directly from the EDR console by:

- Isolating infected hosts
- Terminating malicious processes
- Quarantining malicious files
- Remotely accessing endpoints
- Collecting forensic artefacts

---

## Antivirus vs EDR

A simple airport analogy explains the difference:

**Antivirus = Immigration Check**

Checks people against a list of known criminals and blocks known threats.

**EDR = Security Officers + CCTV**

Continuously monitors behavior inside the airport and detects suspicious activities even if someone bypasses immigration.

| Antivirus | EDR |
|---|---|
| Mainly detects known threats | Detects known and advanced threats |
| Relies heavily on signatures | Uses signatures and behavior analysis |
| Limited endpoint visibility | Collects detailed endpoint telemetry |
| Limited investigation context | Provides complete attack timelines |
| Mainly focused on prevention | Provides detection and response |

**Memory Trick:** `AV = Who are you? | EDR = What are you doing?`

---

## Example Attack Chain

Consider the following attack:

`Phishing Document → Malicious Macro → PowerShell → Payload Download → Process Injection → C2 Communication`

EDR may detect suspicious behavior such as:

- `winword.exe` spawning `powershell.exe`
- Obfuscated PowerShell commands
- Process injection into `svchost.exe`
- Unexpected outbound network connections

The SOC analyst receives an alert containing the attack context and timeline.

---

## EDR Architecture

`Endpoints → EDR Agents/Sensors → Central EDR Console → SOC Analyst`

### EDR Agent / Sensor

A lightweight agent installed on endpoints that:

- Monitors endpoint activity
- Collects telemetry
- Performs basic detections
- Sends data to the central console

### EDR Console

The centralized platform that:

- Receives telemetry from endpoints
- Correlates and analyzes activities
- Uses threat intelligence and detection logic
- Generates alerts
- Allows analysts to investigate and respond

---

## Endpoint Telemetry

**Telemetry** is the detailed activity data collected from endpoints by EDR agents.

| Telemetry Type | Helps Detect |
|---|---|
| Process Activity | Suspicious processes and parent-child relationships |
| Network Connections | C2 communication, exfiltration, lateral movement |
| Command-Line Activity | Malicious CMD and PowerShell commands |
| File Modifications | Malware drops, ransomware, data staging |
| Registry Changes | Persistence and system configuration changes |

Detailed telemetry helps analysts understand the root cause and reconstruct the attack timeline.

---

## EDR Detection Techniques

### Behavioral Detection

Detects suspicious behavior instead of relying only on known signatures.

**Example:** `winword.exe → powershell.exe`

### Anomaly Detection

Detects activity that differs from the normal behavior of an endpoint.

**Example:** Unexpected modification of an auto-start registry key.

### IOC Matching

Compares endpoint activity against known malicious IPs, domains, URLs, and file hashes.

### MITRE ATT&CK Mapping

Maps detected activity to attacker tactics and techniques.

**Example:**

`Scheduled Task Created → Persistence → Scheduled Task/Job`

### Machine Learning

Identifies complex attack patterns where individual actions may appear legitimate.

Useful for detecting fileless malware and multi-stage attacks.

---

## EDR Response Actions

| Action | Purpose |
|---|---|
| Isolate Host | Disconnect compromised endpoint to prevent spread |
| Terminate Process | Stop a malicious running process |
| Quarantine File | Prevent a malicious file from executing |
| Remote Access | Investigate and perform actions remotely |
| Collect Artefacts | Gather evidence for forensic investigation |

Common collected artefacts include memory dumps, event logs, registry hives, and folder contents.

---

## Alert Investigation Workflow

`Alert Triggered → Check Severity → Review Telemetry → Analyze Attack Chain → True/False Positive → Respond`

The analyst examines processes, files, network connections, registry activity, and other telemetry to determine whether the alert represents legitimate or malicious activity.

---

## EDR in the Security Ecosystem

EDR focuses on endpoint activity and works alongside other security solutions such as:

- SIEM -Security Information and Event Management
- Firewalls
- Email Security Gateways
- DLP — Data Loss Prevention
- IAM — Identity and Access Management

These security tools can be integrated with SIEM to provide broader visibility and centralized investigation.

---

## Key Terms

| Term | Definition |
|---|---|
| EDR | Endpoint Detection and Response |
| Endpoint | Laptop, workstation, or server being monitored |
| Agent/Sensor | Software installed on endpoints to collect activity |
| Telemetry | Detailed endpoint activity collected by EDR |
| IOC | Indicator of Compromise |
| C2 | Command and Control communication |
| Process Tree | Parent-child relationship between running processes |
| Host Isolation | Disconnecting an endpoint from the network |
| Quarantine | Preventing a suspicious file from executing |

---

## Personal Takeaways

- EDR goes beyond antivirus by continuously monitoring endpoint behavior.
- Detailed telemetry helps analysts reconstruct the complete attack chain.
- Suspicious parent-child processes can help detect advanced attacks.
- EDR allows analysts to investigate alerts and take direct response actions.
- EDR works alongside SIEM and other security tools to provide broader visibility.

---

*Previous: SOC Metrics and Objectives*  
*Next: Introduction to SIEM *
