# MADE<>BioCreative Project Tracking

> **Last Updated:** March 12, 2026  
> **Maintained by:** Brian Elbert (BioCreative)  
> **For:** Joseph Sinclair, Lucy Taylor, Made Scientific team  
> **Gamma Deck:** [Made Scientific Command Center Overview](https://gamma.app/docs/Made-Scientific-Command-Center-Overview-1ewrjlm3mnnhpx1)  
> **Production:** `madescientificai.com` → `minimal-science-hub` → Transfer DB (`jrfcfayphcmaxsixxupu`)

---

## ✅ Completed

### Infrastructure Transfer (Phases 0–5, Mar 7–10)

| Phase | What | Date | Key Result |
|-------|------|------|------------|
| **Phase 0: Discovery** | Full audit of 13 BC + 11 Made Sci Supabase projects | Mar 7 | CMDO DB identified as migration target (161 tables, 188 views, 80+ functions) |
| **Phase 1: DB Migration** | CMDO DB → Transfer DB | Mar 7 | 299 tables, 260 views, 335 functions, ~175K rows synced, 5 pg_cron jobs, 9 edge functions, 9 auth users |
| **Phase 2: App Migration & Domain** | `madescientificai.com` → `minimal-science-hub` | Mar 10 | Domain transferred via IONOS DNS, 104 table refs verified, `.env.local` for dev |
| **Phase 4: Deactivate BC Assets** | Stop CMDO, fix sync, build Team Tracking UX | Mar 10 | 6 CMDO crons disabled, news sync fixed (0→799), social sync fixed (5,693→8,808), Team Tracking tabs built |
| **Phase 5: Master Git & Windsurf** | Build Made Sci brain repos | Mar 8 | 2 repos (`made-scientific-hub` + `MadeSciComandCenter`), 8 departments, 33 skills, 14 rules, 6 workflows |

### Platform & Data (Mar 10–11)

| Item | Date | Result |
|------|------|--------|
| **AI Second Brain** deployed on RAG Content DB | Mar 10 | 4 edge functions (brain-search, brain-router, brain-remember, brain-recall) live on `fdeyctgjudypbcqnmagw` — 99K+ knowledge chunks |
| **Clay enrichment 19-column upgrade** | Mar 11 | 19 dedicated columns on `leads`, 1,714 previously enriched leads backfilled, `process_clay_leads_enrichment()` dual-write |
| **Campaign tracker views rewired** | Mar 11 | 8 views rewritten to use `heyreach_leads_staging` (1,309 leads), 9 campaigns visible, 5 sending personas |
| **Push-to-Clay edge function** deployed | Mar 11 | `push-to-clay` deployed + cron every 15min, 5 leads queued — blocked on Vault secrets |
| **Campaign contacts fix + AI message gen UX** | Mar 12 | TS interface rewritten (38 real columns), `unified_campaign_contacts` view updated with `matched_lead_id`/`headline`/`sender_name`, 1,554 contacts visible in modals, outreach button wired — **AI gen blocked on Edge Function secrets** |

### Marketing Tasks Completed

| Item | Result |
|------|--------|
| **EmailBison mailboxes** warmed and ready | ✅ |
| **Outreach message generation flow** designed | UX creates campaign → Clay enriches contacts → AI generates personalized messages → review/edit → send via EmailBison |
| **Connection follow-up message generator** active | Live on Campaign Tracker |
| **Recent Connections section** added to Campaign Tracker | Live |

---

## 🔧 Active / This Week

### Marketing — Email Outreach (from Lucy call, Mar 11)

| Task | Owner | Status | Notes |
|------|-------|--------|-------|
| Campaign creation in UX — list builder + targeting by job title | Brian | In progress | Lucy wants to create campaigns herself; UI not yet added |
| Clay auto-enrichment on campaign add | Brian | In progress | Flow: add contacts → queue for Clay → enrich → populate columns |
| Per-contact AI message generation + review UI | Brian | **Blocked on Joe** | UX + edge function built & deployed; contacts load; "Generate" fails without `ANTHROPIC_API_KEY` in Edge Function secrets — see Blocker #5 |
| Inbox visibility — who responded to what campaign | Brian | In progress | EmailBison API has reply tracking; need UX component |
| Response → Salesforce flow (engaged lead → SQL) | Brian + Lucy | Planning | Reply → mark contact as "engaged" → push to SFDC as SQL (not MQL) |
| Nurture workflow — 3-month re-engagement | Brian | Planning | Auto re-run Clay, regenerate message, send follow-up after 3 months |
| Reply forwarding — send from campaign domain, CC rep's Gmail | Brian | Planning | Best solution discussed: first reply from Bison domain + CC rep, then rep takes over |
| HubSpot database overhaul — invalid contacts, automated cleanup | Lucy + Brian | Planning | Clay connector in HubSpot; schedule quarterly refresh via VPS cron |
| Friday team meeting — Brian, Lucy, Joe, Melody, Dustin | All | Scheduled | Lucy to confirm with Joe if full team joins |

### Data & Enrichment

| Task | Owner | Status | Notes |
|------|-------|--------|-------|
| **Contact consolidation** — 78K leads → `new_contacts` | Brian | Plan ready | 1,430 orphan companies to add first, then promote leads, dedup by LinkedIn URL |
| **4 Clay HTTP API fields** to add | Clay admin | Pending | `date_publications`, `url_publications`, `url_experience`, `picture_url_orig` |
| **Vault secrets** for push-to-Clay | Joe | Blocked | `CLAY_API_KEY` + `CLAY_WEBHOOK_URL` needed in Transfer DB Supabase Vault |
| **Account classification pipeline** | Brian | In progress | L1 (description-based) → L2 (deep enrichment) → AI summary; discussed with Lucy |

### Infrastructure

| Task | Owner | Status | Notes |
|------|-------|--------|-------|
| **VPS provisioning** (Phase 6) | Joe + Brian | Blocked | Joe's Hostinger verification code needed; VPS purchased Mar 8 (Ubuntu + Docker) |
| **n8n installation** on Made Sci VPS | Brian | After VPS | Self-hosted n8n for cron jobs, HeyReach sync, Clay automation |
| **Claude Code** on VPS | Brian | After VPS | Subscription-based, enables agent automation |
| **HeyReach .env** on VPS | Brian + Joe | Blocked | Need Transfer DB service role key |
| **UX cleanup** — strip to clean features | Brian | In progress | Mentioned in Lucy call; sandbox version coming after |

---

## 📋 Long-Term / Roadmap

### Phase 3: Sandbox Environment
- Separate Lovable app connected to same production DB for dev/testing
- Fork `minimal-science-hub` → `made-sci-sandbox`
- Sandbox URL (e.g., `sandbox.madescientificai.com`)

### Phase 6: VPS + n8n + RAG (after VPS provisioned)
- Made Sci's own VPS (NOT BioCreative's `168.231.69.81`)
- n8n instance for automated workflows (HeyReach sync, EmailBison sync, Clay enrichment, news/social)
- RAG Content DB paired with VPS + Obsidian — **blocked on Joe's review of embedding dimension mismatch** (stored 1024-dim vs query 512-dim)
- Slack bot for team
- Made Sci API keys needed: OpenAI + Anthropic (billed to Made Sci, not BC)

### Phase 7: Monday.com Rebuild
- New Monday → Transfer DB sync via n8n
- Build OKR features into production app (replace standalone `okr-command-center`)
- Monday MCP integration (30+ API endpoints) — skill built, ready to deploy

### Future Projects
- **3D facility rendering** — Joe interested; tested Nano Banana 2 + Gemini Pro approach for CAD → 3D (from JAM call)
- **Agent Brain automation** — news-triggered outreach, scheduled intelligence, BertBot dashboard
- **HubSpot CRM integration** — eventual Salesforce/HubSpot bridging
- **Atomic AI demo** — Brian to intro Lucy to founder via LinkedIn
- **Biotech startup game concept** — Joe's idea using Made Sci data (long-term R&D)

---

## Database Architecture

```
BioCreative Hub (mjsgtszehjltxmbxtctz) ─── syncs ──→ Transfer DB (jrfcfayphcmaxsixxupu) [PRODUCTION]
                                                       ├── 299 tables, all data
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
│   └── RAG Content (fdeyctgjudypbcqnmagw) → Knowledge base (99K chunks)
└── TIER 3 — Standalone Tools
    ├── Contracts (bexrfaoyhwzhnhzftdhy) — 71 clients, 84 MSAs
    ├── Revenue Forecasting (iyibciagadgbjuphzjvr) — 8.2K forecasts
    ├── RFI Library (nxkqurlesocrpabdjjal) — 404 responses
    ├── Data Hygiene (kjdizfgqvammgrrhsgho) — 263 issues
    └── KFSHRC (kazinkoexzjqvfhrtflo) — empty (reserved)

BioCreative Org (post-migration):
├── Hub DB (mjsgtszehjltxmbxtctz) → ACTIVE (syncs news/social/companies)
├── ELG DB (kqzfrenfbfntwdnnbtlq) → ACTIVE (syncs team metrics)
├── CMDO DB (zmeooytxphryrxiuzusg) → ARCHIVED (data migrated)
└── Monday DB (gcrsxhrxxinryhdrweyj) → STAYS IN BC (rebuild Phase 7)
```

---

## Git Repos

| Repo | Org | Purpose | Status |
|------|-----|---------|--------|
| `MADE-SCI/MadeSciComandCenter` | MADE-SCI | Master brain — depts, skills, workflows | ✅ Active |
| `MADE-SCI/made-scientific-hub` | MADE-SCI | Duplicate brain repo | ✅ Active |
| `MADE-SCI/minimal-science-hub` | MADE-SCI | Production app at `madescientificai.com` | Active |
| `MADE-SCI/made-demand-capacity-planner` | MADE-SCI | Demand/capacity planning | Active |
| `MADE-SCI/made-reporting-ux` | MADE-SCI | Reporting dashboard (4 DBs) | Active |
| `brian-biocreativestrategies/madescientificai2026` | BC | Old CMDO dashboard | Archived |
| `brian-biocreativestrategies/okr-command-center` | BC | OKR tracking | Stays in BC — rebuild Phase 7 |

---

## Team & Departments

| Person | Title | Department | Monday ID |
|--------|-------|-----------|-----------|
| **Joseph Sinclair** | Head of Commercial | ComLT (owner) | 68333015 |
| **Dustin Campbell** | Sr. Dir, Commercial Operations | ComLT, ComOps | 69791837 |
| **Lucy Taylor** | Mgr, Marketing | ComLT, Marketing | 76220564 |
| **Kyle Bullock** | Mgr, ComDev | ComDev | 80151228 |
| **Furat Goris** | Sr. Mgr, Tech Eval & Proposals | ComOps | 79257054 |
| **Kenneth Warrington** | Sr. Mgr, Tech Evaluations | ComOps | 98009454 |
| **Melody Rajkovich** | ComOps | ComOps | 79257053 |
| **Adam Haskett** | BD West | ComBD | 74735177 |
| **Karen Wu** | BD West | ComBD | 81162981 |
| **Chat De Silva** | BD East | ComBD | 70141778 |
| **Simona Jusyte** | BD East / Inside Sales | ComBD | 98616430 |
| **Allison Irrera** | Marketing | Marketing | 73128053 |
| **Jennie Mainyi** | Marketing | Marketing | 70326915 |
| **Michelle Ng** | — | — | 94939527 |
| **Brian Elbert** | BioCreative (admin) | Multi | 97495219 |

**8 Departments:** Commercial Leadership, Business Development, Commercial Operations, Marketing, Commercial Development, Partnerships, Operations, Infrastructure

---

## Meeting Log

| Date | Meeting | Participants | Key Outcomes |
|------|---------|-------------|--------------|
| **Mar 11** | Brian <> Lucy Connect | Brian, Lucy Taylor | EmailBison workflow reviewed; campaign creation UX needed; response → SFDC flow discussed; nurture workflow planned; Friday team meeting to schedule; Atomic AI intro; HubSpot cleanup via Clay |
| **Mar 8** | JAM (Joe 1:1) | Brian, Joseph Sinclair | VPS purchased (Hostinger, Ubuntu+Docker); n8n to install; Claude Code for VPS; 3D facility rendering idea (Nano Banana + Gemini); skills transfer discussed; floor plan test with Windsurf |
| **Mar 7** | Async (email) | Brian → Joe | Edge function secrets request; Windsurf workspace built; Monday MCP integration; VPS+n8n plan outlined |
| **Feb 13** | Full team meeting | Brian, Joe, Made team | Kickoff: "All Supabase data needs to move to Made's org"; Clay enrichment; RAG next big project; Monday ICPP board; CRM costs $66K/yr |
| **Jan 28** | Sync meeting | Brian, Joe | Infrastructure standardization; contact segmentation challenge (47K, 10% verified); revenue forecasting agent |

---

## Blockers / Open Questions

| # | Item | Owner | Status |
|---|------|-------|--------|
| 1 | **VPS verification code** — Joe needs to forward Hostinger email | Joe | Blocked |
| 2 | **Vault secrets** — `CLAY_API_KEY` + `CLAY_WEBHOOK_URL` in Transfer DB | Joe | Blocked |
| 3 | **4 Clay HTTP API fields** — add to Clay table action body | Clay admin (Joe/Lucy) | Pending |
| 4 | **RAG embedding dimension** — 512 vs 1024 mismatch, Joe to review options | Joe | Blocked |
| 5 | **Edge Function secrets** — `ANTHROPIC_API_KEY` (+ optional `OPENAI_API_KEY`) needed in Transfer DB Edge Function secrets **NOW** for AI message generation. Supabase Dashboard → Project Settings → Edge Functions → Secrets. 2 min task. | Joe | **Blocked 🔴** |
| 6 | **Joe's Sandbox UX** — needs Lovable access grant | Joe | Pending |
| 7 | **Salesforce push flow** — define MQL→SQL→pipeline gates with Joe | Joe + Lucy | Planning |
| 8 | **Friday team meeting** — confirm attendees and cadence | Lucy + Joe | Scheduling |
| 9 | **Transfer DB service role key** — needed for HeyReach .env on VPS AND push-to-Clay edge function | Joe | Blocked |

---

## Success Criteria

- [x] All Made Sci databases live in Made Sci Supabase org
- [x] `madescientificai.com` serves the upgraded `minimal-science-hub` build
- [x] CMDO DB archived, crons stopped
- [x] `made-scientific-hub` + `MadeSciComandCenter` repos operational
- [x] Hub syncs working (news, social, ELG team metrics)
- [x] AI Second Brain deployed on RAG Content DB
- [ ] Sandbox app available for dev/testing
- [ ] Made Sci VPS running with n8n and Claude Code
- [ ] Monday.com rebuilt in new infrastructure
- [ ] RAG Content paired with VPS + Obsidian pipeline
- [ ] EmailBison campaign creation + response tracking live in UX
- [ ] Salesforce integration for engaged leads

---

*Consolidated from 16 prior tracking documents. Source plan history in `.windsurf/plans/made-sci-*` files.*
