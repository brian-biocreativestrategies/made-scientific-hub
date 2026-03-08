---
title: Pipeline Execution
department: business-development
version: 1.0
triggers: [pipeline, deal, opportunity, revenue, close, win]
---

# Pipeline Execution

BD pipeline management, deal progression, and revenue tracking.

## Monday Board

- **PROJECT_BD Pipeline Execution** (ID: 18393762882) — Revenue & Pipeline folder

## BD OKR Themes (both East and West)

- Book Revenue That Meets Target
- Build High-Quality Pipeline
- Shorten Sales Cycle
- Expand Through Partnerships

## Database Tables (Transfer DB)

| Table | Purpose |
|-------|---------|
| `companies` | Account records with pipeline_stage, engagement_priority |
| `leads` | Contact records linked to companies |
| `pipeline_opportunities` | Deal tracking with stage, value, assessment |

## App Pages

- `/accounts` — Account list with filters
- `/accounts/:id` — Account detail with intelligence tabs
- `/pipeline` — Sales pipeline board view
