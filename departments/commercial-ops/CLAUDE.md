# Commercial Operations — Department CLAUDE.md

> **Scope:** Accounts, campaigns, HeyReach, EmailBison, pipeline management, social listening, events
> **Production App:** `minimal-science-hub` → Transfer DB (`jrfcfayphcmaxsixxupu`)

---

## When to Load This

You are working on commercial operations if the task involves:
- Account management, ICP scoring, company intelligence
- Campaign creation, tracking, or analytics (HeyReach + EmailBison)
- Social listening profiles, posts, engagements
- Event tracking, exhibitors, speakers, sessions
- Pipeline opportunities, deal tracking
- News intelligence, bookmarks
- Content Studio, post generation, LinkedIn content

---

## Key Database Tables (Transfer DB)

| Category | Tables |
|----------|--------|
| **Accounts** | `companies`, `leads`, `unmatched_leads`, `persona_scores` |
| **Campaigns** | `heyreach_campaigns`, `heyreach_leads`, `heyreach_campaign_leads`, `heyreach_daily_stats` |
| **Email** | `luella_campaigns`, `luella_contacts`, `luella_campaign_contacts`, `luella_daily_stats` |
| **Social** | `social_monitoring_profiles`, `social_posts`, `social_engagements` |
| **Events** | `events`, `event_exhibitors`, `event_speakers`, `event_sessions`, `event_contacts` |
| **News** | `client_news_intelligence`, `news_sources` |
| **Content** | `team_profiles`, `linkedin_hook_library`, `linkedin_content_pillars`, `content_generation_history` |
| **Pipeline** | `pipeline_opportunities`, `pipeline_activities` |

---

## Key Views

- `accounts_dashboard` — Main accounts view with enrichment status
- `campaign_tracker_campaigns` — Unified HeyReach + EmailBison campaigns
- `campaign_tracker_metrics` — Campaign performance metrics
- `unified_campaign_contacts` — All campaign contacts across platforms
- `social_listening_post_cards` — Social posts with engagement counts
- `social_listening_profile_summary` — Profile-level social metrics

---

## Edge Functions

| Function | Purpose |
|----------|---------|
| `heyreach-webhook` | Real-time webhook receiver for HeyReach campaign events |
| `generate-post-multi-source` | Content Studio AI generation |
| `generate-image-from-post` | AI image generation for posts |
| `bulk-export-briefing-sheets` | Export company briefing sheets as PDF |

---

## Cron Jobs (Transfer DB)

| Job | Schedule | Purpose |
|-----|----------|---------|
| `sync-news` | Every 8h | Sync news from Hub DB |
| `sync-social` | Every 4h | Sync social data from Hub DB |
| `sync-elg-team` | Every 4h | Sync team metrics from ELG DB |
| `company-extraction` | Daily | Extract companies from new leads |
| `clay-enrichment` | Every 5min | Process Clay enrichment queue |

---

## Skills

| Skill | File | Purpose |
|-------|------|---------|
| Campaign Tracker | `skills/campaign_tracker.md` | HeyReach + EmailBison campaign management |
| Event Data Collection | `skills/event_data_collection.md` | Conference/event intelligence pipeline |
| Social Listening | `skills/social_listening.md` | LinkedIn monitoring and engagement tracking |
| News Intelligence | `skills/news_intelligence.md` | News collection and sync pipeline |
| Content Studio | `skills/content_studio.md` | AI-powered content generation |
| Account Import | `skills/account_import.md` | Account import and classification pipeline |

---

## App Pages (minimal-science-hub)

| Route | Page | Data Source |
|-------|------|-------------|
| `/` | Dashboard | Multiple views |
| `/accounts` | Accounts | `companies`, `accounts_dashboard` |
| `/events` | Events | `events`, exhibitors, speakers, sessions |
| `/events/:id` | Event Detail | Event + all sub-tables |
| `/news` | News Intelligence | `client_news_intelligence` |
| `/social-listening` | Social Listening | Social views |
| `/post-generator` | Post Generator | Content Studio |
| `/campaigns/create` | Campaign Create | HeyReach API |
| `/reports/campaigns` | Campaign Reports | Campaign views |
| `/team-profile` | Team Profile | `team_profiles` |
