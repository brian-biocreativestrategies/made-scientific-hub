# Operations — Department CLAUDE.md

> **Scope:** Monday.com, OKRs, team management, contracts, data hygiene, internal tooling
> **Status:** Phase 7 (Monday Rebuild) is pending — this department will grow as Monday integration is rebuilt

---

## When to Load This

You are working on operations if the task involves:
- Monday.com boards, items, updates, or sync
- OKR tracking (Objectives & Key Results)
- Team management, user profiles, permissions
- Contract and agreement management
- Data hygiene tracking and cleanup
- Internal process improvement
- RFI library management

---

## Databases

| DB | Ref | Status | Key Data |
|----|-----|--------|----------|
| **Contracts & Agreements** | `bexrfaoyhwzhnhzftdhy` | Active | 71 clients, 84 MSAs |
| **Data Hygiene Tracking** | `kjdizfgqvammgrrhsgho` | Evaluate usage | 263 issues |
| **RFI Library** | `nxkqurlesocrpabdjjal` | Active | 404 responses, 199 questions |
| **KFSHRC Dashboard** | `kazinkoexzjqvfhrtflo` | Reserved | Empty — future development |

---

## Monday.com Integration (Phase 7 — Planned)

**Current state:** Old Monday DB (`gcrsxhrxxinryhdrweyj`) in BioCreative org with synced board data (134 boards, 2,110 items). OKR Command Center app exists but will be rebuilt.

**Planned rebuild:**
1. Design new Monday → Transfer DB sync via n8n
2. Build OKR features into production app (not separate app)
3. Clean up Monday boards (delete test boards, merge duplicates)

**Monday API:** GraphQL v2024-10
**Workspace ID:** 13639214 (MADE - 2026)

---

## Skills

| Skill | File | Purpose |
|-------|------|---------|
| Monday Integration | `skills/monday_integration.md` | Monday.com API and sync workflows |
| Contract Management | `skills/contract_management.md` | Agreement tracking and lifecycle |
| Data Hygiene | `skills/data_hygiene.md` | Data quality monitoring and cleanup |
