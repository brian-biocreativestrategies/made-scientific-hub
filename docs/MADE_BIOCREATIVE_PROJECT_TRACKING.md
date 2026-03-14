# MADE<>BioCreative Project Tracking — Master Plan

> **Last Updated:** March 13, 2026  
> **Maintained by:** Brian Elbert (BioCreative)  
> **For:** Joseph Sinclair, Lucy Taylor, Made Scientific commercial team  
> **Production:** `madescientificai.com` → `minimal-science-hub` → Transfer DB (`jrfcfayphcmaxsixxupu`)  
> **Gamma Deck:** [Made Scientific Command Center Overview](https://gamma.app/docs/Made-Scientific-Command-Center-Overview-1ewrjlm3mnnhpx1)  
> **Master Brain Repo:** `MadeSciComandCenter` (single source of truth)

---

## How This Doc Works

This document organizes all BioCreative↔Made Scientific work into **workstreams** (A–I). Each workstream shows what's **done**, what's **active**, and what's **planned**. It mirrors the transcript-to-work mapping plan so both docs track the same structure.

**Companion doc:** `.windsurf/plans/made-sci-transcript-work-mapping-cd576d.md` — raw transcript quotes + context behind each item below.

**Note:** This is a frozen mirror of `MadeSciComandCenter/docs/MADE_BIOCREATIVE_PROJECT_TRACKING.md`. All future updates go to MadeSciComandCenter only.

---

## A. API Keys & Secrets

The #1 blocker across multiple workstreams. Brian walked Joe through setting keys on the Mar 13 call.

### ✅ Done
- `push-to-clay` edge function v10 deployed (Mar 13) — hardcoded webhook URL + auth token as interim fix
- `generate-outreach-message` edge function deployed (Mar 12) — code complete, reads ANTHROPIC_API_KEY from secrets
- Clay webhook return configured — `import_clay_lead_enrichment` RPC works with anon key (SECURITY DEFINER)

### 🔧 Active — Verify What Joe Set on Call
| Secret | Location | Status |
|--------|----------|--------|
| `ANTHROPIC_API_KEY` | Transfer DB → Edge Function Secrets | ⚠️ Joe was adding live on call — **verify** |
| `CLAY_API_KEY` | Transfer DB → Vault | ⚠️ Joe was adding live on call — **verify** |
| `CLAY_WEBHOOK_URL` | Transfer DB → Vault | ⚠️ Joe was adding live on call — **verify** |
| `OPENAI_API_KEY` | Transfer DB → Edge Function Secrets | Unknown — not discussed on call |
| Service Role Key | Joe to share with Brian | ❌ Still needed — blocks HeyReach sync + Clay push |
| Hostinger VPS verification | Joe's login → code to email | ❌ Still blocked |

### 📋 Planned
- Made Sci API accounts (OpenAI + Anthropic) billed to Made Sci, not BC
- All VPS secrets (.env) once VPS is provisioned

---

## B. RAG / Knowledge Base

Joe has his own RAG system (3,800 docs / 100K chunks / 57 proposals / 5K proposal chunks) in a separate Lovable UX. BioCreative has the AI Second Brain on RAG Content DB. These need to converge.

### ✅ Done
- AI Second Brain deployed on RAG Content DB (`fdeyctgjudypbcqnmagw`) — 4 edge functions (brain-search, brain-router, brain-remember, brain-recall), 99K+ knowledge chunks
- Joe's RAG ingestion code — PDF breakdown → whole doc + chunks → Supabase, working in his Lovable project
- Joe demoed RAG chatbot to full team (Mar 13) — MSC manufacturing protocol from adipose tissue, customer proposal generation

### 🔧 Active
| Task | Owner | Status | Notes |
|------|-------|--------|-------|
| Define clean RAG architecture — where content types live | Brian + Joe | Discussion needed | Joe: "we just need to come up with a really clean architecture as to where certain data lies within a database" |
| Embedding dimension mismatch | Joe + Brian | Blocked | Stored 1024-dim vs query 512-dim — Joe to review options, may require full re-vectorize |
| Google Drive integration for auto doc ingestion | Joe priority | Planning | Joe wants automated pipeline from GDrive → chunk → embed |

### 📋 Planned
- Merge Joe's 3,800 docs + proposal chunks into unified RAG architecture
- **Chatbot in Made AI dashboard** — Dustin + Joe confirmed it should live in the app, not separate
- Re-vectorize with improved chunking/embedding if methodology changes
- Partitioned content types: proposals, modality playbooks, regulatory, client docs, RFI responses, brand positioning
- RAG → custom presentation generation via Figma templates (Joe's vision)

---

## C. Campaign System & Outreach

The most immediate revenue-impacting workstream. 417 MSC contacts ready, NK/TIL campaigns being planned, 290 warm LinkedIn connections never followed up.

### ✅ Done
- EmailBison mailboxes warmed and ready
- Outreach message generation flow designed: campaign → Clay enrich → AI generate → review/edit → send via EmailBison
- Connection follow-up message generator live on Campaign Tracker
- Recent Connections section added to Campaign Tracker
- Campaign tracker views rewired (Mar 12) — 5 migrations, stale Feb 3 data → fresh Mar 12 data from `heyreach_campaign_leads`
- `unified_campaign_contacts` view — 1,315 contacts across 16 campaigns
- Campaign contacts fix + AI message gen UX (Mar 12) — TS interface (38 real columns), outreach button wired
- MSC Email campaigns created — 417 contacts across 10 territory campaigns
- Campaign reports generated — history/results + MSC/NK/TIL campaign plan sent to Lucy (Mar 13)
- Clay enrichment pipeline v10 deployed (Mar 13) — push-to-clay + webhook return, 2,253 enriched / 100,747 total leads

### 🔧 Active
| Task | Owner | Status | Notes |
|------|-------|--------|-------|
| AI message generation | Brian | **Blocked on ANTHROPIC_API_KEY** | UX + edge function deployed; "Generate" fails without key |
| Campaign creation UX — list builder + targeting | Brian | In progress | Lucy wants to create campaigns herself |
| Clay auto-enrichment on campaign add | Brian | In progress | add contacts → queue → Clay → populate |
| Persona classification filtering | Brian | In progress | Exclude unwanted roles from campaigns (Lucy request) |
| Fix modality filters | Brian | In progress | Broken — need alignment with Salesforce + GlobalData |
| 290 warm connection follow-ups | Brian + team | Ready | Immediate opportunity — no new tooling needed |
| Loom tutorial videos | Brian | Committed | End-to-end campaign creation walkthrough |
| Campaign training session | Joe request | Next week | Everyone logged in, focused on list builder + outreach |

### 📋 Planned
- **NK Cell Therapy campaign:** 44 companies, ~1,800 leads
- **TIL Therapy campaign:** 13 companies, ~1,300 leads
- Dual-channel strategy: HeyReach (LinkedIn) + EmailBison (email) for all campaigns
- Inbox visibility — EmailBison API reply tracking → UX component
- Response → Salesforce flow (engaged lead → SQL, not MQL)
- Nurture workflow — 3-month re-engagement (re-Clay, regenerate, follow-up)
- Reply forwarding — Bison domain + CC rep's Gmail, then rep takes over
- Unified inbox system — email replies integrated with reps' accounts
- PhantomBuster running to discover more contacts at target accounts
- Target Universe tab — live account status management in UX (Lucy request)

### Waiting on Lucy
- Full 3,800 MSC contacts spreadsheet for enrichment/campaign setup
- Blacklists and segmented lists from HubSpot → build target universe + filtering
- Explore Atomic AGI app for SEO/AI visibility (Brian to intro founder)

---

## D. Skills & Content Generation

Skills = modular AI capabilities the brain agent can invoke. 3D rendering, video generation, content creation all proven as skills. The RAG brain is the unlock that makes skills richer.

### ✅ Done
- 3D facility floor plan rendering — tested with Nano Banana 2 + Gemini Pro for CAD → 3D
- Video generation — 10-second clips stitched together via AI video gen
- Content Studio (post generator) — `generate-content-multi-source` edge function live
- Outreach message generator — `generate-outreach-message` edge function deployed
- Content agent built (v1.0) — 8 registered tools, 19 brand mappings, 5 content types
- 33 skills documented across 8 departments in MadeSciComandCenter
- Monday MCP integration skill — 30+ API endpoints, ready to deploy

### 🔧 Active
| Task | Owner | Status | Notes |
|------|-------|--------|-------|
| Content Studio polish | Brian | In progress | Multi-source post generation, Claude primary + OpenAI fallback |
| Skill catalog organization | Brian + Dustin | In progress | Department-specific branches in master command center |

### 📋 Planned
- RAG-powered presentation generator via Figma templates (Joe's vision)
- Proposal content generation from RAG — 57 proposals already chunked
- News-triggered outreach — automated intelligence → personalized message
- Weekly automated product update emails + bug reporting feature
- BertBot dashboard agent automation

---

## E. Sales Pipeline & Operations Dashboard

Joe is building operations/demand planning himself. BioCreative supports with SFDC sync, PandaDoc integration, and data surfacing.

### ✅ Done
- `made-demand-capacity-planner` app live — connected to Demand Planning DB (`lyxvgbavbthyggeutzru`)
- `made-reporting-ux` — reporting dashboard connected to 4 DBs, SFDC/HubSpot sync edge functions scaffolded
- Revenue Forecasting DB — 8.2K forecasts
- Strategic Dashboard rewired (Mar 12) — KPIs populated from `v_company_briefing_complete`
- 6 stub hooks replaced with real DB queries in `made-sci-queries.ts`

### 🔧 Active
| Task | Owner | Status | Notes |
|------|-------|--------|-------|
| SFDC sync work | Brian | In progress | `made-reporting-ux` — sync-sfdc edge function |
| Modality data filters | Brian | In progress | Alignment with Salesforce + GlobalData, broken filters reported |
| Operations demand planning | Joe | Joe's build | Suite utilization, manufacturing run demand by year |

### 📋 Planned
- Salesforce pipeline data surfaced in dashboard (no SFDC license needed for whole team)
- PandaDoc API integration — direct links from dashboard to proposals
- Monday.com data on frontend — project tracking visibility
- Manufacturing suite utilization tables
- Clinical trials by modality — Joe already pulling into his UX, needs filter fixes
- Cost/price data in RAG → quick budgetary estimates from chatbot

---

## F. Team Access & Login

Team reported login/access issues at Mar 13 training. Need all 9 users verified before next session.

### ✅ Done
- 9 auth users created in Transfer DB
- 5 team profiles in `team_profiles` table
- `user_profiles` table with RLS policies (permissive SELECT for login)

### 🔧 Active
| Task | Owner | Status | Notes |
|------|-------|--------|-------|
| Verify all 9 auth users can log in | Brian | Immediate | Audit `user_profiles` vs auth users |
| Distribute fresh credentials | Brian | Before next training | Email each team member |
| UX cleanup — strip to clean features | Brian | In progress | Remove broken/dev features before team uses |

### 📋 Planned
- Sandbox app for dev/testing (`sandbox.madescientificai.com`)
- Role-based access — different views per department

---

## G. Git Repos & Organization

Joe wants a Git catalog feature in the UX. Brain repo duplication resolved — MadeSciComandCenter is master.

### ✅ Done
- `MadeSciComandCenter` = **single master brain** — 8 departments, 33 skills, 14 rules, 6 workflows, brands, scripts, docs
- `made-scientific-hub` = lightweight reference for Joe's standalone workspace (frozen — no longer maintained separately)
- Master GitHub project organization reviewed on Joe/Bert call

### Repos

| Repo | Org | Purpose | Status |
|------|-----|---------|--------|
| `MADE-SCI/MadeSciComandCenter` | MADE-SCI | **Master brain** — depts, skills, workflows, scripts | ✅ Active |
| `MADE-SCI/made-scientific-hub` | MADE-SCI | Joe's reference brain (frozen mirror) | ✅ Frozen |
| `MADE-SCI/minimal-science-hub` | MADE-SCI | Production app at `madescientificai.com` | ✅ Active |
| `MADE-SCI/made-demand-capacity-planner` | MADE-SCI | Demand/capacity planning | Active |
| `MADE-SCI/made-reporting-ux` | MADE-SCI | Reporting dashboard (4 DBs) | Active |
| `brian-biocreativestrategies/madescientificai2026` | BC | Old CMDO dashboard | Archived |
| `brian-biocreativestrategies/okr-command-center` | BC | OKR tracking | Stays in BC — rebuild Phase 7 |

### 📋 Planned
- **Git catalog tab in UX** — Joe wants a tab showing all repos, purposes, status (for Dustin + team)
- Dustin to explore Git + VPS automation workflows
- Department-specific branches in master command center

---

## H. Infrastructure & VPS

Phase 6 blocked on VPS provisioning. Everything else dependent on this.

### ✅ Done — Infrastructure Transfer (Phases 0–5, Mar 7–10)

| Phase | What | Date | Key Result |
|-------|------|------|------------|
| **Phase 0: Discovery** | Audit 13 BC + 11 Made Sci Supabase projects | Mar 7 | CMDO DB identified as migration target |
| **Phase 1: DB Migration** | CMDO DB → Transfer DB | Mar 7 | 318 tables, 264 views, 355 functions, ~175K rows, 5 crons, 11 edge functions, 9 auth users |
| **Phase 2: App Migration** | `madescientificai.com` → `minimal-science-hub` | Mar 10 | Domain via IONOS DNS, 104 table refs verified |
| **Phase 4: Deactivate BC** | Stop CMDO, fix syncs, Team Tracking UX | Mar 10 | 6 crons disabled, news 0→865, social 5,693→9,249 |
| **Phase 5: Master Git** | Build Made Sci brain repos | Mar 8 | 2 repos, 8 departments, 33 skills, 14 rules |

### 🔧 Active — Blocked Items
| Task | Owner | Status | Blocker |
|------|-------|--------|---------|
| VPS provisioning (Phase 6) | Joe + Brian | **Blocked** | Hostinger verification code from Joe |
| n8n on Made Sci VPS | Brian | After VPS | Self-hosted n8n for crons, HeyReach sync, Clay, news/social |
| Claude Code on VPS | Brian | After VPS | Subscription-based agent automation |
| HeyReach .env on VPS | Brian + Joe | **Blocked** | Need Transfer DB service role key |

### 📋 Planned
- **Phase 3: Sandbox** — fork `minimal-science-hub` → `made-sci-sandbox`
- **Phase 6: VPS + n8n + RAG** — Made Sci's own VPS, n8n, Slack bot
- **Phase 7: Monday.com Rebuild** — new Monday → Transfer DB sync via n8n, OKR features in app
- HubSpot database overhaul — Clay connector, quarterly refresh via VPS cron

---

## I. Data & Enrichment

### ✅ Done
- Clay enrichment 19-column upgrade (Mar 11) — 19 columns on `leads`, 1,714 backfilled
- Push-to-Clay edge function v10 (Mar 13) — new webhook URL + auth, sends individually
- Clay webhook return — `import_clay_lead_enrichment` RPC, `process_clay_leads_enrichment()` dual-write
- Bug fix: empty timestamp crash + `attempted` status for no-data leads
- Company alias system — 208 aliases for fuzzy event-company matching
- Company match queue — 2,447 queued for review
- Campaign tracker views rewired to `heyreach_campaign_leads` (5 migrations, Mar 12)

### 🔧 Active
| Task | Owner | Status | Notes |
|------|-------|--------|-------|
| Contact consolidation — 100K leads → `new_contacts` | Brian | Plan ready | 1,430 orphan companies first, then promote, dedup by LinkedIn URL |
| 4 Clay HTTP API fields | Clay admin | Pending | `date_publications`, `url_publications`, `url_experience`, `picture_url_orig` |
| Account classification pipeline | Brian | In progress | L1 (description) → L2 (deep enrichment) → AI summary |
| Clay enrichment pipeline verification | Brian | Needs check | Verify CLAY_API_KEY + WEBHOOK_URL in Vault after Joe's call |

### 📋 Planned
- HubSpot ↔ Clay automated sync (API/CSV export-import framework)
- Clinical trials data layer — Joe pulling by modality into UX
- Web crawls + API pulls for therapeutic developer accounts

---

## Transfer DB Live Counts (Mar 13, 5:45 PM)

| Metric | Count |
|--------|-------|
| **Tables** | 318 |
| **Views** | 264 |
| **Functions** | 355 |
| **Edge Functions** | 11 |
| **Companies** | 3,805 |
| **Leads/Contacts** | 100,747 |
| **Drug Candidates** | 5,487 |
| **Clinical Trials** | 4,783 |
| **Campaigns** | 37 |
| **HeyReach Campaign Leads** | 1,186 |
| **News Intelligence** | 865 |
| **Social Posts** | 340 |
| **Social Engagements** | 9,249 |
| **Events** | 92 |
| **Event Companies** | 825 |
| **Company Name Aliases** | 208 |
| **Company Match Queue** | 2,447 |
| **Clay Enriched** | 2,253 |
| **Clay Staging** | 4,963 |
| **Auth Users** | 9 |

### Edge Functions (11 active)
`heyreach-webhook` · `transcribe-interview` · `diagnose-event-contacts` · `bulk-export-briefing-sheets` · `generate-post-multi-source` · `generate-image-from-post` · `download-document` · `transcribe-audio` · `sync-made-sci-data` · `generate-outreach-message` · `push-to-clay`

---

## Database Architecture

```
BioCreative Hub (mjsgtszehjltxmbxtctz) ─── syncs ──→ Transfer DB (jrfcfayphcmaxsixxupu) [PRODUCTION]
                                                       ├── 318 tables, 264 views, 355 functions
                                                       ├── 11 edge functions
                                                       ├── 5 pg_cron jobs
                                                       └── 9 auth users

Made Sci Org (udenwsiwwcsxngjptqxv) — 11 projects:
├── TIER 1 — Core (Git + Lovable UX)
│   ├── Transfer DB (jrfcfayphcmaxsixxupu) → minimal-science-hub [PRODUCTION]
│   ├── Reporting DB (xyopyttkhoxvnyeyijzb) → made-reporting-ux
│   └── Demand Planning (lyxvgbavbthyggeutzru) → made-demand-capacity-planner
├── TIER 2 — Active Data (no own UX)
│   ├── Sandbox BC (kwadsfzzbhjytsruwmtw) → Hub mirror (228K contacts)
│   ├── Sandbox Joe (hcyqnlyseunynswgtwax) → GlobalData + Joe's RAG (3,800 docs)
│   └── RAG Content (fdeyctgjudypbcqnmagw) → AI Second Brain (99K chunks)
└── TIER 3 — Standalone Tools
    ├── Contracts (bexrfaoyhwzhnhzftdhy) — 71 clients, 84 MSAs
    ├── Revenue Forecasting (iyibciagadgbjuphzjvr) — 8.2K forecasts
    ├── RFI Library (nxkqurlesocrpabdjjal) — 404 responses
    ├── Data Hygiene (kjdizfgqvammgrrhsgho) — 263 issues
    └── KFSHRC (kazinkoexzjqvfhrtflo) — reserved

BioCreative Org (post-migration):
├── Hub DB (mjsgtszehjltxmbxtctz) → ACTIVE (syncs news/social/companies)
├── ELG DB (kqzfrenfbfntwdnnbtlq) → ACTIVE (syncs team metrics)
├── CMDO DB (zmeooytxphryrxiuzusg) → ARCHIVED (data migrated)
└── Monday DB (gcrsxhrxxinryhdrweyj) → STAYS IN BC (rebuild Phase 7)
```

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

## Meeting Log (Mar 2026)

| Date | Meeting | Participants | Key Outcomes |
|------|---------|-------------|--------------|
| **Mar 13 PM** | MADE/BioCreative AI Training | Brian, Joe, Dustin, Lucy, Furat, Melody, Chat, Adam | RAG chatbot demo; campaign overview; GitHub consolidation; login issues flagged; Loom videos + training next week; Fort Lauderdale visits planned |
| **Mar 13 AM** | Joe / Bert 1:1 | Brian, Joe | API keys set live on call; RAG architecture discussion; $8.9B forecast; 2nd site expansion; Google Drive ingestion; PandaDoc API; master GitHub review |
| **Mar 11** | Brian <> Lucy Connect | Brian, Lucy | Campaign automation; Clay enrichment; HubSpot cleanup; persona filtering; unified inbox; target universe; Atomic AGI; 3,800 contacts request |
| **Mar 8** | JAM (Joe 1:1) | Brian, Joe | VPS purchased; n8n plan; 3D facility rendering; skills transfer; floor plan test |
| **Mar 7** | Async (email) | Brian → Joe | Edge function secrets; Windsurf workspace; Monday MCP; VPS+n8n plan |
| **Feb 13** | Full team meeting | Brian, Joe, Made team | Kickoff: move all data to Made org; Clay enrichment; RAG; Monday ICPP; CRM $66K/yr |
| **Jan 28** | Sync meeting | Brian, Joe | Infrastructure standardization; contact segmentation (47K, 10% verified); revenue forecasting |

---

## Blockers — Priority Order

| # | Item | Owner | Impact | Status |
|---|------|-------|--------|--------|
| 1 | **ANTHROPIC_API_KEY** in Transfer DB Edge Function Secrets | Joe | Blocks AI message gen in app | ⚠️ May be set — Joe adding on Mar 13 call. **Verify.** |
| 2 | **Transfer DB service role key** — share with Brian | Joe | Blocks HeyReach sync on VPS + Clay push | ❌ Blocked |
| 3 | **CLAY_API_KEY + CLAY_WEBHOOK_URL** in Transfer DB Vault | Joe | Blocks automated Clay enrichment | ⚠️ May be set — Joe adding on Mar 13 call. **Verify.** |
| 4 | **Hostinger VPS verification code** | Joe | Blocks Phase 6 (VPS + n8n + all automation) | ❌ Blocked |
| 5 | **Team login issues** — verify 9 users, distribute credentials | Brian | Blocks next training session | 🔧 Brian to fix |
| 6 | **Modality filters broken** — alignment with SFDC + GlobalData | Brian | Broken UX for team | 🔧 Brian to fix |
| 7 | **RAG embedding dimension** — 512 vs 1024 mismatch | Joe + Brian | Blocks RAG improvements | Discussion needed |
| 8 | **4 Clay HTTP API fields** to add | Clay admin | Missing enrichment data | Pending |
| 9 | **Salesforce push flow** — define MQL→SQL→pipeline gates | Joe + Lucy | Blocks CRM integration | Planning |

---

## Success Criteria

- [x] All Made Sci databases live in Made Sci Supabase org
- [x] `madescientificai.com` serves upgraded `minimal-science-hub` build
- [x] CMDO DB archived, crons stopped
- [x] MadeSciComandCenter = single master brain repo
- [x] Hub syncs working (news, social, ELG team metrics)
- [x] AI Second Brain deployed on RAG Content DB
- [x] Clay enrichment pipeline deployed (push + return)
- [x] Campaign tracker views rewired to live data
- [x] MSC campaigns created (417 contacts, 10 territories)
- [ ] AI message generation unblocked (ANTHROPIC_API_KEY)
- [ ] All team members can log in and use app
- [ ] Campaign training session completed
- [ ] 290 warm connections followed up
- [ ] NK + TIL campaigns launched
- [ ] Sandbox app available for dev/testing
- [ ] Made Sci VPS running with n8n and Claude Code
- [ ] RAG chatbot integrated into Made AI dashboard
- [ ] Monday.com rebuilt in new infrastructure
- [ ] Salesforce integration for engaged leads
- [ ] PandaDoc integration for proposals

---

*Consolidated from 16 prior tracking documents + 3 Fireflies transcripts (Mar 11–13). Source: `.windsurf/plans/made-sci-transcript-work-mapping-cd576d.md`*  
*This is a frozen mirror. Master copy lives in `MadeSciComandCenter/docs/MADE_BIOCREATIVE_PROJECT_TRACKING.md`.*
