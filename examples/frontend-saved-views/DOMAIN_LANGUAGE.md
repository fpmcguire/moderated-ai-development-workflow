# Domain Language – Saved Views Example

Project: Frontend Saved Views  
Owner: Tech Lead  
Last updated: 2026-03-15

| Preferred term          | Category        | Definition                                                         | Business meaning                                         | Technical meaning                                                                     | Allowed synonyms           | Banned / risky synonyms         | Owner         | Source artifact        | Code naming guidance                                      | Notes                                                |
| ----------------------- | --------------- | ------------------------------------------------------------------ | -------------------------------------------------------- | ------------------------------------------------------------------------------------- | -------------------------- | ------------------------------- | ------------- | ---------------------- | --------------------------------------------------------- | ---------------------------------------------------- | --------------------- |
| Dashboard               | Product         | Main screen where users view and interact with their data          | Workspace where users do daily work                      | Top-level page/component showing data and controls                                    | Main view                  | Home, screen                    | Product Owner | PRODUCT.md             | `Dashboard`, `DashboardPage`                              | Keep distinct from the entire application            |
| Saved View              | Business domain | Named snapshot of dashboard configuration                          | A reusable way to return to a preferred dashboard layout | Object holding `id`, `name`, `filters`, `sort`, and `columns`                         | View                       | Preset, template                | Product Owner | PRODUCT.md             | `SavedView`, `savedViews`                                 | Canonical shape should stay stable across Steps      |
| Active Saved View       | Business domain | The Saved View currently selected and applied in the dashboard     | The view the user is currently working from              | Selected Saved View identifier or derived state that points to the applied Saved View | Selected view, active view | Current preset, chosen template | Tech Lead     | PRODUCT.md, STEP-01.md | `activeSavedViewId`, `selectedSavedViewId`                | Keep separate from the Saved Views collection        |
| Filters                 | Business domain | Conditions that narrow the data shown on the dashboard             | How users focus on relevant items                        | Key-value constraints applied when querying or presenting data                        | Filter settings            | Search, query                   | Tech Lead     | PRODUCT.md             | `filters`, `currentFilters`                               | Represent as a simple key-value map                  |
| Sort                    | Business domain | Order in which dashboard items are displayed                       | How users prioritize what they see first                 | Field + direction pair applied to the data                                            | Sort order                 | Rank                            | Tech Lead     | PRODUCT.md             | `sort`, `currentSort`, `sortBy`, `sortDirection`          | Use `'asc'                                           | 'desc'` for direction |
| Columns                 | Product         | Visible columns in a tabular view                                  | What information appears at a glance                     | Array of column keys/names in the dashboard table                                     | Visible columns            | Fields                          | Tech Lead     | PRODUCT.md             | `columns`, `visibleColumns`                               | Keep separate from filter definitions                |
| Dashboard Configuration | Technical       | Combined dashboard state represented by filters, sort, and columns | The user’s current working setup on the dashboard        | Object or related state slices that represent what is currently applied               | Current configuration      | Query state, layout preset      | Tech Lead     | PRODUCT.md, STEP-01.md | `dashboardConfiguration`, `currentDashboardConfiguration` | In Step 1 this should be visibly reflected in the UI |
| Step                    | Delivery        | Small, verifiable unit of work in MOD-W                            | One slice of progress that can be explained to others    | One iteration through the MOD-W Step lifecycle                                        | Roadmap step               | Ticket, task                    | Moderator     | ROADMAP.md             | `step-01`, `step-02` tags & files                         | Always small enough for one iteration                |

## Naming Guidance

- Prefer `SavedView` over generic `view` in code unless the local context is already unambiguous.
- Prefer `filters`, `sort`, and `columns` over alternative terms.
- Prefer `activeSavedViewId` for Step 1 when the UI needs to mark the selected Saved View.
- Avoid introducing synonyms that hide the product language the Development Team is expected to keep consistent.

Use this matrix as a reference when naming components, props, state variables, tests, and prompts for the Saved Views example.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
