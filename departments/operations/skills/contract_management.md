---
title: Contract Management
department: operations
version: 1.0
triggers: [contract, agreement, MSA, client, legal]
---

# Contract & Agreement Management

Track client contracts, MSAs, and agreement lifecycle.

## Database (Contracts DB: `bexrfaoyhwzhnhzftdhy`)

- **Tier 3 standalone tool**
- 71 clients tracked
- 84 MSAs (Master Service Agreements)
- No dedicated app UX — accessed via MCP or direct queries

## Key Queries

```sql
-- Active contracts summary
SELECT client_name, agreement_type, status, start_date, end_date
FROM agreements
WHERE status = 'active'
ORDER BY end_date;

-- Expiring soon
SELECT * FROM agreements
WHERE end_date BETWEEN NOW() AND NOW() + INTERVAL '90 days'
AND status = 'active';
```
