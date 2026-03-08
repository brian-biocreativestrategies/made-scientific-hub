# Debugging & System Evolution Rules

> **Triggers:** bug, fix, error, debug, broken, regression, hotfix
> **Globs:** `["**/*.tsx", "**/*.ts", "**/*.py", "**/*.sql", "**/*.md"]`

## Core Principle

**Don't just fix the bug. Fix the system that allowed the bug.**

## Iteration Limits

When debugging or building iteratively:
- **3-strike rule:** After 3 failed attempts at the same fix, STOP and escalate to the user
- **Explain what was tried** — list the 3 approaches and why each failed
- **Suggest alternatives** — propose a different strategy or ask for more context
- **Never silently retry** — each attempt must produce visible output or a status update

This applies to:
- Bug fixes (same error recurring)
- Build steps (migration, deployment, sync)
- Test failures (same test failing after fix)

---

After resolving any bug or error, run this mental checklist:

## Post-Fix System Audit

1. **Skill check** — Does a `departments/*/skills/` file contain wrong info or an outdated pattern?
   - If yes → Update the skill with the correction
2. **Rule check** — Should a `.windsurf/rules/` file include a new constraint to prevent recurrence?
   - If yes → Add the pattern to the relevant rule
3. **Context check** — Is a `departments/*/context/` doc stale?
   - If yes → Update the context doc
4. **CLAUDE check** — Does a department CLAUDE.md need updating?
   - If yes → Update with the correction

## When to Skip the Audit

- Typos and trivial syntax errors
- One-off data fixes (wrong row value)
- User-specific preference changes

## Common Bug → System-Update Patterns

| Bug Pattern | System Update |
|-------------|---------------|
| Wrong table/column name used | Update the relevant schema doc |
| Forgot RLS policy | Add to deployment checklist |
| Import failed on edge case | Add to import skill troubleshooting |
| Lovable build broke | Document the fix pattern |
| API changed behavior | Update the relevant skill's API reference |
| Sync function missed rows | Update sync function docs |
