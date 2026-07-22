# Detection Engineering Best Practices

## Overview

This document defines the engineering standards and best practices for developing high-quality detection rules within the CrowdStrike NG-SIEM Detection Engineering Framework.

Following these guidelines helps ensure that detections are:

- Reliable
- Maintainable
- High fidelity
- Performance optimized
- Easy to investigate
- Consistent across the repository

These practices apply to all contributors and all detection content.

---

# Core Detection Principles

Every detection should follow these principles.

## 1. Detect Behaviors, Not Tools

Attackers frequently replace tools while maintaining the same behavior.

**Good**

Detect:

- Credential dumping
- Network discovery
- Remote execution
- Persistence mechanisms

**Avoid**

Detect:

- mimikatz.exe
- psexec.exe
- powersploit.ps1

Behavior-based detections remain effective even when attacker tooling changes.

---

## 2. Prefer High-Fidelity Detections

A smaller number of actionable alerts is more valuable than a large number of low-confidence alerts.

Design detections that:

- Have clear malicious intent
- Minimize expected administrative activity
- Reduce analyst fatigue

---

## 3. Validate Before Publishing

Every detection should be tested before it is merged into the repository.

Validation should include:

- Successful query execution
- Expected telemetry
- Alert generation
- False positive review
- Investigation workflow

Never publish untested production detections.

---

# Query Design

## Filter Early

Always reduce the dataset as early as possible.

Good

```cql
#event_simpleName=ProcessRollup2
| FileName=/powershell\.exe/
```

Poor

```cql
| FileName=/powershell/
```

Filtering early improves query performance.

---

## Minimize Regex

Regular expressions are powerful but should be used carefully.

Prefer exact matching whenever possible.

Good

```cql
FileName="powershell.exe"
```

Use regex only when pattern matching is required.

---

## Avoid Unnecessary Aggregation

Aggregation increases query cost.

Use aggregation only when it improves detection quality.

Examples:

- Brute-force detection
- Port scanning
- SMB enumeration
- Multiple failed logins

---

## Keep Queries Readable

Format queries consistently.

Example

```cql
#event_simpleName=ProcessRollup2

| FileName="powershell.exe"

| CommandLine=/EncodedCommand/

| !match(
    file="Allowed_Hosts.csv",
    field=[ComputerName],
    column=ComputerName
)
```

Readable queries are easier to maintain and review.

---

# Lookup Best Practices

Use lookup tables instead of hardcoded values.

Examples:

- Approved hosts
- Service accounts
- Domain Controllers
- Jump servers
- Privileged users
- Vulnerability scanners

Benefits include:

- Easier maintenance
- Reduced false positives
- Environment portability
- Cleaner queries

---

# Correlation Best Practices

Use correlation when multiple events together provide stronger evidence than a single event.

Examples include:

- SMB enumeration followed by ransomware activity
- Multiple failed VPN logins followed by a successful login
- PowerShell execution followed by outbound network connections
- Privilege escalation followed by LSASS access

Correlated detections generally provide higher confidence.

---

# False Positive Reduction

Before excluding activity, determine why it is occurring.

Common legitimate sources include:

- IT administration
- Software deployment
- Patch management
- Vulnerability scanning
- Backup solutions
- Monitoring tools
- Security software

Prefer lookup-based exclusions over hardcoded values.

---

# Performance Optimization

Detection queries should:

- Filter early
- Limit aggregation
- Reduce expensive operations
- Use lookup tables
- Avoid unnecessary joins
- Eliminate redundant conditions

Monitor query execution time after deployment.

---

# Documentation Standards

Every detection should include:

- Description
- Detection objective
- Threat scenario
- MITRE ATT&CK mapping
- Data sources
- Query
- Validation guide
- Investigation guide
- Tuning recommendations
- References

Documentation is part of the detection.

---

# Naming Standards

Follow the repository naming conventions.

Examples:

```
DISC-001

EXEC-003

LAT-002

CRED-004
```

Avoid inconsistent or ambiguous naming.

---

# Version Control

Update the detection version whenever changes are made.

Major

- Detection logic changes

Minor

- Performance improvements

Patch

- Documentation corrections

---

# Testing Standards

Every rule should be tested for:

- Expected detection
- Expected telemetry
- Performance
- Alert quality
- False positives

Testing should be reproducible and documented.

---

# Investigation Readiness

Every alert should provide enough context for a SOC analyst to begin an investigation.

Include where possible:

- Hostname
- Username
- Parent process
- Child process
- Command line
- Network details
- File path
- Timestamp
- MITRE ATT&CK mapping

Avoid alerts that require extensive manual enrichment.

---

# Detection Review Checklist

Before publishing a detection, verify:

- Threat researched
- MITRE ATT&CK mapped
- Query optimized
- Validation completed
- False positives reviewed
- Documentation complete
- Lookup integration implemented
- Naming conventions followed
- Peer review completed

---

# Common Mistakes

Avoid:

- Detecting only filenames
- Excessive regex usage
- Hardcoded exclusions
- Ignoring administrative activity
- Publishing unvalidated rules
- Missing investigation guidance
- Missing ATT&CK mapping
- Poor documentation

---

# Continuous Improvement

Detection engineering is an ongoing process.

Review detections regularly to:

- Incorporate new threat intelligence
- Improve performance
- Reduce false positives
- Expand ATT&CK coverage
- Improve investigation guidance

Version every significant change.

---

# Repository Philosophy

This repository emphasizes:

- Detection quality over quantity
- Behavioral analytics over static indicators
- Standardization over ad hoc development
- Validation over assumptions
- Documentation over tribal knowledge
- Continuous improvement over one-time implementation

---

# Summary

High-quality detection engineering requires more than writing queries. It combines threat intelligence, telemetry analysis, validation, tuning, documentation, and operational feedback into a repeatable engineering process.

Following these best practices ensures that detections within this repository remain accurate, maintainable, and production-ready for CrowdStrike Falcon Next-Gen SIEM environments.
