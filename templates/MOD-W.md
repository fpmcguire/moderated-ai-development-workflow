# Moderated AI Development Workflow (MOD-W)

MOD-W is a role-driven, document-centered workflow for AI-assisted software development. It separates product, design, technical, and implementation decisions across distinct roles, enforces cross-validation between multiple AI agents and models, and requires a human Moderator to approve every step before it is accepted. The result is small, reviewable, traceable increments — viable coding, not vibe coding.

Full methodology reference: https://github.com/fpmcguire/moderated-ai-development-workflow

---

## Roles

| Role                          | Owns                                                               | AI agent (default)                                  |
| ----------------------------- | ------------------------------------------------------------------ | --------------------------------------------------- |
| **Moderator**                 | Workflow orchestration, go/no-go authority, HITL gate              | Human only                                          |
| **Product Owner**             | What and why — `PRODUCT.md`, acceptance intent                     | ChatGPT or Claude chatbot                           |
| **Designer + Prototyper**     | Visual identity, prototype, advisory architecture notes            | **Claude Design** (project-scoped browser env)      |
| **Tech Lead**                 | How — `ARCHITECTURE.md`, `ROADMAP.md`, step design, tech review    | Codex (via `AGENTS.md` at repo root)                |
| **Development Team**          | Implementation — code, tests, docs for each step                   | Claude Code (default) or Claude Design (visual Steps) |
| **QA / Tester**               | End-to-end verification — `QA.md`                                  | Claude Code SubAgent                                |

The Designer + Prototyper role is **new in v4.0.0**. It is optional per project and runs during Project Kickoff to produce a working prototype + design spec before architecture is defined. See §"Prototype Ceremony".

---

## Cross-validation

The key differentiator in MOD-W is **intentional role and model diversity**. No single agent both plans and implements. No single agent both implements and reviews.

```
Product Owner (ChatGPT)                            →  defines what and why
       ↓ cross-checks
Designer + Prototyper (Claude Design) [optional]   →  produces DESIGN-SPEC.md + prototype + ARCHITECTURE-NOTES.md
       ↓ cross-checks (Architecture Handoff)
Tech Lead (Codex)                                  →  authors ARCHITECTURE.md, ROADMAP.md, STEP-XX.md; reviews Dev Team output
       ↓ cross-checks
Development Team (Claude Code | Claude Design)     →  implements only the approved Step
       ↓ cross-checks
Moderator (human)                                  →  reconciles all four; has final authority
```

Each handoff is a validation surface. Using different models for different roles prevents any single model's blind spots from propagating unchecked. The single most-protected boundary is **Tech Lead → Development Team**: Codex always plans; a different model always implements.

---

## Workflow — role sequence per project

The Moderator is always the human gate. Phases iterate until acceptance is met.

### Phase 0 — Project Kickoff (once)

0a. **Moderator + Product Owner** — produce approved `PRODUCT.md`.

0b. **Prototype Ceremony (optional, Moderator's decision)** — Moderator + Designer + Prototyper (Claude Design) produce:
- `DESIGN-SPEC.md` (authoritative)
- `prototype/` folder (research artifact)
- `ARCHITECTURE-NOTES.md` (advisory)

Run the ceremony when the product has novel interaction models, real-time data, or unusual visual systems. Skip it for CRUD apps, headless services, and projects where the visual layer is conventional. See `docs/prototype-ceremony.md`.

0c. **Architecture Handoff (mandatory if 0b ran)** — Moderator + Tech Lead (Codex) consume PRODUCT.md + DESIGN-SPEC.md + prototype/ + ARCHITECTURE-NOTES.md and **independently author** `ARCHITECTURE.md`, `ROADMAP.md`, `CLAUDE.md`, `AGENTS.md`, and the first `STEP-XX.md`. Codex has authority to override structures implied by the prototype. Material divergences are recorded in `ARCHITECTURE.md §"Decisions That Diverge From Prototype"`. See `docs/architecture-handoff.md`.

### Phase 1 — Define the Step

1a. **Tech Lead (Codex)** writes or refines `STEP-XX.md` with scope, inputs, acceptance checks, and (when applicable) the assigned Dev Team interface and Reference Implementation disposition.

1b. **Moderator decision** — confirm `STEP-XX.md` is clear and complete before briefing the Development Team.

### Phase 2 — Implement

2a. **Moderator → Development Team** — provides the context packet (relevant `PRODUCT.md`, `ARCHITECTURE.md`, `DOMAIN_LANGUAGE.md` excerpts) and the active `STEP-XX.md`. Dev Team restates the step, proposes a plan, and waits for Moderator approval before writing code.

2b. **Development Team** implements the approved scope only and runs the blocking build gate (`{{BUILD_COMMAND}}` + `{{TEST_COMMAND}}`).

### Phase 3 — Review and iterate (repeat until green)

3a. **Tech Lead (Codex)** reviews the diff for architectural fit, naming consistency, scope compliance, and maintainability. Writes `REVIEW.md`. Sends rework directly to Dev Team if needed.

3b. **QA SubAgent** validates against acceptance checks; writes `QA.md`.

3c. **Product Owner SubAgent** confirms acceptance intent; writes sign-off.

3d. **Development Team** addresses each finding explicitly. Return to 3a until green.

### Phase 4 — Accept and advance

4a. **Moderator final gate (HITL)** — confirms all checks pass, `REVIEW.md` and `QA.md` are complete, manually exercises the feature.

4b. **Moderator** creates annotated Git tag and advances `ROADMAP.md`.

---

## Canonical documents

| Document                      | Owner              | Purpose                                                                          |
| ----------------------------- | ------------------ | -------------------------------------------------------------------------------- |
| `MOD-W.md`                    | Moderator          | This file — workflow quick-reference for the project                             |
| `PRODUCT.md`                  | Product Owner      | What is being built, for whom, and why                                           |
| `DESIGN-SPEC.md`              | Designer + Prototyper | Visual identity, components, screens, interactions (v4)                       |
| `ARCHITECTURE-NOTES.md`       | Designer + Prototyper | **Advisory** — observations from prototyping for Tech Lead (v4)               |
| `ARCHITECTURE.md`             | Tech Lead          | Authoritative technical structure, stack, patterns, constraints                  |
| `ROADMAP.md`                  | Tech Lead          | Ordered sequence of small, reviewable steps                                      |
| `STEP-XX.md`                  | Tech Lead          | Current step — goal, scope, inputs, acceptance checks                            |
| `REVIEW.md`                   | Tech Lead          | Review notes and decisions for the current step                                  |
| `QA.md`                       | QA / Tester        | Verification evidence for the current step                                       |
| `DOMAIN_LANGUAGE.md`          | Tech Lead          | Canonical terms used across docs, prompts, and code                              |
| `AI_AGENTS.md`                | Moderator          | Agent registry — models, interfaces, data handling decisions                     |
| `CLAUDE.md` (repo root)       | Tech Lead          | Dev Team config for Claude Code                                                  |
| `AGENTS.md` (repo root)       | Tech Lead          | Tech Lead config for Codex                                                       |

All MOD-W docs live under `mod-w/` in the project. `CLAUDE.md` and `AGENTS.md` live at the **repo root** so the CLI agents read them automatically. The `prototype/` folder (v4) lives at the repo root and is explicitly marked as a research artifact via `prototype/README.md`.

---

## Operating rules

- **Documents must earn their existence.** Prefer updating an existing doc over creating a new one.
- **No hidden scope.** Anything not in the current `STEP-XX.md` is out of scope for this step.
- **Explicit out-of-scope.** When something is deferred, state it.
- **Stable naming.** Resolve naming conflicts early; keep `DOMAIN_LANGUAGE.md` current.
- **Pause on ambiguity.** Any role that is unsure stops and clarifies rather than guessing.
- **Lean first, expand later.** Start with `PRODUCT.md`, `ROADMAP.md`, and `STEP-XX.md`; add further docs only when they clearly help.
- **No retroactive gates.** Work produced outside an approved gate is **reference material only**, never adopted as authoritative without re-running the gate from scratch.
- **Single-role-per-session.** A session is started with exactly one role prompt. Mid-session role switching is prohibited.
- **Architecture is authored by Codex, never by Claude Design.** This is the v4 non-negotiable.

---

MOD-W v4.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
