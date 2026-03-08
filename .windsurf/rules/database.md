# Database Operations Rules

> **Triggers:** `*.sql`, `schema_*.md`, `migrations/`
> **Globs:** `["**/migrations/**", "**/schema_*.md", "**/*.sql"]`

## Core Principles

1. **Never UPDATE without WHERE clause** - Always include filtering conditions
2. **Check duplicates before INSERT** - Use unique keys: `domain` for accounts, `linkedin_url` for contacts
3. **Use staging tables** for new data imports before promoting to production
4. **Include timestamps** - Always add `created_at`, `updated_at` on INSERT/UPDATE

## Production Database

- **Project ID:** `jrfcfayphcmaxsixxupu` (Transfer DB)
- **Key Tables:** `companies`, `leads`, `unmatched_leads`, `persona_scores`
- **Tables:** 299 total
- **Org:** Made Scientific (`udenwsiwwcsxngjptqxv`)

## Upstream (Read-Only Sources)

- **Hub DB:** `mjsgtszehjltxmbxtctz` (BioCreative org) — master life science data
- **ELG DB:** `kqzfrenfbfntwdnnbtlq` (BioCreative org) — team analytics

## ⚠️ Generated Column Rules (CRITICAL)

**When writing migrations that add GENERATED ALWAYS columns, you MUST also update all code that INSERTs into that table.**

Known generated columns:

| Table | Column | Expression |
|-------|--------|------------|
| `news_sources` | `url_hash` | `md5(url)` |
| `rss_articles` | `article_url_hash` | `md5(article_url)` |

**When creating a migration that:**
1. **Adds a GENERATED column** → Search all notebooks and scripts that INSERT into that table and remove the column from insert records
2. **Alters a table with existing GENERATED columns** → Verify insert code still works
3. **Error if violated:** `428C9: cannot insert a non-DEFAULT value into column`

## Quick Patterns

```sql
-- Safe upsert pattern
INSERT INTO table_name (...)
VALUES (...)
ON CONFLICT (unique_key) DO UPDATE SET
  field = EXCLUDED.field,
  updated_at = NOW();

-- Always use DRY_RUN for testing
-- Check row counts before and after operations
```
