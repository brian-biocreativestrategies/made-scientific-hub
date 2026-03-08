---
title: Revenue Forecasting
department: commercial-development
version: 1.0
triggers: [revenue, forecast, financial, projection, budget]
---

# Revenue Forecasting

Financial projection and revenue tracking.

## Database

- **Revenue Forecasting DB** (`iyibciagadgbjuphzjvr`)

## ComDev OKR

- **OKR1:** Revenue & Capacity Management (3 KRs)

## Key Queries

```sql
-- Revenue by quarter
SELECT quarter, SUM(amount) FROM revenue_entries GROUP BY quarter;

-- Forecast vs actual
SELECT period, forecast_amount, actual_amount FROM forecasts ORDER BY period;
```
