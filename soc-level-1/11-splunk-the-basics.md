# Room 11 — Splunk: The Basics

**Path:** SOC Level 1 — Core SOC Solutions

**Platform:** TryHackMe

---

## Core Concept

Splunk is a SIEM platform used to collect, process, search, analyze, and visualize machine-generated data.

SOC analysts use Splunk to investigate logs, search for suspicious activity, analyze security events, and create dashboards.

**Basic Splunk Flow:**

`Log Sources → Forwarder → Indexer → Search Head → SOC Analyst`

---

## Splunk Components

Splunk has three main components:

| Component | Purpose |
|---|---|
| Forwarder | Collects and sends logs |
| Indexer | Processes, indexes, and stores logs |
| Search Head | Searches, analyzes, and visualizes data |

**Memory Trick:** `Collect → Store → Search`

---

## Splunk Forwarder

The **Forwarder** is a lightweight agent installed on endpoints.

Its main tasks are:

- Collect logs from data sources
- Send logs to the Splunk Indexer
- Use minimal system resources

Common data sources include:

- Windows Event Logs
- PowerShell and Sysmon logs
- Linux logs
- Web server logs
- Database logs

**Flow:**

`Log Source → Forwarder → Indexer`

---

## Splunk Indexer

The **Indexer** receives data and prepares it for searching.

Its main tasks are:

- Receive logs from Forwarders
- Parse incoming data
- Extract fields
- Organize data into events
- Index and store events

**Simple Flow:**

`Raw Logs → Processing → Indexed Events → Searchable Data`

---

## Splunk Search Head

The **Search Head** is the interface used by SOC analysts to search and analyze indexed data.

Analysts use **SPL (Search Processing Language)** to perform searches.

**Search Flow:**

`SOC Analyst → Search Head → Indexer → Matching Events Returned`

The Search Head can display results as:

- Tables
- Reports
- Pie charts
- Bar charts
- Dashboards

---

## Splunk Interface

The Splunk home page contains several important sections.

### Splunk Bar

The top navigation bar provides access to:

- **Messages** — System notifications
- **Settings** — Splunk configuration
- **Activity** — Search jobs and processes
- **Help** — Documentation and tutorials
- **Find** — Search within Splunk
- **Apps** — Switch between installed applications

### Apps Panel

Displays applications installed in the Splunk instance.

The default application is:

**Search & Reporting**

This is the main application used to search and investigate logs.

### Explore Splunk

Provides quick access to:

- Add Data
- Install Splunk Apps
- Splunk Documentation

### Home Dashboard

Displays selected dashboards.

Users can:

- View existing dashboards
- Create custom dashboards
- Add dashboards to the home page
- Access personal dashboards

---

## Log Ingestion in Splunk

**Log ingestion means getting logs into Splunk so they can be processed, stored, searched, and analyzed.**

**Simple Example:**

`VPN Log File → Upload to Splunk → Process & Index → Search and Analyze`

Splunk can ingest data from:

- Event logs
- VPN logs
- Web server logs
- Firewall logs
- Application logs
- JSON files
- Syslog data

---

## Uploading Data into Splunk

The room used VPN logs to practice manual log ingestion.

The upload process contains five steps:

`Select Source → Select Source Type → Input Settings → Review → Done`

### 1. Select Source

Choose the log file or data source.

### 2. Select Source Type

Tell Splunk what type of data is being uploaded.

Examples:

- JSON
- Syslog
- CSV

### 3. Input Settings

Configure where the events will be stored.

Important settings include:

- Index
- Hostname

### 4. Review

Check the configuration before uploading.

### 5. Done

Complete the upload.

The data is now indexed and ready for analysis.

---

## Important Splunk Terms

### Event

An **event** is a single record of activity stored in Splunk.

Examples:

- VPN connection attempt
- User login
- Process execution
- Firewall connection

### Field

A **field** is a named value extracted from an event.

Example:

`UserName = Maleena`

`Source_ip = 107.14.182.38`

`Source_Country = France`

Fields make logs easier to search and filter.

### Index

An **index** is where Splunk stores processed events.

In this room, VPN logs were stored in:

`VPN_Logs`

---

## Basic SPL Searches

Search all events stored in the VPN index:

```spl
index=VPN_Logs
```

Count the total number of events:

```spl
index=VPN_Logs
| stats count
```

---

## Parsing JSON with `spath`

The VPN log file contains JSON data.

If Splunk does not automatically display the JSON fields, use:

```spl
index=VPN_Logs
| spath
```

`spath` extracts fields from structured data such as JSON.

---

## Searching by Username

Search for VPN activity associated with a specific user:

```spl
index=VPN_Logs
| spath
| search UserName="Maleena"
```

Count the matching events:

```spl
index=VPN_Logs
| spath
| search UserName="Maleena"
| stats count
```

---

## Searching by Source IP

Search for events from a specific source IP:

```spl
index=VPN_Logs
| spath
| search Source_ip="107.14.182.38"
```

Find users associated with the IP:

```spl
index=VPN_Logs
| spath
| search Source_ip="107.14.182.38"
| stats values(UserName) as UserName count
```

---

## Excluding Values

Search for VPN connections where the source country is not France:

```spl
index=VPN_Logs
| spath
| search Source_Country!="France"
| stats count
```

The `!=` operator means **not equal to**.

---

## Investigating a Specific IP

Count how many events are associated with an IP address:

```spl
index=VPN_Logs
| spath
| search Source_ip="107.3.206.58"
| stats count
```

---

## Useful SPL Commands

| Command | Purpose |
|---|---|
| `search` | Filters events based on conditions |
| `stats count` | Counts matching events |
| `spath` | Extracts fields from JSON data |
| `values(field)` | Displays unique values of a field |
| `!=` | Excludes a specific value |

---

## Example Investigation Workflow

Suppose a SOC analyst receives an alert about a suspicious IP address.

The investigation may follow:

`Search IP → Review Events → Identify User → Check Connection Activity → Analyze Location → Determine Verdict`

Example:

```spl
index=VPN_Logs
| spath
| search Source_ip="107.14.182.38"
| stats values(UserName) as UserName count
```

This search identifies which users are associated with the IP address and how many matching events occurred.

---

## Why Splunk is Useful for SOC Analysts

Splunk helps SOC analysts:

- Search large amounts of log data
- Investigate security alerts
- Filter events using fields
- Search for suspicious users and IP addresses
- Correlate activity across multiple systems
- Identify patterns in security events
- Create reports and dashboards

---

## Key Terms

| Term | Definition |
|---|---|
| Splunk | Platform used to collect, search, analyze, and visualize machine data |
| Forwarder | Lightweight agent that collects and sends logs |
| Indexer | Processes, indexes, and stores events |
| Search Head | Interface used to search and analyze indexed data |
| SPL | Search Processing Language |
| Event | Single record of activity stored in Splunk |
| Field | Named value extracted from an event |
| Index | Storage location for processed events |
| Log Ingestion | Process of getting logs into Splunk |
| `spath` | SPL command used to extract fields from structured data |

---

## Personal Takeaways

- Splunk follows a simple architecture: Forwarder collects logs, Indexer processes and stores them, and Search Head allows analysts to investigate the data.
- Log ingestion means getting security data into Splunk so it can be indexed and analyzed.
- SPL allows analysts to search large amounts of data for specific users, IP addresses, and events.
- Fields turn raw logs into searchable information and make investigations easier.
- Commands such as `search`, `stats`, `values()`, and `spath` are useful for basic log investigations.
- For SOC analysts, understanding how to investigate logs is more important than memorizing SPL commands.

---

*Previous: Introduction to SIEM*  
*Next: Elastic Stack — The Basics*
