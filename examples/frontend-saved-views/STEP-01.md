# Step 1 – Saved Views List (Read-only)

## Goal

Render a Saved Views list for the current user and allow selecting a view to apply its configuration to the dashboard (using mocked state).

## Scope

In scope:

- Frontend-only implementation.
- Read-only list of Saved Views.
- Applying a Saved View to update dashboard state.
- Visible active/selected-state for the currently applied Saved View.
- Visible applied-state feedback for `filters`, `sort`, and `columns`.
- Empty state for “no saved views”.

Out of scope (for this Step):

- Creating, renaming, or deleting Saved Views.
- Persistence beyond in-memory state.
- Backend integration or auth.

## Inputs

- `PRODUCT.md` for feature context and workflows.
- `ARCHITECTURE.md` (frontend section) for stack and structure.
- `DOMAIN_LANGUAGE.md` entries for “Dashboard”, “Saved View”, “Filters”, “Sort”, “Columns”, and “Active Saved View”.
- This Step brief.

## Required Changes

- Add a `SavedViewsList` UI component (or equivalent) to the dashboard.
- Display a list of Saved Views with at least a name for each.
- Use the canonical Saved View shape: `{ id, name, filters, sort, columns }`.
- Track the active selected Saved View separately from the Saved Views collection.
- Wire selection so that clicking a Saved View updates the dashboard’s current configuration.
- Show the selected Saved View as active in the list.
- Make the applied `filters`, `sort`, and `columns` visibly testable in the dashboard UI.
- Implement an empty-state message that explains there are no Saved Views yet and that users can save views later.
- Add basic tests for:
  - Rendering Saved Views.
  - Empty state.
  - Selection applying a view.
  - Active/selected-state indication.

Implementation can use dummy data or a simple in-memory store for Saved Views.

## Recommended Implementation Boundary

- `Dashboard` owns the current dashboard configuration state.
- `savedViews` state (or equivalent) owns the collection of Saved Views and the `activeSavedViewId`.
- `SavedViewsList` is kept lightweight and interaction-focused:
  - receives `savedViews`
  - receives `activeSavedViewId`
  - emits selection intent such as `onSelect(savedViewId)`
- Avoid coupling `SavedViewsList` to dashboard-specific state shape beyond what is needed to render and select.

## Files Likely Affected

_(Adjust names to your chosen stack once ARCHITECTURE.md is written.)_

- `src/components/SavedViewsList.*`
- `src/components/Dashboard.*`
- `src/state/savedViews.*` or similar
- `src/tests/SavedViewsList.test.*`
- `src/tests/Dashboard.test.*` or equivalent if visible apply behaviour is asserted at dashboard level

## Acceptance Checks

- When there are one or more Saved Views, their names appear in the UI.
- Clicking a Saved View updates the dashboard’s visible `filters`, `sort`, and `columns` to match that view.
- The selected Saved View is visibly identified as active in the list.
- When there are no Saved Views, an empty-state message explains that users can save views later.
- Tests are present and passing for list rendering, empty state, visible apply behaviour, and active-state indication.
- No console errors or obvious UI glitches for this Step.

## Risks / Considerations

- Keep the Saved View shape simple: `{ id, name, filters, sort, columns }`.
- Avoid introducing alternate names such as “preset”, “template”, “query”, “rank”, or “fields”.
- Avoid tightly coupling the Saved Views list to a specific dashboard implementation so it can be reused.
- Prefer tests that verify visible outcomes instead of internal store implementation details.

## Notes for Reviewers

- Focus review on clarity of component boundaries and state handling.
- Confirm that naming aligns with `DOMAIN_LANGUAGE.md`.
- Confirm that the Step does not sneak in create/rename/delete logic; those belong to later Steps.
- Confirm that apply behaviour is visible and testable from the UI, not only through internal state.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · github.com/fpmcguire/moderated-ai-development-workflow
