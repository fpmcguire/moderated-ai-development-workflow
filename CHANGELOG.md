# Changelog

All notable changes to the Moderated AI Development Workflow (MOD-W) will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## Version history in brief

Each version of MOD-W addressed a specific problem that the previous version could not:

- **v1** — introduced cross-validation, HITL gates, and role separation to address AI hallucinations and unmoderated output.
- **v2** — expanded roles and artifacts (spec-driven development) to address loss of AI context across sessions and handoffs.
- **v3** — refined the workflow around direct repository access (Codex + Claude Code) to eliminate the time-consuming copy-paste bottleneck.
- **v4** — introduced Claude Design as the Designer + Prototyper role, the optional Prototype Ceremony, the mandatory Architecture Handoff gate, and the Reference Implementation dispositional concept.

## [Unreleased]

_No unreleased changes yet._

## [4.0.0] – 2026-05-25

### Added

- **Designer + Prototyper role** — Claude Design as the default interface; optional per project; produces `DESIGN-SPEC.md` (authoritative), `prototype/` (research artifact), and `ARCHITECTURE-NOTES.md` (advisory).
- **Prototype Ceremony** — optional kickoff ceremony slotting between Product Definition and Architecture Definition; 9-step Moderator-gated loop with a mandatory cross-validation pause before exit.
- **Architecture Handoff** — mandatory gate when the Prototype Ceremony ran; Codex independently authors `ARCHITECTURE.md` from all four kickoff inputs and has explicit authority to override prototype-implied structures.
- **Reference Implementation** — dispositional concept (not a file); Tech Lead classifies candidate prototype code in `STEP-XX.md` as `Adopt as-is`, `Adopt with modifications`, or `Reject`.
- `prompts/designer.md` — Designer + Prototyper role prompt; promoted to top-level path.
- `docs/prototype-ceremony.md` — complete Prototype Ceremony lifecycle: when to run, inputs, outputs, 9-step gated loop, exit criteria, and anti-patterns.
- `docs/architecture-handoff.md` — Architecture Handoff ceremony doc; non-negotiable gate, Codex authority scope, 8-step lifecycle, material divergence definition.
- `templates/ARCHITECTURE-NOTES.md` — advisory architecture observations template for Prototype Ceremony output.
- `templates/prototype-README.md` — non-authoritative disclaimer template for the `prototype/` folder.
- `templates/MOD-W.md` — project-level workflow quick-reference: roles table, cross-validation diagram, phase overview, operating rules.
- `articles/modw-with-claude-design.md` — integration guide for Claude Design in MOD-W: where it fits, responsibility split, ceremony lifecycle, drift prevention rules.
- Claude Design as optional Dev Team interface for visual, chart, or interaction-heavy Steps (assigned explicitly in `STEP-XX.md §"Assigned Dev Team Interface"`).

### Changed

- `templates/DESIGN-SPEC.md` — v4 rewrite: 10 structured sections including Visual Identity (5 subsections), Accessibility, Component Library with `data-testid` convention, Domain Language Proposals table, Scope Rules.
- `templates/STEP-XX.md` — added `Assigned Dev Team Interface` section (Claude Code default or Claude Design) and `Reference Implementation` section with `Location`, `Disposition`, and `Required Changes` fields.
- `prompts/tech-lead.md` — Planning Session step 1 expanded to include Prototype Ceremony inputs (`DESIGN-SPEC.md`, `prototype/`, `ARCHITECTURE-NOTES.md`); added step 6 (Architecture Handoff) and step 7 (Domain Language ratification from `DESIGN-SPEC.md §"Domain Language Proposals"`).
- `prompts/development-team-claude.md` — opening note expanded with alternate Claude Design interface (v4) and hard authorship-separation rule: Claude Design implementing a Step must not have authored that Step's `STEP-XX.md`.
- `docs/roles.md` — added `### Designer + Prototyper` role section with authoritative/non-authoritative outputs, authority, and constraints; updated Default Tool Implementations; updated Role Summary Table.
- `docs/ceremonies.md` — kickoff restructured as three sequential Moderator-gated phases: 1a Product Definition, 1b Prototype Ceremony (optional, v4), 1c Architecture Definition (with Architecture Handoff `v4 note` when Prototype Ceremony ran).
- `docs/artifacts.md` — added Designer + Prototyper artifacts section (`DESIGN-SPEC.md`, `ARCHITECTURE-NOTES.md`, `prototype/`) and Reference Implementation concept.
- `README.md` — added "Using MOD-W with Claude Design" section; updated kickoff block to three phases; version footer bumped.
- All file footers standardized to `MOD-W v4.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow`.

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

MOD-W v4.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
