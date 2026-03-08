# Infrastructure (Cross-Cutting)

MADE AI platform, data pipelines, database management, CRM integrations, and market intelligence data. Supports all departments — no single Monday team owner.

## Monday.com Mapping

| Element | Monday Reference |
|---------|-----------------|
| **MADE AI Board** | PROJECT_Infrastructure_08_MADE AI (ID: 18393762871) — 27 items |
| **Project Folder** | Infrastructure & Systems (ID: 19118009) |
| **Summary Board** | PROJECT_Infrastructure & Systems_2026 (ID: 18393644102) — 7 items |

## MADE AI Platform Modules (from Monday)

| Module | Status |
|--------|--------|
| Lead Scoring Engine v4 | Active |
| Company Intelligence & Drug Pipeline Engine | Active |
| Campaign Automation & Outreach Platform | Active |
| Clinical Trial Intelligence System | Active |
| Email Enrichment & Verification Pipeline | Active |
| Territory & Account Assignment Engine | Active |
| Event & Conference Intelligence Module | Active |
| GlobalData Integration & Data Pipeline | Active |
| Cell Therapy Modality Classification System | Active |
| AI-Powered Account Briefing Generator | Active |
| CRM Integration Layer (HubSpot & SFDC) | Active |
| Social Listening & Engagement Tracking | Active |
| News & Market Intelligence Feed | Active |
| Commercial Dashboard & Analytics Layer | Active |
| Outbound Outreach Engine (Luella + HeyReach) | Active |
| Meeting Intelligence & Transcription | Active |
| Proposal & Technical Evaluation System | Active |
| LinkedIn Sales Navigator Integration | Active |
| Funding & VC Intelligence Module | Active |
| Competitor Intelligence & Blacklist Management | Active |
| Marketing Content Hub & Creative Tools | Active |
| Client Management & Experience Portal | Active |
| Inbound Lead Capture & Form Management | Active |
| Miller Heiman Sales Methodology Integration | Active |
| CDMO Capability & Modality Offering Matrix | Active |
| Company Matching & Deduplication Engine | Active |
| Job Function & Persona Taxonomy Management | Active |

## Key Databases

| Database | Project ID | Purpose |
|----------|------------|---------|
| **Transfer DB** ★ | `jrfcfayphcmaxsixxupu` | Production — 299 tables |
| **Sandbox BC** | `kwadsfzzbhjytsruwmtw` | Hub mirror (228K contacts) |
| **Sandbox Joe** | `hcyqnlyseunynswgtwax` | GlobalData |
| **RAG Content** | `fdeyctgjudypbcqnmagw` | Knowledge base |
| **Data Hygiene** | `kjdizfgqvammgrrhsgho` | Quality tracking |

## Upstream (BioCreative — read-only)

| Database | Project ID | Sync |
|----------|------------|------|
| **Hub DB** | `mjsgtszehjltxmbxtctz` | → Transfer DB (news, social, accounts) |
| **ELG DB** | `kqzfrenfbfntwdnnbtlq` | → Transfer DB (team metrics) |

## Skills

| Skill | Triggers |
|-------|----------|
| `database_metrics` | metrics, analytics, database, counts, health |
| `knowledge_base` | knowledge base, RAG, documents, search |
| `monday_integration` | Monday, OKR, board, items, project tracking |
| `data_hygiene` | hygiene, cleanup, quality, issues |
| `academic_market` | academic, institution, PI, lab, university, R1 |
| `clinical_trials` | clinical trial, NCT, phase, modality, CAR-T |
| `drug_pipeline` | drug, candidate, molecule, therapy area, pipeline |
