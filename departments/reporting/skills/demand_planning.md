---
title: Demand Planning
department: reporting
version: 1.0
triggers: [demand, capacity, schedule, planning, PandaDoc, resource]
---

# Demand & Capacity Planning

Schedule management, capacity planning, and resource allocation.

## Database (Demand Planning DB: `lyxvgbavbthyggeutzru`)

| Table | Key Data |
|-------|----------|
| Capacity entries | ~960 records |
| PandaDoc contracts | ~88 records |

## App: made-demand-capacity-planner

**Repo:** `MADE-SCI/made-demand-capacity-planner`
**Connects to 2 databases:**
1. Demand Planning DB (`lyxvgbavbthyggeutzru`) — primary
2. Reporting DB (`xyopyttkhoxvnyeyijzb`) — cross-reference

## Key Features
- Schedule management views
- Capacity and resource allocation
- PandaDoc contract integration
- Forecasting hooks

## Edge Functions
- `pandadoc-proxy/` — PandaDoc API proxy for contract operations

## Hooks
- `useForecasting.ts` — Forecasting logic
- `useScheduleData.ts` — Schedule queries
- `useCapacityData.ts` — Capacity analytics
