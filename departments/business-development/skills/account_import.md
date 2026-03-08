---
title: Account Import
department: business-development
version: 1.0
triggers: [import, CSV, staging, accounts, companies]
---

# Account Import

Import accounts through the staging pipeline with validation and deduplication.

## Staging Pipeline (Transfer DB)

```
CSV/API → new_accounts_staging → validation → dedup → companies (production)
```

### Staging Statuses

| Status | Meaning |
|--------|---------|
| `needs_domain` | No domain — needs enrichment |
| `ready` | Has domain — ready for dedup |
| `duplicate` | Matches existing company |
| `promoted` | Moved to production |
| `rejected` | Failed validation |

## Deduplication

- **Primary key:** `domain` — always check `companies.domain` before promoting
- **Secondary:** Company name similarity

## Workflow

Use `/import-data` workflow for guided import process.
