# Lookup Framework

## Overview

Lookup tables are a fundamental component of detection engineering in CrowdStrike Falcon Next-Gen SIEM. They provide a centralized and maintainable mechanism for enriching events, reducing false positives, and adapting detections to environment-specific requirements.

Rather than embedding static values directly into detection queries, this repository uses lookup tables to identify trusted assets, privileged accounts, approved administrative systems, and other organizational context.

This approach improves rule readability, simplifies maintenance, and enables reusable detection logic across different environments.

---

# Objectives

The lookup framework is designed to:

- Reduce false positives
- Improve detection accuracy
- Eliminate hardcoded values
- Standardize detection development
- Simplify maintenance
- Support environment-specific tuning
- Promote reusable detection logic

---

# Lookup Architecture

```
Telemetry

      │

      ▼

Detection Query

      │

      ▼

Lookup Evaluation

      │

 ┌────┴────┐
 │         │
Match   No Match
 │         │
 ▼         ▼

Exclude  Generate Alert
```

---

# Repository Structure

```
lookups/

├── Allowed_Hosts.csv
├── Approved_Admin_Hosts.csv
├── Domain_Controllers.csv
├── Jump_Servers.csv
├── Privileged_Users.csv
├── Service_Accounts.csv
├── Sensitive_Servers.csv
├── Vulnerability_Scanners.csv
└── README.md
```

Each lookup should contain a single type of entity to keep ownership and maintenance straightforward.

---

# Naming Convention

Use descriptive names in **PascalCase** with underscores separating words.

| Lookup | Purpose |
|----------|----------|
| Allowed_Hosts.csv | Approved endpoints |
| Approved_Admin_Hosts.csv | Administrative workstations |
| Domain_Controllers.csv | Domain Controllers |
| Jump_Servers.csv | Jump hosts |
| Privileged_Users.csv | Administrative accounts |
| Service_Accounts.csv | Service accounts |
| Sensitive_Servers.csv | Critical infrastructure |
| Vulnerability_Scanners.csv | Authorized scanners |

Avoid ambiguous names such as:

- test.csv
- host.csv
- lookup.csv
- temp.csv

---

# CSV Standards

CSV files should include a header row.

Example:

```csv
ComputerName
WSUS01
ADMIN-PC01
HELPDESK-01
```

Example:

```csv
UserName
Administrator
svc_backup
svc_sql
```

Only include the columns required by the detection.

---

# Supported Entity Types

The repository currently recommends lookup tables for:

- Hosts
- Users
- IP Addresses
- Service Accounts
- Administrative Workstations
- Domain Controllers
- Jump Servers
- Security Tools
- Vulnerability Scanners
- Business Applications
- Approved Processes

---

# Query Integration

## Positive Match

Use `match()` when the detection should only apply to approved entities.

Example:

```cql
| match(file="Privileged_Users.csv",
        field=[UserName],
        column=UserName)
```

---

## Negative Match

Use `!match()` to exclude trusted entities.

Example:

```cql
| !match(file="Allowed_Hosts.csv",
         field=[ComputerName],
         column=ComputerName)
```

This is the preferred approach for reducing false positives.

---

# Lookup Design Principles

Every lookup should satisfy the following:

- One entity type per file
- Descriptive filename
- Consistent column names
- Minimal required fields
- Regular maintenance
- Documented ownership

---

# Performance Considerations

To maximize query performance:

- Keep lookup files focused.
- Remove obsolete entries.
- Avoid duplicate values.
- Normalize naming conventions.
- Use exact matching where possible.

Large lookup files should be periodically reviewed to ensure they remain efficient.

---

# Ownership

Every lookup should have an identified owner.

Example:

| Lookup | Owner |
|----------|--------|
| Allowed_Hosts.csv | SOC Engineering |
| Service_Accounts.csv | IAM Team |
| Domain_Controllers.csv | Active Directory Team |
| Jump_Servers.csv | Infrastructure Team |

Ownership ensures that lookup data remains accurate over time.

---

# Maintenance Process

Lookup files should be reviewed:

- Monthly
- After infrastructure changes
- Following major deployments
- After Active Directory updates
- During security reviews

Changes should follow normal change management procedures.

---

# Common Detection Use Cases

Lookup tables are commonly used to:

- Exclude administrative workstations
- Ignore vulnerability scanners
- Exclude approved service accounts
- Suppress expected automation
- Identify privileged users
- Validate authorized systems

---

# Best Practices

✔ Use lookups instead of hardcoded values.

✔ Keep lookups as small as practical.

✔ Validate lookup entries regularly.

✔ Document the purpose of each lookup.

✔ Reuse existing lookups whenever possible.

✔ Apply lookups early in the query to reduce unnecessary processing.

---

# Common Mistakes

Avoid the following:

- Hardcoding hostnames
- Combining unrelated entity types in one lookup
- Using inconsistent column names
- Leaving obsolete entries
- Creating duplicate lookup files
- Using generic filenames

These issues increase maintenance effort and reduce detection quality.

---

# Example Detection

Unauthorized Discovery Commands

```cql
#event_simpleName=ProcessRollup2
| FileName=/ipconfig\.exe|systeminfo\.exe|whoami\.exe/
| !match(
    file="Allowed_Hosts.csv",
    field=[ComputerName],
    column=ComputerName
)
```

Only hosts not present in the lookup will generate detection results.

---

# Repository Standards

Every detection that depends on environment-specific allowlists should reference a documented lookup file instead of embedding static values directly in the query.

This ensures that detection logic remains portable and reusable across different deployments.

---

# Summary

Lookup tables are a critical part of scalable detection engineering. They separate environment-specific knowledge from detection logic, reduce false positives, improve maintainability, and enable reusable CrowdStrike Falcon NG-SIEM detections.

All contributors should follow this framework when creating or modifying lookup-based detections.
