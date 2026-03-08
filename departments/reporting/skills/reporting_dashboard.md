---
title: Reporting Dashboard
department: reporting
version: 1.0
triggers: [SFDC, Salesforce, HubSpot, reporting, leads, pipeline]
---

# Reporting Dashboard

SFDC and HubSpot lead pipeline reporting and analytics.

## Database (Reporting DB: `xyopyttkhoxvnyeyijzb`)

| Table | Key Data |
|-------|----------|
| HubSpot leads | ~5K records |
| SFDC leads | ~423 records |

## App: made-reporting-ux

**Repo:** `MADE-SCI/made-reporting-ux`
**Connects to 4 databases:**
1. Reporting DB (`xyopyttkhoxvnyeyijzb`) — primary
2. Transfer DB (`jrfcfayphcmaxsixxupu`) — company intelligence
3. Sandbox Joe (`hcyqnlyseunynswgtwax`) — GlobalData reference
4. RAG Content (`fdeyctgjudypbcqnmagw`) — knowledge base

## Key Components
- `DashboardSidebar.tsx` — Navigation
- `KPICard.tsx` — Metric display cards
- `ChannelBreakdown.tsx` — Channel analytics
- `charts/` — Chart components
- `tables/` — Data table components

## Edge Functions
- `sync-hubspot/` — HubSpot data sync
- `sync-sfdc/` — Salesforce data sync
