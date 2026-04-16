# Step Lifecycle

In Moderated AI Development Workflow, every meaningful change is delivered as a **Step**.  
A Step is small enough to understand, implement, review, and verify end‑to‑end without overloading any AI agent or the Moderator.

This lifecycle assumes your default roles:

- Moderator (human)
- Product Owner (Claude Code SubAgent)
- Tech Lead (Claude Code full session)
- Development Team (Claude Code full session)
- QA (Claude Code SubAgent)

---

## 1. Define the Step

**Who:** Tech Lead (Claude Code session), Moderator  
**Artifacts:** ARCHITECTURE.md, ROADMAP.md, STEP-XX.md, CLAUDE.md, AGENTS.md

- Moderator triggers a Tech Lead Planning Session.
- Tech Lead reads `PRODUCT.md` and existing `ARCHITECTURE.md`.
- Tech Lead writes or updates `ARCHITECTURE.md`, `ROADMAP.md`, and `STEP-XX.md`.
- Tech Lead generates or updates project-specific `CLAUDE.md` and `AGENTS.md`.
- Moderator reviews and approves all artifacts before implementation begins.
- The Step is small enough to implement and verify without exhausting agent context.

Output: Approved `STEP-XX.md` and updated planning artifacts.

---

## 2. Brief the Development Team

**Who:** Moderator → Development Team (Claude Code session)  
**Artifacts:** CLAUDE.md, STEP-XX.md

- Confirm `CLAUDE.md` and `AGENTS.md` are current in the repo root (Tech Lead maintains these).
- Start a Claude Code session in the project root — role context loads automatically.
- State the active Step at session start, e.g.:
  `The current Step is STEP-02.md`
- Ask the Development Team to confirm understanding and raise any clarifying questions before proceeding.

Output: Shared understanding of the Step; any refinements folded back into `STEP-XX.md`.

---

## 3. Implementation Options Gate

**Who:** Development Team (Claude Code session) → Moderator  
**Artifacts:** STEP-XX.md, ARCHITECTURE.md, AGENTS.md

- Development Team enters Plan Mode: reads relevant files, confirms scope. No files written yet.
- Development Team proposes an implementation plan and pauses.
- Moderator may request one or both of:
  - `options` — 2–3 implementation paths with trade-offs and a recommendation
  - `ramifications` — technical debt risks, side effects, and likely pain points for the chosen path
- Moderator approves a plan before any code is written.

See: [`prompts/prompt-guidelines.md`](../prompts/prompt-guidelines.md) for the Options/Ramifications/Mentorship protocol.

Output: Moderator-approved implementation plan.

---

## 4. Implement the Step

**Who:** Development Team (Claude Code SubAgent)  
**Artifacts:** Code, tests, docs

- Development Team implements only the current Step following the approved plan:
  - Code and configuration
  - Tests (unit/component/integration as appropriate)
  - Any relevant docs (comments, README fragments, etc.)
- **Build Gate (blocking):** runs `{{BUILD_COMMAND}}` and `{{TEST_COMMAND}}`. Fixes all failures and re-runs until both pass. Does not proceed until clean.
- Summarizes changes and open questions for the Moderator.

Output: Implemented Step with passing build.

---

## 5. Tech Lead Review + Revision Loop

**Who:** Tech Lead (Codex Review Session) ↔ Development Team  
**Artifacts:** REVIEW.md

- Moderator triggers a Tech Lead Review Session (Codex).
- Tech Lead reads `STEP-XX.md`, implementation diff.
- Tech Lead reviews for:
  - Architectural alignment
  - Maintainability and readability
  - Domain language consistency
  - Potential risks or follow‑ups
- Tech Lead writes `REVIEW.md` with verdict and findings.
- If rework required: Tech Lead sends findings directly to Dev Team (no Moderator in loop).
- Dev Team revises, re-runs build gate, reports back to Tech Lead.
- Loop continues until Tech Lead approves.
- Moderator may intervene if a revision introduces a scope or product intent conflict.

Output: `REVIEW.md` with Tech Lead approval.

---

## 6. QA + Product Owner Validation

**Who:** QA SubAgent, Product Owner SubAgent (both Claude Code)  
**Artifacts:** QA.md, Product Owner sign-off

Triggered only after Tech Lead approval.

- **QA SubAgent** reads implementation files and `STEP-XX.md` acceptance checks, writes `QA.md`.
- **Product Owner SubAgent** reads `QA.md` and validates against `PRODUCT.md` intent, writes sign-off.

Output: `QA.md` and Product Owner sign-off.

---

## 7. Moderator Spot Check

**Who:** Moderator  
**Artifacts:** QA.md, Product Owner sign-off

- Moderator reviews `QA.md` and Product Owner sign-off.
- Performs manual checks flagged by the QA SubAgent as requiring human or browser verification (UX, visual, edge cases).
- Does **not** re-run the build or tests — the build gate already ensures a clean pass.
- If spot check reveals substantial issues, returns them to the Dev Team with focused feedback.

Output: Manual checks completed; step cleared for final gate.

---

## 8. Tag and Advance (Final Gate)

**Who:** Moderator  
**Artifacts:** Git history, annotated tag, ROADMAP.md

- Moderator creates an **annotated Git tag** for the Step, including:
  - Step identifier and short description
  - Link or reference to `STEP-XX.md`, `REVIEW.md`, and `QA.md`
  - Notable decisions or caveats
- ROADMAP.md is updated to mark the Step as done and highlight follow-up work.
- Moderator selects the next Step and returns to stage 1.

Output: Traceable milestone for the Step and a clear starting point for the next one.

---

## 10. Documentation Update

**Who:** Moderator  
**Artifacts:** PRODUCT.md, ARCHITECTURE.md, ROADMAP.md

- Moderator updates planning artifacts to reflect any decisions made during the Step:
  - `PRODUCT.md` if behaviour or UX changed meaningfully
  - `ARCHITECTURE.md` if design decisions changed
  - `ROADMAP.md` to mark the Step as complete and adjust future Steps if needed

Output: Updated documentation reflecting the completed Step.

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

MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
