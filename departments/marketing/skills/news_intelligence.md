---
title: News Intelligence
department: marketing
version: 1.1
triggers: [news, articles, RSS, intelligence, bookmarks]
---

# News Intelligence

News collection and intelligence pipeline. Articles flow from Life Science Hub DB → Transfer DB (`jrfcfayphcmaxsixxupu`) via `sync_news_from_life_science()` (pg_cron every 8h).

## Database Tables (Transfer DB)

| Table | Purpose | Rows |
|-------|---------|------|
| `news_intelligence` | Enriched articles synced from Hub | ~865 |
| `news_sources` | Local copy of Hub article sources | ~2,532 |
| `news_bookmarks` | User-bookmarked articles | — |
| `news_read_status` | User read tracking | — |
| `saved_news_searches` | Saved filter configurations | — |

## Key Views

| View | Purpose |
|------|---------|
| `v_news_intelligence_table` | Main view, ordered by `published_at` DESC |
| `company_news_intelligence` | JOIN with `companies` for company context |
| `v_news_intelligence_stats` | Aggregate stats (total, by priority, date ranges) |

## Sync Pipeline

Life Science Hub DB (`mjsgtszehjltxmbxtctz`) → Transfer DB via `sync_news_from_life_science()`
- **Client ID:** `09598398-741d-4233-85c4-6dab55317699`
- **Cron:** every 8 hours (`30 */8 * * *`)
- **Auth:** Vault secret `life_sci_service_key`

## Critical Rules

- Date column is `published_at` (TIMESTAMPTZ) — all views and frontend hooks read this
- `source_intelligence_id` is the dedup key (UNIQUE) linking back to Hub `client_news_intelligence.id`

## App Pages

- `/news-intelligence` — Full news feed with tabs (all/opportunities/competitors/priority)
- Dashboard → RecentNewsSection, StrategicAccountsSpotlight
- Company Briefing Sheet → CompanyIntelligenceSection
- Post Generator → NewsSourceTab (select news as content source)
