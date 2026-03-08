---
title: Content Studio
department: marketing
version: 1.0
triggers: [content, post, LinkedIn, generation, writing, creative]
---

# Content Studio

AI-powered content generation for LinkedIn posts and marketing materials.

## Database Tables (Transfer DB)

| Table | Purpose |
|-------|---------|
| `team_profiles` | Writer profiles with voice/tone |
| `linkedin_hook_library` | Hook templates by type |
| `linkedin_content_pillars` | Content themes |
| `intel_entries` | Intelligence snippets for content |
| `content_generation_history` | Generated content log |

## Edge Function

- `generate-content-multi-source` — AI content generation (Lovable Gateway or OpenAI fallback)

## App Pages

- `/content-studio` — Content generation interface

## MADE AI Module

- Marketing Content Hub & Creative Tools
