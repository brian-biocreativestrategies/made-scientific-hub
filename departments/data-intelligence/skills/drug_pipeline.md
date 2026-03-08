---
title: Drug Pipeline Intelligence
department: data-intelligence
version: 1.0
triggers: [drug, candidate, molecule, therapy area, pipeline, pharma]
---

# Drug Pipeline Intelligence

Track drug candidates, company-drug relationships, and therapy area coverage.

## Database Tables (Transfer DB)

| Table | Key Columns | Unique Key |
|-------|-------------|------------|
| `drugs` | drug_name, generic_name, molecule_type, phase, indication | drug_name |
| `drug_company_relationships` | drug_id, company_id, relationship_type, confidence_score | (drug_id, company_id) |
| `drug_therapy_areas` | drug_id, therapy_area | (drug_id, therapy_area) |
| `drug_modalities` | drug_id, modality | (drug_id, modality) |

## Materialized Views
- Company-level modality aggregates
- Drug stats by phase and therapy area
- Refresh required after bulk data loads

## App Page
- `/drug-candidates` — Drug Candidates with filtering by phase, molecule type, therapy area, company

## Data Sources
- Hub DB bulk sync (initial + periodic)
- GlobalData via Sandbox Joe (`hcyqnlyseunynswgtwax`) — 6.3K drugs
