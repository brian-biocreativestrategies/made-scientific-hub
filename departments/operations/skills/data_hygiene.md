---
title: Data Hygiene
department: operations
version: 1.0
triggers: [hygiene, cleanup, quality, issues, data quality]
---

# Data Hygiene Tracking

Monitor and resolve data quality issues across Made Sci databases.

## Database (Data Hygiene DB: `kjdizfgqvammgrrhsgho`)

- **Tier 3 standalone tool**
- 263 tracked issues
- **Evaluate usage** — may be underutilized, consider consolidating

## Issue Types
- Duplicate records
- Missing required fields
- Inconsistent formatting
- Stale/outdated records
- Schema violations

## Key Queries

```sql
-- Open issues by severity
SELECT severity, COUNT(*) 
FROM issues 
WHERE status = 'open' 
GROUP BY severity;

-- Issues by table
SELECT target_table, COUNT(*) 
FROM issues 
WHERE status = 'open' 
GROUP BY target_table 
ORDER BY COUNT(*) DESC;
```
