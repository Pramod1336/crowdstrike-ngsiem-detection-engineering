# Detection Engineering Guide

## Overview

Detection engineering is the process of transforming threat intelligence, attacker behavior, and organizational risk into reliable, high-fidelity detections.

This repository follows a structured methodology to develop production-ready CrowdStrike Falcon Next-Gen SIEM detections that are scalable, maintainable, and validated before deployment.

The primary objectives of this methodology are to:

- Detect attacker behaviors instead of specific malware.
- Reduce false positives through contextual enrichment.
- Maximize visibility across the attack lifecycle.
- Standardize rule development and documentation.
- Align detections with the MITRE ATT&CK Framework.

---

# Detection Engineering Lifecycle

Every detection in this repository follows the same engineering lifecycle.

```text
Threat Intelligence
        │
        ▼
Threat Research
        │
        ▼
Threat Modeling
        │
        ▼
MITRE ATT&CK Mapping
        │
        ▼
Telemetry Analysis
        │
        ▼
Detection Logic Design
        │
        ▼
Query Development
        │
        ▼
Rule Validation
        │
        ▼
False Positive Tuning
        │
        ▼
Production Deployment
        │
        ▼
Continuous Improvement
```

---

# Step 1 – Threat Research

Every detection begins with understanding the adversary.

Sources include:

- MITRE ATT&CK
- CrowdStrike Intelligence
- CISA Advisories
- Microsoft Threat Intelligence
- Google Threat Intelligence (Mandiant)
- Elastic Security Research
- Red Canary
- Unit 42
- Huntress
- Cisco Talos
- Proofpoint
- Recorded Future

Research should answer:

- What is the attacker trying to achieve?
- Which techniques are used?
- Which artifacts are generated?
- Which telemetry is available?

---

# Step 2 – Threat Modeling

Define the behavior to detect.

Example:

Threat:
Unauthorized internal reconnaissance.

Attacker Goal:
Identify network assets.

Potential Commands:

- whoami
- hostname
- ipconfig
- systeminfo
- net
- netstat
- arp
- route
- ping
- nslookup
- tracert

Focus on behavior rather than individual tools whenever possible.

---

# Step 3 – MITRE ATT&CK Mapping

Each detection must map to one or more ATT&CK techniques.

Example:

| Tactic | Technique |
|---------|-----------|
| Discovery | T1016 - System Network Configuration Discovery |
| Discovery | T1082 - System Information Discovery |
| Discovery | T1033 - System Owner/User Discovery |

If multiple techniques apply, document all relevant mappings.

---

# Step 4 – Telemetry Analysis

Identify the Falcon datasets and fields required for detection.

Examples include:

- Process execution
- File activity
- Network connections
- Authentication events
- DNS queries
- Registry modifications
- Identity telemetry
- Cloud activity
- Firewall events

Ensure the required telemetry is available before designing the rule.

---

# Step 5 – Detection Logic Design

Design the detection using behavioral indicators rather than static indicators.

Prefer:

- Process relationships
- Execution context
- Parent-child process chains
- Command-line arguments
- Network behavior
- Authentication anomalies
- Sequence of events
- Multi-event correlation

Avoid relying solely on:

- Hashes
- File names
- IP addresses
- Domains

These indicators change frequently and are better suited for threat intelligence enrichment than detection logic.

---

# Step 6 – Query Development

Translate the detection logic into a Falcon NG-SIEM query.

A production-quality query should be:

- Accurate
- Readable
- Efficient
- Well-commented
- Optimized for performance

Example principles:

- Filter early.
- Aggregate only when necessary.
- Minimize wildcard searches.
- Avoid unnecessary regular expressions.
- Reuse lookup tables instead of hardcoded values.

---

# Step 7 – Lookup Integration

Use lookup tables wherever possible to reduce false positives.

Examples include:

- Approved Hosts
- Domain Controllers
- Jump Servers
- Service Accounts
- Privileged Users
- Vulnerability Scanners
- Administrative Workstations

Benefits:

- Easier maintenance
- Improved readability
- Environment-specific tuning
- Reduced query complexity

---

# Step 8 – Validation

Every rule must be tested before production deployment.

Validation should confirm:

- Expected telemetry is generated.
- Query returns expected results.
- Alert triggers correctly.
- Rule performs efficiently.
- False positives are understood.

Document:

- Test scenario
- Commands executed
- Expected results
- Actual results
- Screenshots (optional)
- Observations

---

# Step 9 – False Positive Analysis

Evaluate legitimate activities that may trigger the detection.

Common sources include:

- System administrators
- IT automation
- Monitoring tools
- Backup software
- Security products
- Vulnerability scanners
- Software deployment systems

Whenever appropriate, use lookup tables instead of permanently excluding behavior.

---

# Step 10 – Production Deployment

Before enabling a rule in production, verify:

- Query syntax
- Performance impact
- Validation status
- Documentation completeness
- Investigation guide availability
- MITRE mapping
- Lookup dependencies

Deploy in monitoring mode if possible before enabling automated response actions.

---

# Rule Documentation Requirements

Every detection folder should contain:

```text
README.md
rule.cql
validation.md
investigation.md
tuning.md
references.md
```

Documentation is considered part of the detection.

---

# Detection Quality Checklist

A production-ready detection should satisfy the following:

- Threat researched
- MITRE ATT&CK mapped
- Telemetry verified
- Detection logic documented
- Query validated
- False positives reviewed
- Lookup tables implemented
- Investigation guide completed
- Validation completed
- References included

---

# Continuous Improvement

Detection engineering is an iterative process.

Review detections regularly to:

- Improve accuracy
- Incorporate new threat intelligence
- Optimize performance
- Reduce false positives
- Expand ATT&CK coverage

Version each rule and document significant changes in the repository changelog.

---

# Guiding Principles

This repository follows these core principles:

1. Detect behavior, not malware.
2. Prefer high-fidelity detections over excessive alert volume.
3. Keep queries simple and maintainable.
4. Validate every rule before production use.
5. Document every engineering decision.
6. Align detections with MITRE ATT&CK.
7. Continuously refine detections as threats evolve.

---

# Summary

Effective detection engineering combines threat intelligence, telemetry analysis, behavioral analytics, and operational experience to produce actionable detections.

By following the methodology described in this guide, contributors can create consistent, validated, and production-ready CrowdStrike Falcon NG-SIEM detections that improve security operations and provide meaningful coverage against modern adversaries.
