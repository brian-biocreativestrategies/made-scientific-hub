---
description: PIV Loop planning phase — create a structured implementation plan with task list and validation strategy before writing any code
---

## /plan-feature — Structured Feature Planning (PIV Loop Phase 1)

This is the **Plan** phase of the PIV (Plan → Implement → Validate) loop. The output is a standalone plan document that contains everything needed for implementation in a **fresh conversation**.

### Pre-Research Phase

Before creating the plan, do thorough research:

1. **Internal codebase research:**
   - Read the relevant `departments/*/skills/` files for the feature domain
   - Read the relevant department CLAUDE.md for database tables, views, functions
   - Check existing code in the affected app repo(s)

2. **Web research** (when the feature involves external APIs, new patterns, or unfamiliar tech):
   - Search for best practices specific to the technology involved
   - Look for common pitfalls and edge cases
   - **Always cite sources** in the plan's References section

3. **Assumption reduction** — Ask the user **at least 5 clarifying questions** covering:
   - Exact scope (what's in vs. out for this feature)
   - Integration points (which existing systems are affected)
   - Data model changes (new tables, columns, migrations)
   - UX expectations (if frontend work is involved)
   - Success criteria (how will we know it's done)

   **Wait for answers before creating the plan.**

### Create the Structured Plan

Save the plan to `.windsurf/plans/{feature-slug}-{random-6-chars}.md` with this structure:

```markdown
# Feature Plan: [Feature Name]

**Created:** [date]
**Status:** Draft | Approved | In Progress | Complete
**Estimated effort:** [hours]
**PIV Phase:** Plan ✅ → Implement ⬜ → Validate ⬜

## 1. Problem Statement
[What problem does this solve? Why now?]

## 2. Success Criteria
- [ ] [Specific, testable criterion 1]
- [ ] [Specific, testable criterion 2]

## 3. Research Findings
### Internal Context
- [Relevant skills, schemas, past implementations found]

### External Best Practices
- [Web research findings with sources]

### Assumptions Resolved
| Question | Answer |
|----------|--------|
| [Question asked] | [User's answer] |

## 4. Architecture & Approach
[How will this be built? Key design decisions.]

### Files to Create
- `path/to/new/file.ts` — [purpose]

### Files to Modify
- `path/to/existing/file.ts` — [what changes]

### Database Changes
- [Migration name] — [what it does]

## 5. Task List
- [ ] Task 1: [description] (~Xmin)
- [ ] Task 2: [description] (~Xmin)
[Keep tasks granular — each should be completable in <30 min]

## 6. Validation Strategy

### Automated Validation
- **Type checks:** `npx tsc --noEmit`
- **Lint:** `npx eslint src/`

### Manual Validation (for the human)
- [ ] Step 1: [exact action to take]
- [ ] Step 2: [what to verify]

## 7. References
- [Internal docs, skills, schemas referenced]
- [External URLs consulted]

## 8. Rollback Plan
[How to undo if something goes wrong]
```

### Validation Gate

Present the plan to the user. **Do NOT proceed to implementation until the user approves the plan.**

Once approved:
1. Update the plan status to "Approved"
2. Tell the user: **"Plan approved. Start a new conversation and run `/execute .windsurf/plans/{filename}`"**

### Key Principles

- **The plan must be self-contained** — a fresh conversation with only this plan should have everything needed
- **Validation strategy is defined BEFORE implementation**
- **Tasks are granular** — no task should take more than 30 minutes
- **Research is done upfront** — don't discover best practices mid-implementation
