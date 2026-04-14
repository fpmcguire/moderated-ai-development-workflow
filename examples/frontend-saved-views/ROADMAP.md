# Roadmap: Saved Views (Frontend Example)

This roadmap breaks the Saved Views feature into small Moderated AI Development Workflow Steps that can each be implemented, reviewed, and tagged independently.

---

## Step 1 – Saved Views List (Read-only)

**Goal**  
Display a list of Saved Views for the current user and allow selecting one to apply its configuration to the current dashboard.

**In scope**

- Render a Saved Views list for the current dashboard
- Allow selecting a Saved View
- Apply the Saved View to mocked dashboard state
- Show which Saved View is currently active/selected
- Show the applied `filters`, `sort`, and `columns` visibly in the dashboard
- Show an empty state when no Saved Views exist
- Add basic component tests for list rendering, empty state, and apply behaviour

**Out of scope**

- Creating new Saved Views
- Renaming or deleting Saved Views
- Cross-dashboard reuse
- Backend persistence

**Deliverables**

- UI panel or menu showing the Saved Views list
- Click handler to apply a Saved View
- Selected/active-state indication for the currently applied Saved View
- Visible dashboard summary or equivalent UI that reflects applied `filters`, `sort`, and `columns`
- Basic empty state when no Saved Views exist
- Basic component tests for list rendering, empty state, and apply behaviour

**Dependencies**

- Basic dashboard shell and dummy data
- Local in-memory representation of Saved Views using the canonical shape: `id`, `name`, `filters`, `sort`, `columns`
- A simple way to track the active selected Saved View separately from the collection itself

**Acceptance checks**

- When at least one Saved View exists, the list renders their names
- Clicking a Saved View changes the visible `filters`, `sort`, and `columns` to match that Saved View
- The currently applied Saved View is visibly identified as active/selected
- When there are no Saved Views, an empty state message explains that users can save views later
- Tests cover list rendering, empty state, and visible apply behaviour

---

## Step 2 – Create Saved View

**Goal**  
Allow users to create a new Saved View from the current dashboard state for the current dashboard only.

**In scope**

- “Save view” entry point
- Create Saved View form with name input
- Capture current dashboard state into a new Saved View using the canonical shape
- Required-name validation
- Duplicate-name validation
- Automatically select the newly created Saved View
- Tests for create flow and validation

**Out of scope**

- Renaming existing Saved Views
- Deleting existing Saved Views
- Explicit overwrite/update of an existing Saved View
- Cross-dashboard reuse
- Backend persistence

**Deliverables**

- “Save view” button or entry point in the dashboard
- Create Saved View form (modal or in-place) with name input
- Logic to capture current dashboard configuration and store a new Saved View
- Validation for required name and duplicate names
- Active selected-state updates after create
- Tests for create flow and validation

**Dependencies**

- Step 1 complete and tagged
- Access to current dashboard state (`filters`, `sort`, `columns`)

**Acceptance checks**

- User can open the Save View UI, type a name, and save a new Saved View
- The new Saved View appears in the list after save
- The new Saved View becomes the active selected view immediately after creation
- Applying the new Saved View restores the visible `filters`, `sort`, and `columns` that were active when it was saved
- If the name is empty, the user sees a validation error
- If the name duplicates an existing Saved View for the same dashboard, the user sees a clear validation error
- Tests cover create flow and visible validation behaviour

---

## Step 3 – Rename and Delete Saved View

**Goal**  
Allow users to rename or delete existing Saved Views for the current dashboard.

**In scope**

- Rename action
- Delete action
- Validation during rename
- Clear feedback or confirmation for delete
- Tests for rename and delete behaviour

**Out of scope**

- Creating new Saved Views
- Explicit overwrite/update of an existing Saved View
- Cross-dashboard reuse
- Backend persistence

**Deliverables**

- UI affordances to rename and delete (for example context menu or inline actions)
- Rename flow with required-name and duplicate-name validation
- Delete confirmation or simple delete with clear feedback
- Correct active-state handling after rename or delete
- Tests for rename and delete behaviour

**Dependencies**

- Steps 1 and 2 complete and tagged

**Acceptance checks**

- User can rename a Saved View and see the new name in the list
- If the renamed value is empty, the user sees a validation error
- If the renamed value duplicates an existing Saved View name for the same dashboard, the user sees a clear validation error
- User can delete a Saved View and it disappears from the list
- Applying remaining Saved Views still works correctly after rename or delete
- Active-state handling remains correct after rename or delete
- Tests cover rename and delete behaviour

---

## Notes

- Saved Views are scoped to one dashboard only in this example
- Persistence remains in memory for this example; a later profile can introduce backend integration as new Steps
- Explicit “Update current view” / overwrite is intentionally deferred out of scope for this initial roadmap
- Each Step should follow the Moderated AI Development Workflow lifecycle: define STEP.md → Development Team implementation → Workbench verification → revision loop → Tech Lead review → QA → annotated tag

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
