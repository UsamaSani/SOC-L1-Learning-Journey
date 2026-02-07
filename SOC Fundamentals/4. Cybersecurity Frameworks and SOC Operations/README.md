# Alert Triage, TTPs, and IOCs

A comprehensive reference for SOC analysts covering core concepts used to detect, triage, and investigate threats.

---

## Table of Contents

1. [Tactics, Techniques & Procedures (TTPs)](#1-tactics-techniques--procedures-ttps-in-soc)
2. [Cyber Kill Chain](#2-cyber-kill-chain-7-stages)
3. [MITRE ATT&CK Framework](#3-mitre-attck)
4. [Three Layers of TTPs](#4-three-layers)
5. [Indicators of Compromise (IOCs)](#5-indicators-of-compromise-iocs)
6. [Four Types of IOCs](#6-four-types-of-iocs)
7. [IOC Confidence Levels](#7-ioc-confidence-levels)
8. [IOCs vs TTPs](#8-iocs-vs-ttps)
9. [Alert Triage](#9-alert-triage)
10. [Why Triage Is Critical](#10-why-triage-is-critical)
11. [Alert Properties](#11-alert-properties)
12. [Alert Prioritization](#12-alert-prioritization)
13. [Real SOC Flow](#13-real-soc-flow)
14. [Alert Triage Workflow](#14-alert-triage-workflow)

---

## 1. Tactics, Techniques & Procedures (TTPs) in SOC

TTPs describe **how attackers think, act, and operate** during cyber-attacks.

- If an IOC tells you **what** happened, TTPs tell you **how** and **why** it happened
- SOC analysts use TTPs to:
  - Detect threats even when IOCs change
  - Understand attacker intent
  - Build better detections, alerts, and response playbooks

---

## 2. Cyber Kill Chain (7 Stages)

The lifecycle of a cyberattack, showing where defenders can detect, block, or disrupt.

| Stage | Name | Description |
|-------|------|-------------|
| 1 | **Reconnaissance** | Gather target info, find weaknesses/entry points |
| 2 | **Weaponization** | Turn intel into tailored payloads to evade defenses |
| 3 | **Delivery** | Send payload (email, links, media, drive-by) |
| 4 | **Exploitation** | Execute delivered artifact, exploit vuln/user action, gain foothold |
| 5 | **Installation** | Establish persistence (malware/backdoors) |
| 6 | **Command & Control (C2)** | Maintain comms for commands/exfiltration |
| 7 | **Action on Objectives** | Exfiltrate data, escalate, move laterally, sabotage, or maintain access |

---

## 3. MITRE ATT&CK

A practical, behavior-focused framework cataloging **what attackers do and how**.

| Tactic | Technique Count |
|--------|-----------------|
| Reconnaissance | 11 |
| Resource Development | 8 |
| Initial Access | 11 |
| Execution | 17 |
| Persistence | 23 |
| Privilege Escalation | 14 |
| Defense Evasion | 47 |
| Credential Access | 17 |
| Discovery | 34 |
| Lateral Movement | 9 |
| Collection | 17 |
| Command & Control | 18 |
| Exfiltration | 9 |
| Impact | 15 |

---

## 4. Three Layers

### Tactics (WHY)

Common attacker goals:

| Tactic | Meaning |
|--------|---------|
| Initial Access | How attacker first gets in |
| Execution | Run malicious code |
| Persistence | Stay in system |
| Privilege Escalation | Become admin |
| Defense Evasion | Avoid AV/EDR |
| Credential Access | Steal passwords |
| Lateral Movement | Move to other systems |
| Exfiltration | Steal data |

### Techniques (HOW)

Examples for Credential Access:
- Keylogging
- Credential dumping (LSASS)
- Browser password theft
- Phishing for credentials

### Procedures (Steps/Tools/Commands/Timing)

**Example:**
- **Technique:** Credential Dumping
- **Procedure:** `procdump.exe -accepteula -m lsass.exe lsass.dmp`

> Most SOCs map TTPs to MITRE ATT&CK (used by SIEM/EDR/XDR)

---

## 5. Indicators of Compromise (IOCs)

Observable evidence of compromise.

> "Something bad happened here and we can prove it with data"

**Sources:**
- Logs
- Network traffic
- Endpoint activity
- Email headers
- File systems

**Uses:**
- Trigger SIEM alerts
- Confirm activity
- Correlate across systems
- Respond (block/isolate)
- Write reports

---

## 6. Four Types of IOCs

### Network-Based
- Malicious IPs
- Suspicious domains
- C2 communications
- Unusual ports/protocols

**Where seen:** Firewall/proxy/DNS logs, IDS/IPS

### Host/Endpoint-Based
- Suspicious processes
- Unexpected services
- Registry changes
- New scheduled tasks

**Where seen:** EDR/XDR, Windows Event Logs, Sysmon, Linux audit logs

### File-Based
- Hashes (MD5/SHA256)
- Name patterns
- Size anomalies

**Where seen:** AV, EDR, email gateways, sandboxes

### Email-Based
- Malicious sender
- Phishing subjects
- Malicious URLs
- Header anomalies

**Where seen:** Email security, Microsoft Defender, Proofpoint/Mimecast, user reports

---

## 7. IOC Confidence Levels

| Level | Example |
|-------|---------|
| **Low** | Single suspicious IP |
| **Medium** | Known phishing domain |
| **High** | Malware hash + execution |
| **Very High** | Multiple correlated IOCs |

---

## 8. IOCs vs TTPs

| Aspect | IOCs | TTPs |
|--------|------|------|
| Type | Evidence | Behavior |
| Answers | What happened | How it happened |
| Lifespan | Short-lived | Long-lived |
| Changeability | Easy to change | Hard to change |
| Usage | Alerts | Detection logic |

---

## 9. Alert Triage

A structured process to quickly judge alerts as **real**, **false**, or **escalate** - separating real attacks from noise accurately.

> "SOC analysts are promoted based on triage quality, not number of alerts closed."

**Flow:**
```
Events occur -> Systems log -> Logs ship to SIEM/EDR -> Alerts highlight suspicious sequences -> Analysts triage dozens of alerts instead of millions of logs
```

---

## 10. Why Triage Is Critical

| Without Triage | With Triage |
|----------------|-------------|
| Drown in alerts | Fewer false positives |
| Miss attacks | Early catches |
| Delayed response | Efficient/trusted SOC |
| Higher business impact | - |

> Triage decides whether an alert becomes an incident.

---

## 11. Alert Properties

| Property | Description | Example |
|----------|-------------|---------|
| **Alert Time** | When generated | Mar 21, 15:35 |
| **Alert Name** | Trigger summary | Unusual login location |
| **Alert Severity** | Urgency level | Low/Medium/High/Critical |
| **Alert Status** | Lifecycle stage | New/In-Progress/Closed |
| **Alert Verdict** | L1 outcome | True Positive/False Positive |
| **Alert Assignee** | Handling analyst | Assigned Analyst name |
| **Alert Description** | Explanation | Detailed suspicious activity |
| **Alert Fields** | Context | Affected hostname, entered command line, etc. |

---

## 12. Alert Prioritization

1. **Filter Alerts:** Take only new/unseen/unresolved, not owned by others
2. **Sort by Severity:** Critical -> High -> Medium -> Low
3. **Sort by Time:** Oldest first - older breaches likely progressed further

---

## 13. Real SOC Flow

```
IOC detected (IP/hash/process) -> SIEM alert -> L1 validates IOCs -> Map to TTP -> Decision (TP/FP) -> Escalate or close
```

---

## 14. Alert Triage Workflow

### Discovery
- External threat intel
- SIEM correlation
- Behavioral/anomaly analytics
- Deception
- Data from logs/endpoints

### Preliminary Investigation
- Linking
- Scoring
- Merging
- Preliminary scoping

### Triage
- Ranking alerts by priority

### Extended Investigation
- Full scoping
- Visualization
- Enrichment

### Contain & Respond
- Quarantine
- Remediate
- Update
- Share

### Initial Actions
1. Assign alert to yourself
2. Move to In-Progress
3. Review name/description/key indicators to avoid collisions and prepare for investigation

---

## Key Takeaways

- **TTPs** reveal attacker behavior and are harder to change than IOCs
- The **Cyber Kill Chain** provides a framework for understanding attack progression
- **MITRE ATT&CK** offers a standardized taxonomy for threat behaviors
- **IOCs** are evidence of compromise across network, host, file, and email sources
- **Alert triage** is critical for efficient SOC operations and accurate threat detection
- Prioritize alerts by **severity** (Critical first) and **time** (oldest first)
