---
description: Create structured git commit messages that serve as long-term memory for future session priming
---

## /commit — Structured Commit Message

Generate a standardized commit message that serves as **long-term memory** for the codebase. The `/prime` workflow reads `git log` to understand recent history, so commit messages must be informative and consistent.

### Pre-Research Phase

Before writing the commit message, gather context:

1. **Check what changed:**

// turbo
```bash
git diff --stat
```

2. **Check staged vs unstaged:**

// turbo
```bash
git status --short
```

3. **Read the active plan** (if one exists in `.windsurf/plans/`) to understand the feature context.

### Commit Message Format

Use **Conventional Commits** with Made Sci extensions:

```
<type>(<scope>): <summary>

<body>

<footer>
```

**Types:**
| Type | When to Use |
|------|-------------|
| `feat` | New feature or capability |
| `fix` | Bug fix |
| `data` | Database migration, data import, enrichment |
| `docs` | Documentation, skills, context files only |
| `refactor` | Code restructuring without behavior change |
| `style` | Formatting, UI tweaks, no logic change |
| `test` | Adding or updating tests |
| `ops` | DevOps, deployment, n8n workflows, VPS |

**Scopes:**
| Scope | Covers |
|-------|--------|
| `hub` | Made Scientific Hub (this master repo) |
| `app` | minimal-science-hub (production dashboard) |
| `reporting` | made-reporting-ux |
| `planner` | made-demand-capacity-planner |
| `skills` | Skills library |
| `context` | Context module system |
| `db` | Database schemas, migrations, RPCs |
| `ux` | Frontend components, pages, hooks |
| `scripts` | Python scripts, notebooks |

**Body** (required for non-trivial commits):
- What was built/changed and why
- Key files created or modified (top 5)
- Database changes (migrations, new tables/columns)
- Any gotchas or decisions made

**Footer** (optional but valuable):
- `Plan: .windsurf/plans/{filename}` — link to the plan that drove this work
- `Next: [what comes next]` — guide future `/prime` sessions
- `Breaking: [description]` — if this changes existing behavior

### Example Commit Messages

**Simple:**
```
feat(app): add Drug Pipeline tab to account detail

Shows drug pipeline data from Transfer DB for therapeutic_developer accounts.
New component: src/components/accounts/tabs/DrugPipelineTab.tsx

Next: Add Clinical Trials tab
```

**Complex:**
```
data(db): apply account classification migration + update classifier v2.0

Added columns: ai_classification_notes, classified_at, classification_version
+ 2 indexes on Transfer DB.

Key files:
- migration: add_classification_columns
- departments/data-intelligence/skills/account_classification.md (updated)

Plan: .windsurf/plans/classification-v2-a1b2c3.md
Next: Run classifier on unclassified accounts (~400 remaining)
```

### Execution

After generating the message, stage and commit:

```bash
git add -A
git commit -m "<generated message>"
```

**Ask the user before running** — show them the commit message first for approval.

### Key Principles

- **Commit messages are memory** — future `/prime` sessions will read these
- **`Next:` footer is critical** — it tells the next session what to work on
- **Be specific about files** — helps the agent understand what was touched
- **One commit per PIV loop** — don't bundle unrelated work
- **Never commit secrets** — check `git diff` for API keys, passwords, tokens
