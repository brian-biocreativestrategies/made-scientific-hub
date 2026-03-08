---
title: Campaign Tracker
department: commercial-ops
version: 1.0
triggers: [campaign, HeyReach, EmailBison, outreach, LinkedIn]
---

# Campaign Tracker

Unified campaign management across HeyReach (LinkedIn) and EmailBison (email).

## Database Tables (Transfer DB: `jrfcfayphcmaxsixxupu`)

### HeyReach (LinkedIn)
| Table | Key Columns | Unique Key |
|-------|-------------|------------|
| `heyreach_campaigns` | campaign_id, name, status, stats | campaign_id |
| `heyreach_leads` | lead_id, linkedin_url, first_name, last_name | lead_id |
| `heyreach_campaign_leads` | campaign_id, lead_id, status, connection_status | (campaign_id, lead_id) |
| `heyreach_daily_stats` | campaign_id, date, connections_sent, messages_sent | (campaign_id, date) |
| `heyreach_webhook_events` | event_type, payload, processed_at | id |

### EmailBison (Email)
| Table | Key Columns | Unique Key |
|-------|-------------|------------|
| `luella_campaigns` | campaign_id, name, status | campaign_id |
| `luella_contacts` | contact_id, email, first_name, last_name | contact_id |
| `luella_campaign_contacts` | campaign_id, contact_id, status | (campaign_id, contact_id) |
| `luella_daily_stats` | campaign_id, date, emails_sent, opens, replies | (campaign_id, date) |

### Unified Views
- `campaign_tracker_campaigns` — Combined HeyReach + EmailBison campaigns
- `campaign_tracker_metrics` — Performance metrics across both platforms
- `unified_campaign_contacts` — All contacts across platforms

## HeyReach API
- **Base URL:** `https://api.heyreach.io/api/v1/`
- **Auth:** Bearer token
- **Webhook:** `heyreach-webhook` edge function on Transfer DB

## EmailBison API
- **Base URL:** `https://send.biocreativestrategies.com`
- **Auth:** Bearer token
- **Self-hosted instance**

## App Pages
- `/reports/campaigns` — Campaign Reports
- `/campaigns/create` — Campaign Creation
