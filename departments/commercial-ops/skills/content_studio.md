---
title: Content Studio
department: commercial-ops
version: 1.0
triggers: [content, post, LinkedIn, generation, writing]
---

# Content Studio

AI-powered content generation for LinkedIn posts and marketing content.

## Database Tables (Transfer DB)

| Table | Purpose |
|-------|---------|
| `team_profiles` | Team member profiles for content personalization |
| `linkedin_hook_library` | Hook templates for post openings |
| `linkedin_content_pillars` | Content pillar categories |
| `content_generation_history` | History of AI-generated content |

## Edge Functions
- `generate-post-multi-source` — AI text generation using multiple intelligence sources
- `generate-image-from-post` — AI image generation for posts

## App Pages
- `/post-generator` — Post Generator with template selection, AI generation, preview
- `/team-profile` — Team Profile management

## Content Generation Flow
1. Select team member (author voice)
2. Choose content pillar and hook type
3. Select intelligence sources (news, events, social)
4. AI generates draft with brand voice
5. Preview, edit, and export
