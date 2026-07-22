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

Codex writes `ARCHITECTURE.md`, `ROADMAP.md`, `CLAUDE.md`, `AGENTS.md`, and `STEP-01.md`. Updates `DOMAIN_LANGUAGE.md` based on `DESIGN-SPEC.md §"Domain Language Proposals"`, accepting / modifying / rejecting each proposal with a one-line rationale per term.

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
