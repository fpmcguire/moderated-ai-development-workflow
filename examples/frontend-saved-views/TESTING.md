# Testing — Saved Views

> Adapted from the Prismatic Testing Standards Guide for this project's stack and scope.

---

## Philosophy

**Pragmatic over perfect.** Tests should give you confidence to ship — not hit a coverage number.

- ✅ Test what matters: critical flows, complex logic, integration points
- ✅ Prefer integration tests over isolated unit tests
- ✅ Tests are documentation — names should explain how features work
- ✅ Skip tests that don't give you confidence or document behavior
- ❌ Don't chase coverage metrics
- ❌ Don't test simple getters, Angular framework behavior, or CSS

---

## Test Distribution

| Type                                                 | Effort  | Tool                                |
| ---------------------------------------------------- | ------- | ----------------------------------- |
| Integration (components + services working together) | **50%** | Vitest + `@testing-library/angular` |
| Unit (complex pure logic only)                       | **30%** | Vitest                              |
| E2E (3–5 critical user journeys only)                | **20%** | Playwright                          |

---

## What We Test

### ✅ Unit tests (Vitest) — complex logic only

Write unit tests for logic that has real branching and is genuinely hard to reason about.

**Worth testing:**

```typescript
// ✅ Duplicate name validation across the saved views collection
validateSavedViewName(name: string, existing: SavedView[]): ValidationResult

// ✅ Raw API → domain mapping with type narrowing (when backend integration arrives)
mapApiSavedView(raw: ApiSavedView): SavedView

// ✅ Persistence load with shape validation and fallback (when persistence is added)
SavedViewsPersistenceService.load(): SavedView[]
```

**Not worth testing:**

```typescript
// ❌ Simple getter or signal read
get activeViewName(): string { return this.activeSavedView()?.name ?? ''; }

// ❌ Angular DI wiring
// ❌ Signal reads/writes with no logic
```

### ✅ Integration tests (Vitest + Angular Testing Library) — primary test type

Test features working together as a user would experience them. Use `render()` from
`@testing-library/angular` and query by `data-testid`.

**Write integration tests for:**

- Store / facade flows (select → apply → active state update)
- Component rendering states (list with items, empty state, active item highlighted)
- User interactions (clicking a Saved View applies it to the dashboard)
- Validation feedback (duplicate name error displayed — when create is in scope)

**Example — store integration test:**

```typescript
it("applies the selected saved view configuration to the dashboard", () => {
  const { store } = setup(makeSavedViews(3));
  store.selectSavedView(store.savedViews()[1].id);
  expect(store.activeSavedViewId()).toBe(store.savedViews()[1].id);
  expect(store.currentDashboardConfiguration()).toEqual(store.savedViews()[1]);
});
```

**Example — component integration test:**

```typescript
it("renders the empty state when there are no saved views", async () => {
  await renderSavedViewsList({ savedViews: [] });
  expect(screen.getByTestId("saved-views-list-empty")).toBeInTheDocument();
});
```

### ✅ E2E tests (Playwright) — critical paths only

3–5 tests covering the journeys that must work before every release. No more.

**E2E tests for this app (grown across Steps):**

1. Dashboard loads; Saved Views list renders with view names
2. Selecting a Saved View updates the visible filters, sort, and columns on the dashboard
3. Empty state renders correctly when there are no Saved Views
4. _(Step 2+)_ Creating a Saved View — it appears in the list and becomes active
5. _(Step 2+)_ Renaming and deleting a Saved View

**Skip E2E for:**

- Edge cases and error states (cover in integration tests)
- Every button variation
- Internal state shape correctness (cover in store/unit tests)

> **Note on mocking:** Step 1 has no HTTP layer — Saved Views are in-memory. E2E tests
> seed state directly; do not reach for `page.route()` until a real backend is introduced.

---

## Selector Strategy

`data-testid` attributes are the **primary selector** for both Vitest and Playwright.

```
data-testid="{feature}-{component}-{element}-{modifier?}"
```

**This project's conventions:**

| Element                           | `data-testid`                         |
| --------------------------------- | ------------------------------------- |
| Saved Views list container        | `saved-views-list`                    |
| Individual list item              | `saved-views-list-item`               |
| Active/selected list item         | `saved-views-list-item--active`       |
| Empty state                       | `saved-views-list-empty`              |
| Dashboard filters display         | `dashboard-filters`                   |
| Dashboard sort display            | `dashboard-sort`                      |
| Dashboard columns display         | `dashboard-columns`                   |
| _(Step 2+)_ Save view button      | `saved-views-save-button`             |
| _(Step 2+)_ Save view name input  | `saved-views-name-input`              |
| _(Step 2+)_ Save view name error  | `saved-views-name-error`              |
| _(Step 2+)_ Rename action         | `saved-views-list-item-rename-button` |
| _(Step 2+)_ Delete action         | `saved-views-list-item-delete-button` |
| _(Step 2+)_ Confirm delete button | `saved-views-delete-confirm-button`   |

**Rules:**

- Always kebab-case
- Specific enough to be unambiguous (`saved-views-list-empty`, not `empty`)
- Applied at build time in templates — never added as a test afterthought
- Never use CSS classes, DOM structure, or text content as primary selectors
- Add new rows to this table in the same Step where the element is introduced

---

## Test File Placement

Tests live next to the file they test:

```
saved-views-list.component.ts
saved-views-list.component.spec.ts    ← component integration test

saved-views.store.ts
saved-views.store.spec.ts             ← integration test (primary coverage)

saved-view.mapper.ts
saved-view.mapper.spec.ts             ← unit test (complex pure logic)

dashboard.component.ts
dashboard.component.spec.ts           ← integration test (apply behaviour)
```

E2E tests live in `e2e/`:

```
e2e/
  helpers.ts                          ← test data factories (makeSavedView, makeSavedViews)
  saved-views.spec.ts                 ← critical user journey tests
    ├── Dashboard loads with saved views list
    ├── Selecting a saved view applies it to the dashboard
    ├── Empty state
    ├── (Step 2+) Create saved view
    └── (Step 2+) Rename and delete saved view
```

---

## Naming Conventions

Test names read as sentences describing behavior, not implementation:

```typescript
// ✅ Describes behavior
it("shows the saved view name in the list");
it("marks the selected saved view as active");
it(
  "updates the visible filters, sort, and columns when a saved view is applied",
);
it("shows the empty state when there are no saved views");
it("prevents saving a view with a duplicate name"); // Step 2+

// ❌ Describes implementation
it("calls selectSavedView with the correct id");
it("sets activeSavedViewId signal");
it("updates the store state");
```

---

## What We Don't Test

| Skip                                  | Why                                   |
| ------------------------------------- | ------------------------------------- |
| Simple Angular `@Input` binding       | Framework behavior — trust Angular    |
| CSS class application                 | Use visual review                     |
| Every validation edge case            | Pick the critical ones; skip the rest |
| Third-party library behavior          | CDK, RxJS operators                   |
| `data-testid` presence on elements    | Already verified manually; brittle    |
| Trivial computed signals (reads only) | No logic to break                     |

---

## Running Tests

```bash
npm test              # All unit + integration tests (Vitest — interactive/watch in terminal)
npm run test:ci       # Same tests, exits cleanly — use this in CI pipelines (--watch=false)
npm run test:watch    # Explicit watch mode during development
npm run e2e           # Playwright E2E (requires dev server on :4200)
npm run e2e:ui        # Playwright interactive UI
```

---

## Current Test State

_Updated at the close of each Step._

| File         | Tests | Type |
| ------------ | ----- | ---- |
| _(none yet)_ | —     | —    |

---

## Decision Tree

```
Should I write a test for this?
│
├─ Is it a critical user flow? → E2E test (Playwright)
│
├─ Is it complex business logic or a store/facade/service? → Integration test (Vitest)
│
├─ Is it a pure utility with real branching? → Unit test (Vitest)
│
├─ Is it a simple getter, Angular wiring, or CSS? → Skip
│
└─ Am I unsure what I'm testing? → Skip
```

---

> **Remember:** The goal is working software with confidence to ship — not coverage metrics.
> 10 focused integration tests beat 50 trivial unit tests every time.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · github.com/fpmcguire/moderated-ai-development-workflow
