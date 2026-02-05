# The Pyramid of Pain: A Strategic Guide to Cyber Defense

[![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-blue)](https://github.com/usamasani)
[![Threat Intelligence](https://img.shields.io/badge/Focus-Threat%20Intelligence-red)](https://github.com/usamasani)
[![SOC Analysis](https://img.shields.io/badge/Role-SOC%20Analyst-green)](https://github.com/usamasani)

## Overview

This repository contains comprehensive educational material on **The Pyramid of Pain** - a foundational framework in Cyber Threat Intelligence (CTI) and Incident Response. Created by David Bianco, this model revolutionizes how security professionals approach threat detection by categorizing Indicators of Compromise (IOCs) based on the operational pain they inflict on adversaries.

**Target Audience:** Threat Hunters, Incident Responders, SOC Analysts, Security Engineers

## Core Concept

> "The amount of pain you cause an adversary depends on the types of indicators you are able to make use of." — David Bianco

The Pyramid of Pain shifts the defensive mindset from:
- "Can we detect this?"
- "How much does this hurt the attacker?"

## The Pyramid Hierarchy

```
        ┌─────────────────────┐
        │   TTPs (Tough)      │ ← Maximum Pain
        ├─────────────────────┤
        │   Tools             │
        ├─────────────────────┤
        │   Network Artifacts │
        ├─────────────────────┤
        │   Host Artifacts    │
        ├─────────────────────┤
        │   Domain Names      │
        ├─────────────────────┤
        │   IP Addresses      │
        ├─────────────────────┤
        │   Hash Values       │ ← Minimal Pain
        └─────────────────────┘
```

### Pain Levels Explained

| Level | Indicator Type | Pain Level | Adversary Impact |
|-------|---------------|------------|------------------|
| 1 | **Hash Values** | Trivial | Change one bit → New hash |
| 2 | **IP Addresses** | Easy | Proxy/VPN switch |
| 3 | **Domain Names** | Simple | Register new domain |
| 4 | **Network Artifacts** | Annoying | Modify C2 protocols |
| 5 | **Host Artifacts** | Annoying | Reconfigure droppers |
| 6 | **Tools** | Challenging | Rebuild/replace toolkit |
| 7 | **TTPs** | Tough | Rethink entire attack methodology |

## Detailed Breakdown

### 1. Hash Values (Trivial)
- **Examples:** MD5, SHA-1, SHA-256
- **Defensive Tools:** VirusTotal, Metadefender
- **Bypass Method:** Single bit change = Complete new hash
- **Use Case:** Quick malware identification, but easily evaded

### 2. IP Addresses (Easy)
- **Evasion Tactics:** Fast Flux networks, Tor, VPNs, compromised proxies
- **Reality:** Attackers rarely use their own infrastructure
- **Value:** Good for containment, poor for eradication

### 3. Domain Names (Simple)
- **Challenges for Attackers:** Registration costs, DNS propagation
- **Evasion Tactics:** 
  - URL shorteners (bit.ly, tinyurl)
  - Punycode attacks (e.g., `adídas.de` → `xn--addas-04a.de`)
- **Detection Tip:** Append `+` to shortened URLs to preview destination

### 4. Host Artifacts (Annoying)
- **Examples:**
  - Registry persistence keys
  - Dropped files in Temp folders
  - Suspicious process execution patterns
- **Impact:** Forces adversary to reconfigure and retest malware

### 5. Network Artifacts (Annoying)
- **Examples:**
  - Custom User-Agent strings
  - URI patterns in C2 communication
  - Specific HTTP headers
- **Tools:** Wireshark, TShark, Snort, Suricata
- **Value:** Remains constant even when IPs change

### 6. Tools (Challenging)
- **Examples:** Cobalt Strike beacons, custom backdoors, credential dumpers
- **Defensive Techniques:**
  - **Fuzzy Hashing (SSDeep):** Detect tool variants
  - **YARA Rules:** Pattern-match malware families
- **Impact:** Adversary must rebuild or acquire new tools (expensive)

### 7. TTPs - Tactics, Techniques & Procedures (Tough)
- **Framework:** MITRE ATT&CK
- **Definition:**
  - **Tactics:** The goal (e.g., Exfiltration)
  - **Techniques:** The method (e.g., Scheduled Tasks)
  - **Procedures:** Specific implementation steps
- **Impact:** Forces adversary to completely rethink attack methodology
- **Result:** Most attackers abandon the target

## Practical Applications

### For Threat Hunters
```
1. Start with TTP-based hypotheses
   Example: "Is PowerShell being used for lateral movement?"
2. Hunt for behavioral patterns, not just signatures
3. Map findings to the pyramid to assess impact
```

### For Detection Engineers
```
Audit Your SIEM Rules:
├── 90% targeting IPs/Hashes? → Brittle defense
└── Focus on:
    ├── YARA rules (Tools level)
    └── Behavioral analytics (TTP level)
```

### For SOC Analysts
```
Incident Response Priority:
1. Identify TTPs used (MITRE ATT&CK mapping)
2. Document tools deployed
3. Capture network/host artifacts
4. Log IPs/domains/hashes (lowest priority)
```

## Strategic Comparison

| Indicator Type | Defender Effort | Attacker Pain | Longevity |
|----------------|-----------------|---------------|-----------|
| Hash, IP, Domain | Low (Automated) | Trivial | Hours/Days |
| Artifacts, Tools | Medium | Annoying | Weeks |
| TTPs | High (Expertise Required) | Devastating | Months/Years |

## Key Takeaways

1. **Don't just block indicators** → Dismantle adversary capabilities
2. **Invest in behavioral detection** → Focus on TTPs over signatures
3. **Force adversary investment** → Make attacks expensive
4. **Think strategically** → Every detection should hurt the attacker

## Resources

- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [VirusTotal](https://www.virustotal.com/)
- [YARA Documentation](https://yara.readthedocs.io/)
- [Original Pyramid of Pain Article by David Bianco](http://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)

## About the Author

I'm **Usama Sani Khanzada**, an aspiring SOC Analyst and Web Application Penetration Tester, actively building expertise in both defensive and offensive security.

### My Journey
- **Defensive Security:** SIEM platforms (Splunk, Wazuh), EDR solutions (CrowdStrike, SentinelOne)
- **Offensive Security:** Penetration testing with Burp Suite, Nmap, Nessus
- **Focus Areas:** Threat detection, vulnerability assessment, OWASP Top 10

### Mission
Transforming security alerts into actionable insights and bridging the gap between threat detection and secure application development.

## Let's Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Usama%20Sani%20Khanzada-0077B5?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/usama-sani-khanzada/)
[![GitHub](https://img.shields.io/badge/GitHub-Usama%20Sani-181717?style=for-the-badge&logo=github)](https://github.com/usamasani)

**Open to:**
- Collaboration opportunities
- Knowledge sharing
- Feedback and discussions
- Networking in cybersecurity

---

## License

This educational content is provided for learning purposes. Feel free to use, share, and adapt with proper attribution.

## Acknowledgments

- **David Bianco** - Creator of the Pyramid of Pain framework
- **MITRE Corporation** - ATT&CK Framework
- The cybersecurity community for continuous knowledge sharing

---

*"In cybersecurity, understanding your adversary's pain points is just as important as understanding your own defenses."*

**Star this repository if you found it helpful!**