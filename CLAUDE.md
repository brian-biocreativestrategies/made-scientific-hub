# CLAUDE.md — Made Scientific

> **Version:** 1.0 | **Last Updated:** March 8, 2026  
> Route to the right department. Load only what you need.  
> **Infra plan:** `docs/INFRASTRUCTURE_CONSOLIDATION.md`

---

## Identity

**Made Scientific** — AI-powered commercial intelligence platform for the life sciences industry.  
**Parent:** BioCreative Strategies (technology & data partner)  
**Production app:** `madescientificai.com` → `minimal-science-hub` repo → Transfer DB

---

## Department Routing

| Your Task | Department | Load This |
|-----------|-----------|-----------|
| Accounts, campaigns, HeyReach, EmailBison, social, events, news, content | **Commercial Ops** | `departments/commercial-ops/CLAUDE.md` |
| Data pipelines, enrichment, academic, clinical trials, drugs, knowledge base | **Data Intelligence** | `departments/data-intelligence/CLAUDE.md` |
| SFDC/HubSpot reporting, demand planning, revenue forecasting, analytics | **Reporting** | `departments/reporting/CLAUDE.md` |
| Monday.com, OKRs, contracts, data hygiene, internal tools | **Operations** | `departments/operations/CLAUDE.md` |

---

## Global Rules (apply everywhere)

1. **Production DB** = Transfer DB (`jrfcfayphcmaxsixxupu`) — NEVER delete production data without confirmation
2. **Hub-and-Spoke:** Data flows BioCreative Hub → Transfer DB only, never reverse
3. **Unique keys:** `domain` for accounts, `linkedin_url` for contacts — always check before INSERT
4. **No UPDATE without WHERE clause**
5. **All new tables need RLS policies**
6. **Staging tables** for all new data imports
7. **Timestamps:** Include `created_at`, `updated_at` on all tables
8. **DRY_RUN mode** for testing before production writes
9. **Windsurf + Claude** = primary work environment
10. Check **git status** before major changes
11. **NEVER run `npm install` locally** — all Lovable repos build remotely. Local `node_modules` waste disk and spike Windsurf memory. If accidentally created, delete immediately.

---

## Databases

**Production + Tier 1 (Git + Lovable UX):**

| Database | Project ID | Git Repo | Status |
|----------|------------|----------|--------|
| **Transfer DB** ★ | `jrfcfayphcmaxsixxupu` | `minimal-science-hub` | Production — 299 tables, all data |
| **Reporting DB** | `xyopyttkhoxvnyeyijzb` | `made-reporting-ux` | Active — SFDC/HubSpot |
| **Demand Planning DB** | `lyxvgbavbthyggeutzru` | `made-demand-capacity-planner` | Active — capacity/scheduling |

**Tier 2 (Active data, no own UX):**

| Database | Project ID | Purpose |
|----------|------------|---------|
| **Sandbox BC** | `kwadsfzzbhjytsruwmtw` | Hub mirror — new unified schema (228K contacts) |
| **Sandbox Joe** | `hcyqnlyseunynswgtwax` | GlobalData (23K investigators, 18K sites) |
| **RAG Content** | `fdeyctgjudypbcqnmagw` | Knowledge base (3.7K docs, 98K chunks) |

**Tier 3 (Standalone tools):**

| Database | Project ID | Purpose |
|----------|------------|---------|
| **Contracts** | `bexrfaoyhwzhnhzftdhy` | 71 clients, 84 MSAs |
| **Revenue Forecasting** | `iyibciagadgbjuphzjvr` | 8.2K monthly forecasts |
| **RFI Library** | `nxkqurlesocrpabdjjal` | 404 responses, 199 questions |
| **Data Hygiene** | `kjdizfgqvammgrrhsgho` | 263 issues |
| **KFSHRC** | `kazinkoexzjqvfhrtflo` | Empty — reserved for future dev |

**Upstream (BioCreative org — read-only sync sources):**

| Database | Project ID | Syncs To |
|----------|------------|----------|
| **Hub DB** (Life Science Master) | `mjsgtszehjltxmbxtctz` | → Transfer DB (news, social, companies) |
| **ELG DB** (Team Analytics) | `kqzfrenfbfntwdnnbtlq` | → Transfer DB (team metrics) |

---

## Workspaces

This master repo should be opened alongside the app repos in a multi-root Windsurf workspace:

```
Workspace roots:
├── made-scientific-hub           ← This repo (brain, rules, workflows, skills)
├── minimal-science-hub           ← Production app (React dashboard)
├── made-demand-capacity-planner  ← Demand planning app
└── made-reporting-ux             ← Reporting dashboard
```

All repos are under the `MADE-SCI` GitHub organization.

---

## Quick Terminology

| Term | Meaning |
|------|---------|
| **Transfer DB** | Production database — migrated from CMDO DB, lives in Made Sci org |
| **CMDO DB** | Legacy database in BioCreative org — archived, data migrated |
| **Hub-and-Spoke** | Architecture: BioCreative Hub feeds Made Sci Transfer DB (one-way) |
| **Hub DB** | BioCreative's master Life Science database — source of truth |
| **ELG** | Content Engine / LinkedIn Engager — team analytics platform |
| **HeyReach** | LinkedIn outreach automation platform |
| **EmailBison** | Email outreach platform (self-hosted at send.biocreativestrategies.com) |
| **Content Studio** | AI-powered content generation feature in the dashboard |
| **GlobalData** | Third-party life science data provider (Sandbox Joe) |

---

## Shared Resources

| Resource | Location |
|----------|----------|
| **Windsurf rules** | `.windsurf/rules/` (8 global + 4 department-scoped = 12) |
| **Windsurf workflows** | `.windsurf/workflows/` (6 slash commands) |
| **Skills** | `departments/*/skills/` (distributed by department) |
| **Scripts** | `scripts/` (utility scripts) |
| **Docs** | `docs/` (architecture, onboarding) |

---

*Made Scientific — AI-Powered Commercial Intelligence for Life Sciences*
