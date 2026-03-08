---
title: Monday.com Integration
department: operations
version: 1.0
triggers: [Monday, OKR, board, items, project tracking]
---

# Monday.com Integration

Monday.com API integration for OKR tracking and project management.

## Current State (Phase 7 — Planned)

The old Monday DB (`gcrsxhrxxinryhdrweyj`) lives in BioCreative org and was synced via a Colab notebook. The OKR Command Center app (`okr-command-center` repo) connects to this DB.

**Decision:** NOT transferring — rebuilding from scratch in Phase 7.

## Monday.com API

- **API Version:** GraphQL v2024-10
- **Workspace ID:** 13639214 (MADE - 2026)
- **Base URL:** `https://api.monday.com/v2`

## Old Monday DB Contents (for reference)
| Table | Records |
|-------|---------|
| `boards` | 134 |
| `board_items` | 2,110 |
| `users` | 18 |
| `board_folders` | 16 |
| `board_column_definitions` | 2,381 |
| `board_groups` | 316 |
| `madeai_features` | 27 |
| `okr_board_registry` | 19 |

## Phase 7 Plan
1. Design new Monday → Transfer DB sync via n8n (on Made Sci VPS)
2. Build OKR features into `minimal-science-hub` (not separate app)
3. Clean up Monday boards (delete test boards, merge duplicates)
