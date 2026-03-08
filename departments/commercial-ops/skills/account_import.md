---
title: Account Import
department: commercial-ops
version: 1.0
triggers: [import, accounts, CSV, staging, companies]
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
| `needs_domain` | No domain found — needs enrichment |
| `ready` | Has domain — ready for dedup check |
| `duplicate` | Matches existing company by domain |
| `promoted` | Successfully moved to production |
| `rejected` | Failed validation |
| `needs_cleanup` | Legacy junk data |

## Deduplication
- **Primary key:** `domain` — always check `companies.domain` before promoting
- **Secondary check:** Company name similarity (for cases where domain differs)

## Import Sources
- **CSV** — Direct upload, map columns to staging fields
- **Clay** — Enrichment API export
- **PhantomBuster** — LinkedIn scrape exports
- **Manual** — Individual account entry

## Key Tables
| Table | Purpose |
|-------|---------|
| `new_accounts_staging` | Staging table for imports |
| `companies` | Production accounts |
| `leads` | Contacts/leads linked to companies |
| `unmatched_leads` | Leads without company match |

## Workflow
Use `/import-data` workflow for guided import process.
