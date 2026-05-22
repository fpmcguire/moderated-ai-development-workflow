# Changelog

All notable changes to the Moderated AI Development Workflow (MOD-W) will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## Version history in brief

Each version of MOD-W addressed a specific problem that the previous version could not:

- **v1** — introduced cross-validation, HITL gates, and role separation to address AI hallucinations and unmoderated output.
- **v2** — expanded roles and artifacts (spec-driven development) to address loss of AI context across sessions and handoffs.
- **v3** — refined the workflow around direct repository access (Codex + Claude Code) to eliminate the time-consuming copy-paste bottleneck.

## [Unreleased]

_No unreleased changes yet._

## [3.0.0] – 2026-05-22

### Added

- Codex as default Tech Lead agent — reads `AGENTS.md` at repo root automatically.
- QA SubAgent and Product Owner SubAgent — Claude Code SubAgents spawned automatically after implementation.
- `prompts/qa.md` — QA SubAgent prompt.
- `articles/modw-with-claude-code.md` — Development Team role guide for Claude Code in VS Code.
- "The workflow must evolve with the tooling" — new core belief in the manifesto.
- Living methodology framing in README — explains MOD-W as a versioned response to evolving AI tooling.

### Changed

- Claude Code is now the sole default Development Team interface — reads `CLAUDE.md` directly, no copy-paste required.
- Direct repository access for both Codex and Claude Code — eliminates the copy-paste context workflow from v2.
- `prompts/tech-lead-chatgpt.md` renamed to `prompts/tech-lead.md`.
- `prompts/product-owner-chatgpt.md` renamed to `prompts/product-owner.md`.
- `docs/moderator-checklist.md` rewritten for the Codex + Claude Code workflow.
- `MOD-W.md` rewritten: roles table, cross-validation diagram, and workflow phases updated for v3.
- `docs/ceremonies.md` Ceremony 3 updated from chatbot-paste to direct repo access workflow.
- `docs/workbench-guide.md` updated — "pull the branch" step removed; Claude Code edits directly.
- License changed from Apache 2.0 to MIT.
- All footers updated to v3.0.0.

### Removed

- ChatGPT references from default role assignments (Product Owner, Tech Lead).
- Chatbot paste interface option for Development Team.

## [2.1.0] – 2026-04-15

### Added

- `CLAUDE.md` template — configures the Development Team role for Claude Code.
- Claude Code as Development Team interface alongside the existing chatbot option.
- Initial Codex integration for the Tech Lead role.

## [2.0.0] – 2026-04-13

### Changed

- Refactored the project structure for improved clarity and maintainability.
- Refactored documentation organization and content for improved clarity.
- Simplified the repository layout to better distinguish core workflow guidance, supporting docs, templates, prompts, and examples.

## [1.1.0] – 2026-04-07

### Added

- Gemini support.

### Changed

- Cleaned and refined the workflow.

## [1.0.0] – 2026-03-26

### Added

- Initial public release of MOD-W (Moderated AI Development Workflow).
- Core docs: manifesto, principles, roles, ceremonies, artifacts, step lifecycle, quality gates, domain language, glossary, FAQ.
- Templates: PRODUCT, ARCHITECTURE, ROADMAP, STEP, REVIEW, QA, DOMAIN_LANGUAGE, AGENTS.
- Prompts: product owner, tech lead, development team, moderator checklist, workbench usage guidelines.
- Example: frontend saved-views feature walkthrough.
- GitHub issue templates and PR template.
- Copilot instructions for AI-assisted contributions.
- Community files: CONTRIBUTING, CODE_OF_CONDUCT, SECURITY, GOVERNANCE.

---

MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
