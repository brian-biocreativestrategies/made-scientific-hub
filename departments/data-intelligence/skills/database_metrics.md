---
title: Database Metrics
department: data-intelligence
version: 1.0
triggers: [metrics, analytics, database, counts, health, dashboard]
---

# Database Metrics & Analytics

Monitor database health, table sizes, and data quality across Made Sci projects.

## App Pages
- `/database-analytics` — Database Analytics dashboard
- `/internal-intel` — Internal Intelligence aggregated view

## Key Queries

```sql
-- Table row counts
SELECT schemaname, tablename, n_live_tup 
FROM pg_stat_user_tables 
ORDER BY n_live_tup DESC;

-- Enrichment pipeline status
SELECT enrichment_status, COUNT(*) 
FROM companies 
GROUP BY enrichment_status 
ORDER BY COUNT(*) DESC;

-- Sync job status
SELECT sync_type, status, MAX(completed_at) as last_run
FROM sync_log 
GROUP BY sync_type, status;
```

## Materialized Views (7 on Transfer DB)
All require `REFRESH MATERIALIZED VIEW` after bulk data loads.

## Cron Job Monitoring
| Job | Schedule | What to Check |
|-----|----------|---------------|
| company-extraction | Daily | New companies extracted from leads |
| news-sync | Every 8h | News articles synced from Hub |
| social-sync | Every 4h | Social data synced from Hub |
| elg-team-sync | Every 4h | Team profiles updated from ELG |
| clay-enrichment | Every 5min | Enrichment queue processing |
