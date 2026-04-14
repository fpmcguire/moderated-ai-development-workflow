# Moderated AI Development Workflow (MOD-W)

MOD-W is a role-driven, document-centered workflow for AI‑assisted software development. It separates product, technical, and implementation decisions across distinct roles, enforces cross-validation between multiple AI agents and models, and requires a human Moderator to approve every step before it is accepted. The result is small, reviewable, traceable increments — viable coding, not vibe coding.

Full methodology reference: https://github.com/fpmcguire/moderated-ai-development-workflow

---

## Roles

| Role                 | Owns                                                            | AI agent (default)                  |
| -------------------- | --------------------------------------------------------------- | ----------------------------------- |
| **Moderator**        | Workflow orchestration, go/no-go authority, HITL gate           | Human only                          |
| **Product Owner**    | What and why — `PRODUCT.md`, acceptance intent                  | ChatGPT                             |
| **Tech Lead**        | How — `ARCHITECTURE.md`, `ROADMAP.md`, step design, tech review | ChatGPT                             |
| **Development Team** | Implementation — code, tests, docs for each step                | Claude (chatbot or Claude Code)     |
| **QA / Tester**      | End-to-end verification — `QA.md`                               | Human (or Moderator on small teams) |

The Development Team has two supported interfaces: the **Claude chatbot** (`development-team-claude.md` pasted at session start) and **Claude Code** (`CLAUDE.md` at repo root, read automatically). Both encode the same role rules. Commit the repo before switching interfaces within a step.

---

## Cross-validation

The key differentiator in MOD-W is **intentional role and model diversity**. No single agent both plans and implements. No single agent both implements and reviews.

```
Product Owner (ChatGPT)   →  defines what and why
       ↓ cross-checks
Tech Lead (ChatGPT)       →  defines how; reviews Dev Team output
       ↓ cross-checks
Development Team (Claude) →  implements only the approved slice
       ↓ cross-checks
Moderator (human)         →  reconciles all three; has final authority
```

Each handoff is a validation surface: the Tech Lead challenges the Product Owner's intent; the Development Team surfaces ambiguities in the Tech Lead's spec; the Moderator detects drift between all three. Using different models for different roles prevents any single model's blind spots from propagating unchecked through the workflow.

---

## Workflow — role sequence per step

The Moderator is always the human gate. Phases 2–3 iterate until all acceptance checks are met.

**Phase 1 — Define the step**

1. **Moderator + Product Owner** — refine the goal, scope, and acceptance intent. Update `PRODUCT.md` if needed.
2. **Moderator + Tech Lead** — validate technical feasibility, update `ARCHITECTURE.md` if needed, write or refine `STEP-XX.md` with scope, inputs, and acceptance checks.
3. **Moderator decision** — confirm `STEP-XX.md` is clear and complete before briefing the Development Team.

**Phase 2 — Implement**

4. **Moderator → Development Team** — provide the context packet (relevant `PRODUCT.md`, `ARCHITECTURE.md`, `DOMAIN-LANGUAGE.md` excerpts) and the active `STEP-XX.md`. Development Team restates the step, proposes a plan, and waits for Moderator approval before writing code.
5. **Development Team** — implements only the approved scope; summarizes changes against the acceptance checks in `STEP-XX.md`.

**Phase 3 — Review and iterate** _(repeat until green)_

6. **Moderator (Workbench)** — pulls changes locally, builds, runs tests, manually exercises the feature. Records findings in `QA.md` and `REVIEW.md`. Minor issues fixed directly; significant issues return to Development Team with explicit feedback.
7. **Tech Lead** — reviews for architectural fit, naming consistency, and maintainability. Classifies findings as must-fix or nice-to-have. Moderator records recommendations in `REVIEW.md`.
8. **Development Team** — addresses each piece of feedback explicitly; adjusts implementation within approved scope.
9. **→ Return to step 6** until all acceptance checks pass and Tech Lead has approved.

**Phase 4 — Accept and advance**

10. **Moderator final gate (HITL)** — confirms all checks pass, `REVIEW.md` and `QA.md` are complete. Creates annotated Git tag. Advances `ROADMAP.md` to the next step.

---

## Canonical documents

| Document             | Purpose                                                      |
| -------------------- | ------------------------------------------------------------ |
| `MOD-W.md`           | This file — workflow quick-reference for the project         |
| `PRODUCT.md`         | What is being built, for whom, and why                       |
| `ARCHITECTURE.md`    | Technical structure, stack, patterns, constraints            |
| `ROADMAP.md`         | Ordered sequence of small, reviewable steps                  |
| `STEP-XX.md`         | Current step — goal, scope, inputs, acceptance checks        |
| `REVIEW.md`          | Review notes and decisions for the current step              |
| `QA.md`              | Verification evidence for the current step                   |
| `DOMAIN-LANGUAGE.md` | Canonical terms used across docs, prompts, and code          |
| `AI_AGENTS.md`       | Agent registry — models, interfaces, data handling decisions |
| `CLAUDE.md`          | Development Team config for Claude Code (lives at repo root) |

All MOD-W docs live under `mod-w/` in the project. `CLAUDE.md` lives at the **repo root** so Claude Code reads it automatically.

---

## Operating rules

- **Documents must earn their existence.** Prefer updating an existing doc over creating a new one.
- **No hidden scope.** Anything not in the current `STEP-XX.md` is out of scope for this step.
- **Explicit out-of-scope.** When something is deferred, state it.
- **Stable naming.** Resolve naming conflicts early; keep `DOMAIN-LANGUAGE.md` current.
- **Pause on ambiguity.** Any role that is unsure stops and clarifies rather than guessing.
- **Lean first, expand later.** Start with `PRODUCT.md`, `ROADMAP.md`, and `STEP-XX.md`; add further docs only when they clearly help.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
