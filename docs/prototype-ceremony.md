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
