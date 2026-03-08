---
title: Drug Pipeline
department: infrastructure
version: 1.0
triggers: [drug, candidate, molecule, therapy area, pipeline, modality]
---

# Drug Pipeline Intelligence

Track drug candidates and therapy areas in advanced therapies.

## Database Tables (Transfer DB — synced from Hub)

| Table | Purpose |
|-------|---------|
| `drug_candidates` | Drug/therapy pipeline records |
| `therapy_areas` | Therapeutic area taxonomy |

## App Page

- `/advanced-therapies` — Drug pipeline and modality analysis

## MADE AI Module

- Company Intelligence & Drug Pipeline Engine

## Data Sources

- GlobalData (via Sandbox Joe DB)
- Manual curation
- Clinical trial cross-reference
