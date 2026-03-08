---
title: Clinical Trials Intelligence
department: data-intelligence
version: 1.0
triggers: [clinical trial, NCT, phase, modality, CAR-T, cell therapy, gene therapy]
---

# Clinical Trials Intelligence

Track and analyze clinical trials across cell and gene therapy modalities.

## Database Tables (Transfer DB)

| Table | Key Columns | Unique Key |
|-------|-------------|------------|
| `clinical_trials` | nct_id, title, phase, status, sponsor, modality, enrollment | nct_id |
| `trial_modalities` | trial_id, modality_name | (trial_id, modality_name) |

## Modalities Tracked (10)
1. Cell Therapy
2. MSC (Mesenchymal Stem Cell)
3. CAR-T
4. CAR-NK
5. Gene Therapy
6. Stem Cell
7. AAV (Adeno-Associated Virus)
8. TCR-T
9. Exosome
10. iPSC

## Data Source
- **ClinicalTrials.gov API v2** — Primary source
- Synced from Hub DB via initial bulk load + ongoing sync

## App Page
- `/clinical-trials` — Clinical Trials Tracker with phase filters, modality breakdown, sponsor search

## Trial Phases
- Phase 1, Phase 1/2, Phase 2, Phase 2/3, Phase 3, Phase 4, Not Applicable
