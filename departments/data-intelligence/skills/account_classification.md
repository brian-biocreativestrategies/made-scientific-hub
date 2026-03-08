---
title: Account Classification
department: data-intelligence
version: 1.0
triggers: [classify, classification, enrichment, category, life science, sequester]
---

# Account Classification Pipeline

AI-powered account classification to categorize companies and filter non-life-science accounts.

## Pipeline Stages

```
L1 Light Enrich → L1 Classify → L2 Deep Enrich → L2 Classify → Summary
```

### Enrichment Statuses
| Status | Stage | Description |
|--------|-------|-------------|
| `needs_enrichment` | 1 | No description — needs L1 light enrichment |
| `needs_L1_classification` | 2 | Has description — needs core segment + LS flag |
| `needs_deep_enrichment` | 3 | L1 classified — needs L2 web research |
| `needs_L2_classification` | 4 | Has enrichment_data — needs detailed subcategory |
| `needs_summary` | 5 | Fully classified — needs human + AI summary |
| `complete` | 6 | Done |
| `sequestered` | — | Non-life-science, excluded from pipeline |
| `enrichment_failed` | — | Error during enrichment |

## Key Columns (companies table)
- `primary_category` — Top-level classification
- `enrichment_status` — Pipeline stage
- `enrichment_data` — JSONB from web research
- `ai_classification_notes` — AI reasoning
- `human_summary` / `ai_summary` — Final summaries

## Classification Categories
- `therapeutic_developer` — Drug/therapy development companies
- `service_provider` — CRO, CDMO, testing services
- `academic` — Universities, research institutions
- `financial_partner` — VCs, investors (typically sequestered)
- `not_classified` — Awaiting classification
