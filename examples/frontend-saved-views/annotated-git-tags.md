# Annotated Git Tags — Frontend Saved Views

This document describes the git tagging convention used in this example project to mark the completion of each Moderated AI Development Workflow step.

---

## Convention

Each completed step is tagged at the commit where its accepted artifacts were merged. Tags follow the format:

```
step/NN-short-title
```

The tag annotation includes:

- Step number and title
- Date completed
- Moderator who accepted the step
- Summary of what was produced

---

## Tags in This Example

### `step/01-savedview-api`

```
git tag -a step/01-savedview-api -m "Step 01: SavedView Data Model and REST API

Completed: 2026-01-20
Moderator: Jordan Rivera
QA: Sam Okafor

Produced:
- migrations/20260113_create_saved_views.sql
- src/api/saved-views/routes.ts
- src/api/saved-views/validators.ts
- src/types/saved-view.ts
- src/api/saved-views/routes.test.ts

All Level 2 quality gate criteria met.
See examples/frontend-saved-views/REVIEW.md and QA.md for details."
```

### `step/02-savedview-store`

```
git tag -a step/02-savedview-store -m "Step 02: Zustand Slice and React Query Hooks

Completed: 2026-01-28
Moderator: Jordan Rivera
QA: Sam Okafor

Produced:
- src/stores/savedViewsSlice.ts
- src/hooks/useSavedViews.ts
- src/types/saved-view.ts (extended with frontend types)
- src/stores/savedViewsSlice.test.ts

All Level 2 quality gate criteria met."
```

---

## Why Tag Steps?

Annotated git tags serve several purposes in a Moderated AI Development Workflow project:

1. **Traceability** — Any commit can be related back to the Moderated AI Development Workflow step that produced it.
2. **Rollback points** — If a later step introduces a regression, the team can quickly identify the last known-good step boundary.
3. **Audit trail** — The tag annotation records who moderated and accepted the step, providing a permanent record alongside the code.
4. **Team communication** — Tags make progress visible to anyone browsing the repository, without needing to read every commit message.

---

## Creating Tags

After a step is accepted (REVIEW.md decision = Accept) and QA passes (QA.md result = Pass):

```bash
git tag -a step/NN-short-title -m "$(cat <<'EOF'
Step NN: Full Step Title

Completed: YYYY-MM-DD
Moderator: Name
QA: Name

Produced:
- path/to/file1
- path/to/file2

[Quality gate level and summary]
EOF
)"

git push origin step/NN-short-title
```

---

MOD-W v1.1.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
