---
trigger: department_match
description: Rules for Infrastructure (cross-cutting) department
globs: ["departments/infrastructure/**"]
---

# Infrastructure Rules

**Scope:** MADE AI platform, databases, data pipelines, Monday sync, knowledge base.
**Monday Board:** PROJECT_Infrastructure_08_MADE AI (ID: 18393762871) — 27 modules
**Project Folder:** Infrastructure & Systems (ID: 19118009)

## Rules

1. **MADE AI board** is the master feature tracker — 27 modules listed. Reference by item name when working on platform features.
2. **Monday DB** (`gcrsxhrxxinryhdrweyj`) is READ-ONLY from our tools. Sync from Monday API → DB. Never write back.
3. **Transfer DB** is the production database for all commercial data — 299 tables.
4. **Hub-and-Spoke** architecture: Hub DB → Transfer DB only. Never reverse the flow.
5. **RAG Content DB** (`fdeyctgjudypbcqnmagw`) — separate from Transfer DB. Knowledge base operations go here.
6. **Data hygiene** tracking in separate DB (`kjdizfgqvammgrrhsgho`).
7. **Generated columns** — `news_summary`, `social_summary` are generated. NEVER INSERT/UPDATE directly.
8. **Database changes** require migration through Supabase MCP — never raw DDL.
