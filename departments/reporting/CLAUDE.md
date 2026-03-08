# Reporting — Department CLAUDE.md

> **Scope:** SFDC/HubSpot reporting, demand & capacity planning, revenue forecasting, analytics dashboards
> **Apps:** `made-reporting-ux`, `made-demand-capacity-planner`

---

## When to Load This

You are working on reporting if the task involves:
- Salesforce or HubSpot data, lead scoring, pipeline reporting
- Demand planning, capacity scheduling, resource allocation
- Revenue forecasting and financial projections
- PandaDoc integration, contract tracking
- Cross-database analytics dashboards
- Data visualization, charts, KPI cards

---

## Databases

| DB | Ref | Git Repo | Key Data |
|----|-----|----------|----------|
| **Reporting DB** | `xyopyttkhoxvnyeyijzb` | `made-reporting-ux` | 5K HubSpot leads, 423 SFDC leads |
| **Demand Planning DB** | `lyxvgbavbthyggeutzru` | `made-demand-capacity-planner` | 960 capacity entries, 88 PandaDocs |
| **Revenue Forecasting DB** | `iyibciagadgbjuphzjvr` | — | 8.2K monthly forecasts |

---

## made-reporting-ux

**Repo:** `MADE-SCI/made-reporting-ux`
**Connects to 4 DBs:** Reporting + Transfer + Sandbox Joe + RAG Content

Key features:
- SFDC/HubSpot lead pipeline dashboards
- Customer intel from multiple data sources
- Channel breakdown analytics
- KPI cards and metric tracking

---

## made-demand-capacity-planner

**Repo:** `MADE-SCI/made-demand-capacity-planner`
**Connects to 2 DBs:** Demand Planning + Reporting

Key features:
- Schedule management and capacity planning
- PandaDoc contract integration (via edge function `pandadoc-proxy`)
- Revenue forecasting views
- Resource allocation tools

---

## Skills

| Skill | File | Purpose |
|-------|------|---------|
| Reporting Dashboard | `skills/reporting_dashboard.md` | SFDC/HubSpot reporting setup and maintenance |
| Demand Planning | `skills/demand_planning.md` | Capacity and scheduling workflows |
| Revenue Forecasting | `skills/revenue_forecasting.md` | Financial projection pipeline |
