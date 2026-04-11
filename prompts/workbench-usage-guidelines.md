# Workbench Usage Guidelines

The **Workbench** is the human-operated development environment used by the Moderator  
(e.g., local Git clone in VS Code with GitHub Copilot enabled).

Its job is to **verify and fine‑tune**, not to replace the Moderated AI Development Workflow.

---

## What the Workbench IS for

- Running builds, tests, and linters.
- Manually exercising the UI and flows for the current Step.
- Applying **small, safe edits**, such as:
  - Fixing typos and obvious bugs
  - Minor refactors (rename, extract small function)
  - Adjusting styles or layout details
- Resolving simple merge conflicts.
- Preparing clean commits and annotated tags.

---

## What the Workbench is NOT for

- Skipping Moderated AI Development Workflow Steps (e.g., implementing large features entirely by hand).
- Making broad architectural changes without going through the Tech Lead.
- Quietly expanding Step scope without updating STEP.md and ROADMAP.md.
- Letting Copilot generate large, unreviewed code dumps.

---

## Practical Rules

- If a change is **larger than a few lines or one small component**, send it back to the Development Team agent as a new revision request.
- If a change affects architecture, domain terms, or multiple modules, involve the Tech Lead agent and update ARCHITECTURE.md and/or DOMAIN_LANGUAGE_MATRIX.md.
- If you fix something directly in the Workbench that matters to behaviour, update:
  - REVIEW.md (what changed and why)
  - QA.md (what you re‑verified)

---

## Typical Workbench Flow for a Step

1. Pull the Development Team’s branch / patch.
2. Build, run tests, and lint.
3. Manually test the Step in the UI.
4. Apply small fixes with Copilot if needed.
5. Commit local changes.
6. Update QA.md and REVIEW.md.
7. Proceed to Tech Lead review and tagging.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
