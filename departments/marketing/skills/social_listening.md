---
title: Social Listening
department: marketing
version: 1.0
triggers: [social, LinkedIn, monitoring, engagement, posts]
---

# Social Listening

LinkedIn monitoring and engagement tracking pipeline.

## Database Tables (Transfer DB)

| Table | Purpose |
|-------|---------|
| `social_listening_profiles` | Monitored LinkedIn profiles |
| `social_listening_posts` | Captured posts |
| `social_listening_engagements` | Post interactions |

## Sync Pipeline

Hub DB (`mjsgtszehjltxmbxtctz`) → Transfer DB via `sync_social_from_life_science()`

## App Page

- `/social-listening` — Engagement feed with filters

## MADE AI Module

- Social Listening & Engagement Tracking
- LinkedIn Sales Navigator Integration
