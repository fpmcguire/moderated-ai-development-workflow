# MOD-W: Moderated AI Development Workflow

Human-moderated workflow for AI-assisted software development

> **Disclaimer**
>
> MOD-W (Moderated AI Development Workflow) is not an AI agent automation framework. It is a disciplined, human-in-the-loop workflow for AI-assisted software development that optimizes for quality, traceability, and maintainability.
>
> This project leads with the full name Moderated AI Development Workflow and the shorthand MOD-W to distinguish itself from manifest-driven or autonomous agent runners.
>
> You can think of Moderated AI Development Workflow as: role-based workflow + Spec-Driven Development (SDD) + AI cross-validation + human-in-the-loop (HITL) moderation.

### A Note on Naming (v1.0.0 Update)

To ensure clarity and avoid confusion with other "MAID" projects in the AI space, this methodology has officially rebranded from MAID to MOD-W (Moderated AI Development Workflow). The new shorthand more accurately reflects our focus on the Moderator role and the disciplined Workflow required for viable coding.

## This is not "vibe coding." It is a disciplined form of viable coding.

Vibe coding is useful for quick experiments, but it collapses product, design, architecture, and implementation into one blurry chat. Moderated AI Development Workflow turns AI-assisted work into viable coding: small, reviewable steps, explicit roles, clear artifacts, and non-negotiable human quality gates.

Moderated AI Development Workflow is a spec-driven workflow that improves quality through separated roles, cross-validation, and explicit human oversight.  
The core roles are **Product Owner**, **Tech Lead**, **Development Team**, and **Moderator**. These roles may be supported by AI tools such as ChatGPT, Claude, Perplexity, Gemini, and Copilot, while the human **Moderator** works in a local **Workbench** (e.g., VS Code + Copilot) to control context, review outputs, run builds and tests, and approve each step through explicit quality gates.

A key aspect of Moderated AI Development Workflow is the intentional separation and diversity of roles and AI tooling to ensure role and agent cross-validation, accountability, and quality.

Version 2.0.0 defines a **minimal role set** for most teams. Example projects (such as the "Frontend Saved Views" example) show how teams can add **extended roles** like CUSTOMER and PRODUCT DESIGNER for deeper cross-validation when needed.

---

## Why Moderated AI Development Workflow?

Most AI coding setups optimize for speed and "let the model code everything." That often leads to:

- large, opaque AI code dumps
- missing validation, logging, and edge cases
- no clear record of why decisions were made

Moderated AI Development Workflow optimizes for:

- **Maintainability** – clean architecture, small verified steps, and up‑to‑date docs instead of giant, opaque AI code dumps.
- **Traceability** – every step has artifacts, reviews, QA notes, and annotated Git tags so you can see what changed, why, and by whom.
- **Human control** – clear ownership for product, architecture, and quality, with AI tools supporting defined roles rather than acting as autonomous committers.
- **Multi‑layer validation** – every change is checked by the Workbench, the Moderator, and the Tech Lead (and QA when needed) before it is accepted.

Modern AI development is converging on three ideas:

- **Spec‑Driven Development (SDD)** – specs and plans as the source of truth.
- **Viable coding (not vibe coding)** – structured, reviewable, production‑safe workflows instead of prompt‑and‑pray coding.
- **Blue‑red / multi‑agent patterns** – clearly separated "plan/implement" (blue) and "review/verify" (red) duties.

Moderated AI Development Workflow sits at the intersection of these trends: it applies spec‑driven discipline to AI‑assisted work, uses explicit roles and model contrast instead of a single all‑knowing agent, and bakes planning and review into every Step.

---

## Core Roles

Moderated AI Development Workflow defines a minimal set of core roles:

- **Moderator** – human operator who orchestrates handoffs, works in the Workbench, validates builds/tests/UX, and controls quality gates.
- **Product Owner** – defines _what_ is built and _why_, maintains `PRODUCT.md`, and sets acceptance intent.
- **Tech Lead** – defines _how_ the product is built, maintains `ARCHITECTURE.md`, shapes the roadmap, and reviews technical quality.
- **Development Team** – generates roadmap proposals, code, tests, and docs for each step, always under moderation. Supports two interfaces: the **Claude chatbot** (claude.ai, using `development-team-claude.md`) and **Claude Code** (CLI, using `CLAUDE.md` at the repo root). Both may be used within the same Step.
- **QA / Tester** – validates that accepted output behaves correctly end‑to‑end (may be the Moderator on small teams).
- **Workbench** – local environment where the Moderator builds, runs, tests, debugs, and fine‑tunes changes before they pass any gate.

See: `docs/roles.md` for full role definitions.

### Extended roles (optional)

Projects can introduce additional cross‑validation roles where useful. Common examples include:

- **Customer** – provides real problems, goals, language, and feedback from the field.
- **Product** – translates customer insights into flows, UX, and interaction patterns.
- **Marketing / Go‑to‑Market** – validates positioning, messaging, and surface alignment.

These extended roles are **optional** in Moderated AI Development Workflow. The core workflow and quality gates can function with just the minimal role set. Extended roles are for teams that want deeper cross-validation and more perspectives in the process.

---

## Step‑by‑step Workflow (High Level)

Each feature or change is delivered through small, traceable **Steps**:

1. **Product shaping** – Moderator + Product Owner refine the idea into `PRODUCT.md`.
2. **Architecture decision** – Moderator + Tech Lead capture direction in `ARCHITECTURE.md`.
3. **Roadmap** – Tech Lead and Development Team create `ROADMAP.md` as an ordered set of Steps.
4. **Implement a Step** – Development Team implements a single Step guided by `STEP.md`.
5. **Workbench verification** – Moderator pulls changes locally, builds, runs tests, and checks UX.
6. **Revision loop** – Issues go back to the Development Team with comments until green.
7. **Tech Lead review** – Tech Lead reviews the Step for correctness and maintainability. Issues iterate to the Development Team until green.
8. **QA + tag** – Moderator/QA records results in `QA.md` and creates an annotated Git tag for the Step.

In practice, this implements a **blue‑red pattern**: Tech Lead and Development Team plan and implement (blue), while Tech Lead and Moderator review and verify (red), before any change is accepted.

---

## The MOD-W Prompting Guide (Critical)

The flow of communication is the engine of this workflow. To ensure high-integrity results, we follow a strict protocol centered on **Options, Ramifications, and Mentorship**. This guide is essential for all roles, regardless of the AI engine used.
**[Read the prompt-guidelines.md](./prompts/prompt-guidelines.md)**

---

## Using MOD-W with Gemini

Gemini users can leverage **Gems** for role separation and **NotebookLM** as a persistent project archive grounded in your specific documentation.
**[See the Gemini Integration Guide here](./articles/modw-with-gemini.md)**

---

## Using Moderated AI Development Workflow with Claude Code

Claude Code is Anthropic's CLI coding agent. It runs in your terminal with direct
access to your local repository, eliminating the copy-paste step that the chatbot
workflow requires. In MOD-W terms, Claude Code is an alternative interface for the
**Development Team** role — same model, same role rules, direct file writes.

### Where Claude Code fits

Claude Code replaces the copy-paste leg of the Development Team workflow:

- The Moderator no longer needs to manually apply file changes from the chatbot.
- Claude Code reads the full repo at session start, so context is always current.
- The Moderator reviews diffs in VS Code before committing — the human gate is preserved.

Claude Code does **not** replace the Tech Lead, Product Owner, or Moderator roles.
MOD-W's cross-validation and human-in-the-loop discipline apply equally regardless
of which Development Team interface is used.

### Setup

1. Place `CLAUDE.md` at the repo root. This is the Claude Code equivalent of
   `development-team-claude.md`. Claude Code reads it automatically at session start.
2. Generate `CLAUDE.md` using the Tech Lead: provide the project's `ARCHITECTURE.md`,
   `DOMAIN-LANGUAGE.md`, and the `CLAUDE.md` template. The Tech Lead fills in all
   placeholders and removes template comments.
3. Start a Claude Code session in the project root. The Development Team role context
   is loaded automatically — no paste required.

### Switching between chatbot and Claude Code within a Step

You may switch interfaces mid-Step. The recommended pattern:

| Phase                     | Interface      | Why                               |
| ------------------------- | -------------- | --------------------------------- |
| Planning and confirmation | Claude chatbot | Conversational back-and-forth     |
| Multi-file implementation | Claude Code    | Direct repo writes, no copy-paste |
| Revision discussion       | Claude chatbot | Easier to discuss findings        |

**Rule:** Commit the repo before switching so Claude Code reads the current file state.

### Responsibility split

- **Claude Code owns:** reading repo files, proposing and writing file changes,
  running commands the Moderator approves.
- **MOD-W owns:** Moderator go/no-go authority, Tech Lead review, step-scoped
  implementation discipline, quality gates.

### Bottom line

Claude Code removes friction from the Development Team workflow.
It does not change the MOD-W roles, review model, or quality gates.
Use `CLAUDE.md` for Claude Code. Use `development-team-claude.md` for the chatbot.
Both encode the same role and may be used on the same project and the same Step.

---

## Using Moderated AI Development Workflow with Kiro

Moderated AI Development Workflow is a governance and workflow methodology that can sit on top of spec‑driven IDEs like **Kiro**.  
Kiro provides the spec‑driven editor/runtime, and Moderated AI Development Workflow provides the roles, moderation, and cross‑review discipline.

### Responsibility split

- **Kiro owns:**
  - creating and editing Requirements / Design / Tasks specs
  - running and tracking spec‑driven tasks inside the IDE
  - integrating tools, MCPs, and execution controls

- **Moderated AI Development Workflow owns:**
  - Moderator authority and go/no‑go decisions
  - separation of Product Owner, Tech Lead, and Development Team roles
  - intentional role/agent/model contrast (e.g., different models per role)
  - cross‑role / cross‑agent verification before acceptance
  - step‑based delivery and acceptance criteria aligned with ROADMAP and STEP docs

### Document and phase mapping

When using Moderated AI Development Workflow with Kiro, map Moderated AI Development Workflow's docs to Kiro's spec phases:

- **Requirements (Kiro)** ↔ `PRODUCT.md`  
  High‑level product problem, users, goals, requirements, and product‑level acceptance criteria.

- **Design (Kiro)** ↔ `ARCHITECTURE.md`  
  Technical approach, architecture decisions, data model, integration points, constraints.

- **Tasks (Kiro)** ↔ `ROADMAP.md` + `STEP-XX.md`  
  Roadmap of steps and task‑level specs: context, scope, inputs, expected outputs, and step‑level acceptance criteria.

Other Moderated AI Development Workflow docs (e.g., `DOMAIN_LANGUAGE.md`, `AGENTS.md`, workbench guidelines) can be treated as **Steering Docs** and referenced from Kiro specs as part of the context.

### Moderator and approvals

In a Kiro + Moderated AI Development Workflow setup:

- The **Moderator** decides when Requirements or Design specs are "approved enough" to move forward.
- The Moderator also decides when a Task/STEP is complete after review and testing, regardless of what Kiro's task status says.
- Teams should treat Kiro's phase transitions (Requirements → Design → Tasks) as **subject to Moderator approval**, not just IDE actions.

Kiro provides the spec‑driven SDD engine, and Moderated AI Development Workflow provides the human‑in‑the‑loop governance and multi‑agent role pattern around it.

---

## Using Moderated AI Development Workflow with GitHub Spec Kit

GitHub Spec Kit is an open‑source toolkit for **Spec‑Driven Development (SDD)** that helps you capture constitutions, specs, technical plans, and tasks in your repo, then drive AI‑assisted implementation from those artifacts.  
Moderated AI Development Workflow layers on top of this: Spec Kit provides the SDD scaffolding, and Moderated AI Development Workflow provides roles, moderation, and cross‑validation.

### Responsibility split

- **Spec Kit owns:**
  - initializing SDD scaffolding (constitution, spec, plan, tasks)
  - generating and refining:
    - constitution (project principles and constraints)
    - spec (what to build, user needs, requirements)
    - plan (technical implementation plan)
    - tasks (task breakdown for implementation)
  - integrating with coding agents (e.g., Copilot, Claude Code) to implement those tasks

- **Moderated AI Development Workflow owns:**
  - defining who is Product Owner, Tech Lead, Development Team, and Moderator
  - deciding who approves constitution, spec, plan, and tasks before they are treated as canonical
  - introducing intentional role/agent/model contrast (e.g., different models or configs for spec, plan, and implementation)
  - requiring cross‑review (human and/or cross‑agent) before accepting generated plans, tasks, and code
  - enforcing step‑based delivery and acceptance criteria aligned with the roadmap and step docs

### Document and phase mapping

When using Moderated AI Development Workflow with Spec Kit, map Moderated AI Development Workflow's docs to Spec Kit's phases:

- **Constitution (Spec Kit)** ↔ Moderated AI Development Workflow principles & steering docs  
  Spec Kit's constitution maps to project‑wide principles and is complemented by Moderated AI Development Workflow steering docs such as `DOMAIN_LANGUAGE.md`, `AGENTS.md`, and any Moderated AI Development Workflow‑specific rules the Moderator enforces.

- **Spec (Spec Kit)** ↔ `PRODUCT.md`  
  Functional problem, users, goals, requirements, and product‑level acceptance criteria.

- **Plan (Spec Kit)** ↔ `ARCHITECTURE.md`  
  Technical approach, stack, architecture decisions, data model, integration points, constraints.

- **Tasks (Spec Kit)** ↔ `ROADMAP.md` + `STEP-XX.md`  
  Task breakdown and sequencing correspond to Moderated AI Development Workflow's roadmap and per‑step templates (context, scope, inputs, expected outputs, and step‑level acceptance criteria).

Moderated AI Development Workflow's `REVIEW.md` and `QA.md` sit on top of these phases to structure human and cross‑agent evaluation of each step.

### Moderator and approval flow

With Spec Kit + Moderated AI Development Workflow:

- The **Moderator** decides when:
  - a constitution is strong enough to drive spec work
  - a spec is clear enough to move into planning
  - a plan is coherent enough to generate tasks
  - tasks and resulting implementation satisfy the acceptance criteria in `PRODUCT.md` and `STEP-XX.md`

- Spec Kit's commands and phases should be treated as **subject to Moderator approval**, not self‑ratifying.
- Moderated AI Development Workflow encourages using different roles/agents/models for spec, plan, and implementation and adding at least one cross‑agent review step before the Moderator accepts a phase.

Spec Kit provides the spec‑driven SDD engine, and Moderated AI Development Workflow provides the human‑in‑the‑loop governance and multi‑agent role pattern around that engine.

---

## Using Moderated AI Development Workflow with Cursor

Cursor is a strong **workbench** for Moderated AI Development Workflow.

It does not define the workflow for you, but it provides useful building blocks for running a spec-driven, human-moderated process: planning, agent assistance, project rules, shared documentation context, and iterative implementation.

### Where Cursor fits

In Moderated AI Development Workflow, Cursor works best as the environment where the **Moderator** and **Development Team**:

- review and refine plans
- inspect and edit code
- run builds, tests, and linters
- enforce project rules and workflow constraints
- iterate on implementation with explicit human approval

### Recommended way to use Cursor in this workflow

Use Cursor as the implementation and review workbench, not as the methodology itself.

A practical pattern is:

1. Define intent and acceptance criteria outside the coding chat, using your normal product and technical artifacts.
2. Use Cursor to turn those artifacts into an implementation plan.
3. Review and edit the plan before any significant code generation.
4. Implement in small, reviewable steps.
5. Run tests, linters, and other checks locally.
6. Require explicit human acceptance before merging or continuing.

### Useful Cursor capabilities for this workflow

- **Plan-first workflow** for turning requirements into a reviewable implementation plan
- **Agent assistance** for codebase research, implementation, refactoring, and debugging
- **Rules** for encoding project conventions, constraints, and working agreements
- **Documentation context** so the agent can work against project docs and technical references
- **CLI and automation support** for teams that want the same rules and workflow outside the editor

### Recommended setup

For a Moderated AI Development Workflow project in Cursor, keep these elements lightweight but explicit:

- a project rules file or rules directory that encodes coding standards and workflow guardrails
- a small set of source artifacts such as goals, scope, constraints, acceptance criteria, and technical notes
- a clear review habit: plan first, implement second, validate third
- human ownership of acceptance decisions

### Suggested operating model

- **Product Owner** defines the goal, scope, and acceptance criteria
- **Tech Lead** shapes the implementation approach and constraints
- **Development Team** uses Cursor to research, implement, and refine
- **Moderator** reviews outputs, preserves context discipline, runs validation, and approves progression through quality gates

### Bottom line

Cursor is not a substitute for Moderated AI Development Workflow.  
It is a capable environment for running it well.

Use Cursor for planning, implementation, and iteration.  
Use Moderated AI Development Workflow for role separation, governance, review, and accountability.

---

## Repository Layout

- `docs/` – methodology reference (manifesto, roles, lifecycle, artifacts, domain language, etc.)
- `templates/` – reusable templates for `PRODUCT.md`, `ARCHITECTURE.md`, `ROADMAP.md`, `STEP.md`, `REVIEW.md`, `QA.md`, `DOMAIN_LANGUAGE.md`, `AGENTS.md`, and `CLAUDE.md`
- `prompts/` – role prompts for Product Owner, Tech Lead, Development Team, Moderator, and Workbench usage. They support per‑request answer depths (`minimal`, `options`, `full`) so Moderators can choose between speed, choice, and depth without changing tools. Includes `CLAUDE.md` — the Development Team prompt config for Claude Code, generated by the Tech Lead from the project's `ARCHITECTURE.md`.
- `examples/` – concrete examples of Moderated AI Development Workflow in action (starting with a small frontend "saved views" feature)

### Example project structure

The `examples/` directory shows how Moderated AI Development Workflow artifacts and code can live together in a real project.

A typical Moderated AI Development Workflow‑enabled project might look like:

```text
my-saas-app/
  CLAUDE.md                     # Claude Code config for the Development Team role (auto-read by Claude Code)
  mod-w/
    MOD-W.md                    # The workflow and process docs
    AGENTS.md                   # Agent definitions and guidelines
    PRODUCT.md                  # What and why for this product
    ARCHITECTURE.md             # How the system is structured
    ROADMAP.md                  # Ordered list of Steps
    STEP-XX.md                  # Current Step brief
    REVIEW.md                   # Review notes and decisions for the current Step
    QA.md                       # Verification evidence for the current Step
    DOMAIN_LANGUAGE.md   # Shared vocabulary for the product's domain
    (Optional) Other supporting docs, only when they earn their existence.
  src/                          # Application code
    ...
  tests/                        # Automated tests
    ...
```

---

## Minimal vs extended docs

To get started with Moderated AI Development Workflow, you only need a small subset of the docs:

- **Minimal Moderated AI Development Workflow set (recommended first):**
  - `docs/manifesto.md` – why Moderated AI Development Workflow exists and the core beliefs.
  - `docs/principles.md` – day‑to‑day principles.
  - `docs/roles.md` – role definitions and responsibilities.
  - `docs/moderator-checklist.md` – the Moderator's go/no‑go checklist for accepting work.
  - `docs/step-lifecycle.md` – end‑to‑end Step workflow.
  - `docs/artifacts.md` – what lives in PRODUCT / ARCHITECTURE / ROADMAP / STEP / REVIEW / QA.

- **Extended references (use as needed):**
  - `docs/quality-gates.md` – detailed quality gate levels.
  - `docs/ceremonies.md` – Moderated AI Development Workflow ceremonies.
  - `docs/domain-language.md` – domain language and the Domain Language .
  - `docs/glossary.md` – terminology.
  - `docs/faq.md` – common questions.

---

## Core Moderated AI Development Workflow docs

- `docs/manifesto.md` – why Moderated AI Development Workflow exists and the core principles.
- `docs/roles.md` – role definitions and responsibilities.
- `docs/lifecycle.md` – step‑by‑step workflow.

---

## Status:

**MOD-W** has transitioned from a personal workflow into a formalized, open methodology.

- **Current State:** The core methodology, role definitions, and document templates are stabilized.
- **Claude Code support:** `CLAUDE.md` template and Claude Code integration are included in v1.1.0. The Development Team role now supports both the Claude chatbot and Claude Code as interchangeable interfaces.
- For both interfaces, the Moderator provides the active `STEP-XX.md`
  at session start — attached or pasted in the chatbot, or stated as
  a file path in Claude Code.
- **Examples Included:** A reference implementation for a **Frontend Saved Views** feature is available in `/examples/frontend-saved-views`, demonstrating the full lifecycle from `PRODUCT.md` to annotated Git tags.

- **Roadmap:** Future updates will introduce specific profiles for backend services, full-stack integration, and advanced AI runners such as Aider.

---

## How to Use This Repo

1. Read `docs/manifesto.md` and `docs/roles.md`.
2. Copy the templates from `/templates` into your own project.
3. Use the role prompts in `/prompts` to create one dedicated thread per Moderated AI Development Workflow role
   (Product Owner, Tech Lead, Development Team, Moderator/Workbench), and adapt them to your ChatGPT / Claude / Perplexity / Gemini setup.
   - For the **Development Team** role, choose your interface:
     - **Claude chatbot** — paste `development-team-claude.md` at the start of a new claude.ai thread.
     - **Claude Code** — place the generated `CLAUDE.md` at the repo root; it is read automatically at session start.
     - Both may be used on the same project or the same Step. Commit the repo before switching interfaces.
   - When prompting, specify the desired answer depth (`minimal`, `options`, or `full`) so you can trade off speed, optionality, and learning depth per request.
4. Run one small feature end‑to‑end using the Moderated AI Development Workflow Step lifecycle.

Contributions, feedback, and adoption stories are welcome – see `CONTRIBUTING.md`.

---

## License

This project is licensed under the Apache License, Version 2.0 – see the `LICENSE` file for details.

---

## Support and Training

If you are adopting Moderated AI Development Workflow in a team or client environment and want help with setup, training, or tailoring the workflow to your stack, consulting is available.

- Moderated AI Development Workflow setup and rollout coaching
- Team training on roles, documents, and review discipline
- Help customizing templates and prompt packs
- Review of your first Moderated AI Development Workflow‑guided feature

For inquiries, open an issue or contact the maintainer via the repository profile or at fpmcguire@gmail.com.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
