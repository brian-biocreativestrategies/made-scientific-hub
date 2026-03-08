# Data Intelligence — Department Rules

> **Globs:** `["departments/data-intelligence/**"]`

When working on files in `departments/data-intelligence/`, load this department's context:

## Quick Reference

- **Department CLAUDE.md:** `departments/data-intelligence/CLAUDE.md`
- **Production DB:** Transfer DB (`jrfcfayphcmaxsixxupu`)
- **Source DB:** Hub DB (`mjsgtszehjltxmbxtctz`) — BioCreative's master
- **Scope:** Data pipelines, enrichment, academic, clinical trials, drugs, knowledge base

## Key Rules

1. **Hub-Spoke sync is one-way** — Hub → Transfer DB only, never write back to Hub
2. **Sync functions use pg_cron** — company extraction (daily), news (8h), social (4h), ELG team (4h), clay (5min)
3. **Materialized views need REFRESH** after bulk data loads
4. **RAG Content DB** (`fdeyctgjudypbcqnmagw`) is a separate project — queries cross DB boundaries
5. **GlobalData lives in Sandbox Joe** (`hcyqnlyseunynswgtwax`) — read-only reference data
