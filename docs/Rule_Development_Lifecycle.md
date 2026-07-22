# Rule Development Lifecycle

## Overview

The Rule Development Lifecycle (RDL) defines the standardized process for creating, validating, deploying, maintaining, and retiring detection rules within the CrowdStrike NG-SIEM Detection Engineering Framework.

A structured lifecycle ensures that every detection is:

- Technically accurate
- Performance optimized
- Properly documented
- Validated before deployment
- Continuously improved throughout its lifecycle

---

# Lifecycle Overview

```text
Threat Intelligence
        │
        ▼
Threat Research
        │
        ▼
Detection Proposal
        │
        ▼
Detection Design
        │
        ▼
Query Development
        │
        ▼
Peer Review
        │
        ▼
Lab Validation
        │
        ▼
False Positive Analysis
        │
        ▼
Performance Optimization
        │
        ▼
Production Deployment
        │
        ▼
Monitoring
        │
        ▼
Continuous Improvement
        │
        ▼
Retirement (If Required)
```

---

# Phase 1 – Threat Intelligence

## Objective

Identify emerging threats, adversary behaviors, and attack techniques that require detection coverage.

### Common Sources

- MITRE ATT&CK
- CrowdStrike Intelligence
- CISA KEV
- Google Threat Intelligence (Mandiant)
- Microsoft Threat Intelligence
- Cisco Talos
- Red Canary
- Elastic Security Labs
- Unit 42
- Huntress

### Deliverables

- Threat Summary
- MITRE ATT&CK Mapping
- Potential Detection Opportunities

---

# Phase 2 – Detection Proposal

## Objective

Define the detection objective before writing any query.

Questions to answer:

- What behavior are we detecting?
- Why is it important?
- Which ATT&CK technique does it map to?
- Which telemetry is required?
- Which environments are affected?
- Expected severity?
- Expected false positives?

---

# Phase 3 – Detection Design

Design the detection logic before implementation.

## Detection Components

- Required Data Sources
- Event Correlation
- Time Window
- Aggregation Logic
- Thresholds
- Lookup Requirements
- Exclusions
- Expected Alert Output

Document assumptions before writing the query.

---

# Phase 4 – Query Development

Translate the detection logic into CrowdStrike NG-SIEM CQL.

Guidelines:

- Filter early.
- Minimize expensive operations.
- Use aggregation only when required.
- Use lookup tables instead of hardcoded values.
- Keep queries readable and maintainable.

All queries should include comments where appropriate.

---

# Phase 5 – Peer Review

Every production detection should undergo technical review.

Review checklist:

- Query accuracy
- ATT&CK mapping
- Performance
- Readability
- Naming standards
- Documentation completeness
- Lookup implementation
- Validation plan

Peer review helps identify logical errors and improve detection quality.

---

# Phase 6 – Laboratory Validation

Before deployment, validate the rule in a controlled environment.

Validation should confirm:

- Expected telemetry is generated.
- Query matches intended events.
- Rule triggers correctly.
- Alert contains required context.
- No syntax errors.

Record:

- Test environment
- Test commands
- Validation date
- Analyst
- Result

---

# Phase 7 – False Positive Analysis

Identify legitimate activities that may trigger the detection.

Examples:

- System administration
- Software deployment
- Backup operations
- Vulnerability scanning
- Monitoring solutions
- Security tooling

Mitigation strategies:

- Lookup tables
- Environment-specific exclusions
- Threshold tuning
- Time-based filtering

---

# Phase 8 – Performance Optimization

Evaluate the operational efficiency of the detection.

Review:

- Query execution time
- Data scanned
- Aggregation cost
- Lookup performance
- Alert volume

Optimization should not reduce detection fidelity.

---

# Phase 9 – Production Deployment

Deployment checklist:

- Query validated
- Documentation complete
- Investigation guide available
- Lookup dependencies created
- Version assigned
- Peer review completed

Deployment should begin in monitoring mode whenever feasible before enabling automated response actions.

---

# Phase 10 – Monitoring

Monitor rule performance after deployment.

Track:

- Alert volume
- Detection accuracy
- False positive rate
- Rule execution time
- SOC analyst feedback
- Threat coverage

Monitoring ensures the rule continues to provide operational value.

---

# Phase 11 – Continuous Improvement

Detection engineering is an ongoing process.

Review detections when:

- New threat intelligence becomes available.
- Falcon introduces new telemetry.
- False positives increase.
- Environment changes.
- ATT&CK mappings are updated.

Each improvement should be versioned and documented.

---

# Phase 12 – Rule Retirement

Retire detections when:

- Telemetry is deprecated.
- Technique is obsolete.
- Detection is replaced.
- Data source removed.
- Rule is no longer operationally valuable.

Retired rules should remain in version history for reference.

---

# Rule Lifecycle Status

| Status | Description |
|---------|-------------|
| Draft | Initial development |
| Under Review | Peer review in progress |
| Validation | Laboratory testing |
| Experimental | Limited production deployment |
| Validated | Successfully tested |
| Production | Actively deployed |
| Deprecated | Scheduled for retirement |
| Retired | No longer maintained |

---

# Required Documentation

Each detection must include:

```text
README.md
rule.cql
validation.md
investigation.md
tuning.md
references.md
```

A detection is considered incomplete if any required documentation is missing.

---

# Versioning

Use semantic versioning for detection rules.

Example:

```
DISC-001

Version 1.0.0

Major:
Detection logic changes

Minor:
Performance improvements

Patch:
Documentation updates
```

---

# Success Criteria

A detection is considered production-ready when:

- Threat researched
- ATT&CK mapped
- Query validated
- Peer reviewed
- False positives analyzed
- Performance optimized
- Documentation completed
- Investigation guide published
- Version assigned

---

# Continuous Feedback Loop

```text
Research
    │
    ▼
Develop
    │
    ▼
Validate
    │
    ▼
Deploy
    │
    ▼
Monitor
    │
    ▼
Tune
    │
    ▼
Improve
    │
    └───────────────┐
                    ▼
              Research
```

Detection engineering is a continuous cycle rather than a one-time activity.

---

# Summary

A disciplined Rule Development Lifecycle enables security teams to create consistent, high-quality detections that are reliable, maintainable, and aligned with evolving threats.

Following this lifecycle ensures every rule in this repository meets the standards required for production deployment in CrowdStrike Falcon Next-Gen SIEM.
