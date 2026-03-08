---
title: Academic Market
department: data-intelligence
version: 1.0
triggers: [academic, institution, PI, lab, principal investigator, university, R1]
---

# Academic Market Intelligence

Track academic institutions, principal investigators, and labs in the life science space.

## Database Tables (Transfer DB)

| Table | Key Columns | Unique Key |
|-------|-------------|------------|
| `academic_institutions` | name, carnegie_classification, location_state, location_city | name |
| `principal_investigators` | name, institution_id, department, specialization, source_id | source_id |
| `labs` | name, institution_id, department, research_focus, location_state | (name, institution_id) |

## App Pages

| Route | Page | Features |
|-------|------|----------|
| `/academic-market` | Academic Market | Tabs: Institutions, PIs, Labs. Filters by state, classification, specialty |
| `/academic-market/institution/:id` | Institution Briefing | Full institution detail with PIs, labs, grants, trials |
| `/academic-market/labs/:id` | Lab Briefing | Lab detail with PIs and research focus |
| `/academic-market/pis/:id` | PI Briefing | PI detail with publications and grants |

## Data Sources
- **NIH Reporter** — Grant data linked to institutions and PIs
- **ClinicalTrials.gov** — Trial data linked to academic sites
- **Carnegie Classification** — Institution categorization (R1/R2/etc.)
- **Hub DB sync** — All data originates from BioCreative Hub

## Key Metrics
- R1 institutions tracked
- PIs with grant data
- Labs with research focus categorized
- Trials linked to academic institutions
