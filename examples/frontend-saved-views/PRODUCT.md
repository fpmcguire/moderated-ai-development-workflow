# Product: Saved Views for Dashboard

## Name

Saved Views

## Problem

Users working in a dashboard often switch between different combinations of filters, sorting, and visible columns (for example, “My open items” or “All items this week”).  
Recreating these combinations every time is slow, repetitive, and error-prone.

## Users

- Individual SaaS users working in a dashboard
- Small teams who share common ways of looking at the same data

## Core Value Proposition

Let users save, apply, rename, and delete their preferred dashboard configurations so they can return to them with a single click instead of rebuilding them manually.

## Product Principles for This Example

- Keep the domain language stable: `SavedView`, `filters`, `sort`, and `columns` are the canonical terms.
- Keep the data shape simple so later Steps do not need to rework Step 1.
- Make “apply Saved View” visible in the UI so behaviour is easy to review and test.
- Keep the implementation frontend-only and junior-friendly, while leaving a clean path to later backend integration.

## Primary Workflow s

1. **Create Saved View**
   - User configures filters, sorting, and columns on the dashboard.
   - User clicks “Save view”, provides a name, and saves.
   - The new Saved View appears in the list and becomes the active selected view.

2. **Apply Saved View**
   - User opens the Saved Views list.
   - User selects a Saved View.
   - The visible filters, sorting, and columns change to match that Saved View.
   - The selected Saved View is shown as the active view in the list.

3. **Rename Saved View**
   - User opens Saved Views actions.
   - User renames an existing Saved View.
   - The updated name appears in the list.

4. **Delete Saved View**
   - User opens Saved Views actions.
   - User deletes a Saved View they no longer need.
   - The Saved View is removed from the list.

## Functional Requirements (v1)

- Show a list of Saved Views for the current user.
- Scope Saved Views to the current dashboard only.
- Represent each Saved View using the canonical shape: `id`, `name`, `filters`, `sort`, `columns`.
- Allow creating a new Saved View from the current dashboard state.
- Allow applying a Saved View to the dashboard.
- Allow renaming a Saved View.
- Allow deleting a Saved View.
- Track which Saved View is currently active/selected in the UI.
- Require a name when creating or renaming a Saved View.
- Do not allow duplicate Saved View names within the same dashboard; show a clear validation error instead.

(For this example, persistence can be mocked or kept in memory; the focus is frontend behaviour.)

## Non-Functional Expectations

- Fast UI feedback with no obvious blocking for basic operations
- Clear, minimal UI that junior developers can understand
- Code organized so it can later be wired to a real backend API
- Behaviour should be easy to verify from the visible UI, not only from internal state

## UX Expectations

- Two screens (or one screen plus modal) are enough:
  - Dashboard with a “Saved Views” panel or menu
  - Create/Edit Saved View form (modal or dedicated area)
- The Saved Views list should show which Saved View is currently active/selected
- The dashboard should visibly reflect the currently applied `filters`, `sort`, and `columns`
- Empty state explains that there are no Saved Views yet and that users will be able to save views
- Basic error states (for example duplicate name or failed save) are surfaced clearly
- After a new Saved View is created, it becomes the active selected view

## Constraints

- Frontend-only example; no real auth or backend integration is required
- Use a modern component-based frontend stack (for example React + TypeScript) but keep the product description framework-agnostic
- Keep state management simple enough for juniors to follow

## In Scope (for this example)

- Single-dashboard Saved Views
- In-memory or mocked persistence
- Create, apply, rename, and delete flows
- Basic validation and component-level tests
- Visible selected-state and visible applied-state feedback in the UI

## Out of Scope (for this example)

- Reusing Saved Views across multiple dashboards
- Multi-user sharing of views
- Permission management
- Complex query builders
- “Default view” behaviour
- Explicit “Update current view” / overwrite flow
- Backend API design and persistence details

## Acceptance Intent

For the **Saved Views example**, Moderated AI Development Workflow is considered successful if:

- A user can create, apply, rename, and delete Saved Views in the UI
- Saved Views are scoped to one dashboard
- Duplicate names are prevented with a clear validation message
- The visible dashboard configuration changes to match the selected Saved View
- The active selected Saved View is clear in the list
- Behaviour is covered by basic tests that verify visible outcomes (at least component-level)
- Steps are delivered via the Moderated AI Development Workflow lifecycle with clear artifacts, reviews, and an annotated tag for at least Step 1

## Open Questions

- How should we represent Saved View state for eventual backend integration?
- When backend persistence is introduced later, should active selection be restored per dashboard session or per user preference?

---

MOD-W v1.1.0 · Moderated AI Development Workflow · github.com/fpmcguire/moderated-ai-development-workflow
