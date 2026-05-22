# Moderated AI Development Workflow (MOD-W)

MOD-W is a role-driven, document-centered workflow for AI‑assisted software development. It separates product, technical, and implementation decisions across distinct roles, enforces cross-validation between multiple AI agents and models, and requires a human Moderator to approve every step before it is accepted. The result is small, reviewable, traceable increments — viable coding, not vibe coding.

Full methodology reference: https://github.com/fpmcguire/moderated-ai-development-workflow

---

## Roles

| Role                 | Owns                                                            | AI agent (default)                                                              |
| -------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Moderator**        | Workflow orchestration, go/no-go authority, HITL gate           | Human only                                                                      |
| **Product Owner**    | What and why — `PRODUCT.md`, acceptance intent                  | Claude chatbot + Perplexity + Gemini (Definition); Claude Code SubAgent (Validation) |
| **Tech Lead**        | How — `ARCHITECTURE.md`, `ROADMAP.md`, step design, tech review | Codex (reads `AGENTS.md` at repo root)                                          |
| **Development Team** | Implementation — code, tests, docs for each step                | Claude Code (reads `CLAUDE.md` at repo root)                                    |
| **QA / Tester**      | End-to-end verification — `QA.md`                               | Claude Code SubAgent (spawned by Development Team session)                      |

Cross-validation is intentional: Codex plans and reviews; Claude Code implements. Model diversity at the Tech Lead / Dev Team boundary is MOD-W's primary quality lever. `AGENTS.md` configures the Tech Lead role for Codex; `CLAUDE.md` configures the Development Team role for Claude Code. Both live at the repo root and are read automatically at session start.

---

## Cross-validation

The key differentiator in MOD-W is **intentional role and model diversity**. No single agent both plans and implements. No single agent both implements and reviews.

```
Product Owner (Claude chatbot / SubAgent)  →  defines what and why
       ↓ cross-checks
Tech Lead (Codex)                          →  defines how; reviews Dev Team output
       ↓ cross-checks
Development Team (Claude Code)             →  implements only the approved slice
       ↓ cross-checks
QA + Product Owner SubAgents (Claude Code) →  validate acceptance checks and intent
       ↓ cross-checks
Moderator (human)                          →  reconciles all; has final authority
```

Each handoff is a validation surface: the Tech Lead challenges the Product Owner's intent; the Development Team surfaces ambiguities in the Tech Lead's spec; the QA SubAgent validates against acceptance checks; the Moderator detects drift across all roles. Using different models for different roles prevents any single model's blind spots from propagating unchecked through the workflow.

---

## Workflow — role sequence per step

The Moderator is always the human gate. Phases 2–3 iterate until all acceptance checks are met.

**Phase 1 — Define the step**

1. **Moderator + Tech Lead (Codex)** — trigger a Tech Lead Planning Session. Codex reads `AGENTS.md` automatically. Provide `PRODUCT.md` and existing `ARCHITECTURE.md`; Codex generates or updates `ARCHITECTURE.md`, `DOMAIN_LANGUAGE.md`, `ROADMAP.md`, `STEP-XX.md`, `CLAUDE.md`, and `AGENTS.md`.
2. **Moderator decision** — review and approve all artifacts. Confirm `CLAUDE.md` and `AGENTS.md` are committed to the repo root before briefing the Development Team.

**Phase 2 — Implement**

3. **Moderator → Development Team (Claude Code)** — open a Claude Code session; `CLAUDE.md` loads automatically. State the active Step (e.g. `The current Step is STEP-02.md`). Development Team restates the step, proposes a plan, and waits for Moderator approval before writing any files.
4. **Development Team** — implements only the approved scope; runs the blocking build gate; summarizes changes against the acceptance checks in `STEP-XX.md`; spawns QA and Product Owner SubAgents.

**Phase 3 — Review and iterate** _(repeat until green)_

5. **QA SubAgent** — validates acceptance checks, writes `QA.md`. **Product Owner SubAgent** — validates against `PRODUCT.md` intent, writes sign-off.
6. **Moderator (Workbench)** — reviews the diff (Claude Code edits directly — no pull required); builds, runs tests, manually exercises the feature; performs manual checks flagged by QA SubAgent. Minor issues fixed directly; significant issues return to Development Team with explicit feedback.
7. **Tech Lead (Codex Review Session)** — Codex reads changed files and `STEP-XX.md` directly; reviews for architectural fit, naming consistency, and maintainability; writes `REVIEW.md` classifying findings as must-fix or could-fix-later.
8. **Development Team** — addresses each must-fix item explicitly; re-runs build gate; reports back.
9. **→ Return to step 5** until all acceptance checks pass and Tech Lead has approved.

**Phase 4 — Accept and advance**

10. **Moderator final gate (HITL)** — confirms all checks pass, `REVIEW.md` and `QA.md` are complete. Creates annotated Git tag. Advances `ROADMAP.md` to the next step.

---

## Canonical documents

| Document             | Purpose                                                      |
| -------------------- | ------------------------------------------------------------ |
| `MOD-W.md`           | This file — workflow quick-reference for the project         |
| `PRODUCT.md`         | What is being built, for whom, and why                       |
| `ARCHITECTURE.md`    | Technical structure, stack, patterns, constraints            |
| `DOMAIN_LANGUAGE.md` | Canonical terms used across docs, prompts, and code          |
| `ROADMAP.md`         | Ordered sequence of small, reviewable steps                  |
| `STEP-XX.md`         | Current step — goal, scope, inputs, acceptance checks        |
| `REVIEW.md`          | Review notes and decisions for the current step              |
| `QA.md`              | Verification evidence for the current step                   |
| `AI_AGENTS.md`       | Agent registry — models, interfaces, data handling decisions |
| `AGENTS.md`          | Tech Lead config for Codex (lives at repo root)              |
| `CLAUDE.md`          | Development Team config for Claude Code (lives at repo root) |

All MOD-W docs live under `mod-w/` in the project. `AGENTS.md` and `CLAUDE.md` live at the **repo root** so Codex and Claude Code read them automatically.

---

## Operating rules

- **Documents must earn their existence.** Prefer updating an existing doc over creating a new one.
- **No hidden scope.** Anything not in the current `STEP-XX.md` is out of scope for this step.
- **Explicit out-of-scope.** When something is deferred, state it.
- **Stable naming.** Resolve naming conflicts early; keep `DOMAIN_LANGUAGE.md` current.
- **Pause on ambiguity.** Any role that is unsure stops and clarifies rather than guessing.
- **Lean first, expand later.** Start with `PRODUCT.md`, `ROADMAP.md`, and `STEP-XX.md`; add further docs only when they clearly help.
- **Commit before switching agents.** If you move between Codex and Claude Code within a step, commit first so both agents read the current file state.

---

MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
