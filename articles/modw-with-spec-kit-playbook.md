# Moderated AI Development Workflow + GitHub Spec Kit Playbook

## Overview

**GitHub Spec Kit** is an open‑source toolkit for **Spec‑Driven Development (SDD)**. It helps you capture a project constitution, spec, plan, and tasks in your repo, then drive AI‑assisted implementation from those artifacts.

**Moderated AI Development Workflow** is a governance and workflow layer that adds roles, artifacts, and human moderation on top of any spec‑driven engine.

Spec Kit answers:

> “How do I create and evolve specs, plans, and tasks inside my repo?”

Moderated AI Development Workflow answers:

> “Who owns which decisions, how are AI outputs reviewed, and when is a change actually accepted?”

This playbook shows how to combine them:

- how Spec Kit’s constitution / spec / plan / tasks map to Moderated AI Development Workflow artifacts
- how Moderated AI Development Workflow roles sit around Spec Kit’s CLI and commands
- a practical checklist to run your **first Moderated AI Development Workflow Step with Spec Kit**

---

## Conceptual mapping

Spec Kit works with four main phases:

- **Constitution** – principles, constraints, and project‑wide rules
- **Spec** – what to build: user needs, requirements, acceptance intent
- **Plan** – how to build it: technical approach and sequencing
- **Tasks** – concrete units of work for implementation

Moderated AI Development Workflow ^(MOD-W) uses these core artifacts:

- `PRODUCT.md` – product problem, users, goals, requirements
- `ARCHITECTURE.md` – technical approach, architecture decisions
- `ROADMAP.md` + `STEP-XX.md` – ordered Steps and per‑Step briefs
- `REVIEW.md` + `QA.md` – review decisions and verification evidence
- `DOMAIN_LANGUAGE_MATRIX.md` + `AGENTS.md` – steering docs for humans and agents

The mapping is:

| Spec Kit phase | MOD-W artifact(s)                                                                        | Purpose                                 |
| -------------- | ---------------------------------------------------------------------------------------- | --------------------------------------- |
| Constitution   | MOD-W principles & steering docs (`docs/*.md`, `AGENTS.md`, `DOMAIN_LANGUAGE_MATRIX.md`) | Project‑wide rules and constraints      |
| Spec           | `PRODUCT.md`                                                                             | What we’re building and why             |
| Plan           | `ARCHITECTURE.md`                                                                        | How we’re building it                   |
| Tasks          | `ROADMAP.md` + `STEP-XX.md`                                                              | Concrete, bounded units of work (Steps) |

MOD-W then layers review and evidence on top of Spec Kit’s flow:

- `REVIEW.md` – why a Step was accepted or rejected
- `QA.md` – how we verified behavior in reality

---

## Roles in a Moderated AI Development Workflow + Spec Kit setup

In a Spec Kit + Moderated AI Development Workflow project, the roles line up like this:

- **Product Owner**
  - Owns the **Spec** phase.
  - Writes and refines the Spec with Spec Kit, then ensures it is reflected in `PRODUCT.md`.
  - Decides when the Spec is “clear enough” to move into planning.

- **Tech Lead**
  - Owns the **Plan** phase.
  - Collaborates with Spec Kit to create the Plan, then keeps it in sync with `ARCHITECTURE.md`.
  - Translates Spec → Plan → Tasks/Steps in a way that supports small, verifiable units.

- **Development Team**
  - Works primarily in the **Tasks** phase.
  - Uses Spec Kit tasks to structure work and drive AI‑assisted implementation (e.g., via Copilot, Claude Code).
  - Treats each Task as one Moderated AI Development Workflow Step or sub‑work within a Step.

- **Moderator**
  - Treats Spec Kit commands and phase changes as **proposals**, not final truth.
  - Ensures that:
    - constitution/spec/plan/tasks are acceptable from Moderated AI Development Workflow’s perspective,
    - each Task’s implementation passes Workbench checks (build/test/UX),
    - `REVIEW.md` and `QA.md` are updated for each Step.
  - Has final say on whether a Step is accepted and tagged.

The central rule: **Spec Kit drives structure; Moderated AI Development Workflow decides when each phase and task is good enough to move on.**

---

## Phase-by-phase playbook

### 1. Constitution ↔ Moderated AI Development Workflow steering docs

**Goal:** Make the project’s principles and rules explicit.

- In Spec Kit:
  - Initialize a constitution with Spec Kit’s CLI (e.g., `speckit init` or equivalent).
  - Capture project‑wide principles, constraints, and non‑negotiables.

- In Moderated AI Development Workflow:
  - Complement the constitution with:
    - `docs/manifesto.md` and `docs/principles.md` – Moderated AI Development Workflow’s own beliefs and day‑to‑day rules.
    - `DOMAIN_LANGUAGE_MATRIX.md` – shared vocabulary.
    - `AGENTS.md` – rules, commands, and limits for AI agents.

**Gate:** The Moderator and Tech Lead decide that the constitution + Moderated AI Development Workflow steering docs are strong enough to guide Specs and Plans.  
Spec Kit’s constitution is **not self‑ratifying**; Moderated AI Development Workflow requires explicit human agreement.

### 2. Spec ↔ PRODUCT.md

**Goal:** Describe the product problem, users, and requirements clearly.

- In Spec Kit:
  - Use the Spec phase to define:
    - target users and their goals,
    - functional and non‑functional requirements,
    - high‑level acceptance intent.

- In Moderated AI Development Workflow:
  - The Product Owner owns `PRODUCT.md` in the repo.
  - Sync Spec Kit’s Spec into `PRODUCT.md`:
    - keep it human‑readable,
    - ensure alignment with any Customer / Product Designer input (if you use those extended roles),
    - capture out‑of‑scope items explicitly.

**Gate:** The Moderator checks that:

- requirements are clear and testable,
- constraints are explicit,
- there is enough information to design a coherent Plan / ARCHITECTURE.

Only then do you move to Spec Kit’s Plan phase.

### 3. Plan ↔ ARCHITECTURE.md

**Goal:** Decide on a technical approach that supports small, safe Steps.

- In Spec Kit:
  - Use the Plan phase to outline:
    - architecture choices,
    - key components and boundaries,
    - data models and integration points,
    - sequencing of work.

- In Moderated AI Development Workflow:
  - The Tech Lead owns `ARCHITECTURE.md`.
  - Translate the Spec Kit Plan into:
    - clear module and boundary definitions,
    - decisions and trade‑offs (with rationale),
    - constraints (tech stack, dependencies).

**Gate:** The Moderator and Tech Lead decide the Plan is coherent enough to generate Tasks/Steps:

- no fundamental unknowns that would blow up every Step,
- clear boundaries for where code should live,
- alignment with `PRODUCT.md` and domain language.

### 4. Tasks ↔ ROADMAP + STEP-XX

**Goal:** Break the Plan into small, traceable units of work.

- In Spec Kit:
  - Use the Tasks phase to generate task breakdowns.
  - Optionally rely on Spec Kit’s AI support to propose tasks from the Plan.

- In Moderated AI Development Workflow:
  - The Tech Lead and Development Team maintain:
    - `ROADMAP.md` – ordered list of Steps with goals and dependencies.
    - `STEP-XX.md` – per‑Step brief (scope, inputs, expected outputs, acceptance checks).

Each Spec Kit Task should:

- map to exactly one Moderated AI Development Workflow Step, or
- be clearly attached as part of a specific Step in `STEP-XX.md`.

**Gate:** Tech Lead enforces **MVP discipline**:

- Steps must be small enough that:
  - a Development Team agent can complete them in a focused work session,
  - a Moderator can review them in one sitting.

---

## Running a Step with Spec Kit and Moderated AI Development Workflow

Here is a concrete end‑to‑end flow for implementing and accepting a Step:

1. **Select a Step**
   - Choose an item from `ROADMAP.md`.
   - Ensure `STEP-XX.md` exists and describes:
     - goal and scope,
     - inputs and relevant files,
     - acceptance checks,
     - risks.

2. **Align with a Spec Kit Task**
   - Identify or create a matching Task in Spec Kit.
   - Link the Task to `STEP-XX.md` (e.g., via a comment or ID).

3. **Implement via AI assistants**
   - Use Spec Kit to drive AI‑assisted implementation (e.g., Copilot, Claude Code, Q Developer).
   - Ensure prompts reference:
     - relevant parts of `PRODUCT.md`, `ARCHITECTURE.md`, `STEP-XX.md`,
     - the Domain Language Matrix,
     - any agent rules from `AGENTS.md`.

4. **Bring changes to the Workbench**
   - Once the Task is “complete” in Spec Kit:
     - pull the changes into the local Workbench (Moderator’s environment).
   - The Moderator:
     - runs builds, tests, and linters,
     - performs manual UX checks if needed,
     - inspects diffs for architectural fit and maintainability.

5. **Review and record**
   - The Moderator fills in `REVIEW.md` for this Step:
     - summary of changes,
     - findings and concerns,
     - required revisions (if any).
   - If revisions are needed:
     - send concrete instructions back to the Development Team,
     - re‑run the Spec Kit Task or create a follow‑up Task as needed.

6. **QA and tag**
   - When the implementation looks good:
     - run the QA plan in `QA.md`,
     - record outcomes, defects, and confidence level.
   - If everything passes:
     - Moderator marks the Step as Done in Moderated AI Development Workflow,
     - creates an annotated Git tag for the Step.

Spec Kit may have marked the Task as done earlier. **The Moderated AI Development Workflow Step is only “done” when the Moderator accepts it.**

---

## Best practices

- **Spec Kit phases are proposals, not verdicts.**  
  Treat `/spec`, `/plan`, and `/tasks` outputs as drafts that still need Moderated AI Development Workflow’s role‑based review.

- **Keep Moderated AI Development Workflow artifacts canonical.**  
  Constitution, Spec, Plan, and Tasks may live in multiple places; Moderated AI Development Workflow’s `PRODUCT.md`, `ARCHITECTURE.md`, `ROADMAP.md`, and `STEP-XX.md` are the primary artifacts in the repo.

- **Use model contrast consciously.**  
  You can use one model for Spec Kit spec/plan phases and another for Moderated AI Development Workflow Dev Team work, letting them cross‑validate each other before the Moderator decides.

- **Store prompts alongside artifacts.**  
  Keep Spec Kit prompts and Moderated AI Development Workflow prompts in the repo (e.g., under `prompts/`) to maintain traceability and reproducibility.

- **Let Moderated AI Development Workflow own acceptance.**  
  Spec Kit is allowed to say “ready”; Moderated AI Development Workflow’s Moderator decides “accepted.”

---

## When Moderated AI Development Workflow + Spec Kit is a good fit

The combination shines when:

- you like Spec Kit’s SDD approach and want to keep using it,
- but you also want:
  - clear human roles,
  - explicit artifacts across the lifecycle,
  - and a non‑negotiable, human‑driven moderation layer.

You don’t have to abandon Spec Kit to adopt Moderated AI Development Workflow.  
You give Spec Kit the job of **structuring** your specs and tasks, and you give Moderated AI Development Workflow the job of **making them safe to depend on**.

---

MOD-W v1.1.0 · Moderated AI Development Workflow · [https://github.com/fpmcguire/moderated-ai-development-workflow](https://github.com/fpmcguire/moderated-ai-development-workflow)
