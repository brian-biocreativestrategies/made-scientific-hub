---
title: News Intelligence
department: commercial-ops
version: 1.0
triggers: [news, articles, RSS, intelligence, bookmarks]
---

# News Intelligence

News collection, sync, and intelligence pipeline.

## Database Tables (Transfer DB)

| Table | Purpose |
|-------|---------|
| `client_news_intelligence` | Curated news articles synced from Hub |
| `news_sources` | RSS feed sources (has GENERATED column `url_hash`) |
| `rss_articles` | Raw RSS articles (has GENERATED column `article_url_hash`) |

## Sync Pipeline
- `sync_news_from_life_science()` runs every **8 hours** via pg_cron
- Pulls from Hub DB's `client_news_intelligence` table

## CRITICAL: Generated Columns
- `news_sources.url_hash` = `md5(url)` — NEVER include in INSERT
- `rss_articles.article_url_hash` = `md5(article_url)` — NEVER include in INSERT
- Error if violated: `428C9: cannot insert a non-DEFAULT value into column`

## App Page
- `/news` — News Intelligence with card grid, filters, detail modal, bookmarks
