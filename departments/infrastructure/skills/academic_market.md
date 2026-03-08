---
title: Academic Market
department: infrastructure
version: 1.0
triggers: [academic, institution, PI, lab, university, R1, Carnegie]
---

# Academic Market Intelligence

Track academic institutions, principal investigators, and research labs.

## Database Tables (Transfer DB — synced from Hub)

| Table | Purpose |
|-------|---------|
| `academic_institutions` | Universities, medical centers |
| `principal_investigators` | PIs with institutional affiliation |
| `labs` | Research labs with PI linkage |
| `nih_grants` | NIH funding data |

## Data Sources

- NIH Reporter API — grants and PIs
- Carnegie Classification — R1/R2 institutions
- ClinicalTrials.gov — trial-sourced PIs

## App Pages

- `/academic` — Academic market overview
- `/academic/:id` — Institution detail with PIs, labs, grants
