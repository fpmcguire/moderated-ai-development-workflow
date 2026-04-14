# Architecture – Saved Views (Frontend Example)

## Project Type

Single-page application (SPA) focused on the dashboard and Saved Views feature.

## Stack (Example Profile)

- Language: TypeScript
- UI Library: React
- Build tool: Vite or Create React App (any simple setup is fine)
- Testing: Jest + React Testing Library (or equivalent)

Moderated AI Development Workflow itself is framework‑agnostic; this profile is just one concrete mapping.

## Structure

- `src/components/` – presentational + container components
- `src/state/` – simple state modules (e.g., React context or hooks)
- `src/pages/` – page‑level components (e.g., Dashboard)
- `src/tests/` – test files mirroring component structure

For the Saved Views example:

- `src/components/SavedViewsList.tsx`
- `src/components/Dashboard.tsx`
- `src/state/savedViews.ts`
- `src/tests/SavedViewsList.test.tsx`

## Data Model (Saved View)

For this example, Saved Views are stored in memory:

```ts
type SavedViewId = string;

interface SavedView {
  id: SavedViewId;
  name: string;
  filters: Record<string, unknown>;
  sort: { field: string; direction: "asc" | "desc" } | null;
  columns: string[];
}
```

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
