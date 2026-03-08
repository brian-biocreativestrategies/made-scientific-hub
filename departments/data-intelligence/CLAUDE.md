# Data Intelligence — Department CLAUDE.md

> **Scope:** Data pipelines, enrichment, classification, academic market, clinical trials, drug candidates, knowledge base
> **Production DB:** Transfer DB (`jrfcfayphcmaxsixxupu`)
> **Source DB:** Hub DB (`mjsgtszehjltxmbxtctz`) — BioCreative's master, syncs downstream

---

## When to Load This

You are working on data intelligence if the task involves:
- Data enrichment, classification, or quality pipelines
- Academic market: institutions, PIs, labs
- Clinical trials tracking and analysis
- Drug candidate pipeline and modality coverage
- Knowledge base management and RAG content
- Hub → Transfer DB sync functions
- GlobalData integration (Sandbox Joe)
- Database schema changes, migrations, views

---

## Key Database Tables (Transfer DB)

| Category | Tables |
|----------|--------|
| **Academic** | `academic_institutions`, `principal_investigators`, `labs` |
| **Trials** | `clinical_trials`, `trial_modalities` |
| **Drugs** | `drugs`, `drug_company_relationships`, `drug_therapy_areas`, `drug_modalities` |
| **Enrichment** | `enrichment_queue`, `enrichment_results` |
| **Knowledge** | Managed via RAG Content DB (`fdeyctgjudypbcqnmagw`) |

---

## Key Views

- `company_modality_aggregates` — Company-level modality rollup
- Materialized views (7): drug stats, trial stats, academic stats, etc.

---

## Sync Architecture

```
BioCreative Hub (mjsgtszehjltxmbxtctz)
    │
    ├── sync_news_from_life_science()      → client_news_intelligence
    ├── sync_social_from_life_science()     → social_monitoring_profiles, social_posts
    ├── sync_team_from_elg()               → team_profiles (from ELG DB)
    ├── extract_companies_from_leads()     → companies (from leads table)
    └── clay_enrichment_processor()        → enrichment results → companies
```

All sync functions run via pg_cron on the Transfer DB and pull data from Hub/ELG using `supabase_functions.http_request()`.

---

## Satellite Databases

| DB | Ref | Purpose | Queried By |
|----|-----|---------|------------|
| **Sandbox Joe** | `hcyqnlyseunynswgtwax` | GlobalData (23K investigators, 18K sites, 6.3K drugs) | `made-reporting-ux` |
| **Sandbox BC** | `kwadsfzzbhjytsruwmtw` | Hub mirror with new unified schema (228K contacts) | MCP queries |
| **RAG Content** | `fdeyctgjudypbcqnmagw` | 3.7K docs, 98K chunks — knowledge base | `made-reporting-ux`, future VPS |

---

## Skills

| Skill | File | Purpose |
|-------|------|---------|
| Academic Market | `skills/academic_market.md` | Institution, PI, lab intelligence |
| Clinical Trials | `skills/clinical_trials.md` | Trial tracking and modality analysis |
| Drug Pipeline | `skills/drug_pipeline.md` | Drug candidate intelligence |
| Account Classification | `skills/account_classification.md` | AI classification pipeline |
| Knowledge Base | `skills/knowledge_base.md` | RAG content management |
| Database Metrics | `skills/database_metrics.md` | DB health and analytics |

---

## App Pages (minimal-science-hub)

| Route | Page | Data Source |
|-------|------|-------------|
| `/clinical-trials` | Clinical Trials Tracker | `clinical_trials` |
| `/drug-candidates` | Drug Candidates | `drugs`, `drug_company_relationships` |
| `/academic-market` | Academic Market | Institutions, PIs, labs |
| `/knowledge-base` | Knowledge Base | RAG Content DB |
| `/database-analytics` | Database Analytics | Multiple tables |
| `/internal-intel` | Internal Intel | Mixed intelligence sources |
