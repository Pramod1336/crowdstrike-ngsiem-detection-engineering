# CrowdStrike NG-SIEM Detection Engineering

> A community-driven repository of production-focused CrowdStrike Falcon Next-Gen SIEM detection rules, lookup templates, validation guides, SOC playbooks, and MITRE ATT&CK mappings.

![MIT License](https://img.shields.io/badge/License-MIT-green.svg)
![CrowdStrike](https://img.shields.io/badge/CrowdStrike-NG--SIEM-orange)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK-red)
![Detection Engineering](https://img.shields.io/badge/Detection-Engineering-blue)

---

## Overview

This repository provides a structured collection of detection engineering content for **CrowdStrike Falcon Next-Gen SIEM**.

Unlike generic rule repositories, every detection is designed to be:

- Behavior-based
- MITRE ATT&CK mapped
- SOC investigation ready
- Production-oriented
- Lookup-aware
- False-positive tuned
- Validation documented

The goal is to build a practical detection library that security teams can deploy, validate, and continuously improve.

---

# Repository Structure

```
crowdstrike-ngsiem-detection-engineering/
│
├── detections/
│   ├── Initial_Access/
│   ├── Execution/
│   ├── Persistence/
│   ├── Privilege_Escalation/
│   ├── Defense_Evasion/
│   ├── Credential_Access/
│   ├── Discovery/
│   ├── Lateral_Movement/
│   ├── Collection/
│   ├── Command_and_Control/
│   ├── Exfiltration/
│   └── Impact/
│
├── lookups/
│
├── hunting/
│
├── playbooks/
│
├── validation/
│
├── dashboards/
│
├── scripts/
│
├── docs/
│
└── README.md
```

---

# Detection Rule Standard

Each detection includes:

- Rule Name
- Description
- Threat Scenario
- MITRE ATT&CK Mapping
- Required Data Sources
- Required Lookup Files
- CQL Query
- Detection Logic
- Validation Procedure
- False Positive Analysis
- Investigation Guide
- Response Recommendations
- References
- Version History

---

# Detection Categories

- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Collection
- Command & Control
- Exfiltration
- Impact

---

# Rule Status

Each rule is classified using one of the following maturity levels:

| Status | Description |
|---------|-------------|
| 🟢 Validated | Tested in Falcon NG-SIEM |
| 🟡 Experimental | Requires additional validation |
| 🔴 Concept | Detection logic proposed |

---

# Current Roadmap

## Phase 1

- Discovery Detection Rules
- Lookup Framework
- Validation Guides
- MITRE Mapping

## Phase 2

- Execution Detection Rules
- Credential Access Detection Rules
- Lateral Movement Detection Rules
- Threat Hunting Queries

## Phase 3

- SOC Dashboards
- Playbooks
- Automation
- Detection Coverage Matrix

---

# Contributing

Contributions are welcome.

When submitting a detection rule, please include:

- Detection query
- MITRE mapping
- Validation steps
- Expected telemetry
- False positives
- Investigation guide

---

# Disclaimer

This repository is intended for educational and defensive security purposes only.

Detection rules should be validated in a non-production environment before deployment.

Always tune detections according to your organization's environment.

---

# Acknowledgements

- CrowdStrike Falcon Platform
- MITRE ATT&CK Framework
- Detection Engineering Community

---

# License

MIT License

See the LICENSE file for details.
