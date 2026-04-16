# Roles in Moderated AI Development Workflow

Moderated AI Development Workflow defines a small set of core roles with clear boundaries and accountability. Some roles may be supported or implemented by AI tools, but the role names remain the same regardless of tool choice.

---

## Human Roles

### Moderator

The Moderator is the primary human-in-the-loop operator of Moderated AI Development Workflow.

The Moderator:

- Orchestrates handoffs between roles and artifacts
- Works in the **Workbench** (e.g., VS Code + Copilot) to build, run, test, debug, and fine‑tune changes
- Reviews each step's AI output against the quality gate criteria
- Records decisions in the [REVIEW.md](../templates/REVIEW.md) and [QA.md](../templates/QA.md) artifacts
- Has authority to reject output, request retries, or adjust scope

On very small teams the Moderator may also be the Tech Lead and/or Product Owner.

### Product Owner

The Product Owner is responsible for defining _what_ is built and _why_.

The Product Owner:

- Authors and maintains the [PRODUCT.md](../templates/PRODUCT.md) artifact
- Sets acceptance intent and criteria for each roadmap step
- Reviews and approves the [ROADMAP.md](../templates/ROADMAP.md) before implementation
- Participates in ceremonies: Kickoff, Step Review, and Retrospective
- Does **not** directly merge code or override quality gates

In one common setup, the Product Owner role is supported by a Claude Code SubAgent for product shaping, user stories, and acceptance validation.

### Tech Lead

The Tech Lead is responsible for _how_ the product is built.

The Tech Lead:

- Iteratively cross-validates the [PRODUCT.md](../templates/PRODUCT.md) artifact with the Product Owner to clarify intent and constraints
- Authors and maintains the [ARCHITECTURE.md](../templates/ARCHITECTURE.md) artifact
- Authors and maintains the [ROADMAP.md](../templates/ROADMAP.md) artifact
- Defines the [DOMAIN_LANGUAGE.md](../templates/DOMAIN_LANGUAGE.md)
- Writes and refines briefs and prompts for AI agents
- Reviews roadmap quality and implementation for technical correctness and maintainability
- Reviews completed steps before they are tagged as done
- Revises output based on Moderator and Product Owner feedback until quality gates are met
- Generates the project-specific `CLAUDE.md` from `ARCHITECTURE.md` and the `CLAUDE.md` template

In one common setup, the Tech Lead role is supported by a Codex full session for architecture thinking, roadmap shaping, step authoring, and technical review.

### Designer

The Designer is responsible for the visual and interaction design of the product.

The Designer:

- Receives `PRODUCT.md`, `ROADMAP.md`, the DOMAIN_LANGUAGE.md, and visual assets (reference images, brand tokens, style descriptions) from the Moderator
- Produces and maintains the `DESIGN-SPEC.md` artifact: colour palette, typography, spacing, component library, screen layouts, interaction patterns, and a Component–Roadmap Map
- Maps every UI component and design decision to the Roadmap Step in which it is first introduced
- Reviews and revises `DESIGN-SPEC.md` based on Product Owner and Moderator feedback until the spec is approved
- Hands the approved `DESIGN-SPEC.md` to the Development Team as a guide for UI implementation
- Does **not** write code or make product scope decisions

In one common setup, the Designer role is supported by Claude for spec generation, visual system definition, and component mapping.

### Development Team

The Development Team is responsible for executing the roadmap steps to build the product.

- Iteratively reviews the [ARCHITECTURE.md](../templates/ARCHITECTURE.md) and [ROADMAP.md](../templates/ROADMAP.md) artifacts with the Tech Lead to understand context and constraints
- Executes the implementation of each step, including code, tests, and documentation
- Revises output based on Moderator and Tech Lead feedback until quality gates are met
- Does **not** directly merge code or override quality gates

**Supported interface:**

| Interface         | Config                               | Best for                                                               |
| ----------------- | ------------------------------------ | ---------------------------------------------------------------------- |
| Claude Code (CLI) | `CLAUDE.md` in repo root, auto-read  | File writing, multi-file changes, direct repo edits, SubAgent spawning |

The active `STEP-XX.md` is provided by the Moderator at session start as a file path. After implementation, the Dev Team session spawns QA and Product Owner SubAgents before handing off to Tech Lead review.

### QA / Tester

The QA role validates that accepted output behaves correctly end‑to‑end.

The QA function is performed by a Claude Code SubAgent spawned by the Dev Team session:

- Reads the implementation and `STEP-XX.md` acceptance checks
- Produces `QA.md` with results, manual check list, and known limitations
- Raises defects if acceptance checks are not met
- Flags checks that require human or browser verification

### Workbench

The Workbench is the human-operated development environment used by the Moderator.

The Workbench:

- Hosts the local clone of the repository (e.g., in VS Code)
- Runs builds, tests, linters, and manual UX checks
- Uses tools like GitHub Copilot for light‑to‑moderate code edits and debugging
- Is the final place where a step must pass before Tech Lead approval and tagging

---

## Default Tool Implementations

All roles use **Claude Code** as the default interface. Full sessions handle complex, multi-step work. SubAgents handle bounded validation tasks.

### Product Owner role — two modes (default)

**Definition phase** (project start, no agent infrastructure yet):

- Moderator uses Claude chatbot to draft and iterate on `PRODUCT.md`
- Moderator uses Perplexity for research and fact-finding
- Moderator uses Gemini for informal cross-validation of scope and goals
- Moderator gates approval before architecture begins

**Validation phase** (per-step, after Tech Lead approval):

- Claude Code SubAgent validates completed Steps against `STEP-XX.md` acceptance checks
- Signs off before Moderator final gate

See: [prompts/product-owner.md](../prompts/product-owner.md)

### Tech Lead role — Codex full session (default)

The Tech Lead session (Codex, reads `AGENTS.md`):

- Generates `ARCHITECTURE.md`, `ROADMAP.md`, and `STEP-XX.md` at planning time
- Generates project-specific `CLAUDE.md` and `AGENTS.md` from `ARCHITECTURE.md` and the MOD-W templates
- Reviews completed Steps and writes `REVIEW.md`

Two session types: **Planning** (writes artifacts) and **Review** (reads diff, writes `REVIEW.md` only).

Cross-validation: Codex plans and reviews; Claude Code implements. Model diversity is intentional.

See: [prompts/tech-lead.md](../prompts/tech-lead.md)

### Designer role — Claude (optional)

Claude may be used to support the Designer role by:

- Analysing `PRODUCT.md`, `ROADMAP.md`, and visual assets to derive a coherent design direction
- Producing `DESIGN-SPEC.md` with colour palette, typography, component library, screen layouts, and interaction patterns
- Mapping UI components to Roadmap Steps so the Development Team knows what to build and when
- Revising the spec based on Product Owner and Moderator feedback

All output is moderated before acceptance.

See: [prompts/additional-roles/designer.md](../prompts/additional-roles/designer.md)

### Development Team role — Claude Code SubAgent (default)

The Dev Team SubAgent (Claude Code, reads `CLAUDE.md`):

- Reads `CLAUDE.md`, `STEP-XX.md`, `ARCHITECTURE.md`, `AGENTS.md`, and `DOMAIN_LANGUAGE.md`
- Enters Plan Mode to confirm scope before writing any files
- Implements the Step with minimal, scoped changes
- Runs blocking build gate before handing off

All output is moderated before acceptance.

See: [templates/CLAUDE.md](../templates/CLAUDE.md)

### QA role — Claude Code SubAgent (default)

The QA SubAgent (Claude Code):

- Spawned after Tech Lead approval
- Reads implementation files and `STEP-XX.md` acceptance checks
- Produces `QA.md` with results, manual check list, and known limitations
- Flags checks requiring human or browser verification

See: [prompts/qa.md](../prompts/qa.md)

---

## Role Summary Table

| Role                    | Human or AI                    | Primary artifacts                                             | Quality gate responsibility               |
| ----------------------- | ------------------------------ | ------------------------------------------------------------- | ----------------------------------------- |
| Moderator               | Human                          | repo state, approvals, git tags                               | Accepts/rejects AI output and step status |
| Product Owner           | Human                          | PRODUCT.md, acceptance intent                                 | Accepts/rejects step scope and intent     |
| Tech Lead               | Human                          | ARCHITECTURE.md, ROADMAP.md, STEP.md, CLAUDE.md               | Reviews technical quality and fit         |
| QA / Tester             | Human                          | QA.md (final sign-off)                                        | Validates end‑to‑end behaviour            |
| Workbench               | Human env.                     | Local repo, build/test tooling                                | Executes builds/tests, manual checks      |
| Product Owner Agent (Definition)  | Claude chatbot + Perplexity + Gemini | PRODUCT.md                                                    | None — all output is moderated            |
| Product Owner Agent (Validation)  | AI (Claude Code SubAgent)            | acceptance sign-off                                           | None — all output is moderated            |
| Tech Lead Agent                   | AI (Codex full session)              | ARCHITECTURE.md, ROADMAP.md, STEP-XX.md, CLAUDE.md, REVIEW.md | None — all output is moderated            |
| Development Team Agent            | AI (Claude Code SubAgent)            | Code, tests, docs for each step                               | None — all output is moderated            |
| QA Agent                          | AI (Claude Code SubAgent)            | QA.md                                                         | None — all output is moderated            |
| ----------------------- | ------------------------------ | ------------------------------------------------------------- | ----------------------------------------- |
| Extended (optional):    |                                |                                                               |                                           |
| Designer                | Human                          | DESIGN-SPEC.md                                                | Reviews visual quality and fit            |
| Designer Agent          | AI (Claude)                    | DESIGN-SPEC.md drafts, component mapping                      | None — all output is moderated            |

---

MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
