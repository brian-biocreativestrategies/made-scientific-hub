---
description: Switch context to a specific Made Sci database for MCP queries and operations
---

## /switch-db — Switch Database Context

When the user says "switch to [database]", update your working context to target the correct Supabase project.

### Database Registry

| Shortcut | Full Name | Project ID | Tier |
|----------|-----------|------------|------|
| `transfer` / `production` / `prod` | Transfer DB | `jrfcfayphcmaxsixxupu` | 1 |
| `reporting` | Reporting DB (SFDC/HubSpot) | `xyopyttkhoxvnyeyijzb` | 1 |
| `planner` / `demand` | Demand Planning DB | `lyxvgbavbthyggeutzru` | 1 |
| `sandbox-bc` | Sandbox Made BioCreative | `kwadsfzzbhjytsruwmtw` | 2 |
| `sandbox-joe` / `globaldata` | Sandbox Joe (GlobalData) | `hcyqnlyseunynswgtwax` | 2 |
| `rag` / `knowledge` | RAG Content DB | `fdeyctgjudypbcqnmagw` | 2 |
| `contracts` | Contracts & Agreements | `bexrfaoyhwzhnhzftdhy` | 3 |
| `forecasting` / `revenue` | Revenue Forecasting | `iyibciagadgbjuphzjvr` | 3 |
| `rfi` | RFI Library | `nxkqurlesocrpabdjjal` | 3 |
| `hygiene` | Data Hygiene Tracking | `kjdizfgqvammgrrhsgho` | 3 |
| `kfshrc` | KFSHRC Dashboard | `kazinkoexzjqvfhrtflo` | 3 |

### Upstream (BioCreative — read-only)

| Shortcut | Full Name | Project ID |
|----------|-----------|------------|
| `hub` | Life Science Master DB | `mjsgtszehjltxmbxtctz` |
| `elg` | ELG Team Analytics | `kqzfrenfbfntwdnnbtlq` |

### On Switch

1. Confirm which database you're switching to
2. Use the correct project ID for all subsequent MCP queries
3. If switching to an upstream DB, remind: "This is a BioCreative-owned read-only source"

### Return to Default

Say "switch to production" or "switch to transfer" to return to the main database.
