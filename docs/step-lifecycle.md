# Step Lifecycle

In Moderated AI Development Workflow, every meaningful change is delivered as a **Step**.  
A Step is small enough to understand, implement, review, and verify end‑to‑end without overloading any AI agent or the Moderator.

This lifecycle is tool‑agnostic but assumes your default roles:

- Moderator (human)
- Product Owner (ChatGPT)
- Tech Lead (ChatGPT)
- Development Team (Claude)
- Workbench (VS Code + Copilot)

---

## 1. Define the Step

**Who:** Product Owner, Tech Lead, Moderator  
**Artifacts:** PRODUCT.md, ROADMAP.md, STEP.md

- Product Owner and Tech Lead agree on the next Step from `ROADMAP.md`.
- Moderator captures it in `STEP.md` with goal, scope, inputs, acceptance checks, and risks.
- The Step is small enough to implement and verify without exhausting agent context.

Output: A clear, approved `STEP.md`.

---

## 2. Brief the Development Team

**Who:** Moderator → Development Team (Claude)  
**Artifacts:** PRODUCT.md, ARCHITECTURE.md, STEP.md, DOMAIN_LANGUAGE.md

The Moderator chooses the Development Team interface for this Step:

**Claude chatbot (claude.ai)**

- Prepare a **context packet**: focused excerpts from PRODUCT, ARCHITECTURE, and
  domain language plus the current `STEP.md`.
- Paste `development-team-claude.md` as the role prompt at session start.
- Attach or paste the active `STEP-XX.md` directly into the thread.

**Claude Code (CLI)**

- Confirm `CLAUDE.md` is current in the repo root.
- Start a Claude Code session in the project root — role context loads automatically.
- State the active Step at session start, e.g.:
  `The current Step is apps/my-app/mod-w/STEP-02.md`

**Hybrid (chatbot for planning, Claude Code for implementation)**

- Use the chatbot for the planning and confirmation pass.
- Commit the repo, then switch to Claude Code for file writing.
- State the active Step path when opening the Claude Code session.

In all cases, ask the Development Team to:

- Confirm understanding
- Ask clarifying questions
- Optionally refine the Step description (without expanding scope)

Output: Shared understanding of the Step and any refinements folded back into `STEP.md`.

---

## 3. Implement the Step

**Who:** Development Team (Claude)  
**Artifacts:** Code, tests, docs; STEP.md

- Development Team implements only the current Step.
- It updates or adds:
  - Code and configuration
  - Tests (unit/component/integration as appropriate)
  - Any relevant docs (comments, README fragments, etc.)
- It summarizes changes and open questions for the Moderator.

Output: A proposed implementation for the Step in a branch or patch, plus a short summary.

---

## 4. Workbench Verification

**Who:** Moderator using the Workbench  
**Artifacts:** QA.md (draft), REVIEW.md (draft)

- Moderator pulls the changes into the local Workbench (e.g., VS Code + Copilot).
- Runs build, tests, and linters.
- Manually exercises the feature or UI for the Step.
- Uses Copilot for light‑to‑moderate fixes (typos, small refactors, trivial bugs).
- Records results and any issues in `QA.md` and `REVIEW.md` as needed.

If problems are minor, the Moderator may fix them directly in the Workbench; if they are substantial, they go back to the Development Team.

Output: Verified or partially verified implementation plus initial QA/Review notes.

---

## 5. Revision Loop

**Who:** Moderator ↔ Development Team, Tech Lead as needed  
**Artifacts:** STEP.md, REVIEW.md, QA.md

- Moderator sends focused feedback to the Development Team:
  - Failing tests
  - Behaviour mismatches
  - Architectural or naming issues
  - UX issues
- Development Team revises the implementation.
- Moderator re‑runs Workbench verification.
- Tech Lead is involved when:
  - Architecture decisions are affected
  - Trade‑offs or alternatives need evaluation

The loop continues until the Step satisfies the acceptance checks in `STEP.md`.

Output: Implementation that passes Workbench verification and addresses review comments.

---

## 6. Tech Lead Review

**Who:** Tech Lead (ChatGPT) + Moderator  
**Artifacts:** REVIEW.md, ARCHITECTURE.md, DOMAIN_LANGUAGE.md

- Moderator prepares a **handoff packet** for the Tech Lead:
  - Current `STEP.md`
  - Summary of changes
  - Key diffs or file list
  - QA/verification notes
- Tech Lead reviews for:
  - Architectural alignment
  - Maintainability and readability
  - Domain language consistency
  - Potential risks or follow‑ups
- Moderator records Tech Lead comments and recommendations in `REVIEW.md`.

If Tech Lead requires changes, the Step returns to the Revision Loop.

Output: Tech Lead approval or specific recommendations applied.

---

## 7. QA & Documentation

**Who:** Moderator / QA  
**Artifacts:** QA.md, PRODUCT.md, ARCHITECTURE.md, ROADMAP.md

- QA/Moderator finalizes `QA.md` for the Step:
  - Tests run and results
  - Manual checks performed
  - Known limitations or deferred tests
- Moderator updates:
  - PRODUCT.md if behaviour or UX changed meaningfully
  - ARCHITECTURE.md if design decisions changed
  - ROADMAP.md to mark the Step as complete and adjust future Steps if needed

Output: Updated documentation and a completed QA record for the Step.

---

## 8. Tag and Advance

**Who:** Moderator  
**Artifacts:** Git history, annotated tag, ROADMAP.md

- Moderator creates an **annotated Git tag** for the Step, including:
  - Step identifier and short description
  - Link or reference to `STEP.md`, `REVIEW.md`, and `QA.md`
  - Notable decisions or caveats
- ROADMAP.md is updated to:
  - Mark the Step as done
  - Highlight any follow‑up work spawned by this Step
- Moderator selects the next Step and returns to stage 1.

Output: Traceable milestone for the Step and a clear starting point for the next one.

---

## Completion Definition

A Step is considered **complete** only when:

- `STEP.md` is satisfied
- Code builds cleanly in the Workbench
- Relevant tests pass or explicitly documented exceptions exist
- Behaviour matches acceptance checks
- Tech Lead has approved
- QA.md is updated
- An annotated Git tag has been created

This lifecycle keeps Moderated AI Development Workflow firmly human‑moderated while allowing AI roles to handle most of the drafting, implementation, and iteration work.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
