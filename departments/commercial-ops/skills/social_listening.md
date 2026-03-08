---
title: Social Listening
department: commercial-ops
version: 1.0
triggers: [social, LinkedIn, monitoring, engagement, posts]
---

# Social Listening

LinkedIn monitoring and engagement tracking for competitive intelligence.

## Database Tables (Transfer DB)

| Table | Purpose | Sync Source |
|-------|---------|-------------|
| `social_monitoring_profiles` | Tracked LinkedIn profiles | Hub DB sync |
| `social_posts` | LinkedIn posts from monitored profiles | Hub DB sync |
| `social_engagements` | Likes, comments, shares on posts | Hub DB sync |

## Views
- `social_listening_post_cards` — Posts with engagement counts (uses lowercase engagement_type)
- `social_listening_profile_summary` — Profile-level metrics

## Sync Pipeline
- `sync_social_from_life_science()` runs every **4 hours** via pg_cron
- Data originates from PhantomBuster scrapers → Hub DB → Transfer DB

## App Page
- `/social-listening` — Social Listening dashboard with filter sidebar, post table, pagination

## Important: Engagement Type Case
- DB check constraint requires **lowercase** values: `'like'`, `'comment'`, `'share'`
- Views compare with lowercase — do NOT use uppercase comparisons
