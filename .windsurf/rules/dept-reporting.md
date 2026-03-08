# Reporting — Department Rules

> **Globs:** `["departments/reporting/**"]`

When working on files in `departments/reporting/`, load this department's context:

## Quick Reference

- **Department CLAUDE.md:** `departments/reporting/CLAUDE.md`
- **Apps:** `made-reporting-ux` (4 DBs), `made-demand-capacity-planner` (2 DBs)
- **Scope:** SFDC/HubSpot reporting, demand planning, revenue forecasting

## Key Rules

1. **Reporting UX connects to 4 databases** — Reporting + Transfer + Sandbox Joe + RAG Content
2. **Demand Planner connects to 2 databases** — Demand Planning + Reporting
3. **PandaDoc integration** via `pandadoc-proxy` edge function on Demand Planning DB
4. **Revenue forecasting** is a standalone Tier 3 DB (`iyibciagadgbjuphzjvr`) — 8.2K forecasts
