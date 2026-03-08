---
description: Import accounts or contacts through the staging pipeline with validation
---

## /import-data — Staging Pipeline Import

When the user invokes this workflow with data to import:

### Step 1: Identify the Import

Ask the user:
- **What data?** Accounts or contacts?
- **Source?** CSV file, API export, PhantomBuster, Clay, manual list
- **Target database?** Transfer DB (`jrfcfayphcmaxsixxupu`) or another Made Sci project?

### Step 2: Check Current Staging State

```sql
-- Check if staging table has existing data
SELECT status, COUNT(*) FROM new_accounts_staging GROUP BY status;
-- or
SELECT status, COUNT(*) FROM new_contacts_staging GROUP BY status;
```

If there's existing data in staging, ask whether to clear it first or append.

### Step 3: Load to Staging

For **CSV imports:**
- Read the CSV structure
- Map columns to staging table fields
- INSERT into `new_accounts_staging` or `new_contacts_staging`
- Set `status = 'needs_domain'` for accounts without domains, `'ready'` for those with domains

For **API/notebook imports:**
- Point to the appropriate Colab notebook or script

### Step 4: Domain Enrichment (Accounts Only)

If any rows have `status = 'needs_domain'`:

```sql
SELECT COUNT(*) FROM new_accounts_staging WHERE status = 'needs_domain';
```

Run domain enrichment (~$0.012/company).

### Step 5: Deduplication Check

```sql
-- Check for duplicates against production
SELECT s.company_name, s.domain, 'DUPLICATE' as reason
FROM new_accounts_staging s
JOIN companies a ON a.domain = s.domain
WHERE s.status = 'ready';
```

Mark duplicates: `UPDATE new_accounts_staging SET status = 'duplicate' WHERE domain IN (...)`.

### Step 6: Promote to Production

```sql
-- Promote ready accounts
INSERT INTO companies (company_name, domain, ...)
SELECT company_name, domain, ...
FROM new_accounts_staging
WHERE status = 'ready';

-- Mark as promoted
UPDATE new_accounts_staging SET status = 'promoted' WHERE status = 'ready';
```

### Step 7: Verify

```sql
-- Final counts
SELECT 'staging' as source, status, COUNT(*) FROM new_accounts_staging GROUP BY status
UNION ALL
SELECT 'production', 'total', COUNT(*) FROM companies;
```

Report: X promoted, Y duplicates skipped, Z need cleanup.
