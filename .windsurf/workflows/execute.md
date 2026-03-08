---
description: PIV Loop implementation phase — execute an approved plan in a fresh context, then run validation
---

## /execute — Plan Execution (PIV Loop Phase 2 + 3)

This is the **Implement + Validate** phase of the PIV loop. Run this in a **fresh conversation** after `/plan-feature` has produced an approved plan.

**Usage:** `/execute .windsurf/plans/{plan-filename}.md`

### Pre-Implementation Setup

1. **Read the plan file** passed as the argument — this is your primary context
2. **Read the global rules** (`.windsurf/rules/` — auto-loaded, but verify key constraints)
3. **Read any referenced files** listed in the plan's "References" section
4. **Verify environment:**

// turbo
```bash
git status --short
```

### Implementation Phase

Execute the task list from the plan **in order**. For each task:

1. **Announce** what you're about to do (one line)
2. **Implement** the task — write the code, create files, run migrations
3. **Mark the task done** in your working memory
4. **If blocked:** Stop and ask the user. Do NOT skip tasks or make assumptions.

**Rules during implementation:**
- Follow all patterns from `.windsurf/rules/` (database.md, frontend.md, etc.)
- Load on-demand context from `departments/*/skills/` only when relevant
- Do NOT deviate from the plan without user approval
- If you discover the plan is wrong or incomplete, STOP and tell the user

### Validation Phase

After all tasks are complete, run the validation strategy from the plan:

1. **Automated validation:**

// turbo
```bash
npx tsc --noEmit 2>&1 | head -20
```

2. **Self-review checklist:**
   - [ ] All tasks from the plan are complete
   - [ ] No TypeScript/Python errors
   - [ ] No hardcoded secrets or test data left in code
   - [ ] New files have proper imports
   - [ ] Database changes have RLS policies (if applicable)
   - [ ] Modified files follow existing code style

### Completion Report

Output a structured completion report:

```markdown
## Execution Complete — [Feature Name]

### Tasks Completed
- [x] Task 1: [description]
- [x] Task 2: [description]

### Files Changed
- **Created:** [list]
- **Modified:** [list]

### Validation Results
- Type check: pass/fail
- Lint: pass/fail

### Deviations from Plan
- [Any changes made vs. the original plan, with reasons]

### Ready for Human Validation
Please verify these manually:
1. [Step from the plan's manual validation section]

### Next Step
Run `/commit` to create a structured commit message.
```

### Key Principles

- **Fresh context** — This conversation should start clean with only the plan as context
- **Plan is the source of truth** — Don't freelance. Follow the plan.
- **Validate before declaring done** — Run every check in the validation strategy
- **Report deviations** — If you had to change anything, document why
