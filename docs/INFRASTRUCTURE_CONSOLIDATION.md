# Made Scientific Infrastructure Consolidation — Reference

> **Source plan:** `C:\Users\elber\.windsurf\plans\made-sci-infra-consolidation-0d833d.md`
> **Last Updated:** March 8, 2026

---

## Migration Status

| Phase | Status |
|-------|--------|
| Phase 0: Discovery | ✅ Complete |
| Phase 1: DB Migration | ✅ Complete |
| Phase 2: App Migration & Domain | Pending |
| Phase 3: Sandbox Environment | Pending |
| Phase 4: Deactivate BC Assets | Pending |
| Phase 5: Master Git & Windsurf | ✅ Complete (this repo) |
| Phase 6: VPS, n8n, RAG | Pending |
| Phase 7: Monday Rebuild | Pending |

---

## Database Architecture

```
BioCreative Hub (mjsgtszehjltxmbxtctz) ─── syncs ──→ Transfer DB (jrfcfayphcmaxsixxupu) [PRODUCTION]
                                                       ├── 299 tables
                                                       ├── 9 edge functions
                                                       ├── 5 pg_cron jobs
                                                       └── 9 auth users

Made Sci Org (udenwsiwwcsxngjptqxv) — 11 projects:
├── TIER 1 — Core (Git + Lovable UX)
│   ├── Transfer DB (jrfcfayphcmaxsixxupu) → minimal-science-hub
│   ├── Reporting DB (xyopyttkhoxvnyeyijzb) → made-reporting-ux
│   └── Demand Planning (lyxvgbavbthyggeutzru) → made-demand-capacity-planner
├── TIER 2 — Active Data (no own UX)
│   ├── Sandbox BC (kwadsfzzbhjytsruwmtw) → Hub mirror (228K contacts)
│   ├── Sandbox Joe (hcyqnlyseunynswgtwax) → GlobalData
│   └── RAG Content (fdeyctgjudypbcqnmagw) → Knowledge base
└── TIER 3 — Standalone Tools
    ├── Contracts (bexrfaoyhwzhnhzftdhy) — 71 clients
    ├── Revenue Forecasting (iyibciagadgbjuphzjvr) — 8.2K forecasts
    ├── RFI Library (nxkqurlesocrpabdjjal) — 404 responses
    ├── Data Hygiene (kjdizfgqvammgrrhsgho) — 263 issues
    └── KFSHRC (kazinkoexzjqvfhrtflo) — empty (reserved)

BioCreative Org (post-migration):
├── Hub DB (mjsgtszehjltxmbxtctz) → ACTIVE (syncs to Transfer DB)
├── ELG DB (kqzfrenfbfntwdnnbtlq) → ACTIVE (syncs team metrics)
├── CMDO DB (zmeooytxphryrxiuzusg) → ARCHIVED (data migrated)
└── Monday DB (gcrsxhrxxinryhdrweyj) → STAYS IN BC (rebuild in Phase 7)
```

---

## Git Repos — Final State

| Repo | Org | Purpose | Status |
|------|-----|---------|--------|
| `MADE-SCI/made-scientific-hub` | MADE-SCI | Master brain — departments, skills, workflows | ✅ Built |
| `MADE-SCI/minimal-science-hub` | MADE-SCI | Production app at `madescientificai.com` | Active |
| `MADE-SCI/made-demand-capacity-planner` | MADE-SCI | Demand/capacity planning | Active |
| `MADE-SCI/made-reporting-ux` | MADE-SCI | Reporting dashboard (4 DBs) | Active |
| `brian-biocreativestrategies/madescientificai2026` | BC | Old CMDO dashboard | To Archive |
| `brian-biocreativestrategies/okr-command-center` | BC | OKR tracking | Stays in BC — rebuild Phase 7 |

---

## Remaining Phases

### Phase 2: Domain Transfer
- Transfer `madescientificai.com` from CMDO Lovable app to `minimal-science-hub`
- Connect `www.madescientificai.com`
- Verify all pages work on production

### Phase 3: Sandbox Environment
- Create sandbox Lovable app connected to same production DB
- Fork `minimal-science-hub` for sandbox repo

### Phase 4: Deactivate BC Assets
- Stop CMDO DB cron jobs, add "MIGRATED" prefix
- Update BioCreative CLAUDE.md references

### Phase 6: VPS + n8n + RAG
- Provision Made Sci VPS (separate from BC)
- Install n8n, migrate Made Sci workflows
- Pair RAG Content DB with VPS + Obsidian
- Build Slack bot

### Phase 7: Monday Rebuild
- Design new Monday → Transfer DB sync via n8n
- Build OKR features in production app
- Clean up Monday boards
