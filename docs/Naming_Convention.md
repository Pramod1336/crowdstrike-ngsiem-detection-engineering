# Naming Convention

## Overview

Consistent naming conventions improve readability, maintainability, and collaboration across the repository. This document defines the naming standards for all repository components, including detection rules, directories, lookup tables, templates, playbooks, validation guides, scripts, dashboards, and documentation.

All contributors should follow these conventions to ensure a uniform repository structure.

---

# General Principles

Follow these principles throughout the repository:

- Use descriptive names.
- Keep names concise and meaningful.
- Avoid abbreviations unless they are widely recognized.
- Use English for all files and documentation.
- Maintain consistency across all directories.

---

# Detection Rule Naming

Each detection is assigned a unique identifier based on the MITRE ATT&CK tactic it primarily addresses.

## Format

```
<PREFIX>-<NUMBER>-<Detection-Name>
```

Example:

```
DISC-001-Unauthorized-Host-Recon
EXEC-001-Encoded-PowerShell
EXEC-002-Certutil-File-Download
PERS-001-Registry-Run-Key-Persistence
PRIV-001-UAC-Bypass
DEF-001-Clear-Windows-Event-Logs
CRED-001-LSASS-Memory-Access
LAT-001-PsExec-Remote-Execution
COLL-001-Sensitive-File-Collection
C2-001-DNS-Tunneling
EXFIL-001-Large-Archive-Upload
IMP-001-Ransomware-File-Encryption
```

---

# Detection Prefixes

| Prefix | MITRE ATT&CK Tactic |
|---------|---------------------|
| INIT | Initial Access |
| EXEC | Execution |
| PERS | Persistence |
| PRIV | Privilege Escalation |
| DEF | Defense Evasion |
| CRED | Credential Access |
| DISC | Discovery |
| LAT | Lateral Movement |
| COLL | Collection |
| C2 | Command and Control |
| EXFIL | Exfiltration |
| IMP | Impact |

---

# Detection Folder Structure

Each detection must reside in its own directory.

Example:

```
detections/

TA0007-Discovery/

DISC-001-Unauthorized-Host-Recon/

README.md
rule.cql
validation.md
investigation.md
tuning.md
references.md
```

Never combine multiple detections in a single directory.

---

# Detection Query Files

Detection query files should use lowercase.

Example:

```
rule.cql
```

Avoid names such as:

```
Query.cql
Detection.cql
Rule_Final.cql
test.cql
```

---

# Documentation Files

Documentation should use PascalCase.

Examples:

```
Architecture.md
Lookup_Framework.md
MITRE_Mapping.md
Detection_Engineering_Guide.md
```

---

# Lookup Files

Lookup filenames should clearly identify the entity they contain.

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

Avoid:

```
hosts.csv
test.csv
lookup.csv
data.csv
```

---

# Lookup Columns

Use descriptive column names.

Good:

```
ComputerName

UserName

IPAddress

ProcessName

SHA256
```

Avoid:

```
host

name

data

value

item
```

---

# Playbooks

Playbooks should follow the format:

```
PB-<NUMBER>-<Name>.md
```

Examples:

```
PB-001-Discovery-Investigation.md
PB-002-Lateral-Movement.md
PB-003-Credential-Access.md
```

---

# Validation Guides

Validation guides should follow:

```
VAL-<NUMBER>-<Detection>.md
```

Examples:

```
VAL-001-Unauthorized-Host-Recon.md

VAL-002-Encoded-PowerShell.md
```

---

# Threat Hunting Queries

Threat hunting documents should use:

```
HUNT-<NUMBER>-<Name>.md
```

Examples:

```
HUNT-001-PowerShell-Abuse.md

HUNT-002-SMB-Recon.md
```

---

# Dashboard Files

Dashboard files should clearly identify the platform.

Examples:

```
Falcon-NGSIEM-Overview.json

PowerBI-SOC-Dashboard.pbix

Grafana-Network-Overview.json
```

---

# Scripts

Scripts should use lowercase with hyphens.

Examples:

```
build-lookups.ps1

generate-report.py

validate-rules.ps1

export-dashboard.py
```

---

# Images

Images should use lowercase.

Examples:

```
repository-architecture.png

rule-development-lifecycle.png

lookup-framework.png
```

---

# Versioning

Detection rules follow Semantic Versioning.

Format:

```
Major.Minor.Patch
```

Example:

```
1.0.0
```

Major

- Detection logic changes

Minor

- Performance improvements
- Lookup enhancements

Patch

- Documentation updates
- Metadata corrections

---

# Git Branches

Recommended naming:

```
feature/discovery-rules

feature/playbooks

bugfix/query-optimization

docs/update-readme

release/v1.0
```

---

# Commit Messages

Use short, descriptive commit messages.

Examples:

```
docs: add lookup framework

docs: update MITRE mapping guide

feat: add DISC-001 detection

feat: add PowerShell hunting query

fix: optimize aggregation logic

refactor: standardize lookup naming

test: validate DISC-001 detection

chore: update references
```

---

# Markdown Formatting

Use:

- ATX headings (`#`)
- Tables for structured information
- Fenced code blocks
- Relative links
- Sentence case headings

Avoid:

- HTML unless necessary
- Inline styling
- Excessive emojis

---

# Reserved File Names

The following filenames are standardized across all detection directories.

```
README.md

rule.cql

validation.md

investigation.md

tuning.md

references.md
```

Do not rename these files.

---

# Repository Consistency Checklist

Before submitting a contribution, verify:

- Naming convention followed
- Detection ID assigned
- Folder structure correct
- Query filename correct
- Documentation complete
- Lookup names standardized
- Markdown formatting validated
- Links verified

---

# Summary

Consistent naming standards improve navigation, simplify automation, and enhance collaboration across the project.

Following these conventions ensures that every detection, lookup, playbook, and document remains easy to locate, understand, and maintain as the repository grows.
