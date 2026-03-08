---
title: Data Hygiene
department: infrastructure
version: 1.0
triggers: [hygiene, cleanup, quality, issues, dedup, duplicate]
---

# Data Hygiene

Data quality tracking and cleanup across databases.

## Database

- **Data Hygiene DB** (`kjdizfgqvammgrrhsgho`)

## Issue Types

- Duplicate companies (domain match)
- Missing domains
- Stale classification data
- Orphaned contacts (no company link)
- Invalid email addresses

## Key Queries

```sql
-- Companies without domains
SELECT COUNT(*) FROM companies WHERE domain IS NULL OR domain = '';

-- Potential duplicates
SELECT domain, COUNT(*) FROM companies 
WHERE domain IS NOT NULL 
GROUP BY domain HAVING COUNT(*) > 1;
```
