---
trigger: department_match
description: Rules for Business Development (ComBD + Inside Sales) department
globs: ["departments/business-development/**"]
---

# Business Development Rules

**Scope:** Pipeline execution, territory management (East/West), inside sales, travel & site visits.
**Monday Team:** ComBD (ID: 1307953)
**Territories:** East (Chat, Simona) | West (Adam, Karen)

## Rules

1. **Territory data** must always specify East or West — never mix territory assignments.
2. **Pipeline stages** follow Transfer DB conventions: `not_yet_reached → queued → targeted → opportunity → nurture_* → disqualified`.
3. **Account imports** always go through staging pipeline — never direct INSERT to `companies`.
4. **Inside Sales** shares OKR structure but is not a separate team in Monday — keep inside sales items under BD department.
5. **Travel & Site Visits** board (114 items) is the source of truth for BD travel — reference before creating new entries.
6. **ICPP tracker** has cross-references with BioCreative — check both boards.
