# Colab Notebook Rules

> **Triggers:** notebooks, data processing, enrichment, classification
> **Globs:** `["**/*.ipynb", "**/*.py"]`

## Standard Cell Structure

```python
# Cell 1: Configuration
import os
from supabase import create_client

SUPABASE_URL = os.environ.get('SUPABASE_URL')
SUPABASE_KEY = os.environ.get('SUPABASE_SERVICE_KEY')
DRY_RUN = True  # Always start with DRY_RUN

# Cell 2: Database connection
supabase = create_client(SUPABASE_URL, SUPABASE_KEY)

# Cell 3+: Processing logic
```

## Safety Rules

1. **Always use DRY_RUN mode** for testing
2. **Check row counts** before and after operations
3. **Use staging tables** for imports
4. **Log all operations** for audit trail
5. **Never use bare `except:` clauses** — always use `except Exception as e:` with logging
6. **Check for GENERATED columns before writing INSERT code**

## ⚠️ Generated Column Rules (CRITICAL)

These columns are **GENERATED ALWAYS** — PostgreSQL auto-computes them. **Never include them in INSERT or UPSERT records.**

| Table | Column | Expression |
|-------|--------|------------|
| `news_sources` | `url_hash` | `md5(url)` |
| `rss_articles` | `article_url_hash` | `md5(article_url)` |

- **OK:** `.eq("url_hash", hash)` in SELECT/WHERE for dedup
- **NOT OK:** `{"url_hash": hash}` in `.insert()` or `.upsert()`
- **Error:** `428C9: cannot insert a non-DEFAULT value into column`

## Target Database

All notebooks should target the **Transfer DB** (`jrfcfayphcmaxsixxupu`) unless explicitly working with a satellite DB.
