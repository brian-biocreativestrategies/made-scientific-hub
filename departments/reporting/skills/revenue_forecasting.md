---
title: Revenue Forecasting
department: reporting
version: 1.0
triggers: [revenue, forecast, financial, projection]
---

# Revenue Forecasting

Financial projection and revenue tracking pipeline.

## Database (Revenue Forecasting DB: `iyibciagadgbjuphzjvr`)

- **Tier 3 standalone tool**
- ~8.2K monthly forecast records
- No dedicated app UX — accessed via MCP or direct queries

## Key Queries

```sql
-- Monthly revenue summary
SELECT 
  date_trunc('month', forecast_date) as month,
  SUM(forecast_amount) as total_forecast,
  SUM(actual_amount) as total_actual
FROM monthly_forecasts
GROUP BY 1
ORDER BY 1 DESC;
```

## Integration Points
- Demand Planning DB for capacity-based forecasting
- Reporting DB for pipeline-based projections
