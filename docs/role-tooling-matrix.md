# Role-Tooling Matrix

This matrix shows the default tool assignment for each MOD-W role. These are the recommended defaults, not requirements — teams may substitute tools where appropriate.

---

## Default Role-Tool Assignments

| Role | Phase | Interface | Config | Primary artifacts |
| ---- | ----- | --------- | ------ | ----------------- |
| Product Owner | Definition (project start) | Claude chatbot + Perplexity + Gemini | None — no project infrastructure yet | `PRODUCT.md` |
| Product Owner | Validation (per-step) | Claude Code SubAgent | `CLAUDE.md` (auto-loaded) | Acceptance sign-off |
| Tech Lead | Planning + Review | Codex (full session) | `AGENTS.md` (auto-loaded) | `ARCHITECTURE.md`, `ROADMAP.md`, `STEP-XX.md`, `REVIEW.md` |
| Development Team | Implementation | Claude Code SubAgent | `CLAUDE.md` (auto-loaded) | Code, tests, docs |
| QA | Acceptance validation | Claude Code SubAgent | `CLAUDE.md` (auto-loaded) | `QA.md` |
| Moderator | All gates | Human | — | Approvals, git tags |

---

## Cross-Validation Design

The tool split is intentional:

| Boundary | Tools | What it catches |
| -------- | ----- | --------------- |
| Plan vs. implement | Codex (Tech Lead) ↔ Claude Code (Dev Team) | Model-level blind spots — Codex plans, Claude Code implements, Codex reviews |
| Implementation vs. acceptance | Dev Team ↔ QA SubAgent | Context-isolated re-read of the same implementation against acceptance checks |
| Acceptance vs. product intent | QA ↔ Product Owner SubAgent | Validates that passing checks actually satisfy user-facing intent |
| All outputs | Human Moderator | Final authority — approves plans, gates steps, tags releases |

---

## Product Definition Tooling

The Product Definition phase (project start) uses external chatbots because no project agent infrastructure exists yet:

| Tool | Use |
| ---- | --- |
| Claude chatbot (claude.ai) | Draft and iterate on `PRODUCT.md` |
| Perplexity | Research, fact-finding, market and domain context |
| Gemini | Informal cross-validation of scope, goals, and user workflows |

The Moderator drives this phase. All three tools are optional — use what fits the project.

---

## Tech Lead Session Types

Codex runs two session types for the Tech Lead role:

| Session | Trigger | Reads | Writes |
| ------- | ------- | ----- | ------ |
| Planning | Before each Step | `PRODUCT.md`, `ARCHITECTURE.md` | `ARCHITECTURE.md`, `ROADMAP.md`, `STEP-XX.md`, `CLAUDE.md`, `AGENTS.md` |
| Review | After Dev Team build gate | `STEP-XX.md`, implementation diff | `REVIEW.md` |

In the Review session, Tech Lead reads only — no edits to implementation files.

---

## Development Team Build Gate

Before handing off to Tech Lead review, the Dev Team SubAgent runs a blocking build gate:

```
{{BUILD_COMMAND}}   # e.g. npm run build
{{TEST_COMMAND}}    # e.g. npm test
```

These commands are populated by the Tech Lead when generating the project-specific `CLAUDE.md`. The Dev Team cannot proceed until both pass cleanly.

---

MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
