---
name: Request security enforcement exemption
about: Request that a repository be excluded from automated security warnings and archiving
title: "[EXEMPT REQUEST] <repo-name>"
labels: 'exempt-request'
assignees: ''

---

## Exemption Request

* repo: repo-name
* justification: explain why this repository should be exempt from automated security enforcement

<!-- DO NOT EDIT BELOW THIS POINT -->

## Tips

#### Repository name

* Replace `<repo-name>` in the **issue title** with the exact repository name (not the full URL)
* The title must keep the `[EXEMPT REQUEST] ` prefix exactly as shown — the automation uses it
  to identify exemption requests
* Repository names are case-sensitive

#### What exemption means

* The repository will still be **scanned** and its alerts will appear in the daily CSV report
* Automated security tracking **issues will not be created or updated** for this repository
* The **Enforcer will not post warnings or archive** this repository, even if SLA deadlines are breached
* Exemption takes effect on the next scanner run (within 24 hours)

#### Justification

* Provide a clear reason why automated enforcement is not appropriate for this repository
* Examples: legacy archived project awaiting decommission, known false-positive alerts under review,
  third-party mirror with upstream-controlled dependency versions

