# Detection Maturity Model

## Overview

The Detection Maturity Model (DMM) defines the lifecycle and quality requirements for detection rules within this repository.

Not every detection is immediately suitable for production use. Each rule progresses through defined maturity stages as it is researched, developed, validated, deployed, and maintained.

The purpose of this model is to:

- Standardize detection quality.
- Ensure consistent validation.
- Improve operational reliability.
- Reduce false positives.
- Track engineering progress.
- Provide transparency to repository users.

---

# Detection Lifecycle

```
Threat Research
        │
        ▼
Draft
        │
        ▼
Experimental
        │
        ▼
Validated
        │
        ▼
Production
        │
        ▼
Maintained
        │
        ▼
Deprecated
        │
        ▼
Retired
```

---

# Maturity Levels

## Level 0 – Draft

**Status:** ⚪ Draft

### Description

Initial implementation of a detection concept.

Rules at this stage may be incomplete and have not undergone validation.

### Characteristics

- Initial detection logic
- MITRE ATT&CK mapping identified
- Query under development
- Documentation incomplete
- No validation performed

### Allowed Usage

- Personal testing
- Development environments

### Not Recommended For

- Production
- SOC alerting

---

## Level 1 – Experimental

**Status:** 🟡 Experimental

### Description

The rule is syntactically correct and functional but requires additional validation.

### Requirements

- Query executes successfully
- Documentation completed
- Initial testing performed
- Basic false-positive analysis
- Initial peer review

### Limitations

- Detection accuracy not fully verified
- Thresholds may require tuning
- Limited production confidence

---

## Level 2 – Validated

**Status:** 🟢 Validated

### Description

The rule has been successfully tested in a controlled environment using known attack simulations or representative telemetry.

### Requirements

- Successful laboratory validation
- Detection triggered as expected
- MITRE ATT&CK mapping verified
- Documentation complete
- Lookup integration tested
- False-positive review completed
- Investigation guide completed

### Deliverables

- Validation report
- Test scenarios
- Screenshots (optional)
- Performance observations

---

## Level 3 – Production

**Status:** 🔵 Production

### Description

The detection has been deployed in a production environment and has demonstrated operational effectiveness.

### Requirements

- Successfully deployed
- Stable performance
- Acceptable alert volume
- SOC analyst approval
- Operational documentation complete
- No unresolved issues

### Success Metrics

- Low false-positive rate
- High detection fidelity
- Acceptable execution time
- Positive SOC feedback

---

## Level 4 – Maintained

**Status:** 🟣 Maintained

### Description

The rule is actively monitored and updated to reflect changes in the threat landscape, Falcon telemetry, or organizational infrastructure.

### Maintenance Activities

- Periodic review
- Query optimization
- ATT&CK mapping updates
- Lookup maintenance
- Documentation improvements
- Performance tuning

---

## Level 5 – Deprecated

**Status:** 🟠 Deprecated

### Description

The detection is scheduled for retirement but retained for compatibility or historical purposes.

### Reasons

- Superior replacement available
- Telemetry deprecated
- Excessive false positives
- Unsupported data source
- Technique no longer relevant

Deprecated rules should not be used for new deployments.

---

## Level 6 – Retired

**Status:** 🔴 Retired

### Description

The detection is no longer maintained or supported.

Retired rules remain in the repository for historical reference but are excluded from active development.

---

# Maturity Matrix

| Stage | Query | Validation | Documentation | Production Ready |
|--------|-------|------------|---------------|------------------|
| Draft | ✅ | ❌ | Partial | ❌ |
| Experimental | ✅ | Partial | ✅ | ❌ |
| Validated | ✅ | ✅ | ✅ | Limited |
| Production | ✅ | ✅ | ✅ | ✅ |
| Maintained | ✅ | Continuous | ✅ | ✅ |
| Deprecated | Archived | N/A | Archived | ❌ |
| Retired | Archived | N/A | Archived | ❌ |

---

# Promotion Criteria

## Draft → Experimental

Requirements:

- Query compiles successfully
- Initial documentation completed
- MITRE ATT&CK mapping documented
- Detection logic reviewed

---

## Experimental → Validated

Requirements:

- Successful validation
- Expected telemetry observed
- False positives reviewed
- Lookup functionality verified
- Investigation guide completed

---

## Validated → Production

Requirements:

- Peer review approved
- Performance acceptable
- Stable alert volume
- SOC acceptance
- Deployment approved

---

## Production → Maintained

Requirements:

- Operational monitoring established
- Version control implemented
- Periodic review scheduled

---

## Production → Deprecated

Conditions:

- Detection superseded
- Data source removed
- Excessive operational overhead
- Unsupported platform

---

## Deprecated → Retired

Conditions:

- No active deployments
- Historical value only
- Documentation archived

---

# Validation Requirements

Every production-ready detection must include:

- Detection description
- MITRE ATT&CK mapping
- Falcon NG-SIEM query
- Validation procedure
- Investigation guide
- Tuning recommendations
- References
- Version history

---

# Repository Status Indicators

Use the following badges in each detection README.

| Badge | Meaning |
|--------|---------|
| 🟢 Validated | Successfully tested |
| 🔵 Production | Operationally deployed |
| 🟡 Experimental | Under evaluation |
| ⚪ Draft | Development |
| 🟠 Deprecated | Scheduled for removal |
| 🔴 Retired | Historical reference |

---

# Continuous Improvement

Detection engineering is an ongoing process.

Production detections should be reviewed when:

- New attack techniques emerge
- MITRE ATT&CK updates techniques
- Falcon introduces new telemetry
- False positives increase
- Customer environments change
- Detection performance degrades

Every update should increment the rule version and be documented in the changelog.

---

# Success Metrics

A mature detection should demonstrate:

- High detection fidelity
- Low false-positive rate
- Stable execution performance
- Clear investigation guidance
- Accurate ATT&CK mapping
- Comprehensive documentation
- Successful validation
- Ongoing maintenance

---

# Summary

The Detection Maturity Model provides a structured framework for evaluating the quality and readiness of detection rules.

By following this model, contributors can consistently develop high-quality CrowdStrike Falcon NG-SIEM detections that are reliable, maintainable, and suitable for production environments.
