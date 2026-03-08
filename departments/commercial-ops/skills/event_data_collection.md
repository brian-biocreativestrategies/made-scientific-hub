---
title: Event Data Collection
department: commercial-ops
version: 1.0
triggers: [event, conference, exhibitor, speaker, session, booth]
---

# Event Data Collection

Collect and manage life science conference/event intelligence.

## Database Tables (Transfer DB)

| Table | Purpose | Key Columns |
|-------|---------|-------------|
| `events` | Master event list | name, start_date, end_date, location, event_type |
| `event_exhibitors` | Companies exhibiting | event_id, company_name, booth_number |
| `event_sponsors` | Event sponsors | event_id, company_name, sponsor_level |
| `event_speakers` | Speaker roster | event_id, speaker_name, title, company, session_title |
| `event_sessions` | Session schedule | event_id, title, track, time_slot, description |
| `event_contacts` | Contacts at events | event_id, contact_name, company, role |

## App Pages

| Route | Page | Features |
|-------|------|----------|
| `/events` | Events List | Filter by date, type, location. Featured event card |
| `/events/:id` | Event Detail | Tabs: Overview, Exhibitors/Sponsors, Speakers, Sessions, Contacts, Companies, Intelligence |
| `/events/:id/focused` | Event Focused Page | Template-based deep dive views |

## Data Collection Process

1. **Manual entry** — Add event via dashboard or SQL
2. **Exhibitor scraping** — Extract from event websites
3. **Speaker extraction** — Parse conference agendas
4. **Company matching** — Match exhibitors/speakers to `companies` table by domain
5. **Contact enrichment** — Link speakers to `leads` by LinkedIn URL

## Event Types
- Conference, Trade Show, Symposium, Workshop, Webinar, Summit
