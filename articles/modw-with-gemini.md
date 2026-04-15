# Moderated AI Development Workflow (MOD-W) with Google Gemini

## Overview

Gemini can support Moderated AI Development Workflow (MOD-W) when you use it as a role assistant, not as an autonomous decision-maker.

Gemini is strongest in this setup when you:

- separate role context clearly,
- anchor prompts to MOD-W artifacts,
- preserve human moderation at every quality gate.

This guide explains a practical pattern to run MOD-W with Gemini while keeping traceability and control.

## Core operating rule

Use Gemini to propose. Humans decide.

In MOD-W terms:

- Product Owner, Tech Lead, and Development Team outputs can be AI-assisted.
- Moderator acceptance remains mandatory before a Step is considered done.
- REVIEW.md and QA.md are the evidence of acceptance, not chat completion status.

## Recommended setup

### 1. Keep artifacts canonical in the repo

Use these as your source of truth:

- [templates/PRODUCT.md](../templates/PRODUCT.md)
- [templates/ARCHITECTURE.md](../templates/ARCHITECTURE.md)
- [templates/ROADMAP.md](../templates/ROADMAP.md)
- [templates/STEP.md](../templates/STEP.md)
- [templates/REVIEW.md](../templates/REVIEW.md)
- [templates/QA.md](../templates/QA.md)
- [templates/DOMAIN_LANGUAGE.md](../templates/DOMAIN_LANGUAGE.md)
- [templates/AI_AGENTS.md](../templates/AI_AGENTS.md)

Treat Gemini chats as working notes. Move accepted content into repo artifacts.

### 2. Create role-specific Gemini contexts

Use separate chats, Gems, or prompt presets per role:

- Product Owner context
- Tech Lead context
- Development Team context
- Moderator checklist context

Do not mix roles in one thread. Context mixing causes scope drift and weak handoffs.

### 3. Ground each role with repository prompts

Start from:

- [prompts/product-owner-chatgpt.md](../prompts/product-owner-chatgpt.md)
- [prompts/tech-lead-chatgpt.md](../prompts/tech-lead-chatgpt.md)
- [prompts/development-team-claude.md](../prompts/development-team-claude.md)
- [docs/moderator-checklist.md](../docs/moderator-checklist.md)
- [prompts/prompt-guidelines.md](../prompts/prompt-guidelines.md)

Even though some prompt files are named for other models, the role constraints and quality expectations still apply when adapted for Gemini.

### 4. Use Gems for role isolation and repeatability

Create one Gem per MOD-W role so each role has stable instructions and bounded scope:

- Product Owner Gem: problem framing, user outcomes, acceptance intent.
- Tech Lead Gem: architecture options, trade-offs, and step shaping.
- Development Team Gem: implementation planning, code/test proposals, revision loops.
- Moderator Gem: review checklist, risk identification, and acceptance criteria checks.

For each Gem, include:

- role responsibilities (from [docs/roles.md](../docs/roles.md)),
- required artifacts as inputs,
- strict non-goals (for example, "do not approve acceptance"),
- expected output format.

Operational tip: start every Step by pasting the current Step brief and artifact excerpts into the role-specific Gem chat instead of relying on previous chat context.

### 5. Use NotebookLM as project context memory

Use NotebookLM as a curated reference layer for long-lived project context, not as the canonical source of truth.

Recommended NotebookLM source set:

- [templates/PRODUCT.md](../templates/PRODUCT.md)
- [templates/ARCHITECTURE.md](../templates/ARCHITECTURE.md)
- [templates/ROADMAP.md](../templates/ROADMAP.md)
- [templates/DOMAIN_LANGUAGE.md](../templates/DOMAIN_LANGUAGE.md)
- [templates/AI_AGENTS.md](../templates/AI_AGENTS.md)
- relevant Step files and review artifacts for active work

How to use it in MOD-W:

1. Upload or refresh sources whenever core artifacts change.
2. Ask NotebookLM for summaries of constraints, decisions, and open risks.
3. Pull those summaries into Gemini prompts as explicit context.
4. Record accepted decisions back into repo artifacts.

Guardrail: if NotebookLM and repository files disagree, repository artifacts win. Update NotebookLM sources after resolving the mismatch.

## Phase-by-phase flow

### Product shaping phase

Goal: produce a clear, testable [templates/PRODUCT.md](../templates/PRODUCT.md).

Use Gemini to:

- clarify user segments,
- sharpen acceptance intent,
- identify out-of-scope boundaries.

Moderator checks:

- requirements are specific and testable,
- constraints are explicit,
- assumptions are documented.

### Technical design phase

Goal: produce an implementable [templates/ARCHITECTURE.md](../templates/ARCHITECTURE.md).

Use Gemini to:

- propose alternatives and trade-offs,
- define boundaries and integration points,
- outline risk controls.

Moderator and Tech Lead checks:

- architecture aligns with PRODUCT intent,
- decisions include rationale,
- unknowns are reduced enough for step planning.

### Step planning phase

Goal: maintain [templates/ROADMAP.md](../templates/ROADMAP.md) with small, reviewable steps.

Use Gemini to:

- split work into thin vertical slices,
- detect hidden dependencies,
- propose acceptance checks per step.

Tech Lead checks:

- each step is small enough for one focused implementation cycle,
- dependencies are explicit,
- rollback or fallback approach exists where needed.

### Implementation phase

Goal: execute one Step at a time with full traceability.

Per step:

1. Copy [templates/STEP.md](../templates/STEP.md) into a concrete STEP-XX file.
2. Ask Gemini for implementation proposals tied to that step only.
3. Apply changes in the Workbench.
4. Run build, tests, lint, and manual checks.
5. Record findings in [templates/REVIEW.md](../templates/REVIEW.md).
6. Record verification evidence in [templates/QA.md](../templates/QA.md).
7. Accept or reject the step.

## Prompting pattern for Gemini

For reliable outputs, include these sections in every task prompt:

- Objective: exact step goal and non-goals.
- Inputs: links or excerpts from PRODUCT, ARCHITECTURE, STEP, domain language.
- Constraints: architecture boundaries, coding standards, quality gates.
- Output format: expected deliverable shape.
- Done criteria: explicit checks for acceptance.

Minimal template:

```text
Role: Development Team assistant in MOD-W.
Objective: Implement STEP-03 exactly as described.
Inputs: PRODUCT sections A/B, ARCHITECTURE sections C/D, STEP-03.
Constraints: Keep module boundaries, no new dependencies, update tests.
Output: Unified diff + short rationale + risk notes.
Done criteria: Build passes, tests pass, no scope expansion.
```

## Quality gate enforcement

Gemini output is draft code or draft decisions until moderated.

Always require:

- technical review in the Workbench,
- reproducible test evidence,
- explicit review notes,
- final moderator decision.

If evidence is weak, request a revision and keep the step open.

## Common failure modes and mitigations

- Role bleed across prompts
  - Mitigation: one role per chat context and explicit role headers.

- Over-broad implementation proposals
  - Mitigation: enforce step scope and list non-goals.

- Missing traceability from prompt to artifact
  - Mitigation: always reference PRODUCT, ARCHITECTURE, and STEP IDs.

- Premature acceptance
  - Mitigation: acceptance only after REVIEW and QA evidence.

## Lightweight first run checklist

1. Prepare PRODUCT and ARCHITECTURE drafts.
2. Create ROADMAP and first STEP-XX.
3. Run one Gemini-assisted implementation cycle for that step.
4. Perform moderator review and QA execution.
5. Tag the step only after acceptance.

## Related docs

- [docs/roles.md](roles.md)
- [docs/quality-gates.md](quality-gates.md)
- [docs/step-lifecycle.md](step-lifecycle.md)
- [docs/artifacts.md](artifacts.md)

---

MOD-W v2.1.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
