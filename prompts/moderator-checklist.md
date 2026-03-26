# Moderator Checklist – MOD-W

Use this checklist for every Step in the MOD-W workflow.

---

## 1. Before Engaging AI

- [ ] ROADMAP.md: next Step chosen and clearly named.
- [ ] STEP-XX.md: goal, scope, inputs, required changes, acceptance checks, risks filled in.
- [ ] DOMAIN_LANGUAGE_MATRIX.md: key terms for this Step defined or updated.
- [ ] PRODUCT.md / ARCHITECTURE.md: still accurate for this Step.

---

## 2. With Product Owner (ChatGPT)

- [ ] Present Step context and current PRODUCT.md excerpt.
- [ ] Ask for refinement of:
  - Problem/goal wording
  - User workflows touched by this Step
  - Acceptance intent for this Step
- [ ] Apply any clarifications back into PRODUCT.md and STEP-XX.md.

---

## 3. With Tech Lead (ChatGPT)

- [ ] Present PRODUCT.md, ARCHITECTURE.md excerpt, DOMAIN_LANGUAGE_MATRIX.md rows, and STEP-XX.md.
- [ ] Ask Tech Lead to:
  - Confirm Step scope (small, verifiable, technically sane).
  - Suggest likely affected files and data structures.
  - Flag any architectural risks.
- [ ] Update ARCHITECTURE.md and STEP-XX.md as needed.

---

## 4. Briefing the Development Team (Claude)

- [ ] Prepare a **context packet**:
  - Relevant PRODUCT.md sections
  - Relevant ARCHITECTURE.md sections
  - Relevant DOMAIN_LANGUAGE_MATRIX.md rows
  - Full STEP-XX.md
- [ ] Instruct Development Team to:
  - Restate goal and scope
  - Propose a short plan and wait for approval
- [ ] Approve or adjust the plan before any code is generated.

---

## 5. Workbench Verification (Local)

After Development Team delivers the Step:

- [ ] Pull changes into local repo (Workbench).
- [ ] Run build.
- [ ] Run tests (and linters if configured).
- [ ] Manually exercise the Step behaviour in the UI.
- [ ] Use Copilot only for:
  - Small refactors
  - Minor bug fixes
  - Non-controversial cleanup
- [ ] Record results in QA.md (for this Step).
- [ ] Draft findings in REVIEW.md.

If issues are significant:

- [ ] Summarize problems clearly.
- [ ] Send feedback back to Development Team and repeat until acceptance checks are met.

---

## 6. Tech Lead Review

- [ ] Prepare a **handoff packet** for Tech Lead:
  - STEP-XX.md
  - Summary of changes (files, behaviours)
  - Key diffs or descriptions
  - QA/verification summary
- [ ] Ask Tech Lead for:
  - Architectural fit review
  - Naming and structure feedback
  - Must-fix vs nice-to-have items
- [ ] Record recommendations in REVIEW.md.
- [ ] If must-fix items exist, send back to Development Team and re-verify.

---

## 7. QA & Documentation

- [ ] Finalize QA.md for this Step:
  - Tests run and results
  - Manual checks list
  - Bugs found and their status
  - Regression risk and confidence level
- [ ] Update PRODUCT.md if behaviour or UX changed.
- [ ] Update ARCHITECTURE.md if design decisions changed.
- [ ] Update ROADMAP.md to mark this Step complete and adjust future Steps if needed.

---

## 8. Tag and Advance

- [ ] Create an **annotated Git tag** for the Step, including:
  - Step identifier (e.g., `step-01-saved-views-list`)
  - Short description
  - References to STEP-XX.md, REVIEW.md, QA.md
  - Notable decisions / caveats
- [ ] Push the tag to the remote repository.
- [ ] Select the next Step from ROADMAP.md and move back to section 1.

---

This checklist should be lightweight enough to use for every Step but strict enough to preserve Moderated AI Development’s multi-layer validation and traceability.

---

> MOD-W v1.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development
