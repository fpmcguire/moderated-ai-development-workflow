# Moderated AI Development Workflow

**Github repo:** https://github.com/fpmcguire/moderated-ai-development-workflow.git

## Purpose

Moderated AI Development Workflow is a role-driven, document-centered workflow for AI‑assisted software development.

It is designed to:

- Reduce ambiguity by separating product, technical, and implementation decisions.
- Catch errors and misalignments early through repeated, focused reviews, and role/AI cross-validation.
- Keep product intent, architecture, and implementation synchronized over time.

## Core principles

- Clear documents beat unstated assumptions.
- Product “what/why” is separate from technical “how.”
- Architecture is separate from day‑to‑day implementation.
- Each role has a defined responsibility and approval boundary.
- Small, reviewable steps are preferred over large, fuzzy scopes.
- Acceptance is written in observable, testable terms wherever possible.

---

## Roles

### Moderator

The Moderator owns the workflow.

Responsibilities:

- Orchestrate the Moderated AI Development Workflow process across all roles.
- Decide direction when outputs conflict.
- Decide what becomes canonical (which doc/version “wins”).
- Approve whether a step is ready to proceed.
- Protect the workflow from scope and process bloat.

The Moderator has final go/no‑go authority within Moderated AI Development Workflow.

---

### Product Owner

The Product Owner defines what is being built and why.

Responsibilities:

- Clarify user value, intent, scope, and priorities.
- Maintain `PRODUCT.md` and shape user‑facing workflows.
- Define acceptance intent for each step in `STEP-XX.md`.
- Keep in‑scope and out‑of‑scope items explicit.
- Avoid technical design unless explicitly requested.

The Product Owner focuses on product clarity, not code structure.

---

### Tech Lead

The Tech Lead defines how to build it safely and coherently.

Responsibilities:

- Maintain `ARCHITECTURE.md` and technical guardrails.
- Maintain `ROADMAP.md` and technical guardrails.
- Review each step for technical fit, risks, and dependencies.
- Protect the system from accidental complexity and architecture drift.
- Recommend patterns, constraints, and naming consistency.
- Avoid redefining product intent without escalation.

The Tech Lead focuses on technical correctness and maintainability.

---

### Development Team

The Development Team implements the approved slice.

Responsibilities:

- Restate understanding of the current `STEP-XX.md` before coding.
- Identify ambiguities, mismatches, or blockers early.
- Implement only the approved scope for the current step.
- Follow product intent, architectural guidance, and test expectations.
- Avoid inventing scope or silently making product/architecture decisions.

The Development Team is responsible for execution, not unilateral re‑design.

---

## Canonical documents

All Moderated AI Development Workflow docs live under `//mod-w` in the project.

- `MOD-W.md` – this workflow methodology overview for the project.
- `PRODUCT.md` – what is being built, for whom, and why it matters.
- `ARCHITECTURE.md` – technical structure, boundaries, patterns, constraints.
- `ROADMAP.md` – ordered sequence of small, reviewable increments.
- `STEP-XX.md` – the current implementation slice (goal, scope, acceptance).
- `REVIEW.md` – review notes and decisions for the current Step.
- `QA.md` – verification evidence for the Step.
- `DOMAIN-LANGUAGE.md` – canonical terms and definitions used across docs and code.
- (Optional) Other supporting docs, only when they earn their existence.

Each Moderated AI Development Workflow doc should include the standard MOD-W footer with name and version.

---

## Review model

Moderated AI Development Workflow deliberately uses multiple reviews before code is merged.

### 1. Product review

Question: **Is this the right thing to build now?**

Owner: Product Owner  
Checks typically include:

- User value and problem clarity.
- In‑scope vs out‑of‑scope items.
- Observable acceptance intent in `STEP-XX.md`.
- Consistency with `PRODUCT.md` and `ROADMAP.md`.

---

### 2. Technical review

Question: **Is this a sound and coherent way to build it?**

Owner: Tech Lead  
Checks typically include:

- Alignment with `ARCHITECTURE.md` and chosen stack.
- Technical risks, dependencies, and constraints.
- Naming and domain alignment with `DOMAIN-LANGUAGE.md`.
- Testability and observability implications.

---

### 3. Workbench review (AI‑assisted in editor)

Question: **Does the code we are about to merge actually match the approved step and acceptance?**

Owner: Development Team (execution), Moderator (policy)

Pattern:

- Run an AI‑assisted review in the developer’s editor (e.g., VS Code with Copilot or a similar tool).
- Ask the AI to compare the actual changes against the current `STEP-XX.md` and its acceptance checks.

The Workbench review is focused on:

- Deviations from the approved scope.
- Missing or misaligned acceptance behavior.
- Obvious defects or risky changes that contradict the architecture.

AI feedback does **not** replace human code review; it is an extra validation surface before merge.

---

### Moderator verification

Question: **Are the outputs aligned enough to proceed?**

Owner: Moderator

The Moderator:

- Reviews Product, Tech, and Development outputs for conflicts.
- Confirms that `STEP-XX.md` and related docs are consistent.
- Decides whether the project may proceed with implementation/merge.
- Sends items back for clarification when ambiguity or conflicts remain.

If any of the reviews is unclear, the workflow pauses for clarification rather than continuing with hidden assumptions.

---

## Workflow at a glance

The Moderator is always human (HITL) and has final go/no‑go authority.

For each Moderated AI Development Workflow step:

1. Product Owner updates `PRODUCT.md` and `STEP-XX.md` (goal, scope, acceptance).

2. Tech Lead reviews/updates `ARCHITECTURE.md` and `ROADMAP.md` as needed and reviews `STEP-XX.md`.

3. Development Team restates the step (in their own words) and implements only the approved slice.

4. Workbench review #1 (AI‑assisted in editor)
   - Run an AI‑assisted review in the editor against `STEP-XX.md` and its acceptance checks.
   - Fix obvious mismatches or defects before raising the work for review.

5. Moderator review (HITL)
   - Moderator checks alignment across `PRODUCT.md`, `ARCHITECTURE.md`, `ROADMAP.md`, `STEP-XX.md`, and the current implementation.
   - Moderator records feedback and a provisional go/no‑go decision.

6. Tech Lead feedback pass
   - Tech Lead reviews the Development Team’s changes and Moderator feedback together.
   - Tech Lead calls out technical issues, risks, or architecture drift and suggests adjustments.

7. Development Team adjustment pass
   - Development Team restates the feedback (what they will change and why).
   - They adjust the implementation, staying within the approved scope.

8. Workbench review #2 (AI‑assisted in editor)
   - Run a second AI‑assisted review on the updated changes against `STEP-XX.md` and prior feedback.
   - Confirm that changes now match the step and acceptance criteria.

9. Final Moderator go/no‑go (HITL)
   - If everything is aligned, the Moderator gives final approval.
   - The step is merged and `ROADMAP.md` is advanced to the next slice.
   - If not, the Moderator sends it back with explicit reasons.

This double‑loop (Product/Tech/Dev + Moderator + Tech + Dev + AI) is intentionally slower than “code first, clarify later,” but in practice it catches misalignment and defects early and reduces painful rework downstream.

---

## Operating rules

To keep Moderated AI Development Workflow lean and effective:

- **Documents must earn their existence.**  
  If an existing doc can hold the information cleanly, prefer updating it.

- **No hidden scope.**  
  Anything not in the current `STEP-XX.md` is out of scope for this step.

- **Explicit out‑of‑scope.**  
  When something is intentionally deferred, state it.

- **Stable naming.**  
  Resolve naming conflicts early and keep `DOMAIN-LANGUAGE.md` updated.

- **Pause on ambiguity.**  
  If any role is unsure, stop and clarify instead of guessing.

- **Lean first, expand later.**  
  Start with `MOD-W.md`, `PRODUCT.md`, `ROADMAP.md`, and the current `STEP-XX.md`; add more docs and controls only when they clearly help.

---

## Tracks and tools (overview only)

Moderated AI Development Workflow is tool‑agnostic but tool‑aware.

- You may use different AI tools or models per role (e.g., one model for Product review, another for Tech review, a coding agent for Workbench review).
- A more agentic “Track 2” (e.g., using a coding agent that can edit repos) can be defined by policy later, but Moderated AI Development Workflow’s core roles and documents do not change.

Default recommendation:

- Treat current Moderated AI Development Workflow as **Track 1 (guided)**: AI assists with reviews and code suggestions but does not act autonomously without explicit policies and human approval.

---

## Folder layout (project level)

At the project root:

- `README.md`
- `//`
  - `MOD-W.md`
  - `PRODUCT.md`
  - `ARCHITECTURE.md`
  - `ROADMAP.md`
  - `STEP-XX.md`
  - `DOMAIN-LANGUAGE.md` (as needed)

`README.md` should briefly mention that the project uses Moderated AI Development Workflow and point to `//`.

---

MOD-W v1.1.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
