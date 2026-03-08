# Frontend Development Rules

> **Triggers:** React, TypeScript, components, UI, pages
> **Globs:** `["src/**/*.tsx", "src/**/*.ts", "src/components/**/*", "src/pages/**/*"]`

## Tech Stack

- **Framework:** React 18 + TypeScript + Vite
- **UI:** Tailwind CSS + shadcn/ui
- **State:** TanStack Query (React Query)
- **Icons:** Lucide React

## Code Patterns

### Hooks Pattern
```typescript
// Always use custom hooks for data fetching
export function useAccounts(filters: AccountFilters) {
  return useQuery({
    queryKey: ['accounts', filters],
    queryFn: () => fetchAccounts(filters),
  });
}
```

### Component Structure
```
src/
├── components/
│   ├── ui/           # shadcn/ui primitives
│   ├── accounts/     # Feature-specific components
│   └── shared/       # Reusable components
├── hooks/            # Custom React hooks
├── pages/            # Route pages
└── lib/              # Utilities and queries
```

## Styling Rules

- Use Tailwind utility classes, not custom CSS
- Follow shadcn/ui patterns for consistency
- Mobile-first responsive design

## App Repos

| Repo | Purpose | DB |
|------|---------|-----|
| `minimal-science-hub` | Production dashboard | Transfer DB (`jrfcfayphcmaxsixxupu`) |
| `made-reporting-ux` | Reporting dashboards | Reporting + Transfer + Sandbox Joe + RAG |
| `made-demand-capacity-planner` | Demand planning | Demand Planning + Reporting |
