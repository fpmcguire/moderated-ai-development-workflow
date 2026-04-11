# Moderated AI Development Workflow + Kiro Playbook

## Overview

**Kiro** is a spec‑driven IDE that turns Requirements, Design, and Tasks into executable work for AI agents.  
**Moderated AI Development Workflow** is a governance and workflow layer that adds roles, artifacts, and human moderation on top of any spec‑driven engine.

Kiro answers:

> “How do I run Spec‑Driven Development in an IDE with agents?”

Moderated AI Development Workflow answers:

> “Who decides what, how do we review, and when is a change actually acceptable?”

This playbook shows how to combine them:

- how to map Kiro’s phases to Moderated AI Development Workflow artifacts
- how roles (Product Owner, Tech Lead, Development Team, Moderator) work in Kiro
- a simple checklist to run your **first Moderated AI Development Workflow Step inside Kiro**

---

## Conceptual mapping

Kiro has three main spec phases:

- **Requirements** – problem, users, goals, constraints
- **Design** – architecture, data, integration points
- **Tasks** – concrete units of work to implement

Moderated AI Development Workflow (MOD-W) has three corresponding core artifacts:

- `PRODUCT.md` – product problem, users, goals, requirements
- `ARCHITECTURE.md` – technical approach, architecture decisions
- `ROADMAP.md` + `STEP-XX.md` – ordered Steps and per‑Step briefs

The mapping is:

| Kiro phase   | MOD-W artifact(s)           | Purpose                                 |
| ------------ | --------------------------- | --------------------------------------- |
| Requirements | `PRODUCT.md`                | What we’re building and why             |
| Design       | `ARCHITECTURE.md`           | How we’re building it                   |
| Tasks        | `ROADMAP.md` + `STEP-XX.md` | Concrete, bounded units of work (Steps) |

MOD-W then layers on:

- `REVIEW.md` and `QA.md` for **validation and evidence**
- `DOMAIN_LANGUAGE_MATRIX.md` and `AGENTS.md` as **steering docs** for humans and agents

---

## Roles in a MOD-W + Kiro setup

In a Kiro + MOD-W project, roles look like this:

- **Product Owner**
  - Collaborates in Kiro’s **Requirements** phase.
  - Ensures `PRODUCT.md` reflects agreed requirements.
  - Approves when Requirements are “good enough” to move to Design.

- **Tech Lead**
  - Works primarily in Kiro’s **Design** and **Tasks** phases.
  - Ensures Kiro’s Design specs reflect `ARCHITECTURE.md`.
  - Helps translate Requirements → Design → Tasks/Steps with clear boundaries.

- **Development Team**
  - Uses Kiro’s Tasks and agent features to implement individual Steps.
  - Treats each Kiro Task as one MOD-W Step (or part of one) driven by `STEP-XX.md`.

- **Moderator**
  - Treats Kiro as one input; the **source of truth is still the repository**.
  - Runs builds/tests in the local Workbench (VS Code + Copilot, etc.).
  - Decides if Requirements, Design, and Tasks are “approved enough” to advance.
  - Decides if a Step is actually complete, regardless of Kiro’s task status.

The core rule: **Kiro can move states inside the IDE; only the Moderator moves states in MOD-W.**

---

## Phase-by-phase playbook

### 1. Requirements ↔ PRODUCT.md

**Goal:** Agree on what problem you’re solving and for whom.

- In Kiro:
  - Use the Requirements phase to capture problems, users, goals, constraints.
  - Use Kiro’s own AI assistance to draft and refine.

- In MOD-W:
  - The Product Owner and Tech Lead sync Kiro’s Requirements into `PRODUCT.md`.
  - The Moderator checks that:
    - Requirements are clear.
    - Acceptance intent is explicit.
    - Risks and out‑of‑scope items are captured.

**Gate:** The Moderator marks the Requirements phase “approved enough” to move to Design.  
Kiro may say “Requirements ready”; MOD-W requires the Moderator’s explicit approval in the repo.

### 2. Design ↔ ARCHITECTURE.md

**Goal:** Decide how the system will be structured.

- In Kiro:
  - Use the Design phase to capture the architecture: components, data models, integrations.
  - Use Kiro’s agents to propose alternatives, then refine.

- In MOD-W:
  - The Tech Lead owns `ARCHITECTURE.md` in the repo.
  - Kiro’s Design spec is treated as a **working draft** that must be reconciled with `ARCHITECTURE.md`.
  - The Moderator ensures:
    - Design matches the constraints and domain language.
    - There is a clear path to small, independent Steps.

**Gate:** The Moderator and Tech Lead agree the Design is stable enough to generate Tasks/Steps.  
Only then do they proceed to Kiro’s Tasks phase and MOD-W’s Step planning.

### 3. Tasks ↔ ROADMAP + STEP-XX

**Goal:** Turn Design into small, verifiable units of work.

- In Kiro:
  - Use Tasks to break work down based on the Design.
  - Optionally use agents to propose a task breakdown.

- In MOD-W:
  - The Tech Lead and Development Team maintain:
    - `ROADMAP.md` – ordered list of Steps.
    - `STEP-XX.md` – detailed Step briefs.
  - Each Kiro Task is:
    - mapped to a MOD-W Step, or
    - treated as sub‑work inside a larger Step.

**Gates:**

- Each Step must be small enough to:
  - be implemented by a Development Team agent in a focused session.
  - be fully reviewed by a Moderator in a single sitting.
- The Tech Lead enforces **MVP discipline**: Steps are minimal, verifiable increments.

---

## Running a MOD-W Step in Kiro

Here is a concrete workflow for a single Step:

1. **Pick a Step**
   - Choose a Step from `ROADMAP.md` (or define a new one).
   - Ensure `STEP-XX.md` is clear (scope, inputs, acceptance checks).

2. **Align Kiro Task**
   - In Kiro, create or select a Task that corresponds to this Step.
   - Paste the relevant parts of `PRODUCT.md`, `ARCHITECTURE.md`, `STEP-XX.md` into the Kiro context.

3. **Let the Development Team implement**
   - Use Kiro’s agents to implement the Task/Step:
     - generate or edit code
     - run tests in the Kiro environment if available
   - Keep prompts and outputs aligned with `DOMAIN_LANGUAGE_MATRIX.md` and `AGENTS.md`.

4. **Bring the result to the Workbench**
   - Sync or pull the changes to the local repo.
   - The Moderator:
     - runs builds and tests in the Workbench
     - performs manual UX checks if needed
     - compares behavior against `STEP-XX.md` acceptance checks

5. **Review and QA**
   - The Moderator fills in `REVIEW.md`:
     - what changed
     - any issues found
     - requested revisions (if any)
   - After revisions, run QA:
     - execute the plan in `QA.md`
     - record outcomes and confidence level

6. **Accept and tag**
   - When everything is green:
     - Moderator marks the Step as complete.
     - Adds an annotated Git tag for the Step.
   - Kiro’s Task may already be marked done; MOD-W acceptance is the final word.

---

## Best practices

- **Kiro is the engine, not the judge.**  
  Use Kiro to generate and coordinate work, but keep **acceptance power** with the Moderator in the local Workbench.

- **Sync artifacts regularly.**  
  Treat Kiro specs as drafts until they are reflected in `PRODUCT.md` and `ARCHITECTURE.md`.

- **Use the same domain language everywhere.**  
  Keep `DOMAIN_LANGUAGE_MATRIX.md` up to date and paste relevant sections into Kiro prompts.

- **Keep Steps small.**  
  If a Kiro Task feels too big to review safely, split it in MOD-W and reflect that split back into Kiro.

- **Record learning in the repo.**  
  If a Kiro session reveals important insights, capture them in `REVIEW.md`, `QA.md`, or the Domain Language Matrix, not just in Kiro’s history.

---

## When MOD-W + Kiro is a good fit

This combined setup is especially strong when:

- you want **spec‑driven execution** with a powerful IDE and agents (Kiro),
- but you also want **human‑in‑the‑loop governance**, traceability, and multi‑role validation (MOD-W).

You get the best of both:

- Kiro drives SDD in the IDE.
- MOD-W keeps the system understandable, reviewable, and safe to evolve.

---

MOD-W v2.0.0 · Moderated AI Development Workflow · [https://github.com/fpmcguire/moderated-ai-development-workflow](https://github.com/fpmcguire/moderated-ai-development-workflow)
