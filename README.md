# Made Scientific Hub

The organizational brain for Made Scientific's AI-powered commercial intelligence platform. This repo contains department structure, skills, Windsurf rules, workflows, and documentation — **no application code**.

Application code lives in the app repos (see Workspace Setup below).

---

## Quick Start

### 1. Clone All Repos

```bash
# Master brain (this repo)
git clone https://github.com/MADE-SCI/made-scientific-hub.git

# Production dashboard
git clone https://github.com/MADE-SCI/minimal-science-hub.git

# Demand planning app
git clone https://github.com/MADE-SCI/made-demand-capacity-planner.git

# Reporting dashboard
git clone https://github.com/MADE-SCI/made-reporting-ux.git
```

### 2. Open Windsurf Workspace

Open all 4 repos as a multi-root workspace in Windsurf:
1. Open Windsurf
2. File → Open Folder → select `made-scientific-hub`
3. File → Add Folder to Workspace → add the other 3 repos
4. Save Workspace as `made-scientific.code-workspace`

### 3. Start a Session

Type `/prime` in the chat to prime the agent with your current codebase state. The agent will:
- Read `CLAUDE.md` for routing rules
- Check git history for recent changes
- Identify active work and plans
- Output a status report for you to validate

---

## Repo Structure

```
made-scientific-hub/
├── CLAUDE.md                              # Root brain — read this first
├── .windsurf/
│   ├── rules/                             # 14 Windsurf rules (6 global + 8 dept)
│   │   ├── database.md                    # DB operations rules
│   │   ├── frontend.md                    # React/TypeScript patterns
│   │   ├── supabase.md                    # Edge functions, RLS, project IDs
│   │   ├── debugging.md                   # Bug fix + system evolution
│   │   ├── planning.md                    # PIV loop, mandate questioning
│   │   ├── colab.md                       # Notebook safety rules
│   │   ├── dept-commercial-leadership.md  # ComLT scope
│   │   ├── dept-business-development.md   # ComBD + Inside Sales scope
│   │   ├── dept-commercial-operations.md  # ComOps scope
│   │   ├── dept-marketing.md              # Marketing scope
│   │   ├── dept-commercial-development.md # ComDev scope
│   │   ├── dept-partnerships.md           # Partnerships scope
│   │   ├── dept-operations.md             # PAD/TechOps/QA scope
│   │   └── dept-infrastructure.md         # MADE AI / data scope
│   └── workflows/                         # 6 slash commands
│       ├── prime.md                       # /prime — session priming
│       ├── plan-feature.md                # /plan-feature — structured planning
│       ├── execute.md                     # /execute — plan execution
│       ├── commit.md                      # /commit — structured commits
│       ├── import-data.md                 # /import-data — staging pipeline
│       └── switch-db.md                   # /switch-db — database context switch
├── departments/                           # 8 departments (mirrors Monday.com)
│   ├── commercial-leadership/             # ComLT — strategic OKRs, portfolio, KPIs
│   │   ├── CLAUDE.md
│   │   ├── context/
│   │   └── skills/ (4 skills)
│   ├── business-development/              # ComBD — pipeline, territories, inside sales
│   │   ├── CLAUDE.md
│   │   ├── context/
│   │   └── skills/ (5 skills)
│   ├── commercial-operations/             # ComOps — proposals, CRM, S&OP, pricing
│   │   ├── CLAUDE.md
│   │   ├── context/
│   │   └── skills/ (5 skills)
│   ├── marketing/                         # Marketing — campaigns, content, events
│   │   ├── CLAUDE.md
│   │   ├── context/
│   │   └── skills/ (6 skills)
│   ├── commercial-development/            # ComDev — revenue, capacity
│   │   ├── CLAUDE.md
│   │   ├── context/
│   │   └── skills/ (2 skills)
│   ├── partnerships/                      # Client experience, strategic partners
│   │   ├── CLAUDE.md
│   │   ├── context/
│   │   └── skills/ (3 skills)
│   ├── operations/                        # PAD + TechOps + QA
│   │   ├── CLAUDE.md
│   │   ├── context/
│   │   └── skills/ (1 skill)
│   └── infrastructure/                    # MADE AI, data, Monday, KB
│       ├── CLAUDE.md
│       ├── context/
│       └── skills/ (7 skills)
├── scripts/                               # Utility scripts
├── docs/                                  # Architecture docs
│   └── INFRASTRUCTURE_CONSOLIDATION.md    # Migration status tracker
└── .gitignore
```

---

## Slash Commands

| Command | Purpose |
|---------|---------|
| `/prime` | Start of session — builds status report from git history + CLAUDE.md |
| `/plan-feature` | Plan a feature with research, questions, task list, validation strategy |
| `/execute {plan}` | Execute an approved plan in a fresh conversation |
| `/commit` | Generate structured commit message as long-term memory |
| `/import-data` | Import accounts/contacts through staging pipeline |
| `/switch-db` | Switch database context for MCP queries |

### Recommended Workflow

```
/prime → understand current state
/plan-feature → create structured plan
--- NEW CONVERSATION ---
/execute .windsurf/plans/{filename} → implement + validate
/commit → structured commit
```

---

## Key Databases

| Database | Project ID | Purpose |
|----------|------------|---------|
| **Transfer DB** ★ | `jrfcfayphcmaxsixxupu` | Production — 299 tables |
| **Reporting DB** | `xyopyttkhoxvnyeyijzb` | SFDC/HubSpot |
| **Demand Planning** | `lyxvgbavbthyggeutzru` | Capacity/scheduling |
| **RAG Content** | `fdeyctgjudypbcqnmagw` | Knowledge base |
| **Sandbox Joe** | `hcyqnlyseunynswgtwax` | GlobalData |

Full database registry: see `CLAUDE.md` → Databases section.

---

## Important Rules

1. **Never run `npm install`** in any Lovable repo — apps build remotely
2. **Hub-and-Spoke architecture** — data flows from BioCreative Hub → Transfer DB, never reverse
3. **Staging tables for imports** — never insert directly into production
4. **RLS on all tables** — no exceptions
5. **DRY_RUN first** — test before production writes

---

## Skills (33 total)

| Department | Count | Skills |
|------------|-------|--------|
| **Commercial Leadership** | 4 | OKR Management, Portfolio Dashboard, KPI Review, Strategic Planning |
| **Business Development** | 5 | Pipeline Execution, Territory Management, Account Import, Meeting Intelligence, Inside Sales |
| **Commercial Operations** | 5 | Proposal Excellence, CRM Integration, Demand Planning, Account Classification, Pricing Framework |
| **Marketing** | 6 | Campaign Tracker, Content Studio, Social Listening, News Intelligence, Event Data Collection, Brand Authority |
| **Commercial Development** | 2 | Revenue Forecasting, Capacity Management |
| **Partnerships** | 3 | Client Experience, New Service Development, Strategic Partnerships |
| **Operations** | 1 | Manufacturing Ops (placeholder) |
| **Infrastructure** | 7 | Database Metrics, Knowledge Base, Monday Integration, Data Hygiene, Academic Market, Clinical Trials, Drug Pipeline |

---

## Contact

**Brian Elbert** — BioCreative Strategies (technology partner)  
**Joe Sinclair** — Made Scientific (operations)
