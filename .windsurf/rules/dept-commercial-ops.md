# Commercial Operations — Department Rules

> **Globs:** `["departments/commercial-ops/**"]`

When working on files in `departments/commercial-ops/`, load this department's context:

## Quick Reference

- **Department CLAUDE.md:** `departments/commercial-ops/CLAUDE.md`
- **Production App:** `minimal-science-hub` → Transfer DB (`jrfcfayphcmaxsixxupu`)
- **Scope:** Accounts, campaigns, HeyReach, EmailBison, social, events, news, content

## Key Rules

1. **Campaign data flows through webhooks** — HeyReach webhook → `heyreach-webhook` edge function → DB
2. **Social data syncs from Hub** — `sync_social_from_life_science()` runs every 4h via pg_cron
3. **News syncs from Hub** — `sync_news_from_life_science()` runs every 8h via pg_cron
4. **Content Studio uses edge functions** — `generate-post-multi-source` for text, `generate-image-from-post` for images
5. **Account imports use staging** — never insert directly into `companies`
