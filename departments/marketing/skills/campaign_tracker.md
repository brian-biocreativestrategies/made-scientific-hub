---
title: Campaign Tracker
department: marketing
version: 1.0
triggers: [campaign, HeyReach, EmailBison, outreach, LinkedIn]
---

# Campaign Tracker

Campaign management across HeyReach (LinkedIn) and EmailBison (email).

## Database Tables (Transfer DB)

| Table | Purpose |
|-------|---------|
| `heyreach_campaigns` | LinkedIn campaign metadata |
| `heyreach_leads` | Individual lead records |
| `campaign_leads` | Campaign-to-lead mapping |
| `daily_campaign_stats` | Daily metrics (sent, replied, connected) |
| `emailbison_campaigns` | Email campaign metadata |
| `emailbison_campaign_leads` | Email campaign contacts |
| `webhook_events` | Real-time webhook data |

## APIs

- **HeyReach API:** `https://api.heyreach.io/api/v1/`
- **EmailBison API:** `https://api.emailbison.com/api/`

## Edge Functions

- `heyreach-webhook` — Real-time campaign event receiver

## App Pages

- `/campaigns` — Campaign list with stats
- `/campaigns/:id` — Campaign detail with leads

## MADE AI Modules

- Campaign Automation & Outreach Platform
- Outbound Outreach Engine (Luella + HeyReach)
