# Moderated AI Development Workflow (MOD-W) with Claude Code

## Overview

**Claude Code** is Anthropic's agentic CLI and VS Code extension. It reads a `CLAUDE.md` file at the repo root to understand its role, context, and constraints — making it the default agent for the **Development Team** role in MOD-W v3.

**Moderated AI Development Workflow (MOD-W)** provides the governance layer: role separation, human quality gates, and cross-agent validation. Claude Code provides the execution: implementing approved steps with plan confirmation, blocking build gates, and SubAgent handoffs — all without leaving VS Code.

This article explains:

- Where Claude Code fits in the MOD-W role structure.
- How `CLAUDE.md` establishes the Development Team role for Claude Code.
- A phase-by-phase playbook for running a MOD-W step with Claude Code.
- How the VS Code extension works in practice.
- How Claude Code and Codex operate side by side in the same project.

---

## Where Claude Code fits in MOD-W

In MOD-W v3, Claude Code is the **default** agent for the **Development Team** role. It reads `CLAUDE.md` from the repo root, enters Plan Mode before writing any files, implements the approved step, and spawns QA and Product Owner SubAgents before handing off to the Tech Lead.

| Role             | Default agent (v3)                                                                     |
| ---------------- | -------------------------------------------------------------------------------------- |
| Product Owner    | Claude chatbot + Perplexity + Gemini (Definition); Claude Code SubAgent (Validation)   |
| Tech Lead        | Codex (full session, reads `AGENTS.md`)                                                |
| **Development Team** | **Claude Code SubAgent (reads `CLAUDE.md`)**                                       |
| QA               | Claude Code SubAgent (spawned by Dev Team session)                                     |
| Moderator        | Human only                                                                             |

Cross-validation is intentional: Codex plans and reviews; Claude Code implements. Model diversity at the Tech Lead / Dev Team boundary is MOD-W's primary quality lever.

Claude Code does **not** generate roadmaps, write architecture docs, or perform Tech Lead review. It owns the Development Team role only: implementing an approved `STEP-XX.md` with minimal, scoped changes.

---

## The `CLAUDE.md` file

Claude Code reads `CLAUDE.md` from the repo root at session start, the same way Codex reads `AGENTS.md`. This file is the Development Team's primary configuration artifact — it defines the role, the context files to read, the expected behavior, and the project conventions to follow.

**Who generates it:** The Tech Lead (Codex) generates the project-specific `CLAUDE.md` from `ARCHITECTURE.md` and `DOMAIN_LANGUAGE.md` using the `templates/CLAUDE.md` template, during the Architecture Definition planning session.

**Where it lives:** Repo root — `CLAUDE.md`.

**When to update it:** Whenever `ARCHITECTURE.md`, the stack, or project conventions change significantly.

---

## Responsibility split

| Claude Code owns                                              | MOD-W owns                                                  |
| ------------------------------------------------------------- | ----------------------------------------------------------- |
| Reading `CLAUDE.md` and `STEP-XX.md` at session start        | Moderator go/no-go authority at every gate                  |
| Restating the step and proposing a plan before writing code   | Moderator approval of the plan before implementation begins |
| Implementing the step with minimal, scoped changes            | Moderator review of the diff in the Workbench               |
| Running a blocking build gate before handoff                  | Tech Lead review of implementation for architectural fit    |
| Spawning QA and Product Owner SubAgents after implementation  | Moderator acceptance and Git tag for the completed step     |

Claude Code does **not** merge code, override quality gates, or make scope decisions.

---

## Setup

1. **Complete the core MOD-W artifacts first.**
   Ensure `PRODUCT.md`, `ARCHITECTURE.md`, `DOMAIN_LANGUAGE.md`, `AGENTS.md`, and a project-specific `CLAUDE.md` exist and are approved before starting a Development Team session.

2. **Install Claude Code.**
   Claude Code is available as a CLI (`npm install -g @anthropic-ai/claude-code`) and as a VS Code extension (search **Claude Code** in the Extensions panel). Both read the same `CLAUDE.md` and share conversation history.

3. **Prepare the step brief.**
   Ensure the active `STEP-XX.md` is approved by the Moderator and Tech Lead before handing it to Claude Code. An ambiguous or over-scoped step brief is a Moderator issue, not a Development Team issue.

4. **Start a Claude Code session.**
   In the VS Code extension, open the Claude Code panel. Provide the path to `STEP-XX.md` as the first message. Claude Code reads `CLAUDE.md` automatically and begins with a plan.

---

## Phase-by-phase playbook

### 1. Session start and context load

**Goal:** Claude Code reads its role and the step before touching any files.

- **Moderator → Claude Code:** Provide the path to the active `STEP-XX.md`.
- **Claude Code:** Reads `CLAUDE.md`, `STEP-XX.md`, `ARCHITECTURE.md`, `AGENTS.md`, and `DOMAIN_LANGUAGE.md`. Restates the step in its own words so the Moderator can confirm understanding before proceeding.
- **Gate:** The Moderator confirms the restatement is correct. Misunderstandings are corrected before any plan is proposed.

### 2. Plan Mode — implementation options gate

**Goal:** Agree on how the step will be implemented before any code is written.

- **Claude Code:** Enters Plan Mode. Proposes an implementation approach: which files change, what is added or modified, what stays out of scope.
- **Gate:** The Moderator reviews the plan. Minor adjustments are made inline; significant scope concerns go back to the Tech Lead before Claude Code proceeds. Claude Code does **not** write files until the Moderator approves the plan.

### 3. Implementation

**Goal:** Execute the approved plan with minimal, scoped changes.

- **Claude Code:** Implements the step according to the approved plan. Changes are limited to what was described; no opportunistic refactors or unrequested additions.
- **Blocking build gate:** Before declaring implementation complete, Claude Code runs the project's build and test commands. A failing gate is not handed off — it is fixed first.
- **Gate:** The Moderator reviews the diff in the Workbench (VS Code). The Git diff and any test output are the source of truth, not Claude Code's summary.

### 4. QA SubAgent

**Goal:** Validate that acceptance checks in `STEP-XX.md` are met.

- **Claude Code:** Spawns a QA SubAgent automatically after the build gate passes.
- **QA SubAgent:** Reads the implementation and `STEP-XX.md` acceptance checks. Produces `QA.md` with outcomes, a manual check list, and known limitations. Flags any checks requiring human or browser verification.
- **Gate:** The Moderator reviews `QA.md`. Items requiring manual verification are checked in the Workbench. If acceptance checks are not met, findings go back to the Development Team.

### 5. Product Owner validation SubAgent

**Goal:** Confirm the step delivers what was intended in `PRODUCT.md`.

- **Claude Code:** Spawns a Product Owner SubAgent after QA passes.
- **Product Owner SubAgent:** Validates completed work against `STEP-XX.md` acceptance intent and signs off.
- **Gate:** The Moderator reviews the sign-off. The step is not marked ready for Tech Lead review until both QA and Product Owner SubAgents have completed.

### 6. Tech Lead review

**Goal:** Verify architectural fit, naming consistency, and maintainability.

- **Moderator → Codex (Tech Lead):** Ask Codex to review the Development Team's output against the active `STEP-XX.md`.
- **Codex:** Produces a structured `REVIEW.md` classifying findings as **must-fix** or **nice-to-have**.
- **Gate:** Must-fix items return to the Development Team. Nice-to-haves are logged for a future step. The step is not accepted until all must-fix items are resolved.

---

## Working in VS Code

Claude Code's VS Code extension integrates directly into the editor. The key behaviors for MOD-W work:

**Chat panel:**
- Open with the Claude Code icon in the Activity Bar or `Ctrl+Shift+C`.
- Conversations persist between sessions. Use `claude --resume` in the integrated terminal to re-enter a prior session.

**Code references:**
- Type `@filename.ts` or `@filename.ts#L10-25` in the chat panel to anchor Claude Code to a specific file or line range.
- Press `Alt+K` to insert the current editor selection into the chat automatically.
- Claude Code can also navigate, edit, and create files directly — you don't need to paste code manually.

**Parallel conversations:**
- Open additional Claude Code tabs (`Ctrl+Shift+Esc`) for independent tasks.
- Each tab has its own conversation context. Do not run two Development Team sessions against the same step simultaneously.

---

## Worktree branches

When Claude Code runs a task in worktree isolation — either via the `--worktree` flag or when the desktop app creates one automatically — it:

1. Creates a new branch from `origin/HEAD` (clean remote state).
2. Names the branch `claude/<slug>`, where `<slug>` is either a name you provide or a randomly generated identifier (e.g., `claude/sweet-fermat-af8f00`).
3. Checks the branch out in a separate working directory so it does not interfere with your main branch.

**Worktrees auto-delete on session exit** if there are no new commits, uncommitted changes, or untracked files. If a session has changes, Claude Code prompts whether to keep or discard the worktree — do not skip that prompt.

**Git hygiene for MOD-W:**
- Name worktrees explicitly to keep branch names readable: `claude --worktree step-03-auth`.
- Commit or discard all changes before ending a worktree session to ensure automatic cleanup fires.
- After any Claude Code session, run `git branch | grep claude/` to spot and prune leftover branches.
- Commit before switching between Claude Code and Codex within the same step so both agents read the current file state.

---

## Claude Code + Codex in the same project

Claude Code (Development Team) and Codex (Tech Lead) are designed to work alongside each other in the same repo. Each reads its own config file and operates within its own role boundary.

|               | Codex (Tech Lead)                                  | Claude Code (Development Team)                  |
| ------------- | -------------------------------------------------- | ----------------------------------------------- |
| Config file   | `AGENTS.md` (repo root)                            | `CLAUDE.md` (repo root)                         |
| Session start | Reads `AGENTS.md` automatically                    | Reads `CLAUDE.md` automatically                 |
| Typical task  | Generate roadmap, write step brief, review output  | Implement a single approved step                |
| Does not      | Write application code, merge changes              | Define architecture, generate roadmaps or steps |

Both tools run inside VS Code. A common setup is Codex in one terminal panel (or the Codex web interface) and Claude Code in the extension panel — the Moderator moves between them as each phase advances.

For a full account of the Tech Lead (Codex) side of this setup, see [modw-with-codex.md](modw-with-codex.md).

---

## Best practices

- **Approve `CLAUDE.md` before the first Dev Team session.** A Development Team prompt that lacks correct stack, naming conventions, or build commands will produce output the Moderator cannot safely accept.
- **Do not skip Plan Mode.** The implementation options gate exists to catch misunderstandings before they become diffs. A two-minute plan review is cheaper than a revert.
- **Keep steps narrow.** If `STEP-XX.md` has more than 5–7 acceptance checks, return it to the Tech Lead to split before handing it to Claude Code.
- **Treat the build gate as non-negotiable.** Do not accept a step that did not pass a clean build and test run inside the Claude Code session.
- **Commit before switching agents.** If you hand work from Claude Code back to Codex for review, commit first so Codex reads the actual output.
- **Clean up worktree branches.** After each session, verify leftover `claude/` branches are pruned. One branch per active session is the right state.

---

## Summary

| Phase                    | Agent                          | MOD-W outcome                                        |
| ------------------------ | ------------------------------ | ---------------------------------------------------- |
| **Session start**        | Claude Code (Dev Team)         | Step understood and confirmed                        |
| **Plan Mode**            | Claude Code (Dev Team)         | Implementation approach approved by Moderator        |
| **Implementation**       | Claude Code (Dev Team)         | Step implemented, build gate passed                  |
| **QA**                   | Claude Code SubAgent           | `QA.md` with acceptance check outcomes               |
| **PO validation**        | Claude Code SubAgent           | Product Owner sign-off                               |
| **Tech Lead review**     | Codex (Tech Lead)              | Must-fix / nice-to-have findings in `REVIEW.md`      |
| **Accept**               | Moderator (human)              | Git tag, `ROADMAP.md` advanced                       |

---

MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
