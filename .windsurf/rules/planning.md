# Planning & Questioning Rules

> **Triggers:** build, create, implement, new feature, new module, major refactor
> **Globs:** `["**/*"]`

## Mandate Questioning

Before implementing any task estimated at >1 hour:

1. **Ask at least 3 clarifying questions** covering:
   - Scope boundaries (what's included vs. excluded)
   - Integration points (which existing systems are affected)
   - Success criteria (how will we know it's done)

2. **Wait for answers** before writing any code

3. **Summarize understanding** back to the user in a brief plan

## When to Skip Questioning

- Bug fixes with clear reproduction steps
- Tasks the user has already fully specified (PRD provided)
- Follow-up work on an approved plan
- Explicit "just do it" from the user

## Planning Checklist (for >1hr tasks)

Before implementation, confirm:
- [ ] Scope is clear (what's in, what's out)
- [ ] Affected files/systems identified
- [ ] Database changes needed? (migrations, RLS)
- [ ] Success criteria defined

## Context Reset Discipline (PIV Loop)

**After creating a plan, tell the user to start a new conversation for implementation.**

The Plan → Implement → Validate (PIV) loop requires context isolation:

1. **Planning conversation** — Research, ask questions, create structured plan in `.windsurf/plans/`
2. **Context reset** — User starts a fresh conversation
3. **Implementation conversation** — Run `/execute {plan-file}`, the plan is the only context needed

**Why:** Planning conversations accumulate tens of thousands of tokens of exploration. Implementation needs only the distilled plan.

**Workflow sequence:**
```
/prime → understand codebase
/plan-feature → create structured plan (research + questions + plan doc)
--- NEW CONVERSATION ---
/execute {plan-file} → implement + validate
/commit → structured commit message
```
