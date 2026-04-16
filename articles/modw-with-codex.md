# Moderated AI Development Workflow (MOD-W) with OpenAI Codex

## Overview

**OpenAI Codex** is a cloud-based AI coding agent that runs directly against your repository. It reads an `AGENTS.md` file at the repo root to understand its role, context, and constraints — making it a natural fit for the **Tech Lead** role in MOD-W.

**Moderated AI Development Workflow (MOD-W)** provides the governance layer: clear role separation, human quality gates, and cross-agent validation. Codex provides the automation: generating roadmaps, step briefs, and technical reviews without requiring copy-paste workflows.

This article explains:

- Where Codex fits in the MOD-W role structure.
- How `AGENTS.md` establishes the Tech Lead role for Codex.
- A phase-by-phase playbook for running MOD-W with Codex as Tech Lead.
- How Codex and Claude Code work together in the same project.

---

## Where Codex fits in MOD-W

In MOD-W v3, Codex is the **default** agent for the **Tech Lead** role. It reads `AGENTS.md` from the repo root, writes planning artifacts directly to the filesystem, and reviews Development Team output — no copy-paste required.

| Role             | Default agent (v3)                                    |
| ---------------- | ----------------------------------------------------- |
| Product Owner    | Claude chatbot + Perplexity + Gemini (Definition phase); Claude Code SubAgent (Validation) |
| **Tech Lead**    | **Codex** (full session, reads `AGENTS.md`)           |
| Development Team | Claude Code SubAgent (reads `CLAUDE.md`)              |
| QA               | Claude Code SubAgent                                  |
| Moderator        | Human only                                            |

Cross-validation is intentional: Codex plans and reviews; Claude Code implements. Model diversity at the Tech Lead / Dev Team boundary is MOD-W's primary quality lever.

Codex does **not** replace the Moderator, Product Owner, or Development Team. It owns the Tech Lead role only: planning artifacts, step briefs, and technical review.

---

## The `AGENTS.md` file

Codex reads `AGENTS.md` from the repo root at session start, the same way Claude Code reads `CLAUDE.md`. This file is the Tech Lead's primary configuration artifact for Codex — it defines the role, the context files to read, the expected outputs, and the conventions to follow.

**Who generates it:** The Tech Lead (Codex) generates `AGENTS.md` from the project's `ARCHITECTURE.md` and `DOMAIN_LANGUAGE.md` using the `templates/AGENTS.md` template, during the Architecture Definition planning session.

**Where it lives:** Repo root — `AGENTS.md`.

**When to update it:** Whenever `ARCHITECTURE.md`, the stack, or project conventions change.

---

## Responsibility split

| Codex owns                                             | MOD-W owns                                               |
| ------------------------------------------------------ | -------------------------------------------------------- |
| Reading repo files and context docs                    | Moderator go/no-go authority                             |
| Generating `ROADMAP.md` and `STEP-XX.md`               | Tech Lead approval of roadmap and step briefs            |
| Reviewing Development Team output                      | Moderator and Tech Lead quality gates                    |
| Classifying review findings as must-fix / nice-to-have | Moderator decision to accept, reject, or request changes |

Codex does **not** merge code, override quality gates, or make product scope decisions.

---

## Setup

1. **Complete the core MOD-W artifacts first.**
   Ensure `PRODUCT.md`, `ARCHITECTURE.md`, and `DOMAIN_LANGUAGE.md` exist and are approved by the Moderator before involving Codex.

2. **Generate `AGENTS.md`.**
   The Tech Lead uses the `templates/AGENTS.md` template, filling all `{{PLACEHOLDERS}}` from `ARCHITECTURE.md` and `DOMAIN_LANGUAGE.md`. Place the completed file at the repo root.

3. **Generate `CLAUDE.md`.**
   The Tech Lead also generates `CLAUDE.md` from `templates/CLAUDE.md` for the Development Team (Claude Code). Both files live at the repo root — Codex reads `AGENTS.md`, Claude Code reads `CLAUDE.md`.

4. **Start a Codex session.**
   Codex reads `AGENTS.md` automatically. The Moderator states the task — generate roadmap, generate a step brief, or review a completed step.

---

## Phase-by-phase playbook

### 1. Roadmap generation

**Goal:** Break the approved `PRODUCT.md` into a sequence of small, reviewable steps.

- **Moderator → Codex:** Provide `PRODUCT.md` and `ARCHITECTURE.md`. Ask Codex to generate `ROADMAP.md`.
- **Codex:** Reads both files, produces an ordered `ROADMAP.md` with one goal and one set of acceptance checks per step.
- **Gate:** The Moderator and Tech Lead review the roadmap for scope, ordering, and feasibility before any step is implemented.

### 2. Step brief generation

**Goal:** Produce a single, unambiguous `STEP-XX.md` for the Development Team to implement.

- **Moderator → Codex:** Reference the approved `ROADMAP.md` entry. Ask Codex to generate `STEP-XX.md`.
- **Codex:** Reads `ROADMAP.md`, `ARCHITECTURE.md`, and `DOMAIN_LANGUAGE.md`, then produces a step brief with goal, scope, inputs, out-of-scope items, and acceptance checks.
- **Gate:** The Moderator confirms the step brief is clear and complete before handing it to the Development Team. Ambiguous or over-scoped briefs go back to Codex for revision.

### 3. Development Team implementation

**Goal:** Implement the approved step.

- **Moderator → Development Team (Claude Code):** Provide the confirmed `STEP-XX.md`.
- **Claude Code:** Reads `CLAUDE.md` and the step brief, restates the step, proposes a plan, and waits for Moderator approval before writing code.
- **Gate:** Moderator reviews the diff in the Workbench (VS Code). Minor issues fixed directly; significant issues returned to the Development Team with feedback.

### 4. Tech Lead review

**Goal:** Validate the implementation for architectural fit, naming consistency, and maintainability.

- **Moderator → Codex:** Ask Codex to review the Development Team's output against the active `STEP-XX.md`.
- **Codex:** Reads changed files and the step brief, then produces a structured review classifying findings as **must-fix** or **nice-to-have**.
- **Gate:** Moderator records findings in `REVIEW.md`. Must-fix items return to the Development Team; nice-to-haves are logged for a future step. The step is not accepted until all must-fix items are resolved.

### 5. Acceptance and tagging

**Goal:** Close the step and advance the roadmap.

- **Moderator:** Confirms all acceptance checks pass, `REVIEW.md` and `QA.md` are complete.
- **Moderator:** Creates an annotated Git tag for the step and marks it done in `ROADMAP.md`.
- The next step cycle begins at phase 2.

---

## Codex + Claude Code in the same project

Codex (Tech Lead) and Claude Code (Development Team) are designed to work alongside each other. Each reads its own config file and operates within its own role boundary.

|               | Codex (Tech Lead)                                 | Claude Code (Development Team)         |
| ------------- | ------------------------------------------------- | -------------------------------------- |
| Config file   | `AGENTS.md` (repo root)                           | `CLAUDE.md` (repo root)                |
| Session start | Reads `AGENTS.md` automatically                   | Reads `CLAUDE.md` automatically        |
| Typical task  | Generate roadmap, write step brief, review output | Implement a single approved step       |
| Does not      | Write application code, merge changes             | Define architecture, generate roadmaps |

**Cross-validation** is preserved: Codex never reviews its own plans without a human gate, and Claude Code never implements without a Codex- and Moderator-approved step brief.

---

## Best practices

- **Approve `AGENTS.md` before the first Codex session.** A Tech Lead prompt that lacks correct stack or naming conventions will produce a roadmap the Development Team cannot safely follow.
- **Keep steps narrow.** If Codex proposes a step with more than 5–7 acceptance checks, ask it to split the step before handing it to the Development Team.
- **Use Codex reviews consistently.** Every completed step should pass through a Codex Tech Lead review before Moderator acceptance — not just complex ones.
- **Update `AGENTS.md` when architecture changes.** If `ARCHITECTURE.md` is updated mid-project, regenerate `AGENTS.md` so Codex's context stays current.
- **Commit before switching agents.** If you switch between Codex and Claude Code within a step, commit the repo first so both agents read the current file state.

---

## Summary

| Phase          | Agent                  | MOD-W outcome                                   |
| -------------- | ---------------------- | ----------------------------------------------- |
| **Roadmap**    | Codex (Tech Lead)      | Approved `ROADMAP.md`                           |
| **Step brief** | Codex (Tech Lead)      | Approved `STEP-XX.md`                           |
| **Implement**  | Claude Code (Dev Team) | Step implemented and summarised                 |
| **Review**     | Codex (Tech Lead)      | Must-fix / nice-to-have findings in `REVIEW.md` |
| **Accept**     | Moderator (human)      | Git tag, `ROADMAP.md` advanced                  |

---

MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
