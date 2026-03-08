---
title: Database Metrics
department: infrastructure
version: 1.0
triggers: [metrics, analytics, database, counts, health, monitoring]
---

# Database Metrics

Monitor database health, table counts, and sync status across all Made Sci Supabase projects.

## Key Databases

| Database | Project ID | Tables |
|----------|------------|--------|
| Transfer DB (prod) | `jrfcfayphcmaxsixxupu` | ~299 |
| Monday DB | `gcrsxhrxxinryhdrweyj` | 15 |
| Reporting DB | `xyopyttkhoxvnyeyijzb` | — |
| Demand Planning DB | `lyxvgbavbthyggeutzru` | — |
| RAG Content DB | `fdeyctgjudypbcqnmagw` | — |

## Key Health Queries

```sql
-- Table row counts
SELECT schemaname, relname, n_live_tup 
FROM pg_stat_user_tables 
ORDER BY n_live_tup DESC LIMIT 20;

-- Sync log recent entries
SELECT sync_type, status, started_at, completed_at, records_processed
FROM sync_log ORDER BY started_at DESC LIMIT 10;

-- Materialized view freshness
SELECT schemaname, matviewname, last_refresh
FROM pg_matviews WHERE schemaname = 'public';
```

## Cron Job Monitoring

Check `cron.job` and `cron.job_run_details` for scheduled function health.
