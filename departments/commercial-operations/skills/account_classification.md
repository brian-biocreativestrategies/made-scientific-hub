---
title: Account Classification
department: commercial-operations
version: 1.0
triggers: [classify, enrichment, category, life science, AI classification]
---

# Account Classification

AI-powered account classification pipeline for categorizing companies.

## Classification Pipeline (Transfer DB)

```
New account → domain lookup → AI classification → category assignment → review
```

### Statuses

| Status | Meaning |
|--------|---------|
| `pending` | Awaiting classification |
| `classified` | AI has assigned category |
| `reviewed` | Human-verified |
| `reclassified` | Changed after review |

### Categories

- Technology Developer (TD)
- CRO/CDMO
- Academic/Research
- Service Provider
- Financial Partner
- Other

## Key Columns (companies table)

- `ai_classification` — AI-assigned category
- `ai_classification_confidence` — 0-1 confidence score
- `ai_classification_notes` — Reasoning
- `is_life_sciences` — Boolean flag

## MADE AI Module

- Cell Therapy Modality Classification System
- Company Matching & Deduplication Engine
