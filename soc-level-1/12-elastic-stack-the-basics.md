# Room 12 — Elastic Stack: The Basics

**Path:** SOC Level 1 — Core SOC Solutions

**Platform:** TryHackMe

---

## Core Concept

The Elastic Stack (ELK) is a collection of tools used to collect, process, store, search, analyze, and visualize large amounts of data.

Although ELK is not traditionally a SIEM, many SOC teams use it for security monitoring, log analysis, threat hunting, and investigations.

**Basic ELK Flow:**

`Endpoints → Beats → Logstash → Elasticsearch → Kibana → SOC Analyst`

---

## Elastic Stack Components

The Elastic Stack has four main components:

| Component | Purpose |
|---|---|
| Elasticsearch | Stores, searches, and analyzes data |
| Logstash | Collects, processes, and normalizes data |
| Beats | Lightweight agents that collect and send data |
| Kibana | Searches, investigates, and visualizes data |

**Memory Trick:** `Collect → Process → Store → Visualize`

---

## Elasticsearch

**Elasticsearch** is the search and analytics engine of the Elastic Stack.

Its main tasks are:

- Store data
- Search large amounts of data
- Analyze logs
- Correlate information
- Store JSON-formatted documents

**Simple Concept:**

`Processed Logs → Elasticsearch → Searchable Data`

---

## Logstash

**Logstash** is a data processing engine.

It receives data, processes it, and sends it to a destination.

A Logstash configuration contains three main sections:

`Input → Filter → Output`

### Input

Defines where the data comes from.

Examples:

- Beats
- Files
- Network ports

### Filter

Processes, parses, and normalizes the data.

### Output

Defines where the processed data will be sent.

Examples:

- Elasticsearch
- File
- Network port

---

## Beats

**Beats** are lightweight agents installed on endpoints.

They collect specific types of data and send it for processing and storage.

Examples:

| Beat | Data Collected |
|---|---|
| Winlogbeat | Windows Event Logs |
| Packetbeat | Network traffic data |
| Filebeat | Log files |
| Metricbeat | System and service metrics |

**Simple Flow:**

`Endpoint → Beats → Logstash / Elasticsearch`

---

## Kibana

**Kibana** is the web-based interface used by SOC analysts.

It works with data stored in Elasticsearch.

Analysts use Kibana to:

- Search logs
- Apply filters
- Investigate security events
- Analyze anomalies
- Create visualizations
- Build dashboards

---

## How ELK Components Work Together

`Endpoints`

`↓`

`Beats collect data`

`↓`

`Logstash processes and normalizes data`

`↓`

`Elasticsearch stores and searches data`

`↓`

`Kibana displays and visualizes data`

`↓`

`SOC Analyst investigates`

---

## Kibana Discover Tab

The **Discover tab** is the main workspace used by SOC analysts to explore and investigate logs.

Analysts can:

- View raw logs
- Search data
- Apply filters
- Select fields
- Analyze events over time
- Identify unusual activity

---

## Discover Tab Components

| Component | Purpose |
|---|---|
| Logs | Displays individual events |
| Fields Pane | Shows available fields from the logs |
| Index Pattern / Data View | Selects which Elasticsearch data to analyze |
| Search Bar | Used to search logs with KQL |
| Time Filter | Limits results to a specific time period |
| Timeline | Displays event counts over time |
| Top Bar | Save, open, and share searches |
| Add Filter | Filter logs using specific fields |

---

## Index Pattern / Data View

An **Index Pattern** tells Kibana which Elasticsearch indices and data should be explored.

A single index pattern can point to multiple Elasticsearch indices.

Different log sources may have different fields and structures.

In this room, VPN logs were stored in:

`vpn_connections`

**Simple Concept:**

`Elasticsearch Data → Select Index Pattern → Explore in Kibana`

---

## Fields Pane

The Fields Pane displays normalized fields found in the logs.

Examples:

- `Source_ip`
- `Source_Country`
- `UserName`
- `action`

Clicking a field shows its common values and occurrence percentages.

Filters can then be applied:

`+` → Include logs containing the value

`-` → Exclude logs containing the value

---

## Time Filter

The **Time Filter** limits search results to a selected time period.

Examples:

- Last 15 minutes
- Last 24 hours
- January 2022
- Custom time range

Selecting the correct time range is important during investigations.

---

## Timeline

The Timeline displays the number of events occurring over time.

It helps analysts identify:

- Log spikes
- Sudden increases in activity
- Unusual patterns
- Specific periods requiring investigation

**Example:**

`Normal Activity → Normal Activity → Large Spike → Investigate`

---

## Creating Tables

Logs are displayed in raw form by default.

Analysts can select important fields and create tables to reduce unnecessary information.

**Example:**

`Raw Logs → Select UserName + Source_ip + action → Clean Investigation Table`

Tables can also be saved for future use.

---

## KQL Overview

**KQL (Kibana Query Language)** is used to search and filter data stored in Elasticsearch.

KQL supports:

- Free text searches
- Field-based searches
- Wildcards
- Logical operators

---

## Free Text Search

A free text search finds documents containing a specific word or phrase.

Example:

```kql
"United States"
```

This returns logs containing the exact phrase.

KQL searches complete terms by default.

Searching:

```kql
United
```

may not return logs containing `United States`.

---

## Wildcard Searches

The wildcard `*` matches additional characters.

Example:

```kql
United*
```

This may match:

- United States
- United Kingdom
- United Nations

---

## Logical Operators

KQL supports:

`AND`

`OR`

`NOT`

### AND Operator

Both conditions must be present.

```kql
"United States" AND "Virginia"
```

### OR Operator

Either condition can be present.

```kql
"United States" OR "England"
```

### NOT Operator

Excludes matching results.

```kql
"United States" AND NOT ("Florida")
```

---

## Field-Based Search

Field-based searches look for specific values inside specific fields.

**Syntax:**

```text
Field: Value
```

Example:

```kql
Source_ip: 238.163.231.224 AND UserName: Suleman
```

This returns events where:

- `Source_ip` matches the specified IP address
- `UserName` is Suleman

Field-based searches are useful during SOC investigations because they allow analysts to search for specific users, IP addresses, actions, and other indicators.

---

## Example Investigation Workflow

Suppose an analyst notices suspicious VPN activity.

The investigation may follow:

`Set Time Range → Select vpn_connections → Search User/IP → Apply Filters → Review Events → Identify Anomalies → Determine Verdict`

Example query:

```kql
Source_ip: 238.163.231.224 AND UserName: Suleman
```

---

## Creating Visualizations

Visualizations convert log data into easier-to-understand formats.

Common visualization types include:

- Tables
- Pie charts
- Bar charts
- Line charts

Visualizations help analysts identify patterns, trends, and suspicious activity.

---

## Correlating Fields

Multiple fields can be combined in a visualization to identify relationships.

Example:

`Source_ip + Source_Country`

This can show which IP addresses are connecting from particular countries.

Another example:

`UserName + Source_ip`

This can help identify users with repeated connection attempts from specific IP addresses.

---

## Failed VPN Connection Visualization

In this room, a visualization was created to investigate failed VPN connections.

### Investigation Setup

**Data View:**

`vpn_connections`

**Time Range:**

`January 2022`

**Filter:**

```kql
action: failed
```

**Table Fields:**

`UserName`

`Source_ip`

This visualization helps identify users and IP addresses involved in repeated failed VPN connection attempts.

---

## Saving Visualizations

After creating a visualization:

`Create Visualization → Add Title & Description → Save → Add to Library`

Saving visualizations allows them to be reused in dashboards.

---

## Kibana Dashboards

A **Dashboard** combines multiple saved searches and visualizations into one centralized view.

Dashboards provide quick visibility into security activity.

A VPN monitoring dashboard may contain:

- Failed VPN connection attempts
- Top source IP addresses
- Source countries
- Users with repeated failed logins
- VPN activity over time

---

## Creating a Custom Dashboard

The basic process is:

`Create Dashboard → Add from Library → Select Saved Searches & Visualizations → Arrange Panels → Save Dashboard`

### Steps

1. Open the Dashboard tab.
2. Click **Create Dashboard**.
3. Select **Add from Library**.
4. Add saved searches and visualizations.
5. Arrange the dashboard panels.
6. Save the dashboard.

---

## Splunk vs Elastic Stack

| Splunk | Elastic Stack |
|---|---|
| Commercial data analytics and SIEM platform | Collection of data processing and analytics tools |
| Forwarder collects logs | Beats collect logs |
| Indexer processes and stores data | Logstash processes data and Elasticsearch stores it |
| Search Head is used for investigation | Kibana is used for investigation |
| Uses SPL | Uses KQL in Kibana |
| Provides dashboards and visualizations | Provides dashboards and visualizations |

**Simple Comparison:**

`Splunk: Forwarder → Indexer → Search Head`

`ELK: Beats → Logstash → Elasticsearch → Kibana`

---

## Why Elastic Stack is Useful for SOC Analysts

Elastic Stack helps SOC analysts:

- Search large amounts of security logs
- Investigate users and IP addresses
- Apply filters to narrow down events
- Analyze activity over specific time periods
- Identify unusual spikes and patterns
- Investigate failed login attempts
- Create visualizations
- Build security monitoring dashboards

---

## Key Terms

| Term | Definition |
|---|---|
| ELK | Elasticsearch, Logstash, and Kibana |
| Elasticsearch | Search and analytics engine that stores and searches data |
| Logstash | Processes, parses, and normalizes incoming data |
| Beats | Lightweight agents used to collect and send data |
| Kibana | Interface used to search, analyze, and visualize Elasticsearch data |
| KQL | Kibana Query Language |
| Index Pattern / Data View | Defines which Elasticsearch data Kibana should explore |
| Field | Named value extracted from a log |
| Time Filter | Limits events to a selected time period |
| Timeline | Displays event counts over time |
| Visualization | Graphical representation of log data |
| Dashboard | Collection of saved searches and visualizations |

---

## Personal Takeaways

- Elastic Stack can be used by SOC teams for log analysis, investigations, and security monitoring even though it was not originally designed as a traditional SIEM.
- The basic ELK architecture is easy to remember: Beats collect data, Logstash processes it, Elasticsearch stores and searches it, and Kibana allows analysts to investigate it.
- The Discover tab is the main workspace for searching logs, applying filters, selecting fields, and investigating anomalies.
- KQL allows analysts to search logs using free text, fields, wildcards, and logical operators.
- Time filters and timelines are important because suspicious activity often becomes visible as spikes or unusual patterns over time.
- Visualizations help convert large amounts of raw log data into patterns that are easier to investigate.
- Dashboards combine saved searches and visualizations to provide quick visibility into security activity.
- For SOC analysts, the main skill is not memorizing the Elastic Stack architecture but knowing how to search, filter, analyze, and investigate security data effectively.

---

*Previous: Splunk — The Basics*  
*Next: Introduction to SOAR*
