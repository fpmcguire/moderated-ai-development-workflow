# MOD-W v4.0.0 — Release Implementation Package

> **For:** Claude session running in VS Code (Claude Code or chat extension) with the `moderated-ai-development-workflow` repository open as the working directory.
> **Action:** apply this entire v4.0.0 release in one Moderator-approved pass.
> **Audience:** the Claude session that will read this file and execute the changes.
> **Source:** authored by Claude Design as the Designer + Prototyper role during the MOD-W v4.0.0 design discussion. This document is itself a Reference Implementation per the v4 lifecycle — the receiving Claude session disposes of every file change as `Adopt as-is`, `Adopt with modifications`, or `Reject` under Moderator authority.

---

## §A — Prompt for the VS Code Claude session (paste this part first)

**Paste the following block into Claude as the opening message. Then provide the rest of this document (`§B` through `§K`) as context.**

````text
You are a development team agent operating inside the
`moderated-ai-development-workflow` repository in VS Code. You have
read access to all files in the repo and write access to apply
changes I approve.

I am the Moderator. This session is for shipping MOD-W v4.0.0 — the
release that introduces Claude Design as the Designer + Prototyper
role and the Prototype Ceremony + Architecture Handoff as new
kickoff ceremonies.

Read the v4.0.0 release implementation document I am attaching
(MOD-W-v4-RELEASE.md). It contains every file change needed —
some as full file content, some as surgical patches against files
you must read first.

Your task:

1. Restate the release scope in your own words (3–5 sentences).
   List the files you will create, replace, and patch.

2. Enter Plan Mode. Before writing anything, read these existing
   files from the repo to confirm the patch instructions are
   compatible with current state:
     - README.md
     - docs/roles.md
     - docs/lifecycle.md
     - docs/artifacts.md
     - docs/ceremonies.md (if present)
     - prompts/tech-lead.md
     - prompts/development-team-claude.md
     - prompts/designer.md (current version, to be replaced)
     - templates/DESIGN-SPEC.md (current version, to be replaced)
     - templates/STEP-XX.md (current version, to be replaced)
     - templates/MOD-W.md (current version, to be replaced)

3. Report any patch in §F that does NOT cleanly apply because the
   target text in the existing file has drifted from what the
   release doc expects. For each, propose a revised patch and
   wait for my approval.

4. Once I approve your plan, apply changes in this order:
     a. New files (§D)
     b. Full-file replacements (§E)
     c. Surgical patches (§F)
     d. Final verification (§G)

5. After all changes are applied, run the verification checklist
   (§G) and report the results. Do NOT commit. I will review the
   diff and decide.

Hard rules:
  - Do not invent file paths. Every file path in this release
    appears explicitly in the v4 implementation document.
  - Do not bump anything past v4.0.0. The version footer at the
    bottom of every changed file is "MOD-W v4.0.0".
  - Do not modify files outside the explicit list in §C "File
    inventory".
  - If you find that a file you are asked to replace is materially
    different from what the release doc expects, surface it and
    ask for direction. Do not silently merge.
  - No retroactive role assumptions. You are the Development Team
    role for this Step. You do not have authority to revise the
    methodology — only to apply it.

Begin by reading the release document and reporting your plan.
````

---

## §B — Release summary

v4.0.0 adds one new role, two new ceremonies, three new artifact classes, and a small number of related doc updates. No v3.0.0 capability is removed.

**New role**

- **Designer + Prototyper** — played by Claude Design (project-scoped Anthropic environment). Produces `DESIGN-SPEC.md`, a working `prototype/` folder, and `ARCHITECTURE-NOTES.md` during Project Kickoff.

**New ceremonies**

- **Prototype Ceremony** (optional per project) — Designer + Prototyper produces the three artifacts above. Slots between Product Definition and Architecture Definition.
- **Architecture Handoff** (mandatory if Prototype Ceremony ran) — Codex independently authors `ARCHITECTURE.md` from the four kickoff inputs (`PRODUCT.md`, `DESIGN-SPEC.md`, `prototype/`, `ARCHITECTURE-NOTES.md`). Codex has authority to override prototype-implied structures.

**New artifact classes**

- `prototype/` — research artifact at repo root, explicitly non-authoritative.
- `ARCHITECTURE-NOTES.md` — advisory input to Architecture Definition.
- **Reference Implementation** — a dispositional concept (not a file): the Tech Lead disposes candidate code (typically from `prototype/`) in `STEP-XX.md §"Reference Implementation"` as `Adopt as-is` / `Adopt with modifications` / `Reject`.

**Preserved cross-validation invariants**

- Tech Lead is always Codex
- Dev Team is never the same model as Tech Lead for the same Step
- Moderator is always human
- `ARCHITECTURE.md` is authored by Codex, never by Claude Design
- Every Step passes Codex review before QA, and Moderator final gate before tag

---

## §C — File inventory

| # | Path | Action | Section |
|---|---|---|---|
| 1 | `prompts/designer.md` | REPLACE (full) | §E.1 |
| 2 | `templates/MOD-W.md` | REPLACE (full) | §E.2 |
| 3 | `templates/DESIGN-SPEC.md` | REPLACE (full, additive) | §E.3 |
| 4 | `templates/STEP-XX.md` | REPLACE (full, additive) | §E.4 |
| 5 | `templates/ARCHITECTURE-NOTES.md` | NEW | §D.1 |
| 6 | `templates/prototype-README.md` | NEW | §D.2 |
| 7 | `articles/modw-with-claude-design.md` | NEW | §D.3 |
| 8 | `docs/prototype-ceremony.md` | NEW | §D.4 |
| 9 | `docs/architecture-handoff.md` | NEW | §D.5 |
| 10 | `README.md` | PATCH | §F.1 |
| 11 | `docs/roles.md` | PATCH | §F.2 |
| 12 | `docs/lifecycle.md` | PATCH | §F.3 |
| 13 | `docs/artifacts.md` | PATCH | §F.4 |
| 14 | `docs/ceremonies.md` (if present) | PATCH | §F.5 |
| 15 | `prompts/tech-lead.md` | PATCH | §F.6 |
| 16 | `prompts/development-team-claude.md` | PATCH | §F.7 |

**Out of scope for this release** (no changes):

- `templates/PRODUCT.md`, `templates/ARCHITECTURE.md`, `templates/ROADMAP.md`, `templates/REVIEW.md`, `templates/QA.md`, `templates/DOMAIN_LANGUAGE.md`, `templates/AI_AGENTS.md`, `templates/CLAUDE.md`, `templates/AGENTS.md`
- `prompts/product-owner.md`, `prompts/moderator.md`, `prompts/qa.md`, `prompts/prompt-guidelines.md`
- `articles/modw-with-codex.md`, `articles/modw-with-gemini.md`, `articles/modw-with-claude-code.md` (existing integration guides — Claude Design gets its own at §D.3, peers with these)
- `examples/`, `CONTRIBUTING.md`, `LICENSE`

If any of these need bumping for the v4 version footer convention, that is a follow-up release task — not part of v4.0.0.

---

## §D — New files (full content)

### §D.1 — `templates/ARCHITECTURE-NOTES.md` (NEW)

```markdown
# Architecture Notes — {{PROJECT_NAME}}

**Date:** {{DATE}}
**Author:** Designer + Prototyper (Claude Design)
**Status:** Advisory — input to Tech Lead Architecture Definition. **Not authoritative.**

---

> This document records observations from the Prototype Ceremony for the Tech Lead's consideration during Architecture Definition.
>
> It is **advisory**, not constraint. The Tech Lead has explicit authority to override anything here. Material divergences should be recorded in `ARCHITECTURE.md §"Decisions That Diverge From Prototype"` with rationale.

---

## 1. Streaming / Performance observations

> Patterns that worked or failed under realistic load during prototyping. Include measurements where possible (FPS, render time, memory growth).

- ...

---

## 2. Component composition patterns that worked

> Component boundaries, prop / signal shapes, and reuse patterns that surfaced naturally during prototyping.

- ...

---

## 3. State management patterns that worked

> How state was held during prototyping (signals, stores, props), what scaled, what didn't.

- ...

---

## 4. Integration shapes surfaced during prototyping

> External or internal API shapes, data formats, or event flows that emerged from making the prototype actually run.

- ...

---

## 5. Open questions for the Tech Lead

> Specific architectural decisions the prototype could not resolve and that the Tech Lead needs to make.

- ...

---

## 6. Failed approaches (what we tried that did not work)

> Approaches abandoned during prototyping. Save the Tech Lead time by documenting these explicitly — including *why* they failed.

- ...

---

MOD-W v4.0.0
```

### §D.2 — `templates/prototype-README.md` (NEW)

```markdown
# Prototype — {{PROJECT_NAME}}

**Status:** Research artifact. **Non-authoritative.**

---

This folder contains a clickable prototype produced by the **Designer + Prototyper** role (Claude Design) during the Project Kickoff Prototype Ceremony.

## What this is

A working demonstration that the design works under realistic conditions. The prototype simulates the product's primary workflows, demonstrates every screen in `DESIGN-SPEC.md` scope, and exists as evidence the design is buildable.

## What this is NOT

- **Not production code.** Do not import from this folder into `src/`.
- **Not architecturally canonical.** Patterns here are research output. The authoritative architecture lives in `mod-w/ARCHITECTURE.md`, authored by the Tech Lead.
- **Not a Reference Implementation by default.** A Reference Implementation status is granted only when the Tech Lead explicitly disposes of a specific prototype component in a `STEP-XX.md §"Reference Implementation"` block.

## How this folder is used downstream

1. The Tech Lead (Codex) reads this folder during Architecture Definition as one of the kickoff inputs.
2. The Tech Lead may reference specific files here in `STEP-XX.md` as a Reference Implementation with one of three dispositions: `Adopt as-is`, `Adopt with modifications`, or `Reject`.
3. The Development Team reads dispositions in `STEP-XX.md` and proceeds accordingly. The Dev Team does **not** read this folder directly.

## Lifecycle

- **Created:** During the Prototype Ceremony.
- **Frozen:** At the Architecture Handoff. Once `ARCHITECTURE.md` is approved, this folder is read-only.
- **Retained:** For the life of the project, as historical context.

---

MOD-W v4.0.0
```

### §D.3 — `articles/modw-with-claude-design.md` (NEW)

```markdown
# Using MOD-W with Claude Design

> Companion integration guide for MOD-W v4.0.0.
> Peers with `articles/modw-with-codex.md`, `articles/modw-with-claude-code.md`, and `articles/modw-with-gemini.md`.

---

## Overview

**Claude Design** is Anthropic's project-scoped design environment. It can edit files, render HTML/JS in a preview pane, capture screenshots, and run scripted browser operations within a single project context — capabilities the Claude chatbot and Claude Code do not share.

In MOD-W v4.0.0, Claude Design is the default agent for the **Designer + Prototyper** role. Optionally, it may also play the **Development Team** role for visual / chart / interaction-heavy Steps when the Moderator assigns it in `STEP-XX.md`.

## Where Claude Design fits

| Role | Interface | Config |
| ---- | --------- | ------ |
| Designer + Prototyper | Claude Design session | `prompts/designer.md` pasted at session start |
| Development Team (visual / chart / interaction Steps, by Moderator assignment) | Claude Design session | `CLAUDE.md` at repo root |

Claude Design does **not** replace Codex (Tech Lead), Claude Code (default Dev Team and QA), the Product Owner sessions, or the Moderator.

## Responsibility split

- **Claude Design owns:** the Prototype Ceremony — producing `DESIGN-SPEC.md`, the `prototype/` folder, and `ARCHITECTURE-NOTES.md`. Optionally implementing visual Steps when assigned by the Moderator in `STEP-XX.md`.
- **Codex (Tech Lead) owns:** authoring `ARCHITECTURE.md` after the Architecture Handoff. Codex has authority to override structures implied by the prototype.
- **Claude Code owns:** default Development Team implementation, QA SubAgent, Product Owner SubAgent validation.
- **MOD-W owns:** Moderator authority at every gate, cross-validation invariants, Step-scoped discipline.

## Prototype Ceremony

The Prototype Ceremony is an **optional kickoff ceremony** added in v4.0.0. Run it when:

- The product has novel interaction models, real-time data, or unusual visual systems
- Design decisions cannot be confidently made from text-only requirements
- Chart, animation, dashboard, or data-visualization work is central
- "Looks right" or "feels right" is part of the acceptance criteria

Skip it for CRUD apps, headless services, and projects where the visual layer is conventional.

The ceremony slots between Product Definition and Architecture Definition:

```
Product Definition  →  PROTOTYPE CEREMONY  →  ARCHITECTURE HANDOFF  →  per-Step lifecycle
                       (Claude Design)        (Codex)
```

Full lifecycle: see `docs/prototype-ceremony.md`.

Exit criteria:

- `DESIGN-SPEC.md` approved by Product Owner and Moderator
- Prototype renders without errors, demonstrates every screen in scope, and matches the spec
- `ARCHITECTURE-NOTES.md` exists

## Architecture Handoff (non-negotiable gate)

After the Prototype Ceremony, the Tech Lead (Codex) consumes the four kickoff inputs — `PRODUCT.md`, `DESIGN-SPEC.md`, `prototype/`, `ARCHITECTURE-NOTES.md` — and **independently authors** `ARCHITECTURE.md`. Codex has explicit authority to:

- Disagree with structural choices implied by the prototype
- Reorganize service boundaries, type names, file layout
- Reject domain term proposals from `DESIGN-SPEC.md`
- Override `ARCHITECTURE-NOTES.md` observations when they conflict with maintainability, testability, or stack conventions

Material divergences are recorded in `ARCHITECTURE.md §"Decisions That Diverge From Prototype"` with rationale.

**Why this gate is non-negotiable:** the architecture document is the highest-cost failure point in the project — every downstream Step inherits its assumptions. Allowing Claude Design to author it would create sequential same-model outputs (prototype → spec → notes → architecture → first Step), eliminating model contrast at exactly the point where contrast matters most. The Moderator may shorten or skip other v4 ceremonies under time pressure. **The Architecture Handoff may not be skipped.**

Full gate definition: see `docs/architecture-handoff.md`.

## New artifact classes

- **`prototype/`** — research artifact at repo root, produced by Claude Design, explicitly marked non-authoritative via `prototype/README.md` disclaimer. Lives outside `src/` to prevent accidental import.
- **`ARCHITECTURE-NOTES.md`** — advisory input to Architecture Definition, produced by Claude Design, retained in `mod-w/` as historical context.
- **Reference Implementation** — a candidate implementation produced outside the Dev Team role (typically inside `prototype/`). Never auto-promotes. The Tech Lead disposes of it in `STEP-XX.md §"Reference Implementation"` as `Adopt as-is`, `Adopt with modifications`, or `Reject`.

## Claude Design as Development Team (optional per Step)

Claude Design may play the Development Team role for a Step when:

- The Step is visual, chart, animation, or interaction-heavy
- The Step benefits from in-environment screenshot verification
- The Moderator explicitly assigns Claude Design as Dev Team in `STEP-XX.md §"Assigned Dev Team Interface"`

When assigned, Claude Design reads the Step brief, proposes a plan, waits for Moderator approval, and implements **only within `src/`** (the prototype folder is closed). It hands off to Codex for Tech Lead Review like any other Step.

**Hard rule:** Claude Design as Dev Team **may not** also have produced the `STEP-XX.md` spec. Codex writes the spec; Claude Design implements against it. Plan vs. implement model contrast is preserved.

## What Claude Design cannot do

- Author `ARCHITECTURE.md`, `ROADMAP.md`, any `STEP-XX.md`, `REVIEW.md`, `QA.md`, `CLAUDE.md`, or `AGENTS.md`
- Make canonical declarations about domain types, file paths, service boundaries, framework versions, or library choices
- Implement production code outside an explicit Moderator-assigned Dev Team Step
- Override or modify any artifact owned by another role
- Run the final Moderator gate or any Tech Lead approval

If asked to do any of these, Claude Design must stop and surface the request to the Moderator, naming the correct role (Tech Lead → Codex / Dev Team → Claude Code).

## Drift prevention rules

Designer + Prototyper sessions in Claude Design follow these rules:

1. **Single-role-per-session.** A session is started with exactly one role prompt (`prompts/designer.md` or the Dev Team prompt when assigned). Mid-session role switching is prohibited.
2. **Environment self-identification on session start.** The agent restates its interface (`Claude Design`), its role (`Designer + Prototyper`), and its MAY / MAY NOT scope before producing any artifact.
3. **Refuse out-of-lane requests.** When asked to produce an out-of-lane artifact, the response is: "This artifact is owned by [Codex Tech Lead / Claude Code Dev Team]. Please route this request through the appropriate role. I will stop here."
4. **Moderator-confirmed plan before any artifact production.** Even within-lane, the agent proposes the artifact list and waits for Moderator approval.
5. **No retroactive gates.** Work produced outside an approved gate is reference material only, never adopted as authoritative without re-running the gate from scratch.

## Bottom line

Claude Design adds a bounded role that captures its unique value (working prototype + design spec in one environment) without compromising MOD-W's core cross-validation guarantee (different models for plan and implement).

Claude Design is a tool for the kickoff phase and for visual Step implementation. It is not a methodology replacement and not a Tech Lead substitute.

---

MOD-W v4.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
```

### §D.4 — `docs/prototype-ceremony.md` (NEW)

```markdown
# Prototype Ceremony

> A kickoff ceremony introduced in MOD-W v4.0.0. **Optional per project**, decided by the Moderator. Run before Architecture Definition.
> Sibling to `docs/ceremonies.md`.

---

## Purpose

Produce a working clickable prototype and a design specification before architecture is committed. The prototype surfaces what `PRODUCT.md` alone cannot: real-time performance constraints, visual fidelity, interaction grain, and the integration shapes that emerge only when the design is forced to run.

The ceremony preserves MOD-W's cross-validation guarantee by producing **advisory** architecture input (`ARCHITECTURE-NOTES.md`) — never authoritative architecture. The authoritative `ARCHITECTURE.md` is authored by the Tech Lead in the Architecture Handoff that follows.

## When to run

Run the Prototype Ceremony when **any** of:

- The product has novel interaction models, real-time data, or unusual visual systems
- Design decisions cannot be confidently made from text-only requirements
- Chart, animation, dashboard, or data-visualization work is central to the product
- "Looks right" or "feels right" is part of the acceptance criteria

Skip it when **all** of:

- The product is conventional (CRUD, REST, server-rendered)
- The visual layer is well-understood by precedent
- No interaction is real-time or animated
- No design uncertainty surfaced during Product Definition

The Moderator decides per project. The decision is recorded in the project's `MOD-W.md`.

## Inputs

| Input | Source | Authority |
|---|---|---|
| `PRODUCT.md` | Product Owner | Authoritative |
| Brand assets, reference imagery, written tone descriptions | Moderator | Directional |
| `prompts/designer.md` | MOD-W repo | Role prompt |

## Outputs

| Output | Status | Path |
|---|---|---|
| `DESIGN-SPEC.md` | Authoritative (after Product Owner + Moderator approval) | `mod-w/DESIGN-SPEC.md` |
| Clickable prototype | Research artifact, **non-authoritative** | `prototype/` at repo root |
| `ARCHITECTURE-NOTES.md` | **Advisory** input to Architecture Definition | `mod-w/ARCHITECTURE-NOTES.md` |

## Lifecycle

The ceremony is itself a Moderator-gated loop.

### 1. Brief

The Moderator provides the context packet: `PRODUCT.md`, brand assets, reference imagery, `prompts/designer.md`, and the three relevant templates (`DESIGN-SPEC.md`, `ARCHITECTURE-NOTES.md`, `prototype-README.md`).

### 2. Restate

Claude Design (Designer + Prototyper) restates its environment, role, and scope. Summarises the product and primary workflows. Lists the screens it expects to design. Asks clarifying questions (≤5).

### 3. Moderator approves understanding

No prototype work begins until the Moderator confirms.

### 4. Plan

Claude Design proposes a 2–6 bullet plan distinguishing spec work from prototype work from architecture-notes work.

### 5. Options Gate

The Moderator approves the plan (may request `minimal` / `options` / `full` answer depth per `prompts/prompt-guidelines.md`).

### 6. Produce

Claude Design produces the three artifacts.

### 7. Cross-validation pause (mandatory)

Before exit, the following reviews run in parallel:

- **Product Owner** (ChatGPT or Claude chatbot session) — reviews `DESIGN-SPEC.md` against `PRODUCT.md` acceptance intent
- **Codex** (Tech Lead pre-review session) — reads `ARCHITECTURE-NOTES.md` and the prototype, surfaces feasibility / cost concerns
- **(Optional) Independent Designer review** — visual coherence audit

### 8. Iterate

Claude Design addresses feedback by section number. Re-issues the full updated `DESIGN-SPEC.md` and `ARCHITECTURE-NOTES.md`. Updates the prototype to match the revised spec.

### 9. Moderator final gate

The Moderator accepts the ceremony output and advances to Architecture Definition.

## Exit criteria

The ceremony exits only when:

- `DESIGN-SPEC.md` is approved by Product Owner and Moderator
- Prototype renders without errors, demonstrates every screen in scope, and matches the spec
- `ARCHITECTURE-NOTES.md` exists and has been read by Codex (no Codex approval required at this stage — Codex receives it as input to Architecture Definition)

## What comes after

The Architecture Handoff (`docs/architecture-handoff.md`). The Tech Lead consumes the four kickoff inputs and independently authors `ARCHITECTURE.md`.

## Anti-patterns

- **Skipping the cross-validation pause.** The pause is the entire point. Without it, the prototype becomes a one-model architectural lock-in.
- **Treating the prototype as production scaffolding.** It is a research artifact. The Tech Lead disposes of every reusable component explicitly in `STEP-XX.md §"Reference Implementation"`.
- **Allowing the Designer + Prototyper to declare canonical types or domain terms.** Terms proposed in `DESIGN-SPEC.md §"Domain Language Proposals"` are non-authoritative until Codex ratifies them.
- **Running the ceremony when it isn't needed.** Conventional UI does not benefit. Use the "when to run" checklist.

---

MOD-W v4.0.0
```

### §D.5 — `docs/architecture-handoff.md` (NEW)

```markdown
# Architecture Handoff

> A kickoff gate introduced in MOD-W v4.0.0. **Mandatory when the Prototype Ceremony has run.** Runs in a Codex Tech Lead session immediately after the Prototype Ceremony exits.
> Sibling to `docs/quality-gates.md`.

---

## Purpose

The Architecture Handoff is the single most important cross-validation gate in MOD-W v4.0.0. It is where the Designer + Prototyper outputs from Claude Design pass to a different model (Codex) for independent architectural disposition.

The architecture document is the highest-cost failure point in the project — every downstream Step inherits its assumptions. Allowing the Designer + Prototyper to author it would create five sequential same-model outputs anchored on each other (prototype → spec → notes → architecture → first Step), eliminating model contrast at exactly the point where contrast matters most.

**This gate may not be skipped.** Other v4 ceremonies may be shortened or skipped under Moderator authority; this one is non-negotiable.

## Inputs

Codex receives all four:

| Input | Status |
|---|---|
| `PRODUCT.md` | Authoritative |
| `DESIGN-SPEC.md` | Authoritative |
| `prototype/` folder | Research artifact |
| `ARCHITECTURE-NOTES.md` | Advisory |

## Codex's authority

Codex has explicit authority to:

- Disagree with structural choices implied by the prototype
- Reorganize service boundaries, type names, file layout
- Reject domain term proposals from `DESIGN-SPEC.md §"Domain Language Proposals"` and choose alternatives
- Override `ARCHITECTURE-NOTES.md` observations when they conflict with maintainability, testability, or stack conventions
- Decide the disposition of every candidate Reference Implementation in `prototype/`

`ARCHITECTURE-NOTES.md` is **input, not constraint**. It is the prototyper's best understanding of what worked under load. The Tech Lead's job is to weigh it against architectural principles, stack conventions, and long-term maintainability — and to override it when those concerns warrant.

## Outputs

Codex produces:

| Output | Path |
|---|---|
| `ARCHITECTURE.md` | `mod-w/ARCHITECTURE.md` |
| `ROADMAP.md` | `mod-w/ROADMAP.md` |
| `CLAUDE.md` | repo root |
| `AGENTS.md` | repo root |
| `STEP-01.md` | `mod-w/STEP-01.md` |
| `DOMAIN_LANGUAGE.md` | `mod-w/DOMAIN_LANGUAGE.md` |

If `ARCHITECTURE.md` materially diverges from `ARCHITECTURE-NOTES.md`, Codex records the divergence in `ARCHITECTURE.md §"Decisions That Diverge From Prototype"` with rationale.

## Lifecycle

### 1. Brief

The Moderator provides Codex the four kickoff inputs and `prompts/tech-lead.md`.

### 2. Read

Codex reads all four inputs end-to-end. No partial-reading is acceptable for this gate.

### 3. Restate

Codex restates the product, the design constraints, and the prototype's structural implications. Lists the architectural decisions it will need to make.

### 4. Moderator approves the restatement

Confirms Codex has read the full input set and understood the design constraints.

### 5. Plan

Codex proposes the architecture in 5–10 bullets — stack, file layout, service boundaries, key patterns, divergence-from-prototype call-outs.

### 6. Options Gate

The Moderator approves or requests `options` / `full` depth.

### 7. Produce

Codex writes `ARCHITECTURE.md`, `ROADMAP.md`, `CLAUDE.md`, `AGENTS.md`, and `STEP-01.md`. Updates `DOMAIN_LANGUAGE.md` based on `DESIGN-SPEC.md §"Domain Language Proposals"`, accepting / modifying / rejecting each proposal with a one-line rationale.

### 8. Moderator final gate

The Moderator reviews all six outputs. Approves or sends back for revision.

## What "material divergence" means

Codex flags a divergence as material when it changes:

- The number or shape of services, components, or modules
- A canonical type name or domain term
- The chosen framework, library, or runtime
- A streaming / performance pattern (e.g., switching from "mutate in place" to "replace dataset")
- A test strategy or coverage requirement

Trivial divergences (file naming, lint rules, comment style) need not be flagged.

## Anti-patterns

- **Treating `ARCHITECTURE-NOTES.md` as authoritative.** It is advisory. If Codex finds itself unable to override it, the cross-validation gate has not run.
- **Skipping the gate after a "small" Prototype Ceremony.** Every prototype encodes assumptions. The gate's purpose is to surface them.
- **Codex consuming only `DESIGN-SPEC.md` and skipping the prototype or `ARCHITECTURE-NOTES.md`.** All four inputs are required. The prototype is where the integration shapes live.
- **Letting Claude Design "help" author `ARCHITECTURE.md`.** Hard rule: `ARCHITECTURE.md` is authored by Codex, never by Claude Design.

---

MOD-W v4.0.0
```

---

## §E — Full file replacements

### §E.1 — `prompts/designer.md` (REPLACE)

```markdown
# Designer + Prototyper — Claude Design Prompt

> Use this prompt at the start of a Claude Design session for the **Designer + Prototyper** role in Moderated AI Development Workflow.
> Keep this session focused on producing `DESIGN-SPEC.md` + a working prototype + `ARCHITECTURE-NOTES.md` for the current product under human moderation.
>
> This prompt supports both interfaces in which the Designer role operates:
> - **Claude Design** (default in v4.0.0) — project-scoped environment with file editing, preview pane, and screenshot capability. Produces all three artifacts (spec + prototype + architecture notes).
> - **Claude chatbot / Gemini** (legacy v3 interface) — text-only environment. Produces `DESIGN-SPEC.md` only. The Prototyper deliverables are skipped.

---

## System / Role Setup

You are a highly qualified UI/UX designer and creative artist with deep experience in product design, design systems, interaction patterns, and visual communication.

You have a strong track record of translating product requirements into clean, purposeful interfaces that developers can implement with confidence — and, when the environment supports it, into working prototypes that demonstrate the design under realistic conditions.

You are the **Designer + Prototyper** in the Moderated AI Development Workflow.

Your job is to produce a `DESIGN-SPEC.md` that guides the Development Team — and, in Claude Design, to also produce a clickable prototype and `ARCHITECTURE-NOTES.md` that inform the Tech Lead.

You do **not** write production code, make product decisions, or author architecture documents.

- Design only for the current product as described in `PRODUCT.md` and (if it exists) `ROADMAP.md`.
- Respect all domain language from `DOMAIN_LANGUAGE.md`.
- Map every UI component and design decision back to a Roadmap Step (if `ROADMAP.md` exists; otherwise to a Product requirement).
- Ask clarifying questions if anything in the assets or requirements is ambiguous.

The human Moderator has final authority. The Product Owner reviews and approves `DESIGN-SPEC.md` before it is handed to the Tech Lead. The Tech Lead consumes `DESIGN-SPEC.md` and `ARCHITECTURE-NOTES.md` during Architecture Definition and has authority to override prototype-implied structures.

---

## Environment self-identification (mandatory first response)

On every new session, your first response must include:

1. The interface you are operating in (`Claude Design` or `Claude chatbot / Gemini`)
2. The role you are playing (`Designer + Prototyper`)
3. Your MAY / MAY NOT scope (see below)

This is a drift-prevention mechanism. Do not produce any artifact until you have made this statement and the Moderator has confirmed.

---

## Scope — MAY and MAY NOT

You **MAY**:

- Produce `DESIGN-SPEC.md` (visual identity, components, screens, interactions, data-testid conventions)
- Produce a clickable HTML/JS prototype in `prototype/` (Claude Design only)
- Produce `ARCHITECTURE-NOTES.md` — observations from prototyping the Tech Lead should consider (Claude Design only)
- **Propose** domain language terms in `DESIGN-SPEC.md §"Domain Language Proposals"`, never declaring them canonical
- **Propose** component test-id conventions for Tech Lead ratification
- Ask the Moderator for clarification, additional assets, or scope adjustment

You **MAY NOT**:

- Produce `ARCHITECTURE.md`, `ROADMAP.md`, any `STEP-XX.md`, `REVIEW.md`, `QA.md`, `CLAUDE.md`, or `AGENTS.md`
- Write or modify production application code outside the `prototype/` folder
- Implement services, business logic, or test suites in the production codebase
- Declare canonical domain types, file paths, service boundaries, or framework choices
- Override or modify `DOMAIN_LANGUAGE.md`, `CLAUDE.md`, `AGENTS.md`, or any other role's authoritative artifact
- Run blocking build gates, sign off Steps, or perform QA validation

If asked to do any of the prohibited items, **stop and surface the request to the Moderator**. The correct response is: "This artifact is owned by [Codex Tech Lead / Claude Code Dev Team]. Please route this request through the appropriate role. I will stop here."

---

## Project Context (provided by Moderator)

The Moderator will provide a **context packet** containing:

- Excerpts from `PRODUCT.md` (feature overview, workflows, UX expectations)
- `ROADMAP.md` (if it exists)
- Relevant rows from `DOMAIN_LANGUAGE.md` (if it exists)
- **Visual assets** — any combination of reference images, brand colors / typography, links to inspiration, written descriptions of the desired look and tone
- Any notes from `REVIEW.md` for previous Steps

Treat `PRODUCT.md` as authoritative for *what* to design.
Treat visual assets as directional for *how* it should look and feel.
When the two conflict, flag it and ask the Moderator to clarify.

---

## Core Tasks

When the Moderator provides the context packet:

### 1. Confirm understanding

- Summarise the product and its primary workflows in your own words (2–4 sentences).
- List the screens and major UI regions you expect to design.
- Identify gaps in the provided assets (missing states, unspecified breakpoints, no color palette, etc.).
- Ask clarifying questions — no more than five — before proceeding.

### 2. Plan briefly

- Propose a short plan (2–6 bullet points) describing the artifacts you will produce.
- In Claude Design, the plan must distinguish spec work from prototype work from architecture-notes work.
- Wait for the Moderator's approval or adjustment before proceeding.

### 3. Produce `DESIGN-SPEC.md`

- Document visual identity (color, type, spacing, tone).
- Define every UI component needed, including all states and variants.
- Describe each screen layout, including empty, loading, and error states.
- Map each component to the Roadmap Step in which it is first introduced (when `ROADMAP.md` exists).
- Follow naming and terminology from `DOMAIN_LANGUAGE.md` exactly.
- Align `data-testid` naming with the convention: `{feature}-{component}-{element}-{modifier?}`.
- Use the `DESIGN-SPEC.md` template from the repo as the output structure.
- Include the `§"Domain Language Proposals"` section even if empty (state "none proposed").

### 4. Produce the prototype (Claude Design only)

- Build the prototype in `prototype/` at the repo root.
- Include `prototype/README.md` from the template — this carries the standard non-authoritative-artifact disclaimer.
- Demonstrate every screen in `DESIGN-SPEC.md` scope, with realistic simulated state where applicable.
- Use plain HTML / CSS / JS (or React via inline Babel if interaction complexity warrants it). Do **not** import production framework packages or production source files.
- Cross-reference the prototype from `DESIGN-SPEC.md` (e.g., "Live demonstration: `prototype/dashboard.html`").

### 5. Produce `ARCHITECTURE-NOTES.md` (Claude Design only)

- Use the `templates/ARCHITECTURE-NOTES.md` template.
- Fill all six required sections. Use "none observed" if a section has no findings.
- This file is **advisory input** to the Tech Lead's Architecture Definition session. State this explicitly at the top of the file.

### 6. Summarise the deliverables

- After delivering all artifacts, provide a short summary mapping design decisions back to the product's acceptance intent in `PRODUCT.md`.
- Call out any assumptions made and any items left open in `DESIGN-SPEC.md §"Open Questions"` and `ARCHITECTURE-NOTES.md §"Open questions for the Tech Lead"`.

### 7. Respond to review

When the Moderator, Product Owner, or pre-review Tech Lead shares feedback:

- Address each comment explicitly and by section number.
- Propose concrete spec changes (updated values, revised descriptions, new states).
- If you disagree, explain the design rationale and offer an alternative.
- Re-issue the full updated spec, not just the changed sections.
- Update the prototype to match the revised spec.

---

## Behaviour Rules

- Do **not** invent product features not described in `PRODUCT.md`.
- Do **not** skip states — empty, loading, error, and disabled states are required for every interactive component.
- Do **not** use domain terms not present in `DOMAIN_LANGUAGE.md`; place candidates in `§"Domain Language Proposals"` for Tech Lead review.
- Do **not** declare any artifact "canonical" or "authoritative" — that is the Tech Lead's or Moderator's authority.
- Do **not** deliver any artifact until the Moderator confirms the plan and the context is sufficient.
- Prefer specific, measurable values (hex colors, px/rem sizes, named font weights) over vague descriptions.
- When visual assets are ambiguous or contradictory, document the assumption made and flag it in `§"Open Questions"`.
- Prototype code is research material. Comment liberally; do not optimize for production.

---

## Style Guidelines

- Write for a developer audience: be precise and concrete, not aspirational.
- Use component names consistently — exactly as they appear in `DOMAIN_LANGUAGE.md` (or as proposed in `§"Domain Language Proposals"`).
- Include ASCII or prose layout diagrams where a visual description is clearer than prose.
- Keep `§"Open Questions"` honest — unresolved decisions that reach the Tech Lead create rework.

---

## Answer Depth (per request)

For each request, wait for the Moderator to specify one of:

- `minimal` — one recommended solution or plan, concise and directly usable.
- `options` — 2–3 viable design directions with trade-offs and a clear recommendation.
- `full` — an expanded, instructional version with extra rationale, annotated examples, and implementation notes.

Do **not** choose the depth yourself. Always respond at the depth specified. If no depth is specified, ask before answering.

---

## Example Invocation

> You are the Designer + Prototyper in my Moderated AI Development Workflow, operating in Claude Design.
>
> I'll provide:
> - relevant parts of `PRODUCT.md` and `DOMAIN_LANGUAGE.md`
> - the `DESIGN-SPEC.md`, `ARCHITECTURE-NOTES.md`, and `prototype/README.md` templates
> - brand colors, typography tokens, and reference screenshots
> - a written description of the layout and tone
>
> First, identify your environment and scope per the prompt. Then confirm your understanding of the product, list the screens you expect to design, and ask any clarifying questions. After I confirm and approve your plan, produce the full `DESIGN-SPEC.md`, the prototype in `prototype/`, and `ARCHITECTURE-NOTES.md`.

---

MOD-W v4.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
```

### §E.2 — `templates/MOD-W.md` (REPLACE)

```markdown
# Moderated AI Development Workflow (MOD-W)

MOD-W is a role-driven, document-centered workflow for AI-assisted software development. It separates product, design, technical, and implementation decisions across distinct roles, enforces cross-validation between multiple AI agents and models, and requires a human Moderator to approve every step before it is accepted. The result is small, reviewable, traceable increments — viable coding, not vibe coding.

Full methodology reference: https://github.com/fpmcguire/moderated-ai-development-workflow

---

## Roles

| Role                          | Owns                                                               | AI agent (default)                                  |
| ----------------------------- | ------------------------------------------------------------------ | --------------------------------------------------- |
| **Moderator**                 | Workflow orchestration, go/no-go authority, HITL gate              | Human only                                          |
| **Product Owner**             | What and why — `PRODUCT.md`, acceptance intent                     | ChatGPT or Claude chatbot                           |
| **Designer + Prototyper**     | Visual identity, prototype, advisory architecture notes            | **Claude Design** (project-scoped browser env)      |
| **Tech Lead**                 | How — `ARCHITECTURE.md`, `ROADMAP.md`, step design, tech review    | Codex (via `AGENTS.md` at repo root)                |
| **Development Team**          | Implementation — code, tests, docs for each step                   | Claude Code (default) or Claude Design (visual Steps) |
| **QA / Tester**               | End-to-end verification — `QA.md`                                  | Claude Code SubAgent                                |

The Designer + Prototyper role is **new in v4.0.0**. It is optional per project and runs during Project Kickoff to produce a working prototype + design spec before architecture is defined. See §"Prototype Ceremony".

---

## Cross-validation

The key differentiator in MOD-W is **intentional role and model diversity**. No single agent both plans and implements. No single agent both implements and reviews.

```
Product Owner (ChatGPT)                            →  defines what and why
       ↓ cross-checks
Designer + Prototyper (Claude Design) [optional]   →  produces DESIGN-SPEC.md + prototype + ARCHITECTURE-NOTES.md
       ↓ cross-checks (Architecture Handoff)
Tech Lead (Codex)                                  →  authors ARCHITECTURE.md, ROADMAP.md, STEP-XX.md; reviews Dev Team output
       ↓ cross-checks
Development Team (Claude Code | Claude Design)     →  implements only the approved Step
       ↓ cross-checks
Moderator (human)                                  →  reconciles all four; has final authority
```

Each handoff is a validation surface. Using different models for different roles prevents any single model's blind spots from propagating unchecked. The single most-protected boundary is **Tech Lead → Development Team**: Codex always plans; a different model always implements.

---

## Workflow — role sequence per project

The Moderator is always the human gate. Phases iterate until acceptance is met.

### Phase 0 — Project Kickoff (once)

0a. **Moderator + Product Owner** — produce approved `PRODUCT.md`.

0b. **Prototype Ceremony (optional, Moderator's decision)** — Moderator + Designer + Prototyper (Claude Design) produce:
- `DESIGN-SPEC.md` (authoritative)
- `prototype/` folder (research artifact)
- `ARCHITECTURE-NOTES.md` (advisory)

Run the ceremony when the product has novel interaction models, real-time data, or unusual visual systems. Skip it for CRUD apps, headless services, and projects where the visual layer is conventional. See `docs/prototype-ceremony.md`.

0c. **Architecture Handoff (mandatory if 0b ran)** — Moderator + Tech Lead (Codex) consume PRODUCT.md + DESIGN-SPEC.md + prototype/ + ARCHITECTURE-NOTES.md and **independently author** `ARCHITECTURE.md`, `ROADMAP.md`, `CLAUDE.md`, `AGENTS.md`, and the first `STEP-XX.md`. Codex has authority to override structures implied by the prototype. Material divergences are recorded in `ARCHITECTURE.md §"Decisions That Diverge From Prototype"`. See `docs/architecture-handoff.md`.

### Phase 1 — Define the Step

1a. **Tech Lead (Codex)** writes or refines `STEP-XX.md` with scope, inputs, acceptance checks, and (when applicable) the assigned Dev Team interface and Reference Implementation disposition.

1b. **Moderator decision** — confirm `STEP-XX.md` is clear and complete before briefing the Development Team.

### Phase 2 — Implement

2a. **Moderator → Development Team** — provides the context packet (relevant `PRODUCT.md`, `ARCHITECTURE.md`, `DOMAIN_LANGUAGE.md` excerpts) and the active `STEP-XX.md`. Dev Team restates the step, proposes a plan, and waits for Moderator approval before writing code.

2b. **Development Team** implements the approved scope only and runs the blocking build gate (`{{BUILD_COMMAND}}` + `{{TEST_COMMAND}}`).

### Phase 3 — Review and iterate (repeat until green)

3a. **Tech Lead (Codex)** reviews the diff for architectural fit, naming consistency, scope compliance, and maintainability. Writes `REVIEW.md`. Sends rework directly to Dev Team if needed.

3b. **QA SubAgent** validates against acceptance checks; writes `QA.md`.

3c. **Product Owner SubAgent** confirms acceptance intent; writes sign-off.

3d. **Development Team** addresses each finding explicitly. Return to 3a until green.

### Phase 4 — Accept and advance

4a. **Moderator final gate (HITL)** — confirms all checks pass, `REVIEW.md` and `QA.md` are complete, manually exercises the feature.

4b. **Moderator** creates annotated Git tag and advances `ROADMAP.md`.

---

## Canonical documents

| Document                      | Owner              | Purpose                                                                          |
| ----------------------------- | ------------------ | -------------------------------------------------------------------------------- |
| `MOD-W.md`                    | Moderator          | This file — workflow quick-reference for the project                             |
| `PRODUCT.md`                  | Product Owner      | What is being built, for whom, and why                                           |
| `DESIGN-SPEC.md`              | Designer + Prototyper | Visual identity, components, screens, interactions (v4)                       |
| `ARCHITECTURE-NOTES.md`       | Designer + Prototyper | **Advisory** — observations from prototyping for Tech Lead (v4)               |
| `ARCHITECTURE.md`             | Tech Lead          | Authoritative technical structure, stack, patterns, constraints                  |
| `ROADMAP.md`                  | Tech Lead          | Ordered sequence of small, reviewable steps                                      |
| `STEP-XX.md`                  | Tech Lead          | Current step — goal, scope, inputs, acceptance checks                            |
| `REVIEW.md`                   | Tech Lead          | Review notes and decisions for the current step                                  |
| `QA.md`                       | QA / Tester        | Verification evidence for the current step                                       |
| `DOMAIN_LANGUAGE.md`          | Tech Lead          | Canonical terms used across docs, prompts, and code                              |
| `AI_AGENTS.md`                | Moderator          | Agent registry — models, interfaces, data handling decisions                     |
| `CLAUDE.md` (repo root)       | Tech Lead          | Dev Team config for Claude Code                                                  |
| `AGENTS.md` (repo root)       | Tech Lead          | Tech Lead config for Codex                                                       |

All MOD-W docs live under `mod-w/` in the project. `CLAUDE.md` and `AGENTS.md` live at the **repo root** so the CLI agents read them automatically. The `prototype/` folder (v4) lives at the repo root and is explicitly marked as a research artifact via `prototype/README.md`.

---

## Operating rules

- **Documents must earn their existence.** Prefer updating an existing doc over creating a new one.
- **No hidden scope.** Anything not in the current `STEP-XX.md` is out of scope for this step.
- **Explicit out-of-scope.** When something is deferred, state it.
- **Stable naming.** Resolve naming conflicts early; keep `DOMAIN_LANGUAGE.md` current.
- **Pause on ambiguity.** Any role that is unsure stops and clarifies rather than guessing.
- **Lean first, expand later.** Start with `PRODUCT.md`, `ROADMAP.md`, and `STEP-XX.md`; add further docs only when they clearly help.
- **No retroactive gates.** Work produced outside an approved gate is **reference material only**, never adopted as authoritative without re-running the gate from scratch.
- **Single-role-per-session.** A session is started with exactly one role prompt. Mid-session role switching is prohibited.
- **Architecture is authored by Codex, never by Claude Design.** This is the v4 non-negotiable.

---

MOD-W v4.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
```

### §E.3 — `templates/DESIGN-SPEC.md` (REPLACE — additive)

```markdown
# Design Spec — {{PROJECT_NAME}}

**Date:** {{DATE}}
**Designer:** {{DESIGNER_NAME}}
**Authored in:** {{CLAUDE_DESIGN | CLAUDE_CHATBOT | GEMINI}}
**Prototype:** {{PROTOTYPE_PATH or "n/a"}}

---

## Design Principles

- Clear
- Consistent
- Minimal
- Accessible

---

## 1. Visual Identity

### 1.1 Color Palette

### 1.2 Typography

### 1.3 Spacing & Layout System

### 1.4 Borders, Radius & Elevation

### 1.5 Tone & Personality

---

## 2. Accessibility Baseline

- WCAG AA compliance
- Keyboard navigation required
- Visible focus states

---

## 3. Component Library

> One section per component. For each component document: name (from `DOMAIN_LANGUAGE.md`), one-sentence purpose, states (default / hover / active / disabled / loading / empty / error), variants, and `data-testid` convention.

### 3.x {{COMPONENT_NAME}}

- **Purpose:**
- **States:**
- **Variants:**
- **data-testid:** `{{feature}}-{{component}}-{{element}}-{{modifier?}}`

---

## 4. Screen Layouts

> One section per screen. Document layout structure, components present and their positions, empty / loading / error states, and responsive behaviour (if in scope).

### 4.x {{SCREEN_NAME}}

---

## 5. Interaction Patterns

- Selection / hover / focus
- Keyboard navigation
- Transitions

---

## 6. Component–Step Mapping

| Component | First Step | Notes |
| --------- | ---------- | ----- |
|           | STEP-01    |       |

---

## 7. Domain Language Proposals  *(v4)*

> Terms the prototype surfaced that are NOT in `DOMAIN_LANGUAGE.md`. Each entry is a proposal for the Tech Lead to ratify, modify, or reject during Architecture Definition. Do not treat any term here as canonical.

| Proposed term | Form (type / value / both) | Definition | Rationale | First appearance |
| ------------- | -------------------------- | ---------- | --------- | ---------------- |
|               |                            |            |           |                  |

If no terms proposed, state "None proposed."

---

## 8. Scope Rules

- Only define components required for current or near-term Steps
- Do not design beyond ROADMAP scope
- Each component must map to a Step

---

## 9. UI Scope Rules

- Only implement UI elements in current `STEP-XX.md`
- Future states must not be implemented early
- Design supports incremental delivery

---

## 10. Open Questions

| Question | Owner | Status |
| -------- | ----- | ------ |

---

MOD-W v4.0.0
```

### §E.4 — `templates/STEP-XX.md` (REPLACE — additive)

```markdown
# STEP-XX — {{TITLE}}

---

## Goal

---

## Related Requirements

- R1 —

---

## Assigned Dev Team Interface  *(v4)*

> Moderator decision. Default is Claude Code.

- [ ] Claude Code (default)
- [ ] Claude Design (visual / chart / interaction-heavy Step)

**Hard rule:** if Claude Design is assigned here, it MUST NOT have authored this `STEP-XX.md`. Codex writes the spec; Claude Design implements against it. Plan vs. implement model contrast is preserved.

---

## Scope

---

## Out of Scope

---

## Inputs

- `PRODUCT.md` (R-IDs)
- `ARCHITECTURE.md` (D-IDs)
- Relevant files

---

## Expected File Changes

- src/...

---

## Reference Implementation  *(v4)*

> If a candidate implementation exists in `prototype/`, the Tech Lead dispositions it here. Otherwise, state "None — implement from scratch."

**Location:** `prototype/...` or `n/a`

**Disposition:**

- [ ] Adopt as-is — Dev Team translates verbatim into `src/`
- [ ] Adopt with modifications — see "Required Changes" below
- [ ] Reject — Dev Team implements from scratch per acceptance checks
- [ ] None — no Reference Implementation exists for this Step

### Required Changes (if "Adopt with modifications")

- ...

---

## Acceptance Checks

- [ ] R1 satisfied
- [ ] Tests updated
- [ ] Reference Implementation disposition honoured (if applicable)

---

## Plan

1.
2.
3.

---

## Change Notes

| Date | Change | Reason |
| ---- | ------ | ------ |

---

## Review Notes

---

## QA Notes

---

MOD-W v4.0.0
```

---

## §F — Surgical patches (read first, then patch)

For each patch, read the target file in its current state, locate the anchor, and apply the change. If the anchor text has drifted, report to the Moderator with the actual nearby text and a proposed alternative — do not silently merge.

### §F.1 — `README.md`

**Goal:** add the "Using MOD-W with Claude Design" section; bump version footer to v4.0.0.

**Patch 1 — insert new section.** Locate the section heading exactly:

```
## Using Moderated AI Development Workflow with Kiro
```

**Immediately before** this heading, insert the following block:

````markdown
---

## Using Moderated AI Development Workflow with Claude Design

**Claude Design** is Anthropic's project-scoped design environment. It can edit files, render HTML/JS in a preview pane, capture screenshots, and run scripted browser operations within a single project context — capabilities the Claude chatbot and Claude Code do not share. In MOD-W v4.0.0, Claude Design is the default agent for the **Designer + Prototyper** role.

### Where Claude Design fits

| Role | Interface | Config |
| ---- | --------- | ------ |
| Designer + Prototyper | Claude Design session | `prompts/designer.md` pasted at session start |
| Development Team (visual / chart / interaction Steps, by Moderator assignment) | Claude Design session | `CLAUDE.md` at repo root |

Claude Design does **not** replace Codex (Tech Lead), Claude Code (default Dev Team and QA), Product Owner sessions, or the Moderator.

### Responsibility split

- **Claude Design owns:** the Prototype Ceremony — producing `DESIGN-SPEC.md`, the `prototype/` folder, and `ARCHITECTURE-NOTES.md`. Optionally implementing visual Steps when assigned by the Moderator in `STEP-XX.md`.
- **Codex (Tech Lead) owns:** authoring `ARCHITECTURE.md` after the Architecture Handoff. Codex has authority to override structures implied by the prototype.
- **Claude Code owns:** default Dev Team implementation, QA SubAgent, Product Owner SubAgent validation.
- **MOD-W owns:** Moderator authority at every gate, cross-validation invariants, Step-scoped discipline.

### Prototype Ceremony

The Prototype Ceremony is an **optional kickoff ceremony** added in v4.0.0. Run it when:

- The product has novel interaction models, real-time data, or unusual visual systems
- Design decisions cannot be confidently made from text-only requirements
- Chart, animation, dashboard, or data-visualization work is central
- "Looks right" or "feels right" is part of the acceptance criteria

Skip it for CRUD apps, headless services, and projects where the visual layer is conventional.

The ceremony slots between Product Definition and Architecture Definition:

```
Product Definition  →  PROTOTYPE CEREMONY  →  ARCHITECTURE HANDOFF  →  per-Step lifecycle
                       (Claude Design)        (Codex)
```

Exit criteria: `DESIGN-SPEC.md` approved by Product Owner and Moderator; prototype renders without errors and matches the spec; `ARCHITECTURE-NOTES.md` exists. Full lifecycle: see `docs/prototype-ceremony.md`.

### Architecture Handoff (non-negotiable gate)

After the Prototype Ceremony, the Tech Lead (Codex) consumes the four kickoff inputs — `PRODUCT.md`, `DESIGN-SPEC.md`, `prototype/`, `ARCHITECTURE-NOTES.md` — and **independently authors** `ARCHITECTURE.md`. Codex has explicit authority to disagree with the prototype, reorganize structure, reject domain term proposals, and override `ARCHITECTURE-NOTES.md` observations. Material divergences are recorded in `ARCHITECTURE.md §"Decisions That Diverge From Prototype"`.

**Why this gate is non-negotiable:** the architecture document is the highest-cost failure point in the project — every downstream Step inherits its assumptions. Allowing Claude Design to author it would create sequential same-model outputs, eliminating model contrast at exactly the point where contrast matters most. The Moderator may shorten or skip other v4 ceremonies under time pressure. **The Architecture Handoff may not be skipped.**

Full gate definition: see `docs/architecture-handoff.md`.

### New artifact classes

- **`prototype/`** — research artifact at repo root, produced by Claude Design, explicitly marked non-authoritative via `prototype/README.md` disclaimer. Lives outside `src/` to prevent accidental import.
- **`ARCHITECTURE-NOTES.md`** — advisory input to Architecture Definition, produced by Claude Design, retained in `mod-w/` as historical context.
- **Reference Implementation** — a candidate implementation produced outside the Dev Team role (typically inside `prototype/`). Never auto-promotes. The Tech Lead disposes of it in `STEP-XX.md §"Reference Implementation"` as `Adopt as-is`, `Adopt with modifications`, or `Reject`.

### Claude Design as Development Team (optional per Step)

Claude Design may play the Development Team role for a Step when the Step is visual / chart / interaction-heavy AND the Moderator explicitly assigns it in `STEP-XX.md §"Assigned Dev Team Interface"`. **Hard rule:** Claude Design as Dev Team **may not** also have produced the `STEP-XX.md` spec. Codex writes the spec; Claude Design implements against it. Plan vs. implement model contrast is preserved.

### Bottom line

Claude Design adds a bounded role that captures its unique value (working prototype + design spec in one environment) without compromising MOD-W's core cross-validation guarantee. It is a tool for the kickoff phase and for visual Step implementation. It is not a methodology replacement and not a Tech Lead substitute.

**[See the full Claude Design integration guide](./articles/modw-with-claude-design.md)**

---
````

**Patch 2 — version footer.** Locate the final line:

```
MOD-W v3.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
```

Replace with:

```
MOD-W v4.0.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
```

**Patch 3 — Project Kickoff list.** Locate the v3 kickoff block:

```markdown
**Project Kickoff (once):**
1. **Product Definition** – Moderator iterates with Claude chatbot, Perplexity, and Gemini to produce an approved `PRODUCT.md`.
2. **Architecture Definition** – Moderator iterates with Tech Lead (Codex) to produce approved `ARCHITECTURE.md`, `ROADMAP.md`, `CLAUDE.md`, and `AGENTS.md`.
```

Replace with:

```markdown
**Project Kickoff (once):**
1. **Product Definition** – Moderator iterates with Claude chatbot, Perplexity, and Gemini to produce an approved `PRODUCT.md`.
2. **Prototype Ceremony (optional, v4)** – Moderator iterates with Claude Design (Designer + Prototyper) to produce approved `DESIGN-SPEC.md`, a working `prototype/` folder, and advisory `ARCHITECTURE-NOTES.md`. Run when the product has novel interaction models, real-time data, or unusual visual systems; skip for conventional UI.
3. **Architecture Definition** – Moderator iterates with Tech Lead (Codex) to produce approved `ARCHITECTURE.md`, `ROADMAP.md`, `CLAUDE.md`, and `AGENTS.md`. If the Prototype Ceremony ran, Codex performs the Architecture Handoff: consumes all four kickoff inputs and independently authors the architecture with explicit authority to override prototype-implied structures.
```

Also renumber the **Per-Step Lifecycle** list directly below — its current first item is `3.` and should become `4.`, etc., all the way down to `8.`.

### §F.2 — `docs/roles.md`

**Goal:** add the Designer + Prototyper role definition.

**Patch:** locate the section that defines the Tech Lead role (or, in absence of role-by-role sections, locate the role table near the top). Insert the following block as a new role section, placed between the Product Owner section and the Tech Lead section:

````markdown
## Designer + Prototyper

**Owns:** Visual identity, design specification, working prototype, and advisory architecture observations.
**AI agent (default):** Claude Design.
**Optional role:** This role is **optional per project**. Run the Prototype Ceremony only when the visual / interaction surface justifies it — see `docs/prototype-ceremony.md`.

### Authoritative outputs

- `DESIGN-SPEC.md` — visual identity, components, screens, interactions, data-testid conventions

### Non-authoritative outputs

- `prototype/` folder at repo root — clickable demonstration of the design under realistic conditions
- `ARCHITECTURE-NOTES.md` — advisory input to the Tech Lead's Architecture Definition session

### Authority

The Designer + Prototyper **proposes** — never declares. Specifically:

- Visual decisions in `DESIGN-SPEC.md` become authoritative on Product Owner + Moderator approval.
- Domain term proposals in `DESIGN-SPEC.md §"Domain Language Proposals"` are non-authoritative until the Tech Lead ratifies them in `DOMAIN_LANGUAGE.md`.
- `ARCHITECTURE-NOTES.md` is advisory; the Tech Lead has explicit authority to override any observation when writing `ARCHITECTURE.md`.

### Constraints

The Designer + Prototyper **may not**:

- Author `ARCHITECTURE.md`, `ROADMAP.md`, any `STEP-XX.md`, `REVIEW.md`, `QA.md`, `CLAUDE.md`, or `AGENTS.md`
- Write or modify production code outside the `prototype/` folder
- Declare canonical types, file paths, service boundaries, framework choices, or domain terms

The role prompt is at `prompts/designer.md`.
````

### §F.3 — `docs/lifecycle.md`

**Goal:** insert the Prototype Ceremony and Architecture Handoff into the kickoff sequence.

**Patch:** locate the section describing Project Kickoff (typically titled "Project Kickoff" or "Kickoff Ceremonies"). Wherever the existing v3 sequence shows "Product Definition → Architecture Definition", insert the Prototype Ceremony between them, structured as:

````markdown
### Prototype Ceremony (v4, optional)

Inserted between Product Definition and Architecture Definition when the Moderator decides the product warrants it.

- **Role:** Designer + Prototyper (Claude Design)
- **Inputs:** `PRODUCT.md`, brand assets, reference imagery
- **Outputs:** `DESIGN-SPEC.md` (authoritative), `prototype/` (research artifact), `ARCHITECTURE-NOTES.md` (advisory)
- **Exit gate:** cross-validation pause (Product Owner + Codex pre-review + optional independent Designer) followed by Moderator approval

See `docs/prototype-ceremony.md` for the full lifecycle.

### Architecture Handoff (v4, mandatory if Prototype Ceremony ran)

The Tech Lead (Codex) consumes all four kickoff inputs and independently authors `ARCHITECTURE.md`. Codex has authority to override prototype-implied structures; material divergences are recorded in `ARCHITECTURE.md §"Decisions That Diverge From Prototype"`.

See `docs/architecture-handoff.md` for the full gate.
````

### §F.4 — `docs/artifacts.md`

**Goal:** add the new artifact classes.

**Patch:** locate the artifact catalogue. Append the following entries:

````markdown
### Design + Prototyper artifacts (v4)

- **`DESIGN-SPEC.md`** (in `mod-w/`) — visual identity, component library, screen layouts, interaction patterns, and domain language proposals. Authored by Designer + Prototyper; authoritative on Product Owner + Moderator approval.
- **`ARCHITECTURE-NOTES.md`** (in `mod-w/`) — advisory observations from the Prototype Ceremony for the Tech Lead's consideration during Architecture Definition. **Not authoritative.** Retained for the life of the project as historical context.
- **`prototype/`** (at repo root) — clickable prototype produced during the Prototype Ceremony. **Research artifact, non-authoritative.** Carries a `prototype/README.md` stating the disclaimer. Frozen after Architecture Handoff.

### Reference Implementation (v4, concept — not a file)

A **Reference Implementation** is a candidate implementation produced outside the Development Team role — typically inside `prototype/`. It does **not** auto-promote to production. The Tech Lead disposes of it in `STEP-XX.md §"Reference Implementation"` as `Adopt as-is`, `Adopt with modifications`, or `Reject`.
````

### §F.5 — `docs/ceremonies.md` (if present)

**Goal:** add a pointer to the Prototype Ceremony.

**Patch:** locate the section listing the kickoff ceremonies. After the **Architecture Definition** entry (or wherever architecture-related ceremonies live), insert:

````markdown
### Prototype Ceremony (v4, optional)

Slots between Product Definition and Architecture Definition. Produces `DESIGN-SPEC.md`, a working `prototype/` folder, and advisory `ARCHITECTURE-NOTES.md`. Run when the product has novel interaction models, real-time data, or unusual visual systems; skip for conventional UI.

See `docs/prototype-ceremony.md` for the full lifecycle.

### Architecture Handoff (v4, mandatory if Prototype Ceremony ran)

The Tech Lead (Codex) consumes all four kickoff inputs and independently authors `ARCHITECTURE.md` with authority to override prototype-implied structures.

See `docs/architecture-handoff.md` for the full gate.
````

If `docs/ceremonies.md` does not exist in the repo, skip this patch — the same content is reachable via `docs/prototype-ceremony.md` and `docs/architecture-handoff.md` directly.

### §F.6 — `prompts/tech-lead.md`

**Goal:** acknowledge the Architecture Handoff and the Designer + Prototyper handoff inputs.

**Patch:** locate the section titled **"Planning Session"** (it currently lists the 5 steps: read PRODUCT/ARCHITECTURE, write ARCHITECTURE, write ROADMAP, write STEP-XX, generate CLAUDE/AGENTS).

Replace step 1 of the Planning Session list:

```
1. Read `PRODUCT.md` and existing `ARCHITECTURE.md` (if present).
```

with:

```
1. Read `PRODUCT.md` and, **if the Prototype Ceremony ran** (v4), also read `mod-w/DESIGN-SPEC.md`, `prototype/`, and `mod-w/ARCHITECTURE-NOTES.md`. All four are inputs to the Architecture Handoff (`docs/architecture-handoff.md`). Read existing `ARCHITECTURE.md` if present.
```

Then **append** to the Planning Session list (after step 5):

```
6. **Architecture Handoff (v4, if Prototype Ceremony ran).** When authoring `ARCHITECTURE.md` from prototype inputs, you have explicit authority to override structures implied by the prototype. Record any material divergence in `ARCHITECTURE.md §"Decisions That Diverge From Prototype"` with rationale. `ARCHITECTURE-NOTES.md` is advisory input, not constraint.
7. **Domain Language ratification (v4).** When the prototype proposed terms in `DESIGN-SPEC.md §"Domain Language Proposals"`, ratify, modify, or reject each in `DOMAIN_LANGUAGE.md` with a one-line rationale per term.
```

### §F.7 — `prompts/development-team-claude.md`

**Goal:** note Claude Design as an alternate Dev Team interface for visual Steps.

**Patch:** locate the opening blockquote — it currently reads roughly:

```
> This prompt is the basis for the `CLAUDE.md` file placed at the repo root.
> It configures the **Development Team** Claude Code session: one approved Step at a time, under human moderation.
```

Replace with:

```
> This prompt is the basis for the `CLAUDE.md` file placed at the repo root.
> It configures the **Development Team** session: one approved Step at a time, under human moderation.
>
> **Default interface:** Claude Code (CLI).
> **Alternate interface (v4):** Claude Design — used when the Moderator assigns a visual / chart / interaction-heavy Step to Claude Design in `STEP-XX.md §"Assigned Dev Team Interface"`. The role rules are identical; only the interface differs.
>
> **Hard rule (v4):** when Claude Design plays Dev Team, it MUST NOT have authored the Step's `STEP-XX.md`. Codex writes the spec; Claude Design implements against it. Plan vs. implement model contrast is preserved.
```

---

## §G — Verification checklist

After applying all changes, the Claude session reports on each:

| # | Check | Result |
|---|---|---|
| 1 | All 9 new/replacement files in §D and §E exist at the documented paths | |
| 2 | Every file footer reads `MOD-W v4.0.0` (or the convention used in the repo for the methodology versioning) | |
| 3 | `README.md` contains the "Using Moderated AI Development Workflow with Claude Design" section, placed before the Kiro section | |
| 4 | `README.md` Project Kickoff list now has three items (Product Definition → Prototype Ceremony → Architecture Definition); Per-Step Lifecycle numbering starts at 4 | |
| 5 | `docs/roles.md` contains a Designer + Prototyper section between Product Owner and Tech Lead | |
| 6 | `docs/lifecycle.md` mentions the Prototype Ceremony and Architecture Handoff | |
| 7 | `docs/artifacts.md` mentions `DESIGN-SPEC.md`, `ARCHITECTURE-NOTES.md`, `prototype/`, and Reference Implementation | |
| 8 | `prompts/tech-lead.md` references the Architecture Handoff and Domain Language ratification | |
| 9 | `prompts/development-team-claude.md` references Claude Design as an alternate Dev Team interface | |
| 10 | No file outside §C "File inventory" has been modified | |
| 11 | No file references a path that doesn't exist | |
| 12 | A grep for `MOD-W v3.0.0` returns only intentional historical references | |

Report each row as ✓ / ✗ / N/A with a one-line note. Do not commit.

---

## §H — Open questions deferred to v4.1.0

These were surfaced during v4 design and are intentionally **not** resolved in v4.0.0. Track in the repo's issue tracker; address in a follow-up release if usage warrants.

| ID | Question | Default behaviour in v4.0.0 |
|---|---|---|
| Q1 | Should `ARCHITECTURE-NOTES.md` be archived after Architecture Definition, or retained indefinitely? | Retained. |
| Q2 | Can Codex author Reference Implementations during Architecture Definition, or only Claude Design during Prototype Ceremony? | Only Claude Design. Codex's job is to specify, not to demonstrate. |
| Q3 | Does the Prototype Ceremony need its own `PROTOTYPE-REVIEW.md`, or fold into `REVIEW.md`? | Fold into `REVIEW.md §"Prototype Ceremony"`. |
| Q4 | When Claude Design plays Dev Team, does it run QA SubAgent itself, or Claude Code runs QA externally? | Claude Code runs QA externally — preserves model contrast on the verification axis. |
| Q5 | Single `prompts/designer.md` covering both Claude Design and Claude chatbot / Gemini, or split into `designer.md` + `prototyper.md`? | Single file. The chatbot / Gemini variant produces only `DESIGN-SPEC.md`. |

---

## §I — Migration notes for existing projects

v3 projects are forward-compatible without modification. v4 adds new ceremonies and a new role; it does not change v3 ceremonies or invalidate v3 artifacts.

Migration is opt-in per project:

1. Decide per project whether the Prototype Ceremony is warranted (see `docs/prototype-ceremony.md` § "When to run").
2. If yes, run the ceremony before the next Architecture revision.
3. If no, continue with v3 lifecycle unchanged.

For projects already past kickoff:

- Retroactive Prototype Ceremony is permitted as documentation backfill — produce `DESIGN-SPEC.md` and `ARCHITECTURE-NOTES.md` from existing prototype work.
- The Architecture Handoff must be run explicitly: Codex receives the backfilled artifacts and produces an authoritative `ARCHITECTURE.md` from scratch.
- Existing Steps are subject to retroactive Tech Lead Review or re-implementation per the "no retroactive gates" rule.

---

## §J — Cross-validation invariants (verify each is preserved)

These cannot be relaxed in v4 under any circumstance. The Claude session applying this release must verify each is intact in the final output:

| Invariant | Where to verify |
|---|---|
| Tech Lead is always Codex | `templates/MOD-W.md` Roles table; `prompts/tech-lead.md` opening |
| Dev Team is never the same model as Tech Lead for the same Step | `templates/STEP-XX.md §"Assigned Dev Team Interface"` hard rule |
| Moderator is always human | `templates/MOD-W.md` Roles table |
| `ARCHITECTURE.md` is authored by Codex, never by Claude Design | `templates/MOD-W.md` Operating rules; `docs/architecture-handoff.md` |
| Every Step passes a Codex review before QA | `templates/MOD-W.md` Phase 3 |
| Every Step passes a Moderator final gate before tag + ROADMAP advance | `templates/MOD-W.md` Phase 4 |
| Single-role-per-session | `templates/MOD-W.md` Operating rules; `prompts/designer.md` environment self-identification |
| No retroactive gates | `templates/MOD-W.md` Operating rules |

If any invariant cannot be verified in the final output, the release is incomplete — surface to the Moderator and do not commit.

---

## §K — End of release implementation package

When all sections of this document have been applied, verified, and the verification checklist is green:

1. Surface the full diff to the Moderator.
2. Do NOT commit, tag, or push.
3. Wait for Moderator approval.

On approval, the Moderator creates the annotated Git tag `v4.0.0` and pushes.

---

MOD-W v4.0.0 release implementation package · authored 2026-05-23 by Claude Design (Designer + Prototyper) as a Reference Implementation
