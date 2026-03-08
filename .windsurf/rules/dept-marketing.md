---
trigger: department_match
description: Rules for Marketing department
globs: ["departments/marketing/**"]
---

# Marketing Rules

**Scope:** Campaigns, content creation, social listening, news, events, brand authority.
**Monday Team:** Marketing (ID: 1307954)
**Key People:** Lucy Taylor (Mgr), Allison Irrera, Jennie Mainyi

## Rules

1. **Tradeshows & Events** tracker (95 items) is the source of truth for event planning — check before adding new events.
2. **Campaign data** flows: HeyReach/EmailBison API → Transfer DB → Dashboard. Never modify campaign data directly.
3. **Content Studio** uses `generate-content-multi-source` edge function — always include team_profile context.
4. **news_summary** is a **generated column** — NEVER INSERT/UPDATE it directly. Use `news_text`.
5. **Social listening** data syncs from Hub DB — read-only in Transfer DB.
6. **MQL-to-SQL** conversion engine (17 items) tracks the lead handoff process to BD.
