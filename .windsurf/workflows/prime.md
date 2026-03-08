---
description: Session priming — catch the agent up on codebase state, active work, and recent history before any implementation
---

## /prime — Session Priming

Run this at the **start of every new conversation** before doing any implementation work. The goal is to build a verified mental model of the codebase so the agent doesn't make assumptions.

### Pre-Research Phase

Before building the status report, do targeted research to ensure best practices:

1. **Internal research** — Read these files to understand current state:
   - `CLAUDE.md` (auto-loaded — routing table to 4 department CLAUDE.md files)
   - Load the relevant department CLAUDE.md based on the work ahead

2. **Check for active plans** — Look for any in-progress work:
   - Scan `C:\Users\elber\.windsurf\plans\` for recent `.md` plan files
   - Check the infrastructure consolidation plan: `docs/INFRASTRUCTURE_CONSOLIDATION.md`

3. **Git history as long-term memory:**

// turbo
```bash
git log --oneline --no-decorate -20
```

4. **Check for uncommitted work:**

// turbo
```bash
git status --short
```

### Build the Status Report

After gathering context, output a structured report for the user to validate:

```markdown
## Session Prime — [Date]

### Codebase State
- **Repo:** [repo name]
- **Branch:** [current branch]
- **Uncommitted changes:** [yes/no, list if yes]
- **Last 5 commits:** [one-line summaries]

### Active Work
- **Current plan/prompt:** [filename or "none detected"]
- **Phase/task in progress:** [description]
- **Blocked on:** [anything waiting for user input or external dependency]

### Key Numbers (quick health check)
- Transfer DB tables: 299 | Supabase projects: 11
- App repos: 3 (minimal-science-hub, made-reporting-ux, made-demand-capacity-planner)

### Recommended Next Action
- [What should we work on based on active plans, git history, and current state]
```

### Validation Gate

**Do NOT proceed to any implementation until the user confirms the status report is accurate.** If the user corrects something, update your understanding and re-present the corrected section.

### When to Use /prime

- Start of every new conversation where you'll be writing code
- After returning from a long break (>4 hours)
- When switching between repos or contexts
- After a major merge or deployment

### When to Skip /prime

- Quick questions ("what's the Transfer DB project ID?")
- Pure documentation tasks
- User says "skip prime" or provides explicit context
