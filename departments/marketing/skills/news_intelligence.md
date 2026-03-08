---
title: News Intelligence
department: marketing
version: 1.0
triggers: [news, articles, RSS, intelligence, bookmarks]
---

# News Intelligence

News collection and intelligence pipeline.

## Database Tables (Transfer DB)

| Table | Purpose |
|-------|---------|
| `news_sources` | RSS/API source configuration |
| `client_news_intelligence` | Collected news articles |
| `news_bookmarks` | Saved/starred articles |

## Sync Pipeline

Hub DB → Transfer DB via `sync_news_from_life_science()`

## Critical Rules

- `news_summary` is a **generated column** — never INSERT/UPDATE directly
- Always use `news_text` column for content

## App Page

- `/news` — News feed with filters and bookmarks

## MADE AI Module

- News & Market Intelligence Feed
