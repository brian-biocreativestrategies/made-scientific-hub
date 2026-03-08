# Supabase Rules

> **Triggers:** Edge Functions, RLS, migrations, Supabase
> **Globs:** `["supabase/**/*", "**/edge-function*", "supabase/functions/**/*"]`

## Edge Functions (Transfer DB)

```
supabase/functions/
├── bulk-export-briefing-sheets/
├── diagnose-event-contacts/
├── download-document/
├── generate-image-from-post/
├── generate-post-multi-source/
├── heyreach-webhook/
├── sync-made-sci-data/
├── transcribe-audio/
└── transcribe-interview/
```

## Edge Function Pattern

```typescript
import "jsr:@supabase/functions-js/edge-runtime.d.ts";

Deno.serve(async (req: Request) => {
  // Always handle CORS
  if (req.method === 'OPTIONS') {
    return new Response(null, { headers: corsHeaders });
  }
  
  // Your logic here
  return new Response(JSON.stringify(data), {
    headers: { 'Content-Type': 'application/json', ...corsHeaders }
  });
});
```

## Security Rules

1. **RLS on ALL tables** - No exceptions
2. **Never expose service role key** in frontend
3. **Validate inputs** in Edge Functions
4. **Use anon key** for client-side operations

## Made Sci Supabase Projects

| Database | Project ID | Tier |
|----------|------------|------|
| **Transfer DB** ★ | `jrfcfayphcmaxsixxupu` | Tier 1 — Production |
| **Reporting DB** | `xyopyttkhoxvnyeyijzb` | Tier 1 |
| **Demand Planning** | `lyxvgbavbthyggeutzru` | Tier 1 |
| **Sandbox BC** | `kwadsfzzbhjytsruwmtw` | Tier 2 |
| **Sandbox Joe** | `hcyqnlyseunynswgtwax` | Tier 2 |
| **RAG Content** | `fdeyctgjudypbcqnmagw` | Tier 2 |
| **Contracts** | `bexrfaoyhwzhnhzftdhy` | Tier 3 |
| **Revenue Forecasting** | `iyibciagadgbjuphzjvr` | Tier 3 |
| **RFI Library** | `nxkqurlesocrpabdjjal` | Tier 3 |
| **Data Hygiene** | `kjdizfgqvammgrrhsgho` | Tier 3 |
| **KFSHRC** | `kazinkoexzjqvfhrtflo` | Tier 3 — empty |
