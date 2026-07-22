# MITRE ATT&CK Mapping Strategy

## Overview

This repository adopts the **MITRE ATT&CK® Enterprise Framework** as the primary methodology for classifying, organizing, and measuring detection coverage.

Every detection rule must map to one or more MITRE ATT&CK tactics and techniques based on the behavior it detects.

The purpose of ATT&CK mapping is to:

- Standardize detection classification.
- Measure detection coverage.
- Identify visibility gaps.
- Prioritize engineering efforts.
- Improve SOC investigations.
- Align with industry-recognized adversary behaviors.

---

# Mapping Philosophy

This repository follows several core principles when mapping detections.

## 1. Map Behavior, Not Tools

Always map the adversary behavior rather than the tool used.

**Correct**

- PowerShell used for encoded execution → **T1059.001**
- PsExec used for remote execution → **T1021.002**
- Mimikatz accessing LSASS → **T1003.001**

**Incorrect**

- PowerShell.exe
- PsExec.exe
- Mimikatz.exe

Detection rules should remain effective even if attackers change tools.

---

## 2. Prefer Technique-Level Mapping

Whenever possible, map detections to the most specific ATT&CK technique.

Example:

Instead of:

```
T1059
Command and Scripting Interpreter
```

Prefer:

```
T1059.001
PowerShell
```

Specific mappings improve coverage reporting and analyst understanding.

---

## 3. Multiple Techniques Are Allowed

A single detection may cover multiple ATT&CK techniques.

Example:

Detection:

Unauthorized Network Discovery

Possible mappings:

| Tactic | Technique |
|---------|-----------|
| Discovery | T1016 - System Network Configuration Discovery |
| Discovery | T1049 - System Network Connections Discovery |
| Discovery | T1082 - System Information Discovery |

Document all applicable mappings.

---

# MITRE ATT&CK Tactics

Detection rules are organized according to the following ATT&CK tactics.

| ID | Tactic |
|----|--------|
| TA0001 | Initial Access |
| TA0002 | Execution |
| TA0003 | Persistence |
| TA0004 | Privilege Escalation |
| TA0005 | Defense Evasion |
| TA0006 | Credential Access |
| TA0007 | Discovery |
| TA0008 | Lateral Movement |
| TA0009 | Collection |
| TA0011 | Command and Control |
| TA0010 | Exfiltration |
| TA0040 | Impact |

---

# Detection Naming Convention

Each detection identifier begins with a category prefix.

Examples:

```
INIT-001

EXEC-001

PERS-001

PRIV-001

DEF-001

CRED-001

DISC-001

LAT-001

COLL-001

C2-001

EXFIL-001

IMP-001
```

The prefix does not replace ATT&CK mapping—it provides an organizational structure within the repository.

---

# Rule Documentation Requirements

Every detection must include an ATT&CK section.

Example:

```
MITRE ATT&CK

Tactic

Discovery (TA0007)

Techniques

T1016
System Network Configuration Discovery

T1082
System Information Discovery

T1033
System Owner/User Discovery
```

---

# Mapping Workflow

Every new detection should follow this process.

```
Threat Intelligence

↓

Identify Adversary Behavior

↓

Identify ATT&CK Tactic

↓

Identify ATT&CK Technique

↓

Identify Sub-technique (if applicable)

↓

Validate Mapping

↓

Document Mapping

↓

Publish Detection
```

---

# Mapping Validation Checklist

Before publishing a detection, verify:

- Correct ATT&CK tactic selected
- Correct ATT&CK technique selected
- Sub-technique used where applicable
- Behavior accurately represented
- Mapping documented in README
- Mapping reviewed during peer review

---

# Detection Coverage Matrix

The repository aims to provide balanced coverage across the ATT&CK Enterprise Matrix.

| Tactic | Planned Coverage |
|---------|------------------|
| Initial Access | High |
| Execution | High |
| Persistence | High |
| Privilege Escalation | High |
| Defense Evasion | High |
| Credential Access | High |
| Discovery | High |
| Lateral Movement | High |
| Collection | Medium |
| Command and Control | High |
| Exfiltration | Medium |
| Impact | High |

Coverage will expand as new detections are developed.

---

# Detection Prioritization

Detection engineering efforts should prioritize:

### Priority 1

- Credential Access
- Defense Evasion
- Lateral Movement
- Execution
- Impact

### Priority 2

- Persistence
- Discovery
- Initial Access
- Command and Control

### Priority 3

- Collection
- Exfiltration

Priorities may vary depending on organizational risk.

---

# ATT&CK Coverage Tracking

Each release should include a coverage summary.

Example:

| Tactic | Rules |
|---------|------:|
| Initial Access | 4 |
| Execution | 12 |
| Persistence | 9 |
| Privilege Escalation | 5 |
| Defense Evasion | 11 |
| Credential Access | 8 |
| Discovery | 15 |
| Lateral Movement | 7 |
| Collection | 3 |
| Command and Control | 6 |
| Exfiltration | 2 |
| Impact | 5 |

This table should be updated as detections are added.

---

# Common Mapping Mistakes

Avoid the following:

- Mapping based on filenames.
- Mapping based on malware family names.
- Using generic techniques when a sub-technique exists.
- Selecting techniques without supporting telemetry.
- Mapping unrelated behaviors to increase coverage.

Accurate mapping is more valuable than broad coverage.

---

# Repository Goal

The long-term objective is to achieve comprehensive detection coverage across the MITRE ATT&CK Enterprise Matrix while maintaining high detection quality and low false-positive rates.

Coverage should be driven by real-world adversary behaviors and validated telemetry rather than by achieving numerical completeness.

---

# References

- MITRE ATT&CK Enterprise Framework
- CrowdStrike Falcon Next-Gen SIEM Documentation
- CrowdStrike Adversary Intelligence
- MITRE ATT&CK Navigator
