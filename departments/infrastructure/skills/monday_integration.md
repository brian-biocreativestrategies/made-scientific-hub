---
title: Monday.com Integration
department: infrastructure
version: 1.0
triggers: [Monday, OKR, board, items, project tracking, workspace]
---

# Monday.com Integration

Monday.com data sync and integration layer.

## Monday Database

- **Monday DB** (`gcrsxhrxxinryhdrweyj`) — 15 tables

## Database Tables

| Table | Rows | Purpose |
|-------|------|---------|
| `boards` | ~110 | All Monday boards (active + subitems) |
| `items` | ~1000+ | Board items with status |
| `board_groups` | — | Groups within boards |
| `column_values` | — | Item field values |
| `column_definitions` | — | Board column schemas |
| `users` | 18 | Team members + team accounts |
| `teams` | 9 | Organizational teams |
| `team_members` | 39 | Team-to-user mapping |
| `folders` | 18 | Board folder structure |
| `workspaces` | 1 | MADE - 2026 |
| `sync_log` | — | Sync history |

## Monday API

- API Key: stored in Monday DB environment
- Endpoint: `https://api.monday.com/v2` (GraphQL)
- MCP Server: `scripts/monday-mcp-server/` (in made-sci-cmdo-dash)

## Sync Architecture

Monday.com API → Monday DB (Supabase) → Available for queries

## Key Board IDs

See department CLAUDE.md files for board IDs mapped to each department.
