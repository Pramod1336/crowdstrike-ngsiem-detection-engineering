# Repository Architecture

## Overview

The **CrowdStrike NG-SIEM Detection Engineering** repository is designed to provide a structured, scalable, and maintainable framework for developing, validating, and sharing CrowdStrike Falcon Next-Gen SIEM detections.

Unlike repositories that only publish detection queries, this project documents the complete lifecycle of detection engineering—from threat research to production deployment.

---

# Architecture Goals

The repository is built around the following objectives:

- Build high-quality production detections.
- Standardize detection development.
- Reduce false positives through tuning and lookup frameworks.
- Provide repeatable validation procedures.
- Document SOC investigation workflows.
- Align detections with the MITRE ATT&CK Framework.
- Encourage community collaboration and peer review.

---

# Repository Layout

```
crowdstrike-ngsiem-detection-engineering
│
├── docs/
├── detections/
├── lookups/
├── playbooks/
├── validation/
├── hunting/
├── dashboards/
├── templates/
├── scripts/
├── analytics/
├── tests/
└── tools/
```

Each directory has a dedicated purpose and should contain only related content.

---

# High-Level Architecture

```
                     Threat Intelligence
                              │
                              ▼
                     Threat Research
                              │
                              ▼
                     Detection Engineering
                              │
                              ▼
                    Falcon NG-SIEM Query
                              │
                              ▼
                  Correlation Rule Creation
                              │
                              ▼
                    Detection Validation
                              │
                              ▼
                 False Positive Tuning
                              │
                              ▼
                   Production Deployment
                              │
                              ▼
                     SOC Investigation
                              │
                              ▼
                    Continuous Improvement
```

---

# Detection Architecture

Every detection follows the same structure.

```
Threat

↓

MITRE Mapping

↓

Required Telemetry

↓

Detection Logic

↓

Falcon Query

↓

Lookup Integration

↓

Validation

↓

Investigation Guide

↓

Production Deployment
```

This ensures consistency across all detections.

---

# Detection Categories

Detection rules are organized according to MITRE ATT&CK tactics.

```
TA0001 Initial Access

TA0002 Execution

TA0003 Persistence

TA0004 Privilege Escalation

TA0005 Defense Evasion

TA0006 Credential Access

TA0007 Discovery

TA0008 Lateral Movement

TA0009 Collection

TA0011 Command and Control

TA0010 Exfiltration

TA0040 Impact
```

Each category contains one or more validated detection rules.

---

# Rule Directory Structure

Every detection should have its own folder.

Example:

```
DISC-001-Unauthorized-Host-Recon/

README.md

rule.cql

validation.md

investigation.md

tuning.md

references.md
```

Keeping rule documentation together makes maintenance much easier.

---

# Lookup Architecture

Lookups reduce false positives and improve rule maintainability.

Examples:

```
Allowed_Hosts.csv

Privileged_Users.csv

Service_Accounts.csv

Jump_Servers.csv

Sensitive_Servers.csv

Domain_Controllers.csv

Approved_Admin_Hosts.csv
```

Rules should reference lookup files instead of embedding environment-specific values directly in queries.

---

# Validation Architecture

Every detection must be validated before being considered production-ready.

Validation includes:

- Test scenario
- Commands executed
- Expected telemetry
- Expected detection
- Expected alert
- False positive review
- Performance observations

---

# Investigation Architecture

Every rule should include an investigation guide describing:

- Initial triage
- Evidence collection
- Threat validation
- Scope determination
- Containment recommendations
- Escalation criteria

---

# Threat Hunting

Threat hunting content complements detection rules by enabling analysts to proactively search for suspicious behavior that may not trigger a correlation rule.

---

# Dashboards

Dashboards provide visibility into:

- Detection coverage
- MITRE ATT&CK coverage
- Alert volume
- Rule performance
- False positive trends

---

# Design Principles

This repository follows several key design principles.

## Standardization

Every detection follows the same documentation format.

## Simplicity

Queries should remain readable and maintainable.

## Performance

Detection logic should minimize unnecessary processing.

## Reusability

Lookup files and templates should be reused whenever possible.

## Validation

No rule should be marked as validated without successful testing.

## Documentation

Every detection must include supporting documentation.

---

# Repository Lifecycle

```
Research

↓

Develop

↓

Validate

↓

Tune

↓

Deploy

↓

Monitor

↓

Improve

↓

Repeat
```

Detection engineering is a continuous improvement process.

---

# Future Enhancements

Future versions of the repository may include:

- GitHub Actions
- Automated query validation
- Detection testing framework
- MITRE ATT&CK Navigator export
- Detection coverage reports
- Dashboard templates
- Community rule review process

---

# Summary

This repository is designed to serve as a complete detection engineering framework for CrowdStrike Falcon Next-Gen SIEM.

Its focus is not only on writing detection rules but also on documenting the engineering process required to build reliable, maintainable, and production-ready detections.
